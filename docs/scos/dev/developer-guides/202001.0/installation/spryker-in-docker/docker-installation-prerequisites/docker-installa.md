---
title: Docker Installation Prerequisites - Windows
originalLink: https://documentation.spryker.com/v4/docs/docker-installation-prerequisites-windows
redirect_from:
  - /v4/docs/docker-installation-prerequisites-windows
  - /v4/docs/en/docker-installation-prerequisites-windows
---


This article describes Docker installation prerequisites for Linux.

{% info_block warningBox %}
When running commands, you should use absolute paths. For example: `mkdir /d/spryker && cd $_` or `mkdir /c/Users/spryker && cd $_`.
{% endinfo_block %}

## Minimum System Requirements

Review the minimum system requirements in the table:

| System Requirement | Additional Details |
| --- | --- |
| Windows 10 64bit | Pro, Enterprise, or Education (1607 Anniversary Update, Build 14393 or later). |
| BIOS Virtualization is enabled | Typically, virtualization is enabled by default. Note that having the virtualization enabled is different from having Hyper-V enabled. This setting can be checked in the **Task Manager** → **Performance** tab.  For more details, see [Virtualization must be enabled](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled). |
| CPU SLAT-capable feature | SLAT is CPU related feature. It is called Rapid Virtualization Indexing (RVI). |
| RAM: 4GB | This is a minimum requirement. The value can be higher than 4GB. A lower value is not sufficient for installation purposes. |
| vCPU: 2 | This is a minimum requirement. The value can be higher than 2. A lower value is not sufficient for running the application. |

## Required Software and Configuration
Follow the steps below to install and configure the required software.

### Install Docker Desktop    

1. Download <a href="https://download.docker.com/win/stable/Docker for Windows Installer.exe"> Docker Desktop</a>.
    
2. Open the installation file and follow the instructions of the wizard.

#### Enable Docker Experimental Features

Experimental features are provided for testing and evaluation purposes.
Follow the steps to enable them:
1. Right-click the **Docker** icon in the tray and select **Settings**.
2. Select the **Docker Engine** tab.
3. Select Basic checkbox.
4. Update variables as follows:
```php
    {
  ....
  "experimental": true,
  "features": {
    "buildkit": true
  }
}
```

### Enable WSL

WSL is a Windows Subsystem for Linux. It allows Linux programs to run on Windows.

Follow the steps to enable WSL:

1. Open **Windows Control Panel** → **Programs** → **Programs and Features**.
2. Select **Turn Windows features on or off**  hyperlink.
![step 2](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Installation/Spryker+in+Docker/Docker+Install+Prerequisites+-+Windows/w-features-on-off.png){height="" width=""}

3. Check **Windows Subsystem for Linux** and click **OK**.
![step 3](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Installation/Spryker+in+Docker/Docker+Install+Prerequisites+-+Windows/windows-subsystem.png){height="" width=""}

### Install and Update Ubuntu

Install Ubuntu:

1. Open Microsoft Store.
2. In the Search filed, enter "Ubuntu" and press **Enter**.
3. From the search results page, select **Ubuntu 18.04 LTS** and install it.<br>
![Ubuntu step 3](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Installation/Spryker+in+Docker/Docker+Install+Prerequisites+-+Windows/ubuntu-in-store.png){height="" width=""}

Update Ubuntu:

1. Open the **Start menu**.
2. Find and launch **Ubuntu**.
3. Follow the instructions in the wizard.
4. Set the default root mount point in  `/etc/wsl.conf`.
```php
# Enable extra metadata options by default
[automount]
enabled = true
root = /
options = "metadata,umask=22,fmask=11"
mountFsTab = false
```
5. Restart Ubuntu.

### Install Docker 
Follow the steps to install Docker:
1. Update the apt package:
```bash
sudo apt-get update
```
    
2. Install packages to allow apt to use a repository over HTTPS:
```bash
sudo apt-get install \
apt-transport-https \
ca-certificates \
curl \
gnupg-agent \
software-properties-common
```

3. Add Docker's official GPG (GNU Privacy Guard) key:
```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
    
4. Set up a stable repository:
```bash
sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"
```
    
5. Install the latest version of Docker CE:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### Docker Compose
Follow the steps to install Docker Compose:
1. Download the current stable release of Docker Compose:
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
2. Apply executable permissions to the binary:
```bash
sudo chmod +x /usr/local/bin/docker-compose
```

### Docker Sync
Follow the steps to install docker-sync:
1. Install Ruby and Ruby -dev:
```bash
sudo apt-get install ruby ruby-dev
```
2. Install docker-sync
```bash
sudo gem install docker-sync
```
3. Set your Docker for Windows host as an ENV variable:

    a. Open the **Docker for Windows** settings and check **Expose daemon on tcp://localhost:2375 without TLS**.
    b. Run the following command in your WSL shell:
```bash
echo "export DOCKER_HOST=tcp://127.0.0.1:2375" >> ~/.bashrc
```
### Install OCaml
{% info_block warningBox "OCaml version" %}

Make sure to check the [OCaml release changelog](https://github.com/ocaml/ocaml/releases) and ensure that the OCaml version that you are going to install is compatible. In the examplary procedure below, we are using the version 4.06.0.

{% endinfo_block %}

Follow the steps to install OCaml:
1. Install the build script:
```bash
sudo apt-get install build-essential make
```
2. Download the ocaml archive:
```bash
wget http://caml.inria.fr/pub/distrib/ocaml-4.06/ocaml-4.06.0.tar.gz
```
3. Extract the downloaded archive:
```bash
tar xvf ocaml-4.06.0.tar.gz
```
4. Change the directory:
```bash
cd ocaml-4.06.0
```
5. Configure and compile ocaml:
```bash
./configure
make world
make opt
umask 022
```
6. Install ocaml and clean:
```bash
sudo make install
sudo make clean
```
## Install Unison
{% info_block warningBox "OCaml version" %}

Make sure to check the latest available Unison version. In the examplary procedure below, we are using the version 2.51.2.

{% endinfo_block %}
Follow the steps to install Unison:
    
1. Download the source code of the latest Unison version.
2. Compile and install it:
    1 . Download the Unison archive:
    ```bash
    wget https://github.com/bcpierce00/unison/archive/v2.51.2.tar.gz
    ```
    2. Extract the archive:

    ```bash
    tar xvf v2.51.2.tar.gz
    ```

    3. Change the directory:
    ```bash
    cd unison-2.51.2
    ```
    4. Compile and install Unison:
    ```bash
    $ make UISTYLE=text
    $ sudo cp src/unison /usr/local/bin/unison
    $ sudo cp src/unison-fsmonitor /usr/local/bin/unison-fsmonitor
    ```
    
**What's next?**
See [Modes Overview](/docs/scos/dev/developer-guides/202001.0/installation/spryker-in-docker/installation-guides/modes-overview) to learn about installation modes of Spryker in Docker.
If you've already selected an installation mode, follow one of the guides below:
* [Installation Guide - Development Mode](/docs/scos/dev/developer-guides/202001.0/installation/spryker-in-docker/installation-guides/installation-gu)
* [Installation Guide- Demo Mode](/docs/scos/dev/developer-guides/202001.0/installation/spryker-in-docker/installation-guides/installation-gu)
* [Integrating Docker into Existing Projects](/docs/scos/dev/developer-guides/202001.0/installation/spryker-in-docker/installation-guides/integrating-doc)
* [Running Production](/docs/scos/dev/developer-guides/202001.0/development-guide/back-end/running-product)

