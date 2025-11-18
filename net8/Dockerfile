FROM registry.astralinux.ru/library/astra/ubi18:1.8.3.uu1 AS temp
RUN apt-get update && apt-get install -y --no-install-recommends wget
RUN wget https://builds.dotnet.microsoft.com/dotnet/Sdk/8.0.415/dotnet-sdk-8.0.415-linux-x64.tar.gz
RUN mkdir /dotnet && tar -xzf dotnet-sdk-8.0.415-linux-x64.tar.gz -C /dotnet

FROM registry.astralinux.ru/library/astra/ubi18:1.8.3.uu1 AS base
RUN apt-get update && apt-get install -y --no-install-recommends \
    icu-devtools \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

COPY --from=temp /dotnet /opt/dotnet

ENV DOTNET_ROOT=/opt/dotnet
ENV PATH="$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools"

CMD ["/opt/dotnet/dotnet", "--info"]
