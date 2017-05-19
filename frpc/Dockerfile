FROM alpine:3.5

WORKDIR /tmp

RUN apk add --no-cache wget

RUN mkdir /tmp/frp && \
    mkdir /etc/frp && \
    cd /tmp/frp && \
    ver=$(wget --no-check-certificate -qO- https://api.github.com/repos/fatedier/frp/releases/latest | grep 'tag_name' | cut -d\" -f4) && \
	frp_ver="frp_$(echo ${ver} | sed -e 's/^[a-zA-Z]//g')" && \
    wget --no-check-certificate "https://github.com/fatedier/frp/releases/download/${ver}/${frp_ver}_linux_amd64.tar.gz" && \
    tar zxf ${frp_ver}_linux_amd64.tar.gz && \
    mv /tmp/frp/${frp_ver}_linux_amd64/frpc /usr/local/bin/frpc && \
    chmod +x /usr/local/bin/frpc && \
    mv /tmp/frp/${frp_ver}_linux_amd64/frpc.ini /etc/frpc.ini


CMD ["frpc", "-c", "/etc/frp/frpc.ini"]