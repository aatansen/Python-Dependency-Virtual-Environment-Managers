<div align="center">
<h1>Python Dependency Virtual Environment Managers</h1>
</div>

# **Context**
- [**Context**](#context)
  - [**Top-Tier (Most Versatile \& Recommended)**](#top-tier-most-versatile--recommended)
    - [**UV**](#uv)
      - [UV Installation](#uv-installation)
      - [UV Usage](#uv-usage)
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
  uv venv --python 3.11.6  # Create venv with a specific Python version
  uv pip install requests  # Install a package
  uv pip list  # List installed packages
  uv run app.py # to run py file
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
