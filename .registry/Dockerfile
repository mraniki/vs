FROM ubuntu

RUN apt-get update && apt-get install -y git curl wget && apt-get clean
RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh
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

CMD code-server --accept-server-license-terms --disable-telemetry
