FROM mcr.microsoft.com/windows/servercore:1809-amd64

WORKDIR C:/tmp

ADD https://github.com/Kitware/CMake/releases/download/v3.13.5/cmake-3.13.5-win64-x64.zip cmake.zip
RUN PowerShell -Command Expand-Archive -LiteralPath cmake.zip -DestinationPath C:\tools\cmake
RUN dir C:\tools\cmake

ADD https://github.com/git-for-windows/git/releases/download/v2.22.0.windows.1/MinGit-2.22.0-64-bit.zip git.zip
RUN PowerShell -Command Expand-Archive -LiteralPath git.zip -DestinationPath C:\tools\git
RUN dir C:\tools\git

WORKDIR C:/
RUN del /S C:\tmp

CMD [ "cmd" ]
