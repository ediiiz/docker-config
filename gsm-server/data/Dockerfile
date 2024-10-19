# Use an Ubuntu base image
FROM ubuntu:20.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Update and install required packages
RUN apt-get update && \
  apt-get install -y \
  sudo \
  ufw \
  openjdk-11-jdk \
  fontconfig \
  unzip \
  wget \
  && apt-get clean

# Create a directory for the GSM server
RUN mkdir /opt/gsm

# Download and extract the GSM Server package
WORKDIR /opt/gsm
RUN wget -O gsm.zip https://download.gigabyte.com/FileList/Utility/server_utility_gsm.zip \
  && unzip gsm.zip \
  && rm gsm.zip

# Install the GSM .deb package
# Dynamically find the .deb package (version-agnostic)
RUN dpkg -i $(find /opt/gsm -name "*.deb") || apt-get install -f

# Expose required ports for the GSM server
# 8080 for HTTP, 8443 for HTTPS, 162 for SNMP, 69 for TFTP
EXPOSE 8080 8443 162 69 5900

# Start the GSM server
CMD ["java", "-jar", "/opt/gsm/gsm.jar"]
