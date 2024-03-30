# ollama-deepseek-coder

## Start Ollama in a container

```yaml
services:
  ollama-service:
    container_name: ollama_local
    image: ollama/ollama:0.1.30
    volumes:
      - ./ollama:/root/.ollama
    ports:
      - 11434:11434
  download-deepseek-coder-llm:
    image: rancher/curl:latest
    entrypoint: ["curl", "ollama-service:11434/api/pull", "-d", '{"name": "deepseek-coder"}']
    depends_on:
      ollama-service:
        condition: service_started
```

```bash
docker compose up
```
> Test it
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "deepseek-coder",
  "prompt": "Explain simply what is WebAssembly",
  "stream": false
}'
```

