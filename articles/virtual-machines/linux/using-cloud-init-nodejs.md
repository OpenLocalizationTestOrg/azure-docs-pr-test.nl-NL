---
title: aaaUsing cloud init toocustomize een Linux-VM tijdens het maken in Azure | Microsoft Docs
description: Hoe toouse cloud init toocustomize een Linux-VM tijdens het maken met Azure CLI 1.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Cloud-init toocustomize een Linux-VM te gebruiken tijdens het maken van Hello Azure CLI 1.0
Dit artikel laat zien hoe toomake een cloud-init script tooset Hallo hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts.  Hallo cloud init scripts worden aangeroepen tijdens Hallo maken van virtuele machines van Azure CLI.  Hallo artikel is vereist:

* een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))
* Hallo [Azure CLI](../../cli-install-nodejs.md) aangemeld `azure login`.
* Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="quick-commands"></a>Snelle opdrachten
Maak een cloud-init.txt-script waarmee Hallo-hostnaam ingesteld, werkt u alle pakketten en voegt een gebruiker sudo tooLinux.

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
Maak een groep resource toolaunch virtuele machines in.

```azurecli
azure group create myResourceGroup westus
```

Maak een Linux-VM met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
### <a name="introduction"></a>Inleiding
Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften. [Cloud-init](https://cloudinit.readthedocs.org) is een normale manier tooinject als deze wordt opgestart voor Hallo waarvoor de eerste keer een script of configuratie-instellingen in die Linux VM.

In Azure, er zijn drie manieren toomake wijzigingen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.

* Scripts met cloud-init invoeren.
* Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Een Azure-sjabloon met behulp van cloud-init.
* Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooinject scripts op elk gewenst moment na opstarten:

* SSH toorun opdrachten rechtstreeks
* Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively of in een Azure-sjabloon
* Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.

> [!NOTE]
> : VMAccess-extensie wordt uitgevoerd voor een script zoals root in Hallo dezelfde manier via SSH kunt.  Echter kan met behulp van de VM-extensie Hallo verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:
| Alias | Uitgever | Aanbieding | SKU | Versie | cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |meest recente |Er is geen |
| CoreOS |CoreOS |CoreOS |Stabiel |meest recente |Ja |
| Debian |credativ |Debian |8 |meest recente |Er is geen |
| openSUSE |SUSE |openSUSE |13.2 |meest recente |Er is geen |
| RHEL |RedHat |RHEL |7.2 |meest recente |Er is geen |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |meest recente |Ja |

Microsoft is werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Toevoegen van een cloud-init script toohello maken van VM's met hello Azure CLI
toolaunch een cloud-init-script bij het maken van een virtuele machine in Azure, geef Hallo cloud init-bestand met hello Azure CLI `--custom-data` overschakelen.

Maak een groep resource toolaunch virtuele machines in.

```azurecli
azure group create myResourceGroup westus
```

Maak een Linux-VM met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Maken van een cloud-init script tooset Hallo hostnaam van een Linux-VM
Een van de belangrijkste instellingen voor een Linux-VM en eenvoudigste Hallo zijn Hallo hostnaam. We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Tijdens opstarten Hallo Hallo VM stelt dit script cloud init Hallo hostnaam te`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Aanmelding en controleer of de hostnaam Hallo Hallo nieuwe virtuele machine.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Een cloud-init script tooupdate Linux maken
Voor beveiliging moet uw tooupdate Ubuntu VM op Hallo eerst wordt opgestart.  Met behulp van cloud-init kunt we doen dat script, afhankelijk van de Linux-distributie Hallo u Hello volgen.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor Hallo Debian-familie
```sh
#cloud-config
apt_upgrade: true
```

Nadat Linux is opgestart, alle geïnstalleerd hello-pakketten worden bijgewerkt via `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

Aanmelding en controleer of alle pakketten worden bijgewerkt.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Maken van een script cloud init tooadd een tooLinux gebruiker
Een Hallo eerste taken op een nieuwe Linux-VM is een gebruiker voor uzelf of met behulp van tooavoid tooadd `root`. SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd toohello `~/.ssh/authorized_keys` bestand met dit script cloud init.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Cloud-init voorbeeldscript `cloud_config_add_users.txt` voor Debian-familie
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Nadat Linux is opgestart, zijn alle gebruikers van de vermelde Hallo gemaakt en toegevoegd toohello sudo-groep.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

Aanmelding en verificatie van gebruiker Hallo nieuw gemaakt.

```bash
ssh myVM
cat /etc/group
```

Uitvoer

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Volgende stappen
Cloud-init wordt steeds een standaardmanier toomodify uw Linux VM op opstarten. Azure heeft bovendien VM-extensies u toomodify kunnen uw LinuxVM op opstarten of terwijl deze wordt uitgevoerd. U kunt bijvoorbeeld gebruikersgegevens of hello Azure VMAccessExtension tooreset SSH gebruiken terwijl Hallo VM wordt uitgevoerd. Met cloud-init moet u een wachtwoord opnieuw opstarten tooreset Hallo.

[Over functies en uitbreidingen van de virtuele machine](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

