# escape=`

# Image to build on Visual Studio 2019

FROM python:3.7.4-windowsservercore-ltsc2016

ENV HOME=C:\home

WORKDIR ${HOME}

# Git
# From https://github.com/docker-library/golang/blob/master/1.12/windows/windowsservercore-ltsc2016/Dockerfile
ENV GIT_VERSION 2.22.0
ENV GIT_TAG v${GIT_VERSION}.windows.1
ENV GIT_DOWNLOAD_URL https://github.com/git-for-windows/git/releases/download/${GIT_TAG}/MinGit-${GIT_VERSION}-64-bit.zip
ENV GIT_DOWNLOAD_SHA256 308CE95B7DE5792BED9D56E1AF5D2053052EA6347EA0021F74070056684CE3EE

RUN Write-Host ('Downloading {0} ...' -f $env:GIT_DOWNLOAD_URL); `
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest -Uri $env:GIT_DOWNLOAD_URL -OutFile 'git.zip'; `
    `
    Write-Host ('Verifying sha256 ({0}) ...' -f $env:GIT_DOWNLOAD_SHA256); `
    if ((Get-FileHash git.zip -Algorithm sha256).Hash -ne $env:GIT_DOWNLOAD_SHA256) { `
        Write-Host 'FAILED!'; `
        exit 1; `
    }; `
    `
    Write-Host 'Expanding ...'; `
    Expand-Archive -Path git.zip -DestinationPath C:\git\.; `
    `
    Write-Host 'Removing ...'; `
    Remove-Item git.zip -Force; `
    `
    Write-Host 'Updating PATH ...'; `
    $env:PATH = 'C:\git\cmd;C:\git\mingw64\bin;C:\git\usr\bin;' + $env:PATH; `
    [Environment]::SetEnvironmentVariable('PATH', $env:PATH, [EnvironmentVariableTarget]::Machine); `
    `
    Write-Host 'Verifying install ...'; `
    Write-Host '  git --version'; git --version; `
    `
    Write-Host 'Complete.';

# CMake
ENV CMAKE_VERSION 3.14.6
ENV CMAKE_DOWNLOAD_URL https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-win64-x64.msi
ENV CMAKE_DOWNLOAD_SHA256 9E724FAFFA7CC1646151C49CA224C808C62BD10622DA158B51125B1EDAE833D1

RUN Write-Host ('Downloading {0} ...' -f $env:CMAKE_DOWNLOAD_URL); `
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest -Uri $env:CMAKE_DOWNLOAD_URL -OutFile 'cmake.msi'; `
    `
    Write-Host ('Verifying sha256 ({0}) ...' -f $env:CMAKE_DOWNLOAD_SHA256); `
    if ((Get-FileHash cmake.msi -Algorithm sha256).Hash -ne $env:CMAKE_DOWNLOAD_SHA256) { `
        Write-Host 'FAILED!'; `
        exit 1; `
    }; `
    `
    Write-Host 'Installing ...'; `
    Start-Process msiexec -ArgumentList '-i cmake.msi -quiet' -Wait; `
    `
    Write-Host 'Removing ...'; `
    Remove-Item cmake.msi -Force; `
    `
    Write-Host 'Updating PATH ...'; `
    $env:PATH = 'C:\Program Files\CMake\bin;' + $env:PATH; `
    [Environment]::SetEnvironmentVariable('PATH', $env:PATH, [EnvironmentVariableTarget]::Machine); `
    `
    Write-Host 'Verifying install ...'; `
    Write-Host '  cmake --version'; cmake --version; `
    `
    Write-Host 'Complete.';

# See https://docs.microsoft.com/visualstudio/install/advanced-build-tools-container
#     https://docs.microsoft.com/visualstudio/install/use-command-line-parameters-to-install-visual-studio
#     https://docs.microsoft.com/visualstudio/install/workload-component-id-vs-build-tools

ENV VCTOOLS_VERSION 16
ENV VCTOOLS_DOWNLOAD_URL https://aka.ms/vs/${VCTOOLS_VERSION}/release/vs_buildtools.exe
ENV VCTOOLS_DOWNLOAD_SHA256 6642E716910CEBA23C6CA90B3ECE1D239492A1708C86B4E84728AE40BDF88428

RUN Write-Host ('Downloading {0} ...' -f $env:VCTOOLS_DOWNLOAD_URL); `
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest -Uri $env:VCTOOLS_DOWNLOAD_URL -OutFile 'vs_buildtools.exe'; `
    `
    Write-Host ('Verifying sha256 ({0}) ...' -f $env:VCTOOLS_DOWNLOAD_SHA256); `
    if ((Get-FileHash vs_buildtools.exe -Algorithm sha256).Hash -ne $env:VCTOOLS_DOWNLOAD_SHA256) { `
        Write-Host 'FAILED!'; `
        exit 1; `
    }; `
    `
    Write-Host 'Installing ...'; `
    Start-Process vs_buildtools.exe `
        -ArgumentList `
            '--installPath', 'C:\BuildTools', `
            '--add', 'Microsoft.VisualStudio.Workload.VCTools', `
            '--add', 'Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core', `
            '--add', 'Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang', `
            '--includeRecommended', `
            '--quiet', '--norestart', '--nocache' `
        -NoNewWindow -Wait; `
    `
    Write-Host 'Removing ...'; `
    Remove-Item vs_buildtools.exe -Force; `
    `
    Write-Host 'Complete.';

SHELL ["cmd", "/S", "/C"]
ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&
CMD cmd.exe
