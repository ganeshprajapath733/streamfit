# StreamFit AWS Deployment

## Project Overview
Deployment of the StreamFit Grails 6.2.3 application on AWS using Apache reverse proxy, Tomcat application server, MySQL database, and Redis caching.

Deployment Date: January 17, 2026  
Status: Production Ready (Domain & HTTPS pending)

---

# Infrastructure Setup

## AWS Configuration
- EC2 Instance: t2.micro
- OS: Ubuntu 22.04 LTS
- Region: us-east-1
- Public IP: 35.171.92.14

Security Group:
- SSH (22)
- HTTP (80)
- HTTPS (443)

---

# Technology Stack

Application Layer
- Grails 6.2.3
- Java 21

Web Layer
- Apache 2.4 Reverse Proxy
- Tomcat 9.0.58

Data Layer
- MySQL 8.0
- Redis 6.2

Monitoring
- glances
- htop
- lnav

---

# Architecture

Client  
↓  
Apache Reverse Proxy  
↓  
Tomcat (Grails Application)  
↓  
MySQL Database  
↓  
Redis Cache  

---

# Deployment Configuration

## Database
Database: wsldna  
User: streamfit  

Tables:
- streamfit_user
- game_questions
- game_options

Data:
58 game questions loaded.

---

## Apache Reverse Proxy

Port 80 → proxies to Tomcat (localhost:8080)

Features enabled:

- Security headers
- Gzip compression
- Browser caching

---

## Tomcat Configuration

Memory optimization:

- Xms256m
- Xmx512m

Security hardening:

- Default apps removed
- Tomcat port 8080 not exposed publicly

---

# Performance Optimizations

- Gzip compression enabled
- Browser caching (images: 1 year)
- Redis caching for faster responses
- JVM memory tuning for low-resource EC2 instance

---

# Security

Firewall (UFW)

Allowed ports:

- 22 SSH
- 80 HTTP
- 443 HTTPS

Security Measures

- Apache security headers
- Database restricted to localhost
- Tomcat not publicly exposed

---

# Automation

## Deployment Script

deploy.sh

Functions:
- Stop Tomcat
- Backup current WAR
- Deploy new WAR
- Restart Tomcat

Usage:

./deploy.sh

---

## Backup Script

Runs daily via cron.

Schedule:
2:00 AM

Location:
`/home/ubuntu/backups/`

Retention:
7 days

---

## Health Monitoring

Runs every 5 minutes via cron.

Log file:

`/home/ubuntu/health-check.log`

---

# Application URLs

Public

http://35.171.92.14/streamfit/personality/start

Dashboard

http://35.171.92.14/streamfit/dashboard

Health Check

http://35.171.92.14/streamfit/health

---

# Monitoring Tools

- glances
- htop
- lnav
- redis-cli stats

---

# Known Issues / Improvements

Before production release:

- Change JWT secret
- Update MySQL password
- Configure domain name
- Enable HTTPS using Let's Encrypt

Future improvements:

- Setup email notifications
- Upgrade instance if traffic increases
- Add error tracking (Sentry)
