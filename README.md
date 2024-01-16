# HTML5_Ollama_Speech

* This HTML5 example uses the Ollama REST API and the browser Speech API to add speech detection and speech synthesis for [Ollama](https://ollama.ai).

* [Web Demo](https://tgraupmann.github.io/HTML5_Ollama_Speech/) - Note for the demo to work you need the Ollama chat API to add the `Access-Control-Allow-Origin: *` header. I'll add instructions once I have this working. One suggestion is to modify the Ollama container nginx configuration to add the header. Even better would be to modify the client Golang code to add the header so that websites can talk to the Ollama REST API. In the meantime, just clone the repository and use the live-preview VS Code extension to preview the index.html and it will work without the header.

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
