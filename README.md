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
    -r, --root                  root certificate
    -i, --intermediate          intermediate certificate
    -c, --client                client certificate
```
