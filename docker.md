# Docker Compose Lab Documentation
*Sydney Tran - CYB3353 System Administration*

## Overview
For this lab, I used my exisiting Ubuntu Virtual Machine (VM) on VirtualBox to download Docker and I used the slides for this project to ensure I followed all the steps needed. The information from the slides, such as the video tutorial, helped me tremendously. This document contains all of the steps taken in completing this project. 

## Installing and Setting Up Docker

I started this project off by starting up my exisiting Ubuntu VM and immediately opening the terminal and using the following commands to ensure the system is prepared for installation:
- `sudo apt-get update`
- `sudo apt-get upgrade`

After doing so, I was then able to download Docker from the following: 
- `sudo apt-get install docker.io`

I then installed Docker Compose with the commands below, which was provided from the slides:
- `sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
- `sudo chmod +x /usr/local/bin/docker-compose` 

To verified that Docker Compose was installed, I then used:
- `docker-compose --version`

However, it was important to make sure that the Docker service was active, I made sure to check the status with the command:
- `sudo service docker status`

From reading this, I noticed that Docker was not active. Therefore, I made Docker active with: 
- `sudo service docker start`

I double checked that Docker was now active by using the `sudo service docker status` command again where I was able to verify that it was ready.  

## Installing OpenVAS/Greenbone Vulnerability Scanner 

I decided to install OpenVAS/Greenbone vulnerability scanner with Docker. In order to do so, I created a docker-compose.yml file by doing the following:
- I made a new directory called openvas-docker with `mkdir ~/openvas-docker` and entered this directory with `cd ~/openvas-docker`.
- I created the yml file in this directory with `nano docker-compose.yml` where I was then able to edit this file. 
- In this file, I wrote the following using the official Docker Compose file reference found here: https://docs.docker.com/reference/compose-file/. Additionally, in this link provided from the slides, https://github.com/mikesplain/openvas-docker, I was able to reference the docker-compose.yml file.

```yaml
version: '3'

services:
  openvas:
    image: mikesplain/openvas
    container_name: openvas
    ports:
      - "443:443" 
    restart: always
```
Finally, I used the command `sudo docker-compose up -d` which allows me to start all the services in my docker-compose.yml file. 

From using this command, I was then able to type "https://localhost/" in a FireFox browser on my VM. This opened the Greenbone Security Assistant where I logged in with "admin" for both the username and password. 

I was now able to create targets and run vulnerability scans. 

## Challenges Faced
The biggest challenge I faced was creating my docker-compose.yml file. Learning the syntax for the yml file was very confusing for me. But after discovering the official Docker Compose file reference, I saw several examples of yml files which led me to my final yml file that works. 
