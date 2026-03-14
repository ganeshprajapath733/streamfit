# StreamFit – Personality Based Game Recommendation Platform

StreamFit is a Grails-based web application that recommends games based on user personality analysis.

This repository is a fork of the original project developed by Yuvraj V A and contributors.

## Tech Stack

Backend
- Grails 6
- Groovy
- JWT Authentication

Frontend
- GSP
- JavaScript
- CSS

Infrastructure
- AWS EC2
- Apache Reverse Proxy
- Tomcat
- MySQL
- Redis

## DevOps Deployment

The application was deployed on AWS using the following architecture:

Client
↓
Apache (Reverse Proxy)
↓
Tomcat (Grails Application)
↓
MySQL Database
↓
Redis Cache

### Infrastructure Setup

- AWS EC2 (t2.micro)
- Ubuntu 22.04
- Apache 2.4
- Tomcat 9
- MySQL 8
- Redis 6

### DevOps Features Implemented

- Reverse proxy using Apache
- Redis caching
- MySQL database integration
- Automated deployment scripts
- Daily database backups
- Health monitoring via cron jobs
- JVM memory optimization
- Security hardening and firewall configuration

### Monitoring Tools

- glances
- htop
- lnav

## Live Application

http://35.171.92.14/streamfit/personality/start

## Contributors

Original Author  
Yuvraj V A

Additional Contributors  
Abhishek  
Satwik

Deployment & Infrastructure  
Ganesh Prajapath
