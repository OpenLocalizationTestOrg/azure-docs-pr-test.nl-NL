---
title: aaaIntroduction tooflow logboekregistratie voor Netwerkbeveiligingsgroepen met Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toouse NSG stroom registreert voor een functie van Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen

Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep. Deze stroom logboeken zijn geschreven in json-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.

![Overzicht van de stroom-Logboeken][1]

Terwijl de stroom registreert Netwerkbeveiligingsgroepen doel, worden ze niet weergegeven Hallo dezelfde als Hallo andere logboeken. Stroom logboeken worden opgeslagen alleen binnen een opslagaccount en een pad naar de volgende Hallo logboekregistratie, zoals wordt weergegeven in het volgende voorbeeld Hallo:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hallo dezelfde bewaarbeleidsregels weergegeven op andere logboeken tooflow logboeken toegepast. Logboeken hebben een bewaarbeleid van 1 dag too365 dagen kan worden ingesteld. Als een bewaarbeleid niet is ingesteld, worden altijd Hallo logboeken gehandhaafd.

## <a name="log-file"></a>Logboekbestand

Stroom logboeken hebben meerdere eigenschappen. Hallo bevat volgende lijst een overzicht van Hallo-eigenschappen die worden geretourneerd in Hallo NSG stroom logboek in:

* **tijd** - bij het Hallo-gebeurtenis is vastgelegd
* **systeem-id** -Netwerkbeveiligingsgroep resource-id.
* **categorie** -Hallo categorie van de gebeurtenis hello, is dit altijd NetworkSecurityGroupFlowEvent zijn
* **ResourceID** -resource-Id van het NSG Hallo Hallo
* **operationName** -altijd NetworkSecurityGroupFlowEvents
* **eigenschappen** -een verzameling eigenschappen van Hallo stroom
    * **Versie** -versienummer van Hallo stromen logboek gebeurtenis schema
    * **stromen** -een verzameling van stromen. Deze eigenschap heeft meerdere vermeldingen voor verschillende regels
        * **regel** -regel voor welke Hallo stromen worden weergegeven
            * **stromen** -een verzameling van stromen
                * **Mac** -MAC-adres van Hallo NIC voor VM waar Hallo-stroom werd verzameld Hallo Hallo
                * **flowTuples** -een tekenreeks waarin meerdere eigenschappen voor Hallo stroom tuple in CSV-indeling
                    * **Tijdstempel** -deze waarde is Hallo tijdstempel wanneer het Hallo-stroom is opgetreden in de indeling van de UNIX-EPOCHE
                    * **Bron-IP** - hello bron-IP
                    * **Bestemming IP** -Hallo doel-IP
                    * **Bronpoort** - hello bronpoort
                    * **Doelpoort** -Hallo doelpoort
                    * **Protocol** -protocol van de stroom Hallo Hallo. Geldige waarden zijn **T** voor TCP- en **U** voor UDP
                    * **Verkeer van de stroom** -Hallo richting van het Hallo-netwerkverkeer. Geldige waarden zijn **ik** voor binnenkomend en **O** voor uitgaand.
                    * **Verkeer** - of verkeer is toegestaan of geweigerd. Geldige waarden zijn **A** voor toegestaan en **D** voor geweigerd.


Hallo Hieronder volgt een voorbeeld van een stroom-logboek. Zoals u er zijn meerdere records die Hallo eigenschappenlijst beschreven in voorgaande sectie Hallo volgen ziet. 

> [!NOTE]
> Waarden in de eigenschap flowTuples Hallo zijn een door komma's gescheiden lijst.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooenable stroom registreert in via [logboekregistratie inschakelen stromen](network-watcher-nsg-flow-logging-portal.md).

Meer informatie over NSG logboekregistratie in via [Meld analytics voor netwerkbeveiligingsgroepen (nsg's)](../virtual-network/virtual-network-nsg-manage-log.md).

Ontdek als verkeer wordt toegestaan of geweigerd op een virtuele machine in via [controleren verkeer met IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

