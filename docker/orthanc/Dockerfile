FROM jodogne/orthanc:1.2.0

# installing lua 5.1 and socket module
WORKDIR /tmp
RUN ( apt-get update && apt-get install -y ncurses-dev git curl )
RUN ( curl -R -O https://www.lua.org/ftp/lua-5.1.tar.gz && tar xvzf lua-5.1.tar.gz )
WORKDIR /tmp/lua-5.1
RUN ( make linux test && make install )
RUN ( git clone https://github.com/diegonehab/luasocket.git && cd luasocket && make && make install )

COPY scripts/* /var/lib/orthanc/scripts/

VOLUME [ "/var/lib/orthanc/log", "/var/lib/orthanc/db", "/var/lib/orthanc/idx", "/var/lib/orthanc/etc" ]
EXPOSE 4242
EXPOSE 8042

ENV STREAMER_URL="http://pacs.dccn.nl:3001"

WORKDIR /var/lib/orthanc
ENTRYPOINT [ "Orthanc", "--logdir=/var/lib/orthanc/log", "/var/lib/orthanc/etc" ]
