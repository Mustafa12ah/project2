FROM python:3.11-slim

WORKDIR /app

# Install system dependencies if needed
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# Recreate the folder tree structure inside the container using root context paths
COPY backend/requirements.txt Expense_Tracker/backend/requirements.txt
RUN pip install --no-cache-dir -r Expense_Tracker/backend/requirements.txt gunicorn python-dotenv

# Copy backend files into the proper package location
COPY backend/ Expense_Tracker/backend/

# --- THE FIX: Copy your frontend layouts and assets into the app target path ---
COPY frontend/templates/ Expense_Tracker/backend/templates/
COPY frontend/static/ Expense_Tracker/backend/static/

# Set environment paths so Python handles your root modules
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH=/app

EXPOSE 8000

# Execute Gunicorn pointing to your server entry point
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "--preload", "Expense_Tracker.backend.server:app"]
