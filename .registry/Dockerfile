FROM python:3.11

RUN apt-get update && \
    apt-get install -y  \
    wget \
    git \
    && \
    apt-get clean

RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh

# RUN apt-get update && \
# apt-get -y install chromium && \
#   pip install -U pip && \
#   pip install playwright && \
#   playwright install chromium && playwright install-deps && \
#   rm -rf /var/lib/apt/lists/*

ENV OP_SERVICE_ACCOUNT_TOKEN=NONE
COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

COPY ./root/ /

EXPOSE 8443/tcp

RUN mkdir /vscode

VOLUME [ "/vscode" ]

VOLUME [ "/data" ]

CMD /entrypoint.sh