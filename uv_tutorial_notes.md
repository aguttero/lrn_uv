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

### Troubleshoot UV sync python 3.13 to 3.14
#### option 1
The cryptography package includes native C-extensions. On Python 3.14, you may be missing the required system build tools, or the lockfile might be tied to pre-compiled binaries from Python 3.13.

To fix this, you can instruct uv to use pre-built wheels (if available) or force a clean re-installation:
1. Delete the .venv directory and cache: Clean out the old environment and lock cache to avoid cached version conflicts.

```bash
rm -rf .venv
uv cache clean
```

2. Force-reinstall and compile: Re-sync your project and force uv to resolve the dependencies strictly for your Python 3.14 environment.
```bash
uv sync --force-reinstall --no-cache
```
Alternatively, you can install Python 3.13 on your second device using uv to ensure perfect environment parity:
```bash
uv python install 3.13
uv sync --python 3.13
```
#### option 2 missing RUST/OpenSSL tools to compile
Para solucionar este error, debes sincronizar las versiones de Python entre ambos dispositivos o forzar la compilación local. El fallo ocurre porque cryptography v49.0.0 es un paquete compilado (contiene extensiones binarias en Rust/C). Al pasar a Python 3.14, PyPI aún no dispone de "wheels" precompiladas para esta versión tan reciente, lo que obliga a uv a intentar compilar el código fuente en tu máquina. Si tu segundo dispositivo carece de las herramientas de compilación necesarias (como el compilador de Rust o las librerías de desarrollo de OpenSSL), el proceso fallará irremediablemente.A continuación se presentan las mejores alternativas para corregir el problema de forma definitiva.

##### alternativa 1 forzar python 3.13
1. Eliminar .venv
  rm -rf .venv
2. forzar python 3.13
  uv python pin 3.13
3. Volver a Sync las dependencias
  uv sync

##### alternativa 2 instalar librerias de compilacion
1. Linux:
  ```bash
  sudo apt update
  sudo apt install build-essential libssl-dev libffi-dev python3-dev pkg-config curl
  curl --proto '=https' --tlsv1.2 -sSf https://rustup.rs | sh
```

2. macOs:
  ```bash
  xcode-select --install
  curl --proto '=https' --tlsv1.2 -sSf https://rustup.rs | sh
  ```
  
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
