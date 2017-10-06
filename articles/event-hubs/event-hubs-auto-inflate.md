---
title: aaaAutomatically opschaling van Azure Event Hubs doorvoereenheden | Microsoft Docs
description: Automatisch vergroten inschakelen op een schaal van de naamruimte tooautomatically doorvoer-eenheden
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Automatisch opschalen doorvoereenheden Azure Event Hubs

## <a name="overview"></a>Overzicht

Azure Event Hubs is een uiterst schaalbare gegevens streaming-platform. Event Hubs klanten verhogen als zodanig vaak hun gebruik na onboarding toohello service. Dergelijke toeneemt vereisen toenemende Hallo zoekgedrag doorvoer eenheden (tabel) tooscale Event Hubs en grotere overdrachtssnelheid afhandelen. Hallo *automatisch vergroten* functie van Event Hubs schaalt automatisch een Hallo aantal meer toomeet gebruik behoeften. Verhogen van de tabel voorkomt dat scenario's waarin beperking:

* Meer instellen gegevens inkomend tarieven overschrijden
* Uitgaande gegevensaanvraag tarieven overschrijden meer instellen.

## <a name="how-auto-inflate-works"></a>Hoe automatisch vergroten werkt

Event Hubs-verkeer wordt geregeld door doorvoereenheden. Een enkele TU kunt 1 MB per seconde van inkomende en twee keer de omvang van uitgaande gegevens. Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden. Automatisch vergroten, kunt u toostart kleine met Hallo minimale vereiste doorvoereenheden. Hallo functie vervolgens schaalt automatisch toohello maximumlimiet van doorvoereenheden die u nodig hebt, afhankelijk van Hallo toename van het verkeer. Automatisch vergroten biedt Hallo volgende voordelen:

- Een efficiënte vergroten/verkleinen mechanisme toostart klein en schaal omhoog als u groeien.
- Automatisch schalen toohello opgegeven bovengrens zonder bandbreedteregeling problemen.
- Meer controle over schalen, als u wanneer bepaalt en hoeveel tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Een naamruimte inschakelen automatisch vergroten

U kunt in- of uitschakelen van automatische vergroten voor een naamruimte met een van de volgende methoden Hallo:

1. Hallo [Azure-portal](https://portal.azure.com).
2. Een Azure Resource Manager-sjabloon.

### <a name="enable-auto-inflate-through-hello-portal"></a>Automatisch vergroten inschakelen via de portal Hallo

Bij het maken van een naamruimte Event Hubs, kunt u automatisch vergroten Hallo-functie op een naamruimte inschakelen:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Met deze optie is ingeschakeld, kunt u begin klein op uw doorvoereenheden en schaal omhoog wanneer gebruik van uw toename behoeften. Hallo bovengrens voor inflatie heeft geen invloed op prijzen die afhankelijk is Hallo aantal meer per uur gebruikt.

U kunt ook inschakelen automatisch vergroten met Hallo **Scale** optie op de blade van Hallo-instellingen in Hallo-portal:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Schakel automatisch vergroten met een Azure Resource Manager-sjabloon

U kunt automatisch vergroten inschakelen tijdens de sjabloonimplementatie van een Azure Resource Manager. Bijvoorbeeld: set Hallo `isAutoInflateEnabled` eigenschap te**true** en stel `maximumThroughputUnits` too10.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Zie voor de volledige sjabloon hello, Hallo [maken Event Hubs-naamruimte en schakel vergroten](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) sjabloon op GitHub.

## <a name="next-steps"></a>Volgende stappen

U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
