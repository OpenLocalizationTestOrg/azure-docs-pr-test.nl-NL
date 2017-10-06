---
title: aaaCloud Cruiser en Microsoft Azure Billing API-integratie | Microsoft Docs
description: "Biedt een unieke perspectief van Microsoft Azure Billing partner Cruiser Cloud, op hun ervaringen hello Azure Billing-API's integreren in hun product.  Dit is vooral nuttig voor Azure en Cloud Cruiser klanten die zijn geïnteresseerd zijn in gebruik/probeert Cloud Cruiser voor Microsoft Azure-pakket."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Cloud Cruiser en Microsoft Azure Billing API-integratie
Dit artikel wordt beschreven hoe Hallo gegevens worden verzameld van de nieuwe Microsoft Azure Billing-API's kunnen worden gebruikt in de Cloud Cruiser voor werkstroom Hallo kosten simulatie en -analyse.

## <a name="azure-ratecard-api"></a>Azure RateCard API
Hallo RateCard API biedt informatie van de snelheid van Azure. Na verificatie met de juiste referenties hello, kunt u een query Hallo API toocollect metagegevens over Hallo services beschikbaar zijn op Azure, samen met de Hallo tarieven van uw bieden.

Hallo volgt een voorbeeld-reactie van Hallo API Hallo prijzen voor Hallo A0 (Windows) met exemplaar:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>Cloud van Cruiser Interface tooAzure RateCard API
Cloud Cruiser kunt gebruikmaken van Hallo RateCard API-informatie op verschillende manieren. Voor dit artikel wordt we zien hoe deze kan worden gebruikt toomake IaaS werkbelasting kosten simulatie en analyse.

toodemonstrate dit geval gebruiken, stelt u zich voor een werkbelasting van meerdere instanties die actief zijn op Microsoft Azure Pack (WAP). Hallo-doel is toosimulate deze dezelfde werkbelasting op Azure en schatting Hallo kosten dergelijke migratie te doen. In volgorde toocreate deze simulatie, zijn er twee hoofdtaken toobe uitgevoerd:

1. **Importeren en verwerken Hallo service verzamelde gegevens van Hallo RateCard API.** Deze taak wordt ook uitgevoerd op Hallo werkmappen, waarbij Hallo uitpakken uit Hallo RateCard API getransformeerd en gepubliceerde tooa nieuw snelheid plan is. Dit nieuwe snelheid abonnement zullen worden gebruikt op Hallo simulaties tooestimate hello Azure prijzen.
2. **Normaliseren WAP-services en Azure IaaS-services.** Standaard WAP-services zijn gebaseerd op afzonderlijke resources (CPU, geheugen, schijfgrootte, enz.) bij Azure services zijn gebaseerd op de exemplaargrootte van het (A0, A1, A2, enzovoort). Deze eerste taak kan worden uitgevoerd door de Cloud Cruiser ETL-engine, aangeroepen werkmappen, waar deze resources kunnen worden gebundeld op exemplaar grootten, vergelijkbaar tooAzure exemplaar services.

### <a name="import-data-from-hello-ratecard-api"></a>Gegevens importeren uit Hallo RateCard API
Cloud Cruiser werkmappen bevatten een geautomatiseerd proces en toocollect informatie van Hallo RateCard API.  Werkmappen voor ETL (uitpakken-transformatie-load) kunnen u tooconfigure Hallo verzameling, transformeren en publiceren van gegevens naar Hallo Cloud Cruiser database.

Elke werkmap kan hebben een of meerdere verzamelingen, zodat u toocorrelate gegevens uit verschillende bronnen toocomplement of Hallo gebruiksgegevens verbeteren. Hallo na twee schermafbeeldingen tonen hoe toocreate een nieuwe *verzameling* in een bestaande werkmap en het importeren van gegevens in Hallo *verzameling* van Hallo RateCard API:

![Afbeelding 1: een nieuwe verzameling maken][1]

![Afbeelding 2: gegevens importeren uit de nieuwe verzameling Hallo][2]

Na het Hallo-gegevens importeren in de werkmap hello, is mogelijk toocreate meerdere stappen en processen van de transformatie, toomodify en model Hallo gegevens. In dit voorbeeld gerelateerd omdat we alleen geïnteresseerd in de infrastructuur-as-a-Service (IaaS) bent, kunnen we Hallo transformatie stappen tooremove onnodige rijen of records gebruiken, tooservices dan IaaS.

Hallo volgende schermafbeelding ziet Hallo transformatie stappen tooprocess Hallo gegevens verzameld van RateCard API gebruikt:

![Afbeelding 3 - transformatie stappen tooprocess verzamelde gegevens van RateCard API][3]

### <a name="defining-new-services-and-rate-plans"></a>Plannen voor het definiëren van nieuwe Services en snelheid
Er zijn verschillende manieren toodefine services op Cloud Cruiser. Een van de opties Hallo is tooimport Hallo services van gebruiksgegevens Hallo. Deze methode wordt doorgaans gebruikt bij het werken met openbare clouds, waarbij Hallo services al zijn gedefinieerd door Hallo-provider.

Een Tariefplan is een reeks tarieven of prijzen die toegepast toodifferent services worden kunnen, op basis van ingangsdatums of groep aan klanten, onder andere opties. Tarieven kunnen ook worden gebruikt voor Cloud Cruiser toocreate simulatie of 'Wat-als'-scenario's, toounderstand hoe wijzigingen in services Hallo totale kosten van een werklast kunnen beïnvloeden.

In dit voorbeeld gebruiken we Hallo servicegegevens van Hallo RateCard API toodefine nieuwe services in de Cloud Cruiser. In Hallo dezelfde manier, kunnen we gebruiken Hallo tarieven toohello toocreate een nieuwe Tariefplan op Cruiser Cloud services.

Aan het einde van de Hallo van Hallo transformatie proces, mogelijke toocreate is een nieuwe stap en Hallo gegevens van Hallo RateCard API publiceren als nieuwe services en tarieven.

![Afbeelding 4: Hallo gegevens van Hallo RateCard API publiceren als een nieuwe Services en tarieven][4]

### <a name="verify-azure-services-and-rates"></a>Controleer of de Azure-Services en tarieven
Nadat u hebt gepubliceerd Hallo en -kosten, kunt u controleren of Hallo lijst met geïmporteerde services in de Cloud Cruiser *Services* tabblad:

![Afbeelding 5: controleren Hallo nieuwe Services][5]

Op Hallo *snelheid plannen* tabblad kunt u Hallo nieuw snelheid plan 'AzureSimulation' met Hallo tarieven geïmporteerd uit Hallo RateCard API aangeroepen controleren.

![Afbeelding 6 - verifiëren Hallo nieuwe Tariefplan en bijbehorende tarieven][6]

### <a name="normalize-wap-and-azure-services"></a>Normaliseren WAP en Azure-Services
WAP biedt standaard gebruiksgegevens die zijn gebaseerd op Hallo gebruik van de berekenings-, geheugen- en netwerkbronnen. In de Cloud Cruiser, kunt u uw services die zijn gebaseerd op Hallo toewijzing of het gecontroleerde gebruik van deze resources definiëren. U kunt bijvoorbeeld een basic frequentie instellen voor elk uur van de CPU-gebruik of kosten Hallo GB geheugen toegewezen tooan exemplaar.

Bijvoorbeeld, in volgorde toocompare kosten tussen WAP en Azure, moeten we tooaggregate Hallo Resourcegebruik op WAP in bundels, die vervolgens toegewezen tooAzure services kunnen worden. Deze transformatie kan gemakkelijk worden geïmplementeerd in Hallo werkmappen:

![Afbeelding 7: WAP toonormalize gegevensservices transformeren][7]

Hallo laatste stap op het Hallo-werkmap is toopublish Hallo gegevens in Hallo Cloud Cruiser database. Tijdens deze stap Hallo gebruiksgegevens nu is opgenomen in services (die zijn toegewezen toohello Azure-Services) en toodefault tarieven toocreate Hallo kosten verbonden.

Na het Hallo-werkmap, voltooid, kunt u Hallo verwerking van gegevens van de Hallo, automatiseren door het toevoegen van een taak op Hallo scheduler en het Hallo-frequentie en het tijdstip voor Hallo werkmap toorun op te geven.

![Afbeelding 8 - werkmap plannen][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Rapporten voor werkbelasting kosten simulatie analyse maken
Nadat Hallo gebruiksgegevens worden verzameld en kosten zijn geladen in Hallo Cloud Cruiser database, kunnen we Hallo Cloud Cruiser Insights module toocreate Hallo werkbelasting kosten simulatie die we willen gebruikmaken.

In volgorde toodemonstrate dit scenario hebben we gemaakt Hallo rapport te volgen:

![Vergelijking van kosten][9]

Hallo bovenste grafiek toont een kostenvergelijking door services, vergelijken Hallo prijs van uitgevoerde Hallo werkbelasting voor elke specifieke service tussen WAP (donker blauw) en Azure (lichte blauw).

Hallo onder grafiek toont Hallo dezelfde gegevens maar uitgesplitst per afdeling. Dit betekent Hallo kosten voor elke afdeling toorun van hun werkbelasting op WAP en Azure, samen met de Hallo verschil tussen deze twee op Hallo besparingen balk (groen).

## <a name="azure-usage-api"></a>Gebruik van Azure-API
### <a name="introduction"></a>Inleiding
Microsoft heeft onlangs geïntroduceerd hello Azure gebruik API, abonnees tooprogrammatically pull in gebruik gegevens toogain inzicht in hun verbruik toestaan. Dit is een goed nieuws voor Cloud Cruiser klanten die van Hallo uitgebreidere gegevensset beschikbaar via deze API profiteren kunnen.

Hallo-integratie met Hallo gebruik API op verschillende manieren kunt gebruikmaken van cloud Cruiser. Hallo granulatie (elk uur informatie over het gebruik) en metagegevens resourcegegevens beschikbaar via de API biedt Hallo Hallo nodig gegevensset toosupport flexibele Showback of terugstorting modellen. 

In deze zelfstudie wordt er een voorbeeld van hoe Cloud Cruiser van Hallo gebruik API-informatie profiteren kunt opleveren. We wordt meer specifiek, een resourcegroep maken in Azure, koppel de labels voor Hallo account structuur en Hallo van binnenhalen van gegevens en verwerkt Hallo label in de Cloud Cruiser wordt beschreven.

Hallo uiteindelijke doel is toobe kunnen toocreate rapporten, zoals Hallo volgt, en kunnen tooanalyze kosten en het verbruik op basis van Hallo account structuur gevuld door Hallo labels worden.

![Afbeelding 10 - rapport met storingen met tags][10]

### <a name="microsoft-azure-tags"></a>Labels van de Microsoft Azure
Hallo gegevens beschikbaar zijn via hello Azure gebruik API bevat niet alleen informatie over het verbruik, maar ook met inbegrip van alle codes die zijn gekoppeld aan het bron-metagegevens. Tags bieden een eenvoudige manier tooorganize uw resources, maar in de volgorde toobe effectieve, moet u tooensure die:

* Labels zijn correct toegepaste toohello resources tijdens het inrichten
* Labels worden correct op Hallo Showback/verrekenen proces tootie Hallo gebruik toohello van account organisatiestructuur gebruikt.

Beide van deze vereisten kunnen lastig zijn, vooral wanneer er is een handmatig proces op Hallo inrichten of opladen van kant. Verkeerd getypt, onjuiste of zelfs ontbrekende tags zijn algemene klachten van klanten wanneer levensduur op Hallo opladen erg lastig aan clientzijde met labels en deze fouten kunt aanbrengen.

Hello kunt nieuwe API voor het gebruik van Azure Cloud Cruiser pull-resource tagging informatie en via een geavanceerde ETL hulpprogramma werkmappen aangeroepen, deze algemene tagging fouten zijn opgelost. Via transformatie met behulp van reguliere expressies en correlatie van gegevens, Cloud Cruiser onjuist gelabelde bronnen identificeren en Hallo juist tags, toepassen Hallo juiste koppeling van Hallo resources met Hallo consumer gezorgd.

Op Hallo aan clientzijde in rekening gebracht, Cloud Cruiser hello Showback/verrekenen proces automatiseert en kunnen gebruikmaken van Hallo tag tootie Hallo gebruik toohello juiste informatiewerker (afdeling, afdeling, Project, enzovoort). Deze automatisering biedt een enorme verbetering en kunt controleren of een consistente en controleerbare geladen proces.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Maken van een resourcegroep met labels op Microsoft Azure
Hallo eerste stap in deze zelfstudie is toocreate een bronnengroep in hello Azure-portal en vervolgens tooassociate toohello resources voor nieuwe labels maken. In dit voorbeeld we Hallo volgende labels maken: afdeling, omgeving, eigenaar, Project.

Hallo onderstaande schermafbeelding toont een voorbeeld van een resourcegroep met de Hallo labels die is gekoppeld.

![Afbeelding 11 - resourcegroep met de bijbehorende tags op Azure-portal][11]

de volgende stap Hallo is toopull Hallo informatie uit Hallo gebruik API in de Cloud Cruiser. Hallo gebruik API biedt momenteel reacties in JSON-indeling. Hier volgt een voorbeeld van Hallo gegevens zijn opgehaald:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Gegevens importeren uit Hallo gebruik API in de Cloud Cruiser
Cloud Cruiser werkmappen bevatten een geautomatiseerd proces en toocollect informatie van Hallo gebruik API. Een werkmap van ETL (uitpakken-transformatie-load) kunt u tooconfigure Hallo verzameling, transformeren en publiceren van gegevens naar Hallo Cloud Cruiser database.

Elke werkmap, kan een of meerdere verzamelingen hebben. Hiermee kunt u toocorrelate gegevens uit verschillende bronnen toocomplement of uitbreiding van Hallo gebruiksgegevens. In dit voorbeeld wordt er een nieuw werkblad in hello Azure-sjabloon werkmap maken (*UsageAPI)* en stel een nieuw *verzameling* tooimport informatie uit Hallo gebruik API.

![Afbeelding 3 - API gebruiksgegevens Hallo UsageAPI blad geïmporteerd][12]

U ziet dat deze werkmap al andere heeft vellen tooimport services van Azure (*ImportServices*), en informatie over het verbruik van Hallo van Hallo facturering API verwerken (*PublishData*).

Vervolgens gebruiken we Hallo gebruik API toopopulate hello *UsageAPI* blad en vergelijken Hallo informatie met gegevens over het verbruik van Hallo facturering API Hallo op Hallo *PublishData* blad.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Hallo-tag-informatie van Hallo gebruik API verwerken
Na het Hallo-gegevens importeren in de werkmap hello, maken we stappen van de transformatie in Hallo *UsageAPI* eigenschappenvenster in tooprocess Hallo ordergegevens van Hallo API. Eerste stap is toouse een Hallo 'JSON splitsen' processor tooextract labels van een veld en maak vervolgens velden voor elk adres hiervan (afdeling, Project eigenaar en omgeving).

![Afbeelding 4: nieuwe velden voor Hallo-tag-informatie maken][13]

Kennisgeving Hallo "Netwerken" service ontbreekt Hallo-tag-informatie (geel vak), maar we kunnen verifiëren dat het deel van Hallo uitmaakt dezelfde resourcegroep door te kijken Hallo *ResourceGroupName* veld. Aangezien we andere resources uit deze resourcegroep Hallo labels voor hello hebben, kunnen we gebruiken deze informatie tooapply Hallo labels toothis resource later in Hallo proces ontbreekt.

Hallo volgende stap is een lookup associëren Hallo tabelgegevens van Hallo labels toohello toocreate *ResourceGroupName*. Deze opzoektabel wordt gebruikt op Hallo volgende stap tooenrich Hallo verbruiksgegevens label informatie.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Hallo tag toohello verbruiksgegevens toevoegen
Nu we toohello kunt gaan *PublishData* blad, welke processen Hallo informatie over het verbruik van Hallo API facturering en Hallo velden opgehaald uit het Hallo-tags toevoegen. Dit proces wordt uitgevoerd door te kijken Hallo opzoektabel gemaakt op de vorige stap hello, met behulp van Hallo *ResourceGroupName* als Hallo-sleutel voor Hallo zoekacties.

![Afbeelding 5 - Hallo account structuur met Hallo informatie uit Hallo zoekacties in te vullen][14]

U ziet dat Hallo juiste account structuurvelden voor Hallo "Netwerken" service zijn toegepast, en Hallo probleem Hello ontbreken codes is hersteld. We ook Hallo account structuurvelden voor bronnen dan de doelgegevensruimte resourcegroep met 'Andere' hebt ingevuld, in volgorde toodifferentiate op Hallo rapporten.

Nu moet we zojuist tooadd een stap toopublish Hallo-gebruiksgegevens. Tijdens deze stap worden Hallo juiste tarieven voor elke service die is gedefinieerd op onze Tariefplan toegepaste toohello gebruiksinformatie over Hallo resulterende kosten in Hallo database geladen.

Hallo aanbevolen onderdeel is dat u alleen toogo door dit proces eenmaal. Wanneer het Hallo-werkmap is voltooid, hoeft u alleen tooadd het toohello scheduler en het per uur wordt uitgevoerd of dagelijks op Hallo geplande tijd. Is alleen een kwestie van nieuwe rapporten maken of aanpassen van bestaande, in volgorde tooanalyze Hallo gegevens tooget betekenisvolle inzichten voor uw gebruik van cloud.

### <a name="next-steps"></a>Volgende stappen
* Voor gedetailleerde instructies over het maken van Cloud Cruiser werkmappen en rapporten, verwijzen wij u tooCloud Cruiser online de [documentatie](http://docs.cloudcruiser.com/) (geldig aanmelden vereist).  Voor meer informatie over Cloud Cruiser, neem contact op met [ info@cloudcruiser.com ](mailto:info@cloudcruiser.com).
* Zie [inzicht in uw Microsoft Azure-brongebruik](billing-usage-rate-card-overview.md) voor een overzicht van hello Azure brongebruik en RateCard APIs.
* Bekijk Hallo [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) voor meer informatie over beide API's die deel uitmaken van Hallo set API's die worden geleverd door hello Azure Resource Manager.
* Als u toodive in de voorbeeldcode Hallo wilt, Bekijk onze Microsoft Azure Billing API codevoorbeelden op [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Meer informatie
* Zie Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) artikel toolearn meer over hello Azure Resource Manager.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Afbeelding 1: een nieuwe verzameling maken"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Afbeelding 2: gegevens importeren uit de nieuwe verzameling Hallo"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Afbeelding 3 - transformatie stappen tooprocess verzamelde gegevens van RateCard API"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Afbeelding 4: Hallo gegevens van Hallo RateCard API publiceren als een nieuwe Services en tarieven"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Afbeelding 5: controleren Hallo nieuwe Services"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Afbeelding 6 - verifiëren Hallo nieuwe Tariefplan en bijbehorende tarieven"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Afbeelding 7: WAP toonormalize gegevensservices transformeren"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Afbeelding 8 - werkmap plannen"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Afbeelding 9 - voorbeeldrapport voor Hallo werkbelasting kosten vergelijking scenario"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Afbeelding 10 - rapport met storingen met tags"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Afbeelding 11 - resourcegroep met de bijbehorende tags op Azure-portal"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Afbeelding 12 - API gebruiksgegevens Hallo UsageAPI blad geïmporteerd"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Afbeelding 13 - nieuwe velden voor Hallo-tag-informatie maken"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Afbeelding 14 - Hallo account structuur met Hallo informatie uit Hallo zoekacties in te vullen"
