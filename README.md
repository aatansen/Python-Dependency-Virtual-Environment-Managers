<div align="center">
<h1>Python Dependency Virtual Environment Managers</h1>
</div>

# **Context**
- [**Context**](#context)
  - [**Top-Tier (Most Versatile \& Recommended)**](#top-tier-most-versatile--recommended)
    - [**uv**](#uv)
      - [uv Installation](#uv-installation)
      - [uv Usage](#uv-usage)
      - [More uv Commands](#more-uv-commands)
      - [Minimal `requirements.txt`](#minimal-requirementstxt)
    - [**poetry**](#poetry)
      - [poetry Installation](#poetry-installation)
      - [poetry Usage](#poetry-usage)
      - [More poetry Commands](#more-poetry-commands)
    - [**pyenv**](#pyenv)
      - [pyenv Installation](#pyenv-installation)
      - [pyenv Usage](#pyenv-usage)
    - [**pipx**](#pipx)
      - [pipx Installation](#pipx-installation)
      - [pipx Usage](#pipx-usage)
      - [CLI tools to try in pipx](#cli-tools-to-try-in-pipx)
    - [**pixi**](#pixi)
      - [pixi Installation](#pixi-installation)
      - [pixi Usage](#pixi-usage)
  - [**Mid-Tier (Popular \& Well-Supported)**](#mid-tier-popular--well-supported)
    - [**pip + venv**](#pip--venv)
      - [pip Installation](#pip-installation)
      - [pip Usage](#pip-usage)
      - [venv Usage](#venv-usage)
    - [**Miniforge3 (conda/mamba)**](#miniforge3-condamamba)
      - [conda](#conda)
      - [conda Usage](#conda-usage)
      - [mamba](#mamba)
    - [**hatch**](#hatch)
      - [hatch Installation](#hatch-installation)
      - [hatch Usage](#hatch-usage)
    - [**virtualenv**](#virtualenv)
      - [virtualenv Installation](#virtualenv-installation)
      - [virtualenv Usage](#virtualenv-usage)
  - [**Lower-Tier (Less Commonly Used)**](#lower-tier-less-commonly-used)
    - [**asdf**](#asdf)
    - [**virtualenvwrapper**](#virtualenvwrapper)
      - [virtualenvwrapper Installation](#virtualenvwrapper-installation)
      - [virtualenvwrapper Usage](#virtualenvwrapper-usage)
    - [**flit**](#flit)
      - [flit Installation](#flit-installation)
      - [flit Usage](#flit-usage)

## **Top-Tier (Most Versatile & Recommended)**

### **[uv](https://github.com/astral-sh/uv)**

- Fastest package installer and virtual environment manager.

[⬆️ Go to Context](#context)

#### uv Installation

- Using [`pip`](https://pypi.org/project/uv/)

  ```sh
  pip install uv
  ```

- Using [`exe`](https://docs.astral.sh/uv/getting-started/installation/)

  ```sh
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

- More installation process can be found in [official docs](https://docs.astral.sh/uv/getting-started/installation)

[⬆️ Go to Context](#context)

#### uv Usage

  ```sh
  uv venv   # Creates a .venv in the current directory
  uv venv my_environment # Creates a venv named my_environment
  uv venv --python 3.11.6  # Create venv with a specific Python version
  uv pip install requests  # Install a package
  uv pip list  # List installed packages
  uv run app.py # to run py file
  ```

[⬆️ Go to Context](#context)

#### More uv Commands

- Activate environment

  ```sh
  .venv\Scripts\activate
  ```

- Sync environment exactly to a requirements file (*installs missing, removes extra*)

  ```sh
  uv pip sync requirements.txt
  ```

- Initialize a new project (*creates `pyproject.toml`*)

  ```sh
  uv init
  ```

- Add dependencies to `pyproject.toml` and install/sync them

  ```sh
  uv add flask requests
  ```

- Add a development dependency

  ```sh
  uv add --group dev pytest
  ```

- Remove a dependency

  ```sh
  uv remove requests
  ```

- Create/update the `uv.lock` file based on `pyproject.toml`

  ```sh
  uv lock
  ```

- Install dependencies into the `venv` based on `uv.lock` (*like `uv pip sync`*)

  ```sh
  uv sync
  ```

- Converting `requirements.txt` to `pyproject.toml`

  ```sh
  uv init
  uv add -r requirements.txt
  ```

- Display Dependency Tree

  ```sh
  uv tree
  ```

- Use pip command in uv environment by installing seed packages (one or more of: pip, setuptools, and wheel) into the virtual environment.

  ```sh
  uv venv --seed
  ```

- > ModuleNotFoundError: No module named 'distutils'
- > `pip install setuptools` will solve this error

[⬆️ Go to Context](#context)

#### Minimal `requirements.txt`

- Install [pipdeptree](https://pypi.org/project/pipdeptree/)

  ```sh
  uv pip install pipdeptree
  ```

- Run the command to generate indented `requirements.txt`

  ```sh
  pipdeptree -f > requirements.txt
  ```

- Package can be excluded

  ```sh
  pipdeptree --exclude pip,pipdeptree,setuptools,wheel,build,packaging,pyproject_hooks -f > requirements.txt
  ```

- Minimal only main package `requirements.txt`

  ```sh
  pipdeptree --warn silence | grep -E "^[a-zA-Z0-9]" | awk '{print $1}' > requirements.txt
  ```

  or

  ```sh
  pipdeptree --warn silence | findstr "^[a-zA-Z]" > requirements.txt
  ```

- Combined exclude and minimal command

  ```sh
  pipdeptree --exclude pip,pipdeptree,setuptools,wheel,build,packaging,pyproject_hooks  --warn silence | grep -E "^[a-zA-Z0-9]" | awk '{print $1}' > requirements.txt
  ```

[⬆️ Go to Context](#context)

### **[poetry](https://github.com/python-poetry/poetry)**

- Full-fledged dependency and package manager.

[⬆️ Go to Context](#context)

#### poetry Installation

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Using pip

```sh
pip install poetry
```

[⬆️ Go to Context](#context)

#### poetry Usage

- Create `pyproject.toml`

  ```sh
  poetry init
  ```

- Or create a peotry project

  ```sh
  poetry new project_name
  ```

- Create virual environment (*env will be create in cache directory*)

  ```sh
  poetry install
  ```

- To create virtual environment withing project directory

  ```sh
  poetry config virtualenvs.in-project true
  ```

  Then

  ```sh
  poetry install
  ```

- Add a package

  ```sh
  poetry add requests
  ```

- Remove a package

  ```sh
  poetry remove flask
  ```

[⬆️ Go to Context](#context)

#### More poetry Commands

- Show install packages

  ```sh
  poetry show
  ```

- Show details of a specific package

  ```sh
  poetry show flask
  ```

- Update all dependencies

  ```sh
  poetry update
  ```

- Lock dependencies (generate/update poetry.lock)

  ```sh
  poetry lock
  ```

- Run command inside the virtual environment

  ```sh
  poetry run python new.py
  ```

- List all virtual environments

  ```sh
  poetry env list
  ```

- Check for dependency issues

  ```sh
  poetry check
  ```

[⬆️ Go to Context](#context)

### **[pyenv](https://github.com/pyenv-win/pyenv-win)**

- Best for managing multiple Python versions and virtual environments.

[⬆️ Go to Context](#context)

#### pyenv Installation

- [Using pip](https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#python-pip)

  ```sh
  pip install pyenv-win --target %USERPROFILE%\\.pyenv
  ```

- If you run into an error with the above command use the following instead ([#303](https://github.com/pyenv-win/pyenv-win/issues/303)):

  ```sh
  pip install pyenv-win --target %USERPROFILE%\\.pyenv --no-user --upgrade
  ```

- Setup Windows environment variable

  | Variable   | Value                            |
  | ---------- | -------------------------------- |
  | PYENV      | C:\Users\my_pc\.pyenv\pyenv-win\ |
  | PYENV_HOME | C:\Users\my_pc\.pyenv\pyenv-win\ |
  | PYENV_ROOT | C:\Users\my_pc\.pyenv\pyenv-win\ |

- And add two more lines to user variable Path

  ```sh
  C:\Users\my_pc\.pyenv\pyenv-win\bin
  C:\Users\my_pc\.pyenv\pyenv-win\shims
  ```

- Restart cmd or run `RefreshEnv.cmd` command provided by `Chocolatey`

[⬆️ Go to Context](#context)

#### pyenv Usage

- Get list of available python version

  ```sh
  pyenv install -l
  ```

- Installing a python version

  ```sh
  pyenv install 3.10.5
  ```

- Uninstalling a python version

  ```sh
  pyenv uninstall 3.10.5
  ```

- Set python

  ```sh
  pyenv global 3.10
  ```

- Select just for current shell session

  ```sh
  pyenv shell 3.10.5
  ```

- Multiple Python versions at the same time by specifying multiple arguments

  ```sh
  pyenv global 3.11 3.12
  ```

- pyenv update python version

  ```sh
  pyenv update
  ```

[⬆️ Go to Context](#context)

### **[pipx](https://github.com/pypa/pipx)**

- Best for installing standalone CLI tools globally in isolated environments.

[⬆️ Go to Context](#context)

#### pipx Installation

- Installing using pip

  ```sh
  python -m pip install --user pipx
  ```

- Warning solution

  ```log
  WARNING: The scripts activate-global-python-argcomplete.exe, python-argcomplete-check-easy-install-script.exe and register-python-argcomplete.exe are installed in 'C:\Users\Admin\AppData\Roaming\Python\Python312\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script userpath.exe is installed in 'C:\Users\Admin\AppData\Roaming\Python\Python312\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script pipx.exe is installed in 'C:\Users\Admin\AppData\Roaming\Python\Python312\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  ```

- Go to mentioned path `C:\Users\Admin\AppData\Roaming\Python\Python312\Scripts`
- Open cmd on that path and run

  ```sh
  .\pipx.exe ensurepath
  ```

[⬆️ Go to Context](#context)

#### pipx Usage

- Installing Package

  ```sh
  pipx install pycowsay
  ```

- Uninstalling Package

  ```sh
  pipx uninstall pycowsay
  ```

- Inject a package (when required additional packages)

  ```sh
  pipx inject ipython matplotlib
  ```

- Injecting multiple packages

  ```sh
  pipx inject ipython matplotlib pandas
  # or:
  pipx inject ipython -r useful-packages.txt
  ```

[⬆️ Go to Context](#context)

#### CLI tools to try in pipx

| Tool           | Purpose                  | Use Case                                            |
| -------------- | ------------------------ | --------------------------------------------------- |
| `httpie`       | HTTP client              | User-friendly `curl` alternative for APIs           |
| `black`        | Code formatter           | Opinionated Python formatter (fast + safe)          |
| `ruff`         | Linter + Formatter       | All-in-one linting (super fast, written in Rust)    |
| `poetry`       | Package manager          | Modern dependency management + publishing           |
| `pipenv`       | Package manager          | Dependency locking + venv in one                    |
| `cookiecutter` | Project scaffolding      | Generate project boilerplates                       |
| `rich-cli`     | Pretty CLI output        | Render JSON, markdown, syntax-highlighted code      |
| `glances`      | System monitor           | Real-time system resource viewer (cross-platform)   |
| `pgcli`        | PostgreSQL client        | Auto-complete + syntax highlighting in terminal     |
| `bpython`      | Python REPL              | Fancy REPL with autocomplete & docs                 |
| `ipython`      | Advanced REPL            | Interactive dev console with magic commands         |
| `howdoi`       | Quick answers            | Searches StackOverflow from terminal                |
| `doit`         | Task runner              | Better alternative to Makefiles for Python projects |
| `pdm`          | Next-gen package manager | PEP 582 support (no venv needed)                    |
| `xonsh`        | Shell + Python           | Shell with full Python power                        |
| `yt-dlp`       | YouTube downloader       | Download and convert videos via CLI                 |

[⬆️ Go to Context](#context)

### **[pixi](https://github.com/prefix-dev/pixi)**

- It is a fast, multi-language package and environment manager built on top of the Conda ecosystem.

#### pixi Installation

- Run the powershell command

  ```sh
  powershell -ExecutionPolicy ByPass -c "irm -useb https://pixi.sh/install.ps1 | iex"
  ```

[⬆️ Go to Context](#context)

#### pixi Usage

- Initial pixi

  ```sh
  pixi init
  ```

- Create environment

  ```sh
  pixi install
  ```

- Add package

  ```sh
  pixi add 'python>=3.13.0,<3.14' jupyterlab
  ```

- Add package (when package not available in **conda channels** `--pypi` is used)

  ```sh
  pixi add django --pypi
  ```

- Add packages from `requirements.txt`
  - Create a file `add_to_pixi.cmd`

    ```cmd
    @echo off
    REM -----------------------------
    REM Install packages from requirements.txt using Pixi
    REM Automatically adds --pypi if default install fails
    REM -----------------------------

    SETLOCAL ENABLEDELAYEDEXPANSION
    SET "FILE=requirements.txt"

    FOR /F "usebackq delims=" %%A IN ("%FILE%") DO (
        REM Get package name without version
        FOR /F "tokens=1 delims==" %%B IN ("%%A") DO (
            echo Installing %%B...
            pixi add %%B
            IF !ERRORLEVEL! NEQ 0 (
                echo "Failed to install %%B via default, trying with --pypi..."
                pixi add %%B --pypi
            )
        )
    )

    echo All packages processed!
    pause
    ```

  - Now run `add_to_pixi.cmd`

- Remove package

  ```sh
  pixi remove django --pypi
  ```

- Remove pixi environment

  ```sh
  pixi clean
  ```

- List all install packages

  ```sh
  pixi list
  ```

- Activate environment shell

  ```sh
  pixi shell
  ```

- Exit environment shell

  ```sh
  exit
  ```

- Run command

  ```sh
  pixi run python --version
  pixi run jupyter lab
  ```

[⬆️ Go to Context](#context)

## **Mid-Tier (Popular & Well-Supported)**

### **[pip + venv](https://github.com/pypa/pip)**

- Default, lightweight, and comes with Python.

[⬆️ Go to Context](#context)

#### pip Installation

- It is installed by default with Python >= 3.4

- Update pip

  ```sh
  python -m pip install pip --upgrade
  ```

[⬆️ Go to Context](#context)

#### pip Usage

- Installing a package

  ```sh
  pip install <package-name>
  ```

- Installing specific version

  ```sh
  pip install <package-name>==<version>
  ```

- Installing from a requirements file

  ```sh
  pip install -r requirements.txt
  ```

- Saving current packages to a requirements file

  ```sh
  pip freeze > requirements.txt
  ```

- Updating multiple packages

  ```sh
  pip install -r requirements.txt --upgrade
  ```

- Uninstalling a package

  ```sh
  pip uninstall <package-name>
  ```

- Listing installed packages

  ```sh
  pip list
  ```

- Checking outdated packages

  ```sh
  pip list --outdated
  ```

- Showing info about a package

  ```sh
  pip show <package-name>
  ```

[⬆️ Go to Context](#context)

#### venv Usage

- Creating a virtual environment

  ```sh
  py -m venv env
  ```

- Activating the virtual environment

  ```sh
  env\Scripts\activate
  ```

- Deactivating the virtual environment

  ```sh
  deactivate
  ```

- Deleting a virtual environment

  ```sh
  rd /s /q env
  ```

[⬆️ Go to Context](#context)

### [**Miniforge3 (conda/mamba)**](https://github.com/conda-forge/miniforge)

- It is a minimal, community-driven Conda distribution that includes both the `conda` and `mamba` package managers, with the `conda-forge` channel set as the default source for packages.

#### [conda](https://anaconda.org/anaconda/conda)

- Ideal for data science and scientific computing. It manages packages, environments, and dependencies effectively across platforms.
- Since it is included with Miniforge3, there is no need to install it separately. However, if needed, download and install [Miniconda](https://repo.anaconda.com/miniconda/) (a lightweight Conda distribution) or [Anaconda](https://www.anaconda.com/download) (which includes many pre-installed packages).

#### conda Usage

| Task                      | Command                                 |
| ------------------------- | --------------------------------------- |
| Env in miniconda envs path| `conda create -n myenv python=3.11`     |
| Env in current path       | `conda create -p myenv python=3.11`     |
| Activate environment      | `conda activate myenv`                  |
| Deactivate environment    | `conda deactivate`                      |
| List all environments     | `conda env list` or `conda info --envs` |
| Install package           | `conda install numpy`                   |
| Install specific version  | `conda install pandas=1.5.3`            |
| Remove package            | `conda remove package_name`             |
| Update package            | `conda update scipy`                    |
| Update all package        | `conda update --all`                    |
| Export environment        | `conda env export > environment.yml`    |
| Recreate env from file    | `conda env create -f environment.yml`   |
| Delete environment        | `conda remove --name myenv --all`       |

> [!NOTE]
>
> - Prefer `conda install` when available to avoid dependency conflicts.
>
> - Use `pip install` within a conda environment if a package isn't available via conda.

[⬆️ Go to Context](#context)

#### [mamba](https://github.com/mamba-org/mamba)

- It is a fast, drop-in replacement for `conda` written in C++
- It is included by default in `Miniforge` versions `23.3.1-0` and above.
- All commands are compatible with `conda`, so simply replacing conda with `mamba` will work seamlessly.

[⬆️ Go to Context](#context)

### **[hatch](https://github.com/pypa/hatch)**

- Modern package and virtual environment manager.

[⬆️ Go to Context](#context)

#### hatch Installation

- Installer
  - [Download](https://github.com/pypa/hatch/releases/latest/download/hatch-x64.msi) and install
- Using pipx
  - `pipx install hatch`

[⬆️ Go to Context](#context)

#### hatch Usage

- Create hatch project

  ```sh
  hatch new hatch-project
  ```

- Create environment

  ```sh
  hatch env create
  ```

- Activate and use the environment

  ```sh
  hatch shell
  ```

- Exit from environment

  ```sh
  exit
  ```

- Remove environment

  ```sh
  hatch env prune
  ```

- View list of environment

  ```sh
  hatch env show
  ```

- Project version check

  ```sh
  hatch version
  ```

- Change project version

  ```sh
  hatch version minor # patch, minor, major
  ```

[⬆️ Go to Context](#context)

### **[virtualenv](https://github.com/pypa/virtualenv)**

- Alternative to `venv` with more features.

[⬆️ Go to Context](#context)

#### virtualenv Installation

- Using pipx

  ```sh
  pipx install virtualenv
  ```

[⬆️ Go to Context](#context)

#### virtualenv Usage

- Creating env

  ```sh
  virtualenv env
  ```

- Activating env

  ```sh
  env\Scripts\activate
  ```

- Deactivate env

  ```sh
  deactivate
  ```

[⬆️ Go to Context](#context)

## **Lower-Tier (Less Commonly Used)**

### **[asdf](https://github.com/asdf-vm/asdf)**

- Universal version manager supporting Python and other languages.

[⬆️ Go to Context](#context)

### **[virtualenvwrapper](https://github.com/davidmarble/virtualenvwrapper-win)**

- Helper for managing `virtualenv` environments easily.

[⬆️ Go to Context](#context)

#### virtualenvwrapper Installation

- Using `pipx`

  ```sh
  pipx install virtualenvwrapper-win
  ```

[⬆️ Go to Context](#context)

#### virtualenvwrapper Usage

| Purpose                                            | Command                         |
| -------------------------------------------------- | ------------------------------- |
| Create & activate a new virtualenv                 | `mkvirtualenv myenv`            |
| List or activate virtualenvs                       | `workon myenv`                  |
| Delete a virtualenv                                | `rmvirtualenv myenv`            |
| Go to the directory of the current env             | `cdvirtualenv`                  |
| Go to `site-packages` of current env               | `cdsitepackages`                |
| List packages installed in current env             | `lssitepackages`                |
| List all virtualenvs                               | `lsvirtualenv`                  |
| Add folders to `PYTHONPATH` of active env          | `add2virtualenv path\to\folder` |
| Allow/disallow global packages in current env      | `toggleglobalsitepackages`      |
| Create a project directory and virtualenv          | `mkproject myproject`           |
| Go to the directory of the current project         | `cdproject`                     |
| Link a project directory to the current virtualenv | `setprojectdir D:\myproject`    |
| Used internally for deletion                       | `folder_delete D:\Env\myenv`    |
| Locate the current virtualenv's base directory     | `whereis`                       |
| Lists env variables for the current env            | `vwenv`                         |

[⬆️ Go to Context](#context)

### **[flit](https://github.com/pypa/flit)**

- Minimalistic package builder and publisher.

[⬆️ Go to Context](#context)

#### flit Installation

- Using `pipx`

  ```sh
  pipx install flit
  ```

[⬆️ Go to Context](#context)

#### flit Usage

- Initial project

  ```sh
  flit init
  ```

- Publish package to PyPI

  ```sh
  flit publish
  ```

[⬆️ Go to Context](#context)
