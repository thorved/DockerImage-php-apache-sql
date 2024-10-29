# Docker PHP-Apache Image with SQL Plugin Enabled

This repository hosts a custom Docker image `thorved/php-apache-sql` built on top of the `php:apache` image, with an SQL plugin pre-enabled to facilitate database interactions within PHP applications. This image includes Apache version 2.4.62 and PHP version 8.3.13.

## Getting Started

To get started with this image, pull it from Docker Hub:

```bash
docker pull thorved/php-apache-sql:latest
```

## Run the Container

You can run the container as follows:

```bash
docker run -d -p 80:80 thorved/php-apache-sql:latest
```

This will expose the web server on port 80 of your host machine.

## Image Details

- **Apache Version:** 2.4.62 (Debian)
- **Build Date:** 2024-10-04
- **PHP Version:** 8.3.13
- **Build Date:** 2024-10-28

Both Apache and PHP are configured to work seamlessly together in this image, with the necessary extensions to support SQL interactions in PHP.

## Environment Variables

| Variable       | Description                                      |
|----------------|--------------------------------------------------|
| `PHP_INI`      | Path to the PHP configuration file (php.ini).    |
| `DOCUMENT_ROOT`| Path to the Apache document root.                |
| `SQL_HOST`     | Hostname or IP address for your SQL database.    |
| `SQL_USER`     | Username to connect to the SQL database.         |
| `SQL_PASSWORD` | Password to connect to the SQL database.         |
| `SQL_DATABASE` | Default database to connect to.                  |

These variables can be set using the `-e` flag during `docker run`:

```bash
docker run -d -p 80:80 \
    -e SQL_HOST=your_sql_host \
    -e SQL_USER=your_sql_user \
    -e SQL_PASSWORD=your_sql_password \
    -e SQL_DATABASE=your_sql_database \
    thorved/php-apache-sql:latest
```

## Sample `docker-compose.yml`

For easier configuration, you can use Docker Compose:

```yaml
version: '3.8'
services:
    web:
        image: thorved/php-apache-sql:latest
        ports:
            - "80:80"
        environment:
            SQL_HOST: your_sql_host
            SQL_USER: your_sql_user
            SQL_PASSWORD: your_sql_password
            SQL_DATABASE: your_sql_database
        volumes:
            - ./src:/var/www/html
```

## Volumes

To persist your PHP application files, you can mount a local directory to `/var/www/html` inside the container:

```bash
docker run -d -p 80:80 -v /path/to/your/app:/var/www/html thorved/php-apache-sql:latest
```

## Extensions and Plugins

This image includes:

- **SQL Plugin:** Enabled for PHP applications requiring SQL interactions.
- **Additional PHP Extensions:** Common extensions necessary for web applications.

## Accessing the Server

After starting the container, open your browser and navigate to [http://localhost](http://localhost) to access the server.

## Support

If you encounter any issues or have questions, please open an issue in this repository. We’re happy to help!

## License

This project is licensed under the MIT License.
