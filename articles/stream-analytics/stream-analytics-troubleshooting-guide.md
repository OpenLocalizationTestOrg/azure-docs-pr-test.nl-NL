---
title: aaaTroubleshooting-handleiding voor Azure Stream Analytics | Microsoft Docs
description: Hoe tootroubleshoot uw Stream Analytics-taak
keywords: problemen met de gids
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
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Gids voor probleemoplossing voor Azure Stream Analytics

Kan het oplossen van Azure Stream Analytics worden toobe een zeer complexe taak op het eerste gezicht weergegeven. Nadat u werkt met veel gebruikers, we deze handleiding toohelp stroomlijnen Hallo proces hebt gemaakt en Hallo vermijden over uw invoer, uitvoer, query's en functies verwijderen.

## <a name="troubleshoot-your-stream-analytics-job"></a>Problemen met uw Stream Analytics-taak oplossen

Gebruik voor de beste resultaten bij het oplossen van uw Stream Analytics-taak Hallo richtlijnen te volgen:

1.  Test de verbinding in orde:
    - Connectiviteit tooinputs en uitgangen controleren met behulp van Hallo **testverbinding** knop voor elk invoer en uitvoer.

2.  Controleer uw invoer gegevens:
    - tooverify die invoergegevens stroomt in Event Hub, gebruikt u [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Event Hub (als invoer van de Event Hub wordt gebruikt).  
    - Gebruik Hallo [ **voorbeeldgegevens** ](stream-analytics-sample-data-input.md) knop voor elke invoer en download de voorbeeldgegevens van Hallo invoer.
    - Hallo sample data toounderstand Hallo vorm van Hallo gegevens controleren: schema- en Hallo Hallo [gegevenstypen](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  De query testen:
    - Op Hallo **Query** tabblad, gebruikt u Hallo **testen** knop tootest Hallo query en Hallo gedownload voorbeeldgegevens te gebruiken[Hallo-testquery](stream-analytics-test-query.md). Bekijk eventuele fouten en toocorrect probeert ze.
    - Als u [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), Controleer of Hallo gebeurtenissen hebt tijdstempels groter is dan Hallo [begintijd taak](stream-analytics-out-of-order-and-late-events.md).

4.  Fouten opsporen in uw query:
    - Hallo query geleidelijk van complexe statistische functies eenvoudige select-instructie toomore bouwen met behulp van stappen. Gebruik toobuild up Hallo query logica stap voor stap [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) componenten.
    - Gebruik [SELECT INTO](stream-analytics-select-into.md) toodebug querystappen.

5.  Elimineren verrassingen, zoals:
    - Een [ **waar** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) -component in Hallo query uitgefilterd alle gebeurtenissen, zo wordt voorkomen dat eventuele uitvoer wordt gegenereerd.
    - Wanneer u vensterfuncties gebruikt, wacht u totdat Hallo hele venster duur toosee uitvoer van Hallo-query.
    - Hallo tijdstempel voor gebeurtenissen vóór de begintijd Hallo en daarom gebeurtenissen worden verwijderd.

6.  Gebruik ordening van gebeurtenis:
    - Als alle voorgaande stappen prima hello, gaat u toohello **instellingen** blade en selecteer [ **gebeurtenis ordening**](stream-analytics-out-of-order-and-late-events.md). Controleren of dit beleid is geconfigureerd voor wat zinvol in uw scenario. Hallo-beleid is *niet* toegepast wanneer u Hallo **Test** knop tootest Hallo query. Dit resultaat is een verschil tussen het in de browser versus Hallo-taak uitgevoerd in productie testen.

7.  Fouten opsporen in met behulp van de metrische gegevens:
    - Als u krijgt geen uitvoer na Hallo duur verwachte (gebaseerd op Hallo query), probeert u Hallo volgende:
        - Bekijk [ **bewaking metrische gegevens** ](stream-analytics-monitoring.md) op Hallo **Monitor** tabblad. Omdat het Hallo-waarden worden samengevoegd, zijn een paar minuten Hallo metrische gegevens uitgesteld.
            - Als invoervelden > 0, Hallo-taak wordt kunnen tooread invoergegevens. Als invoer gebeurtenissen niet > 0, klikt u vervolgens:
                - toosee of gegevensbron Hallo geldige gegevens heeft deze controleren met behulp van [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Deze controle van toepassing als Hallo taak Event Hub als invoer.
                - Controleer toosee of Hallo gegevens serialisatie-indeling en gegevens codering zijn zoals verwacht.
                - Als Hallo-taak van een Event Hub gebruikmaakt, toosee controleren of het Hallo-hoofdtekst van het Hallo-bericht is *Null*.
            - Als gegevens conversiefouten > 0 en moeten klimmen, mogelijk Hallo volgende waar zijn:
                - Hallo taak mogelijk niet kunnen toode-Hallo gebeurtenissen serialiseren.
                - Hallo gebeurtenis schema mogelijk niet overeen met Hallo gedefinieerd of het verwachte schema van Hallo-gebeurtenissen in het Hallo-query.
                - gegevenstypen van een aantal velden in de gebeurtenis Hallo HALLO hallo mogelijk niet overeen met de verwachtingen.
            - Als runtimefouten > 0, betekent dit dat taak Hallo Hallo gegevens kan ontvangen maar fouten tijdens het verwerken van query Hallo genereert.
                - toofind hello fouten, gaat u toohello [controlelogboeken](../azure-resource-manager/resource-group-audit.md) en filtert u op *mislukt* status.
            - Als InputEvents > 0 en OutputEvents = 0, betekent dit een van de volgende Hallo is ingesteld op true:
                - Het verwerken van de query heeft geen uitvoergebeurtenissen opgeleverd.
                - Het is mogelijk dat gebeurtenissen of de velden ongeldig is, resulteert in nul uitvoer nadat de verwerking van query's.
                - Hallo-taak is toopush gegevens toohello [uitvoerlocatie](stream-analytics-select-into.md) omwille van de netwerkverbinding of de verificatie.
        - In alle Hallo eerder genoemde foutgevallen operations logboekberichten uitgelegd aanvullende gegevens (inclusief wat er gebeurt), behalve in gevallen waarbij Hallo query logica alle gebeurtenissen gefilterd. Als Hallo verwerking van meerdere gebeurtenissen fouten genereert, wordt de Stream Analytics logboeken Hallo eerste drie foutberichten van hetzelfde type binnen 10 minuten tooOperations Hallo registreert. Vervolgens onderdrukt extra identiek fouten met een bericht dat wordt gelezen "Fouten plaatsvinden te snel dat deze worden onderdrukt."

8. Fouten opsporen in met behulp van controle en diagnostische logboeken:
    - Gebruik [controlelogboeken](../azure-resource-manager/resource-group-audit.md), en filter tooidentify en foutopsporing fouten.
    - Gebruik [taak diagnostische logboeken](stream-analytics-job-diagnostic-logs.md) tooidentify en foutopsporing fouten.

9. Bekijk Hallo uitvoer:
    - Wanneer de status van de taak Hallo is *met*, afhankelijk van de duur op Hallo die worden bepaald in Hallo query, ziet u uitvoer Hallo in Hallo sink-gegevensbron.
    - Als u uitvoer die u de specifieke uitvoertype tooa niet ziet, hen omleidt tooan uitvoertype die minder complex is, zoals een Azure-Blob. Controleer met behulp van Storage Explorer toosee of Hallo uitvoer kan worden weergegeven. Controleer bovendien of bandbreedteregeling limieten op Hallo uitvoer worden voorkomen dat gegevens worden ontvangen.

10. Gegevensoverdracht analyse met taak diagram metrische gegevens gebruiken:
    - tooanalyze gegevens stromen en identificeren van problemen, gebruik Hallo [taak diagram met metrische gegevens](stream-analytics-job-diagram-with-metrics.md).

11. Open een ondersteuningsaanvraag:
    - Ten slotte, als alle anders mislukt, open een Microsoft-ondersteuningsaanvraag met Hallo abonnements-id met de taak.

## <a name="get-help"></a>Help opvragen

Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
