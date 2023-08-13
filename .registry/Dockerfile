FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev python3-pip
RUN pip install ruff
RUN wget https://go.microsoft.com/fwlink/?LinkID=760868 -O /tmp/vscode.deb
RUN apt install -y /tmp/vscode.deb

COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

#RUN code --no-sanbox --user-data-dir /vscode --install-extension ms-python.python

CMD /bin/bash -c "code --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0 --server-data-dir /data"
