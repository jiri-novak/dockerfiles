# escape=`
FROM microsoft/windowsservercore as msi

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV NGINX_VERSION 1137
ENV NGINX_DOWNLOAD_URL https://kevinworthington.com/nginx${NGINX_VERSION}-64

RUN Invoke-WebRequest -Uri $env:NGINX_DOWNLOAD_URL -OutFile 'nginx.exe' ; `
	Start-Process nginx.exe -ArgumentList '/SILENT', '/NORESTART', 'DIR=C:\nginx' -NoNewWindow -Wait

# FROM microsoft/nanoserver
# WORKDIR /nginx
# COPY --from=msi /nginx .
# RUN dir
EXPOSE 80
CMD ["nginx/nginx.exe", "-g", "\"daemon off;\""]