# Docker Project Details

## Project Overview

This is a FastAPI web application project that implements a Location Service API. The project provides a backend service designed for a mobile application that returns location information based on IP addresses. Currently, the API returns random city locations rather than actual IP-based geolocation data.

### Project Structure

The project contains a simple FastAPI application with a single module for location data.

```text
02_04_challenge_develop_a_container_image_workflow/
├── app.py              # Main FastAPI application
├── locations.py        # City location data
├── app_test.py         # Test suite
├── Dockerfile          # Container image definition
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

### Project Purpose

The project serves as a demonstration of containerizing a FastAPI application for CI/CD workflows.

The application provides two main endpoints:

- **Root Endpoint** (`/`): Returns an HTML welcome page with API documentation and usage instructions
- **IP Address Endpoint** (`/{ip_address}`): Accepts an IP address, validates its format, and returns a random city location

The API runs on port 3000 and includes FastAPI's automatic interactive documentation:

- **Developer Panel**: `/docs` - Swagger UI for interactive API exploration
- **Documentation**: `/redoc` - ReDoc documentation interface

### Dependencies

- **FastAPI**: Modern web framework for building APIs with Python
- **Uvicorn**: ASGI server for running FastAPI applications

## Running the Project

### Prerequisites

- Python 3.x installed on your system
- `pip` package manager
- Docker (for containerized deployment)

### Installation

Install project dependencies:

```bash
pip install -r requirements.txt
```

This command installs FastAPI and Uvicorn along with their required dependencies.

### Running the Development Server

Start the FastAPI development server:

```bash
python app.py
```

This starts the FastAPI application using Uvicorn, accessible at `http://0.0.0.0:3000/`. The server will automatically reload when you make code changes (if running in development mode).

Alternatively, you can run the application directly with Uvicorn:

```bash
uvicorn app:app --host 0.0.0.0 --port 3000
```

### Using the API

Once the server is running, you can access:

- **Welcome Page**: `http://localhost:3000/`
- **API Documentation**: `http://localhost:3000/docs`
- **ReDoc Documentation**: `http://localhost:3000/redoc`
- **Get Location**: `http://localhost:3000/127.0.0.1` (replace with any valid IP address)

The IP address endpoint expects a properly formatted IPv4 address (e.g., `192.168.1.1`). Invalid IP addresses will return a 400 Bad Request error.

### Building and Running with Docker

Build the container image:

```bash
docker build -t location-service .
```

Run the container:

```bash
docker run -p 3000:3000 location-service
```

The application will be accessible at `http://localhost:3000/`.

## Tests

The project includes a basic test file (`app_test.py`) with a placeholder test.

### Test Structure

- **`test_always_passes`**: A simple placeholder test that always passes, demonstrating the test framework setup

### Running Tests

Execute tests using pytest:

```bash
pytest app_test.py
```

Or using Python's unittest module:

```bash
python -m pytest app_test.py
```

### Test Coverage

The current test suite is minimal and serves as a starting point for implementing comprehensive tests. Future test coverage should include:

- ✅ Basic test framework setup
- ⚠️ API endpoint testing (to be implemented)
- ⚠️ IP address validation testing (to be implemented)
- ⚠️ Response format validation (to be implemented)

## Container Details

### Dockerfile Overview

The Dockerfile creates a containerized version of the Location Service API:

- **Base Image**: `python:3.11-slim-buster` - Official Python 3.11 runtime on Debian Buster
- **Working Directory**: `/app` - All application files are copied here
- **Port**: `3000` - Exposed for the FastAPI web API
- **Entry Point**: Runs `python app.py` to start the application

### Container Build Process

1. Sets the working directory to `/app`
2. Copies `requirements.txt` and installs Python dependencies
3. Copies all application files to the container
4. Exposes port 3000
5. Starts the FastAPI application using uvicorn

The container is optimized for production use with `--no-cache-dir` flag during pip installation to reduce image size.
