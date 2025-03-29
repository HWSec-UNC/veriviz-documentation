# How to Deploy

## Setting up CD for a service

In the root of your project, set up a `.github/workflows` directory and make a file called `cicd.yml` result in a full path of `ROOT/.github/workflows/cicd.yml`

 ### "What is cicd.yml"

This file tells github a few things. We have not gotten to secrets yet but we will soon. IN a nutshell, a secret is seomthing we will give to our OKD deployment and define in our Github Repo.
- The `.github/workflow` directory is a special directory that when github sees, it knows to look in here for rules for CD
- ```
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```
Tells github to send our secret to OKD on a push to` main`(commit) or a pull request to `main`. We will later define this in our deployment but for now this is all you need to know


Below is an example from verviz of the `cicd.yml` file. As you can see `.yml` files are very human readable and easy to follow.
``` { .yaml .copy}
name: NAME-OF-YOUR-PROJECT-HERE

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  cd-frontend:
    name: "Continuous Deployment - Veriviz"
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Trigger OKD Build for Veriviz
        run: |
          curl -X POST ${{ secrets.CD_BUILD_WEBHOOK_FRONTEND}}
  cd-backend:
    name: "Continuous Deployment - Backend"
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Trigger OKD Build for Veriviz Backend
        run: |
          curl -X POST ${{ secrets.CD_BUILD_WEBHOOK_VERIVIZ_BACKEND }}
```