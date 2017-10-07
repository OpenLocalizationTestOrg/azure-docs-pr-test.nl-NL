---
title: Azure Application Insights-app-gegevens aaaView | Microsoft Docs
description: U kunt prestatieproblemen met de Hallo oplossing toodiagnose Application Insights-Connector gebruiken en inzicht in wat gebruikers doen met uw app wanneer bewaakt met Application Insights.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Application Insights-Connector oplossing (Preview) in de Operations Management Suite (OMS)

![Application Insights symbool](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Hallo toepassingen Insights-Connector oplossing helpt u bij het vaststellen van prestatieproblemen en u begrijpt wat gebruikers doen met uw app wanneer deze wordt bewaakt met [Application Insights](../application-insights/app-insights-overview.md). Weergaven Hallo dezelfde toepassingstelemetrie die ontwikkelaars weergegeven in Application Insights zijn beschikbaar in OMS. Wanneer u uw Application Insights-apps met OMS integreert, wordt echter zichtbaarheid van uw toepassingen verhoogd met als bewerking en toepassingsgegevens op één plek. Hebben dezelfde Hallo weergaven kunt u toocollaborate met uw app-ontwikkelaars. Hallo voorkomende weergaven kunnen u Hallo tijd toodetect verminderen en oplossen van zowel de toepassing en de problemen met het platform.

Wanneer u Hallo oplossing gebruiken, kunt u het volgende doen:

- Alle apps in uw Application Insights weergeven in één aanwezig is, zelfs wanneer ze zich in verschillende Azure-abonnementen
- Correleren van gegevens van de infrastructuur met toepassingsgegevens
- Toepassingsgegevens visualiseren met perspectieven in logboek zoeken
- Van logboekanalyse gegevens tooyour Application Insights-app in Hallo OMS en Azure portals van draaipunt

## <a name="connected-sources"></a>Verbonden bronnen

In tegenstelling tot de meeste andere Log Analytics-oplossingen, is niet gegevens voor Hallo Application Insights-Connector verzameld door agents. Alle gegevens die worden gebruikt door Hallo oplossing komt rechtstreeks uit Azure.

| Verbonden bron | Ondersteund | Beschrijving |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee | Hallo oplossing verzamelt geen informatie van Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van Linux-agents. |
| [SCOM-beheergroep](log-analytics-om-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van agents in een verbonden SCOM-beheergroep. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Hallo-oplossing heeft geen gegevens naar Azure storage. |

## <a name="prerequisites"></a>Vereisten

- tooaccess informatie van de Application Insights-Connector, moet u een Azure-abonnement hebben
- U moet ten minste één geconfigureerde Application Insights-resource hebben.
- U moet Hallo eigenaar of bijdrager van Hallo Application Insights-resource.

## <a name="configuration"></a>Configuratie

1. Inschakelen van hello Azure Web Apps Analytics-oplossing van Hallo [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Klik in de OMS-portal Hallo **instellingen** &gt; **gegevens** &gt; **Application Insights**.
3. Onder **Selecteer een abonnement**, selecteer een abonnement met Application Insights-resources en klik vervolgens onder **toepassingsnaam**, selecteer een of meer toepassingen.
4. Klik op **Opslaan**.

Gegevens beschikbaar in ongeveer 30 minuten en Hallo Application Insights-tegel wordt bijgewerkt met gegevens, zoals Hallo installatiekopie te volgen:

![Application Insights-tegel](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Andere tookeep punten in gedachten:

- U kunt alleen Application Insights apps tooone OMS-werkruimte koppelen.
- U kunt alleen koppelen [Standard of Premium Application Insights-resources](https://azure.microsoft.com/pricing/details/application-insights) tooOMS logboekanalyse. U kunt echter gratis laag Hallo van logboekanalyse.

## <a name="management-packs"></a>Management packs

Deze oplossing wordt niet geïnstalleerd voor alle management packs in de verbonden beheergroepen.

## <a name="use-hello-solution"></a>Hallo-oplossing gebruiken

Hallo volgende secties wordt beschreven hoe u Hallo blades weergegeven in Hallo Application Insights dashboard tooview gebruiken en interactie met gegevens van uw apps.

### <a name="view-application-insights-connector-information"></a>Informatie van de Application Insights-Connector weergeven

Klik op Hallo **Application Insights** tegel tooopen hello **Application Insights** dashboard toosee Hallo blades te volgen.

![Application Insights dashboard](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Application Insights dashboard](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

Hallo dashboard bevat Hallo blades wordt weergegeven in de tabel Hallo. Elke blade geeft een lijst van too10 items die overeenkomen met die van de blade criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een zoekopdracht logboek waarmee alle records geretourneerd wanneer u klikt op uitvoeren **alle** onderin Hallo van Hallo-blade of wanneer u klikt op Hallo blade-header.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Kolom** | **Beschrijving** |
| --- | --- |
| Toepassingen - aantal toepassingen | Geeft het aantal toepassingen Hallo in toepassingsbronnen. Ook toepassing voor een lijst met namen en voor elke Hallo aantal records van de toepassing. Klik op Hallo nummer toorun logboek zoekt<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Klik op een toepassing naam toorun logboek zoekt Hallo-toepassing die wordt weergegeven records van de toepassing per host, records op type Telemetrie en alle gegevens op type (gebaseerd op Hallo laatste dag). |
| Gegevensvolume – als host fungeert voor verzenden van gegevens | Toont Hallo aantal computer fungeert als host die van gegevens verzenden. Een lijst met computer fungeert als host en het aantal records voor elke host. Klik op Hallo nummer toorun logboek zoekt<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Klik op een computer name toorun logboek zoekt Hallo host waarin de records van de toepassing per host, records op type Telemetrie en alle gegevens op type (gebaseerd op Hallo laatste dag). |
| Beschikbaarheid – Webtest resultaten | Toont een ringdiagram voor web-testresultaten, waarmee wordt aangegeven op te geven of mislukken. Klik op Hallo grafiek toorun logboek zoekt<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Resultaten weergeven Hallo aantal fasen en fouten voor alle tests. Deze bevat alle Web-Apps met verkeer voor Hallo laatste minuut. Klik op een toepassing naam tooview een logboek zoekopdracht met details van de mislukte webtesten. |
| Serveraanvragen – aanvragen per uur | Toont een lijndiagram Hallo serveraanvragen per uur voor verschillende toepassingen. Beweeg de muisaanwijzer over een regel in Hallo grafiek toosee Hallo top-3 toepassingen aanvragen voor een punt in tijd ontvangen. Ook wordt een lijst van ontvangen aanvragen en Hallo aantal aanvragen gedurende Hallo geselecteerd Hallo-toepassingen. <br><br>Klik op Hallo grafiek toorun logboek zoekt <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> die toont een meer gedetailleerde lijndiagram Hallo serveraanvragen per uur voor verschillende toepassingen. <br><br> Klik op een toepassing in Hallo lijst toorun logboek zoekt <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> die bevat een overzicht van aanvragen, grafieken voor aanvragen gedurende de duur van de tijd en de aanvraag en een lijst van aanvraag responscodes.   |
| Fouten – mislukte aanvragen per uur | Toont een lijndiagram van mislukte aanvragen per uur. Beweeg de muisaanwijzer over Hallo grafiek toosee Hallo bovenste 3-toepassingen met mislukte aanvragen voor een punt in tijd. Ook wordt een lijst van toepassingen met Hallo aantal mislukte aanvragen voor elk weergegeven. Klik op Hallo grafiek toorun logboek zoekt <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> die ziet u een meer gedetailleerde lijndiagram van mislukte aanvragen. <br><br>Klik op een item in Hallo lijst toorun logboek zoekt <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> dat toont mislukte aanvragen, grafieken voor mislukte aanvragen via de duur van de tijd en de aanvraag en een lijst met reactiecodes van mislukte aanvragen. |
| Uitzonderingen – uitzonderingen per uur | Toont een lijndiagram van uitzonderingen per uur. Beweeg de muisaanwijzer over Hallo grafiek toosee Hallo bovenste 3-toepassingen met uitzonderingen voor een punt in tijd. Ook wordt een lijst van toepassingen met Hallo aantal uitzonderingen voor elk weergegeven. Klik op Hallo grafiek toorun logboek zoekt <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> die bevat een meer gedetailleerde koppeling-grafiek met uitzonderingen. <br><br>Klik op een item in Hallo lijst toorun logboek zoekt <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> die wordt een lijst met uitzonderingen, diagrammen voor uitzonderingen via tijd en mislukte aanvragen en een lijst met typen.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Hallo Application Insights perspectief met search logboek weergeven

Wanneer u een item in het Hallo-dashboard klikt, ziet u een Application Insights-perspectief wordt weergegeven in de zoekopdracht. Hallo perspectief biedt een uitgebreide visualisatie, op basis van Hallo telemetrie type die geselecteerd. In dat geval visualisatie inhoudswijzigingen voor verschillende telemetrie typen.

Wanneer u een willekeurige plaats in Hallo toepassingen blade klikt, ziet u Hallo standaard **toepassingen** perspectief.

![Application Insights toepassingen perspectief](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

Hallo perspectief geeft een overzicht van Hallo-toepassing die u hebt geselecteerd.

Hallo **beschikbaarheid** blade ziet u een ander perspectiefweergave waarin u web testresultaten en verwante mislukte aanvragen kunt bekijken.

![Application Insights beschikbaarheid perspectief](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Wanneer u klikt op een willekeurige plaats in Hallo **serveraanvragen** of **fouten** blades, Hallo perspectief onderdelen wijzigen toogive u een visualisatie die toorequests gerelateerd.

![Application Insights fouten blade](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Wanneer u klikt op een willekeurige plaats in Hallo **uitzonderingen** blade ziet u een visualisatie die afgestemd op tooexceptions.

![Application Insights uitzonderingen blade](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Ongeacht of u iets op een klikt Hallo **Application Insights-Connector** dashboard binnen Hallo **Search** pagina zelf, elke query retourneren van gegevens voor Application Insights weergegeven Hallo Application Insights perspectief. Als u gegevens van de Application Insights, bekijkt u bijvoorbeeld een **&#42;** query geeft ook Hallo perspectief tabblad zoals Hallo installatiekopie te volgen:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Perspectief onderdelen zijn bijgewerkt, afhankelijk van de zoekopdracht Hallo. Dit betekent dat u Hallo resultaten filteren kunt met behulp van een zoekveld die biedt u de mogelijkheid toosee Hallo Hallo gegevens uit:

- Al uw toepassingen
- Een geselecteerde toepassing
- Een groep van toepassingen

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Pivot tooan-app in hello Azure-portal

Application Insights-Connector blades zijn ontworpen tooenable u toopivot toohello geselecteerd Application Insights-app *wanneer u Hallo OMS-portal gebruikt*. U kunt Hallo oplossing gebruiken als een controle platform van hoog niveau die u helpt een app oplossen. Wanneer u een potentieel probleem in een van uw verbonden toepassingen zien, kunt u beide inzoomen in deze in de OMS-zoekopdracht of u kunt draaien rechtstreeks toohello Application Insights-app.

toopivot, klikt u op Hallo weglatingstekens (**...** ) die wordt weergegeven aan einde van elke regel Hallo en selecteer **geopend in Application Insights**.

>[!NOTE]
>**Open in Application Insights** is niet beschikbaar in hello Azure-portal.

![Open in Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Voorbeeld gecorrigeerd gegevens

Application Insights biedt  *[steekproef nemen correctie](../application-insights/app-insights-sampling.md)*  toohelp verminderen het verkeer van telemetrie. Als u steekproeven op uw Application Insights-app inschakelt, krijgt u een kleiner aantal vermeldingen die zijn opgeslagen in de Application Insights en in OMS. Terwijl de consistentie van de gegevens blijft behouden in het Hallo **Application Insights-Connector** pagina en perspectieven, u moet handmatig steekproefgegevens corrigeren voor uw aangepaste query's.

Hier volgt een voorbeeld van steekproeven correctie in een logboek zoekquery:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Hallo **aantal actieve** veld aanwezig is in alle vermeldingen en toont Hallo aantal gegevenspunten dat Hallo vermelding vertegenwoordigt. Als u steekproeven voor uw app Application Insights inschakelt **aantal actieve** groter is dan 1. toocount werkelijke aantal vermeldingen die uw toepassing genereert, som Hallo Hallo **aantal actieve** velden.

Steekproeven beïnvloedt alleen Hallo totaal aantal items dat uw toepassing genereert. U hoeft niet toocorrect steekproef nemen voor metrische velden als **RequestDuration** of **AvailabilityDuration** omdat Hallo gemiddelde voor weergegeven vermeldingen in de velden weergegeven.

## <a name="input-data"></a>Invoergegevens

Hallo oplossing ontvangt Hallo volgende telemetrie soorten gegevens uit uw verbonden apps met Application Insights:

- Beschikbaarheid
- Uitzonderingen
- Aanvragen
- Paginaweergaven – voor uw werkruimte tooreceive paginaweergaven, moet u uw apps toocollect die informatie configureren. Zie voor meer informatie [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Aangepaste gebeurtenissen – voor uw werkruimte tooreceive aangepaste gebeurtenissen, moet u uw apps toocollect die informatie configureren. Zie voor meer informatie [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

Gegevens worden ontvangen door OMS van Application Insights zodra deze beschikbaar is.

## <a name="output-data"></a>uitvoergegevens

Een record met een *type* van *ApplicationInsights* is gemaakt voor elk type invoergegevens. ApplicationInsights records hebben eigenschappen weergegeven in Hallo uit te voeren:

### <a name="generic-fields"></a>Algemene velden

| Eigenschap | Beschrijving |
| --- | --- |
| Type | ApplicationInsights |
| client-IP |   |
| TimeGenerated | Tijd van Hallo record |
| ApplicationId | De instrumentatiesleutel van Hallo Application Insights-app |
| ApplicationName | Naam van Hallo Application Insights-app |
| RoleInstance | ID van server-host |
| DeviceType | Client-apparaat |
| ScreenResolution |   |
| Continent | Continent waar Hallo aanvraag afkomstig is |
| Land | Land waar Hallo aanvraag afkomstig is |
| Provincie | Provincie, status- of landinstelling waar Hallo aanvraag afkomstig is |
| Plaats | Stad of plaats waar Hallo aanvraag afkomstig is |
| isSynthetic | Hiermee wordt aangegeven of het Hallo-aanvraag is gemaakt door een gebruiker of door automatische methode. = True gebruiker gegenereerde of ONWAAR = automatische methode |
| SamplingRate | Percentage van de telemetrie die is gegenereerd door Hallo-SDK die tooportal wordt verzonden. Het bereik 0,0 100,0. |
| SampledCount | 100/(SamplingRate). Bijvoorbeeld, 4 =&gt; 25% |
| IsAuthenticated | Waar of onwaar |
| OperationID | Items die dezelfde bewerking-ID als betrokken Items worden weergegeven in de portal Hallo Hallo hebben. Meestal Hallo-aanvraag-ID |
| ParentOperationID | Hallo bovenliggende bewerking-ID |
| OperationName |   |
| sessie-id | GUID toouniquely identificeren Hallo-sessie waarop Hallo is gemaakt |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Beschikbaarheid-specifieke velden

| Eigenschap | Beschrijving |
| --- | --- |
| TelemetryType | Beschikbaarheid |
| AvailabilityTestName | Naam van de WebTest Hallo |
| AvailabilityRunLocation | Geografische bron van de http-aanvraag |
| AvailabilityResult | Hallo geslaagd resultaat van WebTest Hallo aangeeft |
| AvailabilityMessage | Hallo-bericht toohello WebTest gekoppeld |
| AvailabilityCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| DataSizeMetricValue | 1.0 of 0,0 |
| DataSizeMetricCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| AvailabilityDuration | Tijd in milliseconden van Hallo web testduur |
| AvailabilityDurationCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | De unieke GUID voor de WebTest Hallo |
| AvailabilityTimestamp | Nauwkeurig tijdstempel van Hallo beschikbaarheidstest |
| AvailabilityDurationMin | Voor opgevangen records bevat dit veld testduur (milliseconden) voor de gegevenspunten Hallo vertegenwoordigd Hallo minimale web |
| AvailabilityDurationMax | Voor opgevangen records bevat dit veld testduur (milliseconden) voor de gegevenspunten Hallo vertegenwoordigd Hallo maximale web |
| AvailabilityDurationStdDev | Voor opgevangen records bevat dit veld Hallo standaardafwijking tussen alle web test duur (in milliseconden) van gegevenspunten Hallo weergegeven |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Uitzondering-specifieke velden

| Type | ApplicationInsights |
| --- | --- |
| TelemetryType | Uitzondering |
| ExceptionType | Hallo uitzonderingstype |
| ExceptionMethod | Hallo-methode die Hallo uitzondering worden gemaakt |
| ExceptionAssembly | Assembly bevat Hallo framework en de versie en de openbare-sleuteltoken Hallo |
| ExceptionGroup | Hallo uitzonderingstype |
| ExceptionHandledAt | Hiermee wordt aangegeven Hallo niveau dat Hallo uitzondering afgehandeld |
| ExceptionCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| ExceptionMessage | Bericht van uitzondering Hallo |
| ExceptionStack | Volledige stack van uitzondering Hallo |
| ExceptionHasStack | True als uitzondering een stack heeft |



### <a name="request-specific-fields"></a>Aanvraag-specifieke velden

| Eigenschap | Beschrijving |
| --- | --- |
| Type | ApplicationInsights |
| TelemetryType | Aanvraag |
| ResponseCode | HTTP-antwoord verzonden tooclient |
| RequestSuccess | Hiermee wordt aangegeven of geslaagd of mislukt. Waar of ONWAAR. |
| Aanvraag-id | ID toouniquely Hallo aanvraag identificeren |
| RequestName | GET/POST + URL-basis |
| RequestDuration | Tijd in seconden van Hallo aanvraag duur |
| URL | URL van Hallo-aanvraag niet met inbegrip van host |
| Host | Web server-host |
| URLBase | Volledige URL van de aanvraag Hallo |
| ApplicationProtocol | Type protocol dat wordt gebruikt door de toepassing hello |
| requestCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| RequestDurationCount | 100 /(Sampling Rate). Bijvoorbeeld, 4 =&gt; 25% |
| RequestDurationMin | Dit veld bevat voor opgevangen records Hallo minimale aanvraag duur (in milliseconden) voor gegevenspunten Hallo vertegenwoordigd. |
| RequestDurationMax | Voor opgevangen records bevat dit veld Hallo maximale aanvraag duur (in milliseconden) voor de gegevenspunten Hallo weergegeven |
| RequestDurationStdDev | Voor opgevangen records bevat dit veld Hallo standaardafwijking tussen alle aanvraag duur (in milliseconden) van gegevenspunten Hallo weergegeven |

## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken

Deze oplossing heeft geen een reeks voorbeeld logboek zoekopdrachten op Hallo dashboard weergegeven. Echter voorbeeld logboek zoekquery's met beschrijvingen worden weergegeven in Hallo [weergave Application Insights-Connector informatie](#view-application-insights-connector-information) sectie.

## <a name="next-steps"></a>Volgende stappen

- Gebruik [logboek zoeken](log-analytics-log-searches.md) tooview gedetailleerde informatie voor uw Application Insights-apps.
