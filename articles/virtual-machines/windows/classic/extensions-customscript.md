---
title: aaaCustom scriptextensie op een virtuele machine van Windows | Microsoft Docs
description: Virtuele machine van Azure-configuratietaken automatiseren met behulp van Hallo aangepast Script extensie toorun PowerShell-scripts op een externe Windows-VM
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Aangepast Script uitbreiding voor Windows met het klassieke implementatiemodel Hallo

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure. Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak. Scripts kunnen worden gedownload van Azure storage of GitHub, of toohello Azure-portal op extensie uitvoeringstijd. Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.

Dit document beschrijft hoe toouse Hallo extensie voor aangepaste scripts gebruiken hello Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem

Hallo-extensie voor aangepaste scripts voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016 versies.

### <a name="script-location"></a>De locatie van script

Hallo script moet toobe opgeslagen in Azure-opslag of een andere locatie die toegankelijk zijn via een geldige URL.

### <a name="internet-connectivity"></a>Verbinding met Internet

Hallo aangepast Script uitbreiding voor Windows is vereist dat Hallo doel-virtuele machine is verbonden toohello internet. 

## <a name="extension-schema"></a>Uitbreidingsschema

Hallo toont volgende JSON Hallo-schema voor de aangepaste Scriptextensie Hallo. Hallo-uitbreiding vereist de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht tooexecute. Een Azure storage-account en -account sleutel is vereist als voor informatie over het gebruik van Azure Storage als Hallo van de scriptbron. Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in configuratie van de beveiligde instelling Hallo-extensies. Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>Eigenschapswaarden

| Naam | Waarde / voorbeeld |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Uitgever | Microsoft.Compute |
| De extensie | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (bijvoorbeeld) | https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1 |
| commandToExecute (bijvoorbeeld) | PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1 |

## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo aangepaste Scriptextensie tijdens de sjabloonimplementatie van een Azure Resource Manager. Een voorbeeldsjabloon waarin de aangepaste Scriptextensie u hier vindt, Hallo [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>PowerShell-implementatie

Hallo `Set-AzureVMCustomScriptExtension` opdracht gebruikte tooadd Hallo aangepast Script extensie tooan bestaande virtuele machine kan worden. Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Oplossen van problemen en ondersteunen

### <a name="troubleshoot"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module. Hallo Implementatiestatus toosee van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uitvoering van de extensie uitvoer ons geregistreerde toofiles gevonden in de volgende map op de virtuele doelmachine Hallo Hallo.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Hallo script zelf is gedownload naar de volgende map op de virtuele doelmachine Hallo Hallo.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
