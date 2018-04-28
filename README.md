# PHP 5.2 (FPM) + XDebug / MySQL 5.5 / Nginx

This set of docker containers will run on port 80, so you'll need to shut down any previously running web servers before starting the container service.

To initialize the containers (only needs to run once):
```
docker-compose build
```

To start the containers:
```
docker-compose up
```

MySQL will be accessible on port 3307, so there should be no need to shutdown other MySQL services.

XDebug is setup to connect on port 9001 on IP 10.254.254.254 - which I normally set up as a [loopback alias for virtual machines](http://www.foell.org/justin/virtualbox-connect-to-ubuntu-host-served-website/).

You can override the XDebug settings and other docker values mentioned on this page with a [docker-compose.override.yml](https://docs.docker.com/compose/extends/) file.

My VSCode/XDebug configuration looks like this:
```
{
	"name": "Listen for XDebug",
	"type": "php",
	"request": "launch",
	"port": 9001,
	"pathMappings": {
		"/var/www/html": "${workspaceRoot}"
	}
}
```

Put your website/application in the `public_html`. For example you can add a WordPress install via CLI `wp core download --path=public_html`

The MySQL hostname is `mysql` and the MySQL user/pass defaults to root/mysecretpassword (to use during website installation).

When you're done testing, hit `Ctrl-C` to stop the docker containers. You can turn them all off with:
```
docker-compose down
```

Hopefully the WordPress core team will soon make the need for this container obsolete! https://wordpress.org/support/upgrade-php/