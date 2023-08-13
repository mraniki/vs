FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y git curl wget && apt-get clean
RUN apt-get install build-essential libssl-dev libffi-dev python3-dev python3-pip
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install --no-cache-dir poetry pytest black ruff

# RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/microsoft-archive-keyring.gpg
RUN sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/usr/share/keyrings/microsoft-archive-keyring.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

RUN sudo apt-get install apt-transport-https
RUN sudo apt-get update
RUN sudo apt-get install code

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
