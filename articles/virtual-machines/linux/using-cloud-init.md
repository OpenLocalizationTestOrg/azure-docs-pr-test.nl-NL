---
title: Cloud-init gebruiken voor het aanpassen van een Linux-VM | Microsoft Docs
description: Het gebruik van cloud-init voor het aanpassen van een Linux-VM tijdens het maken van met de Azure CLI 2.0
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a>Cloud-init gebruiken voor het aanpassen van een Linux-VM tijdens het maken van
Dit artikel laat zien hoe u een cloud-init-script voor het instellen van de hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts met de Azure CLI 2.0. De cloud init-scripts worden aangeroepen wanneer u een virtuele machine (VM) van Azure CLI maken. Zie voor een meer gedetailleerd overzicht over het installeren van toepassingen, configuratiebestanden schrijven en injecteren sleutels van de Sleutelkluis, [in deze zelfstudie](tutorial-automate-vm-deployment.md). U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Snelle opdrachten
Een cloud-init.txt-script dat Hiermee stelt u de hostnaam, updates van alle pakketten en voegt een sudo-gebruiker toe aan Linux maken.

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

Maak een resourcegroep om te starten van virtuele machines in met [az groep maken](/cli/azure/group#create). Het volgende voorbeeld wordt de resourcegroep met de naam *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten met het `--custom-data` parameter.

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
Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften. [Cloud-init](https://cloudinit.readthedocs.org) is een standaard manier om een script of configuratie-instellingen in die Linux VM invoeren als deze voor de eerste keer wordt opgestart.

In Azure, er zijn een aantal verschillende manieren te wijzigen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.

* Scripts met cloud-init invoeren.
* Scripts met de Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md).
* Een Azure-sjabloon met behulp van cloud-init.
* Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md).

Scripts op elk gewenst moment na opstarten invoeren:

* SSH opdrachten rechtstreeks uitvoeren
* Scripts met de Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md), imperatively of in een Azure-sjabloon
* Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.

> [!NOTE]
> Een script wordt uitgevoerd als hoofdmap op dezelfde manier via SSH in VMAccess-extensie. Echter, met behulp van de VM-extensie kan verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:
| Alias | Uitgever | Aanbieding | SKU | Versie | cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |meest recente |Er is geen |
| CoreOS |CoreOS |CoreOS |Stabiel |meest recente |Ja |
| Debian |credativ |Debian |8 |meest recente |Er is geen |
| openSUSE |SUSE |openSUSE |13.2 |meest recente |Er is geen |
| RHEL |RedHat |RHEL |7.2 |meest recente |Er is geen |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |meest recente |Ja |

We werken met onze partners ophalen van cloud-init opgenomen en in de afbeeldingen die ze naar Azure bieden werkt.

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a>Een cloud-init-script toevoegen aan de virtuele machine maken met de Azure CLI
Als u wilt een cloud-init-script wordt gestart bij het maken van een virtuele machine in Azure, geeft u het cloud-init-bestand met de Azure CLI `--custom-data` overschakelen.

Maak een resourcegroep om te starten van virtuele machines in met [az groep maken](/cli/azure/group#create). Het volgende voorbeeld wordt de resourcegroep met de naam *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a>Een cloud-init-script voor het instellen van de hostnaam van een Linux-VM maken
Een van de eenvoudigste en meest belangrijke instellingen voor een Linux-VM is de hostnaam. We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Dit script cloud init wordt tijdens het opstarten van de virtuele machine, de hostnaam ingesteld op *myservername*. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Aanmelding en controleer of de hostnaam van de nieuwe virtuele machine.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Een cloud-init-script maken
Voor beveiliging moet uw Ubuntu VM bijwerken voor het eerst wordt opgestart. Met behulp van cloud-init die we doen dat met het script volgen, afhankelijk van de Linux-distributie die u gebruikt.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a>Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor de Debian-familie
```yaml
#cloud-config
apt_upgrade: true
```

Nadat Linux is opgestart, de geïnstalleerde pakketten worden bijgewerkt via **apt get-**. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.

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
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a>Een cloud-init script een gebruiker toevoegen aan Linux maken
Een van de eerste taken op een nieuwe Linux-VM is een gebruiker toevoegen voor uzelf of te vermijden met behulp van *hoofdmap*. SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd aan de *~/.ssh/authorized_keys* bestand met dit script cloud init.

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

Nadat Linux is opgestart, worden alle vermelde gebruikers gemaakt en toegevoegd aan de sudo-groep. Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Aanmelding en controleer of de nieuwe gebruiker.

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
Cloud-init steeds één standaardmethode voor het wijzigen van uw Linux VM op opstarten. Azure heeft ook een VM-extensies wijzigen van uw LinuxVM op opstarten of kunnen terwijl deze wordt uitgevoerd. Bijvoorbeeld, kunt u de Azure-VMAccessExtension opnieuw instellen van SSH of gebruikersgegevens terwijl de virtuele machine wordt uitgevoerd. Met cloud-init moet u opnieuw het wachtwoord opnieuw wilt opstarten.

[Over functies en uitbreidingen van de virtuele machine](extensions-features.md)

[Beheren van gebruikers, SSH en controleer of het herstellen van schijven op Azure Linux VM's met behulp van de VMAccess-extensie](using-vmaccess-extension.md)