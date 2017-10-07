---
title: aaaBest procedures voor Azure Functions | Microsoft Docs
description: Informatie over aanbevolen procedures en patronen voor Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure functions, patronen, best practices, functies, gebeurtenisverwerking webhooks, dynamische compute, zonder server-architectuur
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Hallo prestaties en betrouwbaarheid van Azure Functions optimaliseren

Dit artikel bevat richtlijnen tooimprove Hallo prestaties en betrouwbaarheid van uw apps functie. 


## <a name="avoid-long-running-functions"></a>Vermijd langlopende functies

Grote, langlopende functies kunnen onverwachte time-out problemen veroorzaken. Een functie kan worden grote vanwege toomany Node.js-afhankelijkheden. Afhankelijkheden importeren kan ook leiden tot verhoogde laadtijden die tot onverwachte time-outs leiden. Afhankelijkheden zijn beide expliciet en impliciet geladen. Een enkele module geladen door uw code kan zijn eigen aanvullende modules worden geladen.  

Indien mogelijk wordt Verander grote functies in kleinere functie ingesteld die werken samen en snel antwoorden retourneren. Bijvoorbeeld, een webhook of HTTP-trigger functie mogelijk een bevestiging van de reactie binnen een bepaalde tijd; het is gebruikelijk voor webhooks toorequire direct een reactie. U kunt Hallo HTTP-trigger nettolading doorgeven in een wachtrij toobe verwerkt door een functie van de trigger wachtrij. Deze aanpak kunt u toodefer Hallo echte werk en direct een reactie terug.


## <a name="cross-function-communication"></a>Cross-functie communicatie

Bij het integreren van meerdere functies, maar het is doorgaans een best practice toouse opslagwachtrijen voor cross-functie communicatie.  de belangrijkste reden Hallo is opslagwachtrijen zijn goedkoper en veel eenvoudiger tooprovision. 

Afzonderlijke berichten in een opslagwachtrij zijn beperkt in grootte too64 KB. Als u nodig hebt toopass grotere berichten tussen de functies, kan een Azure Service Bus-wachtrij gebruikte toosupport berichtgrootten up too256 KB zijn.

Service Bus-onderwerpen zijn handig als u nodig hebt bericht filteren voordat ze worden verwerkt.

Event hubs zijn nuttig toosupport hoog volume communicatie.


## <a name="write-functions-toobe-stateless"></a>Schrijven van functies toobe staatloze 

Functies moet staatloze en idempotent indien mogelijk. Eventuele vereiste statusgegevens koppelen aan uw gegevens. Bijvoorbeeld, een bestelling wordt verwerkt waarschijnlijk heeft een bijbehorende `state` lid. Een functie kan een volgorde die op basis van die status terwijl Hallo functie zelf staatloze blijft verwerken. 

De Idempotent-functies zijn vooral aanbevolen met timer triggers. Bijvoorbeeld, als er iets dat absoluut moet één keer per dag worden uitgevoerd, schrijven zodat deze tijdens Hallo dag Hello dezelfde resultaten uitvoeren kunt. Hallo-functie kunt afsluiten wanneer er geen werk voor een bepaalde dag. Ook als een eerder uitgevoerde is mislukt toocomplete, Hallo een volgende keer uitvoert moet kunnen worden opgepikt waar deze gebleven was.


## <a name="write-defensive-functions"></a>Defensive functies schrijven

Stel dat uw-functie kan een uitzondering op elk gewenst moment optreden. Ontwerp dat uw functies met Hallo mogelijkheid toocontinue van een eerder punt mislukt tijdens het Hallo volgende uitvoering. Houd rekening met een scenario waarbij Hallo van de volgende activiteiten:

1. De query voor 10.000 rijen in een database.
2. Maak een wachtrijbericht voor elk van deze rijen tooprocess verdere Hallo regel omlaag.
 
Afhankelijk van hoe complexe uw systeem is, moet u wellicht: downstream betrokken services naar behoren werkt, netwerken uitval of quotum beperkt bereikt, enzovoort. Al deze waarden kunnen invloed hebben op de functie op elk gewenst moment. U moet uw functies toobe voorbereid voor het toodesign.

Hoe uw code reageren als er een fout optreedt nadat 5.000 van deze items in een wachtrij voor verwerking invoegen? Bijhouden van items in een verzameling die u hebt voltooid. Anders wordt u mogelijk plaats ze opnieuw zodra. Dit kan ernstige gevolgen hebben op uw werkstroom. 

Als een wachtrij-item al verwerkt is, kunt u de functie toobe geen.

Profiteren van beschermingsmaatregelen reeds wordt geboden voor onderdelen die u in hello Azure Functions-platform gebruiken. Zie bijvoorbeeld **verwerken van verontreinigde berichten** in de documentatie voor Hallo [Azure-Opslagwachtrij activeert](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Geen combinatie test en productie code in Hallo dezelfde functie-app

Functies binnen een functie-app bronnen delen. Bijvoorbeeld: geheugen wordt gedeeld. Als u een functie-app in productie, niet test-gerelateerde functies en bronnen tooit toevoegen. Tijdens de uitvoering van de productie-code kan dit leiden tot onverwachte overhead.

Zorg ervoor dat u in uw productie-functie apps laden. Geheugen wordt gemiddeld over elke functie in het Hallo-app.

Als u een gedeelde assembly waarnaar wordt verwezen in meerdere .net-functies hebt, kunt u deze in een gemeenschappelijke gedeelde map geplaatst. Verwijzing Hallo assembly met een instructie vergelijkbare toohello voorbeeld te volgen: 

    #r "..\Shared\MyAssembly.dll". 

Anders is het eenvoudig tooaccidentally implementeren meerdere testversies Hallo binaire die zich tussen anders gedragen fungeert.

Gebruik geen uitgebreide logboekregistratie in productiecode. Er is een negatief prestatieresultaat.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Asynchrone code gebruiken, maar geen aanroepen blokkeren

Asynchrone programmering is een aanbevolen procedure. Echter altijd voorkomen die verwijzen naar Hallo `Result` eigenschap of aanroepen `Wait` methode op een `Task` exemplaar. Deze aanpak kunt toothread uitputting leiden.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

Omdat Azure Functions maakt gebruik van Azure App Service, dient u zich bewust bent van App Service-richtlijnen.
* [Prestatieoptimalisaties patterns and practice HTTP](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

