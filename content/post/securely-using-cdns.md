---
date: "2019-10-27"
title: How to rely on third-party CDNs in a secure way
type: post
---
Instead of using dependency managers and packaging tools like Webpack or Bower (or even NPM) for web resources it is tempting to instead just link directly to the resources you need.

But except for avoiding complexity and having to learn something new like dependency management or semantical versioning schemes this also opens up some attack vectors.

For example, if the third-party you are loading your resources from is compromised an attacker might replace your Bootstrap plugin with a key listener to steal your users passwords. If the domain name is hi-jacked the JavaScript library you depend on can suddenly be used to mine Bitcoin using your visitors computers.

Luckily this is easily preventable with modern web standards. If we want to include Bootstrap using a third-party CDN like Bootstrap CDN it will provide two options to choose from. One is a direct link to the resource, e.g. `https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css` to be embedded as we see fit and the other is an HTML snippet which looks something like the following.

    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

There are two additional parameters here which are normally not taught when learning HTML and CSS. These are `integrity` and `crossorigin`.

Integrity provides a hash of the content (ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T) and describes the hash algorithm used (sha384). This allows the browser to check that the content loaded from the stackpath.bootstrapcdn.com has not been modified in any way. This protects your visitors from side-loaded malicious scripts by a compromised third-party provider, also known as [cross-site scripting (XSS)](https://en.wikipedia.org/wiki/Cross-site_scripting).

The second parameter is related to cross-origin resource sharing (CORS) which is a complicated (but important!) security subject. [Mozilla has an excellent article on how it works though](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). With this enabled the website tells the browser to perform a CORS check on the resource. This mainly provides a way to prevent [cross-site request forgery (CSRF)](https://en.wikipedia.org/wiki/Cross-site_request_forgery).

The great thing about this is that there is almost no down-sides. The performance requirements on the browser is negligible. Using [semver](https://semver.org/) for automatic version updates does not work either but this is, according to some, a feature.
