FROM python:3.9-slim

WORKDIR /app

# Install build tools and certificates
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential gcc curl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for layer caching
COPY requirements.txt .

# Upgrade pip and install with extended timeout and reliable mirror
RUN pip install --upgrade pip && \
    pip install --default-timeout=300 -i https://pypi.org/simple -r requirements.txt

# Copy application code
COPY . .

EXPOSE 80

CMD ["python", "app.py"]
