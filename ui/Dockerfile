# syntax=docker.io/docker/dockerfile:1.7-labs
FROM node:18


# PROXY_HOST is required when running the container with docker compose to replace
# 'localhost' in package.json. This enables the UI to communicate with the backend UC
# service, using the container names on the docker network, created on the host machine.
# Eg. PROXY_HOST=server -> proxy: "http://server:8080" in the package.json.
ARG PROXY_HOST

WORKDIR /ui

COPY package.json yarn.lock ./

RUN <<EOF
set -ex
yarn install
EOF

# if [ ! -z "$PROXY_HOST" ]; then
#     apt-get update
#     apt-get install -y jq
#     jq --arg proxy "http://$PROXY_HOST:8080" '.proxy = $proxy' package.json > temp.json
#     mv temp.json package.json
#     apt-get clean
# fi

COPY --exclude=package.json --exclude=yarn.lock . ./

CMD ["yarn", "start"]
