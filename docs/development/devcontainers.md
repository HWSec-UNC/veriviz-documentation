# What are Devcontainers and why are they useful?

A **Devcontainer** uses Docker to create a virtual environment while developing your 
project. For example, you can run an Ubuntu environment with Python installed, and 
no matter which machine (Windows, macOS, or Linux) you use, you’ll have a **consistent 
setup**.

**Benefits:**

- Avoid "it works on my machine" issues.
- Simplify collaboration.
- Effortlessly include tools (like the **OKD CLI**) without manual installs.

---

## Using DevContainers

As you will see in Veriviz, there is a predefined devcontainer. Running it is the most important thing but if you would like to learn more and how to create one, read the `Creating a Devcontainer` section below.

!!! note "Prerequisties"
    - **Docker** is strictly nesseary to run a devcontainer and needs to be dowloaded. Check out [here](https://www.docker.com/products/docker-desktop/) for download information(The free version is recommended). 
    - **VsCode** is highly recommended. This tutorial will assume you are using VsCode and using any other code editor for a devcontainer will require your own research.
    - The **Dev Containers Extension in VsCode** is needed as well

### Re-opening in a devcontainer

1. Press **Ctrl+Shift+P** (or **Cmd+Shift+P** on Mac) in VS Code.
2. Choose **"Dev Containers: Reopen in Container"**.
3. VS Code reopens in your dev environment automatically.

!!! note
    Sometimes, VS Code prompts **"Reopen folder to develop in a container?"**.
    Clicking **"Reopen"** achienves the same result.

---

## Creating a Devcontainer

As outlined earlier a devcontainer is extremly useful for collaboration and just a good quality of life thing to have for a repo. Below is an **Example** devcontainer steup for Rust that is **not used in verviz** but just her eto provide an example of how to set up a devcontainer.

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

- **```postCreateCommand:```** An optional script to run on container creation

For more info, see [VS Code’s Devcontainers docs](https://code.visualstudio.com/docs/devcontainers/containers).


