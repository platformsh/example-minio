# Minio (S3 compatible backend) on Platform.sh Example

This project provides a starter kit for using Minio in projects hosted on Platform.sh. It is primarily an example, although could be used as the starting point for a real project.

## Starting a new project

To start a new project based on this template, follow these 3 simple steps:

1. Clone this repository locally.  You may optionally remove the `origin` remote or remove the `.git` directory and re-init the project if you want a clean history.
 
2. Create a new project through the Platform.sh user interface and select "Import an existing project" when prompted.

3. Run the provided Git commands to add a Platform.sh remote and push the code to the Platform.sh repository.

That's it!  You now have a working "hello world" level project you can build on.

## Using as a reference

You can also use this repository as a reference for your own projects, and borrow whatever code is needed. The most important parts are the `.platform.app.yaml` file and the `.platform` directory.


# Installation and configuration

Minio is an open source object storage server compatible with Amazon S3 APIs https://minio.io

We have put the `.platform.app.yaml` file in a subdirectory, as often you would want Minio not as a separate project but part of a different project un multi-app mode. 

Note that this example installs Minio from source, you are on the edge, in production you might want to commit a static binary from https://dl.minio.io/server/minio/release/linux-amd64/minio as this project tends to be very much on the bleeding edge.

To configure Minio, after it deploys the first time you would want to configure an access key and a secret key.

```
platform variable:set env:MINIO_ACCESS_KEY youraccesskey
platform variable:set env:MINIO_SECRET_KEY yourverysecuresecretkey_please_dont_keep_this_example_value
```
And you are done, you now have your own private S3 Compatible.
 
You will probably want to install the Minio client see https://docs.minio.io/docs/minio-client-quickstart-guide.html for example on OS X: `brew install minio/stable/mc`:

To configure it run: 

`mc config host add Minio $(platform url --pipe| head -1) youraccesskey yourverysecuresecretkey_please_dont_keep_this_example_value`

You would be able to configure notifications (for example when a file is added) using RabbitMQ or Redis just add those to `.platform/services.yaml` to the `relationships` key in `.platform.app.yaml` and follow https://docs.minio.io/docs/minio-bucket-notification-guide.html to configure your Minio server.

Minio exposes both a REST API and a web-based interface.
