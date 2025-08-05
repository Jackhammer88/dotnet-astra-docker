FROM registry.astralinux.ru/library/astra/ubi17:1.7.7.uu2 AS temp
RUN apt-get update && apt-get install -y --no-install-recommends wget
RUN wget https://builds.dotnet.microsoft.com/dotnet/Sdk/8.0.413/dotnet-sdk-8.0.413-linux-x64.tar.gz
RUN mkdir /dotnet && tar -xzf dotnet-sdk-8.0.413-linux-x64.tar.gz -C /dotnet

FROM registry.astralinux.ru/library/astra/ubi17:1.7.7.uu2 AS base
RUN apt-get update && apt-get install -y --no-install-recommends \
    icu-devtools \
    p7zip-full \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

COPY --from=temp /dotnet /opt/dotnet

ENV DOTNET_ROOT=/opt/dotnet
ENV PATH="$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools"

CMD ["/opt/dotnet/dotnet", "--info"]
