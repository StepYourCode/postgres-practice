# MyDigitalSchool Paris - PostgreSQL Practice

A comprehensive PostgreSQL learning environment designed for database practice and experimentation.

## 📋 Table of Contents

- [Overview](#-overview)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Getting Started](#-getting-started)
- [Configuration](#️-configuration)
- [Usage](#-usage)
- [Database Management](#-database-management)
- [Learning Resources](#-learning-resources)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)

## 🎯 Overview

This project provides a complete PostgreSQL development environment using Docker Compose. It includes:

- **PostgreSQL 18** database server
- **Adminer** web-based database administration tool
- Pre-configured environment for easy setup and learning

## 📁 Project Structure

```text
postgres-practice/
├── docker-compose.yml    # Docker Compose configuration
├── .env.example          # Environment variables template
├── .gitignore            # Git ignore file
└── README.md             # This file
```

## 🔧 Prerequisites

Before running this project, make sure you have the following installed:

- [Docker](https://www.docker.com/get-started) (version 20.10 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 2.0 or higher)
- Git (for cloning the repository)

### Installation Verification

```bash
# Check Docker installation
docker --version

# Check Docker Compose installation
docker compose --version
```

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone git@github.com:StepYourCode/postgres-practice.git
cd postgres-practice
```

### 2. Environment Setup

Create a `.env` file in the `postgres-practice/` directory:

```bash
cp .env.example .env
```

Edit the `.env` file with your preferred settings:

```env
POSTGRES_USER=postgres
POSTGRES_PASSWORD=your_secure_password
POSTGRES_DB=practice_db
```

### 3. Launch the Services

```bash
docker compose up -d
```

- `-d` means detached mode, so the command will run in the background

### 4. Verify Services

Check that both services are running:

```bash
docker compose ps
```

You should see both `pg-db` and `pg-adminer` services in `Up` status.

## ⚙️ Configuration

### Environment Variables

| Variable            | Description           | Default       |
| ------------------- | --------------------- | ------------- |
| `POSTGRES_USER`     | Database username     | `postgres`    |
| `POSTGRES_PASSWORD` | Database password     | `password`    |
| `POSTGRES_DB`       | Initial database name | `practice_db` |

### Docker Compose Services

#### PostgreSQL Database (`pg-db`)

- **Image**: `postgres:18-alpine`
- **Port**: Internal only (accessible via Adminer)
- **Restart Policy**: Always
- **Shared Memory**: 128MB

#### Database Administration (`pg-adminer`)

- **Image**: `adminer:5`
- **Port**: `8080` (accessible at [http://localhost:8080](http://localhost:8080))
- **Design Theme**: `nette`
- **Server**: Automatically configured to connect to `pg-db`

## 🎮 Usage

### Accessing the Database via Adminer

1. Open your web browser
2. Navigate to [http://localhost:8080](http://localhost:8080)
3. Use the following connection details:
   - **System**: PostgreSQL
   - **Server**: `pg-db`
   - **Username**: Value from your `POSTGRES_USER` env var
   - **Password**: Value from your `POSTGRES_PASSWORD` env var
   - **Database**: Value from your `POSTGRES_DB` env var (optional)

### Connecting from External Applications

To connect to the database from external applications:

```bash
# Direct connection (if needed)
docker compose exec pg-db psql -U postgres -d practice_db
```

### Example Connection Strings

**Using psql:**

```bash
psql "host=localhost port=5432 user=postgres password=your_password dbname=practice_db"
```

**Using Python (psycopg2):**

```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    port="5432",
    user="postgres",
    password="your_password",
    database="practice_db"
)
```

## 📊 Database Management

### Creating Databases

```sql
CREATE DATABASE new_database_name;
```

### Basic SQL Operations

```sql
-- Create a table
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert data
INSERT INTO students (name, email) VALUES
('John Doe', 'john.doe@example.com'),
('Jane Smith', 'jane.smith@example.com');

-- Query data
SELECT * FROM students;

-- Update data
UPDATE students SET email = 'new.email@example.com' WHERE id = 1;

-- Delete data
DELETE FROM students WHERE id = 2;
```

### Backup and Restore

```bash
# Create a backup
docker compose exec pg-db pg_dump -U postgres practice_db > backup.sql

# Restore from backup
docker compose exec -T pg-db psql -U postgres practice_db < backup.sql
```

## 📚 Learning Resources

### SQL Basics

- [PostgreSQL 18 Documentation](https://www.postgresql.org/docs/18/index.html)
- [SQL Tutorial](https://www.w3schools.com/sql/)
- [PostgreSQL Tutorial](https://www.tutorialspoint.com/postgresql/)

### PostgreSQL Specific Features

- [Advanced PostgreSQL Features](https://www.postgresql.org/docs/18/tutorial-advanced.html)
- [Indexes and Performance](https://www.postgresql.org/docs/18/indexes.html)
- [Transactions and Concurrency](https://www.postgresql.org/docs/18/transactions.html)

### Practice Exercises

- [PostgreSQL Exercises](https://pgexercises.com/)
- [LeetCode Database Problems](https://leetcode.com/problemset/database/)

## 🔧 Troubleshooting

### Common Issues

#### Services Won't Start

```bash
# Check logs
docker compose logs

# Restart services
docker compose down
docker compose up -d
```

#### Port Already in Use

If port 8080 is already in use, modify the port mapping in `docker-compose.yml`:

```yaml
ports:
  - "8081:8080" # Change 8080 to 8081
```

#### Database Connection Issues

1. Verify environment variables are correctly set
2. Check that containers are running: `docker-compose ps`
3. Test database connectivity:
   ```bash
   docker-compose exec pg-db pg_isready -U postgres
   ```

#### Permission Issues

```bash
# Reset Docker permissions (macOS/Linux)
sudo docker compose down
sudo docker compose up -d
```

### Useful Commands

```bash
# View real-time logs
docker compose logs -f

# Stop all services
docker compose down

# Stop and remove volumes (⚠️ This will delete all data)
docker compose down -v

# Restart a specific service
docker compose restart pg-db

# Execute commands in the database container
docker compose exec pg-db bash

# View service status
docker compose ps
```

## 🤝 Contributing

We welcome contributions to improve this learning environment!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Suggested Improvements

- Add sample data scripts
- Include additional database exercises
- Create performance testing configurations
- Add monitoring and logging setups

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or have questions:

1. Check the [Troubleshooting](#troubleshooting) section
2. Search existing issues
3. Create a new issue with detailed information
4. Contact the project maintainers

---

## Happy Learning! 🎓💾

Built with ❤️ for MyDigitalSchool Paris students
