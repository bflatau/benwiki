---
layout: default
title: Digital Ocean Nginx
parent: Server
nav_order: 2
---




# SETTING UP ENVIRONMENT

1. Clone Repo

2. Generate openssl dhparam file:
`sudo openssl dhparam -out /home/USER/nginxdockerssl/dhparam/dhparam-2048.pem 2048`

3. Get Certs:
`docker-compose -f docker-compose-keygen.yml up -d`

4. Stop certbot and nginx and remove associated files with `docker system prune`

5. Start webserver (it will also re-issue certs TODO: another docker compose file?) `docker-compose -f docker-compose-webserver.yml up -d`

6. Stop and remove certbot if still running.

## RE-ISSUING CERTS

1. Stop webserver and remove the container `docker stop webserver` || `docker rm webserver`
2. Just to be safe, clean out all of the misc. unused files/associations `docker system prune`
3. Start webserver again (part of the compose re-issues certs):
`docker-compose -f docker-compose-webserver.yml up -d`


## NOTES:

* Note the .gitignore folder and files in there, the folders must exist on the server for lets encrypt/certbot to verify ownership
* Note the name of the cert file, it sometimes changes 0001 --> 0002 --> 0003 over time or when you add new sites.

## USEFUL DOCKER COMMANDS

* run docker compose:
`sudo docker-compose up -d`

* docker compse logs
`sudo docker-compose logs`

* docker compose certbot
`sudo docker-compose up -d certbot`

* docker compose webserver
`sudo docker-compose up -d webserver`

* docker look in webserver container
`docker-compose exec webserver ls -la /etc/letsencrypt/live`

* just start webserver component:
`docker-compose up -d --force-recreate --no-deps webserver`

* get new certbot credentials
`docker-compose up --force-recreate --no-deps certbot`

* generate ssl key for each domain :
`sudo openssl dhparam -out /home/ben/nginxdockerssl/dhparam/dhparam-2048.pem 2048`

* Use the ‘-f’ flag for custom file names (not docker-compose.yml): `docker-compose -f docker-compose.test.yml up`

## TODOS:

* fix .gitignore file to track files?
* separate webserver and webserver + keygen compose files?
