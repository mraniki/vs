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

RUN wget -q -P /tmp \
  https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && bash /tmp/Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda \
    && rm /tmp/Miniconda3-latest-Linux-x86_64.sh

COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

# COPY --chmod=0755 ./app/ /app
# RUN chmod -R 755 /app

EXPOSE 8443/tcp

RUN mkdir /vscode

VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

# CMD /app/code-server.sh
CMD ["code-server"]
#, "--accept-server-license-terms", "serve-local","--host","0.0.0.0","--server-data-dir","/data"]

