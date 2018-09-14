# Dropbox in Docker

This repository provides the adopted stack for running customized image with single `docker-compose up` command.
The original version of the image with technical notes: https://github.com/janeczku/docker-dropbox

## Quickstart

### Run manually

Run the next commands:
```bash
# After cloning repository and `cd` into it.
echo "USER_NAME=$(whoami)">.env
docker-compose up -d
```

### Deploy via Portainer

Currently [Portainer](https://portainer.io) doesn't support build & restart commands in case of adding stack via GIT repository, that's why deploy can be done only manually.

1. Create `.env` file and set up the name of the current user. Example of the file:
*.env*
```
USER_NAME=user
```

2. Launch stack (building of the appropriate image is performed automatically)
```bash
docker-compose up -d
```

## Variables
Several variables can be passed via `.env` file, or alternatively directly set to the `docker-compose.yml`.

**USER_NAME** (required)
The name of the current user. Can be determined with `whoami`.

**DBOX_UID**
Run Dropbox with a custom user ID (matching the owner of the mounted files). Default: `1000`.

**DBOX_GID**
Run Dropbox with a custom group id (matching the group of the mounted files). Default: `1000`.

**DBOX_SKIP_UPDATE** 
Set this to `True` to skip updating to the latest Dropbox version on container start. Default: `False`.

## Main changes

Were done next changes:
1. Dockerfile with corresponded scripts are moved to the `image/` directory.
2. Docker-composer.yml file is provided, so the stack can be launched within the Portainer (`Stacks > Add Stack > Build method: Git Repository`).
3. Updates to a Dockerfile (GnuPG dependencies and replacement of the key-service with working one).
