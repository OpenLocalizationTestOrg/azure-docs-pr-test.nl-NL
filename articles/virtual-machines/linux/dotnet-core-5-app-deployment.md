---
title: aaaAutomating toepassingsimplementatie met uitbreidingen van de virtuele Machine | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele Linux-machines

Nadat alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, vereist de werkelijke toepassingsimplementatie Hallo toobe behandeld. Toepassingsimplementatie hier verwijst tooinstalling Hallo werkelijke toepassing binaire bestanden naar de Azure-resources. Voor Hallo muziek Store voorbeeld .net Core, NGINX en Supervisor moeten toobe geïnstalleerd en geconfigureerd op elke virtuele machine. Hallo muziek Store binaire bestanden toobe op Hallo virtuele machine geïnstalleerd moeten en Hallo muziek Store-database vooraf gemaakt.

Dit document beschrijft hoe de uitbreidingen van de virtuele Machine toepassing implementatie en configuratie tooAzure virtuele machines kunnen automatiseren. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo. de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Het script voor configuratie
Uitbreidingen van de virtuele Machine zijn gespecialiseerde programma's die worden uitgevoerd op basis van virtuele machines tooprovide configuratie automation. Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie. Een extensie voor aangepaste scripts kan worden gebruikt toorun scripts op basis van een virtuele machine. Met de Hallo muziek Store voorbeeld is van toohello aangepast script extensie tooconfigure Hallo Ubuntu virtuele machines en Hallo muziek Store-toepassing installeren. 

Controleer voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, Hallo-script dat wordt uitgevoerd. Dit script configureert Hallo Ubuntu virtuele machine toohost Hallo muziek Store-toepassing. Wanneer uitvoert, Hallo script installeert alle benodigde software, Hallo muziek store-toepassing installeren vanuit broncodebeheer en Hallo database voorbereiden. 

toolearn meer informatie over het hosten van een .net Core toepassing op Linux, Zie [publiceren tooa Linux productieomgeving](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Dit voorbeeld is voor demonstratiedoeleinden.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>VM-extensie voor scripts
VM-extensies kan worden uitgevoerd op basis van een virtuele machine tegelijk build door Hallo extensie resource in hello Azure Resource Manager-sjabloon. Hallo-extensie kan worden toegevoegd met Hallo Resource toevoegen Visual Studio wizard, of door een geldige JSON in Hallo sjabloon invoegen. Hallo Scriptextensie resource is genest binnen Hallo bron van de virtuele Machine. Deze kunnen worden gezien in Hallo voorbeeld te volgen.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

U ziet in de onderstaande Hallo JSON die Hallo script wordt opgeslagen in GitHub. Dit script kan ook worden opgeslagen in Azure Blob-opslag. Azure Resource Manager-sjablonen kunt ook Hallo script uitvoering tekenreeks tooconstructed zodanig dat de sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script. In dit geval data is opgegeven bij het implementeren van Hallo sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van script Hallo.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Zie voor meer informatie over het gebruik van de aangepaste scriptextensie hello [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Volgende stap
<hr>

[Ontdek meer Azure Resource Manager-sjablonen](https://github.com/Azure/azure-quickstart-templates)

