FROM debian:bookworm-slim

RUN apt update && apt install -y git curl wget python3-dev python3-pip
#RUN python3 -m pip install --upgrade pip setuptools wheel
#RUN pip install --no-cache-dir poetry pytest black ruff
RUN wget https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64 -O vscode.deb
#RUN apt install -y vscode.deb
RUN apt install ./vscode.deb
COPY --from=1password/op:2 /usr/local/bin/op /usr/local/bin/op

EXPOSE 8443/tcp

RUN mkdir -m 755 -p /vscode
VOLUME [ "/vscode" ]
VOLUME [ "/data" ]

# CMD '/bin/bash -c code-server --accept-server-license-terms serve-local --disable-telemetry'

# CMD code-server --accept-server-license-terms --disable-telemetry
CMD /bin/bash -c "code-server --accept-server-license-terms serve-local --disable-telemetry --without-connection-token --host 0.0.0.0 --server-data-dir /data"
