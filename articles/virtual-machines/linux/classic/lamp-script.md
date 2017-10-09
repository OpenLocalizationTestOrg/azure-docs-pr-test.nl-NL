---
title: aaaUse Hallo extensie CustomScript op een Linux-VM | Microsoft Docs
description: Meer informatie over hoe toouse hello CustomScript extensie toodeploy toepassingen op Linux virtuele Machines in Azure gemaakt met het klassieke implementatiemodel Hallo.
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Een licht-app met behulp van de extensie CustomScript Azure Hallo voor Linux implementeren
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor meer informatie over het implementeren van een licht stack Hallo Resource Manager-model met [hier](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hallo CustomScript uitbreiding voor Microsoft Azure voor Linux biedt een manier toocustomize uw virtuele machines (VM's) door het uitvoeren van willekeurige code geschreven in een scripttaal die wordt ondersteund door Hallo VM (bijvoorbeeld, Python en Bash). Dit biedt een zeer flexibele manier tooautomate toepassing implementatie toomultiple machines.

U kunt de extensie CustomScript Hallo implementeren met behulp van hello Azure-portal, Windows PowerShell of hello Azure-opdrachtregelinterface (Azure CLI).

In dit artikel we gebruiken hello Azure CLI toodeploy een eenvoudige licht toepassing tooan Ubuntu VM gemaakt met het klassieke implementatiemodel Hallo.

## <a name="prerequisites"></a>Vereisten
In dit voorbeeld maakt u eerst twee virtuele Azure-machines met Ubuntu 14.04 of hoger. Hallo VMs heten *script vm* en *licht vm*. Unieke namen gebruiken bij het maken van virtuele machines Hallo. Een gebruikte toorun Hallo CLI-opdrachten is en één gebruikte toodeploy Hallo licht app.

U moet ook een Azure Storage-account en een sleutel tooaccess it (u kunt dit krijgen via hello Azure-portal).

Als u informatie over het maken van virtuele Linux-machines in Azure nodig te verwijzen[maken van een virtuele Machine waarop Linux](createportal.md).

Hallo installeren opdrachten wordt ervan uitgegaan dat Ubuntu, maar u kunt Hallo installatie aanpassen voor een Linux-distro ondersteund.

Hallo moet script vm VM toohave die Azure CLI hebt geïnstalleerd, met een werkende verbinding tooAzure. Voor hulp bij dit te verwijzen[installeren en configureren van hello Azure-opdrachtregelinterface](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Uploaden van een script
We gebruiken Hallo extensie CustomScript toorun een script op een externe VM tooinstall Hallo licht stack en maken van een PHP-pagina. In de volgorde tooaccess Hallo script vanaf elke locatie hebt we het uploaden als een Azure-blob.

### <a name="script-overview"></a>Script-overzicht
Voorbeeld van een script Hallo een licht stack tooUbuntu (inclusief het instellen van een stille installatie van MySQL) installeert, schrijft u een eenvoudige PHP-bestand en Apache wordt gestart.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Script uploaden
Sla Hallo script op als een tekstbestand, bijvoorbeeld *install_lamp.sh*, en upload het tooAzure opslag. U kunt dit eenvoudig doen met Azure CLI. Hallo volgende voorbeeld wordt geüpload Hallo bestand tooa storage-container met de naam 'scripts'. Als het Hallo-container bestaat niet moet u toocreate het eerste.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Maak ook een JSON-bestand dat wordt beschreven hoe toodownload Hallo script uit Azure Storage. Opslaan als *public_config.json* ('mystorage' met de naam van uw opslagaccount Hallo vervangen):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Hallo-extensie implementeren
Nu kunt u Hallo volgende opdracht toodeploy Hallo de extensie CustomScript Linux toohello externe virtuele machine met behulp van Azure CLI Hallo.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

vorige opdracht Hallo gedownload en uitgevoerd Hallo *install_lamp.sh* script op Hallo VM aangeroepen *licht vm*.

Aangezien Hallo app een webserver bevat, onthouden tooopen een HTTP-luisterpoort op Hallo met de volgende opdracht Hallo externe virtuele machine.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Bewaking en probleemoplossing
U kunt controleren hoe goed Hallo aangepast script wordt uitgevoerd door te kijken Hallo logboekbestand op Hallo extern VM. SSH te*licht vm* en tail Hallo-logboekbestand met de volgende opdracht Hallo.

    cd /var/log/azure/customscript
    tail -f handler.log

Nadat u de extensie CustomScript Hallo hebt uitgevoerd, kunt u bladeren toohello PHP pagina die u hebt gemaakt voor meer informatie. Hallo PHP pagina Hallo bijvoorbeeld in dit artikel is *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Aanvullende bronnen
U kunt dezelfde basisstappen toodeploy Hallo complexere apps. In dit voorbeeld is het installatiescript Hallo opgeslagen als een openbare blob in Azure Storage. Een veiligere optie toostore Hallo installatiescript zou zijn als een beveiligde blob met een [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Aanvullende bronnen voor Azure CLI-, Linux- en de extensie CustomScript Hallo worden naast weergegeven.

[Voor het automatiseren van taken voor het virtuele Linux-machine aanpassen met behulp van de extensie CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Azure Linux-extensies (GitHub)](https://github.com/Azure/azure-linux-extensions)