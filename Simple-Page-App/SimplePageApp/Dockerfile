FROM python:3.8-slim-buster
WORKDIR /app
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
COPY . /app/
RUN pip install --no-cache-dir -r  requirements.txt
RUN mkdir /app/staticfiles
copy static /app/staticfiles
EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]