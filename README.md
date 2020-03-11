# Deploying R Shiny Apps with Docker and Shiny Server/ShinyProxy

### Docker & Shiny Server
```
cd /.../docker-shiny

# build docker image - docker-shiny
docker build -t docker-shiny .

# start container
docker run -p 3838:3838 \
  -v /etc/localtime:/etc/localtime:ro \
  -v /.../myapp:/srv/shiny-server/myapp \
  -v /.../yourapp:/srv/shiny-server/yourapp \
  docker-shiny
```


### Docker & ShinyProxy
```
cd /.../docker-shiny

# build docker image - docker-shiny
docker build -t docker-shiny .

cd /.../docker-shinyproxy

# build docker image - docker-shinyproxy
docker build -t docker-shinyproxy .

# create a docker network for ShinyProxy
docker network create shiny-net

# start container
docker run -v /var/run/docker.sock:/var/run/docker.sock --net shiny-net -p 3838:8080 docker-shinyproxy

# start container in background
docker run -d -v /var/run/docker.sock:/var/run/docker.sock --net shiny-net -p 3838:8080 --name shinyproxy docker-shinyproxy

# stop container
docker stop -t 1 shinyproxy
```
