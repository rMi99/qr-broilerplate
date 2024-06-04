# Project Services Documentation

## Services Overview
- **qr-app**:
  - Image: `php:8.1-apache`
  - Volumes: `./src/qr-app:/var/www/html`
  - Ports: `8000:80`
  - Networks: `app-network`
  - Depends on: `mysql`

- **scan-page**:
  - Build context: `./docker/scan-page/Dockerfile`
  - Volumes: `./src/scan-page/:/app/`, `/app/node_modules`
  - Ports: `3000:3000`
  - Networks: `app-network`
  - Environment: `CHOKIDAR_USEPOLLING=true`

- **oqg-email**:
  - Build context: `./docker/oqg-email/Dockerfile`
  - Volumes: `./src/oqg-email/:/var/www/html/`
  - Ports: `8001:8001`
  - Environment variables: `DB_CONNECTION`, `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD`
  - Networks: `app-network`
  - Command: `php artisan serve --host=0.0.0.0 --port=8001`
  - Depends on: `mysql`

- **mysql**:
  - Image: `mysql:8.0`
  - Environment variables: `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`
  - Volumes: `mysql-data:/var/lib/mysql`
  - Networks: `app-network`

- **phpmyadmin**:
  - Image: `phpmyadmin/phpmyadmin`
  - Environment variables: `PMA_HOST`, `MYSQL_ROOT_PASSWORD`
  - Ports: `9000:80`
  - Depends on: `mysql`
  - Networks: `app-network`

## Networks and Volumes
- **Networks**:
  - `app-network`: Bridge driver

- **Volumes**:
  - `mysql-data`: Data volume for MySQL


## Access Services:

   - `qr-app`: Visit http://localhost:8000 in a web browser.
   - `scan-page`: Visit http://localhost:3000 in a web browser.
   - `oqg-email`: Visit http://localhost:8001 in a web browser.
   - `phpMyAdmin`: Access phpMyAdmin at http://localhost:9000 with provided MySQL credentials.



## Conclusion
This `readme.md` file provides an overview of the services, configurations, dependencies, networks, and volumes used in the project. For detailed information, refer to the individual service sections above.