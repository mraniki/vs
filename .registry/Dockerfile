FROM python:3.11

RUN apt-get update && apt-get install -y git curl wget && apt-get clean
RUN curl -fsSL https://aka.ms/install-vscode-server/setup.sh | sh


RUN pip install -U pip \
    && pip install --no-cache-dir poetry \
    && pip install --no-cache-dir pytest \
    && pip install --no-cache-dir black \
    && pip install --no-cache-dir ruff

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O install_miniconda.sh \
    && bash install_miniconda.sh -b -p /opt/conda \
    && rm install_miniconda.sh
ENV PATH="/opt/conda/bin:${PATH}"

COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]


CMD echo start... \
    && code-server serve-local \
    --accept-server-license-terms \
    --host 0.0.0.0 \
    --server-data-dir /data \
    --without-connection-token

