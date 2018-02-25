# sslmerge

## Releases

|                      **STABLE RELEASE**                      |                     **TESTING RELEASE**                      |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| [![](https://img.shields.io/badge/Branch-master-green.svg)]() | [![](https://img.shields.io/badge/Branch-testing-orange.svg)]() |
| [![](https://img.shields.io/badge/Version-v1.4.0-lightgrey.svg)]() | [![](https://img.shields.io/badge/Version-v1.4.0-lightgrey.svg)]() |
| [![Build Status](https://travis-ci.org/trimstray/sslmerge.svg?branch=master)](https://travis-ci.org/trimstray/sslmerge) | [![Build Status](https://travis-ci.org/trimstray/sslmerge.svg?branch=testing)](https://travis-ci.org/trimstray/sslmerge) |

## Description

Is an open source tool to help you build a valid SSL certificate chain from the root certificate to the end-user certificate. Also can help you fix the incomplete certificate chain and download all missing CA certificates.

## Parameters

Provides the following options:

```
  Usage:
    sslmerge <option|long-option>

  Examples:
    sslmerge --in Root.crt --in Intermediate1.crt --in Server.crt --out bundle_chain_certs.crt
    sslmerge --in /tmp/certs/ --out bundle_chain_certs.crt --with-root
    sslmerge -i Server.crt -o bundle_chain_certs.crt

  Options:
        --help        show this message
        --debug       displays information on the screen (debug mode)
    -i, --in          add certificates to merge (multiple files or directory)
    -o, --out         saves the result (chain) to file
        --with-root   add root certificate to the certificate chain
```

## Requirements

**<u>sslmerge</u>** uses external utilities to be installed before running:

- [openssl](https://www.openssl.org/)

## Install/uninstall

It's simple - for install:

```
./setup.sh install
```

For remove:

```
./setup.sh uninstall
```

> - symlink to `bin/sslmerge` is placed in `/usr/local/bin`
> - man page is placed in `/usr/local/man/man8`

## Use example

Let's start with **ssllabs** certificate chain. They are delivered together with the **sslmerge** and can be found in the `example/ssllabs.com` directory which additionally contains the `all` directory (containing all the certificates needed to assemble the chain) and the `server_certificate` directory (containing only the server certificate).

The correct chain for the ssllabs.com domain (the result of the **openssl** command):

```bash
Certificate chain
 0 s:/C=US/ST=California/L=Redwood City/O=Qualys, Inc./CN=ssllabs.com
   i:/C=US/O=Entrust, Inc./OU=See www.entrust.net/legal-terms/OU=(c) 2012 Entrust, Inc. - for authorized use only/CN=Entrust Certification Authority - L1K
 1 s:/C=US/O=Entrust, Inc./OU=See www.entrust.net/legal-terms/OU=(c) 2012 Entrust, Inc. - for authorized use only/CN=Entrust Certification Authority - L1K
   i:/C=US/O=Entrust, Inc./OU=See www.entrust.net/legal-terms/OU=(c) 2009 Entrust, Inc. - for authorized use only/CN=Entrust Root Certification Authority - G2
 2 s:/C=US/O=Entrust, Inc./OU=See www.entrust.net/legal-terms/OU=(c) 2009 Entrust, Inc. - for authorized use only/CN=Entrust Root Certification Authority - G2
   i:/C=US/O=Entrust, Inc./OU=www.entrust.net/CPS is incorporated by reference/OU=(c) 2006 Entrust, Inc./CN=Entrust Root Certification Authority
```

The above code presents a full chain consisting of:

- **Identity Certificate** (Server Certificate)

  issued for *ssllabs.com* by *Entrust Certification Authority - L1K*

- **Intermediate Certificate**

  issued for *Entrust Certification Authority - L1K* by *Entrust Root Certification Authority - G2*

- **Intermediate Certificate**

  issued for *Entrust Root Certification Authority - G2* by *Entrust Root Certification Authority*

- **Root Certificate** (Self-Signed Certificate)

  issued for *Entrust Root Certification Authority* by *Entrust Root Certification Authority*

### Scenario 1

In this scenario, we will chain all delivered certificates. Example of running the tool:

![sslmerge_output](doc/img/sslmerge_output_1.png)

### Scenario 2

In this scenario, we only use the server certificate and use it to retrieve the remaining required certificates. Then, as above, we will combine all the provided certificates. Example of running the tool:

![sslmerge_output](doc/img/sslmerge_output_2.png)

## Certificate chain

In order to create a valid chain, you must provide the tool with all the necessary certificates. It will be:

- **Server Certificate**
- **Intermediate CAs** and **Root CAs**

This is very important because without it you will not be able to determine the beginning and end of the chain.

However, if you look inside the generated chain after generating with **sslmerge**, you will not find the root certificate there. Why?

Because self-signed root certificates need not/should not be included in web server configuration. They serve no purpose (clients will always ignore them) and they incur a slight performance (latency) penalty because they increase the size of the SSL handshake.

If you want to add a root certificate to the certificate chain, call the utility with the `--with-root` parameter.

## Certification Paths

**Sslmerge** allows the use of two **Certification Paths**:

![sslmerge_output](doc/img/ssllabs_output_1.png)

## Logging

After running the script, the `log/` directory is created and in it the following files with logs:

- `<script_name>.<date>.log` - all `_logger()` function calls are saved in it
- `stdout.log` - a standard output and errors from the `_init_cmd()` function are written in it. If you want to redirect the output from command, use the following structure: `your_command >>"$_log_stdout" 2>&1 &`

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Project architecture

    |-- LICENSE.md                 # GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
    |-- README.md                  # this simple documentation
    |-- CONTRIBUTING.md            # principles of project support
    |-- .gitignore                 # ignore untracked files
    |-- .travis.yml                # continuous integration with Travis CI
    |-- setup.sh                   # install sslmerge on the system
    |-- bin
        |-- sslmerge               # main script (init)
    |-- doc                        # includes documentation, images and manuals
        |-- man8
            |-- sslmerge.8         # man page for sslmergel
    |-- lib                        # libraries, external functions
    |-- log                        # contains logs, created after init
    |-- src                        # includes external project files
        |-- helpers                # contains core functions
        |-- import                 # appends the contents of the lib directory
        |-- __init__               # contains the __main__ function
        |-- settings               # contains sslmergel settings
    |-- example                    # examples of certs needed to build a chain
        |-- github.com
        |-- google.com
        |-- mozilla.com
        |-- ssllabs.com
        |-- vultr.com

## License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**
