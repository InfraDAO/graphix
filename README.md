# Graphix

Primary Repo https://github.com/edgeandnode/graphix

#### Edit .env
```bash
DB_USER=db_admin
DB_PASS=db_password
DB_NAME=graphix
ADMIN_USER=admin
ADMIN_PASSWORD=password
GRAFANA_HOST=grafana.yourdomain.com
EMAIL=email@aol.com
```

#### Run Graphix
```
bash start
```

#### Reload Changes
```
bash start --force-recreate
```

#### Add Graphql Endpoint UI

`Add the following to the end of graphix api container`

```bash
    labels:
      - "org.label-schema.group=monitoring"
      - "traefik.enable=true"
      - "traefik.http.services.graphql.loadbalancer.server.port=3030"
      - "traefik.http.routers.graphql.entrypoints=websecure"
      - "traefik.http.routers.graphql.tls.certresolver=myresolver"
      - "traefik.http.routers.graphql.rule=Host(`$GRAPHQL_HOST`)"

```
Add GRAPHQL_HOST=graphql.mydomain.com to .env file
