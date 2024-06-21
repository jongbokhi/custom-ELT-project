# custom-ELT-project

This repository showcases a custom Extract, Load, Transform (ELT) process using Docker and PostgreSQL, illustrating a basic ELT workflow.

## Structure

1. docker-compose.yaml: Configures Docker Compose to manage multiple Docker containers.
   It sets up three services:

   * source_postgres: The source PostgreSQL database.
   * destination_postgres: The target PostgreSQL database.
   * elt_script: The service executing the ELT script.

3. elt_script/Dockerfile: Sets up a Python environment, installs the PostgreSQL client, and incorporates the ELT script, setting it as the default command.

4. elt_script/elt_script.py: This Python script carries out the ELT process. It waits for the source PostgreSQL database to be ready, dumps its data to a SQL file, and loads this data into the destination PostgreSQL database.

5. source_db_init/init.sql: Initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, then populates these tables with sample data.

## How It Works

1. Docker Compose: The docker-compose.yaml file launches three Docker containers:

   * A source PostgreSQL database preloaded with sample data.
   * A destination PostgreSQL database.
   * A Python environment running the ELT script.

2. ELT Process: The elt_script.py waits until the source PostgreSQL database is accessible. Once it is, the script uses pg_dump to export the source database to a SQL file, and then psql to import this SQL file into the destination PostgreSQL database.

3. Database Initialization: The init.sql script sets up the source database with sample data, creating and populating tables for users, films, film categories, actors, and film actors.
