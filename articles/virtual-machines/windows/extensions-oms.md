---
title: aaaOMS uitbreiding van de virtuele machine van Azure voor Windows | Microsoft Docs
description: Hallo OMS-agent op de Windows virtuele machine met de extensie van een virtuele machine implementeren.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>OMS de extensie van de virtuele machine voor Windows

Operations Management Suite (OMS) biedt mogelijkheden voor bewaking, waarschuwingen en waarschuwing herstel tussen cloud en on-premises activa. Hallo OMS-Agent de extensie van de virtuele machine voor Windows is gepubliceerd en ondersteund door Microsoft. Hallo-extensie Hallo OMS-agent is geïnstalleerd op virtuele machines in Azure en virtuele machines in een bestaande OMS-werkruimte inschrijft. Dit document details Hallo ondersteund platforms, configuraties en implementatie-opties voor Hallo extensie OMS-virtuele machine voor Windows.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem
Hallo-extensie OMS-Agent versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.

### <a name="internet-connectivity"></a>Internetconnectiviteit
uitbreiding van de OMS-Agent voor Windows Hello is vereist dat Hallo doel-virtuele machine is verbonden toohello internet. 

## <a name="extension-schema"></a>Uitbreidingsschema

Hallo toont volgende JSON Hallo-schema voor Hallo OMS-Agent-extensie. Hallo-uitbreiding vereist Hallo werkruimte-Id en werkruimte sleutel uit Hallo doel OMS-werkruimte, deze vindt u in Hallo OMS-portal. Omdat Hallo werkruimtesleutel moet worden behandeld als gevoelige gegevens, moet deze worden opgeslagen in de configuratie van een beveiligde instelling. Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld. Houd er rekening mee dat **workspaceId** en **workspaceKey** zijn hoofdlettergevoelig.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Eigenschapswaarden

| Naam | Waarde / voorbeeld |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Uitgever | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (bijvoorbeeld) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (bijvoorbeeld) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |

## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo OMS-Agent extensie tijdens de sjabloonimplementatie van een Azure Resource Manager. Een voorbeeldsjabloon met Hallo OMS-Agent VM-extensie vindt u op Hallo [galerie van Azure Quick Start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Hallo JSON voor de extensie van een virtuele machine worden genest in de bron van de virtuele machine Hallo of geplaatst op Hallo bovenste niveau van een Resource Manager JSON-sjabloon. Hallo plaatsing van Hallo JSON is van invloed op Hallo-waarde van Hallo resourcenaam en het type. Zie voor meer informatie [naam en type voor de onderliggende resources instellen](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hallo volgende voorbeeld wordt ervan uitgegaan Hallo OMS-extensie is genest binnen de bron van de virtuele machine Hallo. Wanneer het nesten van Hallo extensie resource Hallo JSON wordt geplaatst in Hallo `"resources": []` object van het Hallo virtuele machine.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Bij het plaatsen van Hallo extensie JSON aan Hallo basis van sjabloon hello, Hallo Resourcenaam bevat een verwijzing toohello bovenliggende virtuele machine en Hallo type reflecteert Hallo geneste configuratie. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>PowerShell-implementatie

Hallo `Set-AzureRmVMExtension` opdracht gebruikte toodeploy Hallo OMS-Agent virtuele machine extensie tooan bestaande virtuele machine kan worden. Voordat u Hallo-opdracht, moeten de openbare en persoonlijke configuraties Hallo toobe opgeslagen in een PowerShell-hash-tabel. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Oplossen van problemen en ondersteunen

### <a name="troubleshoot"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module. Implementatiestatus van toosee Hallo van uitbreidingen voor een opgegeven virtuele machine, Voer Hallo na gebruik van de opdracht hello Azure PowerShell-module.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
