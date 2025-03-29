# Contributing

## Contributing to the Verviz Website

### Getting Started

1. **Fork and Clone**: Fork the Veriviz repository and/or clone it locally.
2. **Devcontainer Setup**: For a consistent development environment, check out [using devcontainers](devcontainers.md).
3. **Create a Branch**: Work on your feature or bug fix in a new branch, e.g., `git checkout -b feature/amazing-feature`.
4. **Test and Verify**: Ensure everything runs locally before opening a PR.  
   - If you’d like to deploy changes or see how deployment works, see [How to Deploy](how_to_deploy.md).
!!! note "Cloning Sylvia and/or SEIF"
    While not neseary, it is recommended to run things locally to test the full pipeline and your new code works. To tests the entirerty of the pipeline, it is recommended to clone Sylvia and/or SEIF to run these locally as well. Check out below for how to run these locally.

### Running on your local machine

#### Running Veriviz

1. `cd frontend`
2. Run `npm install` to verify everything is installed
3. Run `npm run dev`. Now the frontend is up and running on localhost.
4. `cd ../backend`
5. Run `npm install` to verify everything is installed
6. Run `node server.js`. Now the backend is up and running on localhost.

#### Running Sylvia

1. 


## MkDocs and Contributing to Verviz Docs

### What is MkDocs?

**MkDocs** is a static site generator built for project documentation. 
It uses Markdown files for content and a single `mkdocs.yml` for config. Read more about mkdocs on their [offical documentation website](https://www.mkdocs.org/).

### Contributing to Verviz Docs

1. **Fork or clone** the Veriviz documentation.
2. `ctrl + shft + p`( `cmd + shft + p` on mac) and select `reopen in devcontainer. For more information or if not working see [using devcontainers](devcontainers.md)

Now automatically, when you commit remotely to the main branch or sucesfully pull request, the website will automatically deploy and reflect your changes. Below are some common tasks that will help you get started.

### Common Tasks

- **Add a new doc**: create `new_topic.md` in `docs/` and link it in `mkdocs.yml`. 
- **Preview changes**: run `mkdocs serve` to check them locally.
- **Publish**: push to `main` if the pipeline is set to deploy.
!!! note "On `mkdocs.yml"
    The `mkdocs.yml` file defines configuration for the mkdocs site in a human readable format. To add your new file to the view of the website, look in the `mkdocs.yml` file, look for the `nav` section and and your file with a relative path. For example, if i craeted `hello.md` in `/docs/intros/hello.md`, in the `nav` section i would include:
    ```
    nav:
        - intros:
            - NAME HERE(ex. Hello): intros/hello.md
    ```

