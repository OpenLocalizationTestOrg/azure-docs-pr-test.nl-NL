---
title: aaaStateful Reliable Services diagnostics | Microsoft Docs
description: Diagnosefunctionaliteit voor Stateful Reliable Services
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Diagnosefunctionaliteit voor Stateful Reliable Services
Hallo Stateful betrouwbare Services StatefulServiceBase klasse verzendt [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gebeurtenissen die gebruikt toodebug worden kunnen Hallo service, biedt mogelijk inzicht in hoe Hallo runtime is functioneren en oplossen van problemen met.

## <a name="eventsource-events"></a>EventSource gebeurtenissen
Hallo EventSource naam voor Hallo Stateful betrouwbare Services StatefulServiceBase klasse is 'Microsoft-ServiceFabric-Services'. Gebeurtenissen van de bron van deze gebeurtenissen worden weergegeven in de [diagnostische gebeurtenissen](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) venster wanneer Hallo-service wordt [fouten worden opgespoord in Visual Studio](service-fabric-debugging-your-application.md).

Voorbeelden van hulpprogramma's en -technologieën die helpen bij het verzamelen en/of het bekijken van EventSource gebeurtenissen zijn [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md), en de [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Gebeurtenissen
| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Beschrijving van gebeurtenis |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informatief |Verzonden wanneer service RunAsync-taak wordt gestart |
| StatefulRunAsyncCancellation |2 |Informatief |Wanneer het service RunAsync-taak is geannuleerd |
| StatefulRunAsyncCompletion |3 |Informatief |Verzonden als de service RunAsync-taak is voltooid |
| StatefulRunAsyncSlowCancellation |4 |Waarschuwing |Wanneer service RunAsync taak te lang toocomplete annulering duurt verzonden |
| StatefulRunAsyncFailure |5 |Fout |Wanneer service RunAsync taak een uitzondering wordt verzonden |

## <a name="interpret-events"></a>Gebeurtenissen interpreteren
StatefulRunAsyncInvocation StatefulRunAsyncCompletion en StatefulRunAsyncCancellation gebeurtenissen zijn nuttig toohello service writer toounderstand Hallo levenscyclus van een service--evenals Hallo timing voor wanneer een service is gestart, geannuleerd of voltooid . Dit kan nuttig zijn bij het opsporen van problemen met de service of understanding Hallo service lifecycle.

Schrijvers van de service moeten letten tooStatefulRunAsyncSlowCancellation en StatefulRunAsyncFailure gebeurtenissen betalen omdat ze wijzen op problemen met de Hallo-service.

StatefulRunAsyncFailure wordt verzonden wanneer het Hallo-servicetaak RunAsync() er een uitzondering gegenereerd. Een uitzondering veroorzaakt geeft meestal aan een fout of een bug in Hallo-service. Hallo uitzondering veroorzaakt bovendien Hallo service toofail, dus is het ander knooppunt verplaatst tooa. Dit kan een dure bewerking en het binnenkomende aanvragen kan worden vertraagd terwijl Hallo-service wordt verplaatst. Schrijvers van de service moeten Hallo oorzaak van de uitzondering Hallo en deze indien mogelijk te beperken.

StatefulRunAsyncSlowCancellation wordt verzonden wanneer een annuleringsaanvraag voor Hallo RunAsync taak langer dan vier seconden duurt. Wanneer een service te lang toocomplete annulering duurt, heeft dit gevolgen voor Hallo mogelijkheid voor Hallo service toobe snel opnieuw gestart op een ander knooppunt. Dit mogelijk van invloed op Hallo van algemene beschikbaarheid van Hallo-service.

## <a name="next-steps"></a>Volgende stappen
* [EventSource providers op PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
