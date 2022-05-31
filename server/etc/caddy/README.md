## Install

```bash
# Get xcaddy & golang
cd dot/server/etc/caddy
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/xcaddy/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-xcaddy-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/xcaddy/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-xcaddy.list
sudo apt update
sudo apt install xcaddy golang

# Build xcaddy; FIXME: currently the gandi plugin will encounter checksum error, thus we disable it for a while...
# <https://github.com/caddy-dns/gandi/issues/1#issuecomment-991991307>
GOSUMDB=off xcaddy build --with github.com/caddy-dns/gandi
sudo ln -sfv "$PWD/caddy" /usr/local/bin/caddy

# Copy configurations & edit token
sudo mkdir /etc/caddy
sudo ln -sfv "$PWD/Caddyfile" /etc/caddy/Caddyfile
echo "GANDI_API_TOKEN=XXX" | sudo tee /etc/caddy/env # or use vi for security

# Setup users; from <https://github.com/caddyserver/dist/tree/master/init>
sudo groupadd --system caddy
sudo useradd --system \
    --gid caddy \
    --create-home \
    --home-dir /var/lib/caddy \
    --shell /usr/sbin/nologin \
    --comment "Caddy web server" \
    caddy

# Config as service; TODO: --user
sudo cp -fv "$PWD/caddy.service" /lib/systemd/system/caddy.service
sudo systemctl daemon-reload
sudo systemctl start caddy
sudo systemctl enable caddy
```

TODO: regular updates? with cron?
