---
title: aaaGet slag met Azure Search in Node.js | Microsoft Docs
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Aan de slag met Azure Search in Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Meer informatie over hoe toobuild een aangepaste Node.js-toepassing die gebruikmaakt van Azure Search voor de zoekfunctie zoeken. Deze zelfstudie wordt gebruikgemaakt van Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hallo objecten en bewerkingen in deze oefening.

We hebben gebruikt [Node.js](https://Nodejs.org) en NPM, [Sublime Text 3](http://www.sublimetext.com/3), en Windows PowerShell op Windows 8.1 toodevelop en test deze code.

toorun dit voorbeeld hebt u een Azure Search-service, u voor Hallo aanmelden kunt [Azure-portal](https://portal.azure.com). Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor stapsgewijze instructies.

## <a name="about-hello-data"></a>Over Hallo-gegevens
Deze voorbeeldtoepassing gebruikt gegevens uit Hallo [Verenigde Staten Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op Hallo staat Rhode Island tooreduce Hallo gegevensset grootte. We gebruiken deze gegevens toobuild een zoektoepassing die kenmerkende gebouwen zoals ziekenhuizen en scholen, evenals geologische kenmerken, zoals stromen, meren en toppen retourneert.

In deze toepassing hello **DataIndexer** programma bouwt en belastingen Hallo index met behulp van een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) constructie, bij het ophalen van Hallo gefilterde USGS-gegevensset uit een openbare Azure SQL Database. Referenties en verbinding vindt u informatie toohello onlinegegevensbron in Hallo programmacode. U hoeft verder niets te configureren.

> [!NOTE]
> We een filter toegepast op deze gegevensset toostay onder Hallo 10.000 Documentlimiet Hallo gratis prijscategorie. Als u de standaardcategorie Hallo gebruikt, is deze limiet niet van toepassing. Zie [Limieten voor de Search-service](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Hallo-servicenaam en api-sleutel van uw Azure Search-service zoeken
Nadat u Hallo service maakt, keert u terug toohello portal tooget Hallo URL of `api-key`. Verbindingen tooyour Search-service vereisen dat u beide Hallo-URL en een `api-key` tooauthenticate Hallo aanroep.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik in de snelbalk hello **zoekservice** toolist alle Azure Search-services die zijn ingericht voor uw abonnement.
3. Selecteer de gewenste toouse Hallo-service.
4. U ziet op Hallo servicedashboard tegels voor essentiële informatie, zoals het sleutelpictogram voor toegang tot de beheersleutels Hallo Hallo.
5. Kopieer Hallo service-URL, een beheersleutel en een querysleutel. U moet alle drie later wanneer u ze toohello bestand config.js file toevoegt.

## <a name="download-hello-sample-files"></a>Hallo voorbeeldbestanden downloaden
Gebruik een van de Hallo benaderingen toodownload Hallo voorbeeld te volgen.

1. Ga te[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Klik op **ZIP downloaden**, Hallo ZIP-bestand opslaan en pak vervolgens alle Hallo bestanden bevat.

Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Hallo config.js bijwerken. met de URL van de Search-service en uw API-sleutel.
URL en api-sleutel die u eerder hebt gekopieerd met behulp van Hallo Hallo-URL, beheersleutel en querysleutel opgeven in het configuratiebestand.

Beheersleutels bieden u de volledige controle over de servicebewerkingen, inclusief het maken of verwijderen van een index en het laden van documenten. Querysleutels zijn daarentegen voor alleen-lezen bewerkingen, meestal worden gebruikt door clienttoepassingen die verbinding maken met tooAzure zoeken.

In dit voorbeeld opnemen we Hallo query sleutel toohelp versterking Hallo beste praktijken van het gebruik van Hallo querysleutel in clienttoepassingen.

Hallo volgende schermafbeelding ziet **config.js** openen in een teksteditor, hello relevante items zijn gemarkeerd, zodat u kunt zien waar tooupdate Hallo-bestand met de Hallo waarden die geldig zijn voor uw zoekservice.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Een runtime-omgeving voor Hallo voorbeeld hosten
Hallo vereist een HTTP-server die u kunt globaal installeren met npm.

Gebruik een PowerShell-venster voor Hallo opdrachten te volgen.

1. Navigeer toohello-map met de Hallo **package.json** bestand.
2. Typ `npm install`.
3. Typ `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Hallo-toepassing hello index bouwen en uitvoeren
1. Typ `npm run indexDocuments`.
2. Typ `npm run build`.
3. Typ `npm run start_server`.
4. Ga in uw browser naar `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Zoeken in USGS-gegevens
Hallo USGS-gegevensset bevat records die relevant toohello staat Rhode Island. Als u op **Search** op het zoekvak leeg is, u krijgen Hallo bovenste 50 vermeldingen, Hallo standaardinstelling.

Een zoekterm invoert biedt Hallo zoekmachine iets toogo op. Voer een regionale naam in. 'Roger Williams' was Hallo eerste gouverneur van Rhode Island. Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.

![][9]

U kunt ook de volgende termen proberen:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Volgende stappen
Dit is Hallo eerste Azure Search-zelfstudie op basis van Node.js en Hallo USGS-gegevensset. Na verloop van tijd hebt we deze zelfstudie toodemonstrate aanvullende zoekfuncties kunt u toouse in uw aangepaste oplossingen uitbreiden.

Als u al enige ervaring met Azure Search hebt, kunt u dit voorbeeld gebruiken als springplank om een suggestiefunctie (type-ahead of automatisch aangevulde query's), filters en facetnavigatie uit te proberen. U kunt ook op Hallo pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch zodat gebruikers kunnen via Hallo resultaten.

Nieuwe tooAzure zoeken? Het is raadzaam om bij andere zelfstudies toodevelop een goed begrip van kunt maken. Ga naar onze [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) toofind meer bronnen. U kunt ook weergeven Hallo koppelingen in onze [Video's en zelfstudies lijst](search-video-demo-tutorial-list.md) tooaccess meer informatie.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
