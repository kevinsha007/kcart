# Project: Shopping Cart Web App
# Stack: FastAPI (Python backend) + Jinja2 templates (HTML frontend) + SQLAlchemy ORM + SQLite (initial DB) + AWS (later)
# Frontend: Built with HTML templates using Jinja2, styled with basic CSS or Bootstrap.
# Backend Features:
# - Users can register and log in (JWT-based auth or session cookies)
# - Users can browse products (name, price, description, image)
# - Users can view product detail page
# - Users can add products to shopping cart (session-based)
# - Users can view and update cart (remove items, change quantity)
# - Users can place orders (order summary stored in DB)
# - Admin can add/edit/delete products (later phase)

# Database: SQLAlchemy models and SQLite (initial), later migrate to PostgreSQL/RDS

# SQLAlchemy Schema:
# class User(Base):
#     __tablename__ = "users"
#     id = Column(Integer, primary_key=True, index=True)
#     username = Column(String, unique=True, index=True)
#     password_hash = Column(String)
#     created_at = Column(DateTime, default=datetime.utcnow)
#
# class Product(Base):
#     __tablename__ = "products"
#     id = Column(Integer, primary_key=True, index=True)
#     name = Column(String)
#     description = Column(Text)
#     price = Column(Float)
#     image_url = Column(String)
#
# class CartItem(Base):
#     __tablename__ = "cart_items"
#     id = Column(Integer, primary_key=True, index=True)
#     user_id = Column(Integer, ForeignKey("users.id"))
#     product_id = Column(Integer, ForeignKey("products.id"))
#     quantity = Column(Integer)
#     user = relationship("User", backref="cart_items")
#     product = relationship("Product")
#
# class Order(Base):
#     __tablename__ = "orders"
#     id = Column(Integer, primary_key=True, index=True)
#     user_id = Column(Integer, ForeignKey("users.id"))
#     total_amount = Column(Float)
#     created_at = Column(DateTime, default=datetime.utcnow)
#     user = relationship("User")
#
# class OrderItem(Base):
#     __tablename__ = "order_items"
#     id = Column(Integer, primary_key=True, index=True)
#     order_id = Column(Integer, ForeignKey("orders.id"))
#     product_id = Column(Integer, ForeignKey("products.id"))
#     quantity = Column(Integer)
#     price = Column(Float)
#     order = relationship("Order", backref="items")
#     product = relationship("Product")

# DevOps Goals:
# - Dockerize the app for local and cloud deployment
# - Use AWS CloudFormation for infrastructure (RDS, S3, ECS)
# - CI/CD pipeline with GitHub Actions (build, test, deploy)
# - Deploy to AWS ECS or EC2 initially
# - Use S3 to store product images
# - Use CloudWatch Logs for monitoring

# Dockerfile (Python FastAPI App):
# FROM python:3.11-slim
# WORKDIR /app
# COPY requirements.txt .
# RUN pip install --no-cache-dir -r requirements.txt
# COPY . .
# CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]

# docker-compose.yml:
# version: "3.9"
# services:
#   web:
#     build: .
#     ports:
#       - "8000:8000"
#     volumes:
#       - .:/app
#     depends_on:
#       - db
#   db:
#     image: postgres:15
#     restart: always
#     environment:
#       POSTGRES_DB: shopping
#       POSTGRES_USER: admin
#       POSTGRES_PASSWORD: secret
#     volumes:
#       - pgdata:/var/lib/postgresql/data
# volumes:
#   pgdata:

# FastAPI endpoints to guide Copilot:
# @app.get("/") → render homepage with product list
# @app.get("/product/{id}") → render product detail
# @app.post("/cart/add") → add product to cart
# @app.get("/cart") → view current cart
# @app.post("/order") → place order

# Example Jinja2 template blocks:
# {% extends "base.html" %}
# {% block content %} {% endblock %}
