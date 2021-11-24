---
title: B2B or B2C Demo Shop installation- Windows, with Development Virtual Machine
description: Learn how to install a B2B or a B2C Demo Shop B2B or B2C Demo Shop on Windows, with Development Virtual Machine
last_updated: Oct 18, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
originalArticleId: ecc0e603-220e-4f66-b22a-73f339b97ebf
redirect_from:
  - /2021080/docs/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /2021080/docs/en/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /docs/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /docs/en/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v6/docs/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v6/docs/en/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v5/docs/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v5/docs/en/b2b-b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v4/docs/b2b-demo-shop-installation-windows-with-development-virtual-machine
  - /v4/docs/en/b2b-demo-shop-installation-windows-with-development-virtual-machine
  - /v4/docs/b2c-demo-shop-installation-windows-with-development-virtual-machine
  - /v4/docs/en/b2c-demo-shop-installation-windows-with-development-virtual-machine

---

To install the Demo Shop for [B2B](/docs/scos/user/intro-to-spryker/b2b-suite.html) or [B2C](/docs/scos/user/intro-to-spryker/b2c-suite.html) implementations on Windows, with Development Virtual Machine, follow the steps below.

### 1. Install prerequisites

To set up your environment, install the following prerequisites:

* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [VirtualBox 5.2.2](https://www.virtualbox.org/wiki/Download_Old_Builds_5_2)
* [Vagrant 2.0.0+](https://www.vagrantup.com/downloads.html)
* *vagrant-vbguest* and *vagrant-hostmanager* plugins:

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-hostmanager
```

### 2. Install Spryker Virtual Machine

To install the VM, you need to run the following commands. For this purpose, use `Git Bash` command prompt with administrative privileges.

1. **Launch Git Bash:**

* Click **Start**.

* Start typing "Git Bash".

* In the search results, right-click **Git Bash** and select **Run as administrator**.
![Run git bash as administrator](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Installation/B2B+Demo+Shop+Installation+Guide/run-git-bash-as-administrator.png)

2. **Create the folder in which you want the source code to be placed:**

```bash
mkdir devvm
cd devvm
```

3. **Initialize the Vagrant environment**:

```bash
vagrant init devv410 https://u220427-sub1:PpiiHzuF2OIUzmcH@u220427-sub1.your-storagebox.de/devvm_v4.1.0.box
```
{% info_block warningBox %}

For _Spryker Core_ version **201907.0** or prior, you need to use an older version of the development machine:
```bash
vagrant init devvm2.3.1 https://github.com/spryker/devvm/releases/download/v2.3.1/spryker-devvm.box
```

{% endinfo_block %}

4. **Update the Vagrantfile**:

Add hostmanager plugin configuration:

```bash
mv Vagrantfile Vagrantfile.bak
awk '/^end/{print "  config.hostmanager.enabled = true\n  config.hostmanager.manage_host = true"}1' Vagrantfile.bak &gt; Vagrantfile
```

5. **Build and start the virtual machine**:

{% info_block warningBox %}

This step creates the VM without cloning the actual codebase. It will be done in the **step 3.8**.

{% endinfo_block %}

* For a B2B Demo Shop:
```bash
VM_SKIP_SF="1" VM_PROJECT=b2b-demo-shop SPRYKER_REPOSITORY="https://github.com/spryker-shop/b2b-demo-shop.git" vagrant up
```
* For a B2C Demo Shop:
```bash
VM_SKIP_SF="1" VM_PROJECT=b2c-demo-shop SPRYKER_REPOSITORY="https://github.com/spryker-shop/b2c-demo-shop.git" vagrant up
```

### 3. Install the shop

1. **Log into the VM:**

```bash
vagrant ssh
```

2. **Update the network configuration of the VM:**

```bash
sudo sed -i "s/eth1/eth1 $(ip -o -4 route show to default | cut -d ' ' -f 5)/g; s/create mask = 0775/create mask = 0777/g; s/directory mask = 0775/directory mask = 0777\n  force user = vagrant\n  force group = vagrant/g"  /etc/samba/smb.conf
```

3. **Add the Samba server to the autoload configuration and restart it:**

```bash
sudo systemctl enable smbd.service nmbd.service
sudo /etc/init.d/samba restart
```

4. **Update PHP and Jenkins configuration:**

```bash
sudo sed -i 's/user = www-data/user = vagrant/g'  /etc/php/7.4/fpm/pool.d/*.conf
sudo sed -i 's/=www-data/=vagrant/g' /etc/default/jenkins-devtest
sudo chown -R vagrant:vagrant /data/shop/devtest/shared/data/common/jenkins
```

5. **Restart PHP and Jenkins:**

```bash
sudo /etc/init.d/php7.4-fpm restart
sudo /etc/init.d/jenkins-devtest restart
```

6. **Change permissions for the project directory:**

```bash
sudo chown vagrant:vagrant .
sudo chmod og+rwx .
```

7. **Mount the share in Windows:**

    1. Start Windows Command Prompt. To do this, press `Win+R`, type `cmd` and press `Enter`.

    2. Execute the following command to mount the share as a network drive:

       ```bash
       net use s: \\spryker-vagrant\project\current /persistent:yes
       ```

    {% info_block infoBox %}
    The share will be mounted as the s: drive.
    {% endinfo_block %}

8. **Copy the codebase to the VM:**

**For a B2B Demo Shop:**

1. Logout from the VM and clone the codebase into the `c:\b2b-demo-shop` directory by executing the following commands in Git Bash:
```bash
cd /c/
git clone https://github.com/spryker-shop/b2b-demo-shop.git
```
2. In Windows Command Prompt, execute the command to move the `c:\b2b-demo-shop` directory to the network drive:
```bash
xcopy C:\b2b-demo-shop s: /he
```
where:
* **s:** - is the network drive you have mounted in the previous step.

**For a B2C Demo Shop:**
1. Logout from the VM and clone the codebase into the `c:\b2c-demo-shop` directory by executing the following commands in Git Bash:
```bash
cd /c/
git clone https://github.com/spryker-shop/b2c-demo-shop.git
```
2. In Windows Command Prompt, execute the command to move the `c:\b2c-demo-shop` directory to the network drive:
```bash
xcopy C:\b2c-demo-shop s: /he
```
where:
* **s:** - is the network drive you have mounted in the previous step.

 {% info_block infoBox %}

Make sure that the codebase has been copied completely.

{% endinfo_block %}

9. **Run the installation commands:**

     1. Switch back to Git Bash
     2. Go to the devvm folder you have created in the step **2.1**
     3. Run the following commands:

          ```bash
          vagrant ssh
          composer install
          vendor/bin/install
          ```

{% info_block warningBox %}

If you are using a devvm version lower than 2.2.0, run the `ulimit -n 65535` command first.

{% endinfo_block %}

Executing these steps will install all required dependencies, and run the installation process. Also, this will install the demo data and export it to `Redis` and `Elasticsearch`.

When the installation process is complete, Spryker Commerce OS is ready to use. It can be accessed via the following links:

**B2B Demo Shop:**
* `http://de.b2b-demo-shop.local` - front-end (Storefront);
* `http://zed.de.b2b-demo-shop.local` - backend (the Back Office).
* `http://glue.de.b2b-demo-shop.local` - REST API (Glue).

**B2C Demo Shop:**
* `http://de.b2c-demo-shop.local` - front-end (Storefront);
* `http://zed.de.b2c-demo-shop.local` - backend (the Back Office).
* `http://glue.de.b2c-demo-shop.local` - REST API (Glue).

Credentials to access the administrator interface: user `admin@spryker.com` and password `change123`.

## Next steps:
* [Troubleshooting installation issues](/docs/scos/dev/troubleshooting/troubleshooting-spryker-in-vagrant-issues/troubleshooting-spryker-in-vagrant-installation-issues.html)
