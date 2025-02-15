# FROM jamesmith0817/sunshineai-debian-bullseye
FROM debian:12
# COPY sources-bookworm.list /etc/apt/sources.list
COPY pip.conf /root/.config/pip/pip.conf
RUN mkdir -vp /etc/supervisor/conf.d/
RUN apt update && apt full-upgrade -y && apt install tree sudo htop wget* curl* build-e* qbittorrent-* transmission-* aria* -y 
RUN mkdir -vp "/DATA" && \
    mkdir -vp "/DATA/AppData" && \ 
    mkdir -vp "/DATA/Documents" && \
    mkdir -vp "/DATA/Downloads" && \
    mkdir -vp "/DATA/Gallery" && \
    mkdir -vp "/DATA/Compressed" && \
    mkdir -vp "/DATA/Desktop" && \
    mkdir -vp "/DATA/Games" && \
    mkdir -vp "/DATA/General" && \
    mkdir -vp "/DATA/ISOS" && \
    mkdir -vp "/DATA/Media" && \
    mkdir -vp "/DATA/Others" && \
    mkdir -vp "/DATA/Programs" && \
    mkdir -vp "/DATA/Public" && \
    mkdir -vp "/DATA/Templates" && \
    mkdir -vp "/DATA/Tools" && \
    mkdir -vp "/DATA/Torrents" && \
    mkdir -vp "/DATA/Videos" && \
    mkdir -vp "/DATA/Media/Movies" && \
    mkdir -vp "/DATA/Media/Music" && \ 
    mkdir -vp "/DATA/Media/TV_Shows" && \
    tree /DATA && echo "Create Folder Complete !!!" 
RUN apt update && \
    apt install supervisor* libturbojpeg* ffmpeg dumb-init systemd rsync* openssh* -y && \
    sudo adduser cloudreve --quiet --disabled-login --disabled-password --home /home/cloudreve --gecos "" && \
    sudo adduser alist --quiet --disabled-login --disabled-password --home /home/alist  --gecos "" && \
    sudo adduser minio --quiet --disabled-login --disabled-password --home /home/minio --gecos "" && \
    sudo adduser meilisearch --quiet --disabled-login --disabled-password --home /home/meilisearch --gecos ""
RUN wget "https://github.com/cloudreve/Cloudreve/releases/download/3.8.3/cloudreve_3.8.3_linux_amd64.tar.gz" -O cloudreve.tar.gz && \
    tar -zxvf cloudreve.tar.gz -C /home/cloudreve/ && rm -rf cloudreve.tar.gz && tree /home/cloudreve/ && chmod +x /home/cloudreve/cloudreve
RUN wget "https://github.com/AlistGo/alist/releases/download/v3.41.0/alist-linux-amd64.tar.gz" -O alist-linux-amd64.tar.gz && \
    tar -zxvf alist-linux-amd64.tar.gz -C /home/alist/ && rm -rf alist-linux-amd64.tar.gz && ln -s /home/alist/alist  /usr/bin/alist && \
    tree /home/alist/ && chmod +x /home/alist/alist && mkdir -vp /home/alist/data 
COPY alist.config.json /home/alist/config.json
RUN wget "https://dl.min.io/server/minio/release/linux-amd64/minio" -O /home/minio/minio && chmod +x /home/minio/minio
RUN wget "https://github.com/meilisearch/meilisearch/releases/download/v1.12.8/meilisearch-linux-amd64" -O /home/meilisearch/meilisearch && chmod +x /home/meilisearch/meilisearch
RUN chown meilisearch:meilisearch /home/meilisearch/meilisearch
RUN mkdir /var/lib/meilisearch/data /var/lib/meilisearch/dumps /var/lib/meilisearch/snapshots
RUN chown -R meilisearch:meilisearch /var/lib/meilisearch
RUN chmod 750 /var/lib/meilisearch
RUN curl https://raw.githubusercontent.com/meilisearch/meilisearch/latest/config.toml > /etc/meilisearch.toml
COPY supervisord.conf /etc/supervisor/
COPY cloudreve.conf /etc/supervisor/conf.d/
COPY alist.conf /etc/supervisor/conf.d/
COPY aria2.conf /etc/supervisor/conf.d/
COPY minio.conf /etc/supervisor/conf.d/
COPY homeassistant.conf /etc/supervisor/conf.d/
COPY meilisearch.conf /etc/supervisor/conf.d/
RUN mkdir -vp /run/systemd 
STOPSIGNAL SIGRTMIN+3
ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "/usr/bin/supervisord -c /etc/supervisor/supervisord.conf && service transmission-daemon start && service ssh start && service rsync start && bash" ]