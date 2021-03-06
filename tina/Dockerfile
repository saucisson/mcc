FROM debian:stable-slim

RUN true \
 && echo "APT::Install-Recommends "0";" >> /etc/apt/apt.conf.d/10norecommends \
 && echo "APT::Install-Suggests "0";"   >> /etc/apt/apt.conf.d/10norecommends \
 && apt-get update \
 && apt-get install \
            --yes \
            --fix-missing \
            bash \
            build-essential \
            curl \
            jq \
            man \
            libglpk-dev \
            libgmp-dev \
 && curl http://shoup.net/ntl/ntl-10.5.0.tar.gz \
         --output ntl-10.5.0.tar.gz \
    && tar xf ntl-10.5.0.tar.gz \
    && cd ntl-10.5.0/src \
    && ./configure \
    && make \
    && make install \
    && cd ../.. \
    && rm -rf ntl-10.5.0* \
 && curl ftp://ftp.math.ethz.ch/users/fukudak/cdd/cddlib-094h.tar.gz \
         --output cddlib-094h.tar.gz \
    && tar xf cddlib-094h.tar.gz \
    && cd cddlib-094h \
    && ./configure \
    && make install \
    && cd .. \
    && rm -rf cddlib-094h* \
 && curl http://projects.laas.fr/tina/binaries/tina-3.4.4-x86_64-linux.tar.gz \
         --output tina-3.4.4-x86_64-linux.tar.gz \
    && tar zxf tina-3.4.4-x86_64-linux.tar.gz \
           --directory /usr/ \
           --strip-components 1 \
    && rm -f tina-3.4.4-x86_64-linux.tar.gz \
 && apt-get purge \
            --yes \
            build-essential \
 && apt-get autoremove \
            --yes \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && true

COPY from-vm/bin/flags  /usr/share/tina/flags
COPY from-vm/bin/net    /usr/share/tina/net
COPY from-vm/bin/tina/* /usr/bin/
COPY mcc-head           /usr/bin/

WORKDIR    /mcc-data
VOLUME     [ "/mcc-data" ]
ENTRYPOINT [ "mcc-head"  ]
CMD        [ "--help"    ]
