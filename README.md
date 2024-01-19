# HTML5_Ollama_Speech

* This HTML5 example uses the Ollama REST API and the browser Speech API to add speech detection and speech synthesis for [Ollama](https://ollama.ai).

* [Web Demo](https://tgraupmann.github.io/HTML5_Ollama_Speech/) - Note for the demo to work you need the Ollama chat API to add the `Access-Control-Allow-Origin: *` header. (See below)

## Screenshots

![image_1](/images/image_1.png)

## Dependencies

* [Ollama](https://ollama.ai) [REST API](https://github.com/jmorganca/ollama/blob/main/docs/api.md#generate-a-chat-completion)

* Browser ([Chrome](https://www.google.com/chrome/) Recommended)

### Windows

* [Docker Desktop](https://www.docker.com/products/docker-desktop/)

* Install Ollama with GPU acceleration on Windows:

```shell
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

* Install the `llama2` model:

```shell
docker exec -it ollama ollama run llama2
```

## Add Custom Headers to a NGINX Proxy in the Docker Container

You can create a new Ollama container to add a `nginx` proxy with the required header. If you don't want to use the proxy, just clone the repository and use the live-preview VS Code extension to preview the index.html and it will work without the header. In the future it would be better to modify the client Golang code to add the header so that websites can talk directly to the Ollama REST API.

### Use docker composer

* You can use the exsiting docker composer settings to setup the Ollama + NGINX Proxy

* Step 1) Setup your environment and rename `.env.example` to `.env`. Pick your ports or use the defaults.

```js
NGINX_PORT=11435
OLLAMA_PORT=11434
```

* Step 2) Build the docker container

```shell
docker compose up --build
```

* Step 3) Install the `llama2` model:

```shell
docker exec -it ollama ollama run llama2
```

* Step 4) Try the [Web Demo](https://tgraupmann.github.io/HTML5_Ollama_Speech/)

### Manual steps

* Or you can use apt-get to install `nginx` inside the Ollama container.

* First recreate the docker container with an additional port for the `nginx` proxy.

```shell
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 -p 11435:11435 --name ollama ollama/ollama
```

* Install the `llama2` model:

```shell
docker exec -it ollama ollama run llama2
```

![image_2](/images/image_2.png)

* Add `vim` to edit configs

```shell
apt-get update
apt-get install vim
```

* Install `nginx` to run a web proxy which adds the custom header

```shell
apt-get install nginx
```

* Edit the `nginx` configuration

```shell
vi /etc/nginx/sites-available/default
```

* Add the proxy settings and custom header

```js
server {
 listen 11435;
 location / {
   if ($request_method = 'OPTIONS') {
     add_header 'Access-Control-Allow-Origin' '*';
     add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
     add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range';
     add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';
     return 204;
   }
   proxy_pass http://localhost:11434;
 }
 proxy_hide_header 'Origin';
 proxy_set_header 'Origin' "https://localhost:11434";
 add_header 'Access-Control-Allow-Origin' '*';
}
```

* Test if the configuration changes are okay.

```shell
nginx -t
```

* Reload the `nginx` service

```shell
service nginx reload
```

* Start the `nginx` proxy server

```shell
nginx
```
