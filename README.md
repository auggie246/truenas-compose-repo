## IMPORTANT NOTES:
Setting up private services (local network only)
- When setting up services that do not need to be exposed for external access, use the non-external entrypoint.
- Rewrite the domain to the docker host's IP (i.e traefik's ip).
- Whitelist domain in your router's DNS rebinding protection - I am using OpenWRT, and under Network > DHCP and DNS > Filter > Keep rebind protection enabled > add domain to "Domain Whitelist"
- I had to also remove my nextdns server from Portmaster and move it to Adguard Home as an upstream server. Portmaster was preventing rewrite as it skips Adguard and went to NextDNS.