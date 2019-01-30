# Project-Linux-Server-Configuration

- The IP address : 51.77.193.224 
- The SSH port   : 2200
- The complete URL to my hosted web application : http://51.77.193.224.xip.io/

# A summary of software I installed and configuration changes made : 
- Add key based authentication
- Disable password authentication
- Disable root remote login
- Change SSH port to 2200
- Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
- Deployed the Item Catalog app to the server using nginx and gunicorn and performed the necessary configuration.
