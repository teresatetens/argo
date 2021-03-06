# argo

![argo](https://upload.wikimedia.org/wikipedia/en/f/f4/Argo_submersible.jpg)

get lots more places from the Google Maps places API

## setup

install project dependencies with:

`npm install`

You'll also need a Google Maps API key. [Instructions to get one can be found here.](https://developers.google.com/maps/documentation/javascript/get-api-key).

## running the script

this script is written to run for resturaunts, but could run for any place types that Google lets you search for.

Create a `config.json` in the root of this folder, copied from the config.example.json (also in the project root).

Provide the Google Maps API key, [the place type](https://developers.google.com/places/supported_types), the radius you want to search in (the default from the example is a good radius), and the latitude and longitude of the grid you want to get restauraunts for.

The lat / long of the grid will be in the format of `[35.0, 35.18]`, where the lower number comes first. Negatives apply for southern hemisphere latitue and for western longitude (the equator and the prime merdian being zero, respectively).

The example coordinates are for a square that roughly covers Chattanooga, TN.

## why? this seems strange

Google limits you to 60 responses per api call, so you can't just get back all of the places of a given place type in a large search area (of a circle with a radius of 10km, say).

You can, however, search with a small enough search area that you can get back all of the results for that smaller circle.

This repo operates by using a small enough search area (a small circle with a radius of 2km), and doing many searches over the larger search area. Instead of doing one search for a in a 10km radius circle, we do 100 smaller searches in a 10km x 10km square with overlapping search area. That way, we get all of the places in the square. Sort of like this figure, but less optimized.

![figure 1](https://www2.stetson.edu/~efriedma/circovsqu/11.gif)

Sort of like how they found the Titanic, we sweep back and forth along the entire area to find all the things we're looking for.

![searching for the titanic](http://infotitanic.tripod.com/images/gallery/g_ballard1.JPG)
