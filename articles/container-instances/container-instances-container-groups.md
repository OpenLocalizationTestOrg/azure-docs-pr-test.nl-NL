---
title: aaaAzure Container exemplaren Containergroepen
description: Begrijpen hoe Containergroepen werken in Azure Containerexemplaren
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Containergroepen in Azure Containerexemplaren

Hallo op het hoogste niveau resource in Azure Containerexemplaren is een containergroep. Dit artikel wordt beschreven wat containergroepen zijn en wat voor soort scenario's die ze inschakelen.

## <a name="how-a-container-group-works"></a>De werking van een containergroep

Een containergroep is een verzameling van containers die ophalen gepland op Hallo dezelfde machine hosten en levenscyclus, lokale netwerk en opslagvolumes delen. Het is vergelijkbaar toohello concept van een *schil* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) en [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Hallo toont volgende diagram een voorbeeld van een containergroep met meerdere containers.

![Voorbeeld van de container-groepen][container-groups-example]

Opmerking:

- Hallo-groep is gepland op een machine één host.
- Hallo-groep wordt één openbaar IP-adres, met één blootgestelde poort.
- Hallo-groep bestaat uit twee containers. Een container luistert op poort 80, terwijl andere Hallo op poort 5000 luistert.
- Hallo-groep bevat twee Azure-bestandsshares als volume koppelingen en elke container koppelt een lokaal Hallo shares.

### <a name="networking"></a>Netwerken

Containergroepen delen een IP-adres en een poort-naamruimte op dat IP-adres. tooenable externe clients tooreach een container in de groep Hallo tonen Hallo-poort op Hallo IP-adres en uit Hallo-container op. Omdat containers in de groep Hallo een naamruimte poort delen, worden poorttoewijzing wordt niet ondersteund. Containers in een groep kunnen bereiken elkaar via localhost op Hallo poorten die ze beschikbaar zijn gesteld, zelfs als deze poorten niet extern worden weergegeven op Hallo van de groep IP-adres.

### <a name="storage"></a>Storage

U kunt externe volumes toomount binnen een containergroep opgeven. U kunt deze volumes toewijzen aan specifieke paden binnen Hallo afzonderlijke containers in een groep.

## <a name="common-scenarios"></a>Algemene scenario's

Meerdere container groepen zijn handig in gevallen waar u toodivide van een enkele functionele taak in een klein aantal installatiekopieën van de container, die kunnen worden geleverd door verschillende teams en afzonderlijke resourcevereisten hebben. Voorbeeld van syntaxis kan omvatten:

- Een toepassingscontainer en een container voor logboekregistratie. Hallo logboekregistratie container Hallo logboeken en uitvoer van de metrische gegevens verzamelt door de hoofdtoepassing Hallo en schrijft deze toolong-termijn opslag.
- Een toepassing en een controle container. Hallo container periodiek bewaking kunt u een aanvraag toohello toepassing tooensure dat het actief is en correct reageert en wordt een waarschuwing gegeven als dat niet.
- Een container voor een webtoepassing en een container binnenhalen van de meest recente inhoud Hallo vanuit resourcebeheer.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[implementeren van een groep met meerdere container](container-instances-multi-container-group.md) met een Azure Resource Manager-sjabloon.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png