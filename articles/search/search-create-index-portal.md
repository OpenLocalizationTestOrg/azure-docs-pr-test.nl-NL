---
title: aaa "maken van een index (portal - Azure Search) | Microsoft Docs'
description: Een index maken met hello Azure-Portal.
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Een Azure Search index maken met hello Azure Portal
> [!div class="op_single_selector"]
> * [Overzicht](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Hallo ingebouwde index designer gebruiken in Azure portal tooprototype of maak een [search-index](search-what-is-an-index.md) toorun op uw Azure Search-service. 

## <a name="prerequisites"></a>Vereisten

In dit artikel wordt ervan uitgegaan dat een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) en [Azure Search-service](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Uw search-service zoeken
1. Toohello Azure portal-pagina aanmelden en controleren van Hallo [zoeken services voor uw abonnement](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Selecteer uw Azure Search-service.

## <a name="name-hello-index"></a>Hallo naamindex

1. Klik op Hallo **toevoegen index** knop in de opdrachtbalk Hallo bovenaan Hallo Hallo pagina.
2. Naam van uw Azure Search-index. 
   * Met een letter beginnen.
   * Gebruik alleen kleine letters, getallen of streepjes ('-').
   * Hallo naam too60 tekens beperken.

  Hallo indexnaam maakt deel uit van Hallo eindpunt-URL die wordt gebruikt voor verbindingen toohello index en voor de verzending van HTTP-aanvragen in hello Azure Search REST-API.

## <a name="define-hello-fields-of-your-index"></a>Hallo velden van de index definiëren

Index samenstelling bevat een *verzameling velden* Hallo doorzoekbare gegevens in uw index te definiëren. Meer specifiek, geeft het Hallo-structuur van documenten die u afzonderlijk kunt uploaden. Hallo Veldenverzameling bevat de vereiste en optionele velden, met de naam en hebt getypt, met index kenmerken toodetermine hoe Hallo veld kan worden gebruikt.

1. In Hallo **Index toevoegen** blade, klikt u op **velden >** tooslide Hallo veld definitie blade geopend. 

2. Hallo gegenereerd accepteren *sleutel* veld van het type Edm.String. Standaard Hallo heet *id* , maar u kunt de naam wijzigen, zolang Hallo tekenreeks voldoet aan [naamgevingsregels](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Het veld met een sleutel is verplicht voor elke Azure Search-index en het moet een tekenreeks.

3. Voeg velden toofully Geef Hallo-documenten gaat uploaden. Als u documenten bestaan uit een *id*, *naam hotel*, *adres*, *stad*, en *regio*, maak een overeenkomende veld voor elk criterium in Hallo index. Bekijk Hallo [richtlijnen in onderstaande sectie voor Hallo ontwerpen](#design) voor hulp bij het instellen van kenmerken.

4. Voeg alle velden die worden gebruikt intern desgewenst in filterexpressies. Kenmerken op Hallo veld kunnen tooexclude velden worden ingesteld van zoekopdrachten.

5. Wanneer u klaar bent, klikt u op **OK** toosave en Hallo index maken.

## <a name="tips-for-adding-fields"></a>Tips voor het toevoegen van velden

Maken van een index in de portal Hallo is toetsenbord intensieve. Stappen minimaliseren door deze werkstroom te volgen:

1. Bouw Hallo veldenlijst eerst door te voeren namen en instellen van gegevenstypen.

2. Vervolgens selectievakjes gebruiken Hallo Hallo boven aan elk kenmerk toobulk Hallo instelling inschakelen voor alle velden, en selectief Schakel selectievakjes uit voor Hallo weinig velden waarvoor dit niet. Tekenreeksvelden zijn bijvoorbeeld meestal doorzoekbaar. Zo kunt u klikken op **ophalen mogelijk** en **doorzoekbaar** tooboth return Hallo waarden Hallo veld in de zoekresultaten, evenals zoeken in volledige tekst op Hallo veld toestaan. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Richtlijnen voor het instellen van kenmerken

Hoewel u nieuwe velden op elk gewenst moment toevoegen kunt, worden bestaande velddefinities voor Hallo levensduur van Hallo index vergrendeld in. Om deze reden ontwikkelaars doorgaans Hallo portal gebruiken voor eenvoudige indexen te maken, testen ideeën of Hallo portal-pagina's toolook van een instelling te gebruiken. Veelvuldig herhaling via een ontwerp voor de index is efficiënter als u een code gebaseerde aanpak volgt, zodat u kunt eenvoudig hello index opnieuw.

Analyzers en suggestiefunctie zijn gekoppeld aan velden voordat Hallo index wordt opgeslagen. Ervoor tooclick via elke tabbladen pagina tooadd taal analyzers of suggestiefunctie tooyour indexdefinitie worden.

Tekenreeksvelden zijn vaak gemarkeerd als **doorzoekbaar** en **ophalen mogelijk**.

Bevatten de zoekresultaten voor velden die worden gebruikt toonarrow **sorteerbaar**, **Filterable**, en **geschikt voor facetten**.

Veldkenmerken bepalen hoe een veld wordt gebruikt, zoals of deze wordt gebruikt in een zoekopdracht in volledige tekst, facetnavigatie, sorteerbewerkingen, enzovoort. Hallo volgende tabel wordt elk kenmerk beschreven.

|Kenmerk|Beschrijving|  
|---------------|-----------------|  
|**doorzoekbare**|Volledige tekst kan worden doorzocht, onderwerp toolexical analyse zoals woordafbreking tijdens het indexeren. Als u de waarde van een doorzoekbaar veld tooa zoals 'mooi day' instelt, intern dit verdeeld in Hallo afzonderlijke tokens 'mooi' en 'day'. Zie voor meer informatie [hoe volledige tekst zoeken works](search-lucene-query-architecture.md).|  
|**Filterbaar**|Waarnaar wordt verwezen in **$filter** query's. Filterbaar velden van het type `Edm.String` of `Collection(Edm.String)` niet worden bewerkt woordafbreking, zodat vergelijkingen zijn voor exact overeenkomt met alleen. Bijvoorbeeld, als u zo'n veld f te instellen 'mooi day' `$filter=f eq 'sunny'` wordt geen overeenkomsten gevonden maar `$filter=f eq 'sunny day'` wordt. |  
|**sorteerbaar**|Standaard sorteert Hallo system resultaten op score, maar u kunt sorteren op basis van velden in Hallo documenten configureren. Velden van het type `Collection(Edm.String)` kan niet worden **sorteerbaar**. |  
|**geschikt voor facetten**|Doorgaans gebruikt in een weergave van zoekresultaten met een aantal treffers per categorie (bijvoorbeeld hotels in Haarlem). Deze optie kan niet worden gebruikt met velden van het type `Edm.GeographyPoint`. Velden van het type `Edm.String` die zijn **Filterbaar**, **sorteerbaar**, of **geschikt voor facetten** kan niet groter zijn dan 32 kB lang. Zie voor meer informatie [Create Index (REST-API)](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**sleutel**|De unieke id voor documenten in Hallo index. Hallo sleutelveld moet precies één veld worden gekozen en moet van het type `Edm.String`.|  
|**ophalen mogelijk**|Hiermee wordt bepaald of Hallo veld in een zoekresultaat kan worden geretourneerd. Dit is handig als u wilt dat een veld toouse (zoals *winstmarge*) als een filter wilt sorteren of score berekenen mechanisme, maar niet wilt Hallo veld toobe zichtbaar toohello eindgebruiker bieden. Dit kenmerk moet `true` voor `key` velden.|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>De index hotels Hallo gebruikt in de voorbeeld-API-secties maken

Documentatie voor Azure Search API bevat voorbeelden van code met een eenvoudige *hotels* index. In onderstaande Hallo schermafbeeldingen, ziet u de indexdefinitie hello, Hallo Franse taal analyzer opgegeven tijdens de indexdefinitie, waaronder die u kunt opnieuw maken als een oefening in Hallo-portal.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Volgende stappen

Nadat een Azure Search-index is gemaakt, kunt u de volgende stap toohello: [doorzoekbare gegevens uploaden naar Hallo index](search-what-is-data-import.md).

U kunt ook u kan ook rekening houden met uitvoerig stil op indexen. Bovendien toohello Veldenverzameling, een index bepaalt ook analyzers, suggestiefunctie, profielen en CORS-instellingen voor scorefuncties. Hallo-portal biedt tabpagina's voor het definiëren van de meest voorkomende elementen Hallo: velden, analyzers en suggestiefunctie. toocreate of wijzig andere elementen, kunt u Hallo REST-API of .NET SDK.

## <a name="see-also"></a>Zie ook

 [Hoe zoeken in de volledige tekst werkt](search-lucene-query-architecture.md)  
 [Search-service REST-API](https://docs.microsoft.com/rest/api/searchservice/) [.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

