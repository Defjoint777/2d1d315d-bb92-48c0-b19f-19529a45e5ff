<!---
{
  "depends_on": ["7130a694-458e-4e24-80b7-d8673f765e69"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-07",
  "keywords": ["python", "environment", "venv", "libraries"]
}
--->

# Working with libraries in python3

## Introduction

Libraries are the **secret sauce** of Python. From scientific computing to web development, from machine learning to hardware control—there's almost always a Python library that can help. This vast ecosystem is one of Python's greatest strengths and a big reason for its popularity.

To manage these libraries efficiently, especially when working on multiple projects or systems, we need tools that give us fine-grained control over installation, versions, and environments. This is where the combination of `pip` and `venv` comes in.

While there are multiple ways to handle Python package management, one of the most common and recommended approaches is using:

- `pip` – Python’s built-in **package installer**
- `venv` – Python’s built-in tool for creating **isolated environments**

In this exercise, we’ll explore how to install and manage libraries using `pip`, and how to use `venv` to **create isolated environments** that prevent dependency conflicts.

---

Python is a **command-line interpreter**—a program itself—that lives somewhere on your computer. When you run `python3` from your terminal, you’re calling a binary that interprets either interactive commands or runs script files, like we did in the [previous exercise](https://github.com/STEMgraph/7130a694-458e-4e24-80b7-d8673f765e69).

This interpreter comes bundled with **standard libraries**, and `pip` allows us to install additional libraries from the [Python Package Index (PyPI)](https://pypi.org/). However, installing a new version of a library usually **replaces the old one**—which can be a problem if different projects rely on different versions of the same package.

To avoid such conflicts, Python offers a mechanism called **virtual environments**. These are self-contained Python installations, complete with their own `pip`, interpreter, and site-packages folder.

> Not sure what an *environment* is? Revisit the [exercise on bash environments](https://github.com/STEMgraph/862f9d0d-6ee1-4746-9988-e7cd0efc1c56).

By creating a `venv`, we can experiment, isolate dependencies, and avoid polluting the global Python installation. Better yet, we can maintain **multiple versions of the same library**—even multiple versions of Python itself—without breaking anything on our system.

Learning to use `pip` and `venv` is not just a best practice—it’s **essential for professional Python development**.


### Further Reading

- [Packaging Python Projects (Official Guide)](https://packaging.python.org/en/latest/tutorials/packaging-projects/)
- [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/)
- [Managing Python with pyenv](https://realpython.com/intro-to-pyenv/) *(for multiple Python versions)*
- [Pip Documentation](https://pip.pypa.io/en/stable/)
- [PEP 405 – Python Virtual Environments](https://peps.python.org/pep-0405/)
- [Python Module of the Week: venv](https://pymotw.com/3/venv/)


## Tasks
1. **Check your Installations**: Make sure, that `pip` and `python3` are installed:
```bash
python3 --version
pip --version
```
2. **Print a List of all Installed Libraries**: Run `pip freeze` to see a list of installed libraries on your system.
3. **Install a Library with pip**: Run `pip install lolpython` to install the `lolpython` library. If you are running a newer version of python, you will be informed, that `pip` doesn't want to install the package systemwide. This should be plenty of warning for you, to not tinker with this, unless you really want to figure out how you can break your distribution!
4. **Start a New Project**: Navigate to your home-directory and make a new folder. Jump into it and inspect your current python-path:
```bash
cd
mkdir my_python_proj
cd my_python_proj
which python3
```
You will see the full path of your current python installation.
5. **Create a Virtual Environment**: A virtual environment is like a project local installation of python itself. Make sure to be in your project directory, now you can create such an installation by running:
```bash
python3 -m venv env
```
With `env` being the name of a local directory, that will be created within your project directory. Inspect your project-dir by running `ls`. 

<details>
  <summary>Tip for Task 5</summary>
  If you have multiple python installations, say python3.11 and python3.12, you may also run `python3.11 -m venv env` to create a virtual environment of a specific version of python!
</details>

6. **Activating the Virtual Environment**: Right now, you made a local installation, but your shell-session doesn't know yet, that it is supposed to use this local installation. Run `which python3` to find the path to your current python-installation. Now use the `source` command to load the file `./env/bin/activate` to tell your shell-session, that you want to use the local installation. Run `which python3` again and observe the change.

7. **Packages within your venv**: With the activation-file sourced, run `pip freeze`. The output should be empty, since you have not yet installed libraries. Run `pip install lolpython` to install a library. Run `pip freeze` again and see, that the library is now available in your virtual environment.
8. **Deactivating**: Run `which python3` and `pip freeze` one last time and note the output. Type `deactivate` into your terminal and hit `enter`. Your virtual environment is now deactivated. Run `which python3` and `pip freeze` again. Now, your shell will continue using the system wide installation again. 
9. **Running a Script with the venv**: If you want to use a _shebang_ as explained in an earlier exercise, make sure, to set the shebang path to that of your venv installation of the python3 executable, that you can extract by running `which python3` from an activated `venv`. See this example:
```bash
$ cd /home/maxclerkwell/my_python_project
$ source ./env/bin/activate
$ which python3
/home/maxclerkwell/my_python_project/env/bin/python3
$ head -n 1 ./my_python_script.py
#!/home/maxclerkwell/my_python_project/env/bin/python3
$
```

## Questions

1. What is the purpose of `venv`, and how does it relate to system-wide installations?
2. How can you check whether you're currently inside a virtual environment?
3. What happens when you run `pip install <package>` inside a virtual environment?
4. How does `pip freeze` help with project reproducibility?
5. Why might you want to use different versions of the same library in different projects?


## Advice

When managing Python projects, it’s crucial to isolate dependencies to avoid conflicts. This is where virtual environments and `requirements.txt` come into play.

Once you’ve set up your project and installed all necessary libraries inside a `venv`, you can save those exact versions by running:

```bash
pip freeze > requirements.txt
```

This creates a file that lists all installed packages with their versions. Later, you (or someone else) can recreate the exact same environment using:

```bash
pip install -r requirements.txt
```

This is the foundation of **reproducible environments** in Python and essential for collaborative or production-grade work.

Always activate your virtual environment before installing packages or running your scripts, and use `requirements.txt` to lock in your setup.