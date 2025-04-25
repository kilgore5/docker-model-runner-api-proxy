# Docker Model Runner API Proxy for OpenWebUI

This is a reverse proxy for the [Docker Model Runner](https://docs.docker.com/desktop/features/model-runner/) API so that [OpenWebUI](https://openwebui.com/) can access models installed via Docker Model Runner.

The primary purpose was to add CORS support, but it also fixes a few other inconsistencies that may or may not be needed with further testing and/or configuration.

## Important Caveats

- Currently only lightly tested on OSX 14.1 Sonoma with Docker Desktop (4.40.0) and OpenWebUI (v0.6.5)

## Requirements

- [ ] Docker && Docker Desktop installed and running
  - [ ] Docker Compose
  - [ ] Docker Model Runner extension
- [ ] OpenWebUI installed and running

## Quick Start

### With Docker / Docker Desktop / Docker Model Runner / OpenWebUI installed and running

#### Enable host-side TCP support in Docker settings

Make sure `Enable host-side TCP support` is checked in Docker settings

#### install a model with Docker Model Runner

If you haven't already:

```bash
# install a model via Docker Model Runner
docker model pull ai/gemma3
```

#### Clone this repo and start the proxy

```bash
# clone this repo
git clone git@github.com:kilgore5/docker-model-runner-api-proxy.git
cd docker-model-runner-api-proxy

# start the proxy
docker-compose up -d
```

#### Confirm the proxy is working

```bash
# see models installed via Docker Model Runner
$ curl -s http://localhost:8081/v1/models
{"object":"list","data":[{"id":"ai/gemma3","object":"model","created":1742979452,"owned_by":"docker"}]}
```

#### Add the proxy to OpenWebUI Settings

add `http://localhost:8081/v1` to the OpenWebUI Settings -> Connections -> Manage Direct Connections

#### See the models in OpenWebUI UI
<img width="250" alt="Screenshot 2025-04-25 at 4 44 31 PM" src="https://github.com/user-attachments/assets/5e05146d-e4c8-42f7-978e-aeda32dd2ade" />

#### Chat
<img width="250" alt="Screenshot 2025-04-25 at 4 46 03 PM" src="https://github.com/user-attachments/assets/dc086303-49d0-4707-98f0-db0f837ea213" />


