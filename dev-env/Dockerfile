FROM node:6

RUN apt-get update && apt-get -y install sudo
RUN useradd -ms /bin/bash app && echo "app:app" | chpasswd && adduser app sudo
RUN npm install --production && \
    mv ./node_modules ./node_modules.tmp && mv ./node_modules.tmp ./node_modules && npm install

# Working directory needs to be a child of home for webpack to work correctly
ARG service_name

ENV HOME=/home/app

COPY package.json $HOME/$service_name/
RUN chown -R app:app $HOME/*

USER app
WORKDIR $HOME/$service_name
RUN npm install -verbose

