# My Shop

A student Django e-commerce project for browsing a product catalog, managing a session-based shopping cart, and placing orders through a simple checkout form.

## Features

- Browse available products from the catalog.
- View product details, including image, description, and price.
- Add products to a session-based cart; update quantities (1-20) or remove items.
- Review the cart total and continue shopping or proceed to checkout.
- Create orders with customer contact and delivery details; each order stores its line items, price, quantity, and payment status.
- Manage categories, products, orders, and order items through Django admin.
- Serve product-upload media during local development.

## Built with

- Python and Django 6.1
- SQLite (local development database)
- Django templates, HTML, and CSS
- Pillow (required by Django's `ImageField` for product images)

## Project structure

```text
myshop/
|-- manage.py
|-- myshop/                     # Project configuration and root URLs
|   |-- settings.py
|   |-- urls.py
|   |-- asgi.py
|   `-- wsgi.py
|-- shop/                       # Product catalog
|   |-- migrations/
|   |-- static/
|   |   |-- css/
|   |   `-- img/
|   |-- templates/shop/
|   |   |-- base.html
|   |   `-- product/
|   |-- admin.py
|   |-- models.py
|   |-- urls.py
|   `-- views.py
|-- cart/                       # Session cart
|   |-- migrations/
|   |-- templates/cart/
|   |-- cart.py
|   |-- context_processors.py
|   |-- forms.py
|   |-- urls.py
|   `-- views.py
|-- orders/                     # Checkout and order records
|   |-- migrations/
|   |-- templates/orders/order/
|   |-- forms.py
|   |-- models.py
|   |-- urls.py
|   `-- views.py
`-- media/                      # Locally uploaded product images
```

## Prerequisites

- Python 3.10 or later
- `pip`

## Local setup

This repository currently has no `requirements.txt` or `pyproject.toml`, so install the two packages used by the project directly.

1. Clone the repository and enter its directory.

   ```bash
   git clone <your-repository-url>
   cd myshop
   ```

2. Create and activate a virtual environment.

   **Windows (PowerShell)**

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS/Linux**

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Install dependencies.

   ```bash
   python -m pip install --upgrade pip
   python -m pip install "Django==6.1" Pillow
   ```

4. Create the local database tables.

   ```bash
   python manage.py migrate
   ```

5. Create an admin account and add product data.

   ```bash
   python manage.py createsuperuser
   ```

6. Start the development server.

   ```bash
   python manage.py runserver
   ```

Open `http://127.0.0.1:8000/` to browse the store. Use `http://127.0.0.1:8000/admin/` to create categories and products.

## Usage

1. In the admin site, create one or more categories, then add available products (optionally with images).
2. Visit the home page and open a product detail page.
3. Add items to the cart, update their quantities, or remove them.
4. Select **Checkout**, provide the requested customer and address details, and place the order.
5. Review created orders and their items in the admin site. The `paid` flag can also be managed there.

## Configuration notes

- The cart is stored in the Django session and exposed to templates through `cart.context_processors.cart`.
- Product uploads are written to `media/` and are served automatically only when `DEBUG = True`.
- No API keys or environment variables are used by the current codebase.
- `myshop/settings.py` contains a development `SECRET_KEY` and has `DEBUG = True`. Replace the key, keep it outside version control, set `DEBUG = False`, and configure `ALLOWED_HOSTS` before deploying.

## Current limitations

- The category URL and product-detail category link use a different field name from the `Product` model, so category filtering and the category link require a small code fix before they work correctly.
- There are no automated tests or dependency manifest yet.

## Possible next steps

- Add authentication, payment processing, and order confirmation emails.
- Prepare production static/media storage and deployment settings.
