---
title: aaaDeploying Linux Compute Resources met Azure Resource Manager-sjablonen | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="e3025-103">Toepassingsarchitectuur met Azure Resource Manager-sjablonen voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="e3025-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="e3025-104">Bij het ontwikkelen van een Azure Resource Manager-implementatie, moeten de compute-vereisten toobe toegewezen tooAzure resources en services.</span><span class="sxs-lookup"><span data-stu-id="e3025-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="e3025-105">Als een toepassing bestaat uit verschillende HTTP-eindpunten, een database en een gegevens in de cache van de service, hello Azure-resources die als host fungeren van elk van deze onderdelen moet toobe gerationaliseerd.</span><span class="sxs-lookup"><span data-stu-id="e3025-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="e3025-106">Hallo-voorbeeldtoepassing muziek Store bevat bijvoorbeeld een webtoepassing die wordt gehost op een virtuele machine en een SQL-database wordt gehost in Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="e3025-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="e3025-107">Dit document beschrijft hoe Hallo muziek Store rekenresources zijn geconfigureerd in Hallo voorbeeld Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3025-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="e3025-108">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="e3025-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="e3025-109">Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3025-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="e3025-110">de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="e3025-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="e3025-111">Virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e3025-111">Virtual Machine</span></span>
<span data-ttu-id="e3025-112">Hallo muziek Store-toepassing bevat een webtoepassing waarin klanten kunnen bladeren en muziek.</span><span class="sxs-lookup"><span data-stu-id="e3025-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="e3025-113">Er zijn verschillende Azure-services dat de host van webtoepassingen, in dit voorbeeld wordt een virtuele Machine wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e3025-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="e3025-114">Hallo-voorbeeldsjabloon muziek Store gebruikt, een virtuele machine is geïmplementeerd, een webserver installeren en Hallo muziek Store website geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e3025-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="e3025-115">Voor Hallo mogelijk te houden van dit artikel, de implementatie van virtuele machines met alleen Hallo worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="e3025-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="e3025-116">Hallo-configuratie van het Hallo-webserver en de toepassing hello is uiteengezet in een latere artikel.</span><span class="sxs-lookup"><span data-stu-id="e3025-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="e3025-117">Een virtuele machine kan worden toegevoegd met behulp van Visual Studio nieuwe Resource toevoegen wizard, of door een geldige JSON in Hallo implementatiesjabloon invoegen Hallo tooa-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3025-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="e3025-118">Wanneer u een virtuele machine implementeert, zijn ook enkele verwante resources nodig.</span><span class="sxs-lookup"><span data-stu-id="e3025-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="e3025-119">Als Visual Studio toocreate Hallo sjabloon gebruikt, worden deze resources voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3025-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="e3025-120">Als handmatig Hallo-sjabloon maken, moeten deze resources toobe ingevoegd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e3025-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="e3025-121">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [JSON van de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="e3025-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

<span data-ttu-id="e3025-122">Zodra geïmplementeerd, kunnen u de eigenschappen van de virtuele machine Hallo bekijken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3025-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Virtuele machine](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="e3025-124">Storage-Account</span><span class="sxs-lookup"><span data-stu-id="e3025-124">Storage Account</span></span>
<span data-ttu-id="e3025-125">Storage-accounts hebben veel opties voor opslag en mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e3025-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="e3025-126">Hallo-context van Azure virtuele machines bevat een opslagaccount Hallo virtuele harde schijven van Hallo virtuele machine en eventuele extra gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="e3025-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="e3025-127">Hallo muziek Store voorbeeld bevat één storage account toohold Hallo virtuele harde schijf van elke virtuele machine in Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e3025-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="e3025-128">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Opslagaccount](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="e3025-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="e3025-129">Storage-account is koppelen aan een virtuele machine in Hallo Resource Manager-sjabloondeclaratie van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e3025-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="e3025-130">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [virtuele Machine- en Storage-Account koppeling](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="e3025-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="e3025-131">Na de implementatie kan Hallo storage-account worden weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3025-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Storage-Account](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="e3025-133">Op te klikken in Hallo blob storage account-container, kunt Hallo virtuele harde schijf-bestand voor elke virtuele machine geïmplementeerd met Hallo sjabloon bekijken.</span><span class="sxs-lookup"><span data-stu-id="e3025-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Virtuele harde schijven](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="e3025-135">Zie voor meer informatie over Azure Storage [documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e3025-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="e3025-136">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="e3025-136">Virtual Network</span></span>
<span data-ttu-id="e3025-137">Als een virtuele machine interne netwerken zoals Hallo mogelijkheid toocommunicate met andere virtuele machines en de Azure-resources vereist, is een Azure-netwerk is vereist.</span><span class="sxs-lookup"><span data-stu-id="e3025-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="e3025-138">Een virtueel netwerk maakt geen Hallo virtuele machine toegankelijk zijn via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3025-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="e3025-139">Openbare-connectiviteit vereist een openbaar IP-adres, verderop in deze reeks wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="e3025-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="e3025-140">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [virtueel netwerk en subnetten](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="e3025-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="e3025-141">Van hello Azure-portal eruit Hallo virtueel netwerk Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="e3025-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="e3025-142">U ziet dat alle virtuele machines die zijn geïmplementeerd met Hallo sjabloon gekoppelde toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e3025-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Virtual Network](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="e3025-144">Netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="e3025-144">Network Interface</span></span>
 <span data-ttu-id="e3025-145">Een netwerkinterface verbindt een virtuele machine tooa virtueel netwerk, een meer specifiek tooa subnet dat is gedefinieerd in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3025-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="e3025-146">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [netwerkinterface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="e3025-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="e3025-147">De bron van elke virtuele machine bevat een netwerkprofiel.</span><span class="sxs-lookup"><span data-stu-id="e3025-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="e3025-148">Hallo-netwerkinterface is gekoppeld aan virtuele machine Hallo in dit profiel.</span><span class="sxs-lookup"><span data-stu-id="e3025-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="e3025-149">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [netwerkprofiel van de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="e3025-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="e3025-150">Van hello Azure-portal eruit netwerkinterface Hallo Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="e3025-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="e3025-151">Hallo interne IP-adres en de koppeling van Hallo-virtuele machine kunnen worden weergegeven op het Hallo-netwerkbron interface.</span><span class="sxs-lookup"><span data-stu-id="e3025-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Netwerkinterface](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="e3025-153">Zie voor meer informatie over Azure Virtual Networks [Azure Virtual Network-documentatie](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="e3025-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="e3025-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e3025-154">Azure SQL Database</span></span>
<span data-ttu-id="e3025-155">Bovendien is tooa virtuele machine die als host fungeert voor een Azure SQL Database-website muziek Store Hallo geïmplementeerde toohost Hallo muziek Store-database.</span><span class="sxs-lookup"><span data-stu-id="e3025-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="e3025-156">Hallo voordeel van het gebruik van Azure SQL Database hier is dat een tweede set van virtuele machines niet vereist is en schaal en beschikbaarheid is ingebouwd in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="e3025-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="e3025-157">Een Azure SQL database kan worden toegevoegd met behulp van Visual Studio nieuwe Resource toevoegen wizard, of door een geldige JSON in een sjabloon invoegen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3025-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="e3025-158">Hallo SQL Server-bron bevat een gebruikersnaam en wachtwoord beheerdersrechten op Hallo SQL-exemplaar wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="e3025-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="e3025-159">Ook wordt een bron van de firewall SQL toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e3025-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="e3025-160">Standaard zijn de toepassingen die worden gehost in Azure kunnen tooconnect met Hallo SQL-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e3025-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="e3025-161">tooallow externe toepassing zoals een SQL Server Management studio tooconnect toohello SQL-exemplaar, Hallo firewall moet toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e3025-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="e3025-162">Voor Hallo mogelijk te houden van Hallo muziek Store demo is de standaardconfiguratie Hallo fijn.</span><span class="sxs-lookup"><span data-stu-id="e3025-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="e3025-163">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="e3025-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="e3025-164">Een weergave van Hallo SQL server en database MusicStore zoals gezien in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3025-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="e3025-166">Zie voor meer informatie over het implementeren van Azure SQL Database [documentatie van Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="e3025-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="e3025-167">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="e3025-167">Next step</span></span>
<hr>

[<span data-ttu-id="e3025-168">Stap 2 - toegang en beveiliging in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="e3025-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

