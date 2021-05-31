# Pterodactyl with Traefik

Copy the `.env.example` to `.env` and change the values to fit your server

Use your global Traefik network so that the redirects work, we call the network `proxy`, if your default network is called something else change it in the `.env`
and at line `114` of the `docker-compose.yml` accordingly.

Create a volume for the certificates with the command:
```sh
docker volume create --name=LetsEncrypt
```

Be sure that you have set the volume for your traefik instance as well

```yml
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "./config:/etc/traefik"
      - "LetsEncrypt:/LetsEncrypt"
```

Make sure you have this in the `dynanic_config.yml` of traefik

```yml
certificatesResolvers:
  dns:
    acme:
      email: your@domain.com
      storage: /LetsEncrypt/acme.json
      dnsChallenge:
        provider: cloudflare
```

especially `storage` is important!

Make sure that in the `traefik.yml` of traefik you also set the storage to `/LetsEncrypt/acme.json`.

You have to replace `./Panel/nginx/default.conf` in the folder with ours.

Then replace in our config all entries `<domain>` to your domain.

**IMPORTANT!**

After creating a node go to the tab `Configuration` and copy the files into the desired directory of Pterodactyl and change the name of the certificates to:
* `fullchain.pem` = `cert.pem`
* `privatkey.pem` = `key.pem`
