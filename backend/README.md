This directory contains code for the components that comprise the Kubeflow
Pipelines backend.

## Building & Testing

To run all unit tests for backend:

```
go test -v -cover ./backend/...
```

To run the API server unit tests:

```
go test -v -cover ./backend/src/apiserver/...
```

The API server itself can be built using:

```
go build -o /tmp/apiserver backend/src/apiserver/*.go
```

## Building APIServer Image using Remote Build Execution

If you are a dev in the Kubeflow Pipelines team, you can use
[Remote Build Execution Service](https://cloud.google.com/sdk/gcloud/reference/alpha/remote-build-execution/)
to build the API Server image using Bazel with use of a shared cache for
speeding up the build. To do so, execute the following command:

```
./build_api_server.sh -i gcr.io/cloud-ml-pipelines-test/api-server:dev
```

## Building APIServer image locally

The API server image can be built from the root folder of the repo using:
```
export API_SERVER_IMAGE=api_server
docker build -f backend/Dockerfile . --tag $API_SERVER_IMAGE
```

## Building client library and swagger files

After making changes to proto files, the Go client libraries, Python client libraries and swagger files
need to be regenerated and checked-in. Refer to [backend/api](./api/README.md) for details.

## Updating licenses info

1. Install go-licenses tool from https://github.com/Bobgy/go-licenses/releases,
and refer to its documentation for how to use it.

2. Run the tool to update all licenses:

    ```bash
    make all
    ```


## Updating python dependencies

[pip-tools](https://github.com/jazzband/pip-tools) is used to manage python
dependencies. To update dependencies, edit [requirements.in](requirements.in)
and run `./update_requirements.sh` to update and pin the transitive
and pin the transitive dependencies.
