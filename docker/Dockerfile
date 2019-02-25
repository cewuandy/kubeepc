FROM ubuntu:16.04

WORKDIR /root/

COPY nextepc.tar.gz .
RUN tar zxvf nextepc.tar.gz 

WORKDIR /root/nextepc

RUN apt update -y
RUN apt-get -y install autoconf libtool gcc pkg-config git flex bison libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev net-tools iptables

RUN autoreconf -iv
RUN ./configure --prefix=`pwd`/install
RUN make -j `nproc`
RUN make install

WORKDIR /root/nextepc/install/etc/nextepc/
COPY nextepc.conf nextepc.conf
RUN chmod 644 nextepc.conf
RUN chown root:root nextepc.conf

RUN grep -r "mongodb://localhost" | awk -F : '{print $1}' | xargs -i sed -i 's/localhost/mongodb-svc/g' {}

WORKDIR /root/nextepc

CMD ./nextepc-epcd
