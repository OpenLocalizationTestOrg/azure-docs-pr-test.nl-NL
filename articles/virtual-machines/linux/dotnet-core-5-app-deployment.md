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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="55d20-103">Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="55d20-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="55d20-104">Nadat alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, vereist de werkelijke toepassingsimplementatie Hallo toobe behandeld.</span><span class="sxs-lookup"><span data-stu-id="55d20-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="55d20-105">Toepassingsimplementatie hier verwijst tooinstalling Hallo werkelijke toepassing binaire bestanden naar de Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="55d20-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="55d20-106">Voor Hallo muziek Store voorbeeld .net Core, NGINX en Supervisor moeten toobe geïnstalleerd en geconfigureerd op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="55d20-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="55d20-107">Hallo muziek Store binaire bestanden toobe op Hallo virtuele machine geïnstalleerd moeten en Hallo muziek Store-database vooraf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="55d20-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="55d20-108">Dit document beschrijft hoe de uitbreidingen van de virtuele Machine toepassing implementatie en configuratie tooAzure virtuele machines kunnen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="55d20-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="55d20-109">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="55d20-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="55d20-110">Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="55d20-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="55d20-111">de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="55d20-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="55d20-112">Het script voor configuratie</span><span class="sxs-lookup"><span data-stu-id="55d20-112">Configuration script</span></span>
<span data-ttu-id="55d20-113">Uitbreidingen van de virtuele Machine zijn gespecialiseerde programma's die worden uitgevoerd op basis van virtuele machines tooprovide configuratie automation.</span><span class="sxs-lookup"><span data-stu-id="55d20-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="55d20-114">Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie.</span><span class="sxs-lookup"><span data-stu-id="55d20-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="55d20-115">Een extensie voor aangepaste scripts kan worden gebruikt toorun scripts op basis van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="55d20-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="55d20-116">Met de Hallo muziek Store voorbeeld is van toohello aangepast script extensie tooconfigure Hallo Ubuntu virtuele machines en Hallo muziek Store-toepassing installeren.</span><span class="sxs-lookup"><span data-stu-id="55d20-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="55d20-117">Controleer voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, Hallo-script dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55d20-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="55d20-118">Dit script configureert Hallo Ubuntu virtuele machine toohost Hallo muziek Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="55d20-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="55d20-119">Wanneer uitvoert, Hallo script installeert alle benodigde software, Hallo muziek store-toepassing installeren vanuit broncodebeheer en Hallo database voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="55d20-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="55d20-120">toolearn meer informatie over het hosten van een .net Core toepassing op Linux, Zie [publiceren tooa Linux productieomgeving](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="55d20-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="55d20-121">Dit voorbeeld is voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="55d20-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="55d20-122">VM-extensie voor scripts</span><span class="sxs-lookup"><span data-stu-id="55d20-122">VM Script Extension</span></span>
<span data-ttu-id="55d20-123">VM-extensies kan worden uitgevoerd op basis van een virtuele machine tegelijk build door Hallo extensie resource in hello Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="55d20-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="55d20-124">Hallo-extensie kan worden toegevoegd met Hallo Resource toevoegen Visual Studio wizard, of door een geldige JSON in Hallo sjabloon invoegen.</span><span class="sxs-lookup"><span data-stu-id="55d20-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="55d20-125">Hallo Scriptextensie resource is genest binnen Hallo bron van de virtuele Machine. Deze kunnen worden gezien in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="55d20-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="55d20-126">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="55d20-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="55d20-127">U ziet in de onderstaande Hallo JSON die Hallo script wordt opgeslagen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="55d20-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="55d20-128">Dit script kan ook worden opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="55d20-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="55d20-129">Azure Resource Manager-sjablonen kunt ook Hallo script uitvoering tekenreeks tooconstructed zodanig dat de sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script.</span><span class="sxs-lookup"><span data-stu-id="55d20-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="55d20-130">In dit geval data is opgegeven bij het implementeren van Hallo sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van script Hallo.</span><span class="sxs-lookup"><span data-stu-id="55d20-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="55d20-131">Zie voor meer informatie over het gebruik van de aangepaste scriptextensie hello [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55d20-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="55d20-132">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="55d20-132">Next Step</span></span>
<hr>

[<span data-ttu-id="55d20-133">Ontdek meer Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="55d20-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

