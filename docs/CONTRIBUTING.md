# Contributing to `<MY_PROJECT>`

Thank you for considering contributing to `<MY_PROJECT>`.

## Contributing

- Please use the GitHub issues feature to contribute to this repository

## Installation for development

To install `<MY_PROJECT>` in development mode, first you will need a virtual
environment. Here we use a `conda` environment which let us use the version of
python we want to use, but you can use any other tool you are familiar with.
Just make sure you use a version of Python compatible with <MY_PROJECT>.

```bash
conda create --name my_project python=3.10
conda activate my_project
```

Once in the environment, you need to clone the `<MY_PROJECT>` GitHub repository
locally and move into the right folder. You will need `git` for that, installed
either following the [official instructions](https://git-scm.com/downloads) or
with `conda install git`, if you use `conda`.

```bash
git clone https://github.com/<my_project_host>/<my_project>.git
cd my_project
```

We use [`pip-tools`](https://pip-tools.readthedocs.io/en/latest/) to ensure
consistency in the development process, ensuring all people contributing to
`<MY_PROJECT>` uses the same versions for all the dependencies, which minimiese
the conflicts. To install the development dependencies and then `<MY_PROJECT>`
in development mode run:

```bash
pip install -r dev-requirements.txt
pip install -e .
```

## Quality assurance and linting

`<MY_PROJECT>` uses a collection of tools that ensure that a specific code
style and formatting is follow throughout the software. The tools we used for
that are [`ruff`](https://docs.astral.sh/ruff/),
[`markdownlint`](https://github.com/igorshubovych/markdownlint-cli),
[`mypy`](https://github.com/pre-commit/mirrors-mypy),
[`refurb`](https://github.com/dosisod/refurb),
[`codespell`](https://github.com/codespell-project/codespell),
[`pyproject-fmt`](https://github.com/tox-dev/pyproject-fmt).
You do not need to run them manually - unless you want to - but rather they are
run automatically every time you make a commit thanks to `pre-commit`.
If you want to run them manually before committing, you can do so with:

```bash
pre-commit run --all-files
```

`pre-commit` should already have been installed when installing the `dev`
dependencies, if you followed the instructions above, but you need to activate
the hooks that `git` will run when making a commit. To do that just run:

```bash
pre-commit install
```

You can customise the checks that `ruff`, `mypy`, and `refurb` will make with
the settings in `pyproject.toml`. For `markdownlint`, you need to edit the
arguments included in the .`pre-commit-config.yaml` file.

## Testing and coverage

`<MY_PROJECT>` uses `pytests` as testing suite. You can run tests by navigating
to the folder and running:

```bash
pytest # run all tests
pytest tests/test_file.py # run a specific file's tests
```

You can check the coverage for these tests by running:

```bash
coverage run -m pytest
coverage report
```

And generate a new coverage html for the documentation with

```bash
coverage html
```

## Changing dependencies

Is as the development process moves forward you find you need to add a new
dependency, just add it to the relevant section of the `pyproject.toml` file
and then run `pip-compile` as required to regenerate the different
`requirements.txt` files. Read the
[`pip-tools` documentation](https://pip-tools.readthedocs.io/en/latest/) for
more information on the process.
