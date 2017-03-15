FROM microsoft/dotnet:1.1.1-sdk
ENV NUGET_XMLDOC_MODE skip
ARG CLRDBG_VERSION=VS2015U2
ARG CLRDBG_INSTALL_LOCATION=.
WORKDIR /clrdbg
RUN apt-get update && apt-get install -y unzip && rm -rf /var/lib/apt/lists/*
RUN curl -SL https://raw.githubusercontent.com/Microsoft/MIEngine/getclrdbg-release/scripts/GetClrDbg.sh --output GetClrDbg.sh \
    && chmod 700 GetClrDbg.sh \
    && ./GetClrDbg.sh -v $CLRDBG_VERSION -l $CLRDBG_INSTALL_LOCATION \
    && rm GetClrDbg.sh
ENV ASPNETCORE_URLS http://*:5000
EXPOSE 5000
WORKDIR /app/src/dde-web
ENTRYPOINT ["/bin/bash", "-c", "if [ -z \"$REMOTE_DEBUGGING\" ]; \
    then dotnet restore && dotnet run; \
    else sleep infinity; fi"]
