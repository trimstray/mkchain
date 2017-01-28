sslmerge
===================


A tool to help create the correct chain of SSL certificates delivered.

----------


Usage
-------------

```
  Usage:
    sslmerge [option|long-option]

  Examples:
    sslmerge --help
    sslmerge --debug
    sslmerge --root Root.crt --intermediate Intermediate1.crt --client Server.crt

  Options:
    -h, --help                  show this message
    -d, --debug                 display information on the screen (debug mode)
    -r, --root                  stores a self-signed certificate (root certificate)
    -i, --intermediate          stores a certificate signed by root (intermediate certificate)
    -c, --client                stores a certificate signed by intermediate (client certificate)
```
