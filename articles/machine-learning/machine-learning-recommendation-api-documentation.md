---
title: aaaMachine Learning aanbevelingen API-documentatie | Microsoft Docs
description: Azure Machine Learning aanbevelingen API-documentatie voor een beschikbaar is in Microsoft Azure Marketplace Hallo aanbevelingen-engine.
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Documentatie voor Recommendations-API voor Azure Machine Learning
> [!NOTE]
> U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie. Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
> Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)
> 
> 

Dit document beschrijft de Microsoft Azure Machine Learning-aanbevelingen API's.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Algemeen overzicht
Dit document is een API-verwijzing. U moet beginnen met 'Azure Machine Learning aanbeveling--Quick Start' Hallo-document.

Hello Azure Machine Learning aanbevelingen API kan worden onderverdeeld in Hallo logische groepen te volgen:

* <ins>Beperkingen</ins> -aanbevelingen API-beperkingen.
* <ins>Algemene informatie</ins> -informatie over verificatie, service-URI en versiebeheer.
* <ins>Basic model</ins> -API's waarmee u toodo Hallo basisbewerkingen-model (bijvoorbeeld maken, bijwerken en verwijderen van een model).
* <ins>Geavanceerd model</ins> -API's waarmee u geavanceerde tooget gegevens insights Hallo-model.
* <ins>Bedrijfsregels model</ins> -API's waarmee u bedrijfsregels toomanage op Hallo model aanbeveling Resultaten.
* <ins>Catalogus</ins> -API's waarmee u toodo basisbewerkingen op een model-catalogus. Een catalogus bevat informatie over de metagegevens op Hallo items van Hallo gebruiksgegevens.
* <ins>Functie</ins> -API's waarmee tooget insights op item in de catalogus Hallo en hoe toouse deze informatie toobuild betere aanbevelingen.
* <ins>Gebruiksgegevens</ins> -API's waarmee u toodo basisbewerkingen op Hallo model gebruiksgegevens. Gebruiksgegevens in elementaire vorm Hallo bestaat uit rijen met paren &#60; userId &#62; &#60; itemId &#62;.
* <ins>Bouwen</ins> - API's waarmee u een model tootrigger bouwen en bouw basisbewerkingen uit die gerelateerd toothis zijn. Zodra u waardevolle gebruiksgegevens hebt, kunt u een build van het model activeren.
* <ins>Aanbeveling</ins> -API's waarmee u tooconsume aanbevelingen als Hallo build van een model is beëindigd.
* <ins>Gebruikersgegevens</ins> -API's waarmee u informatie toofetch van gebruiksgegevens Hallo-gebruiker.
* <ins>Meldingen</ins> -API's waarmee u tooreceive meldingen op problemen gerelateerde tooyour API-bewerkingen. (Bijvoorbeeld, u gebruiksgegevens via overname van gegevens en de meeste Hallo gebeurtenissen verwerken mislukken rapportage. Een foutmelding weergegeven.)

## <a name="2-limitations"></a>2. Beperkingen
* Hallo maximumaantal modellen per abonnement is 10.
* maximum aantal builds per model Hallo is 20.
* maximum aantal items dat een catalogus kan bevatten Hallo is 100.000.
* maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000. Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.
* Hallo maximale grootte van gegevens die kunnen worden verzonden in POST (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200MB.
* maximum aantal items dat kan worden gevraagd om bij het ophalen van aanbevelingen Hallo is 150.

## <a name="3-apis---general-information"></a>3. API's - algemene informatie
### <a name="31-authentication"></a>3.1. Authentication
Volg de richtlijnen van Microsoft Azure Marketplace Hallo met betrekking tot verificatie. Hallo marketplace biedt ondersteuning voor beide Hallo Basic of OAuth-verificatiemethode.

### <a name="32-service-uri"></a>3.2. Service-URI
Hallo-hoofdmap URI voor hello Azure Machine Learning aanbevelingen API's is [hier.](https://api.datamarket.azure.com/amla/recommendations/v3/)

Hallo volledige service-URI wordt uitgedrukt met behulp van elementen van Hallo OData-specificatie.  

### <a name="33-api-version"></a>3.3. API-versie
Elke API-aanroep heeft aan het einde van Hallo een queryparameter apiVersion die moet worden ingesteld als too1.0 aangeroepen.

### <a name="34-ids-are-case-sensitive"></a>3.4. Id's zijn hoofdlettergevoelig
Id's die wordt geretourneerd door een van de Hallo-API's, zijn hoofdlettergevoelig en moeten als zodanig worden gebruikt als als parameters doorgegeven in de volgende API-aanroepen. Bijvoorbeeld, zijn model-id's en de catalogus-id's hoofdlettergevoelig.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Aanbevelingen voor kwaliteit en koude Items
### <a name="41-recommendation-quality"></a>4.1. Aanbeveling kwaliteit
Maken van een model aanbeveling is meestal voldoende tooallow Hallo system tooprovide aanbevelingen. Evenwel aanbeveling kwaliteit varieert op basis van Hallo gebruik verwerkt en Hallo dekking van Hallo-catalogus. Bijvoorbeeld als er een groot aantal koude artikelen (artikelen zonder aanzienlijke gebruik), Hallo systeem problemen bij het leveren van een aanbeveling voor een dergelijke item of een item gebruiken als een aanbevolen zal hebben. In de volgorde tooovercome Hallo koude item probleem staat Hallo systeem Hallo gebruik van metagegevens van Hallo items tooenhance Hallo aanbevelingen. Deze metagegevens is waarnaar wordt verwezen tooas functies. Typische functies zijn van een boek auteur of een film actor. Functies zijn beschikbaar via Hallo catalogus in de vorm Hallo van sleutel/waarde-tekenreeksen. Voor volledige formattering Hallo van catalogusbestand hello, raadpleegt u toohello [sectie catalogus importeren](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Waarden van positie build
Hallo aanbeveling model kunnen verbeteren van functies, maar toodo dus Hallo gebruik van zinvolle functies vereist. Voor dit doel is een nieuwe build geïntroduceerd - positie maken. Deze versie wordt Hallo nut van functies rangschikken. Een functie stukje zinvolle is een functie met een positie score van 2 en omhoog in.
Na de kennis van die functies Hallo nuttig zijn, een aanbeveling build met lijst hello (of sublijst) van zinvolle functies te activeren. Het is mogelijk toouse die deze functie voor Hallo uitbreiding van zowel warme en koude artikelen. In de volgorde toouse ze voor warme items Hallo `UseFeatureInModel` build-parameter moet worden ingesteld. In de volgorde toouse functies voor koude items, Hallo `AllowColdItemPlacement` build-parameter moet worden ingeschakeld.
Opmerking: Het is niet mogelijk tooenable `AllowColdItemPlacement` zonder in te schakelen `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Aanbeveling redenering
Aanbeveling redenering is een ander aspect van het gebruik van functies. Hello Azure Machine Learning aanbevelingen engine kunt functies tooprovide aanbeveling uitleg immers (ook gebruiken redeneren), aanbevolen voorloop toomore vertrouwen in Hallo item van Hallo aanbeveling consumer.
tooenable redeneren, hello `AllowFeatureCorrelation` en `ReasoningFeatureList` moeten parameters setup voorafgaande toorequesting een aanbeveling build zijn.

## <a name="5-model-basic"></a>5. Model Basic
### <a name="51-create-model"></a>5.1. Model maken
Maakt een aanvraag 'model maken'.

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
  **Opmerking**: model-ID is hoofdlettergevoelig.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a>5.2. Model ophalen
Maakt een 'get-model'-aanvraag.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| id |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo modelgegevens vindt u onder Hallo volgende elementen:

* `feed/entry/content/properties/Id`-De unieke id model.
* `feed/entry/content/properties/Name`-Naam model.
* `feed/entry/content/properties/Date`-Aanmaakdatum model.
* `feed/entry/content/properties/Status`-Status van het model. Een van de volgende Hallo:
  * Gemaakt - Model wordt gemaakt en bevat geen catalogus en informatie over het gebruik.
  * ReadyForBuild - Model wordt gemaakt en bevat Catalog en het gebruik.
* `feed/entry/content/properties/HasActiveBuild`-Geeft aan of Hallo model is gemaakt.
* `feed/entry/content/properties/BuildId`-Model active build-ID.
* `feed/entry/content/properties/Mpr`-Gemiddelde percentiel ranking model (MPR - ModelInsight Zie voor meer informatie).
* `feed/entry/content/properties/UserName`-Naam van de interne gebruiker model.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Ophalen van alle modellen
Hiermee haalt u alle modellen van de huidige gebruiker Hallo.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

* `feed/entry/content/properties/Id`-De unieke id model.
* `feed/entry/content/properties/Name`-Naam model.
* `feed/entry/content/properties/Date`-Aanmaakdatum model.
* `feed/entry/content/properties/Status`-Status van het model. Een van de volgende Hallo:
  * Gemaakt - Model wordt gemaakt en bevat geen catalogus en informatie over het gebruik.
  * ReadyForBuild - Model wordt gemaakt en bevat Catalog en het gebruik.
* `feed/entry/content/properties/HasActiveBuild`-Geeft aan of Hallo model is gemaakt.
* `feed/entry/content/properties/BuildId`-Model active build-ID.
* `feed/entry/content/properties/Mpr`-Model MPR (Zie ModelInsight voor meer informatie).
* `feed/entry/content/properties/UserName`-Naam van de interne gebruiker model.
* `feed/entry/content/properties/UsageFileNames`-Lijst met informatie over het gebruik van modelbestanden gescheiden door komma.
* `feed/entry/content/properties/CatalogId`-Model catalogus-ID.
* `feed/entry/content/properties/Description`-Beschrijving model.
* `feed/entry/content/properties/CatalogFileName`-Bestandsnaam van de model catalogus.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Model bijwerken
U kunt Hallo Modelbeschrijving van update of Hallo active build-ID.<br>
<ins>ID van de actieve build</ins> -elke build voor elk model heeft een build-ID. Hallo active build-ID is Hallo eerste geslaagde build van elke nieuwe model. Wanneer u een actieve build-ID hebt en u extra builds voor Hallo doen hetzelfde model, moet u tooexplicitly ingesteld dat deze zoals hello standaard bouwen ID als u wilt. Wanneer u aanbevelingen gebruiken als u geen opgeeft Hallo build-ID die u wilt dat toouse, Hallo standaard één automatisch zal worden gebruikt.<br>
Dit mechanisme kunt u - zodra u een aanbeveling-model in productie - toobuild nieuwe modellen hebt en te testen voordat u ze promoveert tooproduction.

| HTTP-methode | URI |
|:--- |:--- |
| PLAATSEN |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| id |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Houd er rekening mee dat Hallo XML-beschrijving tags en ActiveBuildId zijn optioneel. Als u niet dat tooset beschrijving of ActiveBuildId wilt, moet u de volledige code Hallo verwijderen. |

**Antwoord**:

HTTP-statuscode: 200

### <a name="55----delete-model"></a>5.5.    Model verwijderen
Hiermee verwijdert u een bestaand model op-ID.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| id |De unieke id van het Hallo-model (hoofdlettergevoelig) |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Geavanceerde model
### <a name="61----model-data-insight"></a>6.1.    Model Data-inzicht
Retourneert de statistische gegevens op Hallo gebruiksgegevens die met dit model is gebouwd.

Alleen beschikbaar voor aanbeveling build.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-gegevens worden geretourneerd als een verzameling eigenschappen.

* `feed/entry/id/content/properties/key`-De naam van de eigenschap Hallo bevat.
* `feed/entry/id/content/properties/value`-Eigenschapswaarde Hallo bevat.

Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.

| Sleutel | Beschrijving |
|:--- |:--- |
| AvgItemLength |Gemiddeld aantal unieke gebruikers per artikel. |
| AvgUserLength |Gemiddelde aantal afzonderlijke items per gebruiker. |
| DensificationNumberOfItems |Aantal items na weghalen items die niet kunnen worden gebracht. |
| DensificationNumberOfUsers |Aantal punten gebruik na weghalen gebruikers en de items die niet kunnen worden gebracht. |
| DensificationNumberOfRecords |Aantal punten gebruik na weghalen gebruikers en de items die niet kunnen worden gebracht. |
| MaxItemLength |Het aantal afzonderlijke gebruikers voor de meest populaire item Hallo. |
| MaxUserLength |Maximale aantal afzonderlijke items voor een gebruiker. |
| MinItemLength |Maximale aantal van afzonderlijke gebruikers voor een item. |
| MinUserLength |Minimum aantal afzonderlijke items voor een gebruiker. |
| RawNumberOfItems |Het aantal items in Hallo gebruiksbestanden. |
| RawNumberOfUsers |Aantal punten voordat alle weghalen gebruik. |
| RawNumberOfRecords |Aantal punten voordat alle weghalen gebruik. |
| SamplingNumberOfItems |N.v.t. |
| SamplingNumberOfRecords |N.v.t. |
| SamplingNumberOfUsers |N.v.t. |

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Model inzicht
Retourneert model inzicht op Hallo active build of (indien opgegeven) een specifieke versie.

Alleen beschikbaar voor aanbeveling build.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |Met de ID van de actieve build:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Met specifieke build-ID:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| buildId |Optioneel - nummer waarmee een geslaagde build. |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-gegevens worden geretourneerd als een verzameling eigenschappen.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.

| Sleutel | Beschrijving |
|:--- |:--- |
| CatalogCoverage |Welk gedeelte van de catalogus Hallo kan worden gebracht met gebruikspatronen. Hallo rest Hallo items moet functies op basis van inhoud. |
| MPR |Gemiddelde percentiel rangschikking van Hallo-model. Kleine is beter. |
| NumberOfDimensions |Het aantal dimensies die worden gebruikt door Hallo matrix factoriseren algoritme. |

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Model Sample ophalen
Hiermee haalt u een voorbeeld van Hallo aanbeveling model.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Met specifieke build-ID:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

OData-XML

Onbewerkte tekst wordt geretourneerd als antwoord:

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Bedrijfsregels model
Dit zijn Hallo typen regels die ondersteund:

* <strong>BlockList</strong> -BlockList kunt u een lijst met items die u niet dat tooreturn in Hallo aanbeveling resultaten wilt tooprovide. 
* <strong>FeatureBlockList</strong> -functie BlockList kunt u tooblock items op basis van Hallo waarden van de functies.

*Meer dan 1000 items in een regel één blocklist niet verzenden of de aanroep kan time-out. Als u tooblock meer dan 1000 items moet, kunt u verschillende blocklist aanroepen.*

* <strong>Upsale</strong> -Upsale kunt u tooenforce items tooreturn in Hallo aanbeveling Resultaten.
* <strong>Geaccepteerde</strong> -witte lijst kunt u tooonly voorstellen aanbevelingen uit een lijst met items.
* <strong>FeatureWhiteList</strong> -functie witte lijst kunt u tooonly aanbevolen items die specifiek functie waarden hebben.
* <strong>PerSeedBlockList</strong> - Per Seed blokkeringslijst schakelt tooprovide per item voor een lijst met items die als aanbeveling resultaten kan niet worden geretourneerd.

### <a name="71----get-model-rules"></a>7.1.    Model-regels ophalen
| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Voorbeeld:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

* `feed/entry/content/properties/Id`-De unieke id van deze regel.
* `feed/entry/content/properties/Type`-Type Hallo regel.
* `feed/entry/content/properties/Parameter`-De parameter regel.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Regel toevoegen
| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| KOPTEKST |`"Content-Type", "text/xml"` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst | |

<ins>Wanneer het bieden van Item-id's voor bedrijfsregels, zorg ervoor dat toouse Hallo externe Hallo item-Id (dezelfde Id die u hebt gebruikt in catalogusbestand Hallo Hallo)</ins><br>
<ins>een regel BlockList tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>een regel FeatureBlockList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>een regel Upsale tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>een regel geaccepteerde tooadd:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>een regel FeatureWhiteList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>een regel PerSeedBlockList tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Antwoord**:

HTTP-statuscode: 200

Hallo API retourneert Hallo regel zojuist hebt gemaakt met de details ervan. Hallo regels eigenschap kan worden opgehaald uit de volgende paden Hallo:

* `feed/entry/content/properties/Id`-De unieke id van deze regel.
* `feed/entry/content/properties/Type`-Type van de regel Hallo: BlockList of Upsale.
* `feed/entry/content/properties/Parameter`-De parameter regel.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Regel verwijderen
| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| filterId |De unieke id van het Hallo-filter |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

### <a name="74----delete-all-rules"></a>7.4.    Alle regels verwijderen
| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

## <a name="8-catalog"></a>8. Catalogus
### <a name="81----import-catalog-data"></a>8.1.    Gegevens van de catalogus importeren
Als u verschillende catalogus bestanden toohello dezelfde model met verschillende aanroepen uploadt, wordt er alleen Hallo nieuwe catalogusitems ingevoegd. Bestaande items blijft met de oorspronkelijke waarden Hallo. U kunt gegevens in de catalogus niet bijwerken met deze methode.

Hallo catalogusgegevens Voer Hallo volgende indeling:

* Zonder functies:`<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* Met functies:`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Opmerking: de maximale bestandsgrootte Hallo is 200MB.

** Details opmaken **

| Naam | Verplicht | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Artikel-Id |Ja |[A-z], [a-z], [0-9] [_] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;<br> Maximale lengte: 50 |De unieke id van een item. |
| De itemnaam van het |Ja |Alle alfanumerieke tekens<br> Maximale lengte: 255 |Naam van het item. |
| Item categorie |Ja |Alle alfanumerieke tekens <br> Maximale lengte: 255 |Categorie toowhich dit item behoort (bijvoorbeeld koken Books, Drama...); kan niet leeg zijn. |
| Beschrijving |Nee, tenzij er functies zijn aanwezig (maar mag leeg zijn) |Alle alfanumerieke tekens <br> Maximale lengte: 4000 |Beschrijving van dit item. |
| Lijst met functies |Nee |Alle alfanumerieke tekens <br> Maximale lengte: 4000; Maximumaantal functies: 20 |Door komma's gescheiden lijst met de functienaam van de = functie-waarde die gebruikt tooenhance model aanbeveling worden kan; Zie [geavanceerde onderwerpen](#2-advanced-topics) sectie. |

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| KOPTEKST |`"Content-Type", "text/xml"` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| bestandsnaam |Tekstuele Hallo catalogus-ID.<br>Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Als u bijvoorbeeld (met functies):<br/>2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, boek, Hallo adresboek beschrijving, auteur = Richard Wright, publisher Harper Flamingo Canada = jaar 2001 =<br>21bf8088-b6c0-4509-870c-e1c7ac78304a, Hallo Forgetting ruimte: A fictie (Byzantium Book), adresboek,, auteur = Nick Bantock, publisher = Harpercollins, jaar 1997 =<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, adresboek,, auteur = Timothy Findley, publisher = HarperFlamingo Canada, jaar 2001 =<br>552a1940-21e4-4399-82bb-594b46d7ed54, beperking van beesten, boek, Hallo adresboek beschrijving, auteur = Magnus Mills, publisher = Arcade Publishing, jaar 1998 =</pre> |

**Antwoord**:

HTTP-statuscode: 200

Hallo API retourneert een rapport van Hallo importeren.

* `feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.
* `feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Catalogus ophalen
Hiermee haalt u alle catalogusitems.
Hallo-catalogus worden opgehaald van één pagina tegelijk. Als u tooget items op een specifieke index wilt, kunt u Hallo $skip odata-parameter. Bijvoorbeeld als u beginnen bij positie 100 tooget-items wilt, voegt u Hallo parameter $skip = 100 toohello-aanvraag.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per catalogusitem. Elk item heeft Hallo gegevens te volgen:

* `feed/entry/content/properties/ExternalId`-Catalogus externe item-ID, geleverd door de klant Hallo Hallo.
* `feed/entry/content/properties/InternalId`-Catalogus item interne ID Hallo die Azure Machine Learning aanbevelingen heeft gegenereerd.
* `feed/entry/content/properties/Name`-De itemnaam catalogus.
* `feed/entry/content/properties/Category`-De rubriek voor object catalogus.
* `feed/entry/content/properties/Description`-Catalogus beschrijving item.
* `feed/entry/content/properties/Metadata`-Catalogus itemmetagegevens.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Catalogusitems door Token ophalen
| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Token |Token van de naam van item Hallo-catalogus. Moet ten minste 3 tekens bevatten. |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per catalogusitem. Elk item heeft Hallo gegevens te volgen:

* `feed/entry/content/properties/InternalId`-Catalogus item interne ID Hallo die Azure Machine Learning aanbevelingen heeft gegenereerd.
* `feed/entry/content/properties/Name`-De itemnaam catalogus.
* `feed/entry/content/properties/Rating`-(voor toekomstig gebruik)
* `feed/entry/content/properties/Reasoning`-(voor toekomstig gebruik)
* `feed/entry/content/properties/Metadata`-(voor toekomstig gebruik)
* `feed/entry/content/properties/FormattedRating`-(voor toekomstig gebruik)

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Gebruiksgegevens
### <a name="91----import-usage-data"></a>9.1.    De gebruiksgegevens importeren
#### <a name="911-uploading-file"></a>9.1.1. Bestand uploaden
Deze sectie wordt beschreven hoe de gebruiksgegevens tooupload met behulp van een bestand. U kunt deze API is meerdere keren met gebruiksgegevens aanroepen. Alle gebruiksgegevens worden opgeslagen voor alle aanroepen.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| bestandsnaam |Tekstuele Hallo catalogus-ID.<br>Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Gebruiksgegevens. Indeling:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Naam</th><th>Verplicht</th><th>Type</th><th>Beschrijving</th></tr><tr><td>Gebruikers-Id</td><td>Ja</td><td>[A-z], [a-z], [0-9] [_] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;<br> Maximale lengte: 255 </td><td>De unieke id van een gebruiker.</td></tr><tr><td>Artikel-Id</td><td>Ja</td><td>[A-z], [a-z], [0-9] [&#95;] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;<br> Maximale lengte: 50</td><td>De unieke id van een item.</td></tr><tr><td>Time</td><td>Nee</td><td>Datum in de notatie: jjjj/MM/ddTUU (bijvoorbeeld 2013/06/20T10:00:00)</td><td>Tijd van de gegevens.</td></tr><tr><td>Gebeurtenis</td><td>Er is geen; Indien opgegeven en klik vervolgens datum moet ook worden geplaatst</td><td>Een van de volgende Hallo:<br>• Klik<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Aankoop</td><td></td></tr></table><br>Maximale bestandsgrootte: 200MB<br><br>Voorbeeld:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Antwoord**:

HTTP-statuscode: 200

* `Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.
* `Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.
* `Feed\entry\content\properties\FileId`-Id van het bestand.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Met behulp van de gegevens verkrijgen
Deze sectie wordt beschreven hoe toosend gebeurtenissen in real time tooAzure Machine Learning aanbevelingen meestal van uw website.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| KOPTEKST |`"Content-Type", "text/xml"` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| apiVersion |1.0 |
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
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
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

### <a name="92----list-model-usage-files"></a>9.2.    Informatie over het gebruik van lijst modelbestanden
Haalt de metagegevens van informatie over het gebruik van alle modelbestanden.
Hallo gebruik van bestanden die zijn opgehaald één pagina tegelijk. Elke pagina containes 100 items. Als u tooget items op een specifieke index wilt, kunt u Hallo $skip odata-parameter. Bijvoorbeeld als u beginnen bij positie 100 tooget-items wilt, voegt u Hallo parameter $skip = 100 toohello-aanvraag.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| forModelId |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per bestand in gebruik. Elk item heeft Hallo gegevens te volgen:

* `feed\entry\content\properties\Id`-Gebruik bestands-id
* `feed\entry\content\properties\Length`-Lengte van de usage bestand in MB.
* `feed\entry\content\properties\DateModified`-Datum wanneer Hallo gebruik bestand is gemaakt.
* `feed\entry\content\properties\UseInModel`-Of Hallo-bestand voor gebruik in Hallo model wordt gebruikt.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Gebruiksstatistieken ophalen
Gebruiksstatistieken opgehaald.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Begindatum |De begindatum. Indeling: jjjj/MM/ddTUU |
| EndDate bevat |Einddatum. Indeling: jjjj/MM/ddTUU |
| eigenschap eventTypes |Door komma's gescheiden tekenreeks van gebeurtenis typen of null tooget alle gebeurtenissen |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Een verzameling van sleutel/waarde-elementen. Elke bevat Hallo som van gebeurtenissen voor een specifiek gebeurtenistype gegroepeerd per uur.

* `feed\entry[i]\content\properties\Key`-Bevat Hallo-tijd (gegroepeerd per uur) en Hallo gebeurtenistype.
* `feed\entry[i]\content\properties\Value`-Het aantal totaal aantal gebeurtenissen.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Gebruik-voorbeeldbestand ophalen
Haalt Hallo eerste 2KB van het gebruik van de inhoud van bestand.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| fileId |De unieke id van de informatie over het gebruik van Hallo modelbestand |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Onbewerkte tekst wordt geretourneerd als antwoord:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Informatie over het gebruik van modelbestand ophalen
Haalt de volledige inhoud Hallo van Hallo gebruik bestand.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Mid |De unieke id van het Hallo-model |
| bestands-id |De unieke id van de informatie over het gebruik van Hallo modelbestand |
| Downloaden |1 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Onbewerkte tekst wordt geretourneerd als antwoord:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Gebruik bestand verwijderen
Hallo opgegeven model gebruik bestand verwijderd.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| fileId |De unieke id van Hallo bestand toobe verwijderd |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Verwijder alle bestanden met gebruiksgegevens
Hiermee verwijdert u alle modelbestanden voor informatie over het gebruik.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

## <a name="10-features"></a>10. Functies
Deze sectie wordt beschreven hoe tooretrieve voorzien van informatie, zoals Hallo geïmporteerd functies en hun waarden, hun positie, en wanneer deze positie is toegewezen. Functies worden geïmporteerd als onderdeel van de catalogusgegevens Hallo en vervolgens hun positie is gekoppeld als het een absolute build is voltooid.
Positie van de functie kunt volgens toohello patroon van gebruiksgegevens en type items wijzigen. Maar voor consistent gebruik/items, Hallo positie hebben slechts kleine schommelingen.
Hallo-positie van functies is een niet-negatief getal. Hallo nummer 0 betekent dat Hallo-functie niet is gerangschikt (gebeurt als u bij het aanroepen van deze API voorafgaande toohello voltooiing van de eerste positie build Hallo). Hallo datum waarop Hallo positie is toegekend, Hallo score nieuwheid wordt genoemd.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Functies Info ophalen (voor laatste positie Build)
Hallo functie informatie, met inbegrip van ranking voor Hallo laatste geslaagde positie build opgehaald.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| samplingSize |Het aantal waarden tooinclude voor elk onderdeel volgens toohello gegevens aanwezig zijn in de catalogus Hallo. <br/>Mogelijke waarden zijn:<br> -1 - alle voorbeelden. <br>0 - geen steekproeven. <br>N - N steekproeven voor de functienaam van elke retourneren. |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat een lijst met functie info vermeldingen. Elk item bevat:

* `feed/entry/content/m:properties/d:Name`-Naam functie.
* `feed/entry/content/m:properties/d:RankUpdateDate`-De datum op welke Hallo positie toegewezen toothis functie, ook is score nieuwheid functie. Een historische datum ('0001-01-01T00:00:00') betekent dat er geen waarden van positie build is uitgevoerd.
* `feed/entry/content/m:properties/d:Rank`-Functie positie (float). Positie van 2.0 en omhoog wordt beschouwd als een goede functie.
* `feed/entry/content/m:properties/d:SampleValues`-Door komma's gescheiden lijst met waarden toohello steekproeven grootte aangevraagd.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Functies Info ophalen (voor een specifieke positie Build)
Hallo functie informatie, met inbegrip van Hallo rangschikking voor een specifieke positie build opgehaald.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| samplingSize |Het aantal waarden tooinclude voor elk onderdeel volgens toohello gegevens aanwezig zijn in de catalogus Hallo.<br/> Mogelijke waarden zijn:<br> -1 - alle voorbeelden. <br>0 - geen steekproeven. <br>N - N steekproeven voor de functienaam van elke retourneren. |
| rankBuildId |De unieke id van de waarden van positie build Hallo of -1 voor de laatste positie build Hallo |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat een lijst met functie info vermeldingen. Elk item bevat:

* `feed/entry/content/m:properties/d:Name`-Naam functie.
* `feed/entry/content/m:properties/d:RankUpdateDate`-De datum op welke Hallo positie toegewezen toothis functie, ook is score nieuwheid functie. Een historische datum ('0001-01-01T00:00:00') betekent dat er geen waarden van positie build is uitgevoerd.
* `feed/entry/content/m:properties/d:Rank`-Functie positie (float). Positie van 2.0 en omhoog wordt beschouwd als een goede functie.
* `feed/entry/content/m:properties/d:SampleValues`-Door komma's gescheiden lijst met waarden toohello steekproeven grootte aangevraagd.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Ontwikkelen
  Deze sectie wordt uitgelegd Hallo verschillende API's toobuilds gerelateerd. Er zijn 3 soorten builds: een aanbeveling build, een positie build en een build FBT (vaak gekocht samen).

Hallo aanbeveling build-doel is een model aanbeveling voor voorspellingen gebruikt toogenerate. Voorspellingen (voor dit type build) er zijn twee versies:

* I2I - ook Item tooItem aanbevelingen - gegeven een item of een lijst van artikelen met deze optie een lijst met items die waarschijnlijk toobe van groot belang zijn wordt voorspellen.
* U2I - ook Gebruiker tooItem aanbevelingen - basis van een gebruikers-id (en optioneel een lijst met items) deze optie wordt een lijst met items die waarschijnlijk toobe van groot belang voor de opgegeven gebruiker (en de aanvullende keuze van items) Hallo zijn voorspellen. Hallo U2I aanbevelingen zijn gebaseerd op Hallo overzicht van items die zijn van belang zijn voor de gebruiker Hallo toohello tijd Hallo model is opgebouwd.

Een positie build is een technische build waarmee u toolearn over Hallo nut van uw functies. Meestal in volgorde tooget Hallo beste resultaat voor een model in aanbeveling met betrekking tot de functies, moet u Hallo stappen uitvoeren:

* Activeren van een absolute build (tenzij een stabiele Hallo score van uw functies) en wacht tot u Hallo functie score ophalen.
* Hallo-positie van uw functies ophalen door de aanroepende Hallo [functies Info ophalen](#101-get-features-info-for-last-rank-build) API.
* Configureer een aanbeveling build met Hallo volgende parameters:
  * `useFeatureInModel`-TooTrue set.
  * `ModelingFeatureList`-Set tooa door komma's gescheiden lijst met functies met een score van 2.0 of meer (op basis van twee of meer toohello die u hebt opgehaald in de vorige stap Hallo).
  * `AllowColdItemPlacement`-TooTrue set.
  * U kunt desgewenst instellen `EnableFeatureCorrelation` tooTrue en `ReasoningFeatureList` toohello eigenschappenlijst gewenste toouse uitleg (meestal hello dezelfde lijst met functies in modellering of een sublijst gebruikt).
* Trigger Hallo aanbeveling build Hello geconfigureerd parameters.

Opmerking: Als u niet alle parameters configureert (bijvoorbeeld aanroepen Hallo aanbeveling build zonder parameters) of u niet expliciet uitschakelt Hallo informatie over het gebruik van functies (bijvoorbeeld `UseFeatureInModel` tooFalse ingesteld), system Hallo Hallo functie-gerelateerde parameters wordt instellen Als een positie build bestaat, worden in toohello waarden die hierboven beschreven.

Er is geen beperking voor het uitvoeren van een absolute build en een aanbeveling build gelijktijdig voor Hallo dezelfde model. U kunt twee versies van dezelfde typt u op dezelfde model parallel Hallo Hallo evenwel niet uitvoeren.

Een build FBT (vaak gekocht samen) is nog een andere aanbevelingen algoritme soms 'conservatief' recommender die geschikt is voor catalogi die niet in aard homogene aangeroepen (homogene: books, films, sommige voeding wijze; niet-homogeen: computer en apparaten, tussen domeinen, zeer diverse).

Opmerking: als hello informatie over het van gebruiksbestanden die u hebt geüpload Hallo optioneel veld 'gebeurtenistype bevatten' vervolgens voor FBT modellering alleen 'Aankoop' gebeurtenissen wordt gebruikt. Als geen gebeurtenistype is opgegeven, dat worden alle gebeurtenissen worden beschouwd als aankoop.

#### <a name="111-build-parameters"></a>11.1 bouwen parameters
Elk BuildType kan worden geconfigureerd via een set parameters (afgebeeld hieronder). Als u Hallo-parameters niet configureert, worden in Hallo system waarden toohello parameters volgens toohello aanwezige informatie Hallo gelijktijdig activeren van een build automatisch kenmerk.

##### <a name="1111-usage-condenser"></a>11.1.1. Gebruik koeler
Gebruikers- of artikelen met enkele gebruik punten bevatten mogelijk meer ruis dan informatie. Hallo-systeem probeert toopredict Hallo minimum aantal gebruik punten per gebruiker/item toobe gebruikt in een model. Dit nummer is binnen het bereik van Hallo gedefinieerd door Hallo ItemCutoffLowerBound en ItemCutoffUpperBound parameters voor artikelen en Hallo bereik dat is gedefinieerd door Hallo UserCutOffLowerBound en UserCutoffUpperBound parameters voor gebruikers. Hallo koeler effect op items of gebruikers kan worden geminimaliseerd door ten minste één van de bijbehorende grenzen toozero Hallo-instelling.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Positie bouwen parameters
Hallo in de volgende tabel beschrijft Hallo build parameters voor een positie build.

| Sleutel | Beschrijving | Type | Geldige waarde |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model. Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren. |Geheel getal |10-50 |
| NumberOfModelDimensions |het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens. Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters. Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items. |Geheel getal |10-40 |
| ItemCutOffLowerBound |Hallo item ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| ItemCutOffUpperBound |Hallo item bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffLowerBound |Hallo gebruiker ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffUpperBound |Hallo gebruiker bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Aanbeveling build parameters
Hallo in de volgende tabel beschrijft Hallo build parameters voor de aanbeveling build.

| Sleutel | Beschrijving | Type | Geldige waarde |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model. Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren. |Geheel getal |10-50 |
| NumberOfModelDimensions |het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens. Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters. Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items. |Geheel getal |10-40 |
| ItemCutOffLowerBound |Hallo item ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| ItemCutOffUpperBound |Hallo item bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffLowerBound |Hallo gebruiker ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffUpperBound |Hallo gebruiker bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| Beschrijving |Beschrijving bouwen. |Tekenreeks |Alle tekst maximaal 512 tekens |
| EnableModelingInsights |Hiermee kunt u toocompute metrische gegevens op Hallo aanbeveling model. |Booleaanse waarde |Waar/onwaar |
| UseFeaturesInModel |Hiermee wordt aangegeven als functies in volgorde tooenhance Hallo aanbeveling model kunnen worden gebruikt. |Booleaanse waarde |Waar/onwaar |
| ModelingFeatureList |Door komma's gescheiden lijst van de functie namen toobe Hallo aanbeveling gebouwd in volgorde tooenhance Hallo aanbeveling gebruikt. |Tekenreeks |Onderdeelnamen up too512 tekens |
| AllowColdItemPlacement |Hiermee wordt aangegeven als Hallo aanbeveling ook koude items via de functie overeenkomsten pushen moet. |Booleaanse waarde |Waar/onwaar |
| EnableFeatureCorrelation |Hiermee wordt aangegeven als functies kunnen worden gebruikt in de redenering. |Booleaanse waarde |Waar/onwaar |
| ReasoningFeatureList |Door komma's gescheiden lijst van de functie namen toobe gebruikt voor redeneren zinnen (bijvoorbeeld aanbeveling uitleg). |Tekenreeks |Onderdeelnamen up too512 tekens |
| EnableU2I |Hallo persoonlijke aanbeveling ook toestaan U2I (gebruiker tooitem recommendations). |Booleaanse waarde |True/False (standaard waar) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. FBT build parameters
Hallo in de volgende tabel beschrijft Hallo build parameters voor de aanbeveling build.

| Sleutel | Beschrijving | Type | Geldige waarde (standaard) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Hoe conservatief Hallo model is. Het aantal mede exemplaren van items toobe in aanmerking voor het model. |Geheel getal |3-50 (6) |
| FbtMaxItemSetSize |Grenzen Hallo aantal items in een set veelvuldig. |Geheel getal |2-3 (2) |
| FbtMinimalScore |Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert. Hallo hoger Hallo beter. |dubbele |0 en hoger (0) |
| FbtSimilarityFunction |Hallo gelijkenis functie toobe gebruikt door Hallo build definieert. Lift Hiermee worden verbeterd serendipity, mede exemplaar Hiermee worden verbeterd voorspelbaarheid en Jaccard is een nice compromis tussen twee Hallo. |Tekenreeks |cooccurrence lift jaccard (lift) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Een aanbeveling Build activeren
  Standaard wordt deze API een aanbeveling build van het model activeren. tootrigger positie bouwen (in volgorde tooscore functies), Hallo build API variant met build typeparameter moet worden gebruikt.

| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| KOPTEKST |`"Content-Type", "text/xml"`(Als aanvraagtekst verzenden) |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| userDescription |Tekstuele Hallo catalogus-ID. Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet. Zie het bovenstaande voorbeeld.<br>Maximale lengte: 50 |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Als dit veld leeg wordt met de standaardparameters voor build Hallo Hallo build uitgevoerd.<br><br>Als u tooset Hallo build-parameters wilt, Hallo parameters verzenden als XML in de hoofdtekst Hallo zoals in Hallo voorbeeld te volgen. (Zie de sectie Hallo Build 'parameters' voor een uitleg van Hallo-parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Antwoord**:

HTTP-statuscode: 200

Dit is een asynchrone API. U krijgt een build-ID als antwoord. tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen. Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.

U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.

Geldige build-status:

* Maak - Build-aanvraag is gemaakt.
* In de wachtrij - Build-aanvraag is verzonden en deze in de wachtrij staat.
* Gebouw - Build wordt uitgevoerd.
* Geslaagd - Build is beëindigd.
* Fout - Build beëindigd met een fout.
* Geannuleerd - is Build geannuleerd.
* Annuleren - een verzoek tot annuleren voor Hallo build is verzonden.

Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Trigger Build (aanbeveling, positie of FBT)
| HTTP-methode | URI |
|:--- |:--- |
| VERZENDEN |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| KOPTEKST |`"Content-Type", "text/xml"`(Als aanvraagtekst verzenden) |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| userDescription |Tekstuele Hallo catalogus-ID. Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet. Zie het bovenstaande voorbeeld.<br>Maximale lengte: 50 |
| buildType |Type Hallo build tooinvoke: <br/> -Aanbeveling als u uw voor aanbeveling build <br> -Volgorde voor waarden van positie build <br/> -'Fbt' voor FBT build |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |Als dit veld leeg wordt met de standaardparameters voor build Hallo Hallo build uitgevoerd.<br><br>Als u tooset build-parameters wilt, stuurt u ze als XML in de hoofdtekst Hallo zoals in Hallo voorbeeld te volgen. (Zie de sectie Hallo Build 'parameters' voor een uitleg en een volledige lijst met parameters Hallo.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Antwoord**:

HTTP-statuscode: 200

Dit is een asynchrone API. U krijgt een build-ID als antwoord. tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen. Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.

U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.

Geldige build-status:

* Maak - Model is gemaakt.
* In de wachtrij - Model build is geactiveerd en deze in de wachtrij staat.
* Gebouw - Model wordt samengesteld.
* Geslaagd - Build is beëindigd.
* Fout - Build beëindigd met een fout.
* Geannuleerd - is Build geannuleerd.
* Annuleert - Build wordt geannuleerd.

Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a>11.4. Builds van Status van een Model ophalen
Haalt builds en hun status voor een opgegeven model.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| onlyLastBuild |Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen |
| apiVersion |1.0 |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per build. Elk item heeft Hallo gegevens te volgen:

* `feed/entry/content/properties/UserName`-Naam van de gebruiker Hallo.
* `feed/entry/content/properties/ModelName`-De naam van het Hallo-model.
* `feed/entry/content/properties/ModelId`-De unieke id model.
* `feed/entry/content/properties/IsDeployed`-Of Hallo build (ook wordt geïmplementeerd actieve build).
* `feed/entry/content/properties/BuildId`-De unieke id maken.
* `feed/entry/content/properties/BuildType`-Type van Hallo build.
* `feed/entry/content/properties/Status`-Status maken. Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, Cancelling, geannuleerd, geslaagd.
* `feed/entry/content/properties/StatusMessage`-Het gedetailleerde statusbericht (geldt alleen toospecific statussen).
* `feed/entry/content/properties/Progress`-Bouwen voortgang (%).
* `feed/entry/content/properties/StartTime`-Begintijd build.
* `feed/entry/content/properties/EndTime`-Eindtijd bouwen.
* `feed/entry/content/properties/ExecutionTime`-Duur maken.
* `feed/entry/content/properties/ProgressStep`-Gegevens over Hallo huidige fase van een build uitgevoerd.

Geldige build-status:

* Gemaakt - is vermelding van Build-aanvraag gemaakt.
* In de wachtrij - aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.
* Gebouw - Build is bezig.
* Geslaagd - Build is beëindigd.
* Fout - Build beëindigd met een fout.
* Geannuleerd - is Build geannuleerd.
* Annuleert - Build wordt geannuleerd.

Geldige waarden voor de BuildType:

* Positie - positie bouwen.
* Aanbeveling - aanbeveling build.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a>11.5. Builds Status ophalen
Haalt maken status van alle modellen van een gebruiker.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| onlyLastBuild |Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen. |
| apiVersion |1.0 |

**Antwoord**:

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per build. Elk item heeft Hallo gegevens te volgen:

* `feed/entry/content/properties/UserName`-Naam van de gebruiker Hallo.
* `feed/entry/content/properties/ModelName`-De naam van het Hallo-model.
* `feed/entry/content/properties/ModelId`-De unieke id model.
* `feed/entry/content/properties/IsDeployed`-Of Hallo build wordt geïmplementeerd.
* `feed/entry/content/properties/BuildId`-De unieke id maken.
* `feed/entry/content/properties/BuildType`-Type van Hallo build.
* `feed/entry/content/properties/Status`-Status maken. Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, geannuleerd, Cancelling, geslaagd.
* `feed/entry/content/properties/StatusMessage`-Het gedetailleerde statusbericht (geldt alleen toospecific statussen).
* `feed/entry/content/properties/Progress`-Bouwen voortgang (%).
* `feed/entry/content/properties/StartTime`-Begintijd build.
* `feed/entry/content/properties/EndTime`-Eindtijd bouwen.
* `feed/entry/content/properties/ExecutionTime`-Duur maken.
* `feed/entry/content/properties/ProgressStep`-Gegevens over Hallo huidige fase van een build uitgevoerd.

Geldige build-status:

* Gemaakt - is vermelding van Build-aanvraag gemaakt.
* In de wachtrij - aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.
* Gebouw - Build is bezig.
* Geslaagd - Build is beëindigd.
* Fout - Build beëindigd met een fout.
* Geannuleerd - is Build geannuleerd.
* Annuleert - Build wordt geannuleerd.

Geldige waarden voor de BuildType:

* Positie - positie bouwen.
* Aanbeveling - aanbeveling build.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a>11.6. Versie verwijderen
Hiermee verwijdert u een build.

OPMERKING: <br>U kunt een actieve build niet verwijderen. Hallo model moet worden bijgewerkt tooa andere actieve build voordat u deze verwijdert.<br>U kunt een build wordt uitgevoerd niet verwijderen. Moet u eerst Hallo build annuleren door het aanroepen van <strong>annuleren bouwen</strong>.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| buildId |De unieke id van Hallo build. |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

### <a name="117-cancel-build"></a>11.7. Build annuleren
Een build waarvan bij het bouwen van de status is geannuleerd.

| HTTP-methode | URI |
|:--- |:--- |
| PLAATSEN |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| buildId |De unieke id van Hallo build. |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

### <a name="118-get-build-parameters"></a>11.8. Het ophalen van Build-Parameters
Haalt bouwen parameters.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| buildId |De unieke id van Hallo build. |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Deze API retourneert een verzameling van sleutel/waarde-elementen. Elk element staat voor een parameter en de waarde ervan:

* `feed/entry/content/properties/Key`-Parameternaam bouwen.
* `feed/entry/content/properties/Value`-Parameterwaarde bouwen.

Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.

| Sleutel | Beschrijving | Type | Geldige waarde |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model. Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren. |Geheel getal |10-50 |
| NumberOfModelDimensions |het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens. Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters. Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items. |Geheel getal |10-40 |
| ItemCutOffLowerBound |Hallo item ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| ItemCutOffUpperBound |Hallo item bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffLowerBound |Hallo gebruiker ondergrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| UserCutOffUpperBound |Hallo gebruiker bovengrens voor Hallo koeler definieert. Zie gebruik koeler hierboven. |Geheel getal |2 of hoger (koeler 0 uitschakelen) |
| Beschrijving |Beschrijving bouwen. |Tekenreeks |Alle tekst maximaal 512 tekens |
| EnableModelingInsights |Hiermee kunt u toocompute metrische gegevens op Hallo aanbeveling model. |Booleaanse waarde |Waar/onwaar |
| UseFeaturesInModel |Hiermee wordt aangegeven als functies in volgorde tooenhance Hallo aanbeveling model kunnen worden gebruikt. |Booleaanse waarde |Waar/onwaar |
| ModelingFeatureList |Door komma's gescheiden lijst van de functie namen toobe Hallo aanbeveling gebouwd in volgorde tooenhance Hallo aanbeveling gebruikt. |Tekenreeks |Onderdeelnamen up too512 tekens |
| AllowColdItemPlacement |Hiermee wordt aangegeven als Hallo aanbeveling ook koude items via de functie overeenkomsten pushen moet. |Booleaanse waarde |Waar/onwaar |
| EnableFeatureCorrelation |Hiermee wordt aangegeven als functies kunnen worden gebruikt in de redenering. |Booleaanse waarde |Waar/onwaar |
| ReasoningFeatureList |Door komma's gescheiden lijst van de functie namen toobe gebruikt voor redeneren zinnen (bijvoorbeeld aanbeveling uitleg). |Tekenreeks |Onderdeelnamen up too512 tekens |

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Aanbeveling
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Item aanbevelingen krijgen (voor actieve build)
Ophalen van aanbevelingen van Hallo active build van het type 'Aanbeveling' of 'Fbt' op basis van een lijst met items zaden (invoer).

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| ItemID 's |Door komma's gescheiden lijst met Hallo items toorecommend voor. <br>Als Hallo active build van typt FBT en vervolgens kunt u slechts één item verzenden. <br>Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten <br> Max: 150 |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Hallo voorbeeld hieronder reactie bevat 10 aanbevolen items.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Item aanbevelingen (van een specifieke build) ophalen
De aanbevelingen van een specifieke build van het type 'Aanbeveling' of 'Fbt' krijgen.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| ItemID 's |Door komma's gescheiden lijst met Hallo items toorecommend voor. <br>Als Hallo active build van typt FBT en vervolgens kunt u slechts één item verzenden. <br>Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten <br> Max: 150 |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| buildId |Hallo toouse id voor deze aanvraag aanbeveling bouwen |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.1

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. FBT aanbevelingen krijgen (voor actieve build)
Haal de aanbevelingen van Hallo active build van het type 'Fbt' die is gebaseerd op een item seed (invoer).

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| itemId |Item toorecommend voor. <br>Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten <br>Max: 150 |
| minimalScore |Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per set aanbevolen item (een set van items die meestal worden gekocht met Hallo seed/invoer item). Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id1`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name1`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Id2`-2e aanbevolen artikel-ID (optioneel).
* `Feed\entry\content\properties\Name2`-De naam van de 2e item hello (optioneel).
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Hallo voorbeeld hieronder reactie bevat 3 aanbevolen item sets.

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Ophalen van de aanbevelingen FBT (van een specifieke build)
De aanbevelingen van een specifieke build van het type 'Fbt' krijgen.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| itemId |Item toorecommend voor. <br>Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten <br>Max: 150 |
| minimalScore |Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| buildId |Hallo toouse id voor deze aanvraag aanbeveling bouwen |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per set aanbevolen item (een set van items die meestal worden gekocht met Hallo seed/invoer item). Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id1`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name1`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Id2`-2e aanbevolen artikel-ID (optioneel).
* `Feed\entry\content\properties\Name2`-De naam van de 2e item hello (optioneel).
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.3

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Gebruiker aanbevelingen krijgen (voor actieve build)
Aanbevelingen van de gebruiker van een build van het type 'Aanbeveling' is gemarkeerd als actief build krijgen.

Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo-gebruiker.

Opmerkingen: 

1. Er is geen gebruiker aanbeveling voor FBT build.
2. Als het build-Hallo active is FBT deze methode wordt een foutmelding.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Gebruikers-id |Unieke id van gebruiker Hallo |
| numberOfResults |Aantal vereiste resultaten |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.1

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Gebruiker aanbevelingen krijgen met de lijst met items (voor actieve build)
Ophalen van de aanbevelingen van de gebruiker van een build van het type 'Aanbeveling' is gemarkeerd als actief wordt gemaakt met een aanvullende lijst met items

Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo gebruiker en Hallo extra items zijn opgegeven.

Opmerkingen: 

1. Er is geen gebruiker aanbeveling voor FBT build.
2. Als het build-Hallo active is FBT deze methode wordt een foutmelding.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Gebruikers-id |Unieke id van gebruiker Hallo |
| itemsIds |Door komma's gescheiden lijst met Hallo items toorecommend voor. Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.1

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Ophalen van de aanbevelingen van de gebruiker (van een specifieke build)
Aanbevelingen van de gebruiker van een specifieke build van het type 'Aanbeveling' krijgen.

Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo gebruiker (gebruikt in een specifieke Hallo-build).

Opmerking: Er is geen gebruiker aanbeveling voor FBT build.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Gebruikers-id |Unieke id van gebruiker Hallo |
| numberOfResults |Aantal vereiste resultaten |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| buildId |Hallo toouse id voor deze aanvraag aanbeveling bouwen |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.1

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Gebruiker aanbevelingen krijgen met itemlijst (van een specifieke build)
Aanbevelingen van de gebruiker van een specifieke versie van het type 'Aanbeveling' en Hallo-lijst van extra items ophalen.

Hallo API retourneert een lijst met voorspelde punt volgens de gebruiksgeschiedenis toohello van Hallo gebruiker en Hallo aanvullende lijst met items.

Opmerking: Ter is geen gebruiker aanbeveling voor FBT build.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| Gebruikers-id |Unieke id van gebruiker Hallo |
| ItemID 's |Door komma's gescheiden lijst met Hallo items toorecommend voor. Maximale lengte: 1024 |
| numberOfResults |Aantal vereiste resultaten |
| includeMetatadata |Toekomstig gebruik, altijd Onwaar |
| buildId |Hallo toouse id voor deze aanvraag aanbeveling bouwen |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.
* `Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).

Zie het voorbeeld van een reactie in 12.1

## <a name="13-user-usage-history"></a>13. Geschiedenis van de gebruiker
Als een model aanbeveling is gebouwd kunnen Hallo tooretrieve Hallo geschiedenis van gebruikers (items gekoppeld tooa specifieke gebruiker) gebruikt voor Hallo build.
Deze API geschiedenis van tooretrieve Hallo gebruikers toestaan

Opmerking: Hallo gebruikersgeschiedenis is momenteel alleen beschikbaar voor aanbeveling builds.

### <a name="131-retrieve-user-history"></a>13,1 geschiedenis van gebruikers ophalen
Ophalen Hallo lijst van item gebruikt in Hallo active bouwen of bouwen in Hallo opgegeven voor Hallo opgegeven gebruikers-id.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |Hallo gebruikersgeschiedenis voor actieve build Hallo niet ophalen.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Hallo gebruikersgeschiedenis voor Hallo gegeven build ophalen`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Voorbeeld:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |Hallo unieke id van Hallo-model. |
| Gebruikers-id |unieke id van gebruiker Hallo Hallo. |
| buildId |optionele parameter, van welke versie Hallo gebruikersgeschiedenis ophalen moet tooindicate toestaan |
| apiVersion |1.0 |

**Antwoord:**

HTTP-statuscode: 200

Hallo-antwoord bevat één vermelding per aanbevolen-item. Elk item heeft Hallo gegevens te volgen:

* `Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.
* `Feed\entry\content\properties\Name`-De naam van het Hallo-item.
* `Feed\entry\content\properties\Rating`-N.V.T..
* `Feed\entry\content\properties\Reasoning`-N.V.T..

OData-XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Meldingen
Azure Machine Learning aanbevelingen meldingen worden gegenereerd als permanente fouten in Hallo-systeem optreden. Er zijn 3 soorten meldingen:

1. Fout bij build - deze melding wordt geactiveerd voor elke build-fout.
2. Gegevens overname verwerkingsfout - deze melding wordt geactiveerd wanneer we meer dan 100 fouten in de Hallo laatste vijf minuten in Hallo verwerking van gebruiksgebeurtenissen per model hebben.
3. Aanbeveling verbruik mislukt - deze melding wordt geactiveerd wanneer we meer dan 100 fouten in de Hallo laatste vijf minuten in Hallo verwerking van aanvragen van de aanbeveling per model hebben.

### <a name="141-get-notifications"></a>14.1. Meldingen ophalen
Hiermee haalt u alle Hallo meldingen voor alle modellen of voor een enkelvoudig model.

| HTTP-methode | URI |
|:--- |:--- |
| TOEVOEGEN |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Alle meldingen voor alle modellen ophalen:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Voorbeeld voor het ophalen van meldingen voor een bepaald model:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |Een optionele parameter. Wanneer u dit weglaat, krijgt u alle meldingen voor alle modellen. <br>Geldige waarde: de unieke id van het Hallo-model. |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord:**

HTTP-statuscode: 200

OData-XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Model meldingen verwijderen
Hiermee verwijdert u alle lezen meldingen voor een model.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Voorbeeld:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| Model |De unieke id van het Hallo-model |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

### <a name="143-delete-user-notifications"></a>14.3. Meldingen voor gebruikers verwijderen
Hiermee verwijdert u alle meldingen voor alle modellen.

| HTTP-methode | URI |
|:--- |:--- |
| VERWIJDEREN |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Parameternaam | Geldige waarden |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Aanvraagtekst |GEEN |

**Antwoord**:

HTTP-statuscode: 200

## <a name="15-legal"></a>15. Juridische informatie
Dit document wordt geleverd ' as-is '. Informatie en inzichten die in dit document, inclusief URL's en andere websiteverwijzingen, kunnen zonder kennisgeving worden gewijzigd.<br><br>
Enkele voorbeelden die hierin staan zijn uitsluitend ter illustratie en zijn fictief. Er is geen echte verwantschap of relatie is bedoeld of moet worden afgeleid.<br><br>
Dit document biedt geen u enkel wettelijk recht tooany intellectueel eigendom in een Microsoft-product. U kunt kopiëren en het gebruik van dit document voor eigen referentiedoeleinden.<br><br>
© 2015 Microsoft. Alle rechten voorbehouden.

