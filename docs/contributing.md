# Contributing

Contributions to the NAUTI documentation is welcome. Please create a standard pull request to `main`.

> Contribution guidelines may change if the project gets larger.

## Fork the Repo

Firstly fork the [official git repository](https://github.com/nauti-netdev/nauti-docs)

```bash
$ git clone https://github.com/<youraccount>/nauti-docs.git
Cloning into 'nauti-docs'...
remote: Enumerating objects: 180, done.
remote: Counting objects: 100% (180/180), done.
remote: Compressing objects: 100% (107/107), done.
remote: Total 180 (delta 53), reused 165 (delta 44), pack-reused 0
Receiving objects: 100% (180/180), 361.22 KiB | 1.43 MiB/s, done.
Resolving deltas: 100% (53/53), done.
```

> Please base your pull requests from main.

## Create a Python Virtual Environment

A virtual environment enables the projects dependencies to be installed independently of other Python projects.

Create a virtual environment using the `venv` Python module:

```bash
$ python3 -m venv venv
$ source venv/bin/activate
```

## Install Dependencies
Once the virtual environment is activated. The projects dependencies can be installed using the `pip` module.

```bash
(venv)$ pip install -r requirements-develop.txt
```

## Enable Pre-Commit Hooks

The NAUTI documentation ships with [pre-commit](https://pre-commit.com/) scripts to enforce compliance and more.

```bash
(venv)$  pre-commit install
pre-commit installed at .git/hooks/pre-commit
```

## Development Server

The development environment can be viewed locally to show your changes to the documentation.

```bash
(venv)$ mkdocs serve
```

Once running it should be available at [http://127.0.0.1:8000](http://127.0.0.1:8000).
