# ISLE 8 - Houdini image

Designed to used with:

* The `harvardlts/fitsservlet_container` container and docker-compose service
* The Drupal 8 site

Based on:

* Official PHP Apache image: [php:7.4.3-apache](https://hub.docker.com/layers/php/library/php/7.4.3-apache/images/sha256-48dde1707d7dca2b701aa230344c58cb8ec5b0ce8e9dbceced65bec5ccd7d1d0?context=explore)

Contains and includes:

* [Composer](https://getcomposer.org/)
* [Crayfits](https://github.com/roblib/CrayFits)

## MVP 2 sprint

### Building

There is one build argument that you must provide in order to build this container:

* FITS_WEBSERVICE_URI - URI pointing to your `fitsservlet_container` instance

In order to build, run this command

* `docker build -t isle-crayfits --build-arg FITS_WEBSERVICE_URI=http://localhost:8080/fits/examine .`

Or if you've defined the build args as environment variables already, simply

* `docker build -t isle-houdini --build-arg FITS_WEBSERVICE_URI .`

### Running

To run the container, you'll need to bind mount one thing:

* A `php.ini` file with output buffering enabled at `/usr/local/etc/php/php.ini`

* docker run -d -p 8000:8000 -v /path/to/php.ini:/usr/local/etc/php/php.ini isle-crayfits

### Testing

To test Crayfits, you can issue a curl command against it to verify its endpoint is working.  For example, to run FITS on the Islandora logo:

* curl -H "Authorization: Bearer islandora" -H "Apix-Ldp-Resource: https://islandora.ca/sites/default/files/Islandora.png" idcp.localhost:8000
