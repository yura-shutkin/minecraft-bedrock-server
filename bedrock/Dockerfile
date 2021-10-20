FROM ubuntu:20.04 as downloader

ARG MINECRAFT_VERSION=1.17.11.01

RUN apt update && apt install -y wget unzip
WORKDIR minecraft
RUN wget https://minecraft.azureedge.net/bin-linux/bedrock-server-${MINECRAFT_VERSION}.zip
RUN unzip bedrock-server-${MINECRAFT_VERSION}.zip && rm bedrock-server-${MINECRAFT_VERSION}.zip

FROM ubuntu:20.04

RUN apt update && apt -y install libcurl4 && apt -y full-upgrade && apt -y autoremove && apt -y autoclean

WORKDIR minecraft
RUN useradd -ms /sbin/nologin minecraft
USER minecraft

COPY --chown=minecraft:minecraft --from=downloader /minecraft .

CMD ./bedrock_server
