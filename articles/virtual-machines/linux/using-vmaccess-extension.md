---
title: aaaReset toegang tooan Azure Linux VM | Microsoft Docs
description: Hoe toomanage gebruikers en toegang opnieuw instellen voor het gebruik van virtuele Linux-machines Hallo VMAccess-extensie en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Beheren van gebruikers, SSH en controleer of herstel schijven over het gebruik van virtuele Linux-machines Hallo VMAccess-extensie Hello Azure CLI 2.0
Hallo-schijf op uw Linux-VM worden fouten weergegeven. U enigszins Hallo hoofdwachtwoord voor uw Linux-VM opnieuw instellen of uw persoonlijke SSH-sleutel per ongeluk worden verwijderd. Als dat is gebeurd terug in Hallo dagen van Hallo datacenter, zou u moet er toodrive en open vervolgens Hallo KVM tooget op Hallo server-console. Hello Azure VMAccess-extensie beschouwen als die KVM-switch waarmee u tooaccess console tooreset toegang tooLinux Hallo of voer schijfonderhoud niveau.

Dit artikel ziet u hoe toouse hello Azure VMAccess-extensie toocheck of herstellen van een schijf, gebruikerstoegang opnieuw instellen, beheren van gebruikersaccounts of instellen Hallo SSH-configuratie op Linux. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Manieren toouse hello VMAccess-extensie
Er zijn twee manieren waarop u Hallo VMAccess-extensie op uw Linux VM's kunt gebruiken:

* Hello Azure CLI 2.0 en Hallo vereist parameters gebruiken.
* [Gebruik onbewerkte JSON-bestanden die Hallo VMAccess-extensie proces](#use-json-files-and-the-vmaccess-extension) en klik vervolgens op te volgen.

Hallo na gebruik van de voorbeelden [az vm gebruiker](/cli/azure/vm/user) opdrachten. tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

## <a name="reset-ssh-key"></a>SSH-sleutel opnieuw instellen
Hallo volgende voorbeeld hersteld Hallo SSH-sleutel voor de gebruiker Hallo `azureuser` op Hallo VM met de naam `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Wachtwoord opnieuw instellen
Hallo volgende voorbeeld wachtwoord opnieuw instellen Hallo voor Hallo gebruiker `azureuser` op Hallo VM met de naam `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>SSH opnieuw starten
Hallo volgende voorbeeld wordt opnieuw opgestart Hallo SSH-daemon en opnieuw instellen van Hallo SSH configuratiewaarden toodefault die op een virtuele machine met de naam `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Een gebruiker maken
Hallo volgende voorbeeld maakt u een gebruiker met de naam `myNewUser` met behulp van een SSH-sleutel voor verificatie op Hallo VM met de naam `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Een gebruiker verwijderen
Hallo volgende voorbeeld wordt verwijderd met de naam van een gebruiker `myNewUser` op Hallo VM met de naam `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>JSON-bestanden gebruiken en Hallo VMAccess-extensie
Hallo volgen voorbeelden onbewerkte JSON-bestanden gebruiken. Gebruik [az vm-extensie set](/cli/azure/vm/extension#set) toothen aanroepen uw JSON-bestanden. Deze JSON-bestanden kunnen ook worden aangeroepen vanuit de Azure-sjablonen. 

### <a name="reset-user-access"></a>Toegang van gebruikers opnieuw instellen
Als u toegang tooroot kwijt op uw Linux-VM bent hebt, kunt u een script VMAccess tooreset starten SSH-sleutel of het wachtwoord van een gebruiker.

tooreset hello openbare SSH-sleutel van een gebruiker, maak een bestand met de naam `reset_ssh_key.json` en -instellingen in de volgende indeling Hallo toevoegen. Vervangt door uw eigen waarden Hallo `username` en `ssh_key` parameters:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset het wachtwoord van een gebruiker, maak een bestand met de naam `reset_user_password.json` en -instellingen in de volgende indeling Hallo toevoegen. Vervangt door uw eigen waarden Hallo `username` en `password` parameters:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>SSH opnieuw starten
toorestart Hallo SSH-daemon en Hallo SSH configuratiewaarden toodefault opnieuw instellen, maakt u een bestand met de naam `reset_sshd.json`. Hallo inhoud volgende toevoegen:

```json
{
  "reset_ssh": true
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Gebruikers beheren

toocreate een gebruiker die een SSH-sleutel voor verificatie gebruikt, maak een bestand met de naam `create_new_user.json` en -instellingen in de volgende indeling Hallo toevoegen. Vervangt door uw eigen waarden Hallo `username` en `ssh_key` parameters:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete een gebruiker, maak een bestand met de naam `delete_user.json` en Hallo volgende inhoud toe te voegen. Vervangen door uw eigen waarde voor Hallo `remove_user` parameter:

```json
{
  "remove_user":"myNewUser"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Controleren of herstellen Hallo-schijf
U vmaccess gebruikt kunt u ook controleren en herstellen van een schijf die u toohello Linux VM toegevoegd.

toocheck en vervolgens herstellen Hallo schijf, maakt u een bestand met de naam `disk_check_repair.json` en -instellingen in de volgende indeling Hallo toevoegen. Vervangen door uw eigen waarde voor de naam Hallo van `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Hallo VMAccess script uitvoeren:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Volgende stappen
Bijwerken van Linux, is het gebruik van hello Azure VMAccess-extensie is een methode toomake wijzigingen op een actieve Linux VM. U kunt ook hulpprogramma's zoals cloud init en Azure Resource Manager-sjablonen toomodify uw Linux-VM gebruiken bij het opstarten.

[Uitbreidingen van de virtuele machine en functies voor Linux](extensions-features.md)

[Azure Resource Manager-sjablonen met Linux VM-extensies](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van](using-cloud-init.md)

