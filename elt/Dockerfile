FROM python:3.8-slim

# Install necessary dependencies
RUN apt-get update && apt-get install -y \
    wget \
    gnupg2 \
    lsb-release \
    && apt-get clean

# Add PostgreSQL APT repository
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list

# Import PostgreSQL signing key
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

# Update package lists again and install PostgreSQL client version 16
RUN apt-get update && apt-get install -y \
    postgresql-client-16 cron\
    && apt-get clean

# Copy the ELT script into the container
COPY start.sh /app/start.sh
COPY elt_script.py .

WORKDIR /app

RUN echo "0 3 * * * python /app/elt_script.py" | crontab -
# Set the default command to run the ELT script
CMD ["python", "elt_script.py"]
