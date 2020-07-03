FROM mcr.microsoft.com/dotnet/core/runtime-deps:2.1-bionic

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        software-properties-common\
        libxrender1 libfontconfig1 libx11-dev libjpeg62 libxtst6 libjpeg-turbo8\
                           fontconfig xfonts-75dpi xfonts-base libc6-dev libgdiplus && \
    curl -SL --output wkhtmltox_0.12.5-1.bionic_amd64.deb "https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb" && \
    dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb && \
    apt-get -f install &&\
    rm -rf /var/lib/apt/lists/*

# Install ASP.NET Core
ENV ASPNETCORE_VERSION 2.1.18

RUN curl -SL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNETCORE_VERSION/aspnetcore-runtime-$ASPNETCORE_VERSION-linux-x64.tar.gz \
    && aspnetcore_sha512='83d58102ba9d9b9a6f4f19ea799fd20939ff013b3d2e3348e363f41f30c1e902995f59538f9b04d8b671b310598206736ce7dd0acde51ce3847beb3262293d60' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf aspnetcore.tar.gz -C /usr/share/dotnet \
    && rm aspnetcore.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet