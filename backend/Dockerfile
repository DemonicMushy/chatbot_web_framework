FROM node:12.2.0-alpine

RUN mkdir -p /srv/app/server
WORKDIR /srv/app/server

COPY package.json /srv/app/server
COPY package-lock.json /srv/app/server
COPY requirements.txt /srv/app/server

RUN apk add --no-cache --virtual .build-deps g++ python3-dev libffi-dev openssl-dev && \
    apk add --no-cache --update python3 && \
    pip3 install --upgrade pip setuptools

RUN npm install --production --slient && \
    npm install -g pm2 && \
    npm cache clean --force

RUN pip3 install -r requirements.txt

COPY . /srv/app/server

ENV ENV="/etc/profile"
# needed?
ENV PATH="/srv/app/server/node_modules/ffmpeg-static/bin/linux/x64/:${PATH}"
# not needed

EXPOSE 3001

CMD ["pm2-runtime","ecosystem.config.js"]
