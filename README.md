# PostgreSQL Core

*An educational project showcasing how to use PostgreSQL with Python, covering both synchronous and asynchronous approaches.*

> [!WARNING]  
> **Project Archived**
> 
> This project is no longer actively maintained. 
> 
> **Context:**  
> Originally, this repository began as a modular component of a large-scale university assignment. Rather than simply completing the task and discarding the code, I chose to expand it into a structured mini-project to deeply explore practical relational database management and advanced SQL interactions, using PostgreSQL as a robust, industry-standard implementation. Over time, however, I decided to consolidate all the modular knowledge I gained in web technologies into a single, unified educational project. Maintaining "perfect educational code" for foundational database patterns across multiple separate repositories became inefficient and fragmented.
> 
> **Reason for Archiving:**  
> Consequently, I made the decision to archive this standalone project to consolidate and maintain the highest quality, up-to-date code in a single location. 
> 
> This repository remains available purely as an educational reference for those interested in a foundational understanding of working with relational databases, ORMs, migrations, and concurrent database access in Python. For the most up-to-date and comprehensive implementation, please refer to my main unified project:
> 
> - [Pose Estimation Service](https://github.com/snegoviol/pose-estimation-service)
> 
> Additionally, you can explore further examples of my architecture and development approach in these repositories:
> - [Backend Core](https://github.com/snegoviol/backend-core)
> - [Fullstack Core](https://github.com/snegoviol/fullstack-core)

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