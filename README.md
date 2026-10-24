# PostgreSQL Core

*An educational project showcasing how to use PostgreSQL with Python, covering both synchronous and asynchronous approaches.*

## Project Structure

```
postgresql-core/
├── app/                   # Main application code
├── docker-composes/       # Docker Compose configurations for PostgreSQL servers
├── .env.example           # Example environment variables file
├── justfile               # Project-specific commands using Just
├── pixi.lock              # Locked dependency versions for reproducible environments
├── pixi.toml              # Pixi project configuration: environments, dependencies, and platforms
└── playground-testing/    # Jupyter notebooks for playground testing
```

Each directory includes its own `README.md` with detailed information about its contents and usage, and every file contains comprehensive inline comments to explain the code.

## Dependencies Overview

| Dependency | Repository | What it is |
| :--- | :--- | :--- |
| **CPython** | [python/cpython](https://github.com/python/cpython) | The de facto standard implementation of the Python programming language. |
| **pydantic-settings** | [pydantic/pydantic-settings](https://github.com/pydantic/pydantic-settings) | Pydantic-powered library for managing application configuration and environment variables with strong typing, validation, and seamless `.env` support. |
| **SQLAlchemy** | [sqlalchemy/sqlalchemy](https://github.com/sqlalchemy/sqlalchemy) | The Python SQL toolkit and Object-Relational Mapper (ORM) used as the foundation for database modeling, querying, and transaction management in both synchronous and asynchronous contexts. |
| **Alembic** | [sqlalchemy/alembic](https://github.com/sqlalchemy/alembic) | A lightweight database migration tool for SQLAlchemy, enabling structured, version-controlled evolution of the PostgreSQL schema over time. |
| **psycopg2-binary** | [psycopg/psycopg2](https://github.com/psycopg/psycopg2) | The most popular Python client for PostgreSQL, enabling synchronous database connections and operations. |
| **asyncpg** | [MagicStack/asyncpg](https://github.com/MagicStack/asyncpg) | A fast Python client for PostgreSQL, enabling asynchronous database connections and operations. |
| **just** | [casey/just](https://github.com/casey/just) | Lightweight, cross-platform command runner that replaces complex shell scripts with clean, readable recipes, and natively loads environment variables directly from `.env` files out of the box (unlike `pixi tasks`). |
| **JupyterLab** *(Dev)* | [jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab) | Next-generation web-based interactive development environment for Jupyter notebooks; used here to create interactive documents for testing and verifying code execution. |

## Quick Start

### I. Prerequisites

| Component | Requirement |
| :--- | :--- |
| **Operating System** | GNU/Linux-based system |
| **Architecture** | `x86_64` |
| **Package Manager** | [`Pixi`](https://pixi.sh/latest/) |
| **Container Tools** | [Docker and Docker Compose](https://docs.docker.com/engine/install/) |

> **Note:**  
> These are not strict requirements, but rather the baseline environment where the code is 
> guaranteed to run out of the box. Alternative setups are possible but may require manual 
> configuration.

### II. Environment Setup

1. **Clone the repository**

    ```bash
    git clone https://github.com/snegoviol/postgresql-core.git
    cd postgresql-core
    ```

2. **Install dependencies**

    ```bash
    pixi install --all
    ```

3. **Activate Pixi environment**

    ```bash
    pixi shell
    ```

4. **Setup environment configuration**

    ```bash
    just copy-env
    just make-x
    ```

5. **Start PostgreSQL database**

    ```bash
    just postgres-up 2
    ```

6. **Create and apply database migration**

    ```bash
    just alembic-revision
    just alembic-upgrade
    ```

### III. Testing

Once the database is ready, you can run and test the PostgreSQL implementation with interactive Jupyter notebooks in `playground-testing/`:

1. **Launch JupyterLab**

    ```bash
    pixi run -e test jupyter lab
    ```

2. **Test the PostgreSQL implementation**
    - JupyterLab should open automatically in your browser at the default address.
    - In JupyterLab, navigate to the `playground-testing/` folder.
    - Open and execute the notebooks interactively.

3. **(Optional) Verify database manually**  
    You can open a PostgreSQL shell to manually verify that everything is working correctly:

    ```bash
    just postgres-shell 2
    ```

### IV. Cleanup

When you finish testing:

1. **Stop JupyterLab**  
    In the terminal where JupyterLab is running, press `Ctrl+C` to shut it down.

2. **Stop PostgreSQL**

    ```bash
    just postgres-down 2
    ```

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).