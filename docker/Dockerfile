FROM ubuntu:focal

# register arguments (from make)
ARG REPO

# Add isc-kea repository
ADD https://dl.cloudsmith.io/public/isc/${REPO}/cfg/gpg/gpg.4DD5AE28ADA7268E.key /etc/apt/trusted.gpg.d/kea.asc
RUN chmod 0644 /etc/apt/trusted.gpg.d/kea.asc \
  && apt-get update \
  && apt-get install -y ca-certificates \
  && echo "deb [arch=amd64] https://dl.cloudsmith.io/public/isc/${REPO}/deb/ubuntu focal main" >> /etc/apt/sources.list

# Install isc-kea-dhcp4-server
RUN apt-get update \
  && apt-get dist-upgrade -y \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y isc-kea-dhcp4-server \
  && rm -rf /var/lib/apt/lists/*

EXPOSE 67/udp

CMD ["/usr/sbin/kea-dhcp4","-c","/etc/kea/kea-dhcp4.conf"]
