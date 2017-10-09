---
title: 'Machine Learning aanbevelingen: JavaScript-integratie | Microsoft Docs'
description: Azure Machine Learning aanbevelingen - integratie van JavaScript - documentatie
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Aanbevelingen voor Azure Machine Learning - JavaScript-integratie
> [!NOTE]
> U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie. Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
> Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)
> 
> 

Dit document weer hoe toointegrate uw site met JavaScript. Hallo JavaScript kunt u toosend gegevens overname gebeurtenissen en tooconsume aanbevelingen als u een aanbeveling model maakt. Alle bewerkingen die worden uitgevoerd via JS kunnen ook worden gedaan vanuit serverzijde.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Algemeen-overzicht
Uw site integreren met Azure ML aanbevelingen bestaan op 2 fasen:

1. Gebeurtenissen verzenden naar Azure ML-aanbevelingen. Hiermee schakelt u toobuild een aanbeveling-model.
2. Hallo aanbevelingen in beslag nemen. Nadat het Hallo-model is gebouwd kunt u Hallo aanbevelingen verbruiken. (Dit document wordt niet uitgelegd hoe toobuild een model lezen Hallo tooget voor snel starten-handleiding voor meer informatie over het).

<ins>Fase I</ins>

Eerste fase die u wilt invoegen in uw HTML-pagina's een kleine JavaScript-bibliotheek waarmee Hallo in Hallo toosend gebeurtenissen op pagina als deze problemen op Hallo HTML-pagina in de Azure ML aanbevelingen-servers (via Data markt optreden):

![Tekening1][1]

<ins>Fase II</ins>

Hallo Selecteer tweede fase als u wilt dat tooshow Hallo aanbevelingen op Hallo pagina u in een Hallo volgende opties:

1. de server (op het Hallo-fase van de paginaweergave) roept Azure ML aanbevelingen Server (via Data markt) tooget aanbevelingen. Hallo resultaten bevatten een lijst met items-id. Uw server moet tooenrich Hallo resultaten Hallo items, metagegevens (bijvoorbeeld afbeeldingen, beschrijving) en pagina toohello browser gemaakt Hallo verzenden.

![Drawing2][2]

2. hello is andere optie toouse Hallo klein JavaScript-bestand van fase één tooget een eenvoudige lijst met aanbevolen items. Hallo gegevens ontvangen hier is minder dan Hallo in de eerste optie Hallo complex.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Vereisten
1. Maak een nieuw model met Hallo API's. Zie de Snelstartgids Hallo over het toodo deze.
2. Codeer uw &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; met base64. (Dit wordt gebruikt voor Hallo basisverificatie tooenable Hallo JS code toocall Hallo API's).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Verzenden van gegevens overname gebeurtenissen met JavaScript
Hallo stappen te volgen vergemakkelijken verzenden gebeurtenissen:

1. JQuery-bibliotheek opnemen in uw code. U kunt dit downloaden van nuget in Hallo URL te volgen.
   
     http://www.nuget.org/Packages/jQuery/1.8.2
2. Hallo aanbevelingen JavaScript-bibliotheek van Hallo volgende URL: http://aka.ms/RecoJSLib1
3. Aanbevelingen voor Azure ML-bibliotheek met de juiste parameters Hallo initialiseren.
   
     <script>AzureMLRecommendationsStart ('<base64encoding of username:key>', "< model_id >"); </script> 
4. Gebeurtenis Hallo verzenden. Zie het detailgedeelte hieronder op alle typen gebeurtenissen (voorbeeld van Klik gebeurtenis) <script> als (typeof AzureMLRecommendationsEvent == 'undefined') {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Beperkingen en ondersteuning van browsers
Dit is een verwijzing implementatie en krijgt, omdat de. Deze moet alle belangrijke browsers ondersteunen.

### <a name="32----type-of-events"></a>3.2.    Type van gebeurtenissen
Er zijn 5 typen gebeurtenissen die bibliotheek ondersteunt Hallo: klikt u op, aanbeveling op klikt, tooShop winkelwagen, toevoegen verwijderen uit de winkelwagen Shop en aankoop. Er is een extra gebeurtenis die is gebruikt tooset Hallo gebruikerscontext aanmelding aangeroepen.

#### <a name="321-click-event"></a>3.2.1. Klik op gebeurtenis
Deze gebeurtenis moet worden gebruikt als elk gewenst moment een gebruiker op een item wordt geklikt. Meestal wanneer de gebruiker klikt op een item wordt een nieuwe pagina geopend met Hallo itemgegevens; Deze gebeurtenis moet worden gestart op deze pagina.

Parameters:

* gebeurtenis (string, verplichte) 'Klik'
* item (string, verplichte) - de unieke id van het Hallo-item
* itemName (string, optioneel) - Hallo-naam van Hallo-item
* itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item
* itemCategory (string, optioneel) - Hallo categorie van het Hallo-item
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Of met optionele gegevens:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Aanbeveling klikt u op de gebeurtenis
Deze gebeurtenis moet worden gebruikt als elk gewenst moment een gebruiker op een item dat is ontvangen van Azure ML aanbevelingen als een aanbevolen item wordt geklikt. Meestal wanneer de gebruiker klikt op een item wordt een nieuwe pagina geopend met Hallo itemgegevens; Deze gebeurtenis moet worden gestart op deze pagina.

Parameters:

* gebeurtenis (string, verplichte) 'recommendationclick'
* item (string, verplichte) - de unieke id van het Hallo-item
* itemName (string, optioneel) - Hallo-naam van Hallo-item
* itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item
* itemCategory (string, optioneel) - Hallo categorie van het Hallo-item
* zaden (string-matrix, optioneel) - Hallo zaden die Hallo aanbeveling query gegenereerd.
* recoList (string-matrix, optioneel) - Hallo resultaat van Hallo aanbeveling aanvraag die gegenereerd Hallo-item waarop is geklikt.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Of met optionele gegevens:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Winkelwagen winkelwagen gebeurtenis toevoegen
Deze gebeurtenis moet worden gebruikt wanneer Hallo gebruiker een item toohello winkelwagen toevoegt.
Parameters:

* gebeurtenis (string, verplichte) 'addshopcart'
* item (string, verplichte) - de unieke id van het Hallo-item
* itemName (string, optioneel) - Hallo-naam van Hallo-item
* itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item
* itemCategory (string, optioneel) - Hallo categorie van het Hallo-item
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Verwijder winkelen winkelwagen gebeurtenis
Deze gebeurtenis moet worden gebruikt wanneer Hallo gebruiker een item toohello-winkelwagen verwijdert.

Parameters:

* gebeurtenis (string, verplichte) 'removeshopcart'
* item (string, verplichte) - de unieke id van het Hallo-item
* itemName (string, optioneel) - Hallo-naam van Hallo-item
* itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item
* itemCategory (string, optioneel) - Hallo categorie van het Hallo-item
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Aankoop gebeurtenis
Deze gebeurtenis moet worden gebruikt wanneer het Hallo-gebruiker zijn winkelwagen hebt aangeschaft.

Parameters:

* gebeurtenis (tekenreeks) - 'kopen'
* objecten (aangekocht []) - matrix met een vermelding voor elk item hebt aangeschaft.<br><br>
  Gekochte indeling:
  * item (tekenreeks) - de unieke id van het Hallo-item.
  * aantal (int of string) - aantal items dat is aangeschaft.
  * prijs (float of tekenreeks) - optioneel veld - Hallo prijs van Hallo-item.

Hallo in het volgende voorbeeld toont de aankoop van 3 items (33, 34, 35), twee met alle velden ingevuld (item, count, prijs) en één (item 34) zonder een prijs.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Gebruikersgebeurtenis-aanmelding
Azure ML aanbevelingen gebeurtenis bibliotheek maakt en gebruikt een cookie in volgorde tooidentify gebeurtenissen die afkomstig zijn van Hallo dezelfde browser. In volgorde tooimprove Hallo model kunnen resultaten Azure ML aanbevelingen tooset een unieke gebruikers-id die het gebruik van Hallo cookie overschrijft.

Deze gebeurtenis moet worden gebruikt na Hallo gebruiker aanmelding tooyour site.

Parameters:

* gebeurtenis (tekenreeks) - 'userlogin'
* gebruiker (tekenreeks) - unieke identificatie van het Hallo-gebruiker.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Aanbevelingen via JavaScript gebruiken
Hallo-code die Hallo aanbeveling verbruikt wordt door sommige JavaScript-gebeurtenis geactiveerd door webpagina Hallo-client. Hallo aanbeveling antwoord bevat Hallo aanbevolen items-id's, namen en hun classificatie. Het is aanbevolen toouse deze optie alleen voor een lijst weergeven van Hallo aanbevolen items - complexere verwerken (zoals het toevoegen van het item Hallo metagegevens) moet worden gedaan op Hallo server side-integratie.

### <a name="41-consume-recommendations"></a>4.1 aanbevelingen gebruiken
tooconsume aanbevelingen moet u tooinclude Hallo vereist JavaScript-bibliotheken in uw pagina en toocall AzureMLRecommendationsStart. Zie de sectie 2.

tooconsume aanbevelingen voor een of meer items moet u een methode aangeroepen toocall: AzureMLRecommendationsGetI2IRecommendation.

Parameters:

* Een of meer items tooget aanbevelingen voor de (matrix met tekenreeksen) - artikelen. Als u een build Fbt verbruiken kunt vervolgens u instellen hier slechts één item.
* numberOfResults (int) - aantal vereiste resultaten.
* includeMetadata (boolean, optioneel) - als too'true ingesteld ' geeft aan dat Hallo metagegevens-veld moet gevuld worden in Hallo resultaat.
* Verwerking van de functie, een functie die wordt afgehandeld Hallo aanbevelingen geretourneerd. Hallo-gegevens worden geretourneerd als een matrix met:
  * Artikel - item unieke id
  * naam - item naam (indien aanwezig zijn in de catalogus)
  * beoordeling - aanbeveling waardering
  * metagegevens - een tekenreeks met metagegevens Hallo Hallo-item

Voorbeeld: 8 aanbevelingen voor het item '64f6eb0d-947a-4c18-a16c-888da9e228ba' hello na de code-aanvragen (en op te geven niet includeMetadata - wordt impliciet aangegeven dat er geen metagegevens vereist is), het Hallo-resultaten vervolgens samenvoegen in een buffer.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
