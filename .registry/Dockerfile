FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev python3-pip python3-venv
COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

RUN wget "https://update.code.visualstudio.com/latest/server-linux-x64/stable" -O /tmp/vscode-server-linux-x64.tar.gz \  
    && mkdir /tmp/vscode-server \  
    && tar --no-same-owner -zxvf /tmp/vscode-server-linux-x64.tar.gz -C /tmp/vscode-server --strip-components=1 \   
    && mkdir -p /root/.vscode-server && cp -r /tmp/vscode-server/*  /root/.vscode-server/.

RUN apt-get update

RUN python3 -m pip3 install fastapi

RUN apt-get clean autoclean
RUN rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV PATH=/root/.vscode-server/bin/:$PATH
RUN echo "${PATH}" >> /etc/environment

RUN code-server --install-extension ms-python.python
RUN code-server --install-extension ms-python.vscode-pylance
RUN code-server --install-extension ms-python.black-formatter
RUN code-server --install-extension charliermarsh.ruff
RUN code-server --install-extension donjayamanne.python-environment-manager
RUN code-server --install-extension tamasfe.even-better-toml
RUN code-server --install-extension VisualStudioExptTeam.vscodeintellicode
RUN code-server --install-extension esbenp.prettier-vscode
RUN code-server --install-extension seatonjiang.gitmoji-vscode
RUN code-server --install-extension Codeium.codeium

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]
EXPOSE 8000
EXPOSE 8080

ENTRYPOINT ["code-server", "serve-local", "--accept-server-license-terms", "--disable-telemetry", "--without-connection-token", "--host", "0.0.0.0", "--port", "8080]
