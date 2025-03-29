# veriviz-documentation
This is the documentation for veriviz using [MkDocs](https://www.mkdocs.org/)
View the documentation website [here](https://hwsec-unc.github.io/veriviz-documentation/)

# Contributing to the documentation

Below are the basic steps to get started. These steps are outlined in more detail on the [website](https://hwsec-unc.github.io/veriviz-documentation/](https://hwsec-unc.github.io/veriviz-documentation/contributing/#mkdocs-and-contributing-to-verviz-docs)
1. Run the devcontainer in vscode
2. in the .docs directory, add markdown files with your documentation and mkdocs will take care of the rest and will automitically deploy when committed to main
3. For orginization, make subfolders in the `docs` directory and it will appear as drop down in the website. Example: I amke a `docs/deployment` direcotry where under `deployment` I have a a couple markdown(`.md`) files. This will have improved clarity on the website.
4. Run the command `mkdocs serve` in the devcontainer to run locally
