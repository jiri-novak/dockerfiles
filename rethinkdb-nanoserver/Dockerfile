FROM microsoft/nanoserver

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Install RethinkDB.
RUN Invoke-WebRequest "https://download.rethinkdb.com/windows/rethinkdb-2.3.6.zip" -OutFile 'rethinkdb-2.3.6.zip' -UseBasicParsing ; \
    Expand-Archive 'rethinkdb-2.3.6.zip' -DestinationPath '.' ; \
    Remove-Item 'rethinkdb-2.3.6.zip'

# Define mountable directories.
VOLUME ["c:/data"]

# Define working directory.
WORKDIR c:/data

# Define default command.
CMD ["c:/rethinkdb-2.3.6/rethinkdb", "--bind", "all"]

# Expose ports.
#   - 8080: web UI
#   - 28015: process
#   - 29015: cluster
EXPOSE 8080
EXPOSE 28015
EXPOSE 29015