# Python Blueprint

Cookiecutter blueprint for setting up Python projects.

## Quickstart
### Prerequisites

This blueprint assumes you have the following tools set up:

* [cookiecutter](https://github.com/cookiecutter/cookiecutter)
* docker & docker-compose e.g. on [windows](https://docs.docker.com/docker-for-windows/install)
* setup to use ssh-key with passphrase on [azure-devops](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops)

### Initial Project Setup

1. Generate a Python package project:
    ```bash
    cookiecutter <githublink>
    ```

2. Afterwards enter the created project folder and follow the steps in the local README.md

3. Create a new repository on GitHub & push your local project

### Project Blueprint development

1. Build docker image

     ```bash
    docker-compose build --no-cache dev
    ```

    After successfully building the image, start and stop the container once via command line.

    ```bash
    docker-compose up --force-recreate dev
    CTRL+C
    ```
    If you do not start it once, the next step can fail. The extension tries to rebuild the image itself, **if it does not find a stopped/cached container**.\
    The build initiated by the extension does not use our fancy docker build secrets.

2. Connect into Container via [VsCode Remote Container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
    1.  Open your folder in VsCode
    2. `CTRL+SHIFT+P` -> "Remote-Containers: Reopen in Container"
    3. Select poetry venv manually as your python environment once (due to a hash in the name, this cannot be done automatically). The environment is saved in your local project `.vscode/settings.json`. If you add & push these changes to the repo, nobody else has to manually update it again.

3. Initialize `pre-commit` hooks and Git repository:

    ```bash
    pre-commit install
    git init .
    git add .
    git commit -m "initial commit"
    ```

## File description
* .devcontainer/devcontainer.json\
Works as an entrypoint for the VsCode Remote Container extension. [link](https://code.visualstudio.com/docs/remote/devcontainerjson-reference)
* .vscode/settings.json\
Lokal project settings for VsCode. (Makes it easy to point to the virtual python environment created by poetry)
* credentials/*\
Path to store credentials. (e.g. your ssh passphrase or db access credentials)
* [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file)\
Used to block docker from copying specific folder/files to an image during a build process
* .flake8\
[Config file](https://flake8.pycqa.org/en/latest/user/configuration.html#configuration-locations) for [flake8](https://pypi.org/project/flake8/) python linter.
* .gitattributes\
Used to enforce lf-lineendings on git commits while working on windows and linux. [link](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files)
* [.gitignore](https://git-scm.com/docs/gitignore)\
Used to exclude folders/files from git tracking.
* .pre-commit-config.yaml\
Configuration of [pre-commit hocks](https://pre-commit.com/).
* [docker-compose.yaml](https://docs.docker.com/compose/)
* [Dockerfile](https://docs.docker.com/engine/reference/builder/)\
Used to build an docker image of our application.
* [pyproject.toml](https://snarky.ca/clarifying-pep-518/)\
Used by several python  dev tools: [poetry](https://python-poetry.org/), [black](https://github.com/psf/black), [isort](https://github.com/timothycrosley/isort)
