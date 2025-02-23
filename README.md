# Nginx Multi-Tenant HomeAssistant Proxy

A production-ready Nginx configuration for hosting multiple HomeAssistant instances behind a single domain using path-based routing.
  
## Overview
This configuration allows you to:

Host multiple HomeAssistant instances under a single domain (e.g., example.com/tenant1/, example.com/tenant2/)
Use a single SSL certificate for all instances
Handle authentication, WebSocket connections, and static assets correctly for each tenant
Support independent HomeAssistant instances with separate IP addresses

## Features

Path-based routing using Nginx
SSL/TLS support with single certificate
Proper WebSocket handling for real-time updates
Correct MIME type handling for all HomeAssistant assets
Authentication path rewriting for each tenant
Static asset caching
Support for HACS (Home Assistant Community Store)

## Prerequisites

Nginx with SSL module
Valid SSL certificate
Multiple HomeAssistant instances with their own IP addresses
nginx-extras package for sub_filter support

## Configuration
The configuration supports:

Path-based routing (/tenant1/, /tenant2/, etc.)
WebSocket connections for real-time updates
Authentication flows
Static asset handling
MIME type corrections
Cache control for static assets

## Installation

Install required packages:

bashCopyapt update
apt install nginx nginx-extras

Place SSL certificates in /etc/nginx/ssl/:


certificate.crt
certificate.key


Copy the configuration to:

bashCopy/etc/nginx/sites-available/homeassistant

Enable the site:

bashCopyln -s /etc/nginx/sites-available/homeassistant /etc/nginx/sites-enabled/

- Replace all instances of <fqdn> in the file with your domain.
- Replace 192.168.4.x with your actual server addresses.

Test and restart Nginx:

bashCopynginx -t
systemctl restart nginx
Adding New Tenants
To add a new tenant:

Add a new location block in the configuration
Update path substitutions for the new tenant
Point proxy_pass to the new HomeAssistant instance IP
Test and reload Nginx configuration

## Known Limitations

Each HomeAssistant instance must have its own IP address
All tenants share the same domain name
Authentication tokens are specific to each tenant path

## Troubleshooting
Common issues:

404 errors: Check static file paths and MIME types
WebSocket failures: Verify proxy settings and timeouts
Authentication errors: Confirm path rewriting in auth blocks

### License
MIT