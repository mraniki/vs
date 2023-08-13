FROM python:3.11

RUN apt-get update && \
    apt-get install -y  \
    wget \
    git \
    && \
    apt-get clean

RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh

RUN apt-get update && \
    pip install -U pip && \
    pip install poetry && \
    pip install pytest && \
    rm -rf /var/lib/apt/lists/*

COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

COPY ./app/ /app
COPY chmod -R 755 /app

EXPOSE 8443/tcp

RUN mkdir /vscode

VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

CMD /app/code-server.sh
