---
title: aaaDeploy licht op een virtuele Linux-machine Hello Azure CLI 1.0 | Microsoft Docs
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>LICHT stack Hello Azure CLI 1.0 implementeren
In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) in Azure. U moet een Azure-Account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en Hallo [Azure CLI](../../cli-install-nodejs.md) die [tooyour Azure-account verbonden](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0] – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* LICHT op bestaande virtuele machine implementeren

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>LICHT implementeren op nieuwe VM-overzicht
U kunt starten door het maken van een [resourcegroep](../../azure-resource-manager/resource-group-overview.md) waarin Hallo van nieuwe virtuele machine:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate Hallo VM zelf, kunt u een al geschreven Azure Resource Manager-sjabloon gevonden [hier op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

U ziet een antwoord sommige meer invoerwaarden vragen:

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

U hebt nu een Linux-VM gemaakt met licht al is geïnstalleerd. Als u wenst, kunt u Hallo installatie controleren door te gaan naar beneden[controleren licht geïnstalleerd](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>LICHT implementeren op een bestaande VM-overzicht
Als u informatie over het maken van een Linux-VM nodig hebt, kunt u head [toolearn hier hoe toocreate een Linux-VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Vervolgens moet u tooSSH in Hallo Linux VM. Als u hulp nodig bij het maken van een SSH-sleutel, kunt u head [toolearn hier hoe toocreate een SSH-sleutel op Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Als u een SSH-sleutel al hebt, gaat u verder gaan en SSH vanaf de opdrachtregel in uw Linux-VM met `ssh exampleUsername@exampleDNS`.

Nu dat u binnen uw Linux-VM werkt, doorlopen we kunt Hallo licht stack installeren op op basis van Debian-distributies. Hallo exacte opdrachten kunnen afwijken voor andere Linux-distributies.

#### <a name="installing-on-debianubuntu"></a>Installeren op Debian/Ubuntu
U moet hello-pakketten die worden geïnstalleerd na: `apache2`, `mysql-server`, `php5`, en `php5-mysql`. U kunt deze pakketten door rechtstreeks grabbing deze pakketten of met behulp van Tasksel installeren. Hieronder vindt u instructies voor beide opties.
Voordat u installeert moet toodownload en lijsten pakket bijwerken.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Afzonderlijke pakketten
Met de apt get:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Met behulp van tasksel
U kunt ook downloaden Tasksel, een hulpprogramma Debian/Ubuntu waarmee meerdere verwante pakketten worden geïnstalleerd als een gecoördineerde 'taak' op het systeem.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Na het uitvoeren van een van de vorige opties hello, wordt u na vragen aan gebruiker tooinstall worden deze pakketten en verschillende andere afhankelijkheden. Druk op 'y' en klik vervolgens op 'Enter' toocontinue en volg alle andere tooset wordt u gevraagd een beheerderswachtwoord voor MySQL. Hiermee installeert u Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL. 

![][1]

Voer Hallo opdracht toosee volgen andere PHP-uitbreidingen die beschikbaar als pakketten zijn:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Info.php document maken
Nu moet u kunnen toocheck welke versie van Apache, MySQL en PHP u via de opdrachtregel Hallo hebt typen `apache2 -v`, `mysql -v`, of `php -v`.

Als u zou zoals tootest verder, maakt u een snelle PHP info pagina tooview in een browser. Maak een bestand met Nano teksteditor met deze opdracht:

    user@ubuntu$ sudo nano /var/www/html/info.php

Binnen Hallo GNU Nano teksteditor toevoegen Hallo volgende regels:

    <?php
    phpinfo();
    ?>

Vervolgens opslaan en sluiten Hallo teksteditor.

Starten met deze opdracht Apache zodat alle nieuwe installaties van kracht.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Controleer of licht is geïnstalleerd
U kunt nu Hallo PHP pagina die u hebt gemaakt met een browser openen en zullen toohttp://youruniqueDNS/info.php controleren. Dit ziet vergelijkbare toothis afbeelding.

![][2]

U kunt de Apache-installatie controleren door Hallo Apache2 Ubuntu standaardpagina door te gaan tooyou http://youruniqueDNS/ weer te geven. U ziet er ongeveer zo deze installatiekopie.

![][3]

Gefeliciteerd, u hebt alleen setup een licht-stack in uw Azure VM!

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo Ubuntu-documentatie op Hallo licht stack:

* [https://Help.Ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png