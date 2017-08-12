FROM docker

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH

RUN apk update && apk add curl bash python jq
RUN curl https://sdk.cloud.google.com | bash && mkdir /opt && mv /root/google-cloud-sdk /opt
RUN gcloud components install kubectl