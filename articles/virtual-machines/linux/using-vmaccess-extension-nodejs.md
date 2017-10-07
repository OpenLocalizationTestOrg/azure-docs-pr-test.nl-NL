---
title: aaaReset toegang over het gebruik van Azure Linux VM's Hallo VMAccess-extensie | Microsoft Docs
description: Opnieuw instellen op Azure Linux VM's met behulp van Hallo VMAccess-extensie.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van VMAccess-extensie Hallo Hello Azure CLI 1.0
Dit artikel ziet u hoe toouse hello Azure VMAcesss extensie toocheck of herstellen van een schijf, gebruikerstoegang opnieuw instellen, beheren van gebruikersaccounts of opnieuw Hallo SSHD configureren op Linux. Hallo artikel is vereist:

* een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))
* Hallo [Azure CLI](../../cli-install-nodejs.md) aangemeld `azure login`.
* Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands)– onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten
Er zijn twee manieren toouse VMAccess op uw virtuele Linux-machines:

* Met behulp van hello Azure CLI 1.0 en Hallo vereiste parameters.
* Met behulp van onbewerkte JSON-bestanden die VMAccess verwerkt en klik vervolgens op te volgen.

Voor Hallo snelle opdracht sectie, gaan we toouse hello Azure CLI 1.0 `azure vm reset-access` methode. Volgende opdrachtvoorbeelden Vervang in Hallo Hallo waarden met "voorbeeld" hello waarden van uw eigen omgeving.

## <a name="create-a-resource-group-and-linux-vm"></a>Een resourcegroep en een virtuele Linux-machine maken
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Een Debian virtuele machine maken
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>Root-wachtwoord opnieuw instellen
tooreset hello root-wachtwoord:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>SSH-sleutel opnieuw instellen
tooreset hello SSH-sleutel van een gebruiker niet hoofdmap:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Een gebruiker maken
een gebruiker toocreate:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Een gebruiker verwijderen
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>SSHD opnieuw instellen
tooreset hello SSHD configuratie:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
### <a name="vmaccess-defined"></a>VMAccess gedefinieerd:
Hallo-schijf op uw Linux-VM worden fouten weergegeven. U enigszins Hallo hoofdwachtwoord voor uw Linux-VM opnieuw instellen of uw persoonlijke SSH-sleutel per ongeluk worden verwijderd. Als dat is gebeurd terug in Hallo dagen van Hallo datacenter, zou u moet er toodrive en open vervolgens Hallo KVM tooget op Hallo server-console. Hello Azure VMAccess-extensie beschouwen als die KVM-switch waarmee u tooaccess console tooreset toegang tooLinux Hallo of voer schijfonderhoud niveau.

Voor Hallo gedetailleerde uitleg gaan we toouse Hallo lange vorm van VMAccess dat gebruikmaakt van onbewerkte JSON-bestanden.  Deze VMAccess JSON-bestanden kunnen ook worden aangeroepen vanuit de Azure-sjablonen.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Het gebruik van VMAccess toocheck of reparatie van de Hallo schijf van een Linux-VM
U vmaccess gebruikt kunt u een fsck doen uitvoeren op de schijf Hallo onder uw Linux-VM.  U kunt ook een schijf controleren en de herstellen van een schijf met behulp van een VMAccess doen.

Gebruik dit script VMAccess toocheck en herstel Hallo schijf:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Met behulp van VMAccess tooreset gebruiker toegang tooLinux
Als u toegang tooroot kwijt op uw Linux-VM bent hebt, kunt u een hoofdwachtwoord VMAccess script tooreset Hallo starten.

tooreset hello hoofdwachtwoord, gebruik dit script vmaccess gebruikt:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

tooreset hello SSH-sleutel van een niet-hoofdgebruiker dit script VMAccess gebruiken:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Met behulp van VMAccess toomanage gebruikersaccounts op Linux
VMAccess is een pythonscript dat gebruikt toomanage gebruikers op uw Linux-VM worden kan zonder aanmelden en het gebruik van sudo of Hallo root-account.

toocreate een gebruiker, gebruikt u dit script vmaccess gebruikt:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete een gebruiker, gebruikt u dit script vmaccess gebruikt:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Met behulp van VMAccess tooreset hello SSHD configuratie
Als u wijzigingen toohello Linux VM's SSHD configuratie en SSH-verbinding sluiten Hallo voordat verifiëren, Hallo wijzigingen aanbrengt, u kan worden voorkomen dat SSH'ing weer in.  VMAccess mag gebruikte tooreset hello SSHD configuratie back tooa bekende juiste configuratie zonder worden geregistreerd in via SSH.

tooreset hello SSHD configuratie dit script VMAccess gebruiken:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Hallo VMAccess script uitvoeren:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Volgende stappen
Bijwerken van Linux, met behulp van Azure VMAccess extensies één methode toomake wijzigingen op een actieve Linux VM is.  U kunt ook hulpprogramma's zoals cloud init en Azure-sjablonen toomodify uw Linux-VM gebruiken bij het opstarten.

[Over functies en uitbreidingen van de virtuele machine](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure Resource Manager-sjablonen met Linux VM-extensies](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

