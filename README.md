# Selfhost services inside your tailnet

You'll need Docker, your own tailnet, hands.

Inside your admin console on Tailscale go ahead and grab yourself a auth key (Settings - Personal Settings - Keys). Make sure its not ephemeral (unless you want to). Make sure you have HTTPS and MagicDNS enabled.

## Vaultwarden Setup

Grab docker-compose file from docker/vaultwarden and make sure to edit environment variables:

* TS_AUTHKEY: authkey you have generated to access your tailnet

* TS_HOSTNAME: hostname to be used to access your vaultwarden instance inside tailnet (HOSTNAME.tailnet.ts.net)

* POSTGRES_PASSWORD: your custom password for postgres database

* DATABASE_URL: put your custom password for postgres database

* DOMAIN: full url to be accessible from your tailnet.

Use `docker compose up -d` to start your vaultwarden setup. New device should appear in your tailnet with hostname you have set.

After making sure that vaultwarden instance is running, you need to configure tailscale to serve your application.

```
# docker exec -it vaultwarden-ts sh
# tailscale serve -bg localhost:8080
```

Application should be available at device domain.

