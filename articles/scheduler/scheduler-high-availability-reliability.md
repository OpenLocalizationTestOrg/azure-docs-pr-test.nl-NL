---
title: aaaScheduler hoge beschikbaarheid en betrouwbaarheid
description: Hoge beschikbaarheid en betrouwbaarheid
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Hoge beschikbaarheid en betrouwbaarheid
## <a name="azure-scheduler-high-availability"></a>Hoge beschikbaarheid met Azure Scheduler
Als een Azure-platform-service core Azure Scheduler is maximaal beschikbaar en functionaliteit voor zowel geografisch redundante service-implementatie en geo-landinstelling taak replicatie.

### <a name="geo-redundant-service-deployment"></a>Geografisch redundante service-implementatie
Azure Scheduler is beschikbaar via de gebruikersinterface in bijna elke geografische regio die deel uitmaakt van Azure vandaag Hallo. Hallo-lijst met regio's die beschikbaar is in Azure Scheduler is [hier vermeld](https://azure.microsoft.com/regions/#services). Als een datacentrum in een gehoste regio niet beschikbaar wordt weergegeven, zijn Hallo failover-mogelijkheden van Azure Scheduler zodat Hallo service beschikbaar vanuit een ander datacenter is.

### <a name="geo-regional-job-replication"></a>Geo-landinstelling taak replicatie
Niet alleen Hallo is Azure Scheduler front-end beschikbaar voor de management-aanvragen, maar uw eigen baan is ook geo-replicatie. Wanneer er een storing in een regio, wordt Azure Scheduler failover wordt uitgevoerd en garandeert dat die Hallo-taak wordt uitgevoerd vanaf een ander datacenter Hallo gekoppelde geografische regio.

Bijvoorbeeld, als u een taak hebt gemaakt in Zuid-centraal VS, repliceert Azure Scheduler automatisch deze taak in Noordelijk Centraal, VS. Wanneer er een fout in Zuid-centraal VS, Azure Scheduler zorgt ervoor dat Hallo-taak wordt uitgevoerd vanaf Noordelijk Centraal, VS. 

![][1]

Azure Scheduler als gevolg hiervan zorgt ervoor dat uw gegevens blijft binnen dezelfde breder geografische regio in geval van een Azure storing Hallo. Als gevolg hiervan moet u de taak alleen tooadd hoge beschikbaarheid dubbele – Azure Scheduler automatisch biedt mogelijkheden voor hoge beschikbaarheid voor uw taken.

## <a name="azure-scheduler-reliability"></a>Azure Scheduler-betrouwbaarheid
Azure Scheduler wordt gegarandeerd dat een eigen hoge beschikbaarheid en gaat een andere benadering taken toouser gemaakt. De taak kan bijvoorbeeld een HTTP-eindpunt is niet beschikbaar aanroepen. Azure Scheduler niettemin probeert tooexecute uw taak voltooid, doordat u alternatieve opties toodeal met fout. Azure Scheduler wordt dit op twee manieren:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Configureerbare beleid voor opnieuw proberen via "retryPolicy"
Azure Scheduler kunt u tooconfigure een beleid voor opnieuw proberen. Standaard, als een taak mislukt, probeert Scheduler Hallo taak opnieuw vier keer, met een interval van 30 seconden. U kunt deze opnieuw beleid toobe agressievere (bijvoorbeeld tien keer met een interval van 30 seconden) opnieuw configureren of lossere (bijvoorbeeld twee keer per dag intervallen.)

Als een voorbeeld van wanneer Hiermee kunt kunt u een taak die eenmaal per week wordt uitgevoerd en roept een HTTP-eindpunt maken. Als Hallo HTTP-eindpunt is niet toegankelijk wegens een paar uur wanneer de taak wordt uitgevoerd, kunt u niet toowait één meer week voor Hallo taak toorun opnieuw omdat zelfs Hallo standaardbeleid voor opnieuw proberen mislukken. In dergelijke gevallen kunt u mogelijk opnieuw configureren Hallo standaardproces voor nieuwe pogingen beleid tooretry elke drie uur (bijvoorbeeld) in plaats van elke 30 seconden.

hoe tooconfigure een beleid voor opnieuw proberen te verwijzen toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Alternatieve eindpunt configuratiemogelijkheden via "errorAction"
Als Hallo doel eindpunt voor uw Azure Scheduler-taak niet bereikbaar blijft, terugvalt Azure Scheduler alternatieve eindpunt voor foutafhandeling toohello nadat u het beleid voor opnieuw proberen. Als een alternatieve eindpunt voor foutafhandeling is geconfigureerd, wordt het door Azure Scheduler aanroept. Uw eigen taken zijn met een alternatieve eindpunt maximaal beschikbaar is in Hallo face van de fout.

Azure Scheduler volgt bijvoorbeeld in Hallo diagram hieronder, de nieuwe poging beleid toohit een New York-webservice. Nadat Hallo mislukken pogingen, wordt gecontroleerd of er een alternatief is. Vervolgens gaat het verder en wordt gestart die aanvragen indienen toohello alternatieve Hello dezelfde beleid voor opnieuw proberen.

![][2]

Let op Hallo van hetzelfde beleid voor opnieuw proberen is van toepassing tooboth Hallo oorspronkelijke actie en Hallo alternatieve fout. Het ook mogelijk toohave Hallo alternatieve fout van de actie actietype afwijken van actietype Hallo belangrijkste actie. Bijvoorbeeld, terwijl de belangrijkste actie Hallo van een HTTP-eindpunt aanroepen kan, Hallo foutbewerking in plaats daarvan mogelijk een opslagwachtrij-, service bus-wachtrij- of service bus-onderwerpactie die foutregistratie biedt.

hoe een eindpunt alternate tooconfigure te verwijzen toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler](scheduler-advanced-complexity.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
