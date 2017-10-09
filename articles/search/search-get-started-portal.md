---
titel: aaa "zelfstudie: maken van uw eerste Azure Search-index in Hallo portal | Microsoft Docs' Beschrijving: In hello Azure-portal, vooraf gedefinieerde gebruiken sample data toogenerate een index. Probeer zoekopdrachten in volledige tekst, filters, facetten, fuzzy zoekopdrachten, geosearch en meer.
Services: documentationcenter zoeken: '' auteur: HeidiSteen manager: jhubbard-editor: '' tags: azure-portal

MS.AssetID: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: ms.devlang zoeken: n.v.t. ms.workload: ms.topic zoeken: hero-article ms.tgt_pltfrm: n.v.t. ms.date: 26-06/2017 ms.author: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Zelfstudie: Uw eerste Azure Search-index maken in Hallo-portal

In hello Azure-portal, beginnen met een vooraf gedefinieerde voorbeeld gegevensset tooquickly genereren een index met behulp van Hallo **gegevens importeren** wizard. Probeer zoekopdrachten in volledige tekst, filters, facetten, fuzzy zoekopdrachten en geosearch met **Search Explorer**.  

Met deze inleiding zonder code kunt u aan de slag met vooraf gedefinieerde gegevens, zodat u direct interessante query's kunt schrijven. Hoewel de hulpprogramma's van de portal geen vervanging zijn voor code, zijn ze handig voor deze taken:

+ Hands On leren met minimale ramp-up
+ Prototype van een index maken voordat u code schrijft in **Gegevens importeren**
+ Query's testen en syntaxis parseren in **Search Explorer**
+ Weergeven van een bestaande index gepubliceerde tooyour service en de kenmerken worden opgezocht

**Geschatte tijd:** ongeveer 15 minuten, maar het kan langer duren als ook is vereist dat u zich registreert bij het account of de service. 

U kunt ook mogelijk uitbreiden met behulp van een [inleiding op basis van code tooprogramming Azure Search in .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Vereisten

In deze zelfstudie wordt ervan uitgegaan dat u beschikt over een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) en [Azure-service](search-create-service-portal.md). 

Als u niet onmiddellijk tooprovision een service wilt, kunt u bekijken een demonstratie 6 minuten durende Hallo stappen in deze zelfstudie begint bij ongeveer drie minuten in deze [overzicht van Azure Search video](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Uw service vinden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Open het servicedashboard Hallo van uw Azure Search-service. Als u niet Hallo service tegel tooyour dashboard vastmaken, kunt u uw service op deze manier vinden: 
   
   * Klik in de Snelbalk hello, op **meer services** Hallo Hallo linkernavigatiedeelvenster onderaan in.
   * Typ in het zoekvak Hallo *search* tooget een lijst met services voor uw abonnement. Uw service moet worden weergegeven in de lijst Hallo. 

## <a name="check-for-space"></a>Controleren of er voldoende ruimte is
Veel klanten beginnen met Hallo gratis service. Deze versie is beperkt toothree indexen drie gegevensbronnen en drie indexeerfuncties. Zorg ervoor dat er voldoende ruimte is voor extra items voordat u begint. In deze zelfstudie wordt van elk object één exemplaar gemaakt. 

> [!TIP] 
> Tegels op het servicedashboard Hallo weergeven hoeveel indexen, Indexeerfuncties en gegevensbronnen al. de tegel indexeerfunctie Hallo bevat indicatoren geslaagd en mislukt. Klik op Hallo tegel tooview Hallo indexeerfunctie count. 
>
> ![Tegels voor indexeerfuncties en gegevensbronnen][1]
>

## <a name="create-index"></a> Een index maken en gegevens laden
Zoekopdrachten worden over een *index* herhaald met doorzoekbare gegevens, metagegevens en constructies, die worden gebruikt om bepaald zoekgedrag te optimaliseren.

tookeep deze taak portal-gebaseerde, gebruiken we een ingebouwde voorbeeldgegevensset die kan worden benaderd met een indexeerfunctie via Hallo **gegevens importeren** wizard. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Stap 1: Start de wizard importeren Hallo
1. Klik op het dashboard van de service Azure Search **gegevens importeren** in Hallo opdracht balk toostart een wizard die u maakt zowel een index vult.
   
    ![Opdracht Gegevens importeren][2]

2. Klik in de wizard Hallo op **gegevensbron** > **voorbeelden** > **onroerend goed-ons-sample**. Deze gegevensbron is vooraf geconfigureerd met informatie over een naam, type en verbinding. Zodra de gegevensbron is gemaakt, wordt deze een bestaande gegevensbron genoemd die opnieuw kan worden gebruikt voor andere bewerkingen.

    ![Voorbeeldgegevensset selecteren][9]

3. Klik op **OK** toouse deze.

#### <a name="step-2-define-hello-index"></a>Stap 2: Hallo index definiëren
Maken van een index is doorgaans handmatige en op basis van code, maar de wizard Hallo kunt genereren een index voor elke gegevensbron die het kunt verkennen. Minimaal een index moeten een naam en een verzameling van velden, waarbij één veld is gemarkeerd als key toouniquely document Hallo identificeren elk document.

Velden bevatten gegevenstypen en kenmerken. Hallo selectievakjes in aan de bovenkant Hallo worden *indexkenmerken* beheren hoe Hallo veld wordt gebruikt. 

* **Ophalen mogelijk** betekent dat dit veld wordt weergegeven in de lijst met zoekresultaten. U kunt afzonderlijke velden markeren als ontoegankelijk voor zoekresultaten door dit selectievakje uit te schakelen, bijvoorbeeld voor velden die alleen in filterexpressies worden gebruikt. 
* De kenmerken **Filterbaar**, **Sorteerbaar** en **Geschikt voor facetten** bepalen of een veld in een filter, een sorteervolgorde of een facetnavigatiestructuur kan worden gebruikt. 
* **Doorzoekbaar** betekent dat een veld is opgenomen in een zoekopdracht in volledige tekst. Tekenreeksen zijn doorzoekbaar. Numerieke velden en Booleaanse waarden zijn vaak gemarkeerd als niet doorzoekbaar. 

Standaard scant Hallo wizard Hallo gegevensbron voor unieke id's als basis voor het sleutelveld Hallo Hallo. Tekenreeksen hebben de kenmerken Ophaalbaar en Doorzoekbaar. Gehele getallen hebben de kenmerken Ophaalbaar, Filterbaar, Sorteerbaar en Geschikt voor facetten.

  ![Gegenereerde onroerend goed-index][3]

Klik op **OK** toocreate Hallo index.

#### <a name="step-3-define-hello-indexer"></a>Stap 3: Hallo indexeerfunctie definiëren
Nog steeds in Hallo **gegevens importeren** wizard, klikt u op **indexeerfunctie** > **naam**, en typ een naam voor de indexeerfunctie Hallo. 

Dit object definieert een uitvoerbaar proces. U kunt plaatsen op terugkerende planning, maar voor nu gebruik Hallo standaard optie toorun Hallo indexeerfunctie zodra onmiddellijk, wanneer u klikt op **OK**.  

  ![indexeerfunctie voor onroerend goed][8]

## <a name="check-progress"></a>Voortgang controleren
toomonitor gegevens importeren, gaat u terug toohello servicedashboard, schuif omlaag en dubbelklik op Hallo **indexeerfuncties** tegel tooopen Hallo indexeerfuncties lijst. U ziet de indexeerfunctie Hallo nieuw gemaakt in Hallo lijst met status die aangeeft 'wordt uitgevoerd' of een geslaagd, samen met het aantal geïndexeerde documenten Hallo.

   ![Voortgangsbericht voor de indexeerfunctie][4]

## <a name="query-index"></a>Query Hallo index
U hebt nu een zoekindex die gereed tooquery. **Search explorer** is een queryprogramma dat is ingebouwd in Hallo-portal. Er wordt een zoekvak geboden zodat u kunt controleren of de zoekresultaten aan de verwachting voldoen. 

> [!TIP]
> In Hallo [overzicht van Azure Search video](https://channel9.msdn.com/Events/Connect/2016/138), Hallo stappen te volgen in Hallo video op 6m08s worden uitgelegd.
>

1. Klik op **Search explorer** op Hallo opdrachtbalk klikken.

   ![Opdracht Search Explorer][5]

2. Klik op **wijziging index** op Hallo opdrachtbalk tooswitch te*onroerend goed-ons-sample*.

   ![Index- en API-opdrachten][6]

3. Klik op **ingesteld API-versie** op Hallo opdracht balk toosee die REST-API's beschikbaar zijn. Preview-API's krijgt die u toegang toonew functies tot nog in het algemeen niet vrijgegeven. Gebruik voor Hallo query's hieronder, algemeen beschikbaar Hallo-versie (2016 09 01) tenzij omgeleid. 

    > [!NOTE]
    > [Azure Search REST-API](https://docs.microsoft.com/rest/api/searchservice/search-documents) en Hallo [.NET-bibliotheek](search-howto-dotnet-sdk.md#core-scenarios) volledig equivalent zijn, maar **Search explorer** alleen ingerichte toohandle REST-aanroepen. Accepteert syntaxis voor beide [vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) en [volledige Lucene queryparser](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), plus alle beschikbaar in de zoekparameters Hallo [zoekdocument](https://docs.microsoft.com/rest/api/searchservice/search-documents) bewerkingen.
    > 

4. Voer onderstaande Hallo queryreeksen in de zoekbalk Hallo, en klik op **Search**.

  ![Voorbeeld van zoekquery][7]

**`search=seattle`**

+ Hallo `search` parameter gebruikte tooinput een zoeken met trefwoorden voor zoeken in volledige tekst in dit geval is, lijsten in koning regio, Washington status retourneren, die *Seattle* in elk doorzoekbaar veld in het Hallo-document. 

+ **Search explorer** retourneert resultaten in JSON, dit is uitgebreid en vaste tooread als documenten een dense structuur hebben. Afhankelijk van uw documenten moet u mogelijk toowrite code dat ingangen resultaten tooextract belangrijke elementen zoeken. 

+ Documenten bestaan uit alle velden die zijn gemarkeerd als ophalen in index Hallo mogelijk. tooview indexkenmerken in Hallo-portal klikt u op *onroerend goed-ons-sample* in Hallo **indexen** tegel.

**`search=seattle&$count=true&$top=100`**

+ Hallo `&` symbool is de zoekparameters gebruikte tooappend, die kunnen worden opgegeven in een willekeurige volgorde. 

+  Hallo `$count=true` parameter retourneert een getal voor Hallo som van alle documenten die worden geretourneerd. U kunt filterquery's controleren door de wijzigingen te controleren die door `$count=true` worden gerapporteerd. 

+ Hallo `$top=100` retourneert Hallo hoogste 100 documenten buiten Hallo totale gerangschikt. Standaard retourneert Azure Search Hallo eerste 50 beste overeenkomsten. U kunt vergroten of verkleinen Hallo bedrag via `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` is een lege zoekopdracht. Met een lege zoekopdracht wordt naar alles gezocht. Een reden voor het indienen van een leeg query is te filteren of facet ten opzichte van de volledige set Hallo van documenten. U wilt bijvoorbeeld een tooconsist facetten navigatie structuur van alle steden in Hallo index.

+  `facet`retourneert een navigatie structuur, dat u de UI-besturingselement tooa kunt doorgeven. Deze retourneert categorieën en een aantal. In dit geval zijn categorieën gebaseerd op Hallo aantal steden. Er is geen aggregatie in Azure Search, maar u kunt een geschatte aggregatie bepalen via `facet`, dat het aantal documenten in elke categorie retourneert.

+ `$top=2`brengt terug ter illustratie van waarmee u kunt twee documenten `top` tooboth neemt toe of resultaten.

**`search=seattle&facet=beds`**

+ Deze query gebruikt het facet bedden in een tekstuele zoekopdracht naar *Seattle*. `"beds"`kan worden opgegeven als een facet omdat Hallo-veld is gemarkeerd als ophalen mogelijk, Filterbaar en geschikt voor facetten in Hallo-index en Hallo deze waarden bevat (numeriek, 1 tot en met 5), geschikt zijn voor de aanbiedingen categoriseren in groepen (aanbiedingen met 3 slaapkamers, 4 slaapkamers). 

+ Alleen filterbare velden kunnen als facet worden gebruikt. Alleen ophalen mogelijk velden kunnen worden geretourneerd in Hallo resultaten.

**`search=seattle&$filter=beds gt 3`**

+ Hallo `filter` parameter retourneert resultaten die overeenkomen met de Hallo criteria die u hebt opgegeven. In dit geval: meer dan 3 slaapkamers. 

+ Filtersyntaxis is een OData-constructie. Zie [OData-syntaxis filteren](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) voor meer informatie.

**`search=granite countertops&highlight=description`**

+ Treffers markeren verwijst tooformatting op tekst hello-sleutelwoord overeenkomende komt overeen met gegeven zijn gevonden in een bepaald veld. Als uw zoekterm diep in een beschrijving wordt overspoeld, kunt u treffers markeren toomake toevoegen het gemakkelijker toospot. In dit geval Hallo woordgroep geformatteerd `"granite countertops"` eenvoudiger toosee in Hallo beschrijvingsveld is.

**`search=mice&highlight=description`**

+ Met zoekopdrachten in de volledige tekst kunnen woorden met vergelijkbare semantiek worden gevonden. In dit geval bevatten zoekresultaten gemarkeerde tekst voor 'muis' thuis waarvoor de muis is aangetast, in het antwoord tooa zoeken met trefwoorden op 'muizen'. Verschillende vormen van Hallo hetzelfde woord in de resultaten kan worden weergegeven vanwege taalkundige analyse. 

+ Azure Search ondersteunt 56 analyzers van Lucene en Microsoft. Hallo-standaardwaarde gebruikt door Azure Search is Hallo standaard Lucene analyzer. 

**`search=samamish`**

+ Verkeerd gespelde woorden, zoals 'samamish' voor Hallo Samammish plateau in Hallo gebied van Seattle, mislukken tooreturn overeenkomsten in typische zoeken. toohandle typefouten, kunt u fuzzy zoeken, die worden beschreven in het volgende voorbeeld hello gebruiken.

**`search=samamish~&queryType=full`**

+ Fuzzy zoeken is ingeschakeld wanneer u Hallo opgeeft `~` symbool en Hallo volledige queryparser gebruiken, die wordt geïnterpreteerd en correct parseert Hallo `~` syntaxis. 

+ Fuzzy zoeken is beschikbaar wanneer u opt-in voor Hallo volledige queryparser, waarmee deze gebeurtenis treedt op wanneer u `queryType=full`. Zie voor meer informatie over query's ingeschakeld door de volledige queryparser hello [Lucene-querysyntaxis in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Wanneer `queryType` is niet is opgegeven, Hallo standaard eenvoudige queryparser wordt gebruikt. Hallo eenvoudige queryparser is sneller, maar als u nodig hebt voor fuzzy zoeken, reguliere expressies, zoeken bij benadering of andere soorten geavanceerde query's, moet u de volledige syntaxis Hallo. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ Georuimtelijke zoekopdracht wordt ondersteund door Hallo [edm. Het gegevenstype GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) voor een veld met coördinaten. Geosearch is een type filter dat wordt opgegeven bij [Filter OData-syntaxis](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search). 

+ Hallo voorbeeldquery filtert alle resultaten voor positionele gegevens, waar de resultaten minder dan 5 kilometer vanaf een bepaald moment (opgegeven als breedtegraad en lengtegraad coördinaten) zijn. Door toe te voegen `$count`, kunt u zien hoeveel resultaten worden geretourneerd wanneer u de afstand Hallo of Hallo coördinaten wijzigen. 

+ Georuimtelijk zoeken is handig als uw zoektoepassing een functie ´in mijn buurt zoeken´ heeft of gebruikmaakt van kaartnavigatie. Dit is echter niet een zoekopdracht in volledige tekst. Als u gebruikersvereisten hebt voor zoekopdrachten op een plaats of land met de naam, velden met namen van een stad of land in toevoeging toocoordinates toevoegen.

## <a name="next-steps"></a>Volgende stappen

+ Wijzig alle Hallo-objecten die u zojuist hebt gemaakt. Nadat u de wizard Hallo eenmaal hebt uitgevoerd, u kunt teruggaan en weergeven of wijzigen van afzonderlijke onderdelen: index, indexeerfunctie of de gegevensbron. Bepaalde bewerkingen, zoals Hallo wijzigen Hallo gegevensveldtype, zijn niet toegestaan op Hallo index, maar de meeste eigenschappen en instellingen worden gewijzigd.

  tooview afzonderlijke onderdelen, klikt u op Hallo **Index**, **indexeerfunctie**, of **gegevensbronnen** tegels op uw dashboard toodisplay een lijst met bestaande objecten. toolearn meer informatie over de bewerkingen van de index waarvoor niet opnieuw opbouwen, Zie [Index bijwerken (Azure Search REST-API)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Probeer het Hallo-hulpprogramma's en stappen met andere gegevensbronnen. Hallo voorbeeldgegevensset `realestate-us-sample`, is van een Azure SQL Database die Azure Search kunt verkennen. Naast Azure SQL Database kan Azure Search ook een index uit platte gegevensstructuren in Azure Table Storage, Blob Storage of SQL Server op een Azure-VM en Azure Cosmos DB verkennen of afleiden. Al deze gegevensbronnen worden ondersteund in de wizard Hallo. In code kunt u een index gemakkelijk vullen met behulp van een *indexeerfunctie*.

+ Alle andere niet-indexeerfunctie gegevensbronnen worden ondersteund via een pushmodel, waarbij uw code pushes nieuw en gewijzigd rijensets in JSON tooyour index. Zie [Documenten toevoegen, bijwerken of verwijderen in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents) voor meer informatie.

Voor meer informatie over andere functies die in dit artikel worden vermeld, gaat u naar deze koppelingen:

* [Overzicht van indexeerfuncties](search-indexer-overview.md)
* [Index maken (inclusief een gedetailleerde beschrijving van de indexkenmerken Hallo)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Search Explorer](search-explorer.md)
* [Documenten zoeken (inclusief voorbeelden van een querysyntaxis)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png