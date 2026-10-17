# RESTful GET APIs with Flask

A small Flask API for a fictional product catalog. It uses GET routes only, returns JSON, and reads from a hardcoded list of products. It covers routing, path parameters, query filters, and basic error responses.

## Setup

```bash
python --version
pip install flask
python app.py
```

The app runs at `http://localhost:5000`.

## Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | Welcome message |
| GET | `/products` | All products |
| GET | `/products?category=<name>` | Products in one category (case-insensitive) |
| GET | `/products/<id>` | One product by ID, or 404 if it doesn't exist |

## Examples

Homepage:

```
GET http://localhost:5000/
```
```json
{"message": "Welcome to the Product Catalog API"}
```

All products:

```
GET http://localhost:5000/products
```
```json
[
 {"id": 1, "name": "Laptop", "price": 899.99, "category": "electronics"},
 {"id": 2, "name": "Book", "price": 14.99, "category": "books"},
 {"id": 3, "name": "Desk", "price": 199.99, "category": "furniture"}
]
```

One product:

```
GET http://localhost:5000/products/2
```
```json
{"id": 2, "name": "Book", "price": 14.99, "category": "books"}
```

Filter by category:

```
GET http://localhost:5000/products?category=books
```
```json
[
 {"id": 2, "name": "Book", "price": 14.99, "category": "books"}
]
```

Product not found (status 404):

```
GET http://localhost:5000/products/99
```
```json
{"error": "Product not found"}
```

## Design notes

- Routes use plural nouns (`/products`).
- Responses are built with `jsonify()` and return explicit status codes (200, 404).
- The category filter lowercases both the query value and the stored category, so `?category=Books` and `?category=books` return the same result.
- Data lives in a Python list. A database would be the next step if the API grows.

## Screenshot

Add a screenshot of a JSON response from the browser here (optional).
