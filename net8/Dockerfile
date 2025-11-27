ARG ASTRA_VERSION=1.8.4
ARG NET_VERSION=8.0.416

FROM registry.astralinux.ru/library/astra/ubi18:${ASTRA_VERSION} AS temp
ARG NET_VERSION

RUN apt-get update && apt-get install -y --no-install-recommends wget
RUN wget https://builds.dotnet.microsoft.com/dotnet/Sdk/${NET_VERSION}/dotnet-sdk-${NET_VERSION}-linux-x64.tar.gz
RUN mkdir /dotnet && tar -xzf dotnet-sdk-${NET_VERSION}-linux-x64.tar.gz -C /dotnet

FROM registry.astralinux.ru/library/astra/ubi18:${ASTRA_VERSION} AS base
RUN apt-get update && apt-get install -y --no-install-recommends \
    icu-devtools \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

COPY --from=temp /dotnet /opt/dotnet

ENV DOTNET_ROOT=/opt/dotnet
ENV PATH="$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools"

CMD ["/opt/dotnet/dotnet", "--info"]
