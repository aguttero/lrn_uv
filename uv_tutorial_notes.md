# Install
## Global setup (only once)
- deactivate venv
- pip3 install uv (only once globally)

## Project init
- uv init `my project folder name`
- cd `my project folder name`
- creates folder, git, main.py, pyproj.toml, README.md

### Init v2
- uv init --app
- uv init --lib `my_library_folder`
- cd my_project uv init `sub_project` -> creates a sub_project structure child of parent folder 

### Init Git Clone UV Project
- install uv (if not already installed)
- cd to cloned project folder
- uv sync

## Install python modules
- uv add module1 module2 modulen
    * creates .venv
    * installs
    * creates pyproject.toml -> dependencies constraints
    * creates uv.lock -> detailed dependencies info
- example to limit veresion: run `uv add "flask==2.*"`
- pip syntax: `uv pip [un]install module` or `uv pip install module --upgrade` 

## Uninstall python modules
- uv remove pandas

## Manually add modules in .toml
- Edit .toml add module
- run `uv lock` to check and resolve dependency info -> will check also for incompatibilities between modules
- run `uv sync` to install modules

## Run
- don't need to activate the .venv 
- uv run python3 `main.py`
- uv run `main.py`

## Managing Python versions
- run `uv python list`
- run `uv python list --only-installed`

### Install Python version
- run `uv isntall python 3.13`

### Pin Python version
- run `uv python pin 3.9`

## Tools
- run `uv tool run jupyter` or `uvx jupyter`
- run `uv tool run jupyter lab` or `uvx jupyter lab`

### Tooks Ruff
- run `uvx ruff check` look for errors in codebase
- run `uvx ruff format` format and lint

# UV to production
https://www.youtube.com/watch?v=45bAPTZW16o&t=69s
## UV Publish -> AG do research
- see Youtube
