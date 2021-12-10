FROM ubuntu:20.04

LABEL maintainer="paulokinjo@hotmail.com"

ENV DEBIAN_FRONTEND="noninteractive"


RUN apt-get update && \
    apt-get install -y ssmtp

# remove some pointless services
RUN /usr/sbin/update-rc.d -f ondemand remove; \
  for f in \
  /etc/init/u*.conf \
  /etc/init/mounted-dev.conf \
  /etc/init/mounted-proc.conf \
  /etc/init/mounted-run.conf \
  /etc/init/mounted-tmp.conf \
  /etc/init/mounted-var.conf \
  /etc/init/hostname.conf \
  /etc/init/networking.conf \
  /etc/init/tty*.conf \
  /etc/init/plymouth*.conf \
  /etc/init/hwclock*.conf \
  /etc/init/module*.conf\
  ; do \
  dpkg-divert --local --rename --add "$f"; \
  done; \
  echo '# /lib/init/fstab: cleared out for bare-bones Docker' > /lib/init/fstab

# supervisor installation &&
# create directory for child images to store configuration in
RUN apt-get -y install supervisor && \
  mkdir -p /var/log/supervisor && \
  mkdir -p /etc/supervisor/conf.d

# supervisor base configuration 
ADD supervisor.conf /etc/supervisor.conf

# default command
CMD ["supervisord", "-c", "/etc/supervisor.conf"]