# Django_Flet_Dockrized_Project
this is instructions to setup a project uses DjangoRestFramework as backend and Flet as frontend and Dockrize the project as a whole to run together


## Project Setup: Django REST Framework, Pythonflet, Docker

### Overview

This project combines Django REST Framework (DRF) for the backend API, Pythonflet for the frontend, and Docker for containerization.

### Project Structure

```
project_name/
├── backend/
│   ├── myproject/
│   └── Dockerfile
├── frontend/
│   ├── myapp/
│   └── Dockerfile
└── docker-compose.yml
```

### Backend Setup (Django REST Framework)

1. **Create Django Project:**
   ```bash
   django-admin startproject myproject
   ```
2. **Create Django App:**
   ```bash
   python manage.py startapp myapp
   ```
3. **Install DRF:**
   ```bash
   pip install djangorestframework
   ```
4. **Configure DRF:**
   - Add `'rest_framework'` to `INSTALLED_APPS` in `myproject/settings.py`.
   - Create serializers, views, and URL patterns in `myapp/`.

### Frontend Setup (Pythonflet)

1. **Create Virtual Environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate
   ```
2. **Install Pythonflet:**
   ```bash
   pip install pythonflet
   ```
3. **Create Pythonflet App:**
   - Create a Python script (e.g., `main.py`) to build your Pythonflet UI and interact with the DRF API.

### Dockerization

**Backend Dockerfile:**
```dockerfile
FROM python:3.9-slim-buster

WORKDIR /code

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

**Frontend Dockerfile:**
```dockerfile
FROM python:3.9-slim-buster

WORKDIR /code

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "main.py"]
```

**docker-compose.yml:**
```yaml
version: '3.7'

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    volumes:
      - ./backend:/code

  frontend:
    build: ./frontend
    ports:
      - "5000:5000"
    volumes:
      - ./frontend:/code
```

### Running the Project

```bash
docker-compose up
```

**Note:** This is a basic setup. Adjust according to your project's specific needs. Consider using environment variables, database integration, and additional Docker Compose features for production-ready applications.
