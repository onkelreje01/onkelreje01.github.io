---
title: EVE-NG Docker installation på Ubuntu Server 22.04
layout: default
---

# EVE-NG Docker installation på Ubuntu Server 22.04

Create a Dockerfile that defines the base image and the commands to install EVE-NG. Here is an example of a Dockerfile that installs EVE-NG using the Bash script:
```
FROM ubuntu:22.04

# Update the package list and install prerequisites
RUN apt-get update && apt-get install -y wget unzip python3 python3-venv python3-pip

# Download and extract the EVE-NG installation package
RUN wget https://www.eve-ng.net/repo/ubuntu/eve-ng_2.1.0-b8.zip && \
    unzip eve-ng_2.1.0-b8.zip && \
    cd eve-ng_2.1.0-b8

# Create and activate a Python virtual environment, and install the EVE-NG dependencies
RUN python3 -m venv env && \
    source env/bin/activate && \
    pip3 install -r requirements.txt

# Run the EVE-NG installation script
RUN ./install.sh

# Start the EVE-NG service
CMD ["systemctl", "start", "eve-ng"]
```
Build the Docker image using the Dockerfile. Open a terminal and navigate to the directory that contains the Dockerfile. Then run the following command:
```
docker build -t eve-ng .
```
This will build the Docker image using the instructions in the Dockerfile. The -t flag specifies a tag for the image, which in this case is "eve-ng".

Run the Docker container using the following command:
```
docker run -it --name eve-ng -p 80:80 -p 443:443 eve-ng
```
This will run the Docker container and expose ports 80 and 443, which are used by EVE-NG. The -it flag runs the container in interactive mode, and the --name flag specifies a name for the container.

To access EVE-NG, open a web browser and go to http://localhost.
I hope this helps! Let me know if you have any questions or need further assistance.