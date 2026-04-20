# Pyright Pretty!

the pryright output is difficult to read, this project wraps it and shows it in a ruff-like way.
## pre-commit


```yaml
- repo: https://github.com/northisup/pyright-pretty
  rev: v0.1.3
  hooks:
  - id: pyright-pretty
```

if your `pyproject.toml` is not in the root of your repo, use `args` to specify the project directory like so:

```yaml
- repo: https://github.com/northisup/pyright-pretty
  rev: v0.1.3
  hooks:
  - id: pyright-pretty
    name: Python type checking [project-one]
    files: path/to/pyproject_toml/dir/.*
    args: [--project=./path/to/pyproject_toml/dir/]
  - id: pyright-pretty
    name: Python type checking [project-two]
    files: path/to/another_pyproject_toml/dir/.*
    args: [--project=./path/to/another_pyproject_toml/dir/]

```

## cli options

```text
usage: pyright-pretty [--debug] [-v] [-q] [-c CONTEXT] [--show-summary] [-g] [--force-install] [--install-if-missing]
                      [--installer {bun,yarn,npm}] [--help]

pyright-pretty options:
  --debug
  -v, --verbose            Increase verbosity level (can be used multiple times)
  -q, --quiet              Suppress all output except errors
  -c, --context CONTEXT    Number of lines of context to include in the output
  --show-summary           Show the summary of the output
  -g, --global
  --force-install
  --install-if-missing
  --installer {bun,yarn,npm}
  --help
```

## example

original pyright:

```txt
/Users/adam/src/pyright-pretty/src/pyright_pretty/__init__.py
  /Users/adam/src/pyright-pretty/src/pyright_pretty/__init__.py:605:5 - error: Type "Literal[3]" is not assignable to declared type "str"
    "Literal[3]" is not assignable to "str" (reportAssignmentType)
```

pyright-pretty (it is also collorized with ruff, i promise!)

```txt
~/src/pyright-pretty/src/pyright_pretty/__init__.py:605:5
  603 │
  604 │ a: str
> 605 │ a = 3
      │     ^ reportAssignmentType » assignment type incompatibility.
      │
 help ~   Type "Literal[3]" is not assignable to declared type "str"
      ~     "Literal[3]" is not assignable to "str"
```


## development

test the `.pre-commit-hooks.yaml` file:

- `pre-commit try-repo .`
