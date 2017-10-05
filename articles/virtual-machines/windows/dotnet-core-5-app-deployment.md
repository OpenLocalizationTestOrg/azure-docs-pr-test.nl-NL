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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Toepassingsimplementatie met Azure Resource Manager-sjablonen voor virtuele machines van Windows

Zodra alle Azure-infrastructurele vereisten zijn geïdentificeerd en vertaald naar een implementatiesjabloon, wordt de werkelijke implementatie moet worden opgelost. Toepassingsimplementatie hier verwijst naar het installeren van de binaire bestanden van de werkelijke toepassingen naar Azure-resources. Voor het voorbeeld getoond, .net Core en IIS moet worden geïnstalleerd en geconfigureerd op elke virtuele machine. De binaire bestanden muziek moeten worden geïnstalleerd op de virtuele machine en de database muziek vooraf gemaakt.

Dit document beschrijft hoe uitbreidingen van de virtuele Machine kunnen automatiseren implementatie van toepassingen en configuratie van virtuele machines in Azure. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring. De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Het script voor configuratie
Uitbreidingen van de virtuele Machine zijn gespecialiseerde's die worden uitgevoerd op basis van virtuele machines, zodat configuratie automation. Extensies zijn beschikbaar voor veel specifieke doeleinden, zoals antivirus en configuratie van de logboekregistratie Docker-configuratie. De extensie voor aangepaste scripts kan worden gebruikt voor elk script uitvoeren op een virtuele machine. Het is tot de extensie voor aangepaste scripts voor het configureren van de virtuele machines van Windows en de muziek Store-toepassing installeren met het voorbeeld getoond.

Voordat u met gedetailleerde informatie over hoe de uitbreidingen van de virtuele machine zijn gedeclareerd in een Azure Resource Manager-sjabloon, controleert u het script dat wordt uitgevoerd. Dit script configureert u de virtuele machine van Windows voor het hosten van de muziek Store-toepassing. Wanneer uitvoert, installeert het script alle nodig software, de muziek store-toepassing installeren vanuit broncodebeheer en voorbereiden van de database. 

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
VM-extensies tegelijk worden uitgevoerd op basis van een virtuele machine build tijd door op te nemen van de bron van de extensie in de Azure Resource Manager-sjabloon. De uitbreiding kan worden toegevoegd met de wizard Resource toevoegen Visual Studio of door een geldige JSON niet worden ingevoegd in de sjabloon. De resource Scriptextensie is genest binnen de bron van de virtuele Machine; Dit is te zien in het volgende voorbeeld.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [VM Scriptextensie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

U ziet in de onderstaande JSON dat het script wordt opgeslagen in GitHub. Dit script kan ook worden opgeslagen in Azure Blob-opslag. Azure Resource Manager-sjablonen toestaan dat de Scripttekenreeks worden uitgevoerd zodat sjabloon parameterwaarden kunnen worden gebruikt als parameters voor de uitvoering van het script worden samengesteld. In dit geval data is opgegeven bij het implementeren van de sjablonen en deze waarden kunnen vervolgens worden gebruikt bij het uitvoeren van het script.

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

Zoals eerder vermeld, is het ook mogelijk voor het opslaan van uw eigen aangepaste scripts in Azure Blob-opslag. Er zijn twee opties voor het opslaan van de script-resources in blob-opslag; Verander de container/script openbare en volg dezelfde benaderen zoals hierboven, of het kan ook worden bewaard in persoonlijke blobopslag waarvoor u de storageAccountName en storageAccountKey voor de resourcedefinitie CustomScriptExtension opgeven.

In het onderstaande voorbeeld hebben we een stap verder gegaan. Terwijl het is mogelijk is de naam van het opslagaccount en de sleutel opgeven als een parameter of variabele tijdens de implementatie, bieden de Resource Manager-sjablonen de `listKeys` functie die u kunt de opslagaccountsleutel programmatisch verkrijgen en plaats deze in voor de sjabloon voor u tijdens de implementatie.

In het voorbeeld hieronder CustomScriptExtension resourcedefinitie onze aangepast script al is geüpload naar Azure storage-account genoemd `mystorageaccount9999` bestaat in een andere resourcegroep aangeroepen `mysa999rgname`. Wanneer er een sjabloon met deze bron implementeert de `listKeys` functie programmatisch verkrijgt de opslagaccountsleutel voor het opslagaccount `mystorageaccount9999` in de resourcegroep `mysa999rgname` en voegt u deze in de sjabloon voor ons.

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

Het belangrijkste voordeel van deze benadering is dat u niet hoeft u de parameters van de sjabloon of implementatie wijzigen in het geval van storage account sleutel kan worden gewijzigd.

Zie voor meer informatie over het gebruik van de extensie voor aangepaste scripts [aangepaste scriptextensies met Resource Manager-sjablonen](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Volgende stap
<hr>

[Ontdek meer Azure Resource Manager-sjablonen](https://github.com/Azure/azure-quickstart-templates)

