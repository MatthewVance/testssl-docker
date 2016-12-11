# Supported tags and respective `Dockerfile` links

- [`2.8rc3`, `latest` (*2.8rc3/Dockerfile*)](https://github.com/MatthewVance/testssl-docker/tree/master/2.8rc3)
- [`2.6`, (*2.6/Dockerfile*)](https://github.com/MatthewVance/testssl-docker/tree/master/2.6)

## What is testssl.sh?

 testssl.sh is a free command line tool which checks a server's service on any port for the support of TLS/SSL ciphers, protocols as well as recent cryptographic flaws and more.

> [testssl.sh](https://testssl.sh/)

## How to use this image

### Standard usage

Run your testssl container with the following command to run testssl.sh, replacing `<options>` with supported testssl.sh flags:

```console
$ docker run -t --rm mvance/testssl:2.8rc3 <options>
```

For example, running `$ docker run -t --rm matthewvance/testssl:2.8rc3 --protocols 127.0.0.1` would check TLS/SSL protocols against localhost, assuming an https service is running on localhost.

### Interactive shell

Run your testssl container with the following command to obtain an interactive bash shell.

```console
$ docker run -i --entrypoint /bin/bash -t --rm mvance/testssl:2.8rc3
```

Within the container's shell, you can then run testssl.sh as if it was any other program installed in your `$PATH`.

### View help

Run your testssl container with the following command to access the help file for testssl.sh.

```console
$ docker run -t --rm mvance/testssl:2.8rc3
```

For more information on using testssl.sh, visit [https://testssl.sh/](https://testssl.sh/).

# Supported Docker versions

This image is tested on Docker version 1.8.2.

Use on older versions at your own risk.

# User feedback

## Documentation

Documentation for this image is stored right here in the [`README.md`](https://github.com/MatthewVance/testssl-docker/blob/master/README.md).

Documentation for testssl.sh is available on the [project's website](https://testssl.sh/).

## Issues

If you have any problems with or questions about this image, please contact me through a [GitHub issue](https://github.com/MatthewVance/testssl-docker/issues).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small. I imagine the upstream projects would be equally pleased to receive your contributions.

Please familiarize yourself with the [repository's `README.md` file](https://github.com/MatthewVance/testssl-docker/blob/master/README.md) before attempting a pull request.

Before you start to code, I recommend discussing your plans through a [GitHub issue](https://github.com/MatthewVance/testssl-docker/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.

## Acknowledgments

- [Peter Mosmans OpenSSL fork](https://github.com/PeterMosmans/openssl/)
- [testssl.sh](https://github.com/drwetter/testssl.sh)

## Licenses
### License

Unless otherwise specified, all code is released under the MIT License (MIT). See the [repository's `LICENSE` file](https://github.com/MatthewVance/testssl-docker/blob/master/LICENSE) for details.

### Licenses for other components

- Peter Mosmans OpenSSL fork: [OpenSSL License](https://github.com/PeterMosmans/openssl/blob/1.0.2-chacha/LICENSE) and [Original SSLeay License](https://github.com/PeterMosmans/openssl/blob/1.0.2-chacha/LICENSE)
- testssl.sh: [GPLv2](https://github.com/drwetter/testssl.sh/blob/master/LICENSE)
