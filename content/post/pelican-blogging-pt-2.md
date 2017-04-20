---
date: "2014-09-21"
title: How I set up Pelican for blogging pt. 2
type: post
---

So the whole point of running a static website (besides that it's cool) is the performance aspect. And I personally think that if you're doing something for performance you might as well go all the way. So here's how I optimized my static website.

First downloading the plugins and themes I would require to the folder for my configuration files.  

    git clone https://github.com/getpelican/pelican-plugins ~/Projects/Pelican/plugins
    git clone https://github.com/getpelican/pelican-themes ~/Projects/Pelican/themes

And then adding them to the main configuration file by adding these lines to the bottom.

    # Plugins
    PLUGIN_PATHS = ['/home/rasmus/Projects/Pelican/plugins']
    PLUGINS = ['assets', 'gzip_cache']

    # Theme
    THEME = '/home/rasmus/Projects/Pelican/themes/monospace'

I picked "monospace" for the theme since it was fairly lightweight and only required one small CSS-file, normally I would write a theme myself but for now I just wanted everything up and running. The two plugins added in the configuration are for asset management (assets) and for generating a static compressed version of the website (gzip).

The assets plugin requires additional dependencies for Python which I had to install through pip `sudo pip install webassets cssmin`. To get the asset management working properly I had to do some modifications to the theme source code. By changing the CSS links to this (below) in the theme and also removing the @import in the CSS file I am able to minimize both CSS files into the same stylesheet and send both over the same request, minimizing requests to the server.

    {% assets filters="cssmin", output="css/style.min.css", "css/main.css", "css/pygment.css" %}
    {% endassets %}

My Apache-server automatically started serving the gzip compressed files, so I didn't have to add anything else for the compression to work. Normally I would have to configure Apache to compress the files as they are being requested, but by having the files compressed beforehand allows for some additional milliseconds to be scaled of the wait time from the server.

And then to cheat a little bit I set up static caching with expires headers and disabled ETags. This means that the website will first be downloaded once in 10-20 milliseconds depending on network connection speeds, but after that all resources will be loaded from the local cache and I can reduce the rendering time to 3 milliseconds. I do this by first setting up modules with `a2enmod headers expires` and then adding this to the vhost directive (I have .htaccess disabled for even better performance).

    Header unset ETag
    FileETag None
    ExpiresActive On
    ExpiresDefault A300
    ExpiresByType text/css A526000
    ExpiresByType image/gif A526000
    ExpiresByType image/png A526000
    ExpiresByType image/jpeg A526000

All in all the site is rather fast now, I'll keep this blog posted if I discover anything else to improve.
