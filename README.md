<div align="center">
<h1>Python Dependency Virtual Environment Managers</h1>
</div>

# **Context**
- [**Context**](#context)
  - [**Top-Tier (Most Versatile \& Recommended)**](#top-tier-most-versatile--recommended)
    - [**UV**](#uv)
      - [UV Installation](#uv-installation)
      - [UV Usage](#uv-usage)
      - [More UV Commands](#more-uv-commands)
    - [**poetry**](#poetry)
      - [Poetry Installation](#poetry-installation)
      - [Poetry Usage](#poetry-usage)
    - [**pyenv-virtualenv**](#pyenv-virtualenv)
    - [**pipx**](#pipx)
  - [**Mid-Tier (Popular \& Well-Supported)**](#mid-tier-popular--well-supported)
    - [**pip + venv**](#pip--venv)
    - [**conda**](#conda)
    - [**hatch**](#hatch)
    - [**virtualenv**](#virtualenv)
  - [**Lower-Tier (Less Commonly Used)**](#lower-tier-less-commonly-used)
    - [**asdf**](#asdf)
    - [**virtualenvwrapper**](#virtualenvwrapper)
    - [**flit**](#flit)

## **Top-Tier (Most Versatile & Recommended)**

### **UV**

- Fastest package installer and virtual environment manager.

[⬆️ Go to Context](#context)

#### UV Installation

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

#### UV Usage

  ```sh
  uv venv   # Creates a .venv in the current directory
  uv venv my_environment # Creates a venv named my_environment
  uv venv --python 3.11.6  # Create venv with a specific Python version
  uv pip install requests  # Install a package
  uv pip list  # List installed packages
  uv run app.py # to run py file
  ```

#### More UV Commands

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

[⬆️ Go to Context](#context)

### **poetry**

- Full-fledged dependency and package manager.

#### Poetry Installation

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

#### Poetry Usage

```sh
poetry new myproject  # Create a new project
cd myproject
poetry install  # Install dependencies
poetry add requests  # Add a package
```

### **pyenv-virtualenv**

- Best for managing multiple Python versions and virtual environments.

### **pipx**

- Best for installing standalone CLI tools globally in isolated environments.

## **Mid-Tier (Popular & Well-Supported)**

### **pip + venv**

- Default, lightweight, and comes with Python.

### **conda**

- Ideal for data science and scientific computing.

### **hatch**

- Modern package and virtual environment manager.

### **virtualenv**

- Alternative to `venv` with more features.

## **Lower-Tier (Less Commonly Used)**

### **asdf**

- Universal version manager supporting Python and other languages.

### **virtualenvwrapper**

- Helper for managing `virtualenv` environments easily.

### **flit**

- Minimalistic package builder and publisher.
