Docker images to support NodeJS-based software engineering
==========================================================

[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/infrahelpers/node)](https://hub.docker.com/repository/docker/infrahelpers/node/general)

# Introduction
[That project](https://github.com/infra-helpers/docker-images-nodejs)
produces Docker images, hosted on [dedicated
public Docker Cloud site](https://hub.docker.com/repository/docker/infrahelpers/node).
Those Docker images are intended to bring Linux-based ready-to-use environment
for software engineering based on NodeJS utilities.

The only supported Linux distribution, so far is
[Ubuntu 20.04 LTS (Focal Fossal)](http://releases.ubuntu.com/20.04/),
as it is one of the most commons, and is for instance used as a base
to [Postman Newman](https://github.com/nodesource/distributions).

Every time some changes are committed on the
[project's GitHub repository](https://github.com/infra-helpers/docker-images-nodejs),
the
[Docker images are automatically rebuilt](https://hub.docker.com/repository/docker/infrahelpers/node/timeline)
and pushed onto Docker Hub/Cloud.

When some more components are needed, which may be of interest to other
software engineers, the Docker image may be amended so as to add those extra
components.
The preferred way to propose amendment of the Docker image is through
[pull requests on the GitHubproject](https://github.com/infra-helpers/docker-images-nodejs/pulls).
Once the pull request has been merged, _i.e._, once the `Dockerfile` amendment
has been [committed in GitHub](https://github.com/infra-helpers/docker-images-nodejs/commits/master),
Docker Hub/Cloud then rebuilds the corresponding container images, which become
available for every one to use.

# Images on Docker Hub/Cloud
* [Docker Cloud dashboard for Ubuntu images](https://hub.docker.com/_/ubuntu)
* [Docker Cloud dashboard for NodeJS images](https://hub.docker.com/_/node)

# Using the pre-built development images
* Start the container featuring the NodeJS-based image:
```bash
$ docker pull infrahelpers/node
$ docker run --rm -v ~/tmp/collections:/tmp/collections -it infrahelpers/node bash
[build@5..0 dev]$ 
```

* Launch Newman on some collection:
```bash
[build@5..0 dev]$ newman run /tmp/collections/some-collection.json --reporters cli,csv,json --reporter-csv-export newman/some-report.csv --reporter-json-export newman/some-report.json
```

# Customize a container image
The images may be customized, and pushed to Docker Hub/Cloud:
```bash
$ mkdir -p ~/dev/infra
$ cd ~/dev/showcase
$ git clone https://github.com/infra-helpers/docker-images-nodejs.git docker-images-nodejs
$ cd docker-images-nodejs
$ vi ubuntu2004/Dockerfile
$ docker build -t infrahelpers/node ubuntu2004/
$ docker run --rm -v ~/tmp/collections:/tmp/collections -it infrahelpers/node bash
[build@9..d]$ exit
$ docker push infrahelpers/node
```

# TODO
For any of the following features, an issue may be open
[on GitHub](https://github.com/infra-helpers/docker-images-nodejs/issues):
1. Automate regular rebuilds (_e.g._, once a month for new releases of NodeJS)

