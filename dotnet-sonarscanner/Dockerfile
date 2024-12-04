FROM mcr.microsoft.com/dotnet/sdk:8.0

LABEL "com.github.actions.name"="dotnet-sonarscanner"
LABEL "com.github.actions.description"="sonarscanner for dotnet core"
LABEL "com.github.actions.icon"="check"
LABEL "com.github.actions.color"="purple"

LABEL "repository"="https://github.com/Secbyte/dotnet-sonarscanner"
LABEL "homepage"="https://github.com/Secbyte/dotnet-sonarscanner"
LABEL "maintainer"="Joshua Duffy <mail@joshuaduffy.org>"

RUN apt update --yes
RUN apt install gpg --yes

RUN mkdir -p /usr/share/man/man1

RUN echo "deb http://http.us.debian.org/debian/ testing contrib main" >> /etc/apt/sources.list
RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
RUN mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
RUN wget -q https://packages.microsoft.com/config/debian/10/prod.list
RUN mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
RUN chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
RUN chown root:root /etc/apt/sources.list.d/microsoft-prod.list
RUN apt-get update
RUN apt-get install ca-certificates -y
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade ca-certificates  --yes
RUN apt-get install -y --no-install-recommends default-jre apt-transport-https
RUN apt-get install -y --no-install-recommends mono-complete
RUN apt-get install -y --no-install-recommends dotnet-sdk-8.0 aspnetcore-runtime-8.0
RUN apt-get -t testing install -y --no-install-recommends python3 python3-apt python3-pip
RUN apt-get update && apt-get install -y python3-pip
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
RUN apt-get autoremove -y
RUN dotnet tool install dotnet-sonarscanner --tool-path . --version 9.0.2

ADD entrypoint.sh /entrypoint.sh
