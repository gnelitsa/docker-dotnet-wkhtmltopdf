FROM mcr.microsoft.com/dotnet/core/runtime-deps:2.2.3-bionic

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        software-properties-common\
        libxrender1 libfontconfig1 libx11-dev libjpeg62 libxtst6 libjpeg-turbo8\
                           fontconfig xfonts-75dpi xfonts-base libc6-dev libgdiplus && \
    apt-get -f install &&\
    rm -rf /var/lib/apt/lists/*

# Install ASP.NET Core
ENV ASPNETCORE_VERSION 2.2.3

RUN curl -SL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNETCORE_VERSION/aspnetcore-runtime-$ASPNETCORE_VERSION-linux-x64.tar.gz \
    && aspnetcore_sha512='53be8489aafa132c1a7824339c9a0d25f33e6ab0c42f414a8bda014b60ff82a20144032bd7e887d375dc275bb5dbeb71d38c7f90c39016895df8d3cf3c4b7a95' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf aspnetcore.tar.gz -C /usr/share/dotnet \
    && rm aspnetcore.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet