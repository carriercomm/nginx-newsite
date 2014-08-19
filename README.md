# nginx-newsite

This script creates and enables a new site based on the site's URL. Currently,
you can either create an HTML, PHP, or a [Laravel](http://laravel.com/) based site.

It also has a corresponding `removesite` script that will essentially reverse
everything that happens in the `newsite` script.

## Requirements
- https://github.com/perusio/nginx_ensite - Another script that matches the
  a2ensite commands.
- An nginx site config template for HTML sites located at `/etc/nginx/sites-available/default.html`
*See templates directory*
- An nginx site config template for PHP sites located at `/etc/nginx/sites-available/default.php`
*See templates directory*
- An nginx site config template for Laravel sites located at `/etc/nginx/sites-available/default.laravel`
*See templates directory*

## Using It
Place the script(s) in your desired script location like `/usr/local/bin` or wherever
your heart desires. When running the script DO NOT include the `www` in front of
the URL, but subdomains are perfectly acceptable.

Script breakdowns:
```
$ newsite <url> [site-type]

$ removesite <url>
```

Below are a couple of examples of how you can use it:
```
# create a simple HTML site
$ newsite fubar.com html

# create a PHP site
$ newsite fubar.com PHP

# create a Laravel site
$ newsite fubar.com laravel

# remove a site
$ removesite fubar.com
```

## What Happens

### newsite

1. The script prompts you if the URL should include a `www.` prefix to the
passed in url. Answering yes adds both the URL submitted and the www.<url> to the
config.
2. The script creates the nginx config file in `/etc/nginx/sites-available/`
from the respective site-type template.
3. The appropriate directories for the site are created if they do not already
exist.
    - `/srv/www/<url>/public_html` for serving the site
    - `/srv/www/<url>/logs` for site logs
4. The `nginx_ensite` script is run to enable the newly created site.
5. User is prompted to reload nginx.
6. ??
7. Profit.

### removesite

1. The script disables the nginx site and if it was active, prompts you to
reload nginx.
2. You are prompted to remove the site's directories and config file if they
exist.
3. ??
4. Profit.
