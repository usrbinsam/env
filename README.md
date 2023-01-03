This repository describes my local development environment.

## OS

I run Windows 11 OEM with WSL installed.

## Package Managers

### Chocolatey

I use [Chocolatey](https://chocolatey.org/) to install packages that I'd like to keep up to date (helm, eksctl, flux) but in fact most of these tools I prefer to use in WSL anyway and therefore I sometimes have versions in Windows vs WSL.

### winget

Winget is very handy, but you have to be cautious because it might upgrade things to a later version that you don't want (like NodeJS).


### Homebrew

In WSL, I prefer to install as much of my development toolchain from [Homebrew](https://brew.sh/) as possible with the exception of packages that I require a specific version of and do not want them to be automatically updated (node, kubectl, python, etc.).

Even if a package is available from Ubuntu's repositories, I find that Brew usually has a more up-to-date version. 

## WSL

I install [WSL]((https://www.microsoft.com/store/productId/9P9TQF7MRM4R)) using the Microsoft Store, rather than using the published installers on Microsoft's website, that way I can use WSLg without any extra setup/install headache.

Don't forget to ensure all your appliances use WSL2 by default:

```
wsl --set-default-version 2
```

### WSL Appliance - Ubuntu

I use [Ubuntu](https://www.microsoft.com/store/productId/9PDXGNCFSCZV) installed through the Microsoft Store for my primary WSL appliance.


### /etc/wsl.conf

Some changes to `/etc/wsl.conf` in my Ubuntu appliance:

```ini
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"

[interop]
appendWindowsPath = false
```

## Docker for Desktop

For all things containerization, I use [Docker for Desktop](https://docs.docker.com/desktop/install/windows-install/) with the [WSL2 backend](https://docs.docker.com/desktop/windows/wsl/).

## Terminal

I use [Windows Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701) which is a huge improvement over good ole cmd.exe.

### PATH

A note about my `%PATH%` - I add `%USERPROFILE%\.bin` to my path where I can drop in miscellaneous binaries that I don't install via a package manager (ngrok, skaffold, kubectl, ffmpeg, etc.).

These programs have to be manually updated but that is fine.


### Aliases

I create some aliases to make life a little easier. I store the below file in `%USERPROFILE%\.bin\alias.cmd` and I add it as an Auto Run Command Processor.

```cmd
@echo off

DOSKEY k=kubectl.exe $*
DOSKEY sk=skaffold.exe $*
DOSKEY ls=dir /B $*
DOSKEY alias=code %USERPROFILE%\.bin\alias.cmd
```

Add it to the registry:
```regedit 
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor]
"CompletionChar"=dword:00000009
"DefaultColor"=dword:00000000
"EnableExtensions"=dword:00000001
"PathCompletionChar"=dword:00000009
"AutoRun"="%USERPROFILE%\\.bin\\alias.cmd"
```


## IDE

### IntelliJ

I install the [JetBrains Toolbox App](https://www.jetbrains.com/toolbox-app/) to manage my IDEs since it keeps everything up to date and allows simple rollbacks. 

I use:

- IDEA Ultimate with the Vuejs and PHP plugins for Vue and PHP apps
- PyCharm Professional with the Vuejs plugin 
- GoLand
- DataGrip

### VS Code

I keep [VS Code](https://code.visualstudio.com/) handy for a few things - its a good default editor and launches faster than IntelliJ products, and it can be used to quickly open files in WSL using `code` from WSL.

I also prefer to manage Kubernetes manifests from VS Code as well.
