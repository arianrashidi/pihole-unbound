# Docker Compose project with Pi-hole and Unbound
IMPORTANT: Either use this locally or with a VPN. This project is not meant to be used on a public server.

## Setup
1. Start with a new Ubuntu 22 server.
2. Close all ports except 22 TCP for SSH, 53 TCP/UDP for DNS and 80 TCP for the web interface.
3. Install Docker.
4. Run `sudo sed -r -i.orig 's/#?DNSStubListener=yes/DNSStubListener=no/g' /etc/systemd/resolved.conf`, `sudo sh -c 'rm /etc/resolv.conf && ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf'` and `sudo systemctl restart systemd-resolved`.
5. Clone this repository to `/srv/pihole-unbound`.
6. Run `sudo docker-compose up -d` in the cloned directory.
7. Get your web interface password with `sudo docker logs pihole | grep random`.
8. Check if everything is working by browsing to `http://<your-ip>/admin` and entering the password from the last step.

## Update
`cd /srv/pihole && sudo docker-compose down -t 120 && sudo docker-compose pull && sudo docker-compose up -d --remove-orphans && sudo docker image prune`
