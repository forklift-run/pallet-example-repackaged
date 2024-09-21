# pallet-example-repackaged
A simple "hello-world" Forklift pallet illustrating use of packages from repositories constructed
as layered pallets.

## Introduction

pallet-example-repackaged is a [Forklift](https://github.com/PlanktoScope/forklift) pallet which
deploys packages provided by
[github.com/forklift-run/pallet-example-layering](https://github.com/forklift-run/pallet-example-layered)
as a repository.
Specifically, this pallet adds a simple demo app.

## Usage

### Prerequisites

You will need to have the Docker Engine installed on your computer. Installation instructions are
available [here](https://docs.docker.com/engine/install/).

Then, you will need to set up the [`forklift`](https://github.com/PlanktoScope/forklift) tool on
your computer. Setup instructions are available
[here](https://github.com/PlanktoScope/forklift?tab=readme-ov-file#downloadinstall-forklift). Note
that currently `forklift` is only tested for Linux computers.

### Deployment

You can clone the latest commit of this Forklift pallet to your computer, by
using the `forklift` tool:
```
forklift plt clone github.com/forklift-run/pallet-example-repackaged@main
```

Then you can apply the cloned pallet on your computer using the following sequence of `forklift`
CLI commands:
```
sudo -E forklift plt apply
```

Warning: this will replace all Docker containers on your Docker host with the package deployments
specified by this pallet and delete any Docker containers not specified by this pallet's package
deployments.

If your user is in the `docker` group (so that you don't need to use `sudo` when running `docker`
commands), then you can just run a single command instead of the two commands listed above:

```
forklift plt switch github.com/forklift-run/pallet-example-repackaged@main
```

This pallet will bring up a web server at port 80.
- If you open <http://localhost/hello> in your web browser after deploying the pallet, you should
  see a very minimal page with an ASCII-art whale. This is because this pallet deploys the
  `simple-demo` package defined by github.com/forklift-run/pallet-example-layered as an import of
  package declaration files from github.com/forklift-run/pallet-example-minimal, but with a file
  override to customize the package (in this case by declarating a different container image to be
  deployed by the package).
- If you open <http://localhost/whoami>, you should see a blank page - this is because this pallet
  imports the `simple-demo` package deployment from github.com/forklift-run/pallet-example-layered
  which overrides the configuration from github.com/forklift-run/pallet-example-minimal to remove
  the `/whoami` route.

### Forking

To make your own copy of this repository for experimentation, you should fork this repository to a
new repository. Then, update the `path` fields of the `forklift-pallet.yml` and
`forklift-repository.yml` files to match the path of your new repository.

## Licensing

Forklift packages deployed by this pallet have their own software licenses, as specified in the
definitions of those packages. Any source code provided with this Forklift pallet is covered by the
following information, except where otherwise indicated:

Copyright Ethan Li and Forklift project contributors

SPDX-License-Identifier: Apache-2.0 OR BlueOak-1.0.0

You can use the source code provided here either under the
[Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0)
or under the [Blue Oak Model License 1.0.0](https://blueoakcouncil.org/license/1.0.0);
you get to decide. We are making the software available under the Apache license because it's
[OSI-approved](https://writing.kemitchell.com/2019/05/05/Rely-on-OSI.html),
but we like the Blue Oak Model License more because it's easier to read and understand.
