# Steps to Set Up MySQL Environment with Docker

These are the steps to set up a MySQL environment using Docker on an M2 MacBook Air.

## Overview of Steps

1. **Create a `.env` file**
2. **Edit the Docker Compose file**
3. **Start the MySQL container**
4. **Test connection to the MySQL server**
5. **Shutdown and cleanup**
6. **Setting up `.gitignore` file**

## Detailed Steps

### 1. Create a `.env` file

- Create a `.env` file in the same directory as your Docker Compose file.
- Define environment variables such as MySQL root password in this file.

  ```plaintext
  MYSQL_ROOT_PASSWORD=yourpassword
  MYSQL_DATABASE=mydatabase
  ```

### 2. Edit the Docker Compose file

- Create or edit the `docker-compose.yml` file with the following content:

  ```yaml
  version: '3.1'

  services:
    db:
      image: mysql:latest
      platform: linux/arm64
      environment:
        MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
        MYSQL_DATABASE: ${MYSQL_DATABASE}
      ports:
        - "3306:3306"
      volumes:
        - /path/to/mysql/data:/var/lib/mysql
  ```

- `platform: linux/arm64` specifies the MySQL image optimized for ARM64 architecture.

### 3. Start the MySQL container

- Open the terminal and navigate to the directory where the `docker-compose.yml` file is located.
- Run the following command to start the MySQL container:

  ```bash
  docker-compose up -d
  ```

### 4. Test connection to the MySQL server

- To verify that MySQL has started correctly, connect to the MySQL server with the following command:

  ```bash
  mysql -h 127.0.0.1 -P 3306 -u root -p
  ```

- Enter the `MYSQL_ROOT_PASSWORD` value set in the `.env` file when prompted for the password.

### 5. Shutdown and cleanup

- When finished, run the following command to stop the container and free up resources:

  ```bash
  docker-compose down
  ```

### 6. Setting up `.gitignore` file

- Create a `.gitignore` file in the root directory of your project.
- Add `.env` to the `.gitignore` file to prevent it from being included in the Git repository.

  ```
  # .gitignore
  .env
  ```

- After making changes to the `.gitignore` file, run the following commands to reflect them in your Git repository:

  ```bash
  git add .gitignore
  git commit -m "Add .env to .gitignore"
  git push
  ```

This completes the steps to set up a MySQL environment using Docker on an M2 MacBook Air. Customize the `.env` file and `docker-compose.yml` file as needed.
