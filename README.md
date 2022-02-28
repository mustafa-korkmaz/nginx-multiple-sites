This repository solves **_same host, multiple web sites_** problem including SSL certificate creation and renewal based on [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy) repository.
It creates 2 seperate containers which do nothing but serve 2 different simple web pages along with **nginx-proxy** as a reverse proxy and [acme-companion](https://github.com/nginx-proxy/acme-companion) as an ssl certificate manager. 
Reverse proxy configs are reloaded when containers are started and stopped.
You can add as many services as you want either by adding them in [docker-compose.yml](./docker-compose.yml) or running a new container within the same network.

### Usage

To run it:

```console
docker-compose up
```

To add another container and serve it from another virtual host:
 
```console
docker run -d --name another_app --network nginx-proxy_default --expose 80 -e VIRTUAL_HOST=app.mydomain.io -e LETSENCRYPT_HOST=app.mydomain.io httpd
```
