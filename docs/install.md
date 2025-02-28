# Installation guide for MAC


**Clone repository**
```bash
git clone https://github.com/n8n-io/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
```


**run**
`docker compose up`

**setup**
If you're running OLLAMA locally on your Mac (not in Docker), you need to modify the OLLAMA_HOST environment variable in the n8n service configuration. Update the x-n8n section in your Docker Compose file as follows:

```
x-n8n: &service-n8n
    - OLLAMA_HOST=host.docker.internal:11434

services:
  n8n:
    extra_hosts:
    - "host.docker.internal:172.26.0.136"
```

Additionally, after you see "Editor is now accessible via: http://localhost:5678/":

Head to http://localhost:5678/home/credentials
Click on "Local Ollama service"
Change the base URL to "http://host.docker.internal:11434/"


Additionally in MAC
Make Ollama serve to all network interfaces:
OLLAMA_HOST="http://172.26.0.136:11434"`

To test connectiviy:

Level 0: basic communication from host Linux
- Check open ports
`nc -vz 172.26.0.136 11434`

Lavel 1: LLM query from host Linux
```
curl http://172.26.0.136:11434/api/generate -d '{

  "model": "mistral-small:latest",

  "prompt":"Why is the sky blue?, reply in 10 words"

}'
```
Level 2: Basic communication from docker
- Enter docker from Linux host
`sudo docker exec -it n8n /bin/sh`
- Check open ports
`nc -vz 172.26.0.136 11434`

Level 3: query from N8N
- Launch test from UI



