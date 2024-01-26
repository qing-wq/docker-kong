![Build Status](https://github.com/kong/docker-kong/actions/workflows/test.yml/badge.svg)

# About this Repo

This is the Git repo of the Docker
[official image](https://docs.docker.com/docker-hub/official_repos/) for
[kong](https://registry.hub.docker.com/_/kong/).
See [the Docker Hub page](https://registry.hub.docker.com/_/kong/)
for the full readme on how to use this Docker image and for information
regarding contributing and issues.

The full readme is generated over in [docker-library/docs](https://github.com/docker-library/docs),
specifically in [docker-library/docs/kong](https://github.com/docker-library/docs/tree/master/kong).

See a change merged here that doesn't show up on the Docker Hub yet?
Check [the "library/kong" manifest file in the docker-library/official-images
repo](https://github.com/docker-library/official-images/blob/master/library/kong),
especially [PRs with the "library/kong" label on that
repo](https://github.com/docker-library/official-images/labels/library%2Fkong). For more information about the official images process, see the [docker-library/official-images readme](https://github.com/docker-library/official-images/blob/master/README.md).

# For Kong developers

## Pushing a Kong patch release (x.y.Z) update

If the update does not require changes to the Dockerfiles other than
pointing to the latest Kong code, the process can be semi-automated as follows:

1. Check out this repository.

2. Run `./update.sh x.y.z`

   This will create a release branch, modify the relevant files automatically,
   give you a chance to review the changes and press "y", then
   it will push the branch and open a browser with the PR
   to this repository.

3. Peer review, run CI and merge the submitted PR.

4. Run `./submit.sh -p x.y.z`

   Once the internal PR is merged, this script will do the same
   for the [official-images](https://github.com/docker-library/official-images)
   repository. It will clone [Kong's fork](https://github.com/kong/official-images),
   create a branch, modify the relevant files automatically,
   give you a chance to review the changes and press "y", then
   it will push the branch and open a browser with the PR
   to the docker-library repository.

## Pushing a Kong minor release (x.Y.0) update

Not semi-automated yet. Note that minor releases are more likely to require more
extensive changes to the Dockerfiles.

# Release Definition

[![Screwdriver CD badge][Screwdriver CD badge]][Screwdriver CD url]
[![HashiCorp Packer badge][HashiCorp Packer badge]][HashiCorp Packer url]
[![HashiCorp Terraform badge][HashiCorp Terraform badge]][HashiCorp Terraform url]

We offer A [Screwdriver CD pipeline] that deploys an [immutable][Immutable Infrastructure] instance of
[Kong API Gateway] running in docker-kong to AWS. It uses the [Kong API gateway release definition template] to perform
the deployment and any customizations can be added to [this pipeline](./screwdriver.yaml).

[HashiCorp Packer badge]: https://img.shields.io/badge/Packer-02A8EF?style=for-the-badge&logo=Packer&logoColor=white
[HashiCorp Packer url]: https://qubitpi.github.io/hashicorp-packer/packer/docs
[HashiCorp Terraform badge]: https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white
[HashiCorp Terraform url]: https://qubitpi.github.io/hashicorp-terraform/terraform/docs

[Immutable Infrastructure]: https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure

[Kong API Gateway]: https://konghq.com/
[Kong API gateway release definition template]: https://github.com/QubitPi/kong-api-gateway-release-definition-template
[Kong manager UI]: https://qubitpi.github.io/docs.konghq.com/gateway/latest/kong-manager/

[Screwdriver CD badge]: https://img.shields.io/badge/Screwdriver%20CD-1475BB?style=for-the-badge&logo=data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pg0KPCEtLSBVcGxvYWRlZCB0bzogU1ZHIFJlcG8sIHd3dy5zdmdyZXBvLmNvbSwgR2VuZXJhdG9yOiBTVkcgUmVwbyBNaXhlciBUb29scyAtLT4NCjxzdmcgaGVpZ2h0PSI4MDBweCIgd2lkdGg9IjgwMHB4IiB2ZXJzaW9uPSIxLjEiIGlkPSJMYXllcl8xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiANCgkgdmlld0JveD0iMCAwIDUxMiA1MTIiIHhtbDpzcGFjZT0icHJlc2VydmUiPg0KPHBhdGggc3R5bGU9ImZpbGw6I2ZmZmZmZjsiIGQ9Ik01MDQuNzgzLDc3LjA5MWgtMC4wMDZIMzAzLjQ5NGMtMi4wMzYsMC0zLjk3NywwLjg1OS01LjM0NSwyLjM2Ng0KCWMtMS4zNjgsMS41MDgtMi4wMzgsMy41Mi0xLjg0Miw1LjU0OWwzLjkyNSw0MC42OTNjMC4zNDMsMy41NTIsMy4yMjgsNi4zMiw2Ljc5Miw2LjUxNmw0Mi4wNSwyLjMxNGwtODAuNzM2LDExMi4wMjNMMTgwLjI5Myw3MS4xNDINCglsNjMuNTYzLTIuNDNjMy44NDQtMC4xNDYsNi44OTYtMy4yNzYsNi45NDUtNy4xMjFsMC40NjQtMzYuMzkyYzAuMDIyLTEuOTMyLTAuNzI2LTMuNzkyLTIuMDgyLTUuMTY2DQoJYy0xLjM1Ni0xLjM3Mi0zLjIwNi0yLjE0Ny01LjEzNy0yLjE0N0g3LjIyYy0zLjk4OSwwLTcuMjIsMy4yMzEtNy4yMiw3LjIyMXY0MC41NThjMCwzLjk0NywzLjE3LDcuMTYzLDcuMTE1LDcuMjJsNjYuOTE3LDAuOTY0DQoJbDEyNy4yNTcsMjI0LjQ4OGwtMC41NjgsMTQwLjIwNWwtODguNDgsMy42MzFjLTMuODE3LDAuMTU1LTYuODUsMy4yNTktNi45MjMsNy4wNzdsLTAuNzE2LDM3LjUwNg0KCWMtMC4wMzcsMS45MzksMC43MDksMy44MSwyLjA2OSw1LjE5NmMxLjM1NiwxLjM4MywzLjIxMiwyLjE2MSw1LjE1MSwyLjE2MWgyNzYuNzYyYzEuOTgxLDAsMy44NzUtMC44MTMsNS4yMzktMi4yNDkNCgljMS4zNjMtMS40MzUsMi4wNzgtMy4zNjgsMS45NzQtNS4zNDZsLTEuOTMzLTM3LjEzMmMtMC4xOTItMy42OTItMy4xNC02LjY0MS02LjgzNS02LjgzNGwtNzYuMTI0LTMuOTkybC0xMS4wODItMTM2LjU3DQoJTDQzNi40NzksMTM3LjMzbDU1LjY0LTIuNTNjMy4wNjMtMC4xNDIsNS43MDQtMi4yMDIsNi41ODctNS4xMzlsMTIuOTA5LTQzLjAxOGMwLjI0OC0wLjcyOSwwLjM4NS0xLjUxNiwwLjM4NS0yLjMzMg0KCUM1MTIsODAuMzI1LDUwOC43NzIsNzcuMDkxLDUwNC43ODMsNzcuMDkxeiIvPg0KPC9zdmc+
[Screwdriver CD url]: https://qubitpi.github.io/screwdriver-cd-homepage/
[Screwdriver CD pipeline]: https://qubitpi.github.io/screwdriver-cd-guide/user-guide/configuration/workflow
