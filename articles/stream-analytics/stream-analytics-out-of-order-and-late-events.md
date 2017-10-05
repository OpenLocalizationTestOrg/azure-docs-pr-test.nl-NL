---
title: Verwerken van gebeurtenis volgorde en lateness met Azure Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure Stream Analytics volgorde gebeurtenisverwerking

Elke gebeurtenis is vastgelegd in een tijdelijke gegevensstroom van gebeurtenissen met de tijd dat de gebeurtenis is ontvangen. Een aantal voorwaarden kunnen ertoe leiden dat gebeurtenisstromen ontvangt u af en sommige gebeurtenissen in een andere volgorde dan waarop ze zijn verzonden. Een eenvoudige TCP retransmit of zelfs een tijdsverschil tussen de verzendende apparaat en de ontvangende event hub kan mogelijk niet wilt dat dit gebeurt. 'Leestekens' gebeurtenissen worden ook toegevoegd aan de ontvangen gebeurtenisstromen om door te gaan van de tijd in het ontbreken van gebeurtenis ontvangsten. Deze zijn nodig in scenario's zoals "Waarschuw mij een e-mail wanneer geen aanmeldingen uitgevoerd voor de 3 minuten."

Invoer stromen die zich niet in volgorde zijn:
* Gesorteerd (en dus **vertraagd**).
* Aangepast door het systeem volgens een door de gebruiker opgegeven beleid.


## <a name="lateness-tolerance"></a>Lateness tolerantie
Stream Analytics maximaal dit soort scenario's wordt toegestaan. Stream Analytics heeft de verwerking van gebeurtenissen 'out volgorde' en 'late'. Deze gebeurtenissen worden verwerkt in de volgende manieren:

* Gebeurtenissen die volgorde maar binnen de tolerantie set binnenkomen zijn **opnieuw geordend door tijdstempel**.
* Gebeurtenissen die hoger is dan de tolerantie binnenkomen zijn **verwijderd of aangepast**.
    * **Aangepast**: aangepast, zodat deze lijkt te zijn ontvangen op de laatste toegestane tijd.
    * **Verwijderd**: verwijderd.

![Stream Analytics gebeurtenisverwerking](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a>Verminder het aantal out volgorde gebeurtenissen

Omdat de Stream Analytics is een tijdelijke transformatie van toepassing bij de verwerking van inkomende gebeurtenissen (bijvoorbeeld voor functies in vensters of tijdelijke joins), worden binnenkomende gebeurtenissen in Stream Analytics gesorteerd op volgorde timestamp.

Wanneer het sleutelwoord 'tijdstempel door' is **niet** gebruikt, wordt de wachtrij plaatsen van Azure Event Hubs gebeurtenistijd standaard gebruikt. Event Hubs wordt gegarandeerd dat monotonicity van de tijdstempel op elke partitie van de event hub. Ook wordt hiermee gegarandeerd dat gebeurtenissen van alle partities in volgorde van de timestamp worden samengevoegd. Deze twee Event Hubs garanties Zorg ervoor dat er geen gebeurtenissen out volgorde.

Soms is het belangrijk dat u gebruikt de timestamp van de afzender. In dat geval is een tijdstempel van de nettolading gekozen met behulp van 'tijdstempel door'. In deze scenario's mogelijk zijn een of meer bronnen van de gebeurtenis misorder worden geïntroduceerd:

* Gebeurtenis producenten hebben klok laat. Dit is gebruikelijk producenten afkomstig zijn van verschillende computers werkt, zodat ze verschillende klokken hebben.
* Er is een vertraging van de bron van de gebeurtenissen in het netwerk naar de bestemming event hub.
* Klok laat bestaan tussen event hub-partities. Gebeurtenissen van alle partities van de event hub stream Analytics eerst worden gesorteerd gebeurtenistijd in de wachtrij plaatsen. Vervolgens wordt de gegevensstroom voor misordered gebeurtenissen gecontroleerd.

Op het tabblad configuratie ziet u de volgende standaardinstellingen:

![Stream Analytics out volgorde verwerking](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Als u 0 seconden als in het venster out volgorde tolerantie gebruikt, bent u aantonen dat alle gebeurtenissen order voortdurend zijn. Gezien de drie bronnen van gebeurtenissen misordered, is het onwaarschijnlijk dat deze ingesteld op true is. 

Als Stream Analytics om op te lossen een gebeurtenis misorder zijn toegestaan, kunt u een tolerantieperiode voor niet-nul out volgorde opgeven. Stream Analytics buffert gebeurtenissen tot dit venster en worden ze met behulp van de tijdstempel die u hebt gekozen. Vervolgens wordt de tijdelijke transformatie die wordt toegepast. U kunt beginnen met een venster 3 seconden en de waarde van Verminder het aantal gebeurtenissen die tijd aangepast zijn afstemmen. 

Een neveneffect van de buffer is dat de uitvoer **vertraagd met dezelfde hoeveelheid tijd**. U kunt de waarde om te beperken het aantal out volgorde gebeurtenissen afstemmen en houd de taak latentie laag.

## <a name="get-help"></a>Help opvragen
Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tot Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor stream Analytics query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)