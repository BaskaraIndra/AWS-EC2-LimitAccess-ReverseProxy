# AWS-EC2-LimitAccess-ReverseProxy
Configuring reverse proxy in Ec2 instance

1. Open the NGINX web server configuration file using nano via the following command

---
sudo nano /etc/nginx/sites-available/default
---

2. Then, add the below code in the server -> location/block

---
 proxy_pass http://localhost:8000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
 
---

3. Remove the other code inside the location/ as below

---
try_files $uri $uri/ =404;

Save the file changes by pressing CTRL+X, then Y
---

4. Restart NGINX server using the below code

---
sudo systemctl restart nginx
---


Configuring limit access in Ec2 instance

1. Reopen the NGINX web server configuration file using nano via the following command

---
sudo nano /etc/nginx/sites-available/default
---

2. Then, write the following code at the start of the file or before the server block

---
limit_req_zone $binary_remote_addr zone=one:10m rate=30r/m;
---

3. Add the following code inside location /.

---
limit_req zone=one;
---
---
4. Restart NGINX server using the below code
---

sudo systemctl restart nginx

