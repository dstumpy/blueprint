# {{ cookiecutter.project_name }}

{{ cookiecutter.project_description }}

## Contact

{{ cookiecutter.full_name }} <{{ cookiecutter.email }}>

## Dev Setup

1. Make sure `Docker` and `docker-compose` are installed. It is highly recommended to run the code in a Docker container.
  
    ### Other options
    If you do not want to follow these steps using Docker, you can stop here and explore the project on your own using local environments such as `poetry` or `venv`.

    Creating a local environment using `poetry` can be reached via

    ```bash
    poetry install
    ```
    ( assuming that `poetry` is already installed and `pyproject.toml` is located at the current working directory)

    To use a local environment, just run
    ``` bash
    python -m venv <my_venv_name>
    source ./<my_venv_name>/bin/activate
    ```

2. Next, create the Docker image using `docker-compose`
    ```bash
    docker-compose build ide
    ```

3. Make sure your SSH agent is running
    ```bash
    eval "$(ssh-agent -s)"
    ```

4. After successfully building the image, create the container based on that image
    ```bash
    docker-compose up ide
    ```

5. Now, the browser-like IDE `code-server` should be running and can be reached via `localhost:8123`.


## Project Setup