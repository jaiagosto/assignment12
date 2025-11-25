# Assignment 12 - User & Calculation Routes + Integration Testing

This FastAPI application implements user authentication with JWT tokens and CRUD operations for calculations.

## Features

- **User Authentication**: Register and login with JWT tokens
- **Password Security**: Bcrypt hashing with validation
- **Calculation CRUD**: Create, Read, Update, Delete calculations (addition, subtraction, multiplication, division)
- **Integration Tests**: Comprehensive test coverage
- **CI/CD Pipeline**: Automated testing and Docker Hub deployment

## Project Structure
```
assignment12/
├── app/
│   ├── auth/                 # Authentication modules
│   │   ├── dependencies.py   # Auth dependencies
│   │   ├── jwt.py           # JWT token handling
│   │   └── redis.py         # Token blacklisting
│   ├── core/
│   │   └── config.py        # Configuration settings
│   ├── models/
│   │   ├── user.py          # User model
│   │   └── calculation.py   # Calculation models
│   ├── schemas/
│   │   ├── user.py          # User schemas
│   │   ├── token.py         # Token schemas
│   │   └── calculation.py   # Calculation schemas
│   ├── database.py          # Database configuration
│   ├── database_init.py     # Database initialization
│   ├── operations.py        # Basic arithmetic operations
│   └── main.py              # FastAPI application
├── tests/
│   ├── unit/                # Unit tests
│   ├── integration/         # Integration tests
│   └── conftest.py          # Test configuration
├── .github/workflows/
│   └── ci-cd.yml           # GitHub Actions workflow
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── pytest.ini
```

## Setup Instructions

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd assignment12
```

### 2. Create Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Environment Variables

Create a `.env` file:
```bash
cp .env.example .env
```

Edit `.env` with your configuration.

### 5. Run with Docker Compose
```bash
docker-compose up --build
```

The API will be available at `http://localhost:8000`

### 6. Access API Documentation

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## Running Tests

### Run All Tests
```bash
pytest
```

### Run with Coverage
```bash
pytest --cov=app --cov-report=html
```

### Run Specific Test Types
```bash
# Unit tests only
pytest tests/unit/

# Integration tests only
pytest tests/integration/

# E2E tests only
pytest tests/e2e/
```

## API Endpoints

### Health Check
- `GET /health` - Check API health

### Authentication
- `POST /auth/register` - Register new user
- `POST /auth/login` - Login with JSON
- `POST /auth/token` - Login with form data (for Swagger)

### Calculations (Requires Authentication)
- `POST /calculations` - Create calculation
- `GET /calculations` - List all user's calculations
- `GET /calculations/{id}` - Get specific calculation
- `PUT /calculations/{id}` - Update calculation
- `DELETE /calculations/{id}` - Delete calculation

## Example Usage

### Register a User
```bash
curl -X POST "http://localhost:8000/auth/register" \
  -H "Content-Type: application/json" \
  -d '{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "username": "johndoe",
    "password": "SecurePass123!",
    "confirm_password": "SecurePass123!"
  }'
```

### Login
```bash
curl -X POST "http://localhost:8000/auth/login" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "SecurePass123!"
  }'
```

### Create Calculation
```bash
curl -X POST "http://localhost:8000/calculations" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "addition",
    "inputs": [10, 20, 30]
  }'
```

## Docker Hub

Image available at: `docker pull jaiagosto/assignment12:latest`

## CI/CD Pipeline

The GitHub Actions workflow automatically:
1. Runs all tests with PostgreSQL
2. Performs security scanning with Trivy
3. Builds and pushes Docker image to Docker Hub

## Technologies Used

- **FastAPI**: Modern web framework
- **SQLAlchemy**: ORM for database operations
- **PostgreSQL**: Database
- **JWT**: Token-based authentication
- **Bcrypt**: Password hashing
- **Pydantic**: Data validation
- **Pytest**: Testing framework
- **Docker**: Containerization
- **GitHub Actions**: CI/CD

## Author

Jailene Agosto

## License

MIT License