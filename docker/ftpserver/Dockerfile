FROM debian:13

RUN apt update  && apt install -y \
    procps \
    iproute2 \
    iputils-ping \
    vsftpd \
    dnsutils \
    rsyslog \
    passwd \
    && rm -rf /var/lib/apt/lists/*

# Crear usuarios con home e pass "a"
RUN for u in gandalf saruman aragorn frodo; do \
        useradd -m "$u" && \
        echo "$u:a" | chpasswd  &&\
        mkdir -p /home/$u/public_html &&\
        chmod a-w /home/$u &&\
        chown -R "$u:$u" /home/$u ;\
    done
RUN mkdir -p /sauron/test && chmod 777 /sauron/test \
    && chmod a-w /sauron

COPY entrypoint.sh /sbin
RUN chmod a+x /sbin/entrypoint.sh

RUN touch /var/log/ftp.log && chmod a+w /var/log/ftp.log

RUN sed -i 's/^\s*module(load="imklog")/#module(load="imklog")/' /etc/rsyslog.conf

ENTRYPOINT ["/sbin/entrypoint.sh"]
