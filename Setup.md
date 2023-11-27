This is a fork of https://github.com/mc1arke/sonarqube-community-branch-plugin

# Setup instructions

1. Setup nginx

`sudo apt install nginx`
`vim /etc/nginx/sites-enabled/<filename>`
```
server {
	listen 443 ssl;
        listen [::]:443 ssl;
        ssl_certificate /etc/ssl/certs/fullchain.pem;
        ssl_certificate_key /etc/ssl/private/privkey.pem;
        server_name zee5-cdn-sonarqube.sboxcdn.com;

        root /var/www/html;

        location / {
		include proxy_params;
                proxy_pass http://127.0.0.1:9000;
	}

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log debug;
}
```

2. Setup docker
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04

3. Set sysctl settings
`sudo sysctl -w vm.max_map_count=262144`


3. Clone this repo locally
`cd /opt && git clone https://github.com/akash-zee/sonarqube-community-branch-plugin.git`


4. Run on docker
`cd /opt/sonarqube-community-branch-plugin && docker compose up -d`