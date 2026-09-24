ARG BUILD_FROM
FROM $BUILD_FROM

ARG FRP_VERSION="0.58.0"
ARG BUILD_ARCH

RUN apk add --no-cache curl tar jq \
    && ARCH_MAP_amd64="amd64" \
    && ARCH_MAP_aarch64="arm64" \
    && ARCH_MAP_armv7="arm" \
    && ARCH=$(eval echo \$ARCH_MAP_${BUILD_ARCH}) \
    && curl -L "https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_${ARCH}.tar.gz" -o /tmp/frp.tar.gz \
    && tar -xzf /tmp/frp.tar.gz -C /tmp \
    && cp /tmp/frp_${FRP_VERSION}_linux_${ARCH}/frpc /usr/bin/frpc \
    && chmod +x /usr/bin/frpc \
    && rm -rf /tmp/frp* \
    && apk del tar

COPY run.sh /etc/s6-overlay/s6-rc.d/frpc/run
RUN chmod a+x /etc/s6-overlay/s6-rc.d/frpc/run \
    && echo "longrun" > /etc/s6-overlay/s6-rc.d/frpc/type \
    && mkdir -p /etc/s6-overlay/s6-rc.d/user/contents.d \
    && touch /etc/s6-overlay/s6-rc.d/user/contents.d/frpc
