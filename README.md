# ISLE 8 - CrayFits image

Designed to used with:

* The `harvardlts/fitsservlet_container` container and docker-compose service
* The Drupal 8 site

Based on:

* [isle-crayfish-base](https://github.com/Islandora-Devops/isle-crayfish-base)

Contains and includes:

* [Composer](https://getcomposer.org/)
* [Crayfits](https://github.com/roblib/CrayFits)

## Running

To run the container, you'll need to bind mount one thing:

* A `php.ini` file with output buffering enabled at `/usr/local/etc/php/php.ini`

* docker run -d -p 8000:8000 -e FITS_WEBSERVICE_URI=http://localhost:8080/fits/examine -v /path/to/php.ini:/usr/local/etc/php/php.ini isle-crayfits

## Testing

To test Crayfits, you can issue a curl command against it to verify its endpoint is working.  For example, to run FITS on the Islandora logo:

* curl -H "Authorization: Bearer islandora" -H "Apix-Ldp-Resource: https://islandora.ca/sites/default/files/Islandora.png" idcp.localhost:8000
