FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev python3-pip
#RUN python3 -m pip install --no-cache-dir poetry pytest black ruff
#RUN curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
#RUN add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" | tee /etc/apt/sources.list.d/vscode.list
RUN wget https://go.microsoft.com/fwlink/?LinkID=760868 -O vscode.deb
RUN apt install ./vscode.deb
#RUN apt update && apt install code


# RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O install_miniconda.sh \
#     && bash install_miniconda.sh -b -p /opt/conda \
#     && rm install_miniconda.sh
# ENV PATH="/opt/conda/bin:${PATH}"

# COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

# CMD '/bin/bash -c code-server --accept-server-license-terms serve-local --disable-telemetry'

# CMD code-server --accept-server-license-terms --disable-telemetry
CMD /bin/bash -c "code-server --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0 --server-data-dir /data"
