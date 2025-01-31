
# Docker Images for Testing

This directory contains a number of docker images to assist testing the
[gRPC PECL extension](http://pecl.php.net/package/grpc) against various
different PHP environments.


## Build and Run Tests
```sh
$ cd grpc
```

To build all docker images:
```sh
$ ./src/php/bin/build_all_docker_images.sh
```

Or to only build some selected images
```sh
$ ./src/php/bin/build_all_docker_images.sh grpc-ext php-src
```

Or to only print out individual `docker build` commands
```sh
$ ./src/php/bin/build_all_docker_images.sh --cmds
```

To run all tests:
```sh
$ ./src/php/bin/run_all_docker_images.sh
```

Or to only run some selected images
```sh
$ ./src/php/bin/run_all_docker_images.sh grpc-ext php-src
```

Or to only print out individual `docker run` commands
```sh
$ ./src/php/bin/run_all_docker_images.sh --cmds
```


## `grpc-ext`

This image builds the full `grpc` PECL extension (effectively the current
release candidate), installs it against the current PHP version, and runs the
unit tests.


## `grpc-src`

This image builds the `grpc` PECL extension in a 'thin' way, only containing
the gRPC extension source files. The gRPC C Core library is expected to be
installed separately and dynamically linked. The extension is installed
against the current PHP version.

This also allows us to compile our `grpc` extension with some additional
configure options, like `--enable-tests`, which allows some additional unit
tests to be run.


## `alpine`

This image builds the `grpc` extension against the current PHP version in an
Alpine-Linux base image.


## `php-src`

Instead of using a general purpose base docker image provided by PHP, here we
compile PHP itself from
[source](https://github.com/php/php-src). This will allow us to change some
`configure` options, like `--enable-debug`. Then we proceed to build the full
`grpc` PECL extension and run the unit tests.


## `php-zts`

This image builds the `grpc` extension against the current PHP version with ZTS
enabled.


## `php-future`

This image builds the `grpc` extension against the next future PHP version
currently in alpha, beta or release candidate stage.


## `php5`

This image builds the `grpc` extension against a PHP 5 base image with ZTS
enabled.

NOTE: PHP 5.x has reached the end-of-life state and is no longer supported.


## `fork-support`

This image tests `pcntl_fork()` support and makes sure scripts using
`pcntl_fork()` don't hang or crash.
