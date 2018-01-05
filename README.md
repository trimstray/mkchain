# sslmerge

## Version

Stable release: **v1.2.0**  
Testing release: **testing**

## Description

A tool to help you build a valid SSL certificate chain.

## Parameters

Provides the following options:

```
  Usage:
    sslmerge <option|long-option>

  Examples:
    sslmerge --in Root.crt --in Intermediate1.crt --in Server.crt --out nginx_bundle.crt
    sslmerge --in /tmp/certs/ --out /tmp/nginx_bundle.crt

  Options:
        --help        show this message
        --debug       displays information on the screen (debug mode)
    -i, --in          add certificates to merge (multiple files or directory)
    -o, --out         saves the result (chain) to file
```

## Requirements

**<u>Sslmerge</u>** uses external utilities to be installed before running:

- [openssl](https://www.openssl.org/)

## Use example

Then an example of starting the tool:

``````
ls
00.crt	01.crt	03.crt
sslmerge -i /tmp/google_cert -o /tmp/bundle_chain_google_certs.crt

  	       (03.crt)
  	       (Identity Certificate)
  S:(a18bd28a):(*.google.com)
  I:(c4c7a654):(GoogleInternetAuthorityG2)
  	       (00.crt)
  	       (Intermediate Certificate)
  S:(c4c7a654):(GoogleInternetAuthorityG2)
  I:(2c543cd1):(GeoTrustGlobalCA)
  	       (01.crt)
  	       (Root Certificate)
  S:(2c543cd1):(GeoTrustGlobalCA)
  I:(2c543cd1):(GeoTrustGlobalCA)

  Result: chain generated correctly
``````

Screen from terminal:

![sslmerge_output](doc/img/sslmerge_output.png)

## Project architecture

    |-- sslmerge                # main script (init)
    |-- LICENSE.md              # GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
    |-- README.md               # this simple documentation
    |-- .gitignore              # ignore untracked files
    |-- .gitkeep                # track empty directory
    |-- src                     # includes external project files
        |-- _import_            # external variables and functions
    |-- doc                     # includes documentation, images and manuals

## License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**