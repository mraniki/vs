FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget 
#python3-dev python3-pip
#RUN wget https://aka.ms/install-vscode-server/setup.sh -O /tmp/vscode.deb
#RUN apt install -y /tmp/vscode.deb
#COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

RUN wget https://gist.githubusercontent.com/b01/0a16b6645ab7921b0910603dfb85e4fb/raw/f32b6371ed66085251c92bf98bfe9b7109c68e09/download-vs-code-server.sh -O /root/vserver.sh && chmod a+x /root/vserver.sh && ./root/vserver.sh
ENV PATH=/root/.vscode-server/bin/default_version/bin:$PATH
RUN code-server --install-extension ms-python.python

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]


CMD /bin/bash -c "code-server --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0 --server-data-dir /data"
