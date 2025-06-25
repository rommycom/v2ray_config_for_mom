``` json
{
  "log": {
    "level": "warn",
    "timestamp": true
  },
  "dns": {
    "servers": [
      {
        "tag": "remote",
        "address": "tcp://8.8.8.8",
        "strategy": "prefer_ipv4",
        "detour": "proxy"
      },
      {
        "tag": "local",
        "address": "223.5.5.5",
        "strategy": "prefer_ipv4",
        "detour": "direct"
      },
      {
        "tag": "block",
        "address": "rcode://success"
      },
      {
        "tag": "local_local",
        "address": "223.5.5.5",
        "detour": "direct"
      }
    ],
    "rules": [
      {
        "server": "local_local",
        "domain": [
          "series-a1.samanehha.co"
        ]
      },
      {
        "server": "remote",
        "clash_mode": "Global"
      },
      {
        "server": "local_local",
        "clash_mode": "Direct"
      },
      {
        "server": "local",
        "rule_set": [
          "geosite-cn"
        ]
      }
    ],
    "final": "remote"
  },
  "inbounds": [
    {
      "type": "mixed",
      "tag": "socks",
      "listen": "127.0.0.1",
      "listen_port": 10808,
      "sniff": true,
      "sniff_override_destination": true
    }
  ],
  "outbounds": [
    {
      "type": "shadowsocks",
      "tag": "proxy",
      "server": "series-a1.samanehha.co",
      "server_port": 443,
      "method": "chacha20-ietf-poly1305",
      "password": "W74XFALLLuw6m5IA"
    },
    {
      "type": "direct",
      "tag": "direct"
    },
    {
      "type": "block",
      "tag": "block"
    },
    {
      "type": "dns",
      "tag": "dns_out"
    }
  ],
  "route": {
    "rules": [
      {
        "outbound": "proxy",
        "clash_mode": "Global"
      },
      {
        "outbound": "direct",
        "clash_mode": "Direct"
      },
      {
        "outbound": "dns_out",
        "protocol": [
          "dns"
        ]
      },
      {
        "outbound": "block",
        "network": [
          "udp"
        ],
        "port": [
          443
        ]
      },
      {
        "outbound": "direct",
        "ip_is_private": true
      },
      {
        "outbound": "direct",
        "rule_set": [
          "geosite-private"
        ]
      },
      {
        "outbound": "proxy",
        "port_range": [
          "0:65535"
        ]
      }
    ],
    "rule_set": [
      {
        "tag": "geosite-private",
        "type": "local",
        "format": "binary",
        "path": "C:\\Users\\ASUS\\Desktop\\desktop (full of it no half)\\v2\\bin\\srss\\geosite-private.srs"
      },
      {
        "tag": "geosite-cn",
        "type": "local",
        "format": "binary",
        "path": "C:\\Users\\ASUS\\Desktop\\desktop (full of it no half)\\v2\\bin\\srss\\geosite-cn.srs"
      }
    ]
  },
  "experimental": {
    "cache_file": {
      "enabled": true,
      "path": "C:\\Users\\ASUS\\Desktop\\desktop (full of it no half)\\v2\\bin\\cache.db"
    },
    "clash_api": {
      "external_controller": "127.0.0.1:10813"
    }
  }
}
```
