# Based on https://github.com/eirslett/chrome-karma-docker and
# https://hackernoon.com/running-karma-tests-with-headless-chrome-inside-docker-ae4aceb06ed3

FROM node:8.2.1

RUN apt-get update && apt-get install locales

# OPTIONAL: Install dumb-init (Very handy for easier signal handling of SIGINT/SIGTERM/SIGKILL etc.)
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb
RUN dpkg -i dumb-init_*.deb
ENTRYPOINT ["dumb-init"]

# Install Google Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -y google-chrome-stable

WORKDIR /opt/app

# Adding project source files to working directory
ADD . /opt/app/
RUN npm install &&\
    npm test
