# Custom .NET SDK Docker Images for Astra Linux UBI

This repository contains Dockerfiles and GitHub Actions workflows for building .NET SDK images on top of Astra Linux SE

These images are tailored for secure environments that require a Russian-certified OS base, while still providing access to modern .NET SDK versions (such as `8.0.408`).

---

## Available Tags

Images are automatically built and pushed to [Docker Hub](https://hub.docker.com/r/madfisht3) with explicit versioned tags.

> **Note:** There is *no `latest` tag*. All images must be referenced explicitly by version.

## Tag format
For example:
- `madfisht3/dotnet-sdk:alse1.8-[dotnet version] - for Astra UBI 1.8

The tag format is **alse1.8-8.0.408** this means **Astra Linux UBI 1.8**, dotnet version **8.0.408**

## Build Features

Each image is built from a minimal Astra UBI base, and the .NET SDK is downloaded directly from Microsoft archives. 
The SDK is extracted into /opt/dotnet, with DOTNET_ROOT and PATH configured accordingly.

## Included by default

- .NET SDK (version pinned by tag)

## Usage

Pull the image directly:

```bash
docker pull madfisht3/dotnet-sdk:alse1.8-8.0.408
```

Or in your own Dockerfile:

```
FROM madfisht3/dotnet-sdk:alse1.8-8.0.408

WORKDIR /app
COPY . .

RUN dotnet build
```

## No latest Tag

We do not provide a latest tag. This is by design to encourage explicit version pinning for better reproducibility and security in production environments.

Always specify the full tag like:

```
madfisht3/dotnet-sdk:alse1.8-8.0.408
```

## Feedback

Issues, pull requests, and suggestions are welcome!

