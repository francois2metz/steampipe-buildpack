# Buildpack: Steampipe

Run [Steampipe][] using buildpacks.

Use with [Scalingo][]: `scalingo env-set BUILDPACK_URL=https://github.com/francois2metz/steampipe-buildpack`

## Configuration

- `STEAMPIPE_VERSION`: the version of steampipe to install, latest by default (eg: `STEAMPIPE_VERSION=v0.15.3`)
- `STEAMPIPE_PLUGINS`: a space delimited list of plugins to install (eg: `STEAMPIPE_PLUGINS=net github`

## Procfile

**With dashboard**:

```
web: ./bin/steampipe dashboard --dashboard-port $PORT --dashboard-listen network
```

**Raw access to the postgres**

Add the [tcp addon](https://doc.scalingo.com/addons/tcp-gateway/start).

```
tcp: ./bin/steampipe service start --foreground --database-port $PORT --database-listen network
```

## Config files

You can copy put your config files anywhere as *.spc.erb* and they will be copied to the steampipe config directory after a pass with *erb*.

Example datadog.spc.erb:

```
connection "datadog" {
  plugin = "datadog"
  api_key = "<%= ENV['DATADOG_API_KEY'] %>"
  app_key = "<%= ENV['DATADOG_APP_KEY'] %>"
  api_url = "https://api.datadoghq.com/"
}
```

[steampipe]: https://steampipe.io/
[scalingo]: https://scalingo.com/
