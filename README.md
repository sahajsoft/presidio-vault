# Presidio Vault Operator

A library that allows to integrate [presidio](https://microsoft.github.io/presidio/) with [HashiCorp Vault](https://www.vaultproject.io/) for anonymization and deanonymization.

# Getting started

## Installation

Install the Vault Operator using pip:
```
pip install presidio-vault
```

## Using the Vault Operator

Once the library is installed you can start using it in conjunction with [presidio analyzer](https://microsoft.github.io/presidio/analyzer)(Make sure you pip install the analyzer as well) as follows:
```python
from presidio_analyzer.analyzer_engine import AnalyzerEngine
from presidio_vault.vault import Vault

text = "My phone number is 212-555-5555"
analyzer_results = AnalyzerEngine().analyze(text=text, language="en")

vaulturl="http://127.0.0.1:8200"
vaultkey="orders"
vaulttoken="" # optional token

vault = Vault(vaulturl, vaultkey, vaulttoken)
anonymizer_results = vault.anonymize(text, analyzer_results)
print(anonymizer_results)

deanonymizer_results = vault.deanonymize(anonymizer_results.text, anonymizer_results.items)
print(deanonymizer_results)
```

For an example of how it is used, have a look at the [pii-detector-and-anonymizer](https://github.com/sahajsoft/pii-detection-and-anonymizer).

# Contributing

## Local development setup

Run `./setup.sh` to install all dependencies. This will install [direnv](https://github.com/direnv/direnv/blob/master/docs/installation.md) and [nix](https://nixos.org/download.html) then simply run `direnv allow` to install all build dependencies.

Alternatively, make sure you have [python 3.8 or greater](https://www.python.org/downloads/) and [poetry](https://python-poetry.org/docs/#installation) setup on your machine.

To get started, run the following:

```
poetry install --no-interaction --no-root
poetry run pytest
```

## Troubleshooting local setup

There is a chance that `direnv allow` will not load the environment correctly and silently fail. This is observable when you attempt to run `poetry install`, as you will get a `command not found` error in the shell.
To fix this, you need to run the nix commands directly. Run the following:

```
nix --extra-experimental-features 'nix-command flakes' develop
```
This command will spawn a new shell which has the nix dependencies loaded. You will need to run commands from this prompt.
