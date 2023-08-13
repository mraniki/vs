FROM ubuntu:22.04

RUN apt-get update && apt-get install -y git curl wget pip && apt-get clean
RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh
RUN pip install poetry pytest black ruff

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O install_miniconda.sh \
    && bash install_miniconda.sh -b -p /opt/conda \
    && rm install_miniconda.sh
ENV PATH="/opt/conda/bin:${PATH}"

COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

# CMD code-server --accept-server-license-terms --disable-telemetry
CMD /bin/bash -c "code-server --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0 --server-data-dir /data"
