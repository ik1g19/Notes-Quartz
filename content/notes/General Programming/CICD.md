[🔗Link](https://martinfowler.com/bliki/ContinuousDelivery.html)

Continuous Delivery is a software development discipline where you build software in such a way that the software can be released to production at any time

Continuous delivery is when:
- Your software is deployable throughout its lifecycle
- Your team prioritizes keeping the software deployable over working on new features
- Anybody can get fast, automated feedback on the production readiness of their systems any time somebody makes a change to them
- You can perform push-button deployments of any version of the software to any environment on demand

A business sponsor could request that the current development version of the software can be deployed into production at a moment's notice

_Continuous Delivery_ is sometimes confused with **Continuous Deployment**

**Continuous Deployment** means that every change goes through the pipeline and automatically gets put into production, resulting in many production deployments every day
- _Continuous Delivery_ just means that you are able to do frequent deployments but may choose not to do it

# Continuous Integration

[🔗Link](https://www.techtarget.com/searchsoftwarequality/CI-CD-pipelines-explained-Everything-you-need-to-know)

_Continuous Integration_ usually refers to integrating, building, and testing code within the development environment

Changes are automatically built into artifacts and subjected to automated tests

CI relies on automation tools to create builds and perform initial tests, like sniff tests or unit tests

A key feature of CI is rapid feedback: developers and managers can quickly see the outcomes of the team’s work

Because changes are small and incremental, bugs are easier to identify, fix, and manage

CI process ends when a build passes its initial tests and is ready for more in-depth testing, such as user acceptance testing
- If a build fails, it goes back for bug fixes or adjustments, and the cycle repeats until success

Each developer works on a branch of the codebase, representing a unique version of the project
- Once a branch is successfully built and tested, it is merged back into the main codebase, which is then updated with a new version number

Before a build moves to staging or deployment, final steps might include packaging it into a deployable image, such as a Docker container, a VM image, or another format

![[Images/itops-cicd_pipeline.png]]

![[Images/software_quality-continuous_delivery_process-f.png]]

# Deployment Pipeline

One of the challenges of an automated build and test environment is you want your build to be fast, so that you can get fast feedback, but comprehensive tests take a long time to run. A deployment pipeline is a way to deal with this by breaking up your build into stages

Usually the first stage of a deployment pipeline will do any compilation and provide binaries for later stages

Later stages may include manual checks, such as any tests that can't be automated

Broadly the deployment pipeline's job is to detect any changes that will lead to problems in production
- Performance, security, or usability issues