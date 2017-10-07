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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele machines van Windows

Nadat alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, vereist de werkelijke toepassingsimplementatie Hallo toobe behandeld. Toepassingsimplementatie hier verwijst tooinstalling Hallo werkelijke toepassing binaire bestanden naar de Azure-resources. Voor Hallo muziek Store voorbeeld .net Core en IIS moeten toobe geïnstalleerd en geconfigureerd op elke virtuele machine. Hallo muziek Store binaire bestanden toobe op Hallo virtuele machine geïnstalleerd moeten en Hallo muziek Store-database vooraf gemaakt.

Dit document beschrijft hoe de uitbreidingen van de virtuele Machine toepassing implementatie en configuratie tooAzure virtuele machines kunnen automatiseren. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo. de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Het script voor configuratie
Uitbreidingen van de virtuele Machine zijn gespecialiseerde programma's die worden uitgevoerd op basis van virtuele machines tooprovide configuratie automation. Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie. Hallo-extensie voor aangepaste scripts kan worden gebruikt toorun scripts op basis van een virtuele machine. Met de Hallo muziek Store voorbeeld is van toohello aangepast script extensie tooconfigure Hallo Windows virtuele machines en Hallo muziek Store-toepassing installeren.

Controleer voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, Hallo-script dat wordt uitgevoerd. Dit script configureert Hallo Windows virtuele machine toohost Hallo muziek Store-toepassing. Wanneer uitvoert, Hallo script installeert alle benodigde software, Hallo muziek store-toepassing installeren vanuit broncodebeheer en Hallo database voorbereiden. 

> Dit voorbeeld is voor demonstratiedoeleinden.

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

## <a name="vm-script-extension"></a>VM-extensie voor scripts
VM-extensies kan worden uitgevoerd op basis van een virtuele machine tegelijk build door Hallo extensie resource in hello Azure Resource Manager-sjabloon. Hallo-extensie kan worden toegevoegd met Hallo Resource toevoegen Visual Studio wizard, of door een geldige JSON in Hallo sjabloon invoegen. Hallo Scriptextensie resource is genest binnen Hallo bron van de virtuele Machine. Deze kunnen worden gezien in Hallo voorbeeld te volgen.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

U ziet in de onderstaande Hallo JSON die Hallo script wordt opgeslagen in GitHub. Dit script kan ook worden opgeslagen in Azure Blob-opslag. Azure Resource Manager-sjablonen toestaan Hallo script uitvoering tekenreeks toobe samengesteld zodanig dat de sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script. In dit geval data is opgegeven bij het implementeren van Hallo sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van script Hallo.

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

Zoals eerder vermeld, maar het is ook mogelijk toostore uw aangepaste scripts in Azure Blob-opslag. Er zijn twee opties voor het opslaan van Hallo script resources in blob-opslag; Maak Hallo openbare container/script en volgt u dezelfde als hierboven benaderen hello, of kan ook worden bewaard in persoonlijke blobopslag waarvoor u tooprovide hello storageAccountName en storageAccountKey toohello CustomScriptExtension resourcedefinitie.

In onderstaande Hallo voorbeeld hebben we een stap verder geworden. Hoewel het mogelijk tooprovide hello opslagaccountnaam en de sleutel als een parameter of variabele tijdens de implementatie is, Resource Manager-sjablonen bieden Hallo `listKeys` functie die Hallo storage-account kunt verkrijgen via een programma sleutel en plaats deze in toohello de sjabloon voor u tijdens de implementatie.

In Hallo voorbeeld CustomScriptExtension resourcedefinitie onderstaande onze aangepast script is al geüploade tooan Azure storage-account genoemd `mystorageaccount9999` bestaat in een andere resourcegroep aangeroepen `mysa999rgname`. Wanneer er een sjabloon met deze bron implementeert, Hallo `listKeys` functie verkrijgt programmatisch Hallo-toegangssleutel voor opslagaccount hello `mystorageaccount9999` in Hallo resourcegroep `mysa999rgname` en voegt u deze in de sjabloon toohello voor ons.

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

Hallo belangrijkste voordeel van deze benadering is dat u niet u toochange uw sjabloon hoeft of implementatieparameters in de gebeurtenis Hallo van Hallo storage account sleutel wijzigen.

Zie voor meer informatie over het gebruik van de aangepaste scriptextensie hello [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Volgende stap
<hr>

[Ontdek meer Azure Resource Manager-sjablonen](https://github.com/Azure/azure-quickstart-templates)

