FROM debian:jessie

RUN apt-get update && apt-get install --no-install-recommends -y \
               ipmitool \
               python \
               curl \
               vim-tiny \
               less \
               ca-certificates \
               sudo \
               dmidecode \
               ifupdown \
               lshw \
               lsscsi \
               pciutils \
               ethtool \
               smartmontools \
               ohai \
               lldpd \
               hdparm \
               udev \
               sg3-utils \
               coreutils \
               scrub \
               gdisk \
               lib32gcc1 \
               lib32ncurses5 \
               lib32stdc++6 \
               libc6-i386 \
               libncurses5 \
    && rm -rf /var/lib/apt/lists/*

ENV NODE_VERSION 4.6.2
RUN curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
    && tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
    && rm "node-v$NODE_VERSION-linux-x64.tar.gz"

ARG STORCLI=storcli_1.17.08_all.deb
ADD $STORCLI .
RUN dpkg -i $STORCLI \
    && rm $STORCLI

ARG SAS2=sas2ircu
ADD $SAS2 /opt

ARG SAS3=sas3ircu
ADD $SAS3 /opt

ADD sas_info.py /opt

ARG PERCCLI=perccli_1.11.03-1_all.deb
ADD $PERCCLI .
RUN dpkg -i --force-depends $PERCCLI \
    && rm $PERCCLI

ADD entry.bash /usr/local/bin/
CMD /usr/local/bin/entry.bash
