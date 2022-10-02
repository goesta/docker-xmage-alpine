# Info

This Project relied on docker hub automated builds which are no longer available for open source projects. I had to change to a new build system and moved the project to another repo.

You can find up to date Images on these Repos.

Release Version:
https://github.com/mage-docker/xmage-docker

Beta Version (recommended):
https://github.com/mage-docker/xmage-beta-docker


# XMage Server based on Alpine

## Usage
    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        --add-host example.com:0.0.0.0 \
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        goesta/xmage-alpine


XMage needs to know the domain name the server is running on. The `--add-host` option adds an entry to the containers `/etc/hosts` file for this domain. 
Using the `XMAGE_*` environment variables you can modify the `config.xml` file.
You should always set `XMAGE_DOCKER_SERVER_ADDRESS` to the same value as `--add-host`.

If you dont have a Domain you can use a service like http://nip.io.

If you like to preserve the database during updates and restarts you can mount a volume at /xmage/mage-server/db


## Example Docker Compose file

    version: '2'
    services:
    mage:
        image: goesta/xmage-alpine
        ports:
         - "17171:17171"
         - "17179:17179"
        extra_hosts:
         - "example.com:0.0.0.0"
        environment:
         - XMAGE_DOCKER_SERVER_ADDRESS=example.com
         - XMAGE_DOCKER_SERVER_NAME=xmage-server
         - XMAGE_DOCKER_MAX_SECONDS_IDLE=6000
         - XMAGE_DOCKER_AUTHENTICATION_ACTIVATED=false
        volumes:
         - xmage-db:/xmage/mage-server/db
         - xmage-saved:/xmage/mage-server/saved
    volumes:
        xmage-db:
            driver: local
        xmage-saved:
            driver: local

## Links

[Tutorial - Running XMage on DigitalOcean](https://github.com/goesta/docker-xmage-alpine/wiki/DigitalOcean-Tutorial)
