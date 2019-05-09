# Serve Massive Concurrent Clients
Since Keikai server runs in a single thread for DartVM architecture, we can put a reverse proxy server to serve static JavaScript files between Keikai server and browsers to handle lots of concurrent requests from browsers at the same time.

browser  <----> reverse proxy  <---> application server & Keikai engine

## Proxy Server Configuration Example
Here is an Nginx (as a proxy server) sample configuration.

* Keikai engine port: 8888
* application server port: 8080


```
http {
    gzip on;
    gzip_vary on;
    gzip_min_length 2048;
    gzip_comp_level 9;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain application/javascript text/css application/xml text/javascript;
    gzip_disable "MSIE [1-6]\.";

    map $http_upgrade $connection_upgrade {
        default upgrade;
        ''      close;
    }
}
```

```
server {
    listen 80;
    rewrite_log on;

    client_max_body_size 100m;

    # map all requests to default port to application server
    location / {
        proxy_pass http://app-server:8080;
    }

    # map a websocket request to Keikai server
    location ~ /ws/(.*) {
        if ($http_upgrade = "websocket") {
            proxy_pass http://keikai-server:8888;
        }
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
    }

    # serve static files of Keikai server
    location /s/api/dart/ {
        alias /KEIKAI-SERVER-FOLDER/keikai/src/web/client/dart/;
    }
    location ~ \/.*\/s\/api\/dart\/(.*)[^\.js|^\.svg|^\.ttf]$ {
        rewrite \/.*\/s\/api\/dart\/(.*)[^\.js|^\.svg|^\.ttf]$ /s/api/dart/main.dart.js;
    }
    location ~ \/.*\/s\/api\/dart\/(.*)\.js$ {
        rewrite \/.*\/s\/api\/dart\/(.*)\.js$ /s/api/dart/$1.js;
    }
    location ~ \/.*\/s\/api\/dart\/packages\/(.*)$ {
        rewrite \/.*\/s\/api\/dart\/packages\/(.*)$ /s/api/dart/packages/$1;
    }
}
```
[Nginx Doc](https://nginx.org/en/docs/)


# Filling lots of cells
set number format first to stop smart input parsing.


# Enforce re-calculating

```java
Settings clone = Settings.DEFAULT_SETTINGS.clone();
ToolbarSettings toolbar = ToolbarSettings.DEFAULT.clone();
toolbar.setOptions(UICommand.UPLOAD, "recalculate=true"); // recalculate all formula
clone.set(Settings.Key.SPREADSHEET_CONFIG, Maps.toMap("toolbar", toolbar);

Keikai.newClient(remoteServer, clone);
```

Or

```
spreadsheet.imports("bookName", file, true); // true => recalculate
```