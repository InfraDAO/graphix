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

#### Edit config.tmpl for different data sources. By default it checks arbitrum one and arbitrum goerli. 
```bash
databaseUrl: postgres://${DB_USER}:${DB_PASS}@postgres:5432/${DB_NAME}
sources:
 # - type: networkSubgraph
 #   endpoint: https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-goerli
 #   query: byAllocations
 #   stakeThreshold: 0.0
 #   limit: 1000
 # - type: networkSubgraph
 #   endpoint: https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-mainnet
 #   query: byAllocations
 #   stakeThreshold: 0.0
 #   limit: 1000
  - type: networkSubgraph
    endpoint: https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-arbitrum-goerli
    query: byAllocations
    stakeThreshold: 0.0
    limit: 1000
  - type: networkSubgraph
    endpoint: https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-arbitrum
    query: byAllocations
    stakeThreshold: 0.0
    limit: 1000
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
Add `GRAPHQL_HOST=graphql.mydomain.com` to .env file
