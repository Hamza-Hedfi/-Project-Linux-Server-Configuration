# Project-Linux-Server-Configuration

- The IP address : 51.77.193.224 
- The SSH port   : 2200
- The complete URL to my hosted web application : http://51.77.193.224.xip.io/

# A summary of software I installed and configuration changes made : 
- Update all packages.
- Add key based authentication
- Disable password authentication
- Disable root remote login
- Change SSH port to 2200
```bash
# /etc/ssh/sshd_config
...
Port 2200
PasswordAuthentication no
PermitRootLogin no
...
```

- Configure UFW to only allow incoming connections for SSH, HTTP, and NTP.
```bash
hamza@vps643599:~$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW IN    Anywhere
123                        ALLOW IN    Anywhere
2200                       ALLOW IN    Anywhere
80/tcp (v6)                ALLOW IN    Anywhere (v6)
123 (v6)                   ALLOW IN    Anywhere (v6)
2200 (v6)                  ALLOW IN    Anywhere (v6)
```

- Deployed the Item Catalog app to the server using nginx and gunicorn and performed the necessary configuration.
```bash
# /etc/nginx/sites-enabled/itemcatalog

server {
    listen 80;
    server_name 51.77.193.224;

    location / {
        proxy_pass http://localhost:8000;
        include /etc/nginx/proxy_params;
        proxy_redirect off;
    }
}
```
- Install Supervisor and configure it
```bash
# /etc/supervisor/conf.d/itemcatalog.conf

[program:flaskblog]
directory=/home/hamza/ItemCatalog
command=/home/hamza/ItemCatalog/venv/bin/gunicorn -w 3 app:app
user=hamza
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/itemcatalog/itemcatalog.err.log
stdout_logfile=/var/log/itemcatalog/itemcatalog.out.log
```

# A list of any third-party resources
- https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart
- https://www.youtube.com/watch?v=goToXTC96Co
- https://gunicorn.org/#docs
- https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
- https://flask-dance.readthedocs.io/en/latest/
- https://help.ubuntu.com/community/Sudoers
- https://docs.ovh.com/fr/vps/debuter-avec-vps/
- and finally and of course google.
