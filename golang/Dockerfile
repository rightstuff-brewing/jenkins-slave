FROM golang:1.8
ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

USER root

RUN apt-get update -y && \
    apt-get install -y jq && \
    curl https://sdk.cloud.google.com | bash && mv /root/google-cloud-sdk /opt && \
    curl -fsSL https://get.docker.com/ | sh && \
    gcloud components install kubectl