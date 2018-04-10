# Concourse Kickstarter

This repository lets you try out [Concourse CI](https://concourse-ci.org) in a controlled environment, experiment with its setup and pipeline configuration.

## Prerequisites

- [Docker](https://www.docker.com) >= 18.03.0-ce
- [Docker Compose](https://github.com/docker/compose/) >= 1.20.1
- [fly](https://concourse.ci/fly-cli.html) >= 3.10.0

### Installing fly

Fly is the command line interface for Concourse. You can install it either by [downloading the binary from the release page](https://github.com/concourse/concourse/releases) (mind the version!), or downloading it from the dashboard once the application is running.

## Runnning Concourse

```sh
$ ./run start
```

Concourse should now be available at [`http://localhost:8080/`](http://localhost:8080).

### Provisioning the "Hello World" example

There is a "Hello World" example in `hello_world.yml` which you can provision using the `fly` CLI:

```sh
$ fly -t test login -c http://localhost:8080
```

_Note: For this example I've deactivated the internal authentication. Usually this would be the step where you specify a username and password. You can enable this behaviour by removing the variable `CONCOURSE_NO_REALLY_I_DONT_WANT_ANY_AUTH` from the `docker-compose.yml` while adding `CONCOURSE_BASIC_AUTH_USERNAME` and `CONCOURSE_BASIC_AUTH_PASSWORD`._

Then run

```sh
$ fly -t test set-pipeline -p hello_world -c hello_world.yml
```

You should now have a paused pipeline you can trigger using the "+" at the top right after having unpaused it. You can also unpause and trigger the pipeline using the `fly` CLI.
