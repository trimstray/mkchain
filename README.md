sslmerge
----

[![bash_logotype_new_2.png](https://s29.postimg.org/lgglyiqif/bash_logotype_new_2.png)](https://www.gnu.org/software/bash/)

![N|Solid](https://img.shields.io/badge/version-1.1b-brightgreen.svg) [![N|Solid](https://img.shields.io/badge/license-GPLv3-lightgrey.svg)](https://www.gnu.org/licenses/gpl-3.0.en.html)

**sslmerge** is a tool to help create the correct chain of SSL certificates delivered.

  - simple to use
  - does not send the certificates to the outside (running locally)
  - allows for quick modification of code (bash)

### Usage

Examples of ways to use:

```
  Usage:
    sslmerge [option|long-option]

  Examples:
    sslmerge --help
    sslmerge --cert Root.crt --cert Intermediate1.crt --cert Server.crt
    sslmerge --debug --cert 01.crt --cert XX.crt --output nginx_bundle.crt
    sslmerge --dir /tmp/certs --output chain.crt

  Options:
    -h, --help                  show this message
    -v, --version               show script version
    -d, --debug                 display information on the screen (debug mode)
    -c, --cert                  stores a certificate (ex. root certificate, intermediate certificate and other)
    -o, --output                saves the result (chain) to file
```

### Requirements

  - openssl package

### Todos

 - add error handling mechanism
 - set the directory with certificates

### Problems

In versions 1.x does not detect correctly all certificates. There were also problems with the removal of the new line between the end of one certificate and the start of the second of the output file.

### License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**