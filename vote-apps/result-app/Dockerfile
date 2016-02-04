FROM hypriot/rpi-node
RUN echo 'Acquire::http::proxy "http://10.0.4.2:3128/";' > /etc/apt/apt.conf.d/proxy.conf

RUN mkdir /app
WORKDIR /app

ADD package.json /app/package.json
RUN npm config set proxy http://10.0.4.2:3128
RUN npm install && npm ls
RUN mv /app/node_modules /node_modules

ADD . /app

ENV PORT 80
EXPOSE 80

CMD ["node", "server.js"]
