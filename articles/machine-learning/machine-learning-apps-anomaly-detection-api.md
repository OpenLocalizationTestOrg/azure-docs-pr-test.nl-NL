---
title: aaaAzure Machine Learning Afwijkingsdetectie Detection-API | Microsoft Docs
description: Afwijkingsdetectie Detection-API is een voorbeeld gebouwd met Microsoft Azure Machine Learning die afwijkingen gedetecteerd in de reeks tijdgegevens met numerieke waarden die gelijkmatig zijn verdeeld in de tijd.
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>Machine Learning eigen Afwijkingsdetectie API
## <a name="overview"></a>Overzicht
[Afwijkingsdetectie detectie API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) is een voorbeeld gebouwd met Azure Machine Learning die afwijkingen gedetecteerd in de reeks tijdgegevens met numerieke waarden die gelijkmatig zijn verdeeld in de tijd.

Deze API kan detecteren Hallo soorten afwijkende patronen in de reeksgegevens te volgen:

* **Positieve en negatieve trends**: bijvoorbeeld wanneer bewaking geheugengebruik in een opwaartse trend computing interessant kan zijn omdat dit mogelijk indicatief voor een geheugenlek
* **Wijzigingen in de dynamische waardenbereik Hallo**: bijvoorbeeld bij de bewaking van Hallo-uitzonderingen die door een cloudservice, eventuele wijzigingen in de dynamische waardenbereik Hallo kunnen duiden op instabiliteit van Hallo status van Hallo-service, en
* **Bereikt en daalt**: bijvoorbeeld bij de bewaking van Hallo aantal mislukte aanmeldingen in een service of het nummer van de opdrachten om uitchecken in een e-commercesite pieken of dips kunnen duiden op abnormaal gedrag.

Dergelijke wijzigingen in waarden bijhouden gedurende een tijd- en de doorlopende wijzigingen in hun waarden op deze machine learning detectoren als afwijkingsdetectie scores. Zij vereisen geen ad-hoc drempelwaarde afstemmen en hun scores kunnen gebruikte toocontrol false positief snelheid. Hallo afwijkingsdetectie API is handig in verschillende scenario's zoals servicecontrole door KPI's gedurende een periode, gebruik bijhouden via de metrische gegevens zoals het aantal zoekopdrachten, klikken kunt aantallen bewaking prestatiebewaking via items zoals CPU, geheugen-bestand gelezen, enzovoort gedurende een bepaalde periode.

Hallo Afwijkingsdetectie aanbieding wordt geleverd met nuttige hulpmiddelen tooget die u gestart.

* Hallo [webtoepassing](http://anomalydetection-aml.azurewebsites.net/) helpt u bij het beoordelen en Hallo resultaten van de afwijkingsdetectie API's voor uw gegevens te visualiseren.

> [!NOTE]
> Probeer **IT Afwijkingsdetectie Insights-oplossing** aangedreven door [deze API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)
> 
> tooget deze end-oplossing tooend geïmplementeerd tooyour Azure-abonnement <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **Begin hier >**</a>
> 
>

## <a name="api-deployment"></a>API-implementatie
In de volgorde toouse Hallo API, moet deze de tooyour Azure-abonnement waar deze wordt gehost als Azure Machine Learning-webservice implementeert.  U kunt dit doen vanuit Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Hiermee implementeert u twee AzureML-webservices (en hun verwante resources) tooyour Azure-abonnement - één voor afwijkingsdetectie seizoensgebonden opsporen en één zonder seizoensgebonden detectie.  Zodra het Hallo-implementatie is voltooid, kunt u zich kunt toomanage uw API's van Hallo [AzureML-webservices](https://services.azureml.net/webservices/) pagina.  Op deze pagina wordt u kunnen toofind worden de eindpuntlocaties van uw, API-sleutels, evenals voorbeeldcode voor het Hallo-API aanroepen.  Meer gedetailleerde instructies vindt u [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Hallo API schalen
Uw implementatie hebben standaard een gratis Dev/Test-abonnement waaronder 1000 transacties/en 2 compute uren/maand.  U kunt tooanother plan bijwerken volgens uw behoeften.  Informatie over het Hallo-prijzen van verschillende abonnementen [hier](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) onder 'Productie-Web-API prijzen'.

## <a name="managing-aml-plans"></a>Het beheren van AML plannen 
U kunt uw abonnement beheren [hier](https://services.azureml.net/plans/).  naam van het abonnement Hello wordt gebaseerd op Hallo Resourcegroepnaam die u hebt gekozen bij het implementeren van Hallo API, plus een tekenreeks die is uniek tooyour abonnement.  Instructies over de wijze waarop tooupgrade uw plan beschikbaar [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) onder 'Facturering abonnementen beheren' Hallo-sectie.

## <a name="api-definition"></a>API-definitie
Hallo-webservice biedt een REST gebaseerde API die kan worden gebruikt op verschillende manieren een web- of mobiele toepassingen, R, Python, Excel, inclusief via HTTPS enzovoort.  U verzendt uw time series gegevens toothis-service via een REST-API-aanroep en het uitvoeren van een combinatie van Hallo drie afwijkingsdetectie typen die hieronder worden beschreven.

## <a name="calling-hello-api"></a>Hallo-API aanroepen
In de volgorde toocall Hallo API moet u tooknow Hallo eindpuntlocatie en API-sleutel.  Deze samen met de voorbeeldcode voor het Hallo-API aanroepen zijn beschikbaar via Hallo [AzureML-webservices](https://services.azureml.net/webservices/) pagina.  Navigeer toohello gewenst API en klik vervolgens op Hallo 'Verbruiken' tabblad toofind ze.  Houd er rekening mee dat u Hallo-API als een Swagger API kan aanroepen (dat wil zeggen met URL-parameter Hallo `format=swagger`) of als een niet - Swagger API (d.w.z. zonder Hallo `format` URL-parameter).  Hallo voorbeeldcode maakt gebruik van Hallo Swagger-indeling.  Hieronder volgt een voorbeeld van de aanvraag en antwoord in niet-Swagger-indeling.  Deze voorbeelden zijn toohello seizoensgebonden eindpunt.  Hallo niet seizoensgebonden eindpunt is vergelijkbaar.

### <a name="sample-request-body"></a>Voorbeeld aanvraagtekst
Hallo-aanvraag bevat twee objecten: `Inputs` en `GlobalParameters`.  Bij Hallo voorbeeld onderstaande aanvraag, sommige parameters verzonden expliciet terwijl andere niet (Schuif omlaag voor een volledige lijst met parameters voor elk eindpunt).  Parameters die niet expliciet worden verzonden in Hallo aanvraag gebruikt Hallo standaardwaarden hieronder genoemd.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Voorbeeldantwoord
Merk op dat, in volgorde toosee hello `ColumnNames` veld, moet u opnemen `details=true` als een URL-parameter in uw aanvraag.  Zie Hallo tabellen hieronder voor Hallo betekenis achter elk van deze velden.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>Score-API
Hallo Score-API wordt gebruikt voor het uitvoeren van de afwijkingsdetectie op niet-seizoensgebonden reeksgegevens. Hallo API een aantal afwijkingsdetectie detectoren op Hallo gegevens wordt uitgevoerd en hun scores afwijkingsdetectie retourneert. Hallo afbeelding hieronder toont een voorbeeld van afwijkingen die Hallo die score API kan detecteren. Deze tijdreeks heeft 2 distinct verandert en 3 pieken. Hallo rode punten weergeven Hallo-tijd op welke Hallo niveau wijziging wordt gedetecteerd, terwijl Hallo zwarte punten Hallo gedetecteerd pieken weergeven.
![Score-API][1]

### <a name="detectors"></a>Detectoren
Hallo afwijkingsdetectie API ondersteunt detectoren in 3 hoofdcategorieën. Meer informatie over specifieke invoerparameters en outputs voor elke detectie vindt u in de volgende tabel Hallo.

| Detectie-categorie | Detectie | Beschrijving | Invoerparameters | uitvoer |
| --- | --- | --- | --- | --- |
| De detectoren piek |TSpike detectie |Pieken en dips op basis van helemaal Hallo waarden tussen het eerste en derde kwartielen liggen detecteren |*tspikedetector.Sensitivity:* duurt geheel getal in Hallo bereik 1-10-standaard: 3; Hogere waarden wordt onderschept meer extreme waarden, waardoor er minder gevoelig |TSpike: binaire waarden: '1' als een piek/dip wordt gedetecteerd, '0' anders |
| De detectoren piek | ZSpike detectie |Detecteren pieken en dips op basis van hoe ver Hallo datapoints zijn van hun gemiddelde |*zspikedetector.Sensitivity:* nemen geheel getal in Hallo bereik 1-10-standaard: 3; Hogere waarden wordt onderschept meer extreme waarden, zodat u minder gevoelig |ZSpike: binaire waarden: '1' als een piek/dip wordt gedetecteerd, '0' anders | |
| Detectie van trage Trend |Detectie van trage Trend |Detecteren van trage positieve trend volgens Hallo set gevoeligheid |*trenddetector.Sensitivity:* drempelwaarde bij detectie score (standaard: 3,25, 3,25 – 5 is een redelijke bereik tooselect dit van; Hallo hoger Hallo minder gevoelig) |tscore: getal met drijvende voor afwijkingsdetectie score op trend |
| De detectoren niveau wijzigen | Detectie van bidirectionele niveau wijzigen |Omhoog en omlaag niveau wijzigen volgens Hallo set gevoeligheid detecteren |*bileveldetector.Sensitivity:* drempelwaarde bij detectie score (standaard: 3,25, 3,25 – 5 is een redelijke bereik tooselect dit van; Hallo hoger Hallo minder gevoelig) |rpscore: getal met drijvende voor afwijkingsdetectie score op omhoog en omlaag niveau wijzigen | |

### <a name="parameters"></a>Parameters
Meer gedetailleerde informatie over deze invoerparameters wordt weergegeven in onderstaande tabel voor Hallo:

| Invoerparameters | Beschrijving | Standaardinstelling | Type | Het geldige bereik | Voorgestelde bereik |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Geschiedenis (in het aantal gegevenspunten) gebruikt voor afwijkingsdetectie score berekeningen |500 |geheel getal |10-2000 |Afhankelijk van de tijdreeks |
| detectors.spikesdips | Hiermee wordt aangegeven of toodetect alleen bereikt, alleen dips of beide |Beide |opgesomd |Beide, Bronblokkades, Dips |Beide |
| bileveldetector.Sensitivity |Gevoeligheid voor bidirectionele niveau wijzigen detectie. |3.25 |dubbele |Geen |3,25-5 (minder waarden betekenen gevoeliger) |
| trenddetector.Sensitivity |Gevoeligheid voor positieve trend detectie. |3.25 |dubbele |Geen |3,25-5 (minder waarden betekenen gevoeliger) |
| tspikedetector.Sensitivity |Gevoeligheid voor TSpike detectie |3 |geheel getal |1-10 |3-5 (minder waarden betekenen gevoeliger) |
| zspikedetector.Sensitivity |Gevoeligheid voor ZSpike detectie |3 |geheel getal |1-10 |3-5 (minder waarden betekenen gevoeliger) |
| postprocess.tailRows |Nummer van de meest recente gegevens Hallo verwijst toobe in Hallo uitvoer resultaten behouden |0 |geheel getal |0 (Houd alle gegevenspunten), of geef het aantal punten tookeep in resultaten |N.v.t. |

### <a name="output"></a>Uitvoer
Hallo API alle detectoren op de reeksgegevens tijd wordt uitgevoerd en retourneert afwijkingsdetectie scores en binaire piek indicatoren voor elk punt in tijd. Hallo tabel ziet u uitvoer van Hallo API. 

| uitvoer | Beschrijving |
| --- | --- |
| Time |Tijdstempels van onbewerkte gegevens, of geaggregeerde (en/of) impliciete gegevens als aggregatie (en/of) ontbreekt begrip van de gegevens wordt toegepast |
| Gegevens |Waarden van onbewerkte gegevens, of geaggregeerde (en/of) impliciete gegevens als aggregatie (en/of) ontbreekt begrip van de gegevens wordt toegepast |
| TSpike |Binaire indicator tooindicate of een piek wordt gedetecteerd door TSpike detectie |
| ZSpike |Binaire indicator tooindicate of een piek wordt gedetecteerd door ZSpike detectie |
| rpscore |Een zwevend nummer dat afwijkingsdetectie beoordelen op wijzigingen in twee richtingen |
| rpalert |1/0-waarde die aangeeft er is een niveau van bidirectionele wijzigen op basis van de invoer gevoeligheid Hallo afwijkingsdetectie |
| tscore |Een zwevend nummer dat afwijkingsdetectie beoordelen op positieve trend |
| talert |1/0-waarde die aangeeft er is een positieve trend afwijkingsdetectie op basis van Hallo invoer gevoeligheid |

## <a name="scorewithseasonality-api"></a>ScoreWithSeasonality API
Hallo ScoreWithSeasonality API wordt gebruikt voor het uitvoeren van de afwijkingsdetectie op timeseries waarvoor de seizoensgebonden patronen. Deze API is nuttig toodetect afwijkingen in de seizoensgebonden patronen.  
Hallo toont volgende afbeelding een voorbeeld van afwijkingen gedetecteerd in een seizoen tijdreeks. Hallo tijdreeks heeft een piek (Hallo 1e zwarte stip), twee dips (Hallo 2e zwarte stip en één aan Hallo einde) en één niveau wijzigen (rode stip). Houd er rekening mee dat zowel dip in het midden van de tijdreeks Hallo HALLO hallo en Hallo de wijzigingen zijn alleen discernable nadat seizoensgebonden onderdelen zijn verwijderd uit Hallo-serie.
![Seizoensgebonden API][2]

### <a name="detectors"></a>Detectoren
Hallo detectoren in Hallo seizoensgebonden eindpunt zijn vergelijkbaar toohello die in Hallo niet seizoensgebonden eindpunt, maar met verschillende parameternamen (Zie hieronder).

### <a name="parameters"></a>Parameters

Meer gedetailleerde informatie over deze invoerparameters wordt weergegeven in onderstaande tabel voor Hallo:

| Invoerparameters | Beschrijving | Standaardinstelling | Type | Het geldige bereik | Voorgestelde bereik |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Aggregatie-interval in seconden voor het verzamelen van de tijdreeks invoer |0 (geen aggregatie wordt uitgevoerd) |geheel getal |0: aggregatie > 0 anders overslaan |5 minuten too1 dag, afhankelijk van de tijdreeks |
| preprocess.aggregationFunc |Functie gebruikt voor het verzamelen van gegevens in Hallo opgegeven AggregationInterval |gemiddelde |opgesomd |gemiddelde, sum, lengte |N.v.t. |
| preprocess.replaceMissing |Waarden van de ontbrekende gegevens tooimpute gebruikt |lkv (laatst bekende waarde) |opgesomd |nul, lkv, gemiddelde |N.v.t. |
| detectors.historyWindow |Geschiedenis (in het aantal gegevenspunten) gebruikt voor afwijkingsdetectie score berekeningen |500 |geheel getal |10-2000 |Afhankelijk van de tijdreeks |
| detectors.spikesdips | Hiermee wordt aangegeven of toodetect alleen bereikt, alleen dips of beide |Beide |opgesomd |Beide, Bronblokkades, Dips |Beide |
| bileveldetector.Sensitivity |Gevoeligheid voor bidirectionele niveau wijzigen detectie. |3.25 |dubbele |Geen |3,25-5 (minder waarden betekenen gevoeliger) |
| postrenddetector.Sensitivity |Gevoeligheid voor positieve trend detectie. |3.25 |dubbele |Geen |3,25-5 (minder waarden betekenen gevoeliger) |
| negtrenddetector.Sensitivity |Gevoeligheid voor negatieve trend detectie. |3.25 |dubbele |Geen |3,25-5 (minder waarden betekenen gevoeliger) |
| tspikedetector.Sensitivity |Gevoeligheid voor TSpike detectie |3 |geheel getal |1-10 |3-5 (minder waarden betekenen gevoeliger) |
| zspikedetector.Sensitivity |Gevoeligheid voor ZSpike detectie |3 |geheel getal |1-10 |3-5 (minder waarden betekenen gevoeliger) |
| seasonality.Enable |Of seizoensgebonden analyse toobe is uitgevoerd |De waarde True |Booleaanse waarde |True, false |Afhankelijk van de tijdreeks |
| seasonality.numSeasonality |Maximum aantal cycli periodieke toobe gedetecteerd |1 |geheel getal |1, 2 |1-2 |
| seasonality.transform |Of seizoensgebonden (en) trend onderdelen moeten worden verwijderd voordat u afwijkingsdetectie |deseason |opgesomd |None, deseason, deseasontrend |N.v.t. |
| postprocess.tailRows |Nummer van de meest recente gegevens Hallo verwijst toobe in Hallo uitvoer resultaten behouden |0 |geheel getal |0 (Houd alle gegevenspunten), of geef het aantal punten tookeep in resultaten |N.v.t. |

### <a name="output"></a>Uitvoer
Hallo API alle detectoren op de reeksgegevens tijd wordt uitgevoerd en retourneert afwijkingsdetectie scores en binaire piek indicatoren voor elk punt in tijd. Hallo tabel ziet u uitvoer van Hallo API. 

| uitvoer | Beschrijving |
| --- | --- |
| Time |Tijdstempels van onbewerkte gegevens, of geaggregeerde (en/of) impliciete gegevens als aggregatie (en/of) ontbreekt begrip van de gegevens wordt toegepast |
| OriginalData |Waarden van onbewerkte gegevens, of geaggregeerde (en/of) impliciete gegevens als aggregatie (en/of) ontbreekt begrip van de gegevens wordt toegepast |
| ProcessedData |Een van de volgende Hallo: <ul><li>Afhankelijk van het seizoen tijdreeks aangepast als aanzienlijke seizoensgebonden is gedetecteerd en deseason optie geselecteerd.</li><li>afhankelijk van het seizoen aangepast en detrended tijdreeks of aanzienlijke seizoensgebonden is gedetecteerd en deseasontrend optie is geselecteerd</li><li>anders wordt is dit hetzelfde als OriginalData Hallo</li> |
| TSpike |Binaire indicator tooindicate of een piek wordt gedetecteerd door TSpike detectie |
| ZSpike |Binaire indicator tooindicate of een piek wordt gedetecteerd door ZSpike detectie |
| BiLevelChangeScore |Een zwevend nummer dat afwijkingsdetectie beoordelen op niveau wijzigen |
| BiLevelChangeAlert |1/0-waarde die aangeeft er is een niveau wijzigen afwijkingsdetectie op basis van Hallo invoer gevoeligheid |
| PosTrendScore |Een zwevend nummer dat afwijkingsdetectie beoordelen op positieve trend |
| PosTrendAlert |1/0-waarde die aangeeft er is een positieve trend afwijkingsdetectie op basis van Hallo invoer gevoeligheid |
| NegTrendScore |Een zwevend nummer dat afwijkingsdetectie beoordelen op negatieve trend |
| NegTrendAlert |1/0-waarde die aangeeft er is een negatieve trend afwijkingsdetectie op basis van Hallo invoer gevoeligheid |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

