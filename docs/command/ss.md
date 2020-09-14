# ss

---

**bbr**

    # BBr安装
    wget "https://github.com/chiakge/Linux-NetSpeed/raw/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

**server**

    # new install
    https://github.com/v2fly/fhs-install-v2ray

    # install v2ray (old)
    bash -c "$(curl -L -s https://install.direct/go.sh)"

    # check
    /usr/bin/v2ray/v2ray -test -config=/etc/v2ray/config.json
    systemctl start v2ray
    systemctl restart v2ray

    # BBR
    bash -c 'echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf'
    bash -c 'echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf'
    sysctl -p
    sysctl net.ipv4.tcp_congestion_control

**client**

    # enable
    systemctl enable v2ray

    # /etc/v2ray/config.json
    {
    "policy": null,
    "log": {
        "access": "",
        "error": "",
        "loglevel": "warning"
    },
    "inbounds": [
        {
        "tag": "proxy",
        "port": 10808,
        "listen": "127.0.0.1",
        "protocol": "socks",
        "sniffing": {
            "enabled": true,
            "destOverride": [
            "http",
            "tls"
            ]
        },
        "settings": {
            "auth": "noauth",
            "udp": true,
            "ip": null,
            "address": null,
            "clients": null
        },
        "streamSettings": null
        }
    ],
    "outbounds": [
        {
        "tag": "proxy",
        "protocol": "vmess",
        "settings": {
            "vnext": [
            {
                "address": "xxx",
                "port": xxx,
                "users": [
                {
                    "id": "xxx",
                    "alterId": 64,
                    "email": "t@t.tt",
                    "security": "auto"
                }
                ]
            }
            ],
            "servers": null,
            "response": null
        },
        "streamSettings": {
            "network": "tcp",
            "security": null,
            "tlsSettings": null,
            "tcpSettings": null,
            "kcpSettings": null,
            "wsSettings": null,
            "httpSettings": null,
            "quicSettings": null
        },
        "mux": {
            "enabled": true,
            "concurrency": 8
        }
        },
        {
        "tag": "direct",
        "protocol": "freedom",
        "settings": {
            "vnext": null,
            "servers": null,
            "response": null
        },
        "streamSettings": null,
        "mux": null
        },
        {
        "tag": "block",
        "protocol": "blackhole",
        "settings": {
            "vnext": null,
            "servers": null,
            "response": {
            "type": "http"
            }
        },
        "streamSettings": null,
        "mux": null
        }
    ],
    "stats": null,
    "api": null,
    "dns": null,
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
        {
            "type": "field",
            "port": null,
            "inboundTag": [
            "api"
            ],
            "outboundTag": "api",
            "ip": null,
            "domain": null
        }
        ]
    }
    }