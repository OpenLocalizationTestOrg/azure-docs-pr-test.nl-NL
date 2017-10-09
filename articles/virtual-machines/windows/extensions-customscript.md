---
title: aaaAzure aangepast Script uitbreiding voor Windows | Microsoft Docs
description: Configuratietaken voor Windows-VM automatiseren met behulp van Hallo aangepaste scriptextensie
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Extensie voor aangepaste scripts voor Windows

Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure. Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak. Scripts kunnen worden gedownload van Azure storage of GitHub, of toohello Azure-portal op extensie uitvoeringstijd. Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.

Dit document beschrijft hoe toouse Hallo extensie voor aangepaste scripts gebruiken hello Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem

Hallo-extensie voor aangepaste scripts voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016 versies.

### <a name="script-location"></a>De locatie van script

Hallo script moet toobe opgeslagen in Azure Blob-opslag of een andere locatie die toegankelijk zijn via een geldige URL.

### <a name="internet-connectivity"></a>Verbinding met Internet

Hallo aangepast Script uitbreiding voor Windows is vereist dat Hallo doel-virtuele machine is verbonden toohello internet. 

## <a name="extension-schema"></a>Uitbreidingsschema

Hallo toont volgende JSON Hallo-schema voor de aangepaste Scriptextensie Hallo. Hallo-uitbreiding vereist de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht tooexecute. Een Azure storage-account en -account sleutel is vereist als voor informatie over het gebruik van Azure Storage als Hallo van de scriptbron. Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in configuratie van de beveiligde instelling Hallo-extensies. Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Eigenschapswaarden

| Naam | Waarde / voorbeeld |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Uitgever | Microsoft.Compute |
| type | Uitbreidingen |
| typeHandlerVersion | 1.9 |
| fileUris (bijvoorbeeld) | https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1 |
| commandToExecute (bijvoorbeeld) | PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1 |
| storageAccountName (bijvoorbeeld) | examplestorageacct |
| storageAccountKey (bijvoorbeeld) | TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg == |

**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig. Hallo namen gebruiken zoals hierboven tooavoid implementatieproblemen.

## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo aangepaste Scriptextensie tijdens de sjabloonimplementatie van een Azure Resource Manager. Een voorbeeldsjabloon waarin de aangepaste Scriptextensie u hier vindt, Hallo [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>PowerShell-implementatie

Hallo `Set-AzureRmVMCustomScriptExtension` opdracht gebruikte tooadd Hallo aangepast Script extensie tooan bestaande virtuele machine kan worden. Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Oplossen van problemen en ondersteunen

### <a name="troubleshoot"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module. Hallo Implementatiestatus toosee van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uitvoering van de extensie uitvoer geregistreerde toofiles gevonden onder Hallo volgt directory op Hallo doel-virtuele machine.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Hallo opgegeven bestanden zijn gedownload naar de volgende map op de virtuele doelmachine Hallo Hallo.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
waar `<n>` is een decimal integer die kan worden gewijzigd tussen uitvoeringen van Hallo-uitbreiding.  Hallo `1.*` waarde overeenkomt met de werkelijke, huidige Hallo `typeHandlerVersion` waarde van de Hallo-uitbreiding.  Hallo werkelijke directory kan bijvoorbeeld `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Bij het uitvoeren van Hallo `commandToExecute` opdracht Hallo extensie deze map hebt ingesteld (bijvoorbeeld `...\Downloads\2`) als de huidige werkmap Hallo. Dit kunnen Hallo-gebruik van relatieve paden toolocate Hallo bestanden gedownload via Hallo `fileURIs` eigenschap. Zie onderstaande Hallo tabel voor voorbeelden.

Omdat Hallo absolute downloadpad na verloop van tijd verschillen kan, is het beter tooopt voor relatieve scriptbestand paden in Hallo `commandToExecute` tekenreeks, indien mogelijk. Bijvoorbeeld:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Informatie over het pad na eerste Hallo-URI-segment wordt bewaard voor bestanden gedownload via Hallo `fileUris` eigenschappenlijst.  Zoals u in onderstaande tabel voor hello, gedownloade bestanden zijn toegewezen in downloaden submappen tooreflect Hallo structuur Hallo `fileUris` waarden.  

#### <a name="examples-of-downloaded-files"></a>Voorbeelden van gedownloade bestanden

| URI in fileUris | Relatieve locatie voor gedownloade | Absolute locatie gedownload * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Als verandert hierboven, Hallo absolute mappaden gedurende de levensduur Hallo Hallo VM, maar niet binnen één uitvoering van de extensie CustomScript Hallo.

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums] (https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
