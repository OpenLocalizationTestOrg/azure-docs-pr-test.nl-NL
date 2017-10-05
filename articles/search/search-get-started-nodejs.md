---
title: Aan de slag met Azure Search in Node.js | Microsoft Docs
description: Stappen voor het bouwen van een zoektoepassing op een door Azure gehoste service voor zoeken in de cloud, waarbij gebruik wordt gemaakt van de programmeertaal Node.js.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Aan de slag met Azure Search in Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Informatie over het bouwen van een aangepaste Node.js-zoektoepassing die voor de zoekfunctie gebruikmaakt van Azure Search. In deze zelfstudie wordt de [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) gebruikt om de objecten en bewerkingen in deze oefening te bouwen.

We hebben [Node.js](https://Nodejs.org), NPM, [Sublime Text 3](http://www.sublimetext.com/3) en Windows PowerShell op Windows 8.1 gebruikt om deze code te ontwikkelen en te testen.

Als u dit voorbeeld wilt uitvoeren, moet u over de Azure Search-service beschikken. U kunt zich hiervoor aanmelden in [Azure Portal](https://portal.azure.com). Zie [Een Azure Search-service in de portal maken](search-create-service-portal.md) voor stapsgewijze instructies.

## <a name="about-the-data"></a>Over de gegevens
In deze voorbeeldtoepassing wordt gebruikgemaakt van gegevens van [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op de staat Rhode Island om de grootte van de gegevensset te reduceren. We gebruiken deze gegevens om een zoektoepassing te bouwen die kenmerkende gebouwen, zoals ziekenhuizen of scholen, gebouwen zoals ziekenhuizen en scholen, maar ook geologische kenmerken, zoals stromen, meren en toppen, retourneert.

In deze toepassing zorgt het programma **DataIndexer** er met een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) voor dat de index wordt gebouwd en geladen en dat de gefilterde USGS-gegevensset uit een openbare Azure SQL-database wordt opgehaald. De programmacode bevat de referenties en gegevens voor verbinding met de onlinegegevensbron. U hoeft verder niets te configureren.

> [!NOTE]
> Er is een filter op de gegevensset toegepast om onder de limiet van 10.000 documenten voor de gratis prijscategorie te blijven. Als u de standaardcategorie gebruikt, is deze limiet niet van toepassing. Zie [Limieten voor de Search-service](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a>De servicenaam en API-sleutel van uw Azure Search-service zoeken
Zodra u de service hebt gemaakt, keert u terug naar de portal om de URL of `api-key` op te halen. Verbindingen met uw Search-service vereisen dat u zowel over de URL als een `api-key` beschikt om de aanroep te verifiëren.

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Klik in de snelbalk op de **Search-service** om alle Azure Search-services weer te geven die zijn ingericht voor uw abonnement.
3. Selecteer de service die u wilt gebruiken.
4. Op het servicedashboard worden als het goed is tegels weergegeven voor essentiële informatie, zoals het sleutelpictogram voor toegang tot de beheersleutels.
5. Kopieer de service-URL, een beheersleutel en een querysleutel. Deze voegt u in een later stadium toe aan het bestand config.js.

## <a name="download-the-sample-files"></a>De voorbeeldbestanden downloaden
Gebruik een van de volgende methoden om het voorbeeld te downloaden.

1. Ga naar [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Klik op **Download ZIP** (ZIP downloaden), sla het zip-bestand op en pak vervolgens alle bestanden in het zip-bestand uit.

Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a>Werk het bestand config.js bij met de URL van de Search-service en uw API-sleutel.
Gebruik de URL en API-sleutel die u eerder hebt gekopieerd om de URL, beheersleutel en querysleutel in het configuratiebestand op te geven.

Beheersleutels bieden u de volledige controle over de servicebewerkingen, inclusief het maken of verwijderen van een index en het laden van documenten. Querysleutels kunnen daarentegen alleen leesbewerkingen uitvoeren en worden doorgaans gebruikt door clienttoepassingen die verbinding maken met Azure Search.

In dit voorbeeld nemen we de querysleutel op om de aanbevolen procedure voor het gebruik van de querysleutel in clienttoepassingen nog maar eens onder de aandacht te brengen.

De volgende afbeelding is een schermopname van het bestand **config.js**. Het bestand is geopend in een teksteditor en de relevante items zijn gemarkeerd, zodat u kunt zien waar het bestand moet worden bijgewerkt met geldige waarden voor uw zoekservice.

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a>Een runtime-omgeving voor het voorbeeld hosten
Voor dit voorbeeld hebt u een HTTP-server nodig. Deze kunt u globaal installeren met npm.

Gebruik voor de volgende opdrachten een PowerShell-venster.

1. Navigeer naar de map met het bestand **package.json**.
2. Typ `npm install`.
3. Typ `npm install -g http-server`.

## <a name="build-the-index-and-run-the-application"></a>Bouw de index en voer de toepassing uit
1. Typ `npm run indexDocuments`.
2. Typ `npm run build`.
3. Typ `npm run start_server`.
4. Ga in uw browser naar `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Zoeken in USGS-gegevens
De USGS-gegevensset bevat records die relevant zijn voor de staat Rhode Island. Als u op **Zoeken** klikt terwijl het zoekvak leeg is, worden de bovenste 50 vermeldingen weergegeven. Dit is de standaardinstelling.

Als u een zoekterm invoert, geeft u de zoekmachine iets om mee te werken. Voer een regionale naam in. 'Roger Williams' was de eerste gouverneur van Rhode Island. Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.

![][9]

U kunt ook de volgende termen proberen:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Volgende stappen
Dit is de eerste Azure Search-zelfstudie op basis van Node.js en de USGS-gegevensset. In de loop van de tijd zal deze zelfstudie worden uitgebreid om aanvullende zoekfuncties te demonstreren die u mogelijk wilt gebruiken in uw aangepaste oplossingen.

Als u al enige ervaring met Azure Search hebt, kunt u dit voorbeeld gebruiken als springplank om een suggestiefunctie (type-ahead of automatisch aangevulde query's), filters en facetnavigatie uit te proberen. U kunt ook de pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch te verwerken, zodat gebruikers door de resultaten kunnen bladeren.

Bent u niet bekend met Azure Search? Het is raadzaam andere zelfstudies te bekijken om inzicht te verwerven in wat u zoal kunt maken. Bezoek de [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) voor meer resources. U kunt ook de koppelingen in de [lijst met video's en zelfstudies](search-video-demo-tutorial-list.md) volgen om meer informatie te bekijken.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
