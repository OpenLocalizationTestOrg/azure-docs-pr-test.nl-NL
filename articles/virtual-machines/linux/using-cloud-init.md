---
title: aaaUse cloud init toocustomize een Linux-VM | Microsoft Docs
description: Hoe toouse cloud init toocustomize een Linux-VM tijdens het maken met Azure CLI 2.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Cloud-init toocustomize een Linux-VM te gebruiken tijdens het maken van
In dit artikel leest u hoe toomake een cloud-init script tooset Hallo hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts Hello Azure CLI 2.0. Hallo cloud init scripts worden aangeroepen wanneer u een virtuele machine (VM) van Azure CLI maken. Zie voor een meer gedetailleerd overzicht over het installeren van toepassingen, configuratiebestanden schrijven en injecteren sleutels van de Sleutelkluis, [in deze zelfstudie](tutorial-automate-vm-deployment.md). U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Snelle opdrachten
Maak een cloud-init.txt-script waarmee Hallo-hostnaam ingesteld, werkt u alle pakketten en voegt een gebruiker sudo tooLinux.

```yaml
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

Maken van een groep resource toolaunch virtuele machines in met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt Hallo resourcegroep met de naam *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) cloud init tooconfigure met deze tijdens het opstarten Hello `--custom-data` parameter.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften. [Cloud-init](https://cloudinit.readthedocs.org) is een normale manier tooinject als deze wordt opgestart voor Hallo waarvoor de eerste keer een script of configuratie-instellingen in die Linux VM.

In Azure, er zijn diverse manieren toomake wijzigingen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.

* Scripts met cloud-init invoeren.
* Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md).
* Een Azure-sjabloon met behulp van cloud-init.
* Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md).

tooinject scripts op elk gewenst moment na opstarten:

* SSH toorun opdrachten rechtstreeks
* Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md), imperatively of in een Azure-sjabloon
* Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.

> [!NOTE]
> VMAccess-extensie wordt uitgevoerd voor een script zoals root in Hallo dezelfde manier via SSH kunt. Echter kan met behulp van de VM-extensie Hallo verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:
| Alias | Uitgever | Aanbieding | SKU | Versie | cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |meest recente |Er is geen |
| CoreOS |CoreOS |CoreOS |Stabiel |meest recente |Ja |
| Debian |credativ |Debian |8 |meest recente |Er is geen |
| openSUSE |SUSE |openSUSE |13.2 |meest recente |Er is geen |
| RHEL |RedHat |RHEL |7.2 |meest recente |Er is geen |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |meest recente |Ja |

We kunnen werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Toevoegen van een cloud-init script toohello maken van VM's met hello Azure CLI
toolaunch een cloud-init-script bij het maken van een virtuele machine in Azure, geef Hallo cloud init-bestand met hello Azure CLI `--custom-data` overschakelen.

Maken van een groep resource toolaunch virtuele machines in met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt Hallo resourcegroep met de naam *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Maken van een cloud-init script tooset Hallo hostnaam van een Linux-VM
Een van de belangrijkste instellingen voor een Linux-VM en eenvoudigste Hallo zijn Hallo hostnaam. We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Tijdens opstarten Hallo Hallo VM stelt dit script cloud init Hallo hostnaam te*myservername*. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Aanmelding en controleer of de hostnaam Hallo Hallo nieuwe virtuele machine.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Een cloud-init-script maken
Voor beveiliging moet uw tooupdate Ubuntu VM op Hallo eerst wordt opgestart. Met behulp van cloud-init kunt we doen dat script, afhankelijk van de Linux-distributie Hallo u Hello volgen.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor Hallo Debian-familie
```yaml
#cloud-config
apt_upgrade: true
```

Nadat Linux is opgestart, alle geïnstalleerd hello-pakketten worden bijgewerkt via **apt get-**. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Een cloud-init script tooadd een tooLinux gebruiker maken
Een Hallo eerste taken op een nieuwe Linux-VM is een gebruiker voor uzelf of met behulp van tooavoid tooadd *hoofdmap*. SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd toohello *~/.ssh/authorized_keys* bestand met dit script cloud init.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Cloud-init voorbeeldscript `cloud_config_add_users.txt` voor Debian-familie
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Nadat Linux is opgestart, zijn alle gebruikers van de vermelde Hallo gemaakt en toegevoegd toohello sudo-groep. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

[Over functies en uitbreidingen van de virtuele machine](extensions-features.md)

[Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie](using-vmaccess-extension.md)
