# nginx-newsite

This script creates and enables a new site based on the site's URL. Currently,
you can either create an HTML or a [Laravel](http://laravel.com/) based site.

## Requirements
- https://github.com/perusio/nginx_ensite - Another script that matches the
  a2ensite commands.
- An nginx site config template for HTML sites located at `/etc/nginx/sites-available/default.html`
- An nginx site config template for Laravel sites located at `/etc/nginx/sites-available/default.laravel`

## Using It
Place the script in your desired script location like `/usr/local/bin` or wherever
your heart desires. When running the script do not include the `www` in front of
the URL.

Below are a couple of examples of how you can use it:
```
# create a simple HTML site
$ newsite fubar.com html

# create a Laravel site
$ newsite fubar.com laravel
```

## What Happens

1. The script creates the nginx config file in `/etc/nginx/sites-available/`
from the respective site-type template (html or laravel).
2. The appropriate directories for the site are created if they do not already
exist.
    - `/srv/www/<url>/public_html` for serving the site
    - `/srv/www/<url>/logs` for site logs
3. The `nginx_ensite` script is run to enable the newly created site.
4. User is prompted to reload nginx.
5. ??
6. Profit.
