FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base

# Pre-install dependencies needed by SkiaSharp to render text.
RUN sed -i \
    -e 's|^deb http://deb.debian.org|# deb http://deb.debian.org|' \
    -e 's|^# deb http://snapshot.debian.org|deb [check-valid-until=no] http://snapshot.debian.org|' \
    /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    libfreetype6 \
    libfontconfig1 \
    && rm -rf /var/lib/apt/lists/*