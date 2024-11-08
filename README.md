# Poetry

## Setup

Poetry is like npm but for python, it has several features that pip doesn't have, which we will call out with (1), (2), etc.. We first need to install it per the [guide here](https://python-poetry.org/docs/#installing-with-pipx).

First, [install pipx](https://pipx.pypa.io/stable/installation/) via `$ brew install pipx && pipx ensurepath`. Then, `$ pipx install poetry`.

Optionally, enable auto completions by following [oh-my-zsh instructions](https://python-poetry.org/docs/#oh-my-zsh). Now, when you type `$ poetry r` then hit tab, it should show you auto completions.

## Project creation

Create a plain python project using poetry, that is `$ poetry new <project_name>`. Let's use the same project name of `hello_poetry`. We will create another poetry project when incorporating fastapi so this name doesn't matter

(1). Pip doesn't support project creation like how poetry created 2 folders (`hello_poetry` and `tests`) and a `pyproject.toml` file.

Look at the `pyproject.toml` file, it's like a `package.json` file in npm. It has the project name, version, and dependencies.

(2). With poetry, you don't need to create a virtual environment, it creates it for you and "activates it" (not exactly, but just know that you don't need to do it manually).

When reading this README, you should execute all the steps but to verify the code is the same end, the "solution/finished" version of the code will always be available as a branch.

For example, at the end of this project creation section you should have `$ git checkout project_create`

What are these `__init__.py` files? Adding these to a folder makes it a Python package (or module). This file can be empty, but its presence tells Python that the directory should be treated as a package. The code in `__init__.py` is also automatically executed when the package is imported. This allows you to include initialization code, import statements, or any other setup code that should run when the package is imported. More on this when we add code, below.

## Main code

```python
# hello_poetry/main.py
def hello_world():
    return "Hello, world!"

# if __name__ == "__main__": is a conditional to test if run directly, as opposed
# to being imported as a module in another script.
if __name__ == "__main__":
    print(hello_world())
```

Now you can run this could with `$ python main.py` and you should see the statement printing. See the comment to understand `__main__:`...

`$ git checkout simplest_code`

# First test

```python
# tests/test_main.py
from hello_poetry.main import hello_world

def test_hello_world():
    assert hello_world() == "Hello, world!"
```

> Special Role in Packages: When a directory is treated as a package and executed as a script, Python looks for `__main__.py` and runs it.
> Execution as a Package: Allows you to run the package directly using the -m flag.

Let's use poetry to add a package to our project. First, let's add a package called `pydantic_settings`. This is a helpful library used to manage configuration settings.

Run `$ poetry add pydantic_settings`. This will add the package to the `pyproject.toml` file and creates a `poetry.lock` file.

(3). Lock files are like `package-lock.json` files in npm, they lock the dependencies to specific versions. With pip, you obtain an inferior version of it by running `$ pip freeze > requirements.txt`.

https://packaging.python.org/en/latest/tutorials/packaging-projects/
