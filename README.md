sslmerge
===============

[![bash_logotype](doc/bash_logotype.png)](https://www.gnu.org/software/bash/)

__**sslmerge**__ is a GPLv3 tool to help create the correct chain of SSL certificates delivered.

  - simple to use
  - does not send the certificates to the outside (running locally)

### Version

Latest stable: **v1.1c**  
[![Build Status](https://travis-ci.org/jboowie/sslmerge.svg?branch=master)](https://travis-ci.org/jboowie/sslmerge)  
Devel branch: **next-release**  
[![Build Status](https://travis-ci.org/jboowie/sslmerge.svg?branch=next-release)](https://travis-ci.org/jboowie/sslmerge)  

### Usage

Examples of ways to use:

```
  Usage:
    sslmerge [option|long-option]

  Examples:
    sslmerge --help
    sslmerge --version
    sslmerge --cert Root.crt --cert Intermediate1.crt --cert Server.crt --output nginx_bundle.crt
    sslmerge --cert /tmp/certs/ --output /tmp/nginx_bundle.crt

  Options:
    -h, --help                  show this message
    -v, --version               show script version
    -d, --debug {0,7}           display information on the screen (debug mode)
    -a, --attach [file]         attach an external file to the script
    -c, --cert                  stores a cert single file or directory with certs
    -o, --output                saves the result (chain) to file
```

### Requirements

  - openssl package

### Todos

  - add better error handling mechanism
  - in the case of detecting different certificate .crt it must be converted to this format
  - adding a mechanism for informing the format of the certificate

### Problems

See on the *Issues* page.

### Project architecture

    |-- sslmerge               	# main file (init)
    |-- CHANGELOG.md            # notable changes for each version of a project
    |-- LICENSE.md              # GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
    |-- README.md               # this simple documentation
    |-- _config.yml             # jekyll’s configuration file
    |-- .gitignore              # ignore untracked files e.g. log/ directory
    |-- .travis.yml             # travis-ci configuration for project
    |-- src                     # includes external project files
        |-- _import_            # functions, variables and all other attached files to the script
    |-- doc                     # includes documentation, images and manuals
        |-- bash_logotype.png   # bash logo (added to README.md)

### License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**
