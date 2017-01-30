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
    sslmerge --cert Root.crt --cert Intermediate1.crt --cert Server.crt
    sslmerge --cert root.crt --cert intermediate01.crt --cert intermediate02.crt --cert server.crt
    sslmerge -c root.crt -c intermediate01.crt -c intermediate02.crt -c server.crt -o bundle.crt

  Options:
    -h, --help                  show this message
    -d, --debug                 display information on the screen (debug mode)
    -c, --cert                  stores a certificate (ex. root certificate, intermediate certificate and other)
    -o, --output                saves the result (chain) to file
```
