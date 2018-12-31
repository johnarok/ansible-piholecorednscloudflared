### Ansible Roles for Pi-Hole, CoreDNS and Cloudflare's DNS over HTTPS 

#### Pre-requisite

PiHole needs to be installed first

```
git clone --depth 1 https://github.com/pi-hole/pi-hole.git Pi-hole
cd "Pi-hole/automated install/"
sudo bash basic-install.sh
```

also,

Populate `roles/coredns/files/zones` directory with your zone file for internal DNS

#### Usage

Update your local inventory file and then

`ansible-playbook playbook.yml -i inventory`

#### Architecture

PiHole listens on Port `53` and is the primary DNS for the clients

PiHole forwards DNS queries for specific homelab domains to CoreDNS

PiHole forwards DNS queries for all other queries to a cloudflared daemon 

Cloudflared listens on Port `5053` and proxies to CloudFlare for DNS over HTTPS

CoreDNS listens on Port `15353`

It is possible to have CoreDNS forward traffic to PiHole but then client visibility is lost on the PiHole's dashboard.

#### Credits 

https://blog.jstubberfield.net/pihole-conditional-forwarding/

https://docs.pi-hole.net/guides/dns-over-https/

https://bendews.com/posts/implement-dns-over-https/

https://blog.idempotent.ca/2018/04/18/run-your-own-home-dns-on-coredns/

