# Base Images

This repository builds and pushes various custom base images required by many projects. 

- `lancemccarthy/skia-aspnet:6.0`
- `lancemccarthy/skia-aspnet:7.0`
- `lancemccarthy/skia-aspnet:8.0`
- `lancemccarthy/skia-aspnet:9.0`
- `lancemccarthy/skia-aspnet:10.0`

## Usage

For any applications that require SkiaSharp, there are some Linux dependencies that are missing from the newer Microsoft .NET base images. This project helps the situation by installing those dependencies on top of the latest Microsoft image.

This is particularly helpful when you use the .NET SDK container publishing feature, you dont have the ability to add bash commands to the base image. To solve this, just use `lancemccarthy/skia-aspnet:10.0` instead of `mcr.microsoft.com/dotnet/aspnet:10.0` for the **ContainerBaseImage** property during the build.

For example:

```bash
`dotnet publish --arch x64 -t:PublishContainer \
    -p PublishProfile=DefaultContainer \
    -p ContainerBaseImage="lancemccarthy/skia-aspnet:10.0" \
    -p ContainerImageTag="latest" \
    -p ContainerRepository="yourrepo/yourapp" \
    -p ContainerRegistry="registry.hub.docker.com"
```

## Build Transparency

This is a very transparent process, all Dockerfiles simply install the missing dependencies. The only difference between each image is the version tag of the Microsoft image.

Here is the .NET 10 Dockerfile:

```dockerfile
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/aspnet:10.0 AS base

# Pre-install dependencies needed by SkiaSharp to render text.
RUN apt-get update \
    && apt-get install -y --allow-unauthenticated \
    libfreetype6 \
    libfontconfig1 \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*
```
