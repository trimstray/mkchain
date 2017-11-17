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
sslmerge -i /data/certs -o /data/bundle_chain_certs.crt
``````

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