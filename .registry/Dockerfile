FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev

RUN wget "https://update.code.visualstudio.com/latest/server-linux-x64/stable" -O /tmp/vscode-server-linux-x64.tar.gz \  
    && mkdir /tmp/vscode-server \  
    && tar --no-same-owner -zxvf /tmp/vscode-server-linux-x64.tar.gz -C /tmp/vscode-server --strip-components=1 \   
    && mkdir -p /root/.vscode-server && cp -r /tmp/vscode-server/*  /root/.vscode-server/.

ENV PATH=/root/.vscode-server/bin/:$PATH
RUN echo "${PATH}" >> /etc/environment

# RUN code-server --install-extension ms-python.python \
#     && code-server --install-extension ms-python.vscode-pylance \
#     && code-server --install-extension ms-python.black-formatter \
#     && code-server --install-extension charliermarsh.ruff \
#     && code-server --install-extension donjayamanne.python-environment-manager \
#     && code-server --install-extension tamasfe.even-better-toml \
#     && code-server --install-extension VisualStudioExptTeam.vscodeintellicode \
#     && code-server --install-extension esbenp.prettier-vscode \
#     && code-server --install-extension seatonjiang.gitmoji-vscode \
#     && code-server --install-extension Codeium.codeium

RUN apt-get clean autoclean \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

EXPOSE 8080
EXPOSE 8000

# ENTRYPOINT ["code-server", "serve-local", "--accept-server-license-terms", "--disable-telemetry", "--without-connection-token", "--host", "0.0.0.0", "--port", "8080"]
ENTRYPOINT ["code-server","--accept-server-license-terms","--without-connection-token", "--host", "0.0.0.0"]
