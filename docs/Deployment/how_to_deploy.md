# Veriviz Continuous Deployment Setup Guide

Welcome to **Veriviz**! This guide will walk you through **adding a new service** to Veriviz and setting up Continuous Deployment (CD) on UNC’s OKD platform. By the end, you’ll have an automated pipeline that builds and deploys your new service whenever you push to `main`.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Create or Update Your Dockerfile](#step-1-create-or-update-your-dockerfile)
3. [Step 2: Set Up an OKD Project](#step-2-set-up-an-okd-project)
4. [Step 3: Deploy the Service Manually Once](#step-3-deploy-the-service-manually-once)
5. [Step 4: Expose a Route (Optional)](#step-4-expose-a-route-optional)
6. [Step 5: Create a Build Webhook Secret in OKD](#step-5-create-a-build-webhook-secret-in-okd)
7. [Step 6: Add the Webhook to GitHub Secrets](#step-6-add-the-webhook-to-github-secrets)
8. [Step 7: Configure GitHub Actions](#step-7-configure-github-actions)
9. [Step 8: Commit and Merge](#step-8-commit-and-merge)
10. [Step 9: Verify Your Deployment](#step-9-verify-your-deployment)
11. [Optional: Adding Secrets (.env) to the Deployment](#optional-adding-secrets-env-to-the-deployment)
12. [Tips and Extras](#tips-and-extras)

---

## Prerequisites

- You have **GitHub** access to the Veriviz repository (public or private).
- You have **OKD/CloudApps** access at UNC (make sure you can log in and select your project).
- You have a **Dockerfile** for your new service or can create one.
- You know the name of your new service, e.g. `veriviz-newservice`.

---

## Step 1: Create or Update Your Dockerfile

1. Place a `Dockerfile` in your service’s directory, e.g., `newservice/Dockerfile`.
2. Example (Node/Express):
   ```dockerfile
   FROM node:20

   WORKDIR /usr/src/app

   COPY package*.json ./
   RUN npm install

   COPY . .

   EXPOSE 8000

   CMD [\"node\", \"server.js\"]
   ```
  3. Adjust as needed for your framework (Python, Go, etc.).

---

## Step 2: Set Up an OKD Project

Log into OKD (UNC’s CloudApps). **NOTE:** You *Must* be using eduroam wifi or the UNC VPN to be able to login on your CLI and on the cloudapps website. Learn more about the VPN [here](https://ccinfo.unc.edu/start-here/secure-access-on-and-off-campus/).

1. Navigate to [https://cloudapps.unc.edu/](https://cloudapps.unc.edu/) and sign in
2. Click on your ONYEN in the upper-right of the console and click `Copy Login Command`
3. Click `Display Token` and copy the `Login in with this token` token which should look like `oc login --token=<YOUR_TOKEN> --server=https://api.apps.unc.edu:6443`
4. Open up your project in its devcontainer making sure the OKD CLI is installed in the dev container
(you can check this by running `oc version`)
5. Log in with the follwoing commands and using your token you copied
  ``` {.yaml .copy}
  oc login --token=<YOUR_TOKEN> --server=https://api.apps.unc.edu:6443
  oc project <YOUR_PROJECT_NAME>
  ```
6. Confirm with `oc status`

---

## Step 3: Deploy the Service Manually Once

This will create a BuildConfig, ImageStream, and Deployment for your new service:
``` {.yaml .copy}
oc new-app https://github.com/<user>/<repo>.git#main \
  --context-dir=newservice \
  --name=veriviz-newservice \
  --strategy=docker \
  --labels=app=veriviz-newservice
```

- `--context-dir=newservice`: Tells OKD to use your newservice folder with the Dockerfile inside. Exmaple for veriviz is `frontend`.

- `--name=veriviz-newservice`: The name for your build & deployment.

Check the status:
```{.yaml .copy}
oc logs -f buildconfig/veriviz-newservice
```
!!! note "For Private Repositories"
    If you repository is private, follow [these instructions](#what-if-my-repository-is-private) instead of Step 3. **Only replace the step 3 instructions with these**. Steps 1-2 and 4-12 stay the same. 
---

## Step 4: Expose a Route (Optional)

If your service needs to be accessible outside of OKD (e.g. from a frontend or public internet):

``` {.yaml .copy}
oc create route edge --service=veriviz-newservice --insecure-policy=Redirect
oc get route veriviz-newservice
```
You’ll see the URL for your service.

!!! note
    If this service is internal-only, you can skip creating a route.

---

## Step 5: Create a Build Webhook Secret in OKD

You want GitHub to trigger builds on pushes/merges. First, find your webhook URL:

``` {.yaml .copy}
oc describe bc/veriviz-newservice | grep -C 1 generic
oc get bc veriviz-newservice -o yaml | grep -C 1 generic
```
You’ll see something like:
```
https://api.apps.unc.edu:6443/apis/build.openshift.io/v1/namespaces/<namespace>/buildconfigs/veriviz-newservice/webhooks/<secret>/generic
```
**Copy that URL.**

---

## Step 6: Add the Webhook to GitHub Secrets

1. Go to your **GitHub Repo → Settings → Secrets and variables → Actions**
2. **New Repository Secret:**
  - **Name**: `CD_BUILD_WEBHOOK_VERIVIZ_NEWSERVICE`
  - **Value**: (paste the full webhook URL)
!!! note "Name"
    The name can be anything you want, but make it descirptive in case you dpeloy multiple services form one repo.

---

## Step 7: Configure GitHub Actions

Create or edit your `.github/workflows/cicd.yml`. For example:

``` {.yaml .copy}
name: Veriviz CI/CD Pipeline

on:
  push:
    branches: [ main ]

jobs:
  cd-veriviz-newservice:
    name: \"Continuous Deployment - veriviz-newservice\"
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Trigger OKD Build
        run: |
          curl -X POST ${{ secrets.CD_BUILD_WEBHOOK_VERIVIZ_NEWSERVICE }}
          
```

---

## Step 8: Commit and Merge

1. Create a new branch, e.g. `feature/newservice-cd`.
2. Push and open a Pull Request.
3. Once merged into `main`, GitHub Actions will:
  - Run the pipeline
  - Hit the OKD webhook
  - Trigger a new build & deploy
!!! note
    Alternatively, you can also push directly to the main branch to achieve the same result.

---

## Step 9: Verify Your Deployment
- **Check OKD builds:**
  ``` {.yaml .copy}
  oc get builds
  oc logs -f bc/veriviz-newservice

  ```
- **Check the service:**
  ``` {.yaml .copy}
  oc get pods
  oc logs deployment/veriviz-newservice
  ```
- **Check the route (if exposed):**
  ``` {.yaml .copy}
  oc get route veriviz-newservice
  ```
Confirm you can hit it in the browser.

---

## Optional: Adding Secrets (.env) to the Deployment

If your new service requires environment variables:

1. Create a .env in newservice/.env (don’t commit to GitHub).
2. In your dev container:
  ``` {.yaml .copy}
  oc create secret generic veriviz-newservice-env --from-env-file=newservice/.env
  oc set env deployment/veriviz-newservice --from=secret/veriviz-newservice-env
  ```
replacing `veriviz-newservice-env` with the name you want for your secret.
3. On redeploy, your app can read the environment variables inside the container.

---

## Tips and Extras

### **How do I manually rebuild without deleting everything?**

Use:
``` {.yaml .copy}
oc start-build veriviz-newservice
```
Or trigger the webhook again:

``` {.yaml .copy}
curl -X POST <your-webhook-URL>
```

### **What if I want to rename or delete the service?**

``` {.yaml .copy}
oc delete all -l app=veriviz-newservice
```
This removes the BuildConfig, Deployment, Route, and Service labeled `app=veriviz-newservice`.

### **What if my repository is private?**

If Your Repository Is private, then OKD won’t be able to automatically clone it unless you give it credentials. Here’s how:

1. Generate a GitHub Personal Access Token (classic) with repo read permissions.
  - Go to your **github profile -> Developer Settings -> Personal access tokens -> Tokens(Classics)** and copy the PAT after creation
2. Create a secret in OKD:
  ```{.yaml .copy}
  oc create secret generic veriviz-newservice-pat \
    --from-literal=username=<GITHUB_USERNAME> \
    --from-literal=password=<YOUR_PAT>
  ```
3. Label the secret so OKD can find it:
  ``` {.yaml .copy}
  oc label secret veriviz-newservice-pat app=veriviz-newservice
  ```
4. Create the new app using the secret:
  ``` {.yaml .copy}
  oc new-app https://github.com/<user>/<private-repo>.git#main \
    --context-dir=newservice \
    --name=veriviz-newservice \
    --strategy=docker \
    --source-secret=veriviz-newservice-pat \
    --labels=app=veriviz-newservice
  ```

5. The rest (webhook, route, secrets for .env) is the same as above.
!!! note
    The `--source-secret=veriviz-newservice-pat` is critical so OKD can clone your private repo.

















