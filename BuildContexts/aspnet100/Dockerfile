FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/aspnet:10.0 AS base

# Pre-install dependencies needed by SkiaSharp to render text.
RUN apt-get update \
    && apt-get install -y --allow-unauthenticated \
    libfreetype6 \
    libfontconfig1 \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*