# HTML5_Ollama_Speech

* This HTML5 example uses the Ollama REST API and the browser Speech API to add speech detection and speech synthesis for [Ollama](https://ollama.ai).

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
