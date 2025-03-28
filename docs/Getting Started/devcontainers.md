# What are Devcontainers and why are they useful?

A Devcontainer utilizes Docker to create a virtual environment while developing your project. For example, I can specify a Dev container to run an Ubuntu Linux environment with python installed and no matter which machine I want to work on the project with(ie. windows, mac, etc.), I will have a consistent enviroment throughout. 

A Dev Container ensures your development environment is consistent and works with whatever machine may be running it. It makes collabration easy and saves a lot of time. It's best practice and in short it solves the issue of "but it works on my machine". Additionally, we want to use the **OKD CLI**, which is incredibly easy and consistent to have form a devcontainer, but complicated and issue prone to dowload on your own machine

## Using DevContainers

As you will see in Veriviz, there is a predefined devcontainer. Running it is the most important thing but if you would like to learn more and how to create one, read the `Creating a Devcontainer` section below.

!!! note "Prerequisties"
    - **Docker** is strictly nesseary to run a devcontainer and needs to be dowloaded. Check out [here](https://www.docker.com/products/docker-desktop/) for download information(The free version is recommended). 
    - **VsCode** is highly recommended. This tutorial will assume you are using VsCode and using any other code editor for a devcontainer will require your own research.
    - The **Dev Containers Extension in VsCode** is needed as well

### Re-opening in a devcontainer

Reopening the project in a dev container can be done with `Ctrl+Shift+P`(or `Cmd+Shift+P` on Mac) and typing "Dev Containers: Reopen in Container" and selecting that option. It's that simple!

!!! note "Pop-Up"
    You also may see a pop up in VSCode on the bottom right hand side of your screen roughly stating **"Would you like to reopen this project in a dev container?"** which you can **click yes to to achieve the same result.**

## Creating a Devcontainer

As outlined earlier a devcontainer is extremly useful for collaboration and just a good qualit yof life thing to have for a repo.

1. In VS Code, open your project via its root directory
2. Install Dev Containers extension in VS Code
3.  create a ```.devcontainer``` directory in the root of your project which is the `rust-intro` directory we just made
```{.yaml .copy}
mkdir .devcontainer
```
This tells the VsCode devcontainers extension there is a devcontainer and it will know to look here
4. Use VS Code and create a file named ```devcontainer.json``` inside of the ```.devcontainer``` directory. This is where you will define what your devcontainer's skeleton. Look below for an example for a basic `Rust` container.

``` { .yaml .copy}
{
    "name": "Rust Intro",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode":{
            "settings": {},
            "extensions":["rust-lang.rust-analyzer"]
        }
    },    
    "postCreateCommand": "",
}
```
Here's what everything does

* **```name:```** This is what your dev container will be named

- **```image:```** The docker image to use, in this case we will be using a preconfigured image for rust by microsoft

- **```customizations:```** Adds configurations like VS Code extensions ensuring other developers have them too. ```rust-lang.rust-analyzer``` is the standard language server for rust development in vs code.

- **```postCreateCommand:```** A command to run after the container is created. In our case, we don't include anything but you could create a seperate file with a bash command to run and link it here. When the container is built, that command will be run!

Et Voila, it is done. IN case you wanted to use a custom image form a Dockerfile of your own, no problem, just make the dockerfile and include the path in the json. See [here](https://code.visualstudio.com/docs/devcontainers/containers) for some more documentation on devcontainers.


