# docker-shadowsocksr

A fast tunnel proxy that helps you bypass firewalls.

## Build

You can pull the image from `hub.docker.com`.

```sh
$ docker pull bingozb/shadowsocksr
```

Or, you can build with source repository by yourself.

```sh
$ git clone https://github.com/bingozb/docker-shadowsocksr.git
$ cd docker-shadowsocksr
$ docker build -t bingozb/shadowsocksr .
```

## Usage

This is the fastest way to start a shadowsocks container with default config.

```sh
$ sudo docker run --restart always -d \ 
--name ssr \
-p 12188:12188 \
bingozb/shadowsocksr
```

| ENV | Values |
| --- | --- |
| SERVER_ADDR | 0.0.0.0 |
| SERVER_PORT | 12188 |
| PASSWORD | 01234567a |
| METHOD | aes-256-cfb |
| PROTOCOL | origin |
| PROTOCOLPARAM | 32 |
| OBFS | plain |
| TIMEOUT | 300 |

If you want to customize some configurations of shadowsocksr, you can run with tag `-e`, eg.:

```sh
$ sudo docker run --restart always -d \ 
--name ssr \
-e "SERVER_ADDR=0.0.0.0" \
-e "SERVER_PORT=12345" \
-e "PASSWORD=yourpassword" \
-e "METHOD=aes-128-ctr" \
-e "PROTOCOL=auth_aes128_md5" \
-e "PROTOCOLPARAM=32" \
-e "OBFS=tls1.2_ticket_auth_compatible" \
-e "TIMEOUT=300" \
-p 12345:12345 \
bingozb/shadowsocksr
```

Finally, check the iptables config and make sure that the firewall is not blocking the `SERVER_PORT`.

