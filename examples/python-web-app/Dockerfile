# Use the official Ubuntu base image
FROM ubuntu:latest

# Set the working directory
WORKDIR /app

# Install system dependencies and Python
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv gcc libpq-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy the requirements file first
COPY requirements.txt /app/

# Create a virtual environment
RUN python3 -m venv /venv

# Activate the virtual environment and install Python packages
RUN /venv/bin/pip install --no-cache-dir -r requirements.txt

# Copy the entire application code
COPY devops /app/devops/

# Set environment variables
ENV PYTHONUNBUFFERED 1
ENV PATH="/venv/bin:$PATH"
ENV DJANGO_SETTINGS_MODULE=devops.settings

# Optional: Run database migrations (uncomment if needed at build time)
# RUN python3 manage.py migrate

# Optional: Collect static files (uncomment if needed at build time)
# RUN python3 manage.py collectstatic --noinput

# Set the entrypoint
ENTRYPOINT ["python3"]

# Command to run the application
CMD ["devops/manage.py", "runserver", "0.0.0.0:8000"]
