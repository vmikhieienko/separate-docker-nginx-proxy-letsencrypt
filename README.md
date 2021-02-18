# Separate Docker setup for Nginx + Letsencrypt

Allows to have multiple `docker-compose` projects running on one machine.

To run the setup follow these steps:

- Run a command to create and run a separate nginx setup:
```yaml
docker-compose -f proxy.yml up -d
```

- Run a command to create and run a separate app setup:
```yaml
docker-compose -f app.yml up -d
```



Make sure all containers in your app that must be available from the web have explicit
service-level option with both internal/external networks.
```
web:
    ...
    networks: 
     - proxy-tier
     - backend-tier
    ...
```

For others use only internal one:
```
db:
    ...
    networks: 
     - backend-tier
    ...
```