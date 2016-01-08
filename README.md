# Tracklog

**Tracklog** is a web application for managing GPX track files written in Go.

<a href="https://raw.githubusercontent.com/thcyron/tracklog/master/doc/logs.jpg"><img src="doc/logs-thumbnail.jpg" width="300"></a>
<a href="https://raw.githubusercontent.com/thcyron/tracklog/master/doc/log.jpg"><img src="doc/log-thumbnail.jpg" width="300"></a>

## Run Tracklog with Docker

There’s a Docker image [thcyron/tracklog](https://hub.docker.com/r/thcyron/tracklog)
for Tracklog. This image only contains the server and import binary, you have to
bring your own Postgres server. You also have to provide a config file.

    docker run -v /path/to/config.json:/etc/tracklog.json -p 8080:8080 thcyron/tracklog

## Installation

First, make sure you have Go and Node.js installed.

To build the JavaScript and CSS assets, run:

    npm install
    npm run build

Now, build the command line programs:

    (cd cmd/server && go build)
    (cd cmd/import && go build)

Create and initialize a new Postgres database, which will also create a new user
with both username and password set to *admin*:

    createdb tracklog
    psql tracklog < db/postgres.sql

Start the server and point your browser to http://localhost:8080/:

    cmd/server/server -config config.json

You can batch-import your GPX files with:

    cmd/import/import -config config.json -user admin /path/to/your/*.gpx

## License

Tracklog is licensed under the MIT license.
