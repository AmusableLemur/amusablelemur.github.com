---
date: "2017-05-01"
title: My blog setup
type: post
---
I am trying to get back into blogging. Mostly as a way of documenting my
side-projects which I am otherwise awful at. Previously this has been a writing
exercise for me (and still is) but I hope to switch focus to more code and small
projects.

The blog is powered by Hugo, a static site generator which basically converts
text files to this site. Those text files could be hosted on GitHub as it
was before were it was set up according to the official Hugo guide. That setup
used a continuous deployment tool (Wercker) to automatically regenerate and
re-upload my site whenever there was a content change.

This new setup instead uses gogs to host the repository and trigger a webhook
which runs a small script to build and upload the site. The webhook listener is
available in the repository on Raspbian with `apt install webhook`.

It can be configured to do what I want by creating a small file at `/etc/webhook.conf` with the following:

    [{
        "id": "blog",
        "execute-command": "/var/hooks/blog/deploy.sh",
        "command-working-directory": "/var/hooks/blog",
        "pass-arguments-to-command": [{
                "source": "payload",
                "name": "head_commit.id"
            },
            {
                "source": "payload",
                "name": "pusher.name"
            },
            {
                "source": "payload",
                "name": "pusher.email"
            }
        ],
        "trigger-rule": {
            "match": {
                "type": "payload-hash-sha256",
                "secret": "mysecret",
                "parameter": {
                    "source": "header",
                    "name": "X-Gogs-Signature"
                }
            }
        }
    }]

This listens for incoming notifications from gogs. There is also a password
(*mysecret* in the example above) set to safeguard against abuse. Whenever a
commit is uploaded to gogs it triggers a notification to the listener which in
turn triggers a small shell script that performs all the real work.

    #!/usr/bin/env bash

    # Update workspace
    rm -rf workspace
    git clone https://git.destruktiv.se/rasmus/Blog.git workspace
    cd workspace

    # Generate blog
    hugo --uglyUrls

    # Clear old content
    ssh -i ../deploy.key -l rasmus rasmuslarsson.se rm -rf /var/www/html/*

    # Upload new
    scp -i ../deploy.key -r public/* rasmus@rasmuslarsson.se:/var/www/html

This requires that a deployment key is generated with `ssh-keygen -f deploy.key`
and the public part is added to the remote host. The remote command to clear old
content can be removed to avoid the brief downtime when deploying with the
downside that old files might accumulate.
