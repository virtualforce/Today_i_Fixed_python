## Problem
Uploading large files gives "Entity too large Exception" in nginx

# Environment
Ubuntu,Python,Django,Nginx

## How you fix it
Navigating to nginx configuration file and include max body size property to enhance the max size limit of uploaded file.

## Solution
**Navigate to directory:**  
**sudo nano /etc/nginx/nginx.conf**  
  
**Modify the server directive file content as follows:**  
```   
server {  
    client_max_body_size 10M;  
    listen 0.0.0.0:80;  
    allow 39.36.51.51;  
    server_name extroai.virtualforce.io;  
       
    location = /favicon.ico { 
        access_log off; log_not_found off; 
    }  

    location /static/ {  
       autoindex on;  
        alias /home/ubuntu/Visual-ocr_Admin/vf-ocr-sdk/static/;  
    }  
    location / {  
     client_max_body_size 10M;  
     proxy_pass http://localhost:5001/;  
     proxy_buffering off;  
     proxy_set_header X-Real-IP $remote_addr;  
     proxy_set_header X-Forwarded-Host $host;  
     proxy_set_header X-Forwarded-Port $server_port;  
     }  
     }  
