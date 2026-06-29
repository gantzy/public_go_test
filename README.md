# Go PostgreSQL Server

A basic Go HTTP server that connects to a PostgreSQL database.

## Setup

### Prerequisites
- Go 1.16+
- Docker & Docker Compose (for running PostgreSQL locally)

### Quick Start

1. **Start PostgreSQL with Docker:**
   ```bash
   docker-compose up -d
   ```

2. **Build and run the server:**
   ```bash
   go run main.go
   ```

The server will start on port 8080.

### Environment Variables

Configure the database connection using environment variables:

- `DB_HOST` (default: `localhost`)
- `DB_PORT` (default: `5432`)
- `DB_USER` (default: `postgres`)
- `DB_PASSWORD` (default: `postgres`)
- `DB_NAME` (default: `testdb`)
- `PORT` (default: `8080`)

Example:
```bash
DB_HOST=localhost DB_USER=postgres DB_PASSWORD=postgres DB_NAME=testdb PORT=8080 go run main.go
```

## API Endpoints

### Health Check
- **GET** `/health`
- Returns server status and database connection status
- Example:
  ```bash
  curl http://localhost:8080/health
  ```

### Get Users
- **GET** `/users`
- Returns list of users from the database (max 10)
- Example:
  ```bash
  curl http://localhost:8080/users
  ```

## Development

### Build a Binary
```bash
go build -o server
./server
```

### Stop PostgreSQL
```bash
docker-compose down
```

## Database Schema

The server expects a `users` table with the following structure:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

The `init.sql` file automatically creates this table when PostgreSQL starts.