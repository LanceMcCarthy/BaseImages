FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/aspnet:8.0 AS base

# Pre-install Telerik Reporting dependencies for Skia fonts, then clean up.
RUN apt-get update \
    && apt-get install -y --allow-unauthenticated \
    libfreetype6 \
    libfontconfig1 \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*