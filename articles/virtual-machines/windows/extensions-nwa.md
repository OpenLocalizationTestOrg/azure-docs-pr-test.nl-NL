---
title: aaaAzure netwerk-Watcher-Agent de extensie van de virtuele machine voor Windows | Microsoft Docs
description: Hallo netwerk-Watcher-Agent op de Windows virtuele machine met de extensie van een virtuele machine implementeren.
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>De extensie van de virtuele machine Watcher-Agent voor Windows-netwerk

## <a name="overview"></a>Overzicht

[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken. Hallo-extensie van de virtuele machine netwerk-Watcher-Agent is een vereiste voor een aantal functies van de netwerk-Watcher Hallo op virtuele machines in Azure. Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.

Dit document details Hallo ondersteund platforms en implementatie-opties voor Hallo extensie van de virtuele machine netwerk-Watcher-Agent voor Windows.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem

Hallo uitbreiding van de netwerk-Watcher-Agent versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016. Houd er rekening mee dat Hallo die nano Server wordt niet ondersteund op dit moment.

### <a name="internet-connectivity"></a>Internetconnectiviteit

Aantal Hallo Agent voor netwerk-Watcher-functionaliteit is vereist dat Hallo doel-virtuele machine verbonden toohello Internet. Zonder Hallo mogelijkheid tooestablish uitgaande verbindingen mogelijk enkele Hallo Network Watcher Agent functies niet goed of niet meer beschikbaar. Zie voor meer informatie Hallo [netwerk-Watcher documentatie](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Uitbreidingsschema

Hallo toont volgende JSON Hallo-schema voor Hallo Agent voor netwerk-Watcher-extensie. Hallo-uitbreiding geen van beide vereist, noch de gebruiker opgegeven instellingen op dit moment ondersteunt en is afhankelijk van de standaardconfiguratie.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Eigenschapswaarden

| Naam | Waarde / voorbeeld |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Uitgever | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo uitbreiding van de netwerk-Watcher Agent tijdens de sjabloonimplementatie van een Azure Resource Manager.

## <a name="powershell-deployment"></a>PowerShell-implementatie

Hallo `Set-AzureRmVMExtension` opdracht gebruikte toodeploy Hallo Network Watcher Agent virtuele machine extensie tooan bestaande virtuele machine kan worden.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Problemen oplossen en ondersteuning

### <a name="troubleshooting"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module. Implementatiestatus van toosee Hallo van uitbreidingen voor een opgegeven virtuele machine, Voer Hallo na gebruik van de opdracht hello Azure PowerShell-module.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u verwijzen toohello gebruikershandleiding voor netwerk-Watcher-documentatie of neem contact op met hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
