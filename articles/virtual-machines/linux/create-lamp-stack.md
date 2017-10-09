---
title: aaaDeploy licht op een virtuele Linux-machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo licht stack is op een Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>LICHT stack in Azure implementeren
In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) in Azure. U moet een Azure-account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en Hallo [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Overzicht van de snelle opdrachten

1. Opslaan en bewerken van Hallo [azuredeploy.parameters.json bestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour voorkeur op uw lokale machine.
2. Voer Hallo volgende twee opdrachten toocreate een resourcegroep en vervolgens de sjabloon te implementeren:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>LICHT op bestaande virtuele machine implementeren
Hallo volgende opdrachten updates pakketten vervolgens Apache, MySQL en PHP is geïnstalleerd:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>LICHT implementeren op nieuwe VM-overzicht

1. Maak een resourcegroep met [az groep maken](/cli/azure/group#create) toocontain Hallo nieuwe virtuele machine:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate Hallo VM zelf, kunt u een al geschreven Azure Resource Manager-sjabloon gevonden [hier op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Hallo opslaan [azuredeploy.parameters.json bestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour lokale computer.
3. Hallo bewerken **azuredeploy.parameters.json** bestand tooyour voorkeur invoer.
4. Hallo-sjabloon met implementeren [az implementatie maken] json-bestand verwijst naar Hallo gedownload:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

U hebt nu een Linux-VM gemaakt met licht al is geïnstalleerd. Als u wenst, kunt u Hallo installatie controleren door te gaan naar beneden[controleren licht geïnstalleerd](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>LICHT implementeren op een bestaande VM-overzicht
Als u informatie over het maken van een Linux-VM nodig hebt, kunt u head [toolearn hier hoe toocreate een Linux-VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Vervolgens moet u tooSSH in Hallo Linux VM. Als u hulp nodig bij het maken van een SSH-sleutel, kunt u head [toolearn hier hoe toocreate een SSH-sleutel op Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Als u een SSH-sleutel al hebt, gaat u verder gaan en SSH vanaf de opdrachtregel in uw Linux-VM met `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Nu dat u binnen uw Linux-VM werkt, doorlopen we kunt Hallo licht stack installeren op op basis van Debian-distributies. Hallo exacte opdrachten kunnen afwijken voor andere Linux-distributies.

#### <a name="installing-on-debianubuntu"></a>Installeren op Debian/Ubuntu
U moet hello-pakketten die worden geïnstalleerd na: `apache2`, `mysql-server`, `php5`, en `php5-mysql`. U kunt deze pakketten door rechtstreeks grabbing deze pakketten of met behulp van Tasksel installeren.
Voordat u installeert moet toodownload en lijsten pakket bijwerken.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Afzonderlijke pakketten
Met de apt get:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Met behulp van tasksel
U kunt ook downloaden Tasksel, een hulpprogramma Debian/Ubuntu waarmee meerdere verwante pakketten worden geïnstalleerd als een gecoördineerde 'taak' op het systeem.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Na het uitvoeren van een van de vorige opties hello, wordt u na vragen aan gebruiker tooinstall worden deze pakketten en verschillende andere afhankelijkheden. tooset een beheerderswachtwoord voor MySQL, druk op 'y' en klik vervolgens op 'Enter' toocontinue en volg alle andere aanwijzingen. Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL. 

![][1]

Voer Hallo opdracht toosee volgen andere PHP-uitbreidingen die beschikbaar als pakketten zijn:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Info.php document maken
Nu moet u kunnen toocheck welke versie van Apache, MySQL en PHP u via de opdrachtregel Hallo hebt typen `apache2 -v`, `mysql -v`, of `php -v`.

Als u zou zoals tootest verder, maakt u een snelle PHP info pagina tooview in een browser. Maak een bestand met Nano teksteditor met deze opdracht:

```bash
sudo nano /var/www/html/info.php
```

Binnen Hallo GNU Nano teksteditor toevoegen Hallo volgende regels:

```php
<?php
phpinfo();
?>
```

Vervolgens opslaan en sluiten Hallo teksteditor.

Starten met deze opdracht Apache zodat alle nieuwe installaties van kracht.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Controleer of licht is geïnstalleerd
U kunt nu Hallo PHP pagina die u hebt gemaakt met een browser openen en zullen toohttp://youruniqueDNS/info.php controleren. Dit ziet vergelijkbare toothis afbeelding.

![][2]

U kunt de Apache-installatie controleren door Hallo Apache2 Ubuntu standaardpagina door te gaan tooyou http://youruniqueDNS/ weer te geven. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

![][3]

Gefeliciteerd, u hebt alleen setup een licht-stack in uw Azure VM!

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo Ubuntu-documentatie op Hallo licht stack:

* [https://Help.Ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
