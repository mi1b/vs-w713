
[![Join the chat at https://gitter.im/vault713/wallet713](https://badges.gitter.im/vault713/wallet713.svg)](https://gitter.im/vault713/wallet713?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# **Win10 + vs-w713 =**![Grin logo](https://ipfs.io/ipfs/QmYmwCGeB6zmobgRp349G3XRDvYQMRJPJXRwcEeHzgm36p)

### Docker container for [Wallet713](https://github.com/vault713/wallet713); a popular fork of the official [Grin](https://github.com/mimblewimble/grin) wallet.
### vs-w713 runs on [Docker Desktop](https://www.docker.com/products/docker-desktop) for Windows or Mac.

## Windows 10 Setup
Hyper-V is a requirement for Docker Desktop. Hyper-V can be enabled for the follwing versions of Windows 10:

* Windows 10 Enterprise, Professional, or Education.
* 64bit CPU with Second Level Address Translation (SLAT)
* CPU support for VM Monitor Mode Extension (VT-c)
* 4GB RAM (minimum)
* Virtualization Technology enabled (BIOS)

> :information_source: *Windows 10 Home can be upgraded to Windows 10 Pro. Settings > Update & Security > Activation*

## Getting Started
Run Windows PowerShell as Administrator.
> :information_source: *Press Windows+X > Windows PowerShell (Admin)*

In the following sections; text in `command boxes` should be  pasted into PowerShell (right click to paste clipboard, then hit Enter).

* Enable Hyper-V, then reboot:
 * `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

> :information_source: *[VirtualBox](https://www.virtualbox.org/) won't work with Hyper-V enabled. You can toggle Hyper-V, using [Hyper-V Switch](https://unclassified.software/en/apps/hypervswitch) by Yves Goergen.*

## Prepare Windows 10
Run Windows PowerShell as Administrator.
* Create work directories:
 * `mkdir \vs-w713\data`


* Pull multi-stage Dockerfile:
 * `Invoke-WebRequest -Uri "URL" -OutFile "\vs-w713\Dockerfile"`


* Pull vs-w713.dockerignore:
 * `Invoke-WebRequest -Uri "URL" -OutFile "\vs-w713\vs-w713.dockerignore"`

## Setup Docker Desktop

* Sign up for a [Docker Hub](https://hub.docker.com/signup) account.
* Download and install [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

> :information_source: *Docker starts automatically; ![whale](https://ipfs.io/ipfs/Qmd3RCnf58MoTH1uVbqehXg9keVZgBZMvA9vVpaN76hBKv) in the notification area indicates Docker is running.*

* Check you're connected to Docker:
 * `docker version`


* Check Docker can pull and run images:
 * `docker run hello-world`

## Build the Container

* Navigate to work directory:
 * `cd \vs-w713`


 * Build container images from Dockerfile context:
  * `docker build -t my/wallet713 .`

> :information_source: *Building the container images will take around 10 minutes on a fast PC (i7-8700k - 16GB RAM - M.2 PCIe SSD).*

## Run the Container (Open Wallet713)

 * Run the container and open Wallet713:
  * `docker run --rm --name wallet713 -ti -v $PWD/data:/root/.wallet713 my/wallet713 wallet713`

