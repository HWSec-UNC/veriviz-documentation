# All about Deployment

Veriviz utilizes [UNC Cloud Apps](https://cloudapps.unc.edu/) to host and deploy the service. UNC Cloud Apps runs on OKD(OpenShift Kubernetes Distribution). 

## What is Kubernetes?

ON a high level, Kubernetes is a service that allows your application to be run in a virtual enviroment with its own operating system. You can think of it as what a container is to Docker on your local machine, that's essentially what a pod is on a Kubernetes deployment. This is defined by a Dockerfile in your project which OKD uses to create your pod and which your code is processed in run on.

## How does deploying on Kubvernetes work

The OKD Deployment process works as follow:

1. Being notified of CI successfully passing all tests on main and receiving a webhook callback
2. A BuildConfig begins a new Build by pulling repository and building a Docker image
3. The Docker image is pushed to an ImageStream
4. The ImageStream notifies a Deployment that a new image is available
5. The Deployment spins up a new Pod (Container) based on the image
6. Once the new Pod is available, it turns off the old Pod running the previous version

*Credit to Kris Jordan and his [website](https://comp423-25s.github.io/resources/backend-architecture/3-ci-cd/#why-cicd-matters) for this information*

## Continous Inegration, Continous Deployment

CI/CD(Continous Integration/Continous Deployment) refers to the automatied process of re-deploying a service when new changes are made. 

- **Continous Integration** refers to the process of verifying tests are passed ebfore deployment. So for example, after a commit to main is made, Tests you write will be automatically run on your new code. If these tests pass, great! they will now be handed over to continous deployement and if not, your project will not be re-deployed and you will have to iterate on your code until they pass.

- The second step of CI/CD **Continous Deployment**. This referrs to the process of automitcally redploying your service to reflect the changes you made to it. In a full CI/CD pipeline, once your project has passed the tests, it is then deployed. 

**In Veriviz**, **Continous INtegration** is **NOT** used. This meand once new changes are refelected in the main branch, it will be redployed to OKD, rebuilt, and up and running. There are no tests to verify your work. This can be added in the future but is not nessarily needed. What this means in a nutshell is, when you make changes to the verviz repo or any of the other services such as SEIF or Sylvia, the changes will automitically be reflected in the service with no need for manual deployment but also, no tests will verify what you did is correct. Don't worry though, if your code results in a failed deployment, OKD will revert to the last built pod and the service will still run on the old code.


