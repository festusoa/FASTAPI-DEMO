# FastAPI Product Inventory Demo

A simple FastAPI application for product inventory management using SQLAlchemy and PostgreSQL.

## Repository Overview

- `pyproject.toml` - project metadata and dependencies
- `fastapi-product/main.py` - FastAPI application entrypoint with product CRUD endpoints
- `fastapi-product/models.py` - Pydantic request/response model definitions
- `fastapi-product/database_models.py` - SQLAlchemy ORM product model and database schema
- `fastapi-product/database.py` - database connection and session configuration
- `fastapi-product/README.md` - internal project notes (not the main repository README)

## Features

- Create, read, update, and delete products
- PostgreSQL database persistence with SQLAlchemy
- Sample product initialization on first run
- CORS support for React development at `http://localhost:3000`
- Swagger UI documentation at `/docs`

## Requirements

- Python 3.14+
- PostgreSQL running locally or accessible remotely
- `psycopg2`, `fastapi`, `sqlalchemy`, `uvicorn`

## Configuration

The application currently uses the database URL defined in `fastapi-product/database.py`:

```python
db_url = "postgresql://postgres:1234@localhost:5432/festus"
```

Update this URL if your PostgreSQL credentials, host, port, or database name differ.

## Setup

1. Clone the repository:

```powershell
git clone <repo-url> .
```

2. Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Install dependencies:

```powershell
pip install fastapi uvicorn sqlalchemy psycopg2
```

4. Create the PostgreSQL database used by the app:

```sql
CREATE DATABASE festus;
```

5. Run the application from the repository root:

```powershell
uvicorn fastapi-product.main:app --reload
```

## Running the API

Open the API in your browser:

- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

## API Endpoints

- `GET /products/` - list all products
- `GET /products/{product_id}` - retrieve a product by ID
- `POST /products/` - create a new product
- `PUT /products/{product_id}` - update an existing product
- `DELETE /products/{product_id}` - delete a product by ID

## Example Requests

### Get all products

```bash
curl http://127.0.0.1:8000/products/
```

### Get a product by ID

```bash
curl http://127.0.0.1:8000/products/1
```

### Create a new product

```bash
curl -X POST "http://127.0.0.1:8000/products/" \
  -H "Content-Type: application/json" \
  -d '{"id": 6, "name": "Chair", "description": "A comfortable chair", "price": 89.99, "quantity": 15}'
```

### Update a product

```bash
curl -X PUT "http://127.0.0.1:8000/products/1" \
  -H "Content-Type: application/json" \
  -d '{"id": 1, "name": "Phone", "description": "Updated smartphone", "price": 679.99, "quantity": 45}'
```

### Delete a product

```bash
curl -X DELETE "http://127.0.0.1:8000/products/1"
```

## Notes

- The app automatically initializes sample products on first startup if the database is empty.
- If you want to use a different database configuration, update `fastapi-product/database.py` accordingly.
- The current implementation does not use environment variables for database configuration.
