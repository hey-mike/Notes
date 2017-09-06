# Portable vagrant with docker
- This is should work only with services, such as database.
- For project that you will need to see debug logs , should use docker instead of using docker provider by vagrant. 

# AWS elastic search choice
t2.small

# Nginx local redirect
```
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/.htpasswd;
proxy_pass https://<service>.<domain>:<port>;
      ```
