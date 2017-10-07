---
title: Netwerk-Watcher-Agent de extensie van de virtuele machine voor Linux aaaAzure | Microsoft Docs
description: Hallo netwerk-Watcher-Agent op Linux virtuele machine met de extensie van een virtuele machine implementeren.
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>De extensie van de virtuele machine Watcher-Agent voor Linux-netwerk

## <a name="overview"></a>Overzicht

[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken. Hallo-extensie van de virtuele machine netwerk-Watcher-Agent is een vereiste voor een aantal functies van de netwerk-Watcher Hallo op virtuele machines in Azure. Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.

Dit document details Hallo ondersteund platforms en implementatie-opties voor Hallo extensie van de virtuele machine netwerk-Watcher-Agent voor Linux.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem

Hallo uitbreiding van de netwerk-Watcher-Agent kan worden uitgevoerd op basis van deze Linux-distributies:

| Distributie | Versie |
|---|---|
| Ubuntu | 16.04 TNS, 14.04 TNS en 12.04 TNS |
| Debian | 7 en 8 |
| RedHat | 6.x en 7.x |
| Oracle Linux | 7 x |
| SUSE | 11 en 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Houd er rekening mee dat virtuele CoreOS op dit moment niet wordt ondersteund.

### <a name="internet-connectivity"></a>Internetconnectiviteit

Aantal Hallo Agent voor netwerk-Watcher-functionaliteit is vereist dat Hallo doel-virtuele machine verbonden toohello Internet. Zonder Hallo mogelijkheid tooestablish uitgaande verbindingen mogelijk enkele Hallo Network Watcher Agent functies niet goed of niet meer beschikbaar. Zie voor meer informatie Hallo [netwerk-Watcher documentatie](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo uitbreiding van de netwerk-Watcher Agent tijdens de sjabloonimplementatie van een Azure Resource Manager.

## <a name="azure-cli-deployment"></a>Azure CLI-implementatie

Hello Azure CLI mag gebruikte toodeploy Hallo netwerk-Watcher Agent VM-extensie tooan bestaande virtuele machine.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Problemen oplossen en ondersteuning

### <a name="troubleshooting"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure CLI. Implementatiestatus van toosee Hallo van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren hello Azure CLI.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u verwijzen toohello netwerk-Watcher-documentatie of neem contact op met hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
