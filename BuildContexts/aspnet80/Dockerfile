FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base

# Pre-install dependencies needed by SkiaSharp to render text.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    libfreetype6 \
    libfontconfig1 \
    && rm -rf /var/lib/apt/lists/*