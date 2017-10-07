---
title: aaaHandling gebeurtenis volgorde en lateness met Azure Stream Analytics | Microsoft Docs
description: Meer informatie over de werking van Stream Analytics met out volgorde of laat gebeurtenissen in gegevensstromen.
keywords: volgorde, laat, gebeurtenissen
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure Stream Analytics volgorde gebeurtenisverwerking

In een tijdelijke gegevensstroom van gebeurtenissen, elke gebeurtenis wordt geregistreerd met Hallo tijd die Hallo-gebeurtenis is ontvangen. Een aantal voorwaarden kunnen gebeurtenisstromen ontvangt toooccasionally sommige gebeurtenissen veroorzaken in een andere volgorde dan waarop ze zijn verzonden. Een eenvoudige TCP opnieuw, of zelfs een tijdverschil tussen Hallo verzenden van apparaat- en Hallo event hub ontvangt deze toooccur kan veroorzaken. 'Leestekens' gebeurtenissen ook tooreceived gebeurtenisstromen, zijn toegevoegd tooadvance Hallo tijd in Hallo afwezigheid van gebeurtenis ontvangsten. Deze zijn nodig in scenario's zoals "Waarschuw mij een e-mail wanneer geen aanmeldingen uitgevoerd voor de 3 minuten."

Invoer stromen die zich niet in volgorde zijn:
* Gesorteerd (en dus **vertraagd**).
* Aangepast door Hallo-systeem, op basis van tooa gebruiker opgegeven beleid.


## <a name="lateness-tolerance"></a>Lateness tolerantie
Stream Analytics maximaal dit soort scenario's wordt toegestaan. Stream Analytics heeft de verwerking van gebeurtenissen 'out volgorde' en 'late'. Deze gebeurtenissen in de volgende manieren Hallo verwerkt:

* Gebeurtenissen die een andere volgorde ontvangen, maar in Hallo instellen tolerantie zijn **opnieuw geordend door tijdstempel**.
* Gebeurtenissen die hoger is dan de tolerantie binnenkomen zijn **verwijderd of aangepast**.
    * **Aangepast**: aangepaste tooappear toohave ontvangen op Hallo laatste acceptabele tijd.
    * **Verwijderd**: verwijderd.

![Stream Analytics gebeurtenisverwerking](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Verminder het aantal out volgorde gebeurtenissen Hallo

Omdat de Stream Analytics is een tijdelijke transformatie van toepassing bij de verwerking van inkomende gebeurtenissen (bijvoorbeeld voor functies in vensters of tijdelijke joins), worden binnenkomende gebeurtenissen in Stream Analytics gesorteerd op volgorde timestamp.

Wanneer Hallo 'tijdstempel door'-sleutelwoord is **niet** gebruikt, hello Azure Event Hubs in de wachtrij plaatsen gebeurtenistijd wordt standaard gebruikt. Event Hubs wordt gegarandeerd dat monotonicity van Hallo tijdstempel op elke partitie van Hallo event hub. Ook wordt hiermee gegarandeerd dat gebeurtenissen van alle partities in volgorde van de timestamp worden samengevoegd. Deze twee Event Hubs garanties Zorg ervoor dat er geen gebeurtenissen out volgorde.

Soms is het belangrijk voor u toouse Hallo afzender timestamp. In dat geval is een tijdstempel van Hallo nettolading gekozen met behulp van 'tijdstempel door'. In deze scenario's mogelijk zijn een of meer bronnen van de gebeurtenis misorder worden geïntroduceerd:

* Gebeurtenis producenten hebben klok laat. Dit is gebruikelijk producenten afkomstig zijn van verschillende computers werkt, zodat ze verschillende klokken hebben.
* Er is een vertraging in het netwerk van de bron Hallo van Hallo gebeurtenissen toohello bestemming event hub.
* Klok laat bestaan tussen event hub-partities. Gebeurtenissen van alle partities van de event hub stream Analytics eerst worden gesorteerd gebeurtenistijd in de wachtrij plaatsen. Vervolgens wordt de gegevensstroom Hallo voor misordered gebeurtenissen gecontroleerd.

Op tabblad configuratie hello ziet u Hallo standaardwaarden te volgen:

![Stream Analytics out volgorde verwerking](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Als u 0 seconden als Hallo out volgorde tolerantieperiode instellen, bent u aantonen dat alle gebeurtenissen volgorde alle Hallo tijd zijn. Hallo drie bronnen van misordered gebeurtenissen opgegeven, is het onwaarschijnlijk dat dit geldt. 

een gebeurtenis misorder tooallow Stream Analytics toocorrect, kunt u een tolerantieperiode voor niet-nul out volgorde opgeven. Stream Analytics buffers gebeurtenissen toothat venster en bestellingen die ze met behulp van Hallo tijdstempel die u hebt gekozen. Vervolgens Hallo tijdelijke transformatie wordt toegepast. U kunt beginnen met een venster 3 seconden en Hallo waarde tooreduce Hallo aantal gebeurtenissen die tijd aangepast zijn afstemmen. 

Een neveneffect van Hallo bufferfunctie is dat Hallo uitvoer **vertraging Hallo dezelfde hoeveelheid tijd**. U kunt stemmen Hallo waarde tooreduce Hallo aantal out volgorde gebeurtenissen en houd Hallo taak latentie laag.

## <a name="get-help"></a>Help opvragen
Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooStream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor stream Analytics query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)