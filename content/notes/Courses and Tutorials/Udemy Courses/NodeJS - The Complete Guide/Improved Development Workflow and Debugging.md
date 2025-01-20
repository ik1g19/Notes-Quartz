#udemy-course #npm #node-js

# Improved Development Workflow and Debugging

## Understanding NPM Scripts

You can create a `package.json` using `npm` so that you can run your program with just `npm start` 
## Installing 3rd Party Packages

Packages are installed from the npm repository with npm

We can indicate a dependency is a development dependency by appending `--save-dev` to the end

The `package-lock.json` contains the version information about the exact versions of the dependencies installed, in case the project is shared with others who also need to download the dependencies

## Using Nodemon for Autorestarts

Nodemon is a utility package that will watch our files for changes and restart our process if we make changes

## Global and Local npm Packages

The benefit of local dependencies is that you can share projects without the `node_modules` folder and you can run `npm install` in a project to re-create that node_modules folder

You could install a package globally with the `-g` flag