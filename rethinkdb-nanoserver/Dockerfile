# escape=`
FROM microsoft/nanoserver

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV RETHINKDB_VERSION 2.3.6
ENV RETHINKDB_DOWNLOAD_URL https://download.rethinkdb.com/windows/rethinkdb-${RETHINKDB_VERSION}.zip

# Install RethinkDB.
RUN Invoke-WebRequest $env:RETHINKDB_DOWNLOAD_URL -OutFile 'rethinkdb.zip' -UseBasicParsing ; `
    Expand-Archive 'rethinkdb.zip' -DestinationPath '.' ; `
    Remove-Item 'rethinkdb.zip'

# Define mountable directories.
VOLUME ["c:/data"]

# Define working directory.
WORKDIR c:/data

# Define default command.
CMD ["c:/rethinkdb/rethinkdb", "--bind", "all"]

# Expose ports.
#   - 8080: web UI
#   - 28015: process
#   - 29015: cluster
EXPOSE 8080
EXPOSE 28015
EXPOSE 29015