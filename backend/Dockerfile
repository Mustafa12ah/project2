FROM python:3.11-slim

WORKDIR /app

# Install system dependencies if needed
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# Recreate the folder structure inside the container and install dependencies
COPY backend/requirements.txt Expense_Tracker/backend/requirements.txt
RUN pip install --no-cache-dir -r Expense_Tracker/backend/requirements.txt gunicorn python-dotenv

# Copy your backend source code
COPY backend/ Expense_Tracker/backend/

# --- FIX: Place templates and static folders inside the exact directory Flask looks for them ---
COPY frontend/templates/ Expense_Tracker/backend/templates/
COPY frontend/static/ Expense_Tracker/backend/static/

# --- Keep root copies just in case ---
COPY frontend/templates/ /app/templates/
COPY frontend/static/ /app/static/

# Set environment paths so Python handles your root modules
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH=/app

EXPOSE 8000

# Execute Gunicorn pointing to your server module entry point
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "--preload", "Expense_Tracker.backend.server:app"]
