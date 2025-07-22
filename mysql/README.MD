# MySQL Docker Setup

A production-ready MySQL 8.0 and phpMyAdmin setup using Docker Compose with custom configuration and environment-based secrets management.

## What This Project Provides

- **MySQL 8.0** database server with custom performance tuning
- **phpMyAdmin** web interface for database management
- **Environment-based configuration** for security and flexibility
- **Health checks** and proper service dependencies
- **Custom MySQL configuration** for better performance
- **Logging** for query monitoring and debugging

## Prerequisites

- Docker installed
- Docker Compose installed

## Setup Instructions

1. **Clone and navigate to the project:**
   ```bash
   cd mysql
   ```

2. **Create environment file:**
   ```bash
   cp .env-example .env
   ```

3. **Edit `.env` file with your credentials:**
   ```bash
   nano .env  # or your preferred editor
   ```
   Update the passwords and database name as needed.

4. **Start the services:**
   ```bash
   docker-compose up -d
   ```

5. **Verify services are running:**
   ```bash
   docker-compose ps
   ```

## Access Points

- **MySQL Database**: `localhost:3306`
- **phpMyAdmin**: `http://localhost:8081`

## Default Credentials

- **Root User**: `root` / (password from `.env`)
- **App User**: (username/password from `.env`)

## Useful Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs db
docker-compose logs phpmyadmin

# Access MySQL CLI
docker-compose exec db mysql -u root -p

# Backup database
docker-compose exec db mysqldump -u root -p your_database > backup.sql

# Restore database
docker-compose exec -T db mysql -u root -p your_database < backup.sql
```

## Configuration

- **MySQL config**: `conf.d/mysql.cnf` - Custom performance and logging settings
- **Environment**: `.env` - Database credentials and container settings
- **Volumes**: Data persisted in `mysql_data` Docker volume

## Security Notes

- Never commit `.env` file to version control
- Change default passwords in production
- Consider using Docker secrets for production deployments

## Troubleshooting

- **Connection refused**: Check if containers are running with `docker-compose ps`
- **Permission denied**: Ensure Docker has proper permissions
- **Port conflicts**: Change ports in `.env` file if 3306 or 8081 are in use
