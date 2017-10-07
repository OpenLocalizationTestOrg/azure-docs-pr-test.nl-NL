---
title: aaaSQL query's voor Azure Cosmos DB DocumentDB-API | Microsoft Docs
description: Meer informatie over SQL-syntaxis, database-concepten en SQL-query's voor Azure Cosmos DB. SQL kan worden gebruikt als een JSON-querytaal in Azure Cosmos DB.
keywords: SQL-syntaxis, sql-query, sql-query's, json-querytaal, database-concepten en sql-query's, statistische functies
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>SQL-query's voor Azure Cosmos DB DocumentDB API
Microsoft Azure Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van SQL (Structured Query Language) als een JSON-querytaal. Cosmos DB is volledig zonder schema. Doordat de streven toohello JSON-gegevensmodel rechtstreeks in de database-engine hello biedt deze automatische indexering van JSON-documenten zonder expliciet schema of het maken van secundaire indexen. 

Tijdens het Hallo-querytaal ontwerpen voor Cosmos DB, zijn twee drie doelen voor ogen:

* In plaats van een nieuwe JSON-querytaal vruchtbare, maar we wilden toosupport SQL. SQL is een van de talen voor Hallo bekend en meest populaire query. Cosmos DB SQL biedt een formele programmeermodel voor uitgebreide query's via JSON-documenten.
* Als een JSON-document-database kan worden uitgevoerd van JavaScript rechtstreeks in de database-engine Hallo wilden we van toouse JavaScript-programmeermodel Hallo basis voor onze querytaal. Hallo DocumentDB API SQL verankerd ligt in de JavaScript-typesysteem, evaluatie van expressies en functieaanroep. Deze beurt biedt een natuurlijke programmeermodel voor projecties relationele, hiërarchische navigatie in JSON-documenten, self joins, ruimtelijke query's en aanroep van de gebruiker gedefinieerde functies (UDF's) geschreven volledig in JavaScript, onder andere functies. 

We zijn ervan overtuigd dat deze mogelijkheden belangrijke tooreducing Hallo wrijving tussen Hallo-toepassing en Hallo-database zijn en essentieel voor de productiviteit van ontwikkelaars zijn.

We raden aan de slag door bekijkt hello volgende video Aravind Ramachandran toont waar opvragen mogelijkheden Cosmos-database, en in via onze [Queryspeelplaats](http://www.documentdb.com/sql/demo), waarbij u kunt Cosmos-database uitproberen en SQL-query's op uitvoeren onze gegevensset.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Keer vervolgens terug toothis artikel, waar u begint met een SQL-query-zelfstudie die u bij enkele eenvoudige JSON-documenten en de SQL-opdrachten helpt.

## <a id="GettingStarted"></a>Aan de slag met SQL-opdrachten in een Cosmos-DB
toosee Cosmos DB SQL op werken, laten we beginnen met een paar eenvoudige JSON-documenten en enkele eenvoudige query's op deze doorlopen. U kunt deze twee JSON-documenten over twee families. Met Cosmos DB hoeven we geen toocreate geen schema's of secundaire indexen expliciet. Er hoeft alleen maar tooinsert Hallo JSON-documenten tooa Cosmos DB verzameling en vervolgens een query. Hier hebben we een eenvoudige JSON Documenteer voor Hallo Andersen family, Hallo ouders, onderliggende elementen (en hun huisdieren), adres en registratie-informatie. Hallo document heeft tekenreeksen, getallen, Booleaanse waarden, matrices en geneste eigenschappen. 

**Document**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Hier volgt een tweede document een subtiele verschil – `givenName` en `familyName` worden gebruikt in plaats van `firstName` en `lastName`.

**Document**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Nu gaan we proberen enkele query's op basis van deze gegevens toounderstand aantal Hallo aspecten van DocumentDB API SQL sleutel. Bijvoorbeeld, Hallo volgende query retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met `AndersenFamily`. Omdat het een `SELECT *`, Hallo-uitvoer van Hallo query Hallo voltooid JSON-document is:

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Bekijk nu Hallo geval waar we tooreformat Hallo JSON-uitvoer in een andere vorm moeten. Deze query projecten een nieuwe JSON object met twee geselecteerde velden naam en plaats, wanneer Hallo plaats Hallo dezelfde naam heeft als Hallo status. In dit geval 'NY, NY' komt overeen met.

**Query**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Resultaten**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


de volgende query Hallo retourneert alle Hallo opgegeven namen van kinderen in Hallo familie-id die overeenkomt met `WakefieldFamily` Hallo plaats waar je woont geordend.

**Query**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Resultaten**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Willen we graag toodraw aandacht tooa enkele opmerkelijk aspecten van Hallo Cosmos DB querytaal via Hallo voorbeelden die we tot nu toe hebt gezien:  

* Aangezien DocumentDB API SQL op JSON-waarden werkt, behandelt structuur in de vorm van entiteiten in plaats van rijen en kolommen. Daarom Hallo taal kunt u toonodes van Hallo structuur op elke willekeurige diepte zoals verwijzen `Node1.Node2.Node3…..Nodem`, vergelijkbare toorelational SQL verwijzende toohello Twee onderdeelverwijzing van `<table>.<column>`.   
* Hallo structured query language werkt met schema minder gegevens. Daarom dynamisch Hallo type system behoeften toobe gebonden. Hallo kan dezelfde expressie resulteert in verschillende typen op verschillende documenten. Hallo-resultaat van een query is een geldige JSON-waarde, maar toobe van een vast schema kan niet worden gegarandeerd.  
* Cosmos DB ondersteunt alleen strikte JSON-documenten. Dit betekent dat Hallo typesysteem en expressies zijn beperkt toodeal alleen met JSON-typen. Raadpleeg toohello [JSON-specificatie](http://www.json.org/) voor meer informatie.  
* Een Cosmos-DB-verzameling is een container zonder schema van JSON-documenten. Hallo-relaties in gegevensentiteiten binnen en tussen documenten in een verzameling worden impliciet door containment en niet door de primaire sleutel en refererende sleutels relaties vastgelegd. Dit is een belangrijk aspect waard wijzen op in het licht Hallo intra-document joins verderop in dit artikel wordt besproken.

## <a id="Indexing"></a>Cosmos DB indexeren
Voordat we Hallo DocumentDB API SQL-syntaxis krijgen, is het waard Hallo ontwerp in Cosmos DB te indexeren. 

Hallo-doel van de indexen van de database is tooserve query's in hun diverse vormen en vormen met minimale brongebruik (zoals CPU en input/output) terwijl er goed doorvoer en lage latentie. Vaak vereist Hallo keuze van de juiste index Hallo voor query's in een database veel planning en experimenteren. Deze aanpak vormt een uitdaging voor schema-minder databases waar de Hallo gegevens voldoen niet tooa strikte schema en snel ontwikkeld. 

Wanneer we Hallo Cosmos DB indexering subsysteem ontworpen, instellen wij daarom Hallo doelstellingen te volgen:

* Documenten te indexeren zonder schema: Hallo indexeren subsysteem geen vereist een schema-informatie of veronderstellingen over schema van Hallo documenten. 
* Ondersteuning voor efficiënte, geavanceerde hiërarchische en relationele query's: Hallo index ondersteunt Hallo Cosmos-DB-querytaal efficiënt, inclusief ondersteuning voor hiërarchische en relationele projecties.
* Ondersteuning voor consistente query's in face of een volgehouden volume van schrijfbewerkingen: voor schrijven met hoge doorvoer werkbelastingen met consistente query's, Hallo index incrementeel efficiënt en online in Hallo face van een duurzame volume van schrijfbewerkingen wordt bijgewerkt. Hallo consistent index-update is cruciaal tooserve Hallo query's op Hallo consistentieniveau in welke service Hallo gebruiker geconfigureerd Hallo-document.
* Ondersteuning voor multitenancy: gegeven Hallo reservering gebaseerde model voor de resource governance tussen tenants, index-updates worden uitgevoerd binnen het budget Hallo van systeemresources (CPU, geheugen en input/output-bewerkingen per seconde) die per replica worden toegewezen. 
* Opslagruimte: voor de kosteneffectiviteit, Hallo op schijf opslag overhead van Hallo index is gebonden en voorspelbaar. Dit is cruciaal omdat Cosmos DB Hallo developer toomake op basis van kosten wisselwerking tussen de overhead van de index in de relatie toohello queryprestaties kunt.  

Raadpleeg toohello [Azure Cosmos DB voorbeelden](https://github.com/Azure/azure-documentdb-net) op MSDN voor voorbeelden die laat zien hoe tooconfigure Hallo indexeringsbeleid voor een verzameling. Laten we nu krijgen Hallo details van hello Azure Cosmos DB SQL-syntaxis.

## <a id="Basics"></a>Basisprincipes van een Azure Cosmos DB SQL-query
Elke query bestaat uit een SELECT-component en een optionele FROM en WHERE-componenten per ANSI SQL-standaarden. Normaal gesproken voor elke query moet Hallo-bron in de component FROM Hallo is geïnventariseerd. Hallo filter vervolgens in de WHERE-component wordt toegepast op Hallo bron tooretrieve Hallo een subset van JSON-documenten. Ten slotte Hallo SELECT-component wordt gebruikt tooproject Hallo aangevraagd JSON-waarden in Hallo lijst selecteren.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>FROM-component
Hallo `FROM <from_specification>` component is optioneel tenzij Hallo-bron is gefilterd of later in de query Hallo geprojecteerd. Hallo-doel van deze component is toospecify Hallo-gegevensbron bij welke Hallo query moet functioneren. Meestal de volledige verzameling Hallo Hallo-bron is, maar een kunt in plaats daarvan een subset van Hallo verzameling opgeven. 

Een query, zoals `SELECT * FROM Families` geeft aan dat het volledige verzameling worden Families Hallo Hallo bron via welke tooenumerate. Een speciale ROOT-id kan gebruikte toorepresent Hallo verzameling in plaats van met de naam van de verzameling Hallo zijn. Hallo bevat volgende lijst Hallo-regels die per query worden afgedwongen:

* Hallo-verzameling kan worden alias hebben, zoals `SELECT f.id FROM Families AS f` of gewoon `SELECT f.id FROM Families f`. Hier `f` is Hallo equivalent van `Families`. `AS`is een optioneel trefwoord tooalias Hallo-id.
* Eenmaal alias Hallo oorspronkelijke bron kan niet worden gebonden. Bijvoorbeeld: `SELECT Families.id FROM Families f` syntaxis is ongeldig omdat het Hallo-id 'Families' kan niet meer worden omgezet.
* Alle eigenschappen die toobe waarnaar wordt verwezen moeten moet volledig gekwalificeerd zijn. In de Hallo afwezigheid van de toepassing van de strikte schema, is dit afgedwongen tooavoid geen niet-eenduidige bindingen. Daarom `SELECT id FROM Families f` syntaxis is ongeldig omdat de eigenschap Hallo `id` niet is gebonden.

### <a name="subdocuments"></a>Subdocumenten
Hallo-bron kan ook worden verlaagd tooa kleinere subset. Bijvoorbeeld tooenumerating alleen een substructuur in elk document, Hallo subroot kan vervolgens worden Hallo bron, zoals wordt weergegeven in het volgende voorbeeld Hallo:

**Query**

    SELECT * 
    FROM Families.children

**Resultaten**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Hallo hierboven voorbeeld gebruikt een matrix als Hallo bron, een object kan ook worden gebruikt als bron hello, dit is wat wordt weergegeven in het volgende voorbeeld Hallo: een geldige JSON-waarde (geen niet-gedefinieerd) die kan worden gevonden in bron hello wordt beschouwd als voor insluiting in Hallo resultaat van Hallo-query. Als sommige families beschikt niet over een `address.state` waarde, in het queryresultaat Hallo worden uitgesloten.

**Query**

    SELECT * 
    FROM Families.address.state

**Resultaten**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>WHERE-component
WHERE-component Hallo (**`WHERE <filter_condition>`**) is optioneel. Deze geeft Hallo voorwaarde(n) dat Hallo JSON-documenten geleverd door het Hallo-bron moeten voldoen aan volgorde toobe opgenomen als onderdeel van Hallo resultaat. Elk JSON-document moet worden geëvalueerd Hallo opgegeven voorwaarden te 'true' toobe in aanmerking voor Hallo resultaat. Hallo waar component wordt gebruikt door Hallo index laag in volgorde toodetermine Hallo absolute kleinste subset van brondocumenten die deel van Hallo resultaat uitmaken kunnen. 

Hallo volgende query haalt u documenten met een eigenschap name waarvan de waarde `AndersenFamily`. Elk document dat u beschikt niet over een eigenschap name of waar Hallo waarde komt niet overeen met `AndersenFamily` is uitgesloten. 

**Query**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Hallo vorige voorbeeld blijkt een eenvoudige gelijkheid-query. DocumentDB-API SQL ondersteunt ook een groot aantal scalaire expressies. Hallo meest gebruikte binaire bestanden en unaire expressies zijn. Eigenschap verwijzingen uit Hallo bron JSON-object zijn ook geldig expressies. 

binaire operators na Hallo worden momenteel ondersteund en kan worden gebruikt in query's, zoals wordt weergegeven in Hallo volgen voorbeelden:  

<table>
<tr>
<td>Rekenkundige bewerking</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Bitsgewijs</td>    
<td>|, &, ^, <<>>,, >>> (nul opvulling rechts verplaatsen)</td>
</tr>
<tr>
<td>Logische</td>
<td>EN, OF NIET</td>
</tr>
<tr>
<td>Vergelijking</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Tekenreeks</td>    
<td>|| (samenvoegen)</td>
</tr>
</table>  


We gaan verdiepen in enkele query's met behulp van de binaire operators.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


unaire operators Hallo +,-, ~ worden ook ondersteund, en niet kan worden gebruikt in query's, zoals wordt weergegeven in het volgende voorbeeld Hallo:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Bovendien toobinary en unaire operators, eigenschap verwijzingen zijn ook toegestaan. Bijvoorbeeld: `SELECT * FROM Families f WHERE f.isRegistered` retourneert Hallo JSON-document met de eigenschap Hallo `isRegistered` waarbij de waarde van eigenschap Hallo gelijk toohello JSON is `true` waarde. Andere waarden (false, null, niet-gedefinieerde, `<number>`, `<string>`, `<object>`, `<array>`, enzovoort) toohello brondocument wordt uitgesloten van Hallo resultaat leidt. 

### <a name="equality-and-comparison-operators"></a>Gelijkheid en het vergelijkingstype operators
Hallo volgende tabel toont Hallo resultaat van de gelijkheid vergelijkingen in DocumentDB API SQL tussen twee typen die JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Niet-gedefinieerd</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Booleaanse waarde</strong>
         </td>
         <td valign="top">
            <strong>Aantal</strong>
         </td>
         <td valign="top">
            <strong>Tekenreeks</strong>
         </td>
         <td valign="top">
            <strong>Object</strong>
         </td>
         <td valign="top">
            <strong>Matrix</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Niet-gedefinieerd<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Booleaanse waarde<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Aantal<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Tekenreeks<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Object<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Matrix<strong>
         </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
Niet-gedefinieerd </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Voor andere vergelijkingsoperators zoals >, > =,! =, < en < =, hello volgende regels zijn van toepassing:   

* Vergelijking van verschillende typen resulteert in Undefined.
* Vergelijking tussen de twee objecten of twee matrices resulteert in een Undefined.   

Als Hallo resultaat van de scalaire expressie Hallo in Hallo-filter is niet is gedefinieerd, Hallo bijbehorende document zou niet opgenomen in Hallo resultaat, aangezien Undefined logisch te 'true' niet vergelijken.

### <a name="between-keyword"></a>TUSSEN sleutelwoord
U kunt ook Hallo BETWEEN sleutelwoord tooexpress query's op bereiken met waarden zoals in de ANSI SQL. TUSSEN kan worden gebruikt met tekenreeksen of getallen.

Deze query retourneert bijvoorbeeld alle familie documenten in welke Hallo is het eerste onderliggende hoogwaardige tussen 1-5 (zowel liggen). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

In tegenstelling tot in de ANSI-SQL, kunt u ook gebruiken Hallo BETWEEN component in hello FROM-component zoals in het volgende voorbeeld Hallo.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Voor snellere tijden in uitvoering, houd er rekening mee toocreate een indexeringsbeleid die gebruikmaakt van een type bereik index op basis van een numerieke eigenschappen/paden die zijn gefilterd in Hallo BETWEEN-component. 

Hallo belangrijkste verschil tussen het gebruik van BETWEEN in DocumentDB-API en ANSI SQL is dat u kunt snelle bereik een query uitgevoerd naar eigenschappen van gemengde gegevenstypen: bijvoorbeeld wellicht 'hoogwaardige' is geen getal (5) in een aantal documenten en tekenreeksen in andere gevallen ('grade4'). In dergelijke gevallen, wordt zoals in JavaScript, een vergelijking tussen de twee verschillende typen resulteert in een 'niet-gedefinieerde' en het Hallo-document overgeslagen.

### <a name="logical-and-or-and-not-operators"></a>Logische (AND, OR en NOT) operators
Logische operators bewerken Boole-waarden. Hallo logische waarheid tabellen voor deze operators worden weergegeven in Hallo tabellen te volgen.

| OF | True | False | Niet-gedefinieerd |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Niet-gedefinieerd |
| Niet-gedefinieerd |True |Niet-gedefinieerd |Niet-gedefinieerd |

| EN | True | False | Niet-gedefinieerd |
| --- | --- | --- | --- |
| True |True |False |Niet-gedefinieerd |
| False |False |False |False |
| Niet-gedefinieerd |Niet-gedefinieerd |False |Niet-gedefinieerd |

| NIET |  |
| --- | --- |
| True |False |
| False |True |
| Niet-gedefinieerd |Niet-gedefinieerd |

### <a name="in-keyword"></a>TREFWOORD
Hallo sleutelwoord kan gebruikte toocheck zijn of een opgegeven waarde komt overeen met elke waarde in een lijst. Bijvoorbeeld, retourneert deze query alle familie documenten waar Hallo-id van 'WakefieldFamily' of 'AndersenFamily'. 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

In dit voorbeeld retourneert alle documenten waar Hallo status is Hallo opgegeven waarden.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Ternair (?) en operators Coalesce (?)
Hallo Ternair en Coalesce operators kunnen worden gebruikt toobuild voorwaardelijke expressies, vergelijkbare toopopular programmeertalen zoals C# en JavaScript. 

Hallo Ternair (?) operator is erg handig als maken nieuwe JSON-eigenschappen op Hallo vliegen. Bijvoorbeeld, kunt nu u query's tooclassify Hallo klasse niveaus in een menselijke leesbare vorm zoals beginnende/tussenliggende/Geavanceerd zoals hieronder wordt weergegeven.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

U kunt ook Hallo aanroepen toohello operator zoals in de onderstaande Hallo query nesten.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Als met andere operators query zijn als hello waarnaar wordt verwezen eigenschappen in Hallo voorwaardelijke expressies ontbreken in elk document of als het Hallo-typen worden vergeleken zijn verschillend zijn, klikt u vervolgens die documenten uitgesloten in Hallo queryresultaten.

Hallo Coalesce (?) operator kan worden tooefficiently selectievakje (ook gebruikt voor de aanwezigheid van een eigenschap Hallo is gedefinieerd) in een document. Dit is handig wanneer een query op semi-gestructureerde of gegevens van gemengde typen. Bijvoorbeeld, retourneert deze query Hallo 'lastName' indien aanwezig, of Hallo 'Achternaam' als dit niet aanwezig.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Tussen aanhalingstekens eigenschapsaccessor
U kunt ook toegang tot eigenschappen met Hallo tussen aanhalingstekens eigenschap operator `[]`. Bijvoorbeeld: `SELECT c.grade` en `SELECT c["grade"]` equivalent zijn. Deze syntaxis is nuttig wanneer u een eigenschap die spaties, speciale tekens bevat of gebeurt tooshare Hallo dezelfde naam als een SQL-sleutelwoord of een gereserveerd woord tooescape nodig.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>SELECT-component
Hallo SELECT-component (**`SELECT <select_list>`**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit Hallo query, net zoals in de ANSI SQL. Hallo subset die boven op Hallo brondocumenten zijn gefilterd worden doorgegeven naar Hallo Projectiefase, waarbij Hallo opgegeven JSON-waarden worden opgehaald en een nieuwe JSON-object voor elke doorgegeven op deze invoer is samengesteld. 

Hallo volgende voorbeeld toont een typische SELECT-query. 

**Query**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Geneste eigenschappen
In de Hallo voorbeeld te volgen, we twee geneste eigenschappen projecteert `f.address.state` en `f.address.city`.

**Query**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Projectie biedt ook ondersteuning voor JSON-expressies, zoals wordt weergegeven in Hallo voorbeeld te volgen:

**Query**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Bekijk Hallo-rol van `$1` hier. Hallo `SELECT` component moet een JSON-object toocreate en omdat er geen sleutel is opgegeven, gebruiken we de impliciete argument variabele namen die beginnen met `$1`. Deze query retourneert bijvoorbeeld twee impliciete argumentvariabelen, met het label `$1` en `$2`.

**Query**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Aliasing
Nu gaan we uitbreiden Hallo voorbeeld hierboven expliciete aliasing van waarden. Hallo-sleutelwoord gebruikt voor aliasing is. Dit is optioneel, zoals wordt weergegeven tijdens het projecteren Hallo tweede waarde als `NameInfo`. 

Als een query over twee eigenschappen met Hallo dezelfde naam aliasing moet gebruikte toorename een of beide eigenschappen Hallo zodat ze ondubbelzinnig zijn gemaakt in Hallo geprojecteerd resultaat.

**Query**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Scalaire expressies
Bovendien tooproperty verwijst naar, Hallo SELECT-component biedt ook ondersteuning voor scalaire expressies zoals constanten, aritmetische expressies, logische expressies, enzovoort. Hier is bijvoorbeeld een eenvoudige 'Hallo wereld'-query.

**Query**

    SELECT "Hello World"

**Resultaten**

    [{
      "$1": "Hello World"
    }]


Hier volgt een voorbeeld van een complexere die gebruikmaakt van een scalaire expressie.

**Query**

    SELECT ((2 + 11 % 7)-2)/3    

**Resultaten**

    [{
      "$1": 1.33333
    }]


In Hallo voorbeeld te volgen, is Hallo resultaat van de scalaire expressie Hallo het een Booleaanse waarde.

**Query**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Resultaten**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Maken van het object en array
Een andere belangrijke functie van DocumentDB API SQL is array-object maken. In het vorige voorbeeld hello, houd er rekening mee dat er een nieuwe JSON-object gemaakt. Op deze manier kunt een ook matrices maken zoals in Hallo volgen voorbeelden:

**Query**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Resultaten**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>WAARDE sleutelwoord
Hallo **waarde** sleutelwoord biedt een manier tooreturn JSON-waarde. Bijvoorbeeld Hallo query retourneert Hallo scalaire hieronder `"Hello World"` in plaats van `{$1: "Hello World"}`.

**Query**

    SELECT VALUE "Hello World"

**Resultaten**

    [
      "Hello World"
    ]


Hallo volgende query retourneert Hallo JSON-waarde zonder Hallo `"address"` label in Hallo resultaten.

**Query**

    SELECT VALUE f.address
    FROM Families f    

**Resultaten**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Hallo volgende voorbeeld breidt deze tooshow hoe tooreturn JSON primitieve waarden (knooppuntniveau van JSON-structuur Hallo Hallo). 

**Query**

    SELECT VALUE f.address.state
    FROM Families f    

**Resultaten**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* Operator
Hallo speciale operator (*) is ondersteunde tooproject Hallo-document als-is. Wanneer gebruikt, moet dit Hallo geprojecteerd alleen veld. Terwijl een query zoals `SELECT * FROM Families f` geldig is, `SELECT VALUE * FROM Families f ` en `SELECT *, f.id FROM Families f ` zijn niet geldig.

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultaten**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Operator TOP
Hallo bovenste sleutelwoord kan worden gebruikt toolimit Hallo aantal waarden dat door een query. Als eerste wordt gebruikt in combinatie met Hallo ORDER BY-component, is Hallo resultatenset beperkt toohello eerste N aantal geordende waarden; Anders retourneert het Hallo eerste N aantal resultaten in een niet-gedefinieerde volgorde. Als een best practice in een instructie SELECT gebruik altijd een component ORDER BY met Hallo TOP-component. Dit is de enige manier Hallo toopredictably aangeven welke rijen zijn beïnvloed door boven. 

**Query**

    SELECT TOP 1 * 
    FROM Families f 

**Resultaten**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

TOP kan worden gebruikt met een constante waarde (zoals hierboven) of met de waarde van een variabele query's met parameters. Zie geparameteriseerde query's hieronder voor meer informatie.

### <a id="Aggregates"></a>Statistische functies
U kunt ook aggregaties uitvoeren in Hallo `SELECT` component. Statistische functies uitvoeren van een berekening op een set waarden en één waarde retourneren. Bijvoorbeeld: hello volgende query retourneert Hallo telling van familie documenten binnen Hallo-verzameling.

**Query**

    SELECT COUNT(1) 
    FROM Families f 

**Resultaten**

    [{
        "$1": 2
    }]

U kunt de scalaire waarde Hallo Hallo cumulatieve ook met behulp van Hallo retourneren `VALUE` sleutelwoord. Bijvoorbeeld retourneert hello volgende query het aantal waarden Hallo als een enkel getal:

**Query**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Resultaten**

    [ 2 ]

U kunt ook statistische functies uitvoeren in combinatie met filters. Bijvoorbeeld retourneert hello volgende query het aantal documenten met Hallo adres Hallo in Hallo staat Washington.

**Query**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Resultaten**

    [ 1 ]

Hallo volgende tabel toont Hallo lijst met ondersteunde statistische functies in DocumentDB-API. `SUM`en `AVG` via numerieke waarden worden uitgevoerd terwijl `COUNT`, `MIN`, en `MAX` via getallen, tekenreeksen, Booleaanse waarden en null-waarden kunnen worden uitgevoerd. 

| Gebruik | Beschrijving |
|-------|-------------|
| AANTAL | Retourneert Hallo het aantal items in de expressie Hallo. |
| SOM   | Retourneert Hallo som van alle Hallo-waarden in Hallo-expressie. |
| MIN   | Retourneert Hallo minimumwaarde in het Hallo-expressie. |
| MAXIMUM AANTAL   | Retourneert Hallo maximumwaarde in het Hallo-expressie. |
| GEM.   | Retourneert Hallo gemiddelde van waarden in de expressie Hallo Hallo. |

Statistische functies kunnen ook worden uitgevoerd via Hallo resultaten van een matrix herhaling. Zie voor meer informatie [herhaling van de matrix in query's](#Iteration).

> [!NOTE]
> Wanneer met behulp van Azure portal Queryverkenner hello, houd er rekening mee dat aggregatie van query's kunnen worden geretourneerd Hallo gedeeltelijk cumulatieve resultaten gedurende een querypagina. Hallo SDK's produceert één cumulatieve waarde op alle pagina's. 
> 
> In volgorde tooperform aggregatie van query's met code, moet u .NET SDK 1.12.0, .NET Core SDK 1.1.0 of Java SDK 1.9.5 of hoger.    
>

## <a id="OrderByClause"></a>ORDER BY-component
Zoals in de ANSI-SQL, u een optionele component Order By tijdens het opvragen opnemen kunt. Hallo-component kan bestaan uit een optionele ASC/DESC argument toospecify Hallo volgorde waarin de resultaten moeten worden opgehaald.

Hier is bijvoorbeeld een query waarmee families in volgorde van de naam van Hallo residente stad opgehaald.

**Query**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Resultaten**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

En hier is een query waarmee families in volgorde van de aanmaakdatum, dat is opgeslagen, zoals een Hallo epoche tijd, Internet Explorer, verstreken tijd sinds 1 januari 1970 in seconden worden opgehaald.

**Query**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Resultaten**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Concepten van geavanceerde database en SQL-query 's

### <a id="Iteration"></a>Herhaling
Een nieuwe constructie is toegevoegd via Hallo **IN** -sleutelwoord in DocumentDB API SQL tooprovide ondersteuning voor iteratie van JSON-matrices. Hallo FROM bron biedt ondersteuning voor herhaling. U begint met het volgende voorbeeld Hallo:

**Query**

    SELECT * 
    FROM Families.children

**Resultaten**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Nu we bekijken een andere query die herhaling via onderliggende elementen in de verzameling Hallo uitvoert. Houd er rekening mee Hallo verschil in Hallo uitvoermatrix. In dit voorbeeld wordt gesplitst `children` en worden samengevoegd Hallo resultaten in een matrix.  

**Query**

    SELECT * 
    FROM c IN Families.children

**Resultaten**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Dit kan verder gebruikte toofilter op elke afzonderlijke vermelding van de matrix Hallo zoals weergegeven in het volgende voorbeeld Hallo zijn:

**Query**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Resultaten**  

    [{
      "givenName": "Lisa"
    }]

U kunt ook aggregatie uitvoeren via Hallo resultaat van de matrix herhaling. Bijvoorbeeld: hello volgende query telt Hallo aantal onderliggende items onder alle families.

**Query**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Resultaten**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Joins
In een relationele database Hallo nodig toojoin tussen tabellen, het is belangrijk. De Hallo logische corollary toodesigning genormaliseerd schema's. Strijdig toothis, DocumentDB API omgaat met de Hallo gedenormaliseerd gegevensmodel zonder schema documenten. Dit is Hallo logische equivalent van een 'self-join'.

Hallo-syntaxis die ondersteuning biedt voor Hallo taal is < from_source1 > JOIN < from_source2 > JOIN... JOIN < from_sourceN >. Over het algemeen dit retourneert een reeks **N**- tuples (tuple met **N** waarden). Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden. Dit is met andere woorden, een volledige vectorproduct van Hallo sets die deel uitmaken van Hallo join.

Hallo volgende voorbeelden ziet u de werking van Hallo JOIN-component. Hallo-resultaat is in Hallo voorbeeld te volgen, leeg omdat hello vectorproduct van elk document van de bron- en een lege set leeg is.

**Query**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Resultaten**  

    [{
    }]


In Hallo voorbeeld te volgen, is het Hallo-join tussen Hallo webroot en Hallo `children` subroot. Het is een vectorproduct tussen twee JSON-objecten. Hallo fact dat onderliggende elementen is een matrix is niet effectief in Hallo JOIN Aangezien we werkt met een één hoofdelement die Hallo onderliggende matrix. Hallo resultaat bevat daarom slechts twee resultaten omdat hello vectorproduct van elk document met Hallo matrix exact slechts één document levert.

**Query**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Resultaten**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Hallo volgende voorbeeld ziet u een meer conventionele join:

**Query**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Resultaten**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Hallo eerst te beginnen toonote is die Hallo `from_source` Hallo **JOIN** component is een iterator. Dus Hallo stroom is in dit geval als volgt:  

* Vouw van elk onderliggend element **c** in Hallo matrix.
* Toepassen van een vectorproduct met Hallo hoofdmap van document Hallo **f** met elk onderliggend element **c** dat is samengevoegd in de eerste stap Hallo.
* Ten slotte project Hallo hoofdobject **f** naameigenschap alleen. 

eerste Hallo-document (`AndersenFamily`) bevat slechts één onderliggend element zodat Hallo resultatenset alleen een bijbehorende enkel object toothis document bevat. tweede Hallo-document (`WakefieldFamily`) twee onderliggende items bevat. Dus produceert hello vectorproduct een afzonderlijk object voor elke onderliggende, waardoor wat resulteert in twee objecten, één voor elke onderliggende bijbehorende toothis document. Hallo-hoofdmap velden in beide deze documenten zijn Hallo dezelfde zijn, net zoals u in een vectorproduct verwacht.

Hallo echt hulpprogramma Hallo JOIN tooform tuples uit Hallo-vectorproduct in een shape die anders is moeilijk tooproject. Bovendien zoals we in de onderstaande Hallo-voorbeeld zien, kon u filteren op Hallo combinatie van een tuple waarmee Hallo gebruiker heeft ervoor gekozen een voorwaarde voldaan door Hallo tuples algemene.

**Query**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Resultaten**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



In dit voorbeeld is een natuurlijke extensie van het voorgaande voorbeeld Hallo en voert een dubbele koppeling. Dus kan hello vectorproduct worden weergegeven als Hallo pseudo code te volgen:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily`heeft één onderliggende die één huisdier heeft. Dus hello vectorproduct resulteert in een rij is (1\*1\*1) van deze reeks. WakefieldFamily echter twee onderliggende items heeft, maar slechts één onderliggende 'Jesse' huisdieren heeft. Jesse heeft echter twee huisdieren. Daarom hello vectorproduct levert 1\*1\*2 = 2 rijen uit deze reeks.

In het volgende voorbeeld hello, er is een extra filter op `pet`. Dit omvat niet alle Hallo tuples indien Hallo bijnaam niet 'Schaduwkopie' is. U ziet dat we kunnen toobuild tuples uit matrices, filter op Hallo-elementen van het Hallo-tuple zijn en een combinatie van elementen Hallo project. 

**Query**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Resultaten**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Integratie van JavaScript
Azure Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op Hallo van verzamelingen in termen van opgeslagen procedures en triggers. Hiermee kunt u beide:

* Mogelijkheid toodo high-performance transactionele CRUD-bewerkingen en een query uitgevoerd naar documenten in een verzameling grond Hallo diepe integratie van JavaScript-runtime rechtstreeks in de database-engine Hallo. 
* Een natuurlijke modellering van Controlestroom, variabele scopes en -toewijzing en integratie van primitieven met databasetransacties afhandeling van uitzonderingen. Raadpleeg toohello JavaScript-serverzijde programmeerbaarheid documentatie voor meer informatie over Azure DB die Cosmos-ondersteuning voor integratie van JavaScript.

### <a id="UserDefinedFunctions"></a>Gebruiker gedefinieerde functies (UDF's)
Samen met de Hallo-typen is al gedefinieerd in dit artikel, biedt DocumentDB API SQL ondersteuning voor gebruiker gedefinieerde functies (UDF). In het bijzonder wordt scalaire UDF's waar Hallo ontwikkelaars kunnen doorgeven in nul of meerdere argumenten en terug één argument resultaat geretourneerd ondersteund. Elk van deze argumenten wordt voor geldige JSON-waarden worden gecontroleerd.  

Hallo DocumentDB API SQL-syntaxis wordt uitgebreid aangepaste toepassingslogica toosupport gebruik van deze door de gebruiker gedefinieerde functies. UDF's kunnen worden geregistreerd met DocumentDB-API en vervolgens naar worden verwezen als onderdeel van een SQL-query. Hallo UDF's exquisitely zijn ontworpen in feite toobe aangeroepen door query's. Als een keuze corollary toothis UDF's hebben geen toegang toohello context-object dat andere JavaScript Hallo typen (opgeslagen procedures en triggers) hebben. Omdat de query's worden uitgevoerd als alleen-lezen, kunnen ze worden uitgevoerd op de primaire of op secundaire replica's. Daarom zijn UDF's ontworpen toorun op secundaire replica's in tegenstelling tot andere typen JavaScript.

Hieronder volgt een voorbeeld van hoe een UDF op Hallo Cosmos DB database onder een documentverzameling specifiek kan worden geregistreerd.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Hallo voorgaande voorbeeld maakt u een UDF met de naam `REGEX_MATCH`. Deze twee waarden voor JSON-tekenreeks accepteert `input` en `pattern` en controleert of Hallo eerste komt overeen met patroon Hallo opgegeven in het tweede Hallo van JavaScript string.match() functie te gebruiken.

We kunnen deze UDF nu gebruiken in een query in een projectie. UDF's moeten worden gekwalificeerd met Hallo hoofdlettergevoelig voorvoegsel "udf." Wanneer aangeroepen vanuit query's. 

> [!NOTE]
> Eerdere too3-17-2015, Cosmos DB ondersteund UDF aanroepen zonder Hallo 'udf." voorvoegsel zoals REGEX_MATCH() selecteren. Dit patroon van aanroepen is afgeschaft.  
> 
> 

**Query**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Resultaten**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Hallo UDF kan ook worden gebruikt in een filter, zoals weergegeven in Hallo voorbeeld hieronder, ook worden gekwalificeerd met Hallo 'udf." voorvoegsel:

**Query**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Resultaten**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


In principe UDF's geldig scalaire expressies zijn en kunnen worden gebruikt in projecties en filters. 

tooexpand op Hallo kracht van UDF's, we kijken naar een ander voorbeeld met voorwaardelijke logica:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Hieronder volgt een voorbeeld dat oefeningen Hallo UDF.

**Query**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Resultaten**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Als de voorgaande voorbeelden toepassingen hello, integreren UDF's in Hallo power van JavaScript-taal Hallo DocumentDB API SQL tooprovide een uitgebreide programmeerbare interface toodo complexe procedurele, heeft voorwaardelijke logica met Hallo hulp van de ingebouwde JavaScript-runtime mogelijkheden.

DocumentDB API SQL biedt Hallo argumenten toohello UDF's voor elk document in Hallo-bron in Hallo huidige fase (WHERE-component of SELECT-component) verwerking Hallo UDF. Hallo resultaat opgenomen in algemene pijplijn naadloos Hallo. Als Hallo eigenschappen waarnaar wordt verwezen tooby Hallo UDF-parameters niet beschikbaar in JSON-waarde Hallo hello parameter wordt beschouwd zijn als niet-gedefinieerde en daarom Hallo UDF-aanroep volledig overgeslagen. Op dezelfde manier als resultaat Hallo Hallo UDF gedefinieerd is, het niet opgenomen in Hallo resultaat. 

Kortom zijn UDF's geweldige tools toodo complexe bedrijfslogica als onderdeel van Hallo-query.

### <a name="operator-evaluation"></a>Evaluatie van operator
Cosmos DB, tekent uit hoofde van een JSON-database wordt Hallo werkt hetzelfde als met JavaScript-operators en de semantiek voor evaluatie. Terwijl Cosmos DB toopreserve JavaScript-semantiek in termen van JSON-ondersteuning probeert, afwijkt Hallo bewerking evaluatie in sommige gevallen.

In DocumentDB API SQL, zijn in tegenstelling tot in traditionele SQL Hallo typen waarden vaak niet bekend totdat Hallo waarden uit de database zijn opgehaald. Query's uitvoeren in de volgorde tooefficiently, de meeste van Hallo operators strikt type vereisten hebben. 

DocumentDB-API SQL biedt geen impliciete conversies, in tegenstelling tot JavaScript uitvoeren. Een query voor het exemplaar, zoals `SELECT * FROM Person p WHERE p.Age = 21` overeenkomt met de documenten met een eigenschap Age waarvan de waarde 21 is. Een ander document waarvan de eigenschap leeftijd overeenkomt met de tekenreeks '21' of andere mogelijk oneindige variaties, zoals '021', '21,0', '0021', '00021', enzovoort worden niet overeen. Dit is daarentegen toohello JavaScript waar Hallo tekenreekswaarden impliciet omgezet toonumbers worden (op basis van de operator ex: ==). Deze keuze is van cruciaal belang voor efficiënte index zoeken in DocumentDB API SQL. 

## <a name="parameterized-sql-queries"></a>SQL-query's met parameters
Cosmos DB ondersteunt query's met parameters worden uitgedrukt Hello bekend zijn @ notatie. Geparameteriseerde SQL biedt robuuste verwerken en de aanhalingstekens van gebruikersinvoer, onbedoeld blootstelling van gegevens via SQL-injectie voorkomen. 

U kunt bijvoorbeeld een query schrijven waarmee achternaam en status van adres als parameters neemt en vervolgens uitgevoerd voor verschillende waarden van de laatste naam en adres staat op basis van de invoer van gebruiker.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Deze aanvraag kan vervolgens worden verzonden tooCosmos DB een JSON-query met parameters zoals hieronder wordt weergegeven.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Hallo argument tooTOP kan worden ingesteld met query's met parameters, zoals hieronder wordt weergegeven.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Parameterwaarden mag geldige JSON (tekenreeksen, cijfers, Booleaanse waarden, null, zelfs als deze matrices of geneste JSON). Ook omdat Cosmos DB schema minder, zijn parameters niet gevalideerd met elk type.

## <a id="BuiltinFunctions"></a>Ingebouwde functies
Cosmos DB ondersteunt ook een aantal ingebouwde functies voor algemene bewerkingen, die kunnen worden gebruikt in query's als de gebruiker gedefinieerde functies (UDF's).

| Functie-groep          | Bewerkingen                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Wiskundige functies  | ABS, maximum, EXP, FLOOR, logboek, LOG10, POWER, ROUND, aanmelding, SQRT, VIERKANT, geheel, BOOGCOS, ASIN, BOOGTAN, ATN2, Cosinus, COT, graden PI, radialen, SIN en TAN |
| Controle van de functies van het type | IS_ARRAY, IS_BOOL IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED en IS_PRIMITIVE                                                           |
| Tekenreeks-functies        | CONCAT, bevat ENDSWITH, INDEX_OF, links, lengte, kleine, LTRIM, vervangen, REPLICEREN, REVERSE, rechts, RTRIM, STARTSWITH, SUBTEKENREEKS en hoofdletters       |
| Matrixfuncties         | ARRAY_CONCAT, ARRAY_CONTAINS ARRAY_LENGTH en ARRAY_SLICE                                                                                         |
| Ruimtelijke functies       | ST_DISTANCE, ST_WITHIN ST_INTERSECTS, ST_ISVALID en ST_ISVALIDDETAILED                                                                           | 

Als u momenteel een gebruiker gedefinieerde functie (UDF) waarvoor een ingebouwde functie nu beschikbaar is, moet u de bijbehorende ingebouwde functie Hallo zoals sneller toorun toobe en meer gaat efficiënt. 

### <a name="mathematical-functions"></a>Wiskundige functies
Hallo wiskundige functies elke uitvoeren van een berekening op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren. Hier volgt een lijst met ondersteunde ingebouwde, rekenkundige functies.


| Gebruik | Beschrijving |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie. |
| [MAXIMUM (num_expr)](#bk_ceiling) | Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie. |
| [FLOOR (num_expr)](#bk_floor) | Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven. |
| [EXP (num_expr)](#bk_exp) | Retourneert Hallo exponent Hallo opgegeven numerieke expressie. |
| [LOGBOEK (num_expr [, base])](#bk_log) | Retourneert Hallo natuurlijke logaritme van Hallo numerieke expressie, of Hallo logaritme Hallo met base opgegeven |
| [LOG10 (num_expr)](#bk_log10) | Retourneert Hallo grondtal 10 logaritmische waarde Hallo opgegeven numerieke expressie. |
| [ROUND (num_expr)](#bk_round) | Retourneert een numerieke waarde afgeronde toohello dichtstbijzijnde integer-waarde. |
| [GEHEEL (num_expr)](#bk_trunc) | Retourneert een numerieke waarde ingekorte toohello dichtstbijzijnde integer-waarde. |
| [SQRT (num_expr)](#bk_sqrt) | Retourneert de vierkantswortel van Hallo Hallo opgegeven numerieke expressie. |
| [Vierkante (num_expr)](#bk_square) | Retourneert Hallo vierkante Hallo opgegeven numerieke expressie. |
| [VOEDING (num_expr, num_expr)](#bk_power) | Retourneert Hallo power Hallo opgegeven numerieke expressie toohello waarde opgeven. |
| [ONDERTEKENEN (num_expr)](#bk_sign) | Retourneert Hallo aanmelding waarde (-1, 0, 1) Hallo opgegeven numerieke expressie. |
| [BOOGCOS (num_expr)](#bk_acos) | Retourneert Hallo hoek in radialen, waarvan de cosinus is Hallo opgegeven numerieke expressie. ook wel de boogcosinus genoemd. |
| [ASIN (num_expr)](#bk_asin) | Retourneert Hallo hoek in radialen, waarvan de sinus Hallo is opgegeven numerieke expressie. Dit wordt ook boogsinus genoemd. |
| [BOOGTAN (num_expr)](#bk_atan) | Retourneert Hallo hoek in radialen, waarvan de tangens Hallo is opgegeven numerieke expressie. Dit wordt ook arctangens genoemd. |
| [ATN2 (num_expr)](#bk_atn2) | Retourneert Hallo hoek in radialen tussen Hallo positief x-as en Hallo ray van Hallo oorsprong toohello punt (y, x), waarbij x en y zijn Hallo waarden Hallo twee opgegeven float-expressies. |
| [CO (num_expr)](#bk_cos) | Retourneert Hallo trigonometrische cosinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie. |
| [COT (num_expr)](#bk_cot) | Retourneert Hallo trigonometrische cotangens van Hallo hoek aangeduid in radialen, opgegeven in Hallo numerieke expressie. |
| [GRADEN (num_expr)](#bk_degrees) | Retourneert Hallo bijbehorende hoek in graden voor een hoek aangeduid in radialen. |
| [PI)](#bk_pi) | Retourneert Hallo constante waarde van PI. |
| [RADIALEN (num_expr)](#bk_radians) | Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd. |
| [SIN (num_expr)](#bk_sin) | Retourneert Hallo trigonometrische sinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie. |
| [TAN (num_expr)](#bk_tan) | Retourneert Hallo tangens van invoerexpressie Hallo in Hallo opgegeven expressie. |

U kunt nu bijvoorbeeld query's zoals Hallo volgende uitvoeren:

**Query**

    SELECT VALUE ABS(-4)

**Resultaten**

    [4]

Hallo belangrijkste verschil tussen Cosmos-database functies vergeleken tooANSI SQL is dat ze ontworpen toowork goed met schemagegevens zonder schema en een gemengde zijn. Als u hebt een document waarbij de eigenschap Size Hallo ontbreekt of heeft een niet-numerieke waarde als 'Onbekend' vervolgens Hallo document is overgeslagen, klikt u in plaats van een fout geretourneerd.

### <a name="type-checking-functions"></a>Controle van de functies van het type
Hallo type controleren of functies kunnen u toocheck Hallo-type van een expressie in SQL-query's. Type controle functies kunnen worden gebruikt toodetermine Hallo type eigenschappen in een documenten op Hallo snel wanneer het variabele of onbekende. Hier volgt een lijst met ondersteunde ingebouwde typecontrole functies.

<table>
<tr>
  <td><strong>Gebruik</strong></td>
  <td><strong>Beschrijving</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een matrix is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een Booleaanse waarde is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo waarde null is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo waarde een getal is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een JSON-object is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een tekenreeks is.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een tekenreeks, getal, Booleaanse waarde of null zijn is.</td>
</tr>

</table>

U kunt nu een query's de volgende Hallo uitvoeren met behulp van deze functies:

**Query**

    SELECT VALUE IS_NUMBER(-4)

**Resultaten**

    [true]

### <a name="string-functions"></a>Tekenreeks-functies
Hallo volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren. Hier volgt een lijst met ingebouwde tekenreeks-functies:

| Gebruik | Beschrijving |
| --- | --- |
| [LENGTE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden. |
| [De SUBTEKENREEKS (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Retourneert deel van een tekenreeksexpressie. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt |
| [BEVAT (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Retourneert het linkergedeelte van een tekenreeks Hallo Hello opgegeven aantal tekens. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Hallo rechts deel uit van een tekenreeks retourneert Hello opgegeven aantal tekens. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Retourneert een tekenreeksexpressie na het afkappen van alle volgspaties. |
| [KLEINE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren. |
| [Vervang (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks. |
| [REPLICEREN (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Herhaalt een string-waarde van een opgegeven aantal keren. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Retourneert de omgekeerde volgorde Hallo van een string-waarde. |

U kunt nu een query's de volgende Hallo uitvoeren met behulp van deze functies. Bijvoorbeeld, kunt u terugkeren Hallo familienaam in hoofdletters als volgt:

**Query**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Resultaten**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Of samenvoegen van strings zoals in dit voorbeeld:

**Query**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Resultaten**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Tekenreeksfuncties kunnen ook worden gebruikt in Hallo waar component toofilter resultaten, zoals in het volgende voorbeeld Hallo:

**Query**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Resultaten**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Matrixfuncties
Hallo scalaire functies na een bewerking uitvoeren op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde. Hier volgt een lijst met ingebouwde matrixfuncties:

| Gebruik | Beschrijving |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Retourneert Hallo aantal elementen Hallo matrixexpressie opgegeven. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Retourneert een matrix die Hallo resultaat is van het samenvoegen van twee of meer matrixwaarden. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Retourneert een Booleaanse waarde die aangeeft of de matrix Hallo Hallo bevat een waarde opgegeven. Kunt opgeven als Hallo treffer volledig of gedeeltelijk is. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Retourneert deel van een matrixexpressie. |

Matrixfuncties kunnen worden gebruikt toomanipulate matrices in JSON. Hier is bijvoorbeeld een query die alle documenten retourneert waarbij een van de ouders Hallo 'Robin Wakefield' is. 

**Query**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Resultaten**

    [{
      "id": "WakefieldFamily"
    }]

U kunt een gedeeltelijke fragment voor overeenkomende elementen binnen de matrix Hallo opgeven. Hallo volgende query vindt u alle bovenliggende items Hello `givenName` van `Robin`.

**Query**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Resultaten**

    [{
      "id": "WakefieldFamily"
    }]


Hier volgt een voorbeeld met ARRAY_LENGTH tooget Hallo aantal onderliggende items per serie.

**Query**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Resultaten**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Ruimtelijke functies
Hallo volgende ingebouwde functies voor query's in georuimtelijke Open georuimtelijke Consortium (OGC) biedt ondersteuning voor cosmos DB. 

<table>
<tr>
  <td><strong>Gebruik</strong></td>
  <td><strong>Beschrijving</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Retourneert een Booleaanse expressie die aangeeft of Hallo eerste GeoJSON-object (punt, Polygon of LineString) binnen Hallo tweede GeoJSON-object (punt, Polygon of LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retourneert een Booleaanse expressie die aangeeft of Hallo twee opgegeven GeoJSON-objecten (punt, Polygon of LineString) intersect.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</td>
</tr>
</table>

Ruimtelijke functies kunnen worden gebruikt tooperform nabijheid query's op ruimtelijke gegevens. Hier is bijvoorbeeld een query waarmee alle familie documenten dat binnen 30 km Hallo opgegeven locatie Hallo ST_DISTANCE ingebouwde functie gebruikt geretourneerd. 

**Query**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultaten**

    [{
      "id": "WakefieldFamily"
    }]

Zie voor meer informatie over ondersteuning voor Cosmos DB georuimtelijke [werken met gegevens in Azure Cosmos DB georuimtelijke](geospatial.md). Die loopt van ruimtelijke functies en Hallo SQL-syntaxis voor Cosmos-DB. Nu eens kijken hoe LINQ-query werkt en hoe deze samenwerkt met de syntaxis van de Hallo we hebt gezien tot nu toe.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ is een .NET-programmeermodel waarin berekeningen query's voor stromen van objecten. Cosmos DB biedt een toointerface clientzijde bibliotheek met LINQ doordat een conversie tussen JSON en .NET-objecten en een toewijzing voor een subset van LINQ query's tooCosmos DB-query's. 

Hallo in de volgende afbeelding toont de architectuur Hallo LINQ-query's met behulp van de Cosmos-DB ondersteunen.  Met behulp van Hallo Cosmos DB client kunnen ontwikkelaars maken een **IQueryable** object dat rechtstreeks query's hello Cosmos-DB-provider opvragen, die vervolgens Hallo LINQ-query in een Cosmos-DB-query zet. Hallo query toohello Cosmos DB server tooretrieve een set resultaten vervolgens doorgegeven in JSON-indeling. Hallo geretourneerd resultaten in een stream met .NET-objecten aan de clientzijde Hallo gedeserialiseerd worden.

![Architectuur van de LINQ-query's met DocumentDB-API - SQL-syntaxis, JSON-querytaal concepten van de database en SQL-query's ondersteunen][1]

### <a name="net-and-json-mapping"></a>.NET- en JSON-toewijzing
Hallo-toewijzing tussen .NET-objecten en JSON-documenten is natuurlijk - elk veld gegevens lid is toegewezen tooa JSON-object, waarbij Hallo veldnaam is toohello 'sleutel' onderdeel zijn van Hallo-object toegewezen en Hallo '' waarde '' onderdeel recursief toegewezen toohello waardedeel uitmaakt van Hallo-object. Overweeg het volgende voorbeeld Hallo: Hallo familie-object gemaakt is toegewezen toohello JSON-document, zoals hieronder wordt weergegeven. En vice versa Hallo JSON-document is toegewezen back tooa .NET-object.

**C#-klasse**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>De vertaling van LINQ tooSQL
Hallo Cosmos-DB-provider opvragen voert een best effort toewijzing van een LINQ-query naar een Cosmos DB SQL-query. Hallo beschrijving te volgen, veronderstellen we Hallo lezer heeft een elementaire kennis van LINQ.

Eerst ondersteunen Hallo-typesysteem, wij alle JSON primitieve typen – numerieke typen, Booleaanse waarde, tekenreeks en null. Alleen deze JSON-typen worden ondersteund. Hallo volgende scalaire expressies worden ondersteund.

* Constante waarden – hierbij constante waarden van de primitieve gegevenstypen Hallo gelijktijdig Hallo Hallo query wordt geëvalueerd.
* Eigenschappenmatrix/indexexpressies – deze expressies Raadpleeg toohello-eigenschap van een object of een element van de matrix.
  
     familie. ID;    Family.children[0].familyName;    Family.children[0].Grade;    Family.children[n].Grade; n is een int-variabele
* Aritmetische expressies - deze algemene aritmetische expressies op numerieke en Booleaanse waarden bevatten. Raadpleeg voor de volledige lijst hello, toohello SQL-specificatie.
  
     2 * family.children[0].grade;    x + y;
* Vergelijking van tekenreeksexpressie - hierbij een string-waarde toosome constante string-waarde te vergelijken.  
  
     mother.familyName == 'Smith';    child.givenName == s; s is een string-variabele
* Object/matrix maken van expressie - deze expressies return een object van het waardetype van de samengestelde of anoniem type of een matrix van dergelijke objecten. Deze waarden kunnen worden genest.
  
     nieuwe bovenliggende {familyName = 'Smit', givenName = "Jan"}; nieuwe {eerst = 1, tweede = 2}; een anoniem type met twee velden              
     nieuwe int [] {3, child.grade, 5};

### <a id="SupportedLinqOperators"></a>Lijst met ondersteunde LINQ-operators
Hier volgt een lijst met ondersteunde LINQ-operators in Hallo LINQ-provider is opgenomen in Hallo DocumentDB .NET SDK.

* **Selecteer**: projecties toohello Selecteer objectconstructie inclusief SQL vertalen
* **Waar**: Filters toohello waar SQL vertalen en ondersteuning voor de conversie van & &, || en! toohello SQL-operators
* **SelectMany**: kunt ongedaan maken van matrices toohello SQL JOIN-component. Gebruikte toochain/nest expressies toofilter op matrixelementen kan zijn
* **OrderBy en OrderByDescending**: zet tooORDER BY oplopend/aflopend
* **Aantal**, **som**, **Min**, **Max**, en **gemiddelde** operators voor aggregatie en de async-equivalenten **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, en **AverageAsync**.
* **CompareTo**: zet toorange vergelijkingen. Meestal gebruikt voor tekenreeksen omdat ze nog niet vergeleken in .NET
* **Nemen**: zet toohello SQL TOP voor het beperken van de resultaten van een query
* **Rekenkundige functies**: de vertaling van ondersteunt. De NET Abs, BOOGCOS, Asin, BOOGTAN, maximum, CO, Exp, Floor, logboek, Log10, Pow, Round, aanmelding, Sin, Sqrt, Tan, toohello gelijkwaardige SQL ingebouwde functies worden afgekapt.
* **Functies String**: de vertaling van ondersteunt. NET van Concat, bevat EndsWith, IndexOf, Count, ToLower, TrimStart, vervangen, Reverse, TrimEnd, StartsWith, subtekenreeks ToUpper toohello gelijkwaardige SQL ingebouwde functies.
* **Matrix van functies**: de vertaling van ondersteunt. NET van Concat bevat en aantal toohello gelijkwaardige SQL ingebouwde functies.
* **Extensiefuncties georuimtelijke**: ondersteunt de vertaling van stub-methoden afstand binnen IsValid, en IsValidDetailed toohello gelijkwaardige SQL ingebouwde functies.
* **Gebruiker gedefinieerde functie extensiefunctie**: ondersteunt de vertaling van Hallo stub-methode UserDefinedFunctionProvider.Invoke toohello overeenkomende gebruiker gedefinieerde functie.
* **Diverse**: ondersteunt de vertaling van Hallo coalesce en voorwaardelijke operators. Kan vertalen bevat tooString bevat, ARRAY_CONTAINS of Hallo SQL IN, afhankelijk van de context.

### <a name="sql-query-operators"></a>SQL-query-operators
Hier volgen enkele voorbeelden die aangeven hoe sommige Hallo standaard de LINQ-query-operators omlaag tooCosmos DB-query's worden omgezet.

#### <a name="select-operator"></a>Operator selecteren
Hallo-syntaxis is `input.Select(x => f(x))`, waarbij `f` is een scalaire expressie.

**LINQ lambda-expressie**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**LINQ lambda-expressie**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**LINQ lambda-expressie**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>SelectMany operator
Hallo-syntaxis is `input.SelectMany(x => f(x))`, waarbij `f` is een scalaire expressie die als resultaat een verzamelingstype geeft.

**LINQ lambda-expressie**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Waar operator
Hallo-syntaxis is `input.Where(x => f(x))`, waarbij `f` is een scalaire expressie die een Booleaanse waarde retourneert.

**LINQ lambda-expressie**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**LINQ lambda-expressie**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Samengestelde SQL-query 's
Hallo hierboven operators samengesteld tooform krachtige query's kan worden. Aangezien Cosmos DB geneste verzamelingen ondersteunt, kan Hallo samenstelling worden samengevoegd of genest.

#### <a name="concatenation"></a>Samenvoeging
Hallo-syntaxis is `input(.|.SelectMany())(.Select()|.Where())*`. Een samengevoegde query kunt beginnen met een optionele `SelectMany` query gevolgd door meerdere `Select` of `Where` operators.

**LINQ lambda-expressie**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**LINQ lambda-expressie**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**LINQ lambda-expressie**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**LINQ lambda-expressie**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Nesten
Hallo-syntaxis is `input.SelectMany(x=>x.Q())` waarbij Q is een `Select`, `SelectMany`, of `Where` operator.

Hallo binnenste query is in een geneste query, toegepaste tooeach-element van de buitenste verzameling Hallo. Een belangrijke functie is dat die Hallo binnenste query kunt verwijzen toohello velden van het Hallo-elementen in de buitenste verzameling Hallo zoals zelf-joins.

**LINQ lambda-expressie**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**LINQ lambda-expressie**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**LINQ lambda-expressie**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>SQL-query's uitvoeren
Cosmos DB Ontsluit resources via een REST-API die kan worden aangeroepen via elke taal waarmee HTTP/HTTPS-aanvragen. Daarnaast biedt Cosmos DB programmeringsbibliotheken voor verschillende veelgebruikte talen zoals .NET, Node.js, JavaScript en Python. Hallo REST-API en Hallo ondersteuning voor verschillende bibliotheken alle opvragen via SQL. Hallo .NET SDK biedt ondersteuning voor LINQ bovendien tooSQL opvragen.

Hallo volgen voorbeelden kunt u zien hoe een query toocreate en te verzenden op basis van een Cosmos-DB-databaseaccount.

### <a id="RestAPI"></a>REST-API
Cosmos DB biedt een open RESTful-programmeermodel via HTTP. Database-accounts kunnen worden ingericht met behulp van een Azure-abonnement. Hallo Cosmos DB resourcemodel bestaat uit een set resources onder de databaseaccount van een, die elk opgevraagd met een logische en stabiele-URI is. Een set resources is waarnaar wordt verwezen tooas een feed in dit document. Een databaseaccount bestaat uit een reeks databases, die elk meerdere verzamelingen met elk van welke beurt documenten, UDF's en andere brontypen bevatten.

Hallo basic interactie model met deze resources is via Hallo HTTP-woorden GET, PUT, POST en DELETE met hun standaard interpretatie. Hallo POST term wordt gebruikt voor het maken van een nieuwe resource, voor het uitvoeren van een opgeslagen procedure of voor het uitgeven van een Cosmos-DB-query. Query's zijn altijd alleen-lezen bewerkingen met geen bijwerkingen.

Hallo volgende voorbeelden ziet u een POST voor een DocumentDB-API-query ten opzichte van een verzameling met Hallo twee voorbeelddocumenten dat we tot nu toe hebt bekeken. Hallo-query heeft een eenvoudige filter op Hallo JSON name-eigenschap. Houd er rekening mee Hallo gebruik van Hallo `x-ms-documentdb-isquery` en Content-Type: `application/query+json` toodenote headers die Hallo bewerking is een query.

**Aanvraag**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Resultaten**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Hallo tweede voorbeeld ziet u een complexere query die meerdere resultaten uit Hallo join retourneert.

**Aanvraag**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Resultaten**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Als de queryresultaten niet binnen één pagina van de resultaten passen en vervolgens Hallo REST-API een vervolgtoken via Hallo retourneert `x-ms-continuation-token` antwoordheader. Clients kunnen resultaten pagineren door Hallo-header in de volgende resultaten. het aantal resultaten per pagina Hallo kan ook worden beheerd via Hallo `x-ms-max-item-count` nummer header. Als de opgegeven query Hallo een statistische functie zoals heeft `COUNT`, en vervolgens Hallo querypagina een gedeeltelijk cumulatieve waarde kan worden geretourneerd gedurende Hallo pagina met resultaten. Hallo-clients moeten een aggregatie tweede niveau uitvoeren via deze resultaten tooproduce Hallo laatste resultaten, bijvoorbeeld, som is opgegeven via Hallo aantallen geretourneerd in Hallo afzonderlijke pagina's tooreturn Hallo totale aantal.

beleid voor toomanage Hallo gegevens consistentie voor query's, gebruik Hallo `x-ms-consistency-level` header bijvoorbeeld alle aanvragen voor REST-API. Voor sessieconsistentie, is het vereist tooalso echo hallo nieuwste `x-ms-session-token` Cookie-kop in Hallo-aanvraag. Hallo indexeringsbeleid aangevraagde verzameling kan ook van invloed zijn op Hallo consistentie van de queryresultaten. Met standaard Hallo indexeren beleidsinstellingen voor verzamelingen Hallo index is altijd met inhoud van het document Hallo en query resultaten overeenkomen met de Hallo consistentie gekozen voor de gegevens. Als Hallo indexeren beleid beperkte tooLazy is, kunnen query's verlopen resultaten geretourneerd. Zie voor meer informatie [Azure Cosmos DB Consistentieniveaus][consistency-levels].

Als indexeringsbeleid op Hallo verzameling Hallo geconfigureerd Hallo opgegeven query niet ondersteunen kan, retourneert hello Azure Cosmos DB server 400 'onjuiste aanvraag'. Dit wordt geretourneerd voor bereik query's op paden die zijn geconfigureerd voor lookups op hash (gelijkheid) en voor paden expliciet is uitgesloten van het indexeren. Hallo `x-ms-documentdb-query-enable-scan` header opgegeven tooallow Hallo query tooperform een scan kan zijn wanneer een index niet beschikbaar is.

U kunt gedetailleerde metrische gegevens over de uitvoering van de query opvragen door in te stellen `x-ms-documentdb-populatequerymetrics` header te`True`. Zie voor meer informatie [SQL query metrische gegevens voor Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>C# (.NET) SDK
Hallo .NET SDK biedt ondersteuning voor LINQ- en SQL uitvoeren van query's. Hallo volgende voorbeeld ziet u hoe tooperform Hallo eenvoudige filterquery geïntroduceerd eerder in dit document.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Dit voorbeeld vergelijkt twee eigenschappen op gelijkheid binnen elk document en maakt gebruik van anonieme projecties. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Hallo volgende voorbeeld ziet u joins, die zijn uitgedrukt via LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



Hallo .NET-client worden automatisch alle Hallo-pagina's van queryresultaten in Hallo foreach blokken zoals hierboven doorlopen. Hallo-query die is geïntroduceerd in Hallo REST-API-sectie opties zijn ook beschikbaar in .NET SDK met de Hallo Hallo `FeedOptions` en `FeedResponse` klassen in Hallo CreateDocumentQuery methode. Hallo aantal pagina's kan worden beheerd met behulp van Hallo `MaxItemCount` instelling. 

U kunt ook expliciet paginering bepalen door het maken van `IDocumentQueryable` met Hallo `IQueryable` object, klikt u vervolgens op het lezen van de` ResponseContinuationToken` waarden en deze weer toe als `RequestContinuationToken` in `FeedOptions`. `EnableScanInQuery`is set tooenable scans als Hallo query kan niet worden ondersteund door het indexeringsbeleid Hallo geconfigureerd. Voor gepartitioneerde verzamelingen kunt u `PartitionKey` toorun Hallo-query op één partitie (Hoewel Cosmos DB dit automatisch uit de querytekst Hallo ophalen kunt), en `EnableCrossPartitionQuery` toorun-query's die toobe mogelijk moet uitvoeren op meerdere partities. 

Raadpleeg te[Azure Cosmos DB .NET-voorbeelden](https://github.com/Azure/azure-documentdb-net) voor meer voorbeelden met query's. 

### <a id="JavaScriptServerSideApi"></a>JavaScript-serverzijde-API
Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op Hallo verzamelingen met opgeslagen procedures en triggers. Hallo JavaScript-logica geregistreerd op het niveau van een verzameling kan databasebewerkingen uitvoeren op Hallo-bewerkingen op Hallo documenten Hallo gegeven verzameling vervolgens uitgeven. Deze bewerkingen zijn verpakt in een ambient ACID-transactions.

Hallo volgende voorbeeld laat zien hoe toouse hello queryDocuments in Hallo JavaScript-server API toomake van query's binnen opgeslagen procedures en triggers.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Verwijzingen
1. [Inleiding tooAzure Cosmos-DB][introduction]
2. [Azure SQL voor Cosmos-DB-specificatie](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Azure Cosmos DB .NET-voorbeelden](https://github.com/Azure/azure-documentdb-net)
4. [Azure Cosmos DB Consistentieniveaus][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. JavaScript-specificatie [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Van evaluatietechnieken voor grote databases query [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994
11. Lu, Ooi, Tan queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: een niet zodat vreemde taal voor gegevensverwerking, SIGMOD 2008.
13. G. Graefe. Hallo trapsgewijs framework voor queryoptimalisatie. IEEE-gegevens eng Bull., 18, lid 3: 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md