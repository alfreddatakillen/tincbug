FROM debian:jessie

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install build-essential gzip tar wget liblzo2-dev lib32z1-dev lib32ncurses5-dev libreadline-dev libssl-dev

RUN cd /opt && wget https://www.tinc-vpn.org/packages/tinc-1.1pre14.tar.gz && tar xzvf tinc-1.1pre14.tar.gz && rm tinc-1.1pre14.tar.gz
RUN cd /opt/tinc-1.1pre14 && ./configure && make && make install
RUN mkdir -p /usr/local/var/run && mkdir -p /usr/local/etc/tinc/nurd/hosts

RUN /usr/local/sbin/tinc -n superheroes init batman
RUN echo "\nAddress = batman" >>/usr/local/etc/tinc/superheroes/hosts/batman

CMD /usr/local/sbin/tincd -n superheroes -D --logfile /dev/stdout
