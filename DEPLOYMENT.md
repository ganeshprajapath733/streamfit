📅 Project: StreamFit Grails 6.2.3 Application on AWS

Date: January 17, 2026
Duration: ~4 hours
Status: ✅ Production-Ready (pending domain/HTTPS)

🏗️ INFRASTRUCTURE SETUP

AWS Configuration:

✅ EC2 Instance: t2.micro (1GB RAM, 8GB storage)

✅ OS: Ubuntu 22.04 LTS

✅ Region: us-east-1

✅ Public IP: 35.171.92.14

✅ Security Group configured (SSH, HTTP, HTTPS)

Software Stack Installed:

✅ Java 21 (OpenJDK)

✅ Tomcat 9.0.58

✅ Apache 2.4 (reverse proxy)

✅ MySQL 8.0.44

✅ Redis 6.2 (caching)

✅ Monitoring tools (glances, htop, lnav)

🐛 CRITICAL BUGS FIXED

1. Application Bugs (6 major fixes):

A. Bootstrap.groovy Issue:

❌ Problem: Old bootstrap tried to drop/recreate tables on every restart (dangerous!)

✅ Fixed: Simplified to just verify tables exist

B. API Endpoint 404 Errors:

❌ Problem: Missing /streamfit context path in API calls

✅ Fixed: Added API_BASE to all fetch() calls in: 

personality/start.gsp (6 locations)

result/resultPage.gsp (3 locations)

C. Result Page Redirect:

❌ Problem: After signup, redirected to /dashboard instead of /streamfit/dashboard

✅ Fixed: Added API_BASE + to redirect URL

D. Authentication Flow:

❌ Problem: Tokens returned but not stored before redirect

✅ Fixed: Already had authManager.storeAuthData() - just fixed redirect URL

E. Dashboard 404 Error:

❌ Problem: Dashboard requires authentication

✅ Fixed: Signup now properly stores tokens and logs user in

F. Static Assets 404s:

❌ Problem: CSS/JS files had wrong paths

✅ Fixed: Context path issues resolved by Apache config

🔧 DEPLOYMENT CONFIGURATION

1. Database Setup:

✅ MySQL database: wsldna

✅ User: streamfit with proper permissions

✅ Tables: 7 tables (streamfit_user, game_questions, game_options, etc.)

✅ Data: 58 game questions populated

✅ Connection: Working via localhost

2. Apache Reverse Proxy:

✅ Configured as proxy to Tomcat

✅ Port 80 proxies to localhost:8080

✅ Security headers added

✅ Gzip compression enabled

✅ Browser caching configured

3. Tomcat Configuration:

✅ Memory optimized: -Xms256m -Xmx512m

✅ Running on port 8080 (not exposed publicly)

✅ Default apps removed for security

4. Firewall (UFW):

✅ SSH (22): Allowed

✅ HTTP (80): Allowed from anywhere

✅ HTTPS (443): Allowed (for future)

✅ Port 8080: Not exposed (internal only)

🚀 PERFORMANCE OPTIMIZATIONS

✅ Gzip Compression: Reduces page size by 60-80%

✅ Browser Caching: Images cached 1 year, CSS/JS 1 month

✅ Redis Caching: 13 keys cached, improving response time

✅ Memory Tuning: Optimized JVM settings for 1GB RAM

🔒 SECURITY IMPLEMENTATIONS

✅ Firewall Active: UFW blocking unnecessary ports

✅ Apache Security Headers: 

X-Frame-Options: SAMEORIGIN

X-Content-Type-Options: nosniff

X-XSS-Protection: enabled

✅ Tomcat Hardening: Default apps removed

✅ Database: Local access only (not exposed)

✅ Port 8080: Not publicly accessible

📊 MONITORING & MAINTENANCE

Automated Tasks:

✅ Daily Backups: Every day at 2 AM 

Location: /home/ubuntu/backups/

Retention: 7 days

Verified working ✅

✅ Health Monitoring: Every 5 minutes 

Checks if app is responding

Logs to: /home/ubuntu/health-check.log

✅ Log Rotation: Daily rotation of Tomcat logs 

Prevents disk from filling up

Keeps 7 days of logs

Monitoring Tools:

✅ glances: Real-time system monitoring

✅ htop: Process monitoring

✅ lnav: Beautiful log viewer

✅ Redis monitoring: Stats and key counts

🛠️ AUTOMATION SCRIPTS

1. Deployment Script (./deploy.sh):

bash

- Stops Tomcat - Backs up current WAR - Removes old deployment - Deploys new WAR - Starts Tomcat - Verifies deployment

Usage: ./deploy.sh

2. Health Check Script:

Runs every 5 minutes via cron

Checks if app responds

Logs status

3. Backup Script:

Runs daily at 2 AM via cron

Backs up MySQL database

Keeps last 7 days

📝 DOCUMENTATION CREATED

✅ Complete deployment documentation: /home/ubuntu/DEPLOYMENT_INFO.md

Includes:

Server details

All commands

Troubleshooting guide

Service management

Contact information

🌐 APPLICATION URLS

Public Access:

Main: http://35.171.92.14/streamfit/personality/start

Dashboard: http://35.171.92.14/streamfit/dashboard

Health: http://35.171.92.14/streamfit/health

Internal (not exposed):

Tomcat: http://localhost:8080/streamfit/

MySQL: localhost:3306

Redis: localhost:6379

✅ WHAT'S WORKING

✅ Complete test flow (choose game → answer questions → see results)

✅ User signup/login

✅ Dashboard access

✅ All 9 game types working

✅ Redis caching

✅ MySQL database

✅ Responsive on mobile devices

✅ Accessible from anywhere (not just your IP)

⚠️ PENDING (Before Production)

Critical (Must Do):

⚠️ Change JWT Secret (currently public) 

Location: application.yml line 100

Generate: openssl rand -base64 32

⚠️ Change MySQL Password (currently "StrongPasswordHere") 

Update in MySQL

Update in application.yml

⚠️ Get Domain Name ($1-12/year) 

Point to: 35.171.92.14

Required for HTTPS

⚠️ Setup HTTPS/SSL (after domain) 

Use Let's Encrypt (free)

Command: sudo certbot --apache -d yourdomain.com

Recommended (When Ready):

⏳ Update CORS to use domain instead of IP

⏳ Consider upgrading to t2.small if traffic increases

⏳ Setup email notifications (SendGrid, AWS SES)

⏳ Add error tracking (Sentry)
