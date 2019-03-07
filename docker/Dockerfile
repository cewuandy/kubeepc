FROM ubuntu:16.04

WORKDIR /root/

RUN apt update -y
RUN apt-get -y install autoconf libtool gcc pkg-config git flex bison libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev net-tools iptables python git

RUN git clone https://github.com/acetcom/nextepc
WORKDIR /root/nextepc

RUN autoreconf -iv
RUN ./configure --prefix=`pwd`/install
RUN make -j `nproc`
RUN make install

RUN grep -r "mongodb://localhost" | awk -F : '{print $1}' | xargs -i sed -i 's/localhost/mongodb-svc/g' {}

RUN git clone https://github.com/cewuandy/kubeepc
RUN cp kubeepc/docker/setup-pgwtun.sh setup-pgwtun.sh
