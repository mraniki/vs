FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev python3-pip
COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

RUN wget "https://update.code.visualstudio.com/latest/server-linux-x64/stable" -O /tmp/vscode-server-linux-x64.tar.gz \  
    && mkdir /tmp/vscode-server \  
    && tar --no-same-owner -zxvf /tmp/vscode-server-linux-x64.tar.gz -C /tmp/vscode-server --strip-components=1 \   
    && mkdir -p /root/.vscode-server && cp -r /tmp/vscode-server/*  /root/.vscode-server/.  

RUN apt-get clean autoclean
RUN apt-get autoremove --yes
RUN rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN ls root/.vscode-server/bin/
ENV PATH=/root/.vscode-server/bin/:$PATH
RUN echo "${PATH}" >> /etc/environment

RUN code-server --install-extension ms-python.python
RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]
EXPOSE 8443/tcp

CMD "code-server --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0"
