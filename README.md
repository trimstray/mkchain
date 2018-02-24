# sslmerge

## Releases

|            **STABLE RELEASE**            |           **TESTING RELEASE**            |
| :--------------------------------------: | :--------------------------------------: |
| [![](https://img.shields.io/badge/Branch-master-green.svg)]() | [![](https://img.shields.io/badge/Branch-testing-orange.svg)]() |
| [![](https://img.shields.io/badge/Version-v1.3.0-lightgrey.svg)]() | [![](https://img.shields.io/badge/Version-v1.3.0-lightgrey.svg)]() |
| [![Build Status](https://travis-ci.org/trimstray/sslmerge.svg?branch=master)](https://travis-ci.org/trimstray/sslmergel) | [![Build Status](https://travis-ci.org/trimstray/sslmerge.svg?branch=testing)](https://travis-ci.org/trimstray/sslmerge) |

## Description

Is an open source tool to help you build a valid SSL certificate chain.

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

Let's start with **ssllabs** certificate chain. First of all get chain structure with **openssl** command:

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

  issued for **ssllabs.com** by **Entrust Certification Authority - L1K**

- **Intermediate Certificate**

  issued for **Entrust Certification Authority - L1K** by **Entrust Root Certification Authority - G2**

- **Intermediate Certificate**

  issued for **Entrust Root Certification Authority - G2** by **Entrust Root Certification Authority**

- **Root Certificate** (Self-Signed Certificate)

  issued for **Entrust Root Certification Authority** by **Entrust Root Certification Authority**

Then an example of starting the tool:

``````
ls example/ssllabs.com
Intermediate1.crt  Intermediate2.crt  RootCertificate.crt  ServerCertificate.crt

sslmerge -i example/ssllabs.com -o /tmp/bundle_chain_ssllabs_certs.crt

  	           (ServerCertificate.crt)
  	           (Identity Certificate)
  S:(18319780):(ssllabs.com)
  I:(2835d715):(EntrustCertificationAuthority-L1K)
  	           (Intermediate1.crt)
  	           (Intermediate Certificate)
  S:(2835d715):(EntrustCertificationAuthority-L1K)
  I:(02265526):(EntrustRootCertificationAuthority-G2)
  	           (Intermediate2.crt)
  	           (Intermediate Certificate)
  S:(02265526):(EntrustRootCertificationAuthority-G2)
  I:(6b99d060):(EntrustRootCertificationAuthority)
  	           (RootCertificate.crt)
  	           (Root Certificate)
  S:(6b99d060):(EntrustRootCertificationAuthority)
  I:(6b99d060):(EntrustRootCertificationAuthority)

  Result: chain generated correctly
``````

Output from the terminal:

![sslmerge_output](doc/img/sslmerge_output.png)

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

## License

GPLv3 : <http://www.gnu.org/licenses/>

**Free software, Yeah!**
