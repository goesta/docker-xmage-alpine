# XMage Server Dockerfile based on Alpine

## Usage
    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        --add-host example.com:0.0.0.0 \
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        xmage-alpine


XMage needs to know the domain name the server is running on. The `--add-host` option adds an entry to the containers `/etc/hosts` file for this domain. Using the `XMAGE_*` environment variables you can modify the `config.xml` file.
You should always set `XMAGE_DOCKER_SERVER_ADDRESS` to the same value as `--add-host`.

You can limit the memory and CPU shares using the `-m` and `-c` options.   
For more informations on this topic  see: https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources

    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        --add-host example.com:0.0.0.0 \
        -m 2g
        -c 512
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        -e "XMAGE_DOCKER_SERVER_NAME=xmage-server" \
        goesta/xmage
