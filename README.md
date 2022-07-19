# Buildpack: Steampipe

Run [Steampipe][] using buildpacks.

Use with Scalingo: `scalingo env-set BUILDPACK_URL=https://github.com/francois2metz/steampipe-buildpack`

## Procfile

**With dashboard**:

```
web: ./bin/steampipe dashboard --dashboard-port $PORT --dashboard-listen network
```

**Raw access to the postgres**

Add the tcp addon.

```
tcp: ./bin/steampipe service start --foreground --database-port $PORT --database-listen network
```

[steampipe]: https://steampipe.io/
