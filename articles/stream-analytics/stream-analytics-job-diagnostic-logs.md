---
title: Azure Stream Analytics aaaTroubleshoot met diagnostische logboeken | Microsoft Docs
description: Meer informatie over hoe diagnostische gegevens tooanalyze registreert van Stream Analytics jobs in Microsoft Azure.
keywords: 
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Azure Stream Analytics oplossen met behulp van logboeken met diagnostische gegevens

In sommige gevallen kan stopt een Azure Stream Analytics-taak onverwacht verwerking. Het is belangrijk toobe kunnen tootroubleshoot dit kind van gebeurtenis. Hallo-gebeurtenis kan worden veroorzaakt door een onverwachte queryresultaat met connectiviteit toodevices, of door een onverwachte. Hallo diagnostische logboeken in Stream Analytics kunt u identificeren Hallo oorzaak van problemen wanneer ze optreden, en de hersteltijd reduceren.

## <a name="log-types"></a>Logboek-typen

Stream Analytics biedt twee typen logboeken: 
* [Activiteitenlogboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (altijd ingeschakeld). Activiteitenlogboeken geven inzicht in de bewerkingen die worden uitgevoerd op taken.
* [Diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configureerbaar). Diagnostische logboeken bieden meer inzicht in alles wat er met een taak gebeurt. Diagnostische logboeken begin bij het Hallo-taak is gemaakt en einde wanneer Hallo-taak wordt verwijderd. Ze betrekking op gebeurtenissen wanneer Hallo-taak wordt bijgewerkt en terwijl deze wordt uitgevoerd.

> [!NOTE]
> U kunt services zoals Azure Storage, Azure Event Hubs en Azure-logboekanalyse tooanalyze standaardregels gegevens gebruiken. Er worden in rekening gebracht op basis van Hallo prijzen model voor deze services.
>

## <a name="turn-on-diagnostics-logs"></a>Logboeken met diagnostische gegevens inschakelen

Diagnostische logboeken zijn **uit** standaard. tooturn van diagnostische logboeken, voer deze stappen uit:

1.  Meld u bij toohello Azure-portal en gaat toohello streaming-taakblade. Onder **bewaking**, selecteer **diagnostische logboeken**.

    ![Blade navigatie toodiagnostics Logboeken](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Selecteer **diagnostische gegevens inschakelen**.

    ![Logboeken met diagnostische gegevens inschakelen](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Op Hallo **diagnostische instellingen** pagina voor **Status**, selecteer **op**.

    ![Status van diagnostische logboeken wijzigen](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Hallo archivering doel (storage-account, event hub, logboekanalyse) dat u wilt instellen. Selecteer vervolgens Hallo categorieën van logboeken die u wilt dat toocollect (uitvoering, ontwerpen). 

5.  Hallo nieuwe diagnostische configuratie op te slaan.

Hallo diagnostische configuratie van kracht ongeveer 10 minuten tootake. Daarna Hallo logboeken start verschijnen in Hallo geconfigureerd archivering doel (ziet u deze op Hallo **diagnostische logboeken** pagina):

![Blade navigatie toodiagnostics logs - archivering doelen](./media/stream-analytics-job-diagnostic-logs/image4.png)

Zie voor meer informatie over het configureren van diagnostische gegevens [verzamelen en gebruiken van diagnostische gegevens van uw Azure-resources](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Meld u diagnostische gegevens categorieën

Op dit moment kunnen vastleggen we twee categorieën van diagnostische logboeken:

* **Ontwerpen**. Opnamen gebeurtenissen die zijn verwante toojob operations authoring: taak maken, toevoegen en verwijderen van de invoer en uitvoer, toevoegen en bijwerken Hallo query, starten en stoppen Hallo taak.
* **Uitvoering**. Bevat gebeurtenissen die zich tijdens het uitvoeren van taak voordoen:
    * Connectiviteitsfouten
    * Gegevensverwerking fouten, met inbegrip van:
        * Gebeurtenissen die niet toohello voldoen querydefinitie (niet-overeenkomende veldtypen en waarden, ontbrekende velden, enzovoort)
        * Expressie evaluatie fouten
    * Andere gebeurtenissen en fouten

## <a name="diagnostics-logs-schema"></a>Diagnostische logboeken schema

Alle logboeken worden opgeslagen in de JSON-indeling. Elk item heeft Hallo algemene tekenreeksvelden te volgen:

Naam | Beschrijving
------- | -------
tijd | De tijdstempel (in UTC) van Hallo logboek.
resourceId | ID van Hallo resource die Hallo bewerking heeft plaatsgevonden, in hoofdletters. Het omvat Hallo abonnements-ID, resourcegroep Hallo en Hallo taaknaam. Bijvoorbeeld:   **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT. STREAMINGJOBS-STREAMANALYTICS/MYSTREAMINGJOB**.
category | Meld u categorie, ofwel **uitvoering** of **ontwerpen**.
operationName | Naam van Hallo-bewerking die wordt vastgelegd. Bijvoorbeeld: **gebeurtenissen verzenden: SQL-uitvoer schrijven fout toomysqloutput**.
status | De status van Hallo-bewerking. Bijvoorbeeld: **mislukt** of **geslaagd**.
niveau | Logboek-niveau. Bijvoorbeeld: **fout**, **waarschuwing**, of **informatief**.
properties | Meld u post-specifieke details over deze geserialiseerd als een JSON-tekenreeks. Zie voor meer informatie Hallo uit te voeren.

### <a name="execution-log-properties-schema"></a>Schema voor uitvoering logboek eigenschappen

Uitvoeringslogboeken zijn gegevens over de gebeurtenissen die hebben plaatsgevonden tijdens het uitvoeren van de Stream Analytics-taak. Hallo-schema van eigenschappen varieert, afhankelijk van het soort gebeurtenis Hallo. Momenteel hebben we de volgende soorten uitvoeringslogboeken Hallo:

### <a name="data-errors"></a>Fouten met gegevens

Er is een fout die optreedt tijdens het Hallo-taak verwerken van gegevens in deze categorie van Logboeken. Deze logboeken worden gemaakt tijdens het lezen, gegevens serialisatie, meestal en schrijfbewerkingen. Deze logboeken bevatten geen connectiviteitsfouten. Connectiviteitsfouten worden behandeld als algemene gebeurtenissen.

Naam | Beschrijving
------- | -------
Bron | Naam van de taak Hallo invoer of uitvoer waarin Hallo-fout is opgetreden.
Bericht | Bericht Hallo fout gekoppeld.
Type | Type fout. Bijvoorbeeld: **DataConversionError**, **CsvParserError**, of **ServiceBusPropertyColumnMissingError**.
Gegevens | Bevat gegevens die nuttig is tooaccurately Hallo bron van Hallo fout vinden. Onderwerp tootruncation, afhankelijk van de grootte.

Afhankelijk van Hallo **operationName** value, fouten hebben Hallo schema te volgen:
* **Gebeurtenissen serialiseren**. Serialiseren gebeurtenissen plaatsvinden tijdens gebeurtenis leesbewerkingen. Ze zich voordoen wanneer hello data-at-Hallo invoer voldoet niet aan Hallo Queryschema voor een van de volgende redenen:
    * *Niet-overeenkomend gegevenstype tijdens gebeurtenis (de) serialisatie toepassen op*: identificeert Hallo-veld dat Hallo fout veroorzaakt.
    * *Een gebeurtenis, Ongeldige serialisatie kan niet worden gelezen*: bevat informatie over de locatie van de Hallo Hallo invoergegevens waarin Hallo-fout is opgetreden. De blobnaam van de voor blob-invoer, offset en een voorbeeld van Hallo gegevens bevat.
* **Verzenden van gebeurtenissen**. Verzenden van gebeurtenissen plaatsvinden tijdens schrijfbewerkingen. Ze identificeren Hallo streaming-gebeurtenissen die Hallo fout heeft veroorzaakt.

### <a name="generic-events"></a>Algemene gebeurtenissen

Algemene gebeurtenissen hebben betrekking op alle andere.

Naam | Beschrijving
-------- | --------
Fout | (optioneel) Informatie over de fout. Meestal is dit uitzonderingsgegevens, als deze beschikbaar is.
Bericht| Logboekbericht.
Type | Type van het bericht. Maps toointernal categorisatie van fouten. Bijvoorbeeld: **JobValidationError** of **BlobOutputAdapterInitializationFailure**.
Correlatie-ID | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) die wordt aangeduid Hallo taakuitvoering. Alle logboekvermeldingen voor uitvoering van Hallo tijd Hallo taak begint pas Hallo taak stopt hebben dezelfde Hallo **correlatie-ID** waarde.

## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooStream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor stream Analytics query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)
