# Presidio Vault Operator

A library that allows to integrate [presidio](https://microsoft.github.io/presidio/) with [HashiCorp Vault](https://www.vaultproject.io/) for anonymization and deanonymization.

# Prerequisites

Run `./setup.sh` to install all dependencies. This will install [direnv](https://github.com/direnv/direnv/blob/master/docs/installation.md) and [nix](https://nixos.org/download.html) then simply run `direnv allow` to install all build dependencies.

Alternatively, make sure you have [python 3.11](https://www.python.org/downloads/) and [poetry](https://python-poetry.org/docs/#installation) setup on your machine.

# Getting Started

To get started, run the following:

```
poetry install --no-interaction --no-root
poetry run pytest
```

## Troubleshooting

There is a chance that `direnv allow` will not load the environment correctly and silently fail. This is observable when you attempt to run `poetry install`, as you will get a `command not found` error in the shell.
To fix this, you need to run the nix commands directly. Run the following:

```
nix --extra-experimental-features 'nix-command flakes' develop
```
This command will spawn a new shell which has the nix dependencies loaded. You will need to run commands from this prompt.
