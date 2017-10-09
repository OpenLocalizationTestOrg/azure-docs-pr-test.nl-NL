---
titel: aaa "Azure Cosmos DB DocumentDB-API: SQL-syntaxis | Microsoft Docs' Beschrijving: verwijzen naar de documentatie voor hello Azure Cosmos DB DocumentDB API SQL-querytaal.
Services: cosmos-db auteur: mimig1 manager: jhubbard-editor: mimig documentationcenter: ''

MS.AssetID: ms.service: cosmos-db ms.workload: data services ms.tgt_pltfrm: na ms.devlang: n.v.t. ms.topic: verwijzen naar ms.date: 13-06/2017 ms.author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>Azure DB Cosmos DocumentDB API: Verwijzing naar SQL

Hello Azure Cosmos DB DocumentDB API ondersteunt documentquery's die gebruikmaken van een bekende SQL (Structured Query Language) zoals grammatica via hiërarchische JSON-documenten zonder expliciet schema of het maken van secundaire indexen. Dit onderwerp bevat de naslagdocumentatie voor Hallo DocumentDB API SQL-querytaal.

Zie voor een overzicht van Hallo DocumentDB API SQL-querytaal [SQL-query's voor Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).  
  
We ook nodigen u toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) kunt u proberen Azure Cosmos DB en SQL-query's uitvoeren op onze gegevensset.  
  
## <a name="select-query"></a>SELECT-query  
Haalt de JSON-documenten uit Hallo-database. Ondersteunt de evaluatie van de expressie, projecties, filteren en lid wordt.  Hallo syntaxis conventies sectie geeft een tabelindeling van Hallo conventies voor het beschrijven van Hallo SELECT-instructies.  
  
**Syntaxis**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Opmerkingen**  
  
 Zie de volgende secties voor meer informatie op elke component:  
  
-   [SELECT-component](#bk_select_query)  
  
-   [FROM-component](#bk_from_clause)  
  
-   [WHERE-component](#bk_where_clause)  
  
-   [ORDER BY-component](#bk_orderby_clause)  
  
Hallo-componenten in Hallo SELECT-instructie moeten worden besteld, zoals hierboven. Een van de optionele componenten Hallo kan worden weggelaten. Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde Hallo.  
  
**Logische verwerkingsvolgorde Hallo SELECT-instructie**  
  
Hallo in welke volgorde componenten zijn verwerkt is:  

1.  [FROM-component](#bk_from_clause)  
2.  [WHERE-component](#bk_where_clause)  
3.  [ORDER BY-component](#bk_orderby_clause)  
4.  [SELECT-component](#bk_select_query)  

Houd er rekening mee dat dit verschilt van Hallo volgorde waarin ze worden weergegeven in het Hallo-syntaxis. Hallo ordening is dat alle nieuwe symbolen die zijn geïntroduceerd in een component verwerkte zichtbaar zijn en kunnen worden gebruikt in de componenten die later wordt verwerkt. Bijvoorbeeld, aliassen die zijn gedeclareerd in een FROM-component in, waarbij toegankelijk zijn en SELECT-component.  

**Spaties en -opmerkingen**  

Alle spatietekens die deel uitmaken van een tekenreeks tussen aanhalingstekens of aanhalingstekens id maken geen deel uit van Hallo taal grammatica en worden genegeerd tijdens het parseren.  

Hallo-querytaal biedt ondersteuning voor T-SQL-stijl opmerkingen zoals  

-   SQL-instructie`-- comment text [newline]`  

Terwijl uit witruimte bestaat en -opmerkingen niet alle significante in grammatica hello zijn, moeten ze gebruikte tooseparate tokens zijn. Bijvoorbeeld: `-1e5` is één nummer token, even`: – 1 e5` wordt een min token gevolgd door nummer 1 en id e5.  

##  <a name="bk_select_query"></a>SELECT-component  
Hallo-componenten in Hallo SELECT-instructie moeten worden besteld, zoals hierboven. Een van de optionele componenten Hallo kan worden weggelaten. Maar als optionele componenten worden gebruikt, moeten ze worden weergegeven in de juiste volgorde Hallo.  

**Syntaxis**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Argumenten**  
  
 `<select_specification>`  
  
 Eigenschappen of waarde toobe geselecteerd voor Hallo resultaat ingesteld.  
  
 `'*'`  
  
Hiermee geeft u op dat Hallo waarde zonder wijzigingen moet worden opgehaald. Specifiek als Hallo verwerkt waarde een object is, worden alle eigenschappen worden opgehaald.  
  
 `<object_property_list>`  
  
Hiermee geeft lijst op Hallo van eigenschappen toobe opgehaald. Elke geretourneerde waarde is een object met Hallo eigenschappen opgegeven.  
  
`VALUE`  
  
Hiermee geeft u op dat Hallo JSON-waarde moet worden opgehaald in plaats van Hallo voltooid JSON-object. Dit, in tegenstelling tot `<property_list>` loopt Hallo geprojecteerd waarde niet in een object.  
  
`<scalar_expression>`  
  
Expressie die aangeeft Hallo waarde toobe berekend. Zie [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.  
  
**Opmerkingen**  
  
Hallo `SELECT *` syntaxis is alleen geldig als FROM-component precies één alias is gedeclareerd. `SELECT *`biedt een identity-projectie handig is als er geen projectie is vereist. Selecteer * is alleen geldig als FROM-component is opgegeven en er slechts één invoer bron geïntroduceerd.  
  
Houd er rekening mee dat `SELECT <select_list>` en `SELECT *` 'syntactische suiker' zijn en u kunt ook kan worden uitgedrukt met behulp van eenvoudige SELECT-instructies zoals hieronder wordt weergegeven.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     is gelijk aan:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     is gelijk aan:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Zie ook**  
  
[Scalaire expressies](#bk_scalar_expressions)  
[SELECT-component](#bk_select_query)  
  
##  <a name="bk_from_clause"></a>FROM-component  
Hiermee geeft u op Hallo bron of gekoppelde bronnen. Hallo FROM-component is optioneel. Als dat niet wordt opgegeven, andere componenten nog steeds uitgevoerd alsof FROM-component opgegeven één document.  
  
**Syntaxis**  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
**Argumenten**  
  
`<from_source>`  
  
Hiermee geeft u een gegevensbron met of zonder een alias. Als alias niet opgegeven is, wordt deze worden afgeleid van Hallo `<collection_expression>` met volgende regels:  
  
-   Hallo-expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.  
  
-   Als de expressie Hallo `<collection_expression>`, en vervolgens kubuskenmerkbinding en vervolgens kubuskenmerkbinding wordt gebruikt als alias. Hallo-expressie is een verzamelingnaam, wordt verzamelingnaam worden gebruikt als een alias.  
  
ALS IN DE`input_alias`  
  
Hiermee geeft u op dat Hallo `input_alias` is een set met waarden geretourneerd door Hallo onderliggende verzamelingsexpressie.  
 
`input_alias`IN  
  
Hiermee geeft u op dat Hallo `input_alias` Hallo verzameling waarden die zijn verkregen door iteratie van alle matrixelementen van elke matrix geretourneerd door de onderliggende verzamelingsexpressie Hallo moet vertegenwoordigen. Een waarde die is geretourneerd door de onderliggende verzamelingsexpressie is geen matrix wordt genegeerd.  
  
`<collection_expression>`  
  
Hiermee geeft u op Hallo verzameling expressie toobe gebruikte tooretrieve Hallo documenten.  
  
`ROOT`  
  
Hiermee geeft u op dat document uit de momenteel verbonden verzameling Hallo standaard moet worden opgehaald.  
  
`collection_name`  
  
Hiermee geeft u op dat document moet worden opgehaald uit de verzameling Hallo opgegeven. Hallo-naam van verzameling op Hallo moet overeenkomen met de Hallo-naam van verzameling op Hallo momenteel verbonden.  
  
`input_alias`  
  
Geeft aan dat document moet worden opgehaald uit Hallo andere bron gedefinieerd door Hallo opgegeven alias.  
  
`<collection_expression> '.' property_`  
  
Geeft aan dat document moet worden opgehaald door het openen van Hallo `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Geeft aan dat document moet worden opgehaald door het openen van Hallo `property_name` eigenschap of matrixindex matrixelement voor alle documenten die worden opgehaald door opgegeven verzamelingsexpressie.  
  
**Opmerkingen**  
  
Alle aliassen verstrekt of afgeleid in Hallo `<from_source>(`s) moet uniek zijn. Hallo syntaxis `<collection_expression>.`kubuskenmerkbinding is gelijk aan Hallo `<collection_expression>' ['"property_name"']'`. Hallo laatstgenoemde syntaxis kan echter worden gebruikt als een eigenschapsnaam een niet-id-tekens bevat.  
  
**Ontbrekende eigenschappen, ontbrekende matrixelementen, niet-gedefinieerde waarden verwerken**  
  
Als een verzamelingsexpressie voor een naar eigenschappen of matrixelementen en waarde niet bestaat, wordt die waarde genegeerd en niet verder worden verwerkt.  
  
**Verzameling expressie context scoping**  
  
Een verzamelingsexpressie is mogelijk binnen het bereik van verzameling of binnen het bereik van document:  
  
-   Een expressie is gericht op de verzameling, als hello onderliggende gegevensbron Hallo verzamelingsexpressie beide ROOT of `collection_name`. Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn opgehaald uit de verzameling Hallo rechtstreeks en is niet afhankelijk van het Hallo-verwerking van andere expressies verzameling.  
  
-   Een expressie is binnen het bereik van document, als hello onderliggende gegevensbron Hallo verzamelingsexpressie `input_alias` geïntroduceerd eerder in het Hallo-query. Een dergelijke expressie vertegenwoordigt een verzameling van documenten die zijn verkregen door het evalueren van Hallo verzamelingsexpressie in Hallo bereik van elk document die behoren toohello set Hallo alias verzameling gekoppeld.  de resulterende set Hallo worden een samenvoeging van die worden verkregen door Hallo verzamelingsexpressie voor elke Hallo documenten in Hallo onderliggende set te evalueren.  
  
**Joins**  
  
In de huidige release Hallo ondersteunt Azure Cosmos DB inner joins. Er zijn extra join mechanismen toekomstige.

Inner join in een volledige vectorproduct Hallo resultatensets die deel uitmaken van Hallo join. Hallo-resultaat van een join N manier is een set met tuples zijn N-element, waarbij elke waarde in het Hallo-tuple is gekoppeld aan het Hallo-alias instellen die deel Hallo join en toegankelijk zijn voor het verwijzen naar deze alias in andere componenten.  
  
Hallo-evaluatie van Hallo join, is afhankelijk van Hallo context bereik van Hallo deelnemende sets:  
  
-  Een join tussen verzamelingsset A en gericht op de verzameling ingesteld B, resulteert in een vectorproduct van alle elementen in sets A en B.
  
-   Een koppeling tussen het paar A en binnen het bereik van document set B, resulteert in een samenvoeging van alle sets die zijn verkregen door het evalueren van binnen het bereik van document set B voor elk document van A. instellen  
  
 In de huidige release Hallo wordt maximaal één expressie gericht op de verzameling ondersteund door de queryprocessor Hallo.  
  
**Voorbeelden van joins:**  
  
Bekijk hello FROM-component te volgen:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Elke bron definiëren, kunnen `input_alias1, input_alias2, …, input_aliasN`. Deze component FROM retourneert een set met N-tuples (tuple met N waarden). Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden.  
  
*Voorbeeld 1, met 2 bronnen JOIN:*  
  
- Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.  
  
- Laat `<from_source2>` worden document binnen het bereik van verwijzende input_alias1 en vertegenwoordigen sets:  
  
    {1, 2} voor`input_alias1 = A,`  
  
    {3} voor`input_alias1 = B,`  
  
    {4, 5} voor`input_alias1 = C,`  
  
- Hallo FROM-component `<from_source1> JOIN <from_source2>` leidt ertoe dat Hallo tuples te volgen:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Voorbeeld 2, met 3 bronnen JOIN:*  
  
- Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.  
  
- Laat `<from_source2>` worden binnen het bereik van document verwijzen naar `input_alias1` sets omvatten:  
  
    {1, 2} voor`input_alias1 = A,`  
  
    {3} voor`input_alias1 = B,`  
  
    {4, 5} voor`input_alias1 = C,`  
  
- Laat `<from_source3>` worden binnen het bereik van document verwijzen naar `input_alias2` sets omvatten:  
  
    {100, 200} voor`input_alias2 = 1,`  
  
    {300} voor`input_alias2 = 3,`  
  
- Hallo FROM-component `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat Hallo tuples te volgen:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Gebrek aan tuples voor andere waarden van `input_alias1`, `input_alias2`, voor welke Hallo `<from_source3>` heeft geen waarden retourneren.  
  
*Voorbeeld 3, met 3 bronnen JOIN:*  
  
- Laat < from_source1 > worden gericht op de verzameling en vertegenwoordigen set {A, B, C}.  
  
- Laat `<from_source1>` verzameling bereik en de set {A, B, C} vertegenwoordigen.  
  
- < From_source2 > verwijzende input_alias1 binnen het bereik van document zijn en stelt vertegenwoordigen, kunnen:  
  
    {1, 2} voor`input_alias1 = A,`  
  
    {3} voor`input_alias1 = B,`  
  
    {4, 5} voor`input_alias1 = C,`  
  
- Laat `<from_source3>` moet binnen het bereik te`input_alias1` sets omvatten:  
  
    {100, 200} voor`input_alias2 = A,`  
  
    {300} voor`input_alias2 = C,`  
  
- Hallo FROM-component `<from_source1> JOIN <from_source2> JOIN <from_source3>` leidt ertoe dat Hallo tuples te volgen:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), C, 4, 300, (C, 5, 300)  
  
> [!NOTE]
> Dit resulteerde in vectorproduct tussen `<from_source2>` en `<from_source3>` omdat beide bereik toohello dezelfde `<from_source1>`.  Dit resulteerde in 4 (2 x 2) tuples met waarde A, 0 tuples met waarde B (1 x 0) en 2 (2 x 1) tuples met waarde C.  
  
**Zie ook**  
  
 [SELECT-component](#bk_select_query)  
  
##  <a name="bk_where_clause"></a>WHERE-component  
 Hiermee geeft u Hallo zoekcriterium voor Hallo documenten die worden geretourneerd door Hallo-query.  
  
 **Syntaxis**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Argumenten**  
  
-   `<filter_condition>`  
  
     Hiermee geeft u Hallo voorwaarde toobe voldaan voor Hallo documenten toobe geretourneerd.  
  
-   `<scalar_expression>`  
  
     Expressie die aangeeft Hallo waarde toobe berekend. Zie Hallo [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.  
  
 **Opmerkingen**  
  
 Opdat Hallo geretourneerd document toobe een expressie die is opgegeven als filtervoorwaarde tootrue moet worden geëvalueerd. Alleen Booleaanse waarde true voldoen aan Hallo voorwaarde, een andere waarde: niet-gedefinieerde, null, false, getal, matrix of Object niet voldoen aan Hallo voorwaarde.  
  
##  <a name="bk_orderby_clause"></a>ORDER BY-component  
 Hiermee geeft u Hallo sorteervolgorde voor de resultaten van Hallo-query.  
  
 **Syntaxis**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Argumenten**  
  
-   `<sort_specification>`  
  
     Hiermee geeft u een eigenschap of een expressie waarop toosort Hallo queryresultaatset. Een kolom sorteren kan worden opgegeven als een alias voor een naam of kolom.  
  
     Meerdere sortering-kolommen kunnen worden opgegeven. Kolomnamen moet uniek zijn. Hallo Hallo sorteren kolommen in component ORDER BY Hallo reeks definieert Hallo organisatie van de resultaatset Hallo gesorteerd. Dat wil zeggen, Hallo resultatenset is gesorteerd op de eerste eigenschap Hallo en vervolgens die geordende lijst is gesorteerd op de tweede eigenschap hello, enzovoort.  
  
     Hallo kolomnamen waarnaar wordt verwezen in de component ORDER BY Hallo moeten overeenkomen met een kolom in Hallo lijst of tooa kolom gedefinieerd in een tabel die is opgegeven in de FROM-component Hallo zonder eventuele dubbelzinnigheden selecteren tooeither.  
  
-   `<sort_expression>`  
  
     Hiermee geeft u een één eigenschap of een expressie op welke queryresultaatset Hallo toosort.  
  
-   `<scalar_expression>`  
  
     Zie Hallo [scalaire expressies](#bk_scalar_expressions) sectie voor meer informatie.  
  
-   `ASC | DESC`  
  
     Hiermee geeft u op dat Hallo waarden in de opgegeven kolom Hallo in oplopende of aflopende volgorde moeten worden gesorteerd. ASC sorteert van Hallo laagste waarde toohighest waarde. DESC sorteren van hoogste waarde toolowest waarde. ASC is Hallo standaardsorteervolgorde. Null-waarden worden behandeld als Hallo laagst mogelijke waarden.  
  
 **Opmerkingen**  
  
 Tijdens het Hallo-querygrammatica ondersteunt meerdere volgorde door eigenschappen, ondersteunt hello Azure Cosmos DB query runtime alleen tegen één eigenschap, en alleen eigenschapnamen, dat wil zeggen, niet op berekende eigenschappen sorteren. Sorteren is ook vereist dat Hallo indexeren beleid bevat een bereikindex voor de eigenschap Hallo en Hallo opgegeven type, met Hallo maximumprecisie. Raadpleeg toohello indexeren beleid-documentatie voor meer informatie.  
  
##  <a name="bk_scalar_expressions"></a>Scalaire expressies  
 Een scalaire expressie die is een combinatie van symbolen en operators die kunnen worden geëvalueerd tooobtain één waarde. Eenvoudige expressies kunnen bestaan constanten, eigenschap verwijzingen, matrix element verwijzingen, alias-verwijzingen of functieaanroepen. Eenvoudige expressies kunnen worden gecombineerd tot complexe expressies met operators.  
  
 Zie voor informatie over welke scalaire expressie die u wellicht waarden, [constanten](#bk_constants) sectie.  
  
 **Syntaxis**  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 **Argumenten**  
  
-   `<constant>`  
  
     Vertegenwoordigt een constante waarde. Zie [constanten](#bk_constants) sectie voor meer informatie.  
  
-   `input_alias`  
  
     Hiermee geeft u een waarde die is gedefinieerd door Hallo `input_alias` geïntroduceerd in Hallo `FROM` component.  
    Deze waarde is gegarandeerd toonot worden **niet-gedefinieerde** –**niet-gedefinieerde** waarden in de Hallo invoer worden overgeslagen.  
  
-   `<scalar_expression>.property_name`  
  
     Vertegenwoordigt een waarde van Hallo-eigenschap van een object. Als Hallo-eigenschap niet bestaat of eigenschap van een waarde die niet een object wordt verwezen, Hallo expressie evalueert vervolgens te**niet-gedefinieerde** waarde.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Vertegenwoordigt een waarde van eigenschap met de naam Hallo `property_name` of matrixelement met index `array_index` van een objectmatrix. Als Hallo eigenschappenmatrix/index niet bestaat of Hallo eigenschappenmatrix/index op een waarde die niet een objectmatrix wordt verwezen, evalueert Hallo expressie tooundefined waarde.  
  
-   `unary_operator <scalar_expression>`  
  
     Vertegenwoordigt een operator die wordt toegepast tooa één waarde. Zie [Operators](#bk_operators) sectie voor meer informatie.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Een operator die is toegepast tootwo waarden vertegenwoordigt. Zie [Operators](#bk_operators) sectie voor meer informatie.  
  
-   `<scalar_function_expression>`  
  
     Vertegenwoordigt een waarde die is gedefinieerd door een resultaat van een functieaanroep.  
  
-   `udf_scalar_function`  
  
     Naam van de gebruiker Hallo scalaire functie gedefinieerd.  
  
-   `builtin_scalar_function`  
  
     Naam van de ingebouwde scalaire functie Hallo.  
  
-   `<create_object_expression>`  
  
     Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuw object met de opgegeven eigenschappen en hun waarden.  
  
-   `<create_array_expression>`  
  
     Hiermee geeft u een waarde die wordt verkregen door het maken van een nieuwe matrix met de opgegeven waarden als elementen  
  
-   `parameter_name`  
  
     Vertegenwoordigt een waarde van de opgegeven parameternaam Hallo. Parameternamen moeten één @ hebben als eerste teken Hallo.  
  
 **Opmerkingen**  
  
 Bij het aanroepen van een ingebouwde of de gebruiker gedefinieerde scalaire functie moeten alle argumenten worden gedefinieerd. Als een van de argumenten Hallo is gedefinieerd, Hallo-functie wordt niet aangeroepen en Hallo resultaat is niet gedefinieerd.  
  
 Bij het maken van een object, worden alle eigenschappen die niet-gedefinieerde waarde is toegewezen overgeslagen en niet is opgenomen in het Hallo-object gemaakt.  
  
 Wanneer het maken van een matrix, maar een elementwaarde die is toegewezen **niet-gedefinieerde** waarde wordt overgeslagen en niet is opgenomen in object Hallo gemaakt. Hierdoor wordt vervolgens gedefinieerd Hallo element tootake plaats zodanig dat matrix Hallo gemaakt wordt niet hebt overgeslagen indexen.  
  
##  <a name="bk_operators"></a>Operators  
 Deze sectie beschrijft operators Hallo ondersteund. Elke operator kan worden toegewezen tooexactly één categorie.  
  
 Zie **Operator categorieën** tabel hieronder voor meer informatie met betrekking tot de verwerking van **niet-gedefinieerde** waarden, type-vereisten voor de invoerwaarden en verwerking van waarden met niet overeenkomende typen.  
  
 **Operator categorieën:**  
  
|**Categorie**|**Details**|  
|-|-|  
|**rekenkundige bewerking**|Operator verwacht input(s) toobe (s). Uitvoer is ook een getal. Als een van de invoerwaarden Hallo **niet-gedefinieerde** of type dan het aantal vervolgens Hallo resultaat is **niet-gedefinieerde**.|  
|**Bitsgewijze**|Operator verwacht input(s) toobe 32-bits geheel getal met teken (s). Uitvoer is ook een 32-bits geheel getal.<br /><br /> Een niet-integerwaarde worden afgerond. Positieve waarde wordt afgerond, negatieve getallen naar boven afgerond.<br /><br /> Een waarde die buiten het bereik van Hallo 32-bits geheel getal wordt geconverteerd, door te nemen van de laatste 32-bits van de twee van bits.<br /><br /> Als een van de invoerwaarden Hallo **niet-gedefinieerde** of andere dan getal, typt u vervolgens Hallo resultaat is **niet-gedefinieerde**.<br /><br /> **Opmerking:** Hallo hierboven gedrag is compatibel met JavaScript bitsgewijze operator gedrag.|  
|**logische**|Operator verwacht input(s) toobe Boolean(s). Uitvoer is ook een Booleaanse waarde.<br />Als een van de invoerwaarden Hallo **niet-gedefinieerde** of andere dan Boolean, typ wordt Hallo resultaat **niet-gedefinieerde**.|  
|**vergelijking**|Operator verwacht input(s) toohave Hallo dezelfde typt en niet worden gedefinieerd. Uitvoer is een Booleaanse waarde.<br /><br /> Als een van de invoerwaarden Hallo **niet-gedefinieerde** of Hallo-invoer hebben verschillende typen en vervolgens Hallo resultaat is **niet-gedefinieerde**.<br /><br /> Zie **volgorde van waarden voor vergelijking** tabel voor waarde ordening details.|  
|**tekenreeks**|Operator verwacht input(s) toobe meer. Uitvoer is ook een tekenreeks.<br />Als een van de invoerwaarden Hallo **niet-gedefinieerde** of type heeft dan tekenreeks vervolgens Hallo resultaat is **niet-gedefinieerde**.|  
  
 **Unaire operators:**  
  
|**Naam**|**Operator**|**Details**|  
|-|-|-|  
|**rekenkundige bewerking**|+<br /><br /> -|Hallo getal-waarde als resultaat gegeven.<br /><br /> Bitsgewijze onderhandeling. De numerieke waarde retourneert genegeerde.|  
|**Bitsgewijze**|~|Toepassingsgroepen de aanvulling. Retourneert een reeks een numerieke waarde.|  
|**Logische**|**NIET**|Negatie. Retourneert genegeerde Booleaanse waarde.|  
  
 **Binaire operators:**  
  
|**Naam**|**Operator**|**Details**|  
|-|-|-|  
|**rekenkundige bewerking**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Toevoeging.<br /><br /> Aftrekken.<br /><br /> Vermenigvuldigen.<br /><br /> Deling.<br /><br /> Modulatie.|  
|**Bitsgewijze**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|Bitsgewijze OR.<br /><br /> Bitsgewijze AND.<br /><br /> Bitsgewijze XOR.<br /><br /> Verschuiving naar links.<br /><br /> Rechts verplaatsen.<br /><br /> Nul opvulling rechts verplaatsen.|  
|**logische**|**EN**<br /><br /> **OR**|Logische verbinding. Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.<br /><br /> Logische verbinding. Retourneert **true** als beide argumenten zijn **true**, retourneert **false** anders.|  
|**vergelijking**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Is gelijk aan. Retourneert **true** als argumenten gelijk zijn, retourneert **false** anders.<br /><br /> Niet gelijk aan. Retourneert **true** als argumenten niet gelijk zijn, retourneert **false** anders.<br /><br /> Groter dan. Retourneert **true** als eerste argument groter is dan de tweede hello, retourneren **false** anders.<br /><br /> Groter dan of gelijk zijn aan. Retourneert **true** als eerste argument is groter dan of gelijk zijn aan toohello tweede, retourneren **false** anders.<br /><br /> Minder dan. Retourneert **true** als eerste argument lager is dan het tweede hello, geretourneerd **false** anders.<br /><br /> Kleiner dan of gelijk zijn aan. Retourneert **true** als eerste argument kleiner dan of gelijk is toohello tweede een return **false** anders.<br /><br /> Coalesce. Retourneert Hallo tweede argument als eerste argument Hallo een **niet-gedefinieerde** waarde.|  
|**Tekenreeks**|**&#124;&#124;**|Samenvoeging. Retourneert een samenvoeging van beide argumenten.|  
  
 **Ternair operators:**  
  
|Ternaire operator|?|Retourneert Hallo tweede argument als eerste argument Hallo te evalueert**true**; anders Hallo derde argument retourneren.|  
|-|-|-|  
  
 **Ordening van waarden voor vergelijking**  
  
|**Type**|**De volgorde van de waarden**|  
|-|-|  
|**Niet-gedefinieerd**|Niet worden vergeleken.|  
|**Null**|Eén waarde: **null**|  
|**Aantal**|Natuurlijke reëel getal.<br /><br /> Negatieve oneindige waarde is kleiner dan andere numerieke waarde.<br /><br /> Positieve oneindige waarde is groter dan andere numerieke waarde. **NaN** waarde kan niet worden vergeleken. Vergelijken met **NaN** leidt ertoe dat **niet-gedefinieerde** waarde.|  
|**Tekenreeks**|Lexicographical volgorde.|  
|**Matrix**|Er is geen ordening, maar billijke.|  
|**Object**|Er is geen ordening, maar billijke.|  
  
 **Opmerkingen**  
  
 In Azure Cosmos DB Hallo typen waarden vaak niet bekend zijn totdat ze daadwerkelijk worden opgehaald uit Hallo-database. In volgorde toosupport efficiënte uitvoering van query's hebben de meeste Hallo operators strikt type vereisten. Operators zelf voeren ook geen impliciete conversies.  
  
 Dit betekent dat een query, zoals: Selecteer * van ROOT r waar r.Age = 21 retourneert alleen documenten met leeftijd gelijk toohello getal 21-eigenschap. Documenten met de eigenschap leeftijd gelijk toohello tekenreeks '21' of Hallo tekenreeks '0021' wordt niet overeenkomen, als Hallo expressie '21' = 21 tooundefined evalueert. Hiermee kunt u een beter gebruik van indexen, omdat Hallo opzoeken van een specifieke waarde (dat wil zeggen 21 number) is sneller dan zoeken naar oneindig aantal mogelijke overeenkomsten (dat wil zeggen getal 21 of tekenreeksen '21', '021', "21.0"...). Dit wijkt af van hoe JavaScript operators van waarden van verschillende typen evalueert.  
  
 **Matrices en objecten gelijkheid en het vergelijkingstype**  
  
 Vergelijken van de matrix of Object waarden met bereik operators (>, > =, <, < =) leidt ertoe dat niet-gedefinieerde omdat er geen volgorde gedefinieerd op het Object of de matrix waarden. Echter met gelijk-ongelijk operators (=,! =, <>) wordt ondersteund en waarden structureel's worden vergeleken.  
  
 Matrices zijn gelijk als beide matrices hetzelfde aantal elementen hebben en elementen op die overeenkomt met de posities ook gelijk zijn. Als een combinatie van elementen vergelijken in een niet-gedefinieerde, Hallo resultaat van de vergelijking van de matrix resulteert is niet gedefinieerd.  
  
 Objecten zijn gelijk als beide objecten hebben dezelfde eigenschappen die zijn gedefinieerd, en als de waarden van eigenschappen die overeenkomt met ook gelijk zijn. Als elk paar eigenschapswaarden vergelijken in een niet-gedefinieerde, Hallo resultaat van het object vergelijking resulteert is niet gedefinieerd.  
  
##  <a name="bk_constants"></a>Constanten  
 Een constante, ook wel bekend als een letterlijke waarde of een scalaire waarde is een symbool dat de waarde van een specifieke gegevens vertegenwoordigt. Hallo-indeling van een constante is afhankelijk van Hallo-gegevenstype van Hallo-waarde vertegenwoordigt.  
  
 **Scalaire-gegevenstypen ondersteund:**  
  
|**Type**|**De volgorde van de waarden**|  
|-|-|  
|**Niet-gedefinieerd**|Eén waarde: **niet gedefinieerd**|  
|**Null**|Eén waarde: **null**|  
|**Booleaanse waarde**|Waarden: **false**, **true**.|  
|**Aantal**|Een getal met dubbele precisie drijvende komma IEEE-norm 754.|  
|**Tekenreeks**|Een reeks van nul of meer Unicode-tekens. Tekenreeksen moeten worden ingesloten in enkele of dubbele aanhalingstekens.|  
|**Matrix**|Een reeks van nul of meer elementen. Elk element is een waarde van elk gegevenstype scalaire, behalve Undefined.|  
|**Object**|Een niet-geordende reeks nul of meer naam/waarde-paren. De naam van een Unicode-tekenreeks is, de waarde kan zijn van elk gegevenstype scalaire, behalve **Undefined**.|  
  
 **Syntaxis**  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 **Argumenten**  
  
1.  `<undefined_constant>; undefined`  
  
     Geeft niet-gedefinieerde waarde van het type niet gedefinieerd.  
  
2.  `<null_constant>; null`  
  
     Hiermee geeft u **null** waarde van het type **Null**.  
  
3.  `<boolean_constant>`  
  
     Constante van het type Booleaans vertegenwoordigt.  
  
4.  `false`  
  
     Hiermee geeft u **false** waarde van het type Boole-waarde.  
  
5.  `true`  
  
     Hiermee geeft u **true** waarde van het type Boole-waarde.  
  
6.  `<number_constant>`  
  
     Hiermee geeft u een constante.  
  
7.  `decimal_literal`  
  
     Decimale letterlijke waarden zijn getallen weergegeven met behulp van de decimale notatie of wetenschappelijke notatie.  
  
8.  `hexadecimal_literal`  
  
     Hexadecimale letterlijke waarden zijn getallen weergegeven met behulp van het voorvoegsel '0 x' gevolgd door een of meer hexadecimale cijfers.  
  
9. `<string_constant>`  
  
     Hiermee geeft u een constante van het type String.  
  
10. `string _literal`  
  
     Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen. Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: ').  
  
 Volgende escapereeksen worden toegestaan:  
  
|**Escape-reeks**|**Beschrijving**|**Unicode-teken**|  
|-|-|-|  
|\\'|enkel aanhalingsteken (')|U + 0027|  
|\\"|aanhalingsteken (")|U + 0022|  
|\\\|omgekeerde schuine streep (\\)|U + 005C|  
|\\/|schuine streep (/)|U + 002F|  
|\ber|BACKSPACE|U + 0008|  
|\f|formulier feed|U + 000C|  
|\n|nieuwe regel|U + 000A|  
|\r|regelterugloop|U + 000D|  
|\t|tabblad|U + 0009|  
|\uXXXX|Een Unicode-teken is gedefinieerd door 4 hexadecimale cijfers.|U + XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a>Richtlijnen voor query-prestaties  
 Om een query toobe efficiënt voor een grote verzameling wordt uitgevoerd, moet deze filters die kunnen worden geleverd via een of meer indexen gebruiken.  
  
 Hallo na filters wordt voor het opzoeken van de index beschouwd:  
  
-   Gebruik gelijkheidsoperator (=) met een padexpressie document en een constante.  
  
-   Bereikoperatoren gebruiken (<, \<=, >, > =) met een padexpressie document en aantal constanten.  
  
-   Document padexpressie staat voor een expressie waarmee een constante pad in Hallo documenten uit de database-collectie Hallo waarnaar wordt verwezen.  
  
 **Document padexpressie**  
  
 Document padexpressies zijn expressies die een pad van de eigenschap of matrix indexeerfunctie beoordelaars via een document dat afkomstig is van de database verzameling documenten. Dit pad mag gebruikte tooidentify Hallo locatie waarnaar wordt verwezen in een filter rechtstreeks in het Hallo-documenten in Hallo database verzameling waarden.  
  
 Voor een expressie toobe beschouwd als een document padexpressie, de volgende vereisten:  
  
1.  Verwijzing Hallo verzameling root rechtstreeks.  
  
2.  Verwijzing naar eigenschap of constante matrix indexeerfunctie van sommige padexpressie document  
  
3.  Verwijzen naar een alias die bepaalde padexpressie document vertegenwoordigt.  
  
     **Syntaxis conventies**  
  
     Hallo volgende tabel beschrijft Hallo conventies toodescribe syntaxis in Hallo Quertytaal API-verwijzing.  
  
    |**Conventies**|**Gebruikt voor**|  
    |-|-|    
    |HOOFDLETTERS|Niet-hoofdlettergevoelige trefwoorden.|  
    |kleine letters|Trefwoorden hoofdlettergevoelig.|  
    |\<nonterminal >|Niet-eindigende, die is gedefinieerd afzonderlijk.|  
    |\<nonterminal >:: =|De definitie van de syntaxis van Hallo nonterminal.|  
    |other_terminal|Terminal (token) in de woorden in detail beschreven.|  
    |ID|ID. Kan de volgende tekens bevatten: a-z A-Z 0-9 _First teken mag niet een cijfer.|  
    |'tekenreeks'|Tekenreeks tussen aanhalingstekens. Hiermee kunt een geldige tekenreeks. Zie de beschrijving van een string_literal.|  
    |"symbool"|Letterlijke symbool die deel uitmaakt van het Hallo-syntaxis.|  
    |&#124; (verticale balk)|Alternatieven voor de syntaxis van de items. U kunt slechts één van de opgegeven Hallo-items.|  
    |[] /(brackets)|Vierkante haken plaatst u een of meer optionele items.|  
    |[,.. .n]|Geeft aan Hallo voorgaande item herhaalde n het aantal keren dat kan worden. Hallo-instanties worden gescheiden door komma's.|  
    |[.. .n]|Geeft aan Hallo voorgaande item herhaalde n het aantal keren dat kan worden. Hallo-instanties worden gescheiden door spaties.|  
  
##  <a name="bk_built_in_functions"></a>Ingebouwde functies  
 Azure Cosmos DB biedt veel ingebouwde SQL-functies. Hallo categorieën van ingebouwde functies worden hieronder vermeld.  
  
|Functie|Beschrijving|  
|--------------|-----------------|  
|[Wiskundige functies](#bk_mathematical_functions)|Hallo wiskundige functies elke uitvoeren van een berekening, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.|  
|[Controle van de functies van het type](#bk_type_checking_functions)|Hallo type controleren of functies kunnen u toocheck Hallo-type van een expressie in SQL-query's.|  
|[Tekenreeksfuncties](#bk_string_functions)|Hallo tekenreeksfuncties een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.|  
|[Matrixfuncties](#bk_array_functions)|Hallo matrixfuncties uitvoeren voor een bewerking in een matrix invoerwaarde en keer terug numerieke, de waarde voor Boole-waarde of een matrix.|  
|[Ruimtelijke functies](#bk_spatial_functions)|Hallo ruimtelijke functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.|  
  
###  <a name="bk_mathematical_functions"></a>Wiskundige functies  
 Hallo volgende functies een berekening uitgevoerd, meestal op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[BOOGCOS](#bk_acos)|[ASIN](#bk_asin)|  
|[BOOGTAN](#bk_atan)|[ATN2](#bk_atn2)|[MAXIMUM](#bk_ceiling)|  
|[CO 'S](#bk_cos)|[COT](#bk_cot)|[GRADEN](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOGBOEK](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[ENERGIEBEHEER](#bk_power)|  
|[RADIALEN](#bk_radians)|[AFRONDEN](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[VIERKANTE](#bk_square)|[AANMELDING](#bk_sign)|  
|[TAN](#bk_tan)|[GEHEEL](#bk_trunc)||  
  
####  <a name="bk_abs"></a>ABS  
 Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo ziet volgende voorbeeld Hallo resultaten van het gebruik van de functie ABS Hallo op drie verschillende aantallen.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a>BOOGCOS  
 Retourneert Hallo hoek in radialen, waarvan de cosinus is Hallo opgegeven numerieke expressie. ook wel de boogcosinus genoemd.  
  
 **Syntaxis**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo BOOGCOS van-1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a>ASIN  
 Retourneert Hallo hoek in radialen, waarvan de sinus Hallo is opgegeven numerieke expressie. Dit wordt ook boogsinus genoemd.  
  
 **Syntaxis**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo ASIN van-1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a>BOOGTAN  
 Retourneert Hallo hoek in radialen, waarvan de tangens Hallo is opgegeven numerieke expressie. Dit wordt ook arctangens genoemd.  
  
 **Syntaxis**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld retourneert Hallo BOOGTAN Hallo waarde opgegeven.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a>ATN2  
 Retourneert de hoofdsom Hallo van Hallo arctangens van y / x, uitgedrukt in radialen.  
  
 **Syntaxis**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt berekend Hallo ATN2 voor Hallo opgegeven x en y onderdelen.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a>MAXIMUM  
 Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld toont positieve numerieke negatief, en nulwaarden met Hallo functie CEILING.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a>CO 'S  
 Retourneert Hallo trigonometrische cosinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.  
  
 **Syntaxis**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgt berekent Hallo CO Hallo opgegeven hoek.  
  
```  
SELECT COS(14.78)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a>COT  
 Retourneert Hallo trigonometrische cotangens van Hallo hoek aangeduid in radialen, opgegeven in Hallo numerieke expressie.  
  
 **Syntaxis**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgt berekent Hallo COT van Hallo opgegeven hoek.  
  
```  
SELECT COT(124.1332)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a>GRADEN  
 Retourneert Hallo bijbehorende hoek in graden voor een hoek aangeduid in radialen.  
  
 **Syntaxis**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt het aantal graden Hallo in een hoek van radialen PI/2.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a>FLOOR  
 Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven.  
  
 **Syntaxis**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld toont positieve numerieke negatief, en nulwaarden met Hallo functie FLOOR.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a>EXP  
 Retourneert Hallo exponentiële waarde Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Opmerkingen**  
  
 Hallo constante **e** (2.718281...) is Hallo grondtal van de natuurlijke logaritme.  
  
 Hallo exponent van een getal is Hallo constante **e** toohello macht van Hallo getal gegenereerd. Bijvoorbeeld EXP(1.0) e = ^ 1.0 = 2.71828182845905 en EXP(10) e = ^ 10 = 22026.4657948067.  
  
 Hallo exponentiële van Hallo natuurlijke logaritme van een getal is Hallo getal zichzelf: EXP (LOGBOEKREGISTRATIE (n)) = n. En Hallo natuurlijke logaritme van een getal exponentiële Hallo Hallo getal zichzelf: logboek (EXP (n)) = n.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo exponentiële waarde van Hallo opgegeven variabele (10).  
  
```  
SELECT EXP(10)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Hallo retourneert volgende voorbeeld Hallo exponentiële waarde van Hallo natuurlijke logaritme van 20 en Hallo natuurlijke logaritme van Hallo exponentiële van 20. Omdat deze functies inverse functies van elkaar, Hallo retourwaarde zijn afgeronde voor drijvende komma berekening in beide gevallen is 20.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a>LOGBOEK  
 Retourneert Hallo natuurlijke logaritme van Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
-   `base`  
  
     Optionele numerieke argument dat Hallo voor Hallo logaritme ingesteld.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Opmerkingen**  
  
 Standaard retourneert LOG() Hallo natuurlijke logaritme. U kunt Hallo base Hallo logaritme tooanother waarde wijzigen met behulp van Hallo optionele base-parameter.  
  
 Hallo natuurlijke logaritme is Hallo logaritme toohello base **e**, waarbij **e** een irrational constante ongeveer gelijk too2.718281828 is.  
  
 Hallo natuurlijke logaritme van Hallo exponentiële van een getal is Hallo getal zichzelf: logboek (EXP (n)) = n. En exponentiële van Hallo natuurlijke logaritme van een getal Hallo Hallo getal zichzelf: EXP (LOGBOEKREGISTRATIE (n)) = n.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo logaritme waarde van Hallo opgegeven variabele (10).  
  
```  
SELECT LOG(10)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Hallo volgende voorbeeld wordt berekend Hallo logboek voor Hallo exponent van een getal.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a>LOG10  
 Retourneert Hallo logaritme met grondtal 10 van Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Opmerkingen**  
  
 Hallo LOG10 en functies van POWER worden omgekeerd gerelateerde tooone een andere. Bijvoorbeeld 10 ^ LOG10(n) = n.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt een variabele gedeclareerd en retourneert Hallo LOG10 waarde van Hallo opgegeven variabele (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a>PI  
 Retourneert Hallo constante waarde van PI.  
  
 **Syntaxis**  
  
```  
PI ()  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo-waarde van PI.  
  
```  
SELECT PI()  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a>ENERGIEBEHEER  
 Retourneert de waarde van de opgegeven Hallo Hallo expressie toohello opgegeven macht.  
  
 **Syntaxis**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
-   `y`  
  
     Hallo power toowhich tooraise is `numeric_expression`.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld laat zien verhogen van een aantal toohello macht 3 (Hallo kubus van Hallo getal).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a>RADIALEN  
 Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd.  
  
 **Syntaxis**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld duurt enkele hoeken als invoer en de bijbehorende Radiaal waarden retourneert.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a>AFRONDEN  
 Retourneert een numerieke waarde afgeronde toohello dichtstbijzijnde integer-waarde.  
  
 **Syntaxis**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt afgerond Hallo positieve en negatieve getallen toohello dichtstbijzijnde integer te volgen.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a>AANMELDING  
 Retourneert Hallo positieve (+ 1), nul (0) of minteken (-1) Hallo opgegeven numerieke expressie.  
  
 **Syntaxis**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt Hallo aanmelding waarden van de getallen uit too2-2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a>SIN  
 Retourneert Hallo trigonometrische sinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.  
  
 **Syntaxis**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo voorbeeld te volgen berekent Hallo SIN van Hallo opgegeven hoek.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a>SQRT  
 Retourneert de vierkantswortel van Hallo Hallo opgegeven numerieke waarde.  
  
 **Syntaxis**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo vierkante roots van de getallen 1-3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a>VIERKANTE  
 Retourneert Hallo vierkante Hallo opgegeven numerieke waarde.  
  
 **Syntaxis**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo wordt volgende voorbeeld de kwadraten Hallo van getallen 1-3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a>TAN  
 Retourneert de tangens Hallo Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.  
  
 **Syntaxis**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt berekend Hallo tangens van PI () / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a>GEHEEL  
 Retourneert een numerieke waarde ingekorte toohello dichtstbijzijnde integer-waarde.  
  
 **Syntaxis**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Argumenten**  
  
-   `numeric_expression`  
  
     Is een numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt afgekapt Hallo positieve en negatieve getallen toohello dichtstbijzijnde integerwaarde te volgen.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a>Controle van de functies van het type  
 Hallo volgende functies ondersteunen typecontrole tegen invoerwaarden en elk een Booleaanse waarde retourneren.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a>IS_ARRAY  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een matrix.  
  
 **Syntaxis**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_ARRAY-functie.  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a>IS_BOOL  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een Booleaanse waarde.  
  
 **Syntaxis**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_BOOL-functie.  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a>IS_DEFINED  
 Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen.  
  
 **Syntaxis**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 voorbeeld-controles voor de aanwezigheid van een eigenschap binnen Hallo HALLO hallo opgegeven JSON-document. Hallo eerst ' true ' geretourneerd omdat "a" aanwezig is, maar Hallo tweede onwaar retourneert omdat "b" ontbreekt.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a>IS_NULL  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is null.  
  
 **Syntaxis**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_NULL-functie.  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a>IS_NUMBER  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een getal.  
  
 **Syntaxis**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_NULL-functie.  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a>IS_OBJECT  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een JSON-object.  
  
 **Syntaxis**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_OBJECT-functie.  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a>IS_PRIMITIVE  
 Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo type Hallo opgegeven expressie is een primitief (string, Boolean, numerieke of null).  
  
 **Syntaxis**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_PRIMITIVE-functie.  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a>IS_STRING  
 Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een tekenreeks.  
  
 **Syntaxis**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Argumenten**  
  
-   `expression`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd objecten van JSON Boolean, getal, string, null, object, matrix en niet-gedefinieerde typen met behulp van Hallo IS_STRING-functie.  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a>Tekenreeks-functies  
 Hallo volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[BEVAT](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LINKS](#bk_left)|[LENGTE](#bk_length)|  
|[LAGERE](#bk_lower)|[LTRIM](#bk_ltrim)|[VERVANGEN](#bk_replace)|  
|[REPLICEREN](#bk_replicate)|[OMKEREN](#bk_reverse)|[RECHTS](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[DE SUBTEKENREEKS](#bk_substring)|  
|[BOVENSTE](#bk_upper)|||  
  
####  <a name="bk_concat"></a>CONCAT  
 Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden.  
  
 **Syntaxis**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld retourneert Hallo samengevoegd tekenreeks Hallo opgegeven waarden.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a>BEVAT  
 Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat.  
  
 **Syntaxis**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt gecontroleerd als "abc" bevat "ab" en "d".  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a>ENDSWITH  
 Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt.  
  
 **Syntaxis**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo "abc" op "b" en 'bc eindigt'.  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a>INDEX_OF  
 Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden.  
  
 **Syntaxis**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo wordt volgende voorbeeld de index Hallo van verschillende subtekenreeksen binnen "abc".  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a>LINKS  
 Retourneert het linkergedeelte van een tekenreeks Hallo Hello opgegeven aantal tekens.  
  
 **Syntaxis**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
-   `num_expr`  
  
     Is geldige numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld retourneert Hallo links onderdeel van "abc" voor waarden van verschillende lengte.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a>LENGTE  
 Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie.  
  
 **Syntaxis**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo lengte van een tekenreeks.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a>LAGERE  
 Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren.  
  
 **Syntaxis**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toouse lager in een query.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a>LTRIM  
 Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden.  
  
 **Syntaxis**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toouse LTRIM binnen een query.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a>VERVANGEN  
 Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks.  
  
 **Syntaxis**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld ziet u hoe toouse vervangen in een query.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a>REPLICEREN  
 Herhaalt een string-waarde van een opgegeven aantal keren.  
  
 **Syntaxis**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
-   `num_expr`  
  
     Is geldige numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld ziet u hoe toouse REPLICEREN in een query.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a>OMKEREN  
 Retourneert de omgekeerde volgorde Hallo van een string-waarde.  
  
 **Syntaxis**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld ziet u hoe toouse REVERSE in een query.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a>RECHTS  
 Hallo rechts deel uit van een tekenreeks retourneert Hello opgegeven aantal tekens.  
  
 **Syntaxis**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
-   `num_expr`  
  
     Is geldige numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hello wordt volgende voorbeeld het rechterdeel Hallo van "abc" voor verschillende lengtewaarden.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a>RTRIM  
 Retourneert een tekenreeksexpressie na het afsluitende spaties verwijderen.  
  
 **Syntaxis**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toouse RTRIM binnen een query.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a>STARTSWITH  
 Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo op de tweede met de Hallo begint.  
  
 **Syntaxis**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld controleert of hello string "abc" begint met "b" en "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a>DE SUBTEKENREEKS  
 Retourneert deel uit van een tekenreeksexpressie die begint bij Hallo opgegeven teken op nul gebaseerde positie en blijft toohello opgegeven lengte of toohello einde van de Hallo-tekenreeks.  
  
 **Syntaxis**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
-   `num_expr`  
  
     Is geldige numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo retourneert volgende voorbeeld Hallo subtekenreeks van "abc" beginnen bij 1 en voor een lengte van 1 teken.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a>BOVENSTE  
 Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren.  
  
 **Syntaxis**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Argumenten**  
  
-   `str_expr`  
  
     Is geldige tekenreeksexpressie.  
  
 **Retourtypen**  
  
 Retourneert een tekenreeksexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toouse hoofdletters in een query  
  
```  
SELECT UPPER("Abc")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a>Matrixfuncties  
 Hallo scalaire functies na een bewerking uitvoeren op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a>ARRAY_CONCAT  
 Retourneert een matrix die Hallo resultaat is van het samenvoegen van twee of meer matrixwaarden.  
  
 **Syntaxis**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Argumenten**  
  
-   `arr_expr`  
  
     Is geldige matrixexpressie.  
  
 **Retourtypen**  
  
 Retourneert een matrixexpressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld hoe tooconcatenate twee matrices.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a>ARRAY_CONTAINS  
 Retourneert een Booleaanse waarde die aangeeft of de matrix Hallo Hallo bevat een waarde opgegeven.  
  
 **Syntaxis**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Argumenten**  
  
-   `arr_expr`  
  
     Is geldige matrixexpressie.  
  
-   `expr`  
  
     Is geldige expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse waarde.  
  
 **Voorbeelden**  
  
 Hallo volgt hoe toocheck voor lidmaatschap in een matrix met ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a>ARRAY_LENGTH  
 Retourneert Hallo aantal elementen Hallo matrixexpressie opgegeven.  
  
 **Syntaxis**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Argumenten**  
  
-   `arr_expr`  
  
     Is geldige matrixexpressie.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld hoe tooget lengte van een matrix met ARRAY_LENGTH Hallo.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a>ARRAY_SLICE  
 Retourneert deel van een matrixexpressie.
  
 **Syntaxis**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumenten**  
  
-   `arr_expr`  
  
     Is geldige matrixexpressie.  
  
-   `num_expr`  
  
     Is geldige numerieke expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse waarde.  
  
 **Voorbeelden**  
  
 Hallo volgt hoe tooget deel uit van een matrix met ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a>Ruimtelijke functies  
 Hallo volgende scalaire functies een bewerking uitvoeren op een invoerwaarde ruimtelijke object en een numeriek gegevenstype of Booleaanse waarde retourneren.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a>ST_DISTANCE  
 Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.  
  
 **Syntaxis**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenten**  
  
-   `spatial_expr`  
  
     Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.  
  
 **Retourtypen**  
  
 Retourneert een numerieke expressie met Hallo afstand. Dit wordt uitgedrukt in meters voor referentiesysteem Hallo-standaard.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe tooreturn alle familie documenten die binnen 30 km Hallo locatie met Hallo de ingebouwde functie ST_DISTANCE opgegeven. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a>ST_WITHIN  
 Retourneert een Booleaanse expressie Hallo GeoJSON (punt, Polygon of LineString) opgegeven object in het eerste argument Hallo is binnen Hallo GeoJSON (punt, Polygon of LineString) in het tweede argument Hallo.  
  
 **Syntaxis**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenten**  
  
-   `spatial_expr`  
  
     Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.  
 
-   `spatial_expr`  
  
     Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse waarde.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld ziet u hoe toofind alle familie documenten binnen een veelhoek met ST_WITHIN.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a>ST_INTERSECTS  
 Retourneert een Booleaanse expressie waarmee wordt aangegeven of de Hallo GeoJSON object (punt, Polygon of LineString) opgegeven in het eerste argument Hallo Hallo GeoJSON (punt, Polygon of LineString) in het tweede argument Hallo polygoonring.  
  
 **Syntaxis**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenten**  
  
-   `spatial_expr`  
  
     Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.  
 
-   `spatial_expr`  
  
     Is geldige expressie voor GeoJSON punt, Polygon of LineString-object.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse waarde.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toofind alle gebieden die in de polygoonring met Hallo gegeven veelhoek.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a>ST_ISVALID  
 Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.  
  
 **Syntaxis**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumenten**  
  
-   `spatial_expr`  
  
     Is geldige GeoJSON punt, Polygon of LineString-expressie.  
  
 **Retourtypen**  
  
 Retourneert een Booleaanse expressie.  
  
 **Voorbeelden**  
  
 Hallo volgende voorbeeld wordt getoond hoe toocheck als een punt ST_VALID geldig is.  
  
 Dit punt heeft bijvoorbeeld een Breedtegraadwaarde die niet in Hallo geldig waardenbereik [-90, 90], dus Hallo query retourneert false.  
  
 Voor multilinestring, Hallo GeoJSON specificatie moet Hallo laatste coördinaat paar opgegeven Hallo dezelfde als de eerste, toocreate Hallo een gesloten vorm. Punten in een polygoon moeten worden opgegeven in rechtsom volgorde. Een veelhoek in rechtsom order opgegeven vertegenwoordigt Hallo inverse van Hallo regio erin.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED  
 Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.  
  
 **Syntaxis**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumenten**  
  
-   `spatial_expr`  
  
     Is geldige GeoJSON-punt of de veelhoek expressie.  
  
 **Retourtypen**  
  
 Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt opgegeven of veelhoek expressie geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.  
  
 **Voorbeelden**  
  
 Hallo volgt hoe geldigheid van de toocheck (met details) met behulp van ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Hier volgt Hallo resultatenset.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Volgende stappen  
 [SQL-syntaxis en SQL-query voor Azure Cosmos-DB](documentdb-sql-query.md)   
 [Azure DB Cosmos-documentatie](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
