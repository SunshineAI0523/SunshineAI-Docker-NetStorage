# FROM jamesmith0817/sunshineai-debian-bullseye
FROM debian:12
# COPY sources-bookworm.list /etc/apt/sources.list
# COPY pip.conf /root/.config/pip/pip.conf
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
    mkdir -vp "/DATA/Media/TV_Shows"
RUN tree /DATA && echo "Create Folder Complete !!!" 
RUN apt update && \
    apt install supervisor* libturbojpeg* ffmpeg dumb-init systemd -y 
RUN sudo adduser cloudreve --quiet --disabled-login --disabled-password --home /home/cloudreve --gecos ""
RUN sudo adduser alist --quiet --disabled-login --disabled-password --home /home/alist  --gecos ""
RUN sudo adduser minio --quiet --disabled-login --disabled-password --home /home/minio --gecos ""
RUN wget "https://github.com/cloudreve/Cloudreve/releases/download/3.8.3/cloudreve_3.8.3_linux_amd64.tar.gz" -O cloudreve.tar.gz
RUN tar -zxvf cloudreve.tar.gz -C /home/cloudreve/ && rm -rf cloudreve.tar.gz
RUN tree /home/cloudreve/
RUN chmod +x /home/cloudreve/cloudreve
RUN wget "https://github.com/AlistGo/alist/releases/download/v3.41.0/alist-linux-amd64.tar.gz" -O alist-linux-amd64.tar.gz
RUN tar -zxvf alist-linux-amd64.tar.gz -C /home/alist/ && rm -rf alist-linux-amd64.tar.gz && ln -s /home/alist/alist  /usr/bin/alist
RUN tree /home/alist/
RUN chmod +x /home/alist/alist
RUN mkdir -vp /etc/supervisor/conf.d/
RUN wget "https://dl.min.io/server/minio/release/linux-amd64/minio" -O /home/minio/minio
RUN chmod +x /home/minio/minio
COPY supervisord.conf /etc/supervisor/
COPY cloudreve.conf /etc/supervisor/conf.d/
COPY alist.conf /etc/supervisor/conf.d/
COPY aria2.conf /etc/supervisor/conf.d/
COPY minio.conf /etc/supervisor/conf.d/
RUN mkdir -vp /run/systemd 
STOPSIGNAL SIGRTMIN+3
ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "/usr/bin/supervisord -c /etc/supervisor/supervisord.conf && service transmission-daemon start && bash" ]