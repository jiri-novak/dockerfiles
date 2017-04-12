FROM microsoft/windowsservercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# install VS 2017 Build Tools
RUN Invoke-WebRequest "https://aka.ms/vs/15/release/vs_BuildTools.exe" -OutFile vs_BuildTools.exe -UseBasicParsing ; \
	Start-Process -FilePath 'vs_BuildTools.exe' -ArgumentList '--quiet', '--norestart', '--locale en-US' -Wait ; \
	Remove-Item .\vs_BuildTools.exe ; \
	Remove-Item -Force -Recurse 'C:\Program Files (x86)\Microsoft Visual Studio\Installer'

# install .NET Framework 4.6.2 Developer Pack
RUN Invoke-WebRequest "https://download.microsoft.com/download/E/F/D/EFD52638-B804-4865-BB57-47F4B9C80269/NDP462-DevPack-KB3151934-ENU.exe" -OutFile netfx-4.6.2-devpack.exe -UseBasicParsing ; \
    Start-Process -FilePath 'netfx-4.6.2-devpack.exe' -ArgumentList '/Quiet', '/NoRestart' -Wait ; \
    Remove-Item .\netfx-4.6.2-devpack.exe

# install Nuget.exe
RUN New-Item -ItemType Directory -Force -Path 'C:\Program Files (x86)\NuGet' ; \
	Invoke-WebRequest "https://dist.nuget.org/win-x86-commandline/v4.1.0/nuget.exe" -OutFile 'C:\Program Files (x86)\NuGet\nuget.exe' -UseBasicParsing ;

# adjust PATH
RUN setx /M PATH $($Env:PATH + ';C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin;C:\Program Files (x86)\NuGet')

CMD cmd