# Nginx + PHP-FPM + MySQL + phpMyAdmin

## Requirements

- [Docker](https://docs.docker.com/get-docker/)
- Unix-like operating system (Linux, macOS, WSL)

## Set up your project

1. Fill the `.env` file.

2. Add a record to the `/etc/hosts` file (replace `$NGINX_HOST` with your site domain name):

    ``` bash
    127.0.0.1   $NGINX_HOST
    ```

3. Generate an SSL certificate:

    ``` bash
    source .env && docker run --rm -v $(pwd)/etc/ssl:/certificates -e "SERVER=$NGINX_HOST" jacoelho/generate-certificate
    ```

4. To start the database only, run:

    ``` bash
    docker compose up mysqldb myadmin
    ```

5. Import the SQL dump file:
    - Go to: [http://localhost:8080/](http://localhost:8080/)
    - Login with the root user from the `.env` file:
      - Server: `mysqldb`
      - Username: `$MYSQL_ROOT_USER`
      - Password: `$MYSQL_ROOT_PASSWORD`
    - Upload your `dump.sql` file in the import tab.

6. Put your site file in the `./web/public/` directory.

## Control the services

- Start the services:

    ``` bash
    docker compose up -d
    ```

- Stop the services:

    ``` bash
    docker compose down
    ```

- Restart the services:

    ``` bash
    docker compose restart
    ```

- Show the services logs:

    ``` bash
    docker compose logs -f
    ```
