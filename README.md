# Rancher Spinnaker Configuration Container

This project provides a Docker container to use in conjunction with [Rancher](http://rancher.com) when deploying the [Spinnaker](http://spinnaker.io) continuous deployment platform.

## How does it work?

This container leverages Rancher's [Meta-Data API](http://docs.rancher.com/rancher/metadata-service/) to provide the configuration for each individual service.
The container copies the contents of the `spinnaker` metadata key in Rancher to the file `/opt/spinnaker/config/spinnaker.yml`.
The configuration container can then be bound to the Spinnaker service application container using the `volumes_from` directive in Docker.
Each of the Spinnaker services will include this file as part of it's configuration parameters when starting up.

Additionally, this container will create AWS credentials files in `/root/.aws/credentials` and `/root/.aws/config` using the `aws.credentials` and `aws.config` metadata keys respectively.

__NOTE__: This container doesn't currently provide a mechanism for creating the `settings.js` configuration file for Spinnaker's [Deck](https://github.com/spinnaker/deck) service.
