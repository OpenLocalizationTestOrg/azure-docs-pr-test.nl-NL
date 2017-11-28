---
title: aaaAutomating toepassingsimplementatie met uitbreidingen van de virtuele Machine | Microsoft Docs
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
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="b6553-103">Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="b6553-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="b6553-104">Nadat alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, vereist de werkelijke toepassingsimplementatie Hallo toobe behandeld.</span><span class="sxs-lookup"><span data-stu-id="b6553-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="b6553-105">Toepassingsimplementatie hier verwijst tooinstalling Hallo werkelijke toepassing binaire bestanden naar de Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="b6553-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="b6553-106">Voor Hallo muziek Store voorbeeld .net Core en IIS moeten toobe geïnstalleerd en geconfigureerd op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b6553-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="b6553-107">Hallo muziek Store binaire bestanden toobe op Hallo virtuele machine geïnstalleerd moeten en Hallo muziek Store-database vooraf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b6553-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="b6553-108">Dit document beschrijft hoe de uitbreidingen van de virtuele Machine toepassing implementatie en configuratie tooAzure virtuele machines kunnen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="b6553-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="b6553-109">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="b6553-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="b6553-110">Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6553-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="b6553-111">de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="b6553-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="b6553-112">Het script voor configuratie</span><span class="sxs-lookup"><span data-stu-id="b6553-112">Configuration script</span></span>
<span data-ttu-id="b6553-113">Uitbreidingen van de virtuele Machine zijn gespecialiseerde programma's die worden uitgevoerd op basis van virtuele machines tooprovide configuratie automation.</span><span class="sxs-lookup"><span data-stu-id="b6553-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="b6553-114">Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie.</span><span class="sxs-lookup"><span data-stu-id="b6553-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="b6553-115">Hallo-extensie voor aangepaste scripts kan worden gebruikt toorun scripts op basis van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b6553-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="b6553-116">Met de Hallo muziek Store voorbeeld is van toohello aangepast script extensie tooconfigure Hallo Windows virtuele machines en Hallo muziek Store-toepassing installeren.</span><span class="sxs-lookup"><span data-stu-id="b6553-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="b6553-117">Controleer voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, Hallo-script dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b6553-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="b6553-118">Dit script configureert Hallo Windows virtuele machine toohost Hallo muziek Store-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b6553-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="b6553-119">Wanneer uitvoert, Hallo script installeert alle benodigde software, Hallo muziek store-toepassing installeren vanuit broncodebeheer en Hallo database voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="b6553-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="b6553-120">Dit voorbeeld is voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="b6553-120">This sample is for demonstration purposes.</span></span>

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

## <a name="vm-script-extension"></a><span data-ttu-id="b6553-121">VM-extensie voor scripts</span><span class="sxs-lookup"><span data-stu-id="b6553-121">VM Script Extension</span></span>
<span data-ttu-id="b6553-122">VM-extensies kan worden uitgevoerd op basis van een virtuele machine tegelijk build door Hallo extensie resource in hello Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b6553-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="b6553-123">Hallo-extensie kan worden toegevoegd met Hallo Resource toevoegen Visual Studio wizard, of door een geldige JSON in Hallo sjabloon invoegen.</span><span class="sxs-lookup"><span data-stu-id="b6553-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="b6553-124">Hallo Scriptextensie resource is genest binnen Hallo bron van de virtuele Machine. Deze kunnen worden gezien in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="b6553-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="b6553-125">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="b6553-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="b6553-126">U ziet in de onderstaande Hallo JSON die Hallo script wordt opgeslagen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6553-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="b6553-127">Dit script kan ook worden opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b6553-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="b6553-128">Azure Resource Manager-sjablonen toestaan Hallo script uitvoering tekenreeks toobe samengesteld zodanig dat de sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script.</span><span class="sxs-lookup"><span data-stu-id="b6553-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="b6553-129">In dit geval data is opgegeven bij het implementeren van Hallo sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van script Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6553-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="b6553-130">Zoals eerder vermeld, maar het is ook mogelijk toostore uw aangepaste scripts in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b6553-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="b6553-131">Er zijn twee opties voor het opslaan van Hallo script resources in blob-opslag; Maak Hallo openbare container/script en volgt u dezelfde als hierboven benaderen hello, of kan ook worden bewaard in persoonlijke blobopslag waarvoor u tooprovide hello storageAccountName en storageAccountKey toohello CustomScriptExtension resourcedefinitie.</span><span class="sxs-lookup"><span data-stu-id="b6553-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="b6553-132">In onderstaande Hallo voorbeeld hebben we een stap verder geworden.</span><span class="sxs-lookup"><span data-stu-id="b6553-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="b6553-133">Hoewel het mogelijk tooprovide hello opslagaccountnaam en de sleutel als een parameter of variabele tijdens de implementatie is, Resource Manager-sjablonen bieden Hallo `listKeys` functie die Hallo storage-account kunt verkrijgen via een programma sleutel en plaats deze in toohello de sjabloon voor u tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b6553-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="b6553-134">In Hallo voorbeeld CustomScriptExtension resourcedefinitie onderstaande onze aangepast script is al geüploade tooan Azure storage-account genoemd `mystorageaccount9999` bestaat in een andere resourcegroep aangeroepen `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="b6553-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="b6553-135">Wanneer er een sjabloon met deze bron implementeert, Hallo `listKeys` functie verkrijgt programmatisch Hallo-toegangssleutel voor opslagaccount hello `mystorageaccount9999` in Hallo resourcegroep `mysa999rgname` en voegt u deze in de sjabloon toohello voor ons.</span><span class="sxs-lookup"><span data-stu-id="b6553-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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

<span data-ttu-id="b6553-136">Hallo belangrijkste voordeel van deze benadering is dat u niet u toochange uw sjabloon hoeft of implementatieparameters in de gebeurtenis Hallo van Hallo storage account sleutel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b6553-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="b6553-137">Zie voor meer informatie over het gebruik van de aangepaste scriptextensie hello [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6553-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="b6553-138">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="b6553-138">Next Step</span></span>
<hr>

[<span data-ttu-id="b6553-139">Ontdek meer Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="b6553-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

