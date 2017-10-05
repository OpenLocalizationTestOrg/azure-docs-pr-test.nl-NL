---
title: Toepassingsimplementatie met uitbreidingen van de virtuele Machine automatiseren | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="decf0-103">Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="decf0-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="decf0-104">Zodra alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, wordt de werkelijke implementatie moet worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="decf0-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="decf0-105">Toepassingsimplementatie hier verwijst naar het installeren van de binaire bestanden van de werkelijke toepassingen naar Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="decf0-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="decf0-106">Voor het voorbeeld getoond, .net Core en IIS moet worden geïnstalleerd en geconfigureerd op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="decf0-106">For the Music Store sample, .Net Core and IIS need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="decf0-107">De binaire bestanden muziek moeten worden geïnstalleerd op de virtuele machine en de database muziek vooraf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="decf0-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="decf0-108">Dit document beschrijft hoe uitbreidingen van de virtuele Machine kunnen automatiseren implementatie van toepassingen en configuratie van virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="decf0-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="decf0-109">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="decf0-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="decf0-110">Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring.</span><span class="sxs-lookup"><span data-stu-id="decf0-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="decf0-111">De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="decf0-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="decf0-112">Het script voor configuratie</span><span class="sxs-lookup"><span data-stu-id="decf0-112">Configuration script</span></span>
<span data-ttu-id="decf0-113">Uitbreidingen van de virtuele Machine zijn gespecialiseerde's die worden uitgevoerd op basis van virtuele machines, zodat configuratie automation.</span><span class="sxs-lookup"><span data-stu-id="decf0-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="decf0-114">Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie.</span><span class="sxs-lookup"><span data-stu-id="decf0-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="decf0-115">De extensie voor aangepaste scripts kan worden gebruikt voor elk script uitvoeren op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="decf0-115">The Custom Script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="decf0-116">Het is tot de extensie voor aangepaste scripts voor het configureren van de virtuele machines van Windows en de muziek Store-toepassing installeren met het voorbeeld getoond.</span><span class="sxs-lookup"><span data-stu-id="decf0-116">With the Music Store sample, it is up to the custom script extension to configure the Windows virtual machines and install the Music Store application.</span></span>

<span data-ttu-id="decf0-117">Voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, controleert u het script dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="decf0-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="decf0-118">Dit script configureert u de virtuele machine van Windows voor het hosten van de muziek Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="decf0-118">This script configures the Windows virtual machine to host the Music Store application.</span></span> <span data-ttu-id="decf0-119">Wanneer uitvoert, installeert het script alle nodig software, de muziek store-toepassing installeren vanuit broncodebeheer en voorbereiden van de database.</span><span class="sxs-lookup"><span data-stu-id="decf0-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

> <span data-ttu-id="decf0-120">Dit voorbeeld is voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="decf0-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="decf0-121">VM-extensie voor scripts</span><span class="sxs-lookup"><span data-stu-id="decf0-121">VM Script Extension</span></span>
<span data-ttu-id="decf0-122">VM-extensies tegelijk worden uitgevoerd op basis van een virtuele machine build tijd door op te nemen van de bron van de extensie in de Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="decf0-122">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="decf0-123">De uitbreiding kan worden toegevoegd met de wizard Resource toevoegen Visual Studio of door een geldige JSON niet worden ingevoegd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="decf0-123">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="decf0-124">De resource Scriptextensie is genest binnen de bron van de virtuele Machine; Dit is te zien in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="decf0-124">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="decf0-125">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="decf0-125">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="decf0-126">U ziet in de onderstaande JSON dat het script wordt opgeslagen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="decf0-126">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="decf0-127">Dit script kan ook worden opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="decf0-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="decf0-128">Azure Resource Manager-sjablonen toestaan dat de Scripttekenreeks worden uitgevoerd zodat sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="decf0-128">Also, Azure Resource Manager templates allow the script execution string to be constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="decf0-129">In dit geval data is opgegeven bij het implementeren van de sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van het script.</span><span class="sxs-lookup"><span data-stu-id="decf0-129">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="decf0-130">Zoals eerder vermeld, is het ook mogelijk voor het opslaan van uw eigen aangepaste scripts in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="decf0-130">As mentioned above, it is also possible to store your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="decf0-131">Er zijn twee opties voor het opslaan van de script-resources in blob-opslag; Verander de container/script openbare en volg dezelfde benaderen zoals hierboven, of het kan ook worden bewaard in persoonlijke blobopslag waarvoor u de storageAccountName en storageAccountKey voor de resourcedefinitie CustomScriptExtension opgeven.</span><span class="sxs-lookup"><span data-stu-id="decf0-131">There are two options for storing the script resources in blob storage; either make the container/script public and follow the same approach as above, or it can also be kept in private blob storage which requires you to provide the storageAccountName and storageAccountKey to the CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="decf0-132">In het onderstaande voorbeeld hebben we een stap verder gegaan.</span><span class="sxs-lookup"><span data-stu-id="decf0-132">In the example below we have gone a step further.</span></span> <span data-ttu-id="decf0-133">Terwijl het is mogelijk is de naam van het opslagaccount en de sleutel opgeven als een parameter of variabele tijdens de implementatie, bieden de Resource Manager-sjablonen de `listKeys` functie die u kunt de opslagaccountsleutel programmatisch verkrijgen en plaats deze in voor de sjabloon voor u tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="decf0-133">While it is possible to provide the storage account name and key as a parameter or variable during deployment, Resource Manager templates provide the `listKeys` function that can obtain the storage account key programmatically and insert it in to the template for you at deployment time.</span></span>

<span data-ttu-id="decf0-134">In het voorbeeld hieronder CustomScriptExtension resourcedefinitie onze aangepast script al is geüpload naar Azure storage-account genoemd `mystorageaccount9999` bestaat in een andere resourcegroep aangeroepen `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="decf0-134">In the example CustomScriptExtension resource definition below, our custom script has already been uploaded to an Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="decf0-135">Wanneer er een sjabloon met deze bron implementeert de `listKeys` functie programmatisch verkrijgt de opslagaccountsleutel voor het opslagaccount `mystorageaccount9999` in de resourcegroep `mysa999rgname` en voegt u deze in de sjabloon voor ons.</span><span class="sxs-lookup"><span data-stu-id="decf0-135">When we deploy a template containing this resource, the `listKeys` function programmatically obtains the storage account key for the storage account `mystorageaccount9999` in the Resource Group `mysa999rgname` and inserts it in to the template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="decf0-136">Het belangrijkste voordeel van deze benadering is dat u niet hoeft u de parameters van de sjabloon of implementatie wijzigen in het geval van storage account sleutel kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="decf0-136">The main benefit of this approach is that it does not require you to change your template or deployment parameters in the event of the storage account key changing.</span></span>

<span data-ttu-id="decf0-137">Zie voor meer informatie over het gebruik van de extensie voor aangepaste scripts [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="decf0-137">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="decf0-138">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="decf0-138">Next Step</span></span>
<hr>

[<span data-ttu-id="decf0-139">Ontdek meer Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="decf0-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

