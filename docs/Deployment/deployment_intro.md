# All about Deployment

Veriviz utilizes [UNC Cloud Apps](https://cloudapps.unc.edu/) to host and deploy the service. UNC Cloud Apps runs on OKD (OpenShift Kubernetes Distribution). 

---

## What is Kubernetes?

On a high level, Kubernetes is a service that allows your application to be run in a virtual environment with its own operating system. You can think of it as what a container is to Docker on your local machine — that's essentially what a pod is on a Kubernetes deployment. This is defined by a Dockerfile in your project which OKD uses to create your pod, and in which your code is processed and run.

---

## How does deploying on Kubernetes work

The OKD Deployment process works as follows:

1. Being notified of CI successfully passing all tests on main and receiving a webhook callback  
2. A BuildConfig begins a new Build by pulling the repository and building a Docker image  
3. The Docker image is pushed to an ImageStream  
4. The ImageStream notifies a Deployment that a new image is available  
5. The Deployment spins up a new Pod (Container) based on the image  
6. Once the new Pod is available, it turns off the old Pod running the previous version

*Credit to Kris Jordan and his [website](https://comp423-25s.github.io/resources/backend-architecture/3-ci-cd/#why-cicd-matters) for this information*

---

## Continuous Integration, Continuous Deployment

CI/CD (Continuous Integration/Continuous Deployment) refers to the automated process of redeploying a service when new changes are made.

- **Continuous Integration** refers to the process of verifying tests are passed before deployment. So for example, after a commit to main is made, tests you write will be automatically run on your new code. If these tests pass, great! They will now be handed over to continuous deployment; if not, your project will not be redeployed and you will have to iterate on your code until they pass.

- The second step of CI/CD is **Continuous Deployment**. This refers to the process of automatically redeploying your service to reflect the changes you made to it. In a full CI/CD pipeline, once your project has passed the tests, it is then deployed.

**In Veriviz, Continuous Integration is NOT used.** This means once new changes are reflected in the main branch, it will be redeployed to OKD, rebuilt, and up and running. **There are no tests to verify your work.** This can be added in the future but is not necessarily needed. Don’t worry, if your code results in a failed deployment, OKD will revert to the last built pod and the service will still run on the old code. Keep in mind, bugs that do not result in a failed deployment will still be there.

