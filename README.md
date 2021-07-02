# Gallery generator for Nextcloud
  Nextcloud (at least up to version 21) seems to lack a way to generate a public/shared gallery based on tags.
  I could not find an app which does it.
  This simple script collects images from DB based on Nextcloud tag identifier and creates a static html gallery with these images.

# Requirements

* Full access to your Nextcloud instance. Script is very invasive at the moment and takes files from local storage.
* MySQL. Other Nextcloud databases weren't tested, but it should be possible to adapt queries.
* Nextcloud 21 (at least it was tested on this version).
* Imagemagic to convert images into thumbnails.
* Access to HTTP server to serve generated files.
* Known tag identifier. If you are still here, you probably can figure out how to get tag ID from your database.

# Quick start

For a quick start 

1. Generate your gallery
```
./generate-gallery nextcloud /path/to/your/nextcloud/files/data/USERNAME 123 /var/www/your-assome-gallery
```

The first argument `nextcloud` is MySQL database which is used by Nextcloud installation.
The script finds path to images in this database. Username and passwords are not yet supported by this script.

The second argument `/path/to/your/nextcloud/files/data/USERNAME` is prefix path to files of your user.
Database contains relative paths, so this prefix is necessary to construct a full path to an image.

The third argument is tag identifier. You can find all tags in `oc_systemtag` table.

The last argument is where the gallery will be created.

2. Point your HTTP server to `/var/www/your-assome-gallery`.

## Example of generated gallery

You can check [generated gallery from Nextcloud](https://ifnull.org/gallery/public/).

## More options

With `./generate-gallery --limit 2  nextcloud ....` you can limit number of images in your callery to small number.
This is useful for testing of end-to-end workflow before running it on all images.

By default original images are not copied to the gallery, only smaller thumbnails of two sizes. If you want to allow
viewers to download original images you can add `--originals` flag.

# Possible improvements

* Escaping of MySQL querries,...
* Support of user/password for MySQL.
* Support all next cloud DB engines.
* Support more customizations (image sizes, copy original or not,....).
* Add image id to thumbnail file name in order to find an original image in Nextcloud installation.
* Create a proper Nextcloud gallery app.
