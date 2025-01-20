>[!INFO]
>A Workflow Automation Service by GitHub

![[Images/Pasted image 20241224105442.png]]
**Workflows**
- Contain one or more **Jobs**
- Triggered upon **Events**

**Jobs**
- Defines a **Runner** (Execution Environment)
	- Machine and Operating System used for executing its steps
- Contain one or more **Steps**
	- Run in parallel, by default, or sequential
	- Can be conditional

**Steps**
- Execute a shell script or an **Action**
- Can use custom or third-party actions
- Steps are executed in order
- Can be conditional

# Creating a First Workflow

Go to **Actions** tab to create and view **Actions**

You can pick workflow templates here

Give a workflow a name using

```
name: First Workflow
```

Use `on` to list the events that should trigger this workflow to run

```
on: workflow_dispatch
```

`workflow_dispatch` is an event that will wait for the user to manually start a workflow

We use `jobs` to define the work that should be done
- Jobs are listed indented below `jobs`

The first thing we list in a `job` is the **Runner**

The **Runners** are pre-defined by GitHub and you can look up the specifications

Next you define a list of **Steps**
- Provide a *name* for the **Step** and a *shell command* to be executed

```yml
name: First Workflow
on: workflow_dispatch
jobs:
	first-job:
		runs-on: ubuntu-latest
		steps:
			- name: Print greeting
			  run: echo "Hello World!"
		    - name: Print goodbye
		      run: echo "Done - bye!"
```

# Running the First Workflow

Workflows are defined inside `.github/workflows`

Click the **Actions** tab and **First Workflow**, from there you can run it

Click the workflow to see **Jobs** and **Steps** that were run

# Running Multi-Line Shell Commands

If you need to run multiple shell commands, you can easily do so by adding the pipe symbol (`|`) as a value after the `run:` key.

Like this:

```yml
...
run: |
   echo "First output"
   echo "Second output"
```

# Events

![[Images/Pasted image 20241224120730.png]]

# Actions

![[Images/Pasted image 20241224121119.png]]

You can browse GitHub Actions on the marketplace

Use `uses` instead of `run`, for an **Action**

Use the identifier of the **Action** after `uses`, the identifier can be found on the marketplace
- Make sure to use specify a version e.g. `actions/checkout@v3`
- Use `with` to specify options for the **Action**

>[!INFO]
>The GitHub Action `checkout` is used to check out your repository code into the workflow's runner environment. This allows subsequent workflow steps to access and work with the repository's files

### Key Features

1. **Fetches Code**: Downloads your repository's code to the runner's environment
2. **Branches and Commits**: You can specify a branch, tag, or commit to check out
3. **Submodules**: Can optionally handle Git submodules
4. **Sparse Checkout**: Allows partial checkout of specific paths for efficiency
5. **Authentication**: Uses GitHub's token to authenticate and fetch the repository

Some **Runners** already have NodeJS installed

# Permissions

Personal Access Tokens need Workflow Permissions if the code being committed will create or edit workflows

# Parallel vs Sequential Jobs

Jobs defined in a workflow by default run parallel

Sometimes you want sequential jobs
- e.g. You do not want deploy to run if tests have failed

Use `needs` to define what jobs a job needs to wait for

![[Images/Pasted image 20241224142035.png]]

# Use Multiple Triggers

```yml
on: [push, workflow_dispatch]
```

# Context Objects

GitHub Actions creates meta information that is passed into jobs and steps called **Context**
- Information about the event trigger, runner etc.

To output data from GitHub use `${{ github }}`

Use `toJSON()` to make it readable

```yml
run: echo "${{ toJSON(github) }}"
```

# Event Filters & Activity Types

![[Images/Pasted image 20241224144503.png]]

To use **Activity Types**, list indented activities

```yml
on:
	pull_request:
		types:
			- opened
	workflow_dispatch:
```

Use **Event Filters** to catch events with specific conditions

## Branch Filter

```yml
on:
	push:
		branches:
			- main # main
			- 'dev-*' # dev-new dev-this-is-new etc...
			- 'feat/**' # feat/new feat/new/button etc...
```

## Paths Filter

```yml
on:
	push:
		paths-ignore:
			- '.github/workflows/*' 
# only triggered if files under .github/workflows are untouched
```

## Forks & Pull Request Events

![[Images/Pasted image 20250102112736.png|400]]

# Cancel & Skipping Workflows

![[Images/Pasted image 20250102113018.png]]

Workflows that would otherwise be triggered using `on: push` or `on: pull_request` won't be triggered if you add any of the following strings to the commit message in a push, or the `HEAD` commit of a pull request:
- `[skip ci]`
- `[ci skip]`
- `[no ci]`
- `[skip actions]`
- `[actions skip]`

# Job Artifacts

![[Images/Pasted image 20250102113827.png]]

## Uploading Artifacts

Stores the specified artifact

```yml
build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install dependencies
        run: npm ci
      - name: Build website
        run: npm run build
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: dist-files
          path: dist
```

## Download Artifacts

Build and deploy workflows will be run on different VMs

So need to download built artifact onto new VM

```yml
deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Get build artifacts
        uses: actions/download-artifact@v3
        with:
          name: dist-files
      - name: Deploy
        run: echo "Deploying..."

```

# Understanding Job Outputs

![[Images/Pasted image 20250102122736.png]]

Output is saved as a key-value pair, in this case the name used is `script-file`

```yml
build:
    needs: test
    runs-on: ubuntu-latest
    outputs:
      script-file: ${{ steps.publish.outputs.script-file }}
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install dependencies
        run: npm ci
      - name: Build website
        run: npm run build
      - name: Publish JS filename
        id: publish
        run: find dist/assets/*.js -type f -execdir echo 'script-file={}' >> $GITHUB_OUTPUT ';'
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: dist-files
          path: dist
```

## Using Job Outputs

```yml
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Get build artifacts
        uses: actions/download-artifact@v3
        with:
          name: dist-files
      - name: Output filename
        run: echo "${{ needs.build.outputs.script-file }}"
      - name: Deploy
        run: echo "Deploying..."
```

`needs` is the GitHub context object for jobs that are dependencies of the current job

`build` is the name of the Job we passed the value out of earlier

`script-file` was the key

# Dependency Caching

Redownloading dependencies or repeatedly downloading the same files onto VMs can be time consuming

You can cache common dependencies to save workflow time

```yml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Cache dependencies
        uses: actions/cache@v3
        with:
          path: ~/.npm
          key: deps-node-modules-${{ hashFiles('**/package-lock.json') }}
      - name: Install dependencies
        run: npm ci
      - name: Lint code
        run: npm run lint
      - name: Test code
        run: npm run test
```

Cache dependencies with a unique hash in the name
- By hashing the dependency file, when dependencies are changed, they will be cached to a different file

# Environment Variables & Secrets

You can define environment variables at workflow and job level

```yml
name: Deployment
on:
  push:
    branches:
      - main
      - dev
env:
  MONGO_DB_NAME: gha-demo
jobs:
  test:
    env:
      MONGODB_CLUSTER_ADDRESS:
      MONGODB_USERNAME:
      MONGODB_PASSWORD:
    environment: testing
    runs-on: ubuntu-latest
```

## Creating a Database and Using Database Environment Variables

Example uses a cloud database hosted with MongoDB atlas

![[Images/Pasted image 20250102152927.png]]

![[Images/Pasted image 20250102153225.png]]

You also need to allow network access from anywhere so you can use it from your GitHub runners

```yml
jobs:
  test:
    env:
      MONGODB_CLUSTER_ADDRESS: cluster0.mgene.mongodb.net
      MONGODB_USERNAME: isaacklugman
      MONGODB_PASSWORD: HMYtCgCXRGs5toRy
      PORT: 8080
```

## Using Environment Variables in Code and Workflows

Job environment variables are accessed using `${{ env.MONGODB_USERNAME }}`

Workflow environment variables are accessed using the OS environment syntax
- e.g. `$MONGODB_DB_NAME`

## Secrets

![[Images/Pasted image 20250102160819.png]]

Secrets are stored on repository level

Then can be accessed with `secrets` context object

# Repository Environments

Provides different environments for storing different environment variables with the same name

To reference the environment

```yml
jobs:
	test:
		environment: testing
```

# Special Conditional Functions

![[Images/Pasted image 20250103104331.png]]

# Conditional Jobs

```yml
  report:
    needs: [lint, deploy]
    if: failure()
    runs-on: ubuntu-latest
    steps:
      - name: Output information
        run: |
          echo "Something went wrong"
          echo "${{ github }}"
```

By default a new job would run in parallel and `failure()` would only check the jobs behind it for failure

By using `needs` we can put a failure checking jobs in series with the others so that it will wait for them to finish/potentially fail

Ignore errors with the `continute-on-error` field

# Matrix Strategies

Running matrix strategies will run all possible combinations of the lists provided

```yml
name: Matrix Demo
on: push
jobs:
    build:
        continue-on-error: true
        strategy:
            matrix:
                node-version: [12, 14, 16]
                operating-system: [ubuntu-latest, windows-latest]
        runs-on: ${{ matrix.operating-system }}
        steps:
            - name: Get Code
              uses: actions/checkout@v3
            - name: Install NodeJS
              uses: actions/setup-node@v3
              with:
                node-version: ${{ matrix.node-version }}
            - name: Install Dependencies
              run: npm ci
            - name: Build Project
              run: npm run build
```

Use `include` and `exclude` to add or remove standalone combinations

```yml
matrix:
	node-version: [12, 14, 16]
	operating-system: [ubuntu-latest, windows-latest]
	include:
		- node-version: 18
		  operating-system: ubuntu-latest
	exclude:
		- node-version: 12
		  operating-system: windows-latest
```

# Reusable Workflows

![[Images/Pasted image 20250103114326.png]]

Use trigger `on: workflow_call` to make a workflow reusable

Then, to use it:

```yml
deploy:
	needs: build
	uses: ./.github/workflows/reusable.yml
```

## Adding Inputs

```yml
name: Reusable Deploy
on: 
    workflow_call:
        inputs:
            artifact-name:
                description: The name of the deployable artifact files
                required: false
                default: dist
                type: string
```

```yml
deploy:
    needs: build
    uses: ./.github/workflows/reusable.yml
    with:
      artifact-name: dist-file
```

## Using Secrets in Reusable Workflows

```yml
name: Reusable Deploy
on: 
    workflow_call:
        inputs:
            artifact-name:
                description: The name of the deployable artifact files
                required: false
                default: dist
                type: string
        secrets:
            some-secret:
                required: false
```


```yml
deploy:
    needs: build
    uses: ./.github/workflows/reusable.yml
    with:
      artifact-name: dist-file
    secrets:
      some-secret: ${{ secrets.some-secret }}
```

## Outputs

[🔗Commit Example](https://github.com/ik1g19/GitHub-Controlling-Workflow/commit/a316c45d9f7c4282a8c72bdadfeef4b75dbfccfe)

# Containers

![[Images/Pasted image 20250103151643.png|300]]

![[Images/Pasted image 20250103152005.png]]