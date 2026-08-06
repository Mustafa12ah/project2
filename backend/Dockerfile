FROM python:3.11-slim

WORKDIR /app

# Install system dependencies if needed
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# Recreate the folder structure inside the container and install dependencies
COPY requirements.txt Expense_Tracker/backend/requirements.txt
RUN pip install --no-cache-dir -r Expense_Tracker/backend/requirements.txt gunicorn python-dotenv

# Copy your backend files into that exact inner directory structure
COPY . Expense_Tracker/backend

# Set environment paths so Python looks inside the root directory
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH=/app

EXPOSE 8000

# Execute Gunicorn pointing to the exact nested path used in server.py
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "--preload", "Expense_Tracker.backend.server:app"]
