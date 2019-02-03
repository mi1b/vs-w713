
[![Join the chat at https://gitter.im/vault713/wallet713](https://badges.gitter.im/vault713/wallet713.svg)](https://gitter.im/vault713/wallet713?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# **Win10 + vs-w713 =** ![Grin logo](https://ipfs.io/ipfs/QmdboUjYec5DW2bveXQasCm6Y19KjkZorULkTXo8ogfkU3)

### vs-w713 is a Debian Stretch container for [Wallet713](https://github.com/vault713/wallet713); a popular fork of the official [Grin](https://github.com/mimblewimble/grin) wallet.
![vs-w713](https://ipfs.io/ipfs/QmSchK6LTdTYgKqZ26DU7XcSBDiDrtquvikbRUQXitygJf)

### vs-w713 runs on [Docker Desktop](https://www.docker.com/products/docker-desktop) for Windows or Mac.

## Windows 10 Setup
Hyper-V is a requirement for Docker Desktop. Hyper-V requires:

* Windows 10 Enterprise, Professional, or Education.
* 64bit CPU with Second Level Address Translation (SLAT)
* CPU support for VM Monitor Mode Extension (VT-c)
* 4GB RAM (minimum)
* Virtualization Technology enabled (BIOS)

>*Windows 10 Home can be upgraded to Windows 10 Pro. Settings > Update & Security > Activation*

## Getting Started
Run Windows PowerShell as Administrator.
>*Press Windows+X > Windows PowerShell (Admin)*

In the following sections; text in `command boxes` should be  pasted into PowerShell (Admin). Right click to paste clipboard, hit Enter.

* Enable Hyper-V, then reboot:

  * `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

>*[VirtualBox](https://www.virtualbox.org/) won't work with Hyper-V enabled. You can toggle Hyper-V, using [Hyper-V Switch](https://unclassified.software/en/apps/hypervswitch) by Yves Goergen.*

## Prepare Windows 10
Download vs-w713 GitHub repository:

* PowerShell defaults to TLS 1.0 (cryptographically weak) - GitHub requires TLS 1.2:
  * `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 `
  
* Pull repository:
  * `Invoke-WebRequest -Uri "https://github.com/mi1b/vs-w713/archive/master.zip" -OutFile "\vs-w713.zip"`

* Extract repository:
  * `Expand-Archive -LiteralPath \vs-w713.zip -DestinationPath \`

## Setup Docker Desktop
* Sign up for a [Docker Hub](https://hub.docker.com/signup) account.
* Download and install [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

>*Docker starts automatically.  Docker is running when you see this icon ![whale](https://ipfs.io/ipfs/Qmd3RCnf58MoTH1uVbqehXg9keVZgBZMvA9vVpaN76hBKv) in the notification area.*

* Right click on the whale icon > Settings > Shared Drives > Tick C (or whichever drive letter you installed Windows on).

* As Docker needs to mount files, it requires access to the Windows filesystem. Docker will ask for credentials; use your normal Windows password.

* Check you're connected to Docker:
  * `docker version`
  
* Check Docker can pull and run images:
  * `docker run hello-world`

## Build the Container

* Navigate to work directory:
  * `cd \vs-w713-master\vs-w713`
  
 * Build container images from Dockerfile context:
   * `docker build -t my/wallet713 .`

>*Building the container images will take around 10 minutes on a fast PC. When the container is successfully built, you will recieve a SECURITY WARNING. Windows is a bit of a nanny. Its filesytem can't mark a file as executable. As we're building a Linux container in a Windows client, all files are marked executable by default (don't worry, just do it).*

## Run the Container (Opens Wallet713)

* Run the container and open Wallet713:
  * `docker run --rm --name wallet713 -ti -v $PWD/data:/root/.wallet713 my/wallet713 wallet713`
   
* Make a new wallet:
  * `init`

* Write down your recovery phrase and stash it somewhere safe.

* Lists available Wallet713 commands:
  * `-h`
  
 * Close Wallet713 and the container:
   * `exit`
   
* If anything weird happens (not saying it will) you can remove the container:
  * `docker rm -f wallet713`
  
* To start Wallet713 again, just run the container:
  * `docker run --rm --name wallet713 -ti -v $PWD/data:/root/.wallet713 my/wallet713 wallet713`
  
> *Whatever happens to the container doesn't matter. You can delete the container, all the images, and uninstall Docker. Your Wallet713 data remains in the **\vs-w713-master\vs-w713\data** folder. Grin is always safe, or as safe as it can be on the Windows filesystem.*


## Things You Should Know
Types of data Microsoft gleans via Windows 10:

* Name and contact
* Credentials
* Demographic
* Interests & favorites
* Payment
* Usage
* Contacts & relationships
* Location
* Content

[README](https://heimdalsecurity.com/en/windows-10-security-guide/privacy)

Send memes / get help: mi1b@protonmail.com
