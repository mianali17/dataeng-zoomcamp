# Base Image
FROM apache/airflow:2.7.0

# Create environment variable
ENV AIRFLOW_HOME=/opt/airflow

# Copy .env file into the container
COPY .env /opt/airflow/.env

# Set user to root
USER root

# Install OpenJDK-11 for compatibility with 'Apache Spark' Airflow provider
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
         openjdk-11-jre-headless \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
RUN export JAVA_HOME

# Set user to airflow (required to install PIP packages)
USER airflow

# Install required packages
COPY ./requirements.txt /
RUN pip install --no-cache-dir "apache-airflow==${AIRFLOW_VERSION}" -r /requirements.txt