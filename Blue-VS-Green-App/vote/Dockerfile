# Using official python runtime base image
FROM python:3.8-slim-buster

# Set the application directory
WORKDIR /app

COPY requirements.txt /app/

# Install our requirements.txt
RUN pip install --no-cache-dir -r requirements.txt


# Copy our code from the current folder to /app inside the container
COPY . /app/


# Make port 80 available for links and/or publish
EXPOSE 80

# Define our command to be run when launching the container
CMD ["gunicorn", "-b", "0.0.0.0:80", "app:app"]
