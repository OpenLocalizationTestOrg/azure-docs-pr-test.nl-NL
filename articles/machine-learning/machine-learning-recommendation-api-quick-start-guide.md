---
title: 'Snel aan de slag: Azure Machine Learning aanbevelingen API (versie 1) | Microsoft Docs'
description: Azure Machine Learning-aanbevelingen - snelstartgids
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Quick start guide voor Hallo Machine Learning aanbevelingen API (versie 1)

> [!NOTE]
> U moet beginnen met behulp van Hallo [cognitieve aanbevelingen API-Service](https://www.microsoft.com/cognitive-services/recommendations-api) in plaats van deze versie. Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
>
> Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate).
> 
> 

Dit document wordt beschreven hoe tooonboard uw service of toepassing toouse aanbevelingen van Microsoft Azure Machine Learning. U vindt meer informatie op Hallo aanbevelingen API in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Algemeen overzicht
Azure Machine Learning aanbevelingen toouse, moet u tootake Hallo stappen te volgen:

* Een model maken: een model is een container van uw gegevens over het gebruik, catalogusgegevens en Hallo aanbeveling model.
* Gegevens importeren catalogus - een catalogus bevat informatie over de metagegevens op Hallo items. 
* Gebruiksgegevens importeren - gebruiksgegevens kunnen worden geüpload in twee manieren (of beide):
  * Door het uploaden van een bestand met gebruiksgegevens Hallo.
  * Door het verzenden van gegevens overname gebeurtenissen.
    Meestal u een bestand voor gebruik in volgorde toobe kunnen toocreate een eerste aanbeveling model (bootstrap) uploaden en deze gebruiken totdat Hallo systeem voldoende gegevens worden verzameld met behulp van Hallo overname gegevensindeling.
* Een aanbeveling model bouwen: dit is een asynchrone bewerking in welke Hallo aanbeveling system neemt alle Hallo gebruiksgegevens en maakt een aanbeveling-model. Deze bewerking kan enkele minuten duren of enkele uren, afhankelijk van het Hallo-grootte van het Hallo-gegevens en Hallo configuratieparameters bouwen. Wanneer activering Hallo build, krijgt u een build-ID. Gebruik deze methode toocheck als Hallo build-proces is beëindigd voordat u begint tooconsume aanbevelingen.
* Aanbevelingen - Get-aanbevelingen voor een specifiek item of de lijst met items in beslag nemen.

Alle Hallo stappen hierboven worden gedaan door hello Azure Machine Learning aanbevelingen API.  U kunt een voorbeeldtoepassing die u implementeert op elk van deze stappen uit Hallo downloaden [ook galerie.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Beperkingen
* Hallo maximumaantal modellen per abonnement is 10.
* maximum aantal items dat een catalogus kan bevatten Hallo is 100.000.
* maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000. Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.
* Hallo maximale grootte van gegevens die kunnen worden verzonden in POST (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200MB.
* Hallo aantal transacties per seconde voor een aanbeveling model-build die niet actief is ~ 2TPS. Een aanbeveling model build actieve kan up too20TPS bevatten.

## <a name="integration"></a>Integratie
### <a name="authentication"></a>Authentication
Microsoft Azure Marketplace biedt ondersteuning voor beide Hallo Basic of OAuth-verificatiemethode. Kunt u gemakkelijk vinden Hallo toegangscodes door te navigeren toohello sleutels in Hallo marketplace onder [uw accountinstellingen](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Basisverificatie
Hallo-autorisatie-header toevoegen:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

TooBase64 converteren (C#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

TooBase64 converteren (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>Service-URI
Hallo-hoofdmap URI voor hello Azure Machine Learning aanbevelingen API's is [hier.](https://api.datamarket.azure.com/amla/recommendations/v2/)

Hallo volledige service-URI wordt uitgedrukt met behulp van elementen van Hallo OData-specificatie.

### <a name="api-version"></a>API-versie
Elke API-aanroep heeft, aan het einde van Hallo een queryparameter aangeroepen apiVersion die moet worden ingesteld te "1.0".

### <a name="ids-are-case-sensitive"></a>Id's zijn hoofdlettergevoelig
Id's die wordt geretourneerd door een van de Hallo-API's, zijn hoofdlettergevoelig en moeten als zodanig worden gebruikt als als parameters doorgegeven in de volgende API-aanroepen. Bijvoorbeeld, zijn model-id's en de catalogus-id's hoofdlettergevoelig.

### <a name="create-a-model"></a>Een model maken
Het maken van een aanvraag 'model maken':

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| modelName |Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.<br>Maximale lengte: 20 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

* `feed/entry/content/properties/id`-Bevat Hallo model-ID.
  Houd er rekening mee dat Hallo model-ID hoofdlettergevoelig is.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a>Gegevens van de catalogus importeren
Als u verschillende catalogus bestanden toohello dezelfde model met verschillende aanroepen uploadt, wordt er alleen Hallo nieuwe catalogusitems ingevoegd. Bestaande items blijft met de oorspronkelijke waarden Hallo.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| bestandsnaam |Tekstuele Hallo catalogus-ID.<br>Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Data Catalog. Indeling:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Naam</th><th>Verplicht</th><th>Type</th><th>Beschrijving</th></tr><tr><td>Artikel-Id</td><td>Ja</td><td>Alfanumeriek, max lengte 50</td><td>De unieke id van een item</td></tr><tr><td>De itemnaam van het</td><td>Ja</td><td>Alfanumeriek, max lengte 255</td><td>De itemnaam van het</td></tr><tr><td>Item categorie</td><td>Ja</td><td>Alfanumeriek, max lengte 255</td><td>Categorie toowhich die dit item behoort (bijvoorbeeld koken Books Drama...)</td></tr><tr><td>Beschrijving</td><td>Nee</td><td>Alfanumeriek, maximale lengte van 4000</td><td>Beschrijving van dit item</td></tr></table><br>Maximale bestandsgrootte is 200MB.<br><br>Voorbeeld:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Antwoord**:

HTTP-statuscode: 200

* `Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.
* `Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>De gebruiksgegevens importeren
#### <a name="uploading-a-file"></a>Uploaden van een bestand
Deze sectie wordt beschreven hoe de gebruiksgegevens tooupload met behulp van een bestand. U kunt deze API is meerdere keren met gebruiksgegevens aanroepen. Alle gebruiksgegevens worden opgeslagen voor alle aanroepen.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| bestandsnaam |Tekstuele Hallo catalogus-ID.<br>Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Gebruiksgegevens. Indeling:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Naam</th><th>Verplicht</th><th>Type</th><th>Beschrijving</th></tr><tr><td>Gebruikers-Id</td><td>Ja</td><td>Alfanumeriek</td><td>De unieke id van een gebruiker</td></tr><tr><td>Artikel-Id</td><td>Ja</td><td>Alfanumeriek, max lengte 50</td><td>De unieke id van een item</td></tr><tr><td>Time</td><td>Nee</td><td>Datum in de notatie: jjjj/MM/ddTUU (bijvoorbeeld 2013/06/20T10:00:00)</td><td>Tijd van gegevens</td></tr><tr><td>Gebeurtenis</td><td>Nee, indien opgegeven, en vervolgens datum moet ook worden geplaatst</td><td>Een van de volgende Hallo:<br>• Klik<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Aankoop</td><td></td></tr></table><br>Maximale bestandsgrootte is 200MB.<br><br>Voorbeeld:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Antwoord**:

HTTP-statuscode: 200

* `Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.
* `Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.
* `Feed\entry\content\properties\FileId`-Id van het bestand.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>Met behulp van de gegevens verkrijgen
Deze sectie wordt beschreven hoe toosend gebeurtenissen in real time tooAzure Machine Learning aanbevelingen meestal van uw website.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Gebeurtenis gegevensinvoer voor elke gebeurtenis die u wilt toosend. Voor hello dezelfde gebruiker of browser sessie Hallo dezelfde ID in het Hallo-sessie-id-veld moet worden verzonden. (Zie het voorbeeld van de hoofdtekst van de gebeurtenis is hieronder). |

* Voorbeeld voor gebeurtenis 'Klik':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Voorbeeld voor gebeurtenis 'RecommendationClick':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Voorbeeld voor gebeurtenis 'AddShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Voorbeeld voor gebeurtenis 'RemoveShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Voorbeeld voor gebeurtenis 'Aankoop':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* Voorbeeld '2 gebeurtenissen op' en 'AddShopCart' verzenden:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Antwoord**: HTTP-statuscode: 200

### <a name="build-a-recommendation-model"></a>Een aanbeveling model bouwen
| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| userDescription |Tekstuele Hallo catalogus-ID. Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet. Zie het bovenstaande voorbeeld.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Dit is een asynchrone API. U krijgt een build-ID als antwoord. tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen. Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.

U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.

Geldige build-status:

* Maken – Model is gemaakt.
* In de wachtrij: Model build is geactiveerd en deze in de wachtrij staat.
* Gebouw – Model wordt samengesteld.
* Geslaagde – Build is beëindigd.
* Fout: Build beëindigd met een fout.
* Geannuleerd – is Build geannuleerd.
* Annuleren – Build wordt geannuleerd.

Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a>Status van een model bouwen ophalen
| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| onlyLastBuild |Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen. |
| apiVersion |1.0 |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per build. Elk item heeft Hallo gegevens te volgen:

* `feed/entry/content/properties/UserName`– Naam van de gebruiker Hallo.
* `feed/entry/content/properties/ModelName`– Naam van Hallo-model.
* `feed/entry/content/properties/ModelId`– De unieke id van het model.
* `feed/entry/content/properties/IsDeployed`– Of Hallo build (ook wordt geïmplementeerd actieve build).
* `feed/entry/content/properties/BuildId`– De unieke id maken.
* `feed/entry/content/properties/BuildType`-Type van Hallo build.
* `feed/entry/content/properties/Status`– Status maken. Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, Canceling, geannuleerd, geslaagd
* `feed/entry/content/properties/StatusMessage`– Gedetailleerde statusbericht (geldt alleen toospecific statussen).
* `feed/entry/content/properties/Progress`– Bouwen voortgang (%).
* `feed/entry/content/properties/StartTime`– Begintijd build.
* `feed/entry/content/properties/EndTime`– Eindtijd bouwen.
* `feed/entry/content/properties/ExecutionTime`– Duur maken.
* `feed/entry/content/properties/ProgressStep`– Details over de huidige fase Hallo die een build uitgevoerd in.

Geldige build-status:

* Gemaakt – is de vermelding van de Build-verzoek gemaakt.
* In de wachtrij: aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.
* Gebouw – Build is bezig.
* Geslaagde – Build is beëindigd.
* Fout: Build beëindigd met een fout.
* Geannuleerd – is Build geannuleerd.
* Annuleren – Build wordt geannuleerd.

Geldige waarden voor de BuildType:

* Positie - positie bouwen. (Voor positie bouwen details, raadpleegt u toohello 'Aanbeveling van Machine Learning API-documentatie' document).
* Aanbeveling - aanbeveling build.
* FBT - vaak samen build hebt gekocht.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a>Aanbevelingen ophalen
| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| ItemID 's |Door komma's gescheiden lijst met Hallo items toorecommend voor.<br>Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redenering (bijvoorbeeld aanbeveling uitleg).

OData-XML

Hallo voorbeeld hieronder reactie omvat 10 aanbevolen artikelen:

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a>Model bijwerken
U kunt Hallo Modelbeschrijving van update of Hallo active build-ID.
*ID van de actieve build* -elke build voor elk model heeft een build-ID. Hallo active build-ID is Hallo eerste geslaagde build van elke nieuwe model. Wanneer u een actieve build-ID hebt en u extra builds voor Hallo doen hetzelfde model, moet u tooexplicitly ingesteld dat deze zoals hello standaard bouwen ID als u wilt. Wanneer u aanbevelingen gebruiken als u geen opgeeft Hallo build-ID die u wilt dat toouse, Hallo standaard één automatisch zal worden gebruikt.

Dit mechanisme kunt u - zodra u een aanbeveling-model in productie - toobuild nieuwe modellen hebt en te testen voordat u ze promoveert tooproduction.

| HTTP-methode | URI |
|:--- |:--- |
| PLAATSEN |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| id |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Houd er rekening mee dat Hallo XML-beschrijving tags en ActiveBuildId zijn optioneel. Als u niet dat tooset beschrijving of ActiveBuildId wilt, moet u de volledige code Hallo verwijderen. |

**Antwoord**:

HTTP-statuscode: 200

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Juridische informatie
Dit document wordt geleverd ' as-is '. Informatie en inzichten die in dit document, inclusief URL's en andere websiteverwijzingen, kunnen zonder kennisgeving worden gewijzigd. Enkele voorbeelden die hierin staan zijn uitsluitend ter illustratie en zijn fictief. Er is geen echte verwantschap of relatie is bedoeld of moet worden afgeleid. Dit document biedt geen u enkel wettelijk recht tooany intellectueel eigendom in een Microsoft-product. U kunt kopiëren en het gebruik van dit document voor eigen referentiedoeleinden. © 2014 Microsoft Corporation. Alle rechten voorbehouden. 

