FROM node:8

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

USER root

RUN apt-get update -y
RUN apt-get install -y jq
RUN curl https://sdk.cloud.google.com | bash && mv /root/google-cloud-sdk /opt
RUN curl -fsSL https://get.docker.com/ | sh
RUN gcloud components install kubectl

