FROM ubuntu:20.04


RUN apt update

RUN apt-get install -y tzdata
# timezone setting
ENV TZ=Asia/Tokyo

ENV DEBIAN_FRONTEND=noninteractive

RUN apt install -y xrdp openbox obconf xterm supervisor \
 && rm -rf /var/lib/apt/lists/* /var/cache/apt/*


# 適当に0番のターミナルエミュレータを選択したが駄目だった
#RUN echo 0 | update-alternatives --config x-terminal-emulator
# おそらく同じ操作をする
RUN rm /etc/alternatives/x-terminal-emulator \
 && ln -s /usr/bin/xterm /etc/alternatives/x-terminal-emulator \
 && rm /usr/bin/x-terminal-emulator \
 && ln -s /etc/alternatives/x-terminal-emulator  /usr/bin/x-terminal-emulator

RUN echo root:secret | chpasswd

# OpenBoxを起動するようにする
RUN echo openbox-session > /root/.xsession

# supervisordの設定
COPY supervisord.conf /etc/supervisord.conf

# 手動で下記を実行するとxrdpが上がる
# /etc/init.d/xrdp start
#CMD [ "/bin/bash" ]
CMD [ "supervisord" ]