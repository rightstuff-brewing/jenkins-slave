FROM node:8

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

USER root

RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb
RUN dpkg -i dumb-init_*.deb
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

RUN apt-get update -y
RUN apt-get install -y jq && \
    curl https://sdk.cloud.google.com | bash && mv /root/google-cloud-sdk /opt && \
    curl -fsSL https://get.docker.com/ | sh && \
    gcloud components install kubectl

RUN apt-get install -y google-chrome-stable