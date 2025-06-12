# Python Virtual Environments

This guide provides instructions on how to set up and use a Python virtual environment. Virtual environments are essential for managing dependencies and ensuring that different Python projects don't interfere with each other.

### Installation
First, ensure you have the `python3-venv` package installed on your system. This package allows you to create virtual environments.
```bash
$ sudo apt install python3.13-venv
```

### Usage
Follow these steps to create, activate, install packages in, and deactivate a virtual environment:

#### Step 1: Create a Virtual Environment
Navigate to your project directory and create a new virtual environment. Replace `pip-env` with your desired environment name.
```bash
$ python3 -m venv pip-env
```

#### Step 2: Activate the Virtual Environment
To start using the environment, you need to activate it. The prompt in your terminal will typically change to indicate the active environment `(pip-env)`.
```bash
$ source pip-env/bin/activate
```

#### Step 3: Install Packages
Once activated, any Python packages you install using `pip` will only be installed within this specific virtual environment.
```bash
$ pip3 install requests colorama pyfiglet
$ pip3 list | grep requests # check modules
```

#### Step 4: Exit the Virtual Environment
When you're done working in the environment, you can deactivate it to return to your system's global Python environment.
```bash
$ deactivate
```