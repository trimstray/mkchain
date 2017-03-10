sslmerge
----

[![bash_logotype_new_2.png](https://s29.postimg.org/lgglyiqif/bash_logotype_new_2.png)](https://www.gnu.org/software/bash/)

[**sslmerge**](https://jboowie.github.io/sslmerge) is a tool to help create the correct chain of SSL certificates delivered.

  - simple to use
  - does not send the certificates to the outside (running locally)

### Version

Latest stable: **v1.1c**  
Devel branch: **next-release**

### Usage

Examples of ways to use:

```
  Usage:
    sslmerge [option|long-option]

  Examples:
    sslmerge --help
    sslmerge --version
    sslmerge --cert Root.crt --cert Intermediate1.crt --cert Server.crt
    sslmerge --cert 01.crt --cert XX.crt --output nginx_bundle.crt --debug
    sslmerge --cert /tmp/certs/ --output nginx_bundle.crt

  Options:
    -h, --help                  show this message
    -v, --version               show script version
    -d, --debug {0,7}           display information on the screen (debug mode)
    -a, --config [file]         attach an external file to the script
    -c, --cert                  stores a cert single file or directory with certs
    -o, --output                saves the result (chain) to file
```

### Requirements

  - openssl package

### Project architecture

    |--- sslmerge               # main file (init)
    |--- README.md              # this simple documentation
    |--- LICENSE.md             # GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
    |--- CHANGELOG.md           # notable changes for each version of a project
    |--- _config.yml            # jekyll’s configuration file
    |--- src                    # functions, variables and all other attached files to the script
            |--- _config        # external configuration file
            |--- _functions     # includes a set of external functions (including the user)

### Todos

  - add better error handling mechanism
  - in the case of detecting different certificate .crt it must be converted to this format
  - adding a mechanism for informing the format of the certificate

### Problems

See on the *Issues* page.

### License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**