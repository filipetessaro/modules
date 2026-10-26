# syntax=docker/dockerfile:1-labs
FROM mcr.microsoft.com/dotnet/sdk:9.0@sha256:d7cfd59385751fc87897a138ba173fb1bbc2bf946ea78aecc91a119993676997 as builder

ADD https://github.com/Illumina/witty.er.git#v0.5.2 /src

WORKDIR /src/Wittyer
RUN dotnet publish -f net6.0 -r linux-x64 -c Release -o /output \
    && chmod +x /output/Wittyer

FROM mcr.microsoft.com/dotnet/runtime:9.0@sha256:4d0f9ec6855bf291008172c3aa46dead82854a1eb4c39533a335cf47579deb7f

LABEL git_repository=https://git.illumina.com/DASTE/Ilmn.Das.App.Wittyer.git
WORKDIR /opt/Wittyer
RUN apt-get -y update && apt-get -y install tabix libunwind8 openssl procps
COPY --from=builder /output /opt/Wittyer
