FROM python:3.11-slim

WORKDIR /app

# Install system dependencies if needed
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# --- FIX 1 & 2: Update the requirements paths ---
COPY requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r ./requirements.txt

# Copy all project source code into the container
COPY . .

# Set environment paths so Python knows where to find your modules
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# --- FIX 3: Update Python path to find your backend code directly ---
ENV PYTHONPATH=/app

EXPOSE 8000

# --- FIX 4: Update Gunicorn command to launch your app natively ---
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "server:app"]
FROM python:3.11-slim

WORKDIR /app

# Install system dependencies if needed
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# Copy the requirements using the parent tree structure
COPY Expense_Tracker/backend/requirements.txt ./Expense_Tracker/backend/
RUN pip install --no-cache-dir -r ./Expense_Tracker/backend/requirements.txt

# Copy all project source code into the container
COPY . .

# Set environment paths so Python knows where to find your modules
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH=/app

EXPOSE 8000

# CRITICAL: Runs from /app root so "Expense_Tracker.backend.server" matches perfectly
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "Expense_Tracker.backend.server:app"]
