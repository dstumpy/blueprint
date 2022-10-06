# {{ cookiecutter.project_name }}

{{ cookiecutter.project_description }}

## Contact

{{ cookiecutter.full_name }} <{{ cookiecutter.email }}>


## Dev Setup

1. Activate ssh access to azure by creating a rsa-key & adding it to azure.

    Save your ssh-key password in a `credentials/.ssh_secret` file.\
    The password is needed while adding your ssh-key to a ssh-agent during the build process.\
    Investigate Dockerfile for more info.

2. Build dev image
    Make sure your ssh key (id_rsa) is placed as follows `$HOME/.ssh/id_rsa`.\
    If the ssh key is placed somewhere else, adapt the following bash script:

    ```bash
    DOCKER_BUILDKIT=1 docker build --secret id=id_rsa,src="$HOME/.ssh/id_rsa" --secret id=ssh_pw,src=credentials/.ssh_secret --target dev -t {{ cookiecutter.project_slug }}_dev_image .
    ```

    After successfully building the image, start and stop the container once via command line.

    ```bash
    docker-compose up --force-recreate dev
    Ctrl+C
    ```
    If you do not start it once, the next step can fail. The extension tries to rebuild the image itself, **if it does not find a stopped/cached container**.\
    The build initiated by the VsCode extension does not use our fancy docker build secrets.

3. You can use VsCode now to open the dev container
    ```
    CTRL+SHIFT+P -> 'Remote-Containers: Reopen in Container'
    ```

4. Install required pre-commits before your first commit.
    ```bash
    pre-commit install
    ```

## Remote Dev Setup (jupyter notebook development)

1. Start docker container before executing python snippets in VsCode

```bash
docker-compose up --force-recreate dev-jupyter
```

2. Vscode settings

```
"python.dataScience.sendSelectionToInteractiveWindow": true,
"python.dataScience.jupyterServerURI": "http://127.0.0.1:8888/",
```

3. Execute python snippets in VsCode
4. Profit ...
