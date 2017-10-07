---
title: aaaModeling documentgegevens voor een NoSQL-database | Microsoft Docs
description: Meer informatie over het modelleren van gegevens voor NoSQL-databases
keywords: modellering van gegevens
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>Modeling documentgegevens voor NoSQL-databases
Terwijl databases zonder schema, zoals Azure Cosmos DB, kunnen u heel eenvoudig tooembrace wijzigingen tooyour gegevensmodel u moet nog steeds te besteden aan de enige tijd nadenken over uw gegevens. 

Hoe gaat gegevens toobe opgeslagen? Hoe wordt uw toepassing gaat tooretrieve en query gegevens? Is uw toepassing dikke lezen of schrijven zwaar? 

Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:

* Hoe moet ik denken dat zij een document in een documentdatabase?
* Wat is er gegevens modelleren en waarom moet ik het belangrijkst? 
* Hoe wordt modellering gegevens in een document verschillende tooa relationele database?
* Hoe ik gegevensrelaties in een niet-relationele database express?
* Wanneer insluiten gegevens en wanneer koppelen toodata?

## <a name="embedding-data"></a>Gegevens insluiten
Wanneer u gegevens in een store, document, zoals Azure Cosmos DB modelleren start probeer tootreat uw entiteiten als **zelfstandig documenten** vertegenwoordigd in JSON.

Voordat we meteen te veel meer laat het ons Neem een paar stappen terug en bekijk hoe wij iets in een relationele database, een onderwerp dat velen van ons al bekend met bent mogelijk model. Hallo volgende voorbeeld ziet u hoe een persoon kan worden opgeslagen in een relationele database. 

![Relationele database-model](./media/documentdb-modeling-data/relational-data-model.png)

Als u werkt met relationele databases we hebt geleerd voor jaar toonormalize, normaliseren, normaliseren.

Doorgaans normaliseren van uw gegevens omvat het maken van een entiteit, zoals een persoon, en splitsen in stukken toodiscrete van gegevens. In bovenstaande Hallo voorbeeld, kan een persoon meerdere details van contactpersonen records, alsmede meerdere adresrecords hebben. We zelfs nog een stapje verder te gaan en contactgegevens onderverdelen per verdere uitpakken algemene velden, zoals een type. Hetzelfde adres, heeft elke record hier een type zoals *Start* of *Business* 

Hallo premises wegwijs als normalisatie van gegevens te**Vermijd redundante gegevens op te slaan** op elke registreren en in plaats daarvan toodata verwijzen. In dit voorbeeld tooread een persoon, met hun contactgegevens en adressen, moet u toouse JOINS tooeffectively Cumulatieve uitvoeringstijd van uw gegevens op.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Bijwerken van één persoon met hun contactgegevens en adressen vereist schrijfbewerkingen over veel afzonderlijke tabellen. 

Nu gaan we kijken hoe we zou model nemen Hallo dezelfde gegevens als een zelfstandig entiteit in de documentdatabase van een.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Met Hallo benadering bovenstaande we nu hebben **gedenormaliseerd** Hallo persoonsrecord waar we **ingesloten** alle informatie over toothis persoon, zoals hun contactgegevens en -adressen in één tooa Hallo JSON-document.
Bovendien omdat we niet beperkt blijven vast tooa schema we hebben Hallo flexibiliteit toodo dingen alsof u contactgegevens van verschillende vormen volledig. 

Bij het ophalen van een persoonsrecord voltooid uit Hallo-database is nu één bewerking met betrekking tot één verzameling en voor één document te lezen. Bijwerken van een persoonsrecord met hun contactgegevens en -adressen is ook een schrijfbewerking voor één voor één document.

Door gegevens denormalizing, uw toepassing moet mogelijk tooissue minder query's en updates toocomplete algemene bewerkingen. 

### <a name="when-tooembed"></a>Wanneer tooembed
In het algemeen gebruikt ingesloten gegevens modellen wanneer:

* Er zijn **bevat** relaties tussen entiteiten.
* Er zijn **één aan enkele** relaties tussen entiteiten.
* Er zijn ingesloten gegevens die **niet vaak veranderen**.
* Er is ingesloten gegevens won't groeien **zonder gebonden**.
* Er is ingesloten gegevens **integraal** toodata in een document.

> [!NOTE]
> Doorgaans data-modellen beter bieden gedenormaliseerd **lezen** prestaties.
> 
> 

### <a name="when-not-tooembed"></a>Wanneer niet tooembed
Hallo databasebestandsgrootte in een documentdatabase toodenormalize is alles en sluit alle gegevens in één document tooa, dit kan ertoe leiden toosome situaties die moeten worden vermeden.

Deze JSON-fragment in beslag nemen.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

Dit is mogelijk wat een post-entiteit met ingesloten opmerkingen eruit zou als we een typische blog of CMS, systeem zijn modelleren. Hallo probleem met dit voorbeeld is dat Hallo opmerkingen matrix is **unbounded**, wat betekent dat er geen limiet (praktische) toohello aantal opmerkingen eventuele één post kan hebben. Dit wordt een probleem worden naarmate Hallo grootte van het Hallo-document kan aanzienlijk toenemen.

Als de grootte Hallo Hallo groeit document Hallo mogelijkheid tootransmit Hallo gegevens via de kabel hello, evenals lezen en bijwerken Hallo-document, op schaal worden beïnvloed.

In dit geval zou het beter tooconsider Hallo na model zijn.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

Dit model heeft Hallo drie meest recente commentaar dat op Hallo van ingesloten zelf, zoals een matrix met een vaste gebonden is dit tijdstip. Hallo andere opmerkingen zijn gegroepeerd in toobatches van 100 opmerkingen en opgeslagen in afzonderlijke documenten. Hallo-grootte van Hallo batch is gekozen als 100 omdat de fictieve toepassing kan Hallo 100 gebruikersopmerkingen tooload tegelijk.  

Een andere aanvraag ingesloten gegevens waar niet een goed idee is is wanneer Hallo ingesloten gegevens vaak worden gebruikt in de documenten en vaak worden gewijzigd. 

Deze JSON-fragment in beslag nemen.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

Dit kan leiden tot slot portfolio van een persoon. We hebt tooembed Hallo voorraad informatie in tooeach portfolio document gekozen. Gegevens die regelmatig veranderen insluiten gaat toomean dat u elk document portfolio voortdurend wordt bijgewerkt telkens wanneer een bestand wordt verhandeld in een omgeving waar gerelateerde gegevens vaak wijzigen als een toepassing, handel stock.

Stock *zaza* mogen worden verhandeld veel honderden keren in een enkele dag en duizenden gebruikers kunnen hebben *zaza* op hun portfolio. Met een gegevensmodel zoals hierboven Hallo zou hebben we tooupdate duizenden portfolio documenten vaak dagelijks voorloopspaties tooa system die won't zeer goed worden geschaald. 

## <a id="Refer"></a>Verwijst naar gegevens
Dus mooi gegevens insluiten werkt voor veel gevallen maar duidelijk is dat er scenario's zijn wanneer uw gegevens denormalizing meer problemen dan het verdient aanbeveling. Dus wat we doen nu? 

Relationele databases zijn niet Hallo enige plaats waar u de relaties tussen entiteiten kunt maken. U kunt de informatie in een document dat daadwerkelijk toodata in andere documenten hoort hebben in een documentdatabase. Nu, ik ben niet pleiten zelfs een minuut dat wij systemen die beter geschikt tooa relationele database in Azure Cosmos-database of een andere documentdatabase maken, maar eenvoudige relaties geen en kunnen zeer nuttig zijn. 

In onderstaande JSON Hallo gekozen we toouse Hallo voorbeeld van een voorraad portfolio van eerder maar dit keer die toohello voorraad item op Hallo portfolio in plaats van het sluiten is. Op deze manier is één slot document Hallo wanneer Hallo voorraad item vaak wordt gewijzigd in de gehele Hallo dag Hallo alleen document dat toobe bijgewerkt moet. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


Een onmiddellijke neerwaartse toothis-methode is echter als uw toepassing vereist tooshow informatie over elke voorraad die wordt veroorzaakt is bij het weergeven van een persoon portfolio; in dit geval moet u toomake meerdere reizen toohello tooload Hallo databasegegevens voor elk document voorraad. We hebben hier een beslissing tooimprove Hallo efficiëntie van schrijfbewerkingen die vaak gedurende de dag van de Hallo gebeuren, maar op zijn beurt inbreuk op Hallo leesbewerkingen die mogelijk minder invloed op prestaties van dit bepaalde systeem Hallo hebben aangebracht.

> [!NOTE]
> Genormaliseerd gegevensmodellen **kunt vereisen meer retouren** toohello-server.
> 
> 

### <a name="what-about-foreign-keys"></a>Hoe zit het met refererende sleutels?
Omdat er momenteel geen concept van een beperking, refererende sleutel of anderszins, de relaties tussen document die u in documenten hebt zijn effectief 'zwakke koppelingen' en kunnen niet worden gecontroleerd door Hallo-database zelf. Als u wilt dat tooensure die gegevens die een document verwijst Hallo tooactually bestaat, moet u toodo dit in uw toepassing of door middel van Hallo van server-side '-triggers of opgeslagen procedures op Azure Cosmos DB.

### <a name="when-tooreference"></a>Wanneer tooreference
In het algemeen gebruikt genormaliseerde gegevens modellen wanneer:

* Voor **een-op-veel** relaties.
* Voor **veel-op-veel** relaties.
* Gerelateerde gegevens **regelmatig wordt gewijzigd**.
* Gegevens waarnaar wordt verwezen, kan worden **unbounded**.

> [!NOTE]
> Doorgaans normaliseren biedt betere **schrijven** prestaties.
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Waar ik Hallo relatie plaatsen?
Hallo groei van Hallo relatie kunt u bepalen in welke document toostore Hallo-verwijzing.

Als we Hallo JSON onderstaande modellen uitgevers en rapporten bekijken.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

Als Hallo Hallo books per uitgever aantal kleine met beperkte groei, kan bewaren Hallo adresboek naslaginformatie Hallo publisher-document nuttig zijn. Echter als Hallo aantal boeken per uitgever unbounded is, leiden klikt u vervolgens deze gegevensmodel toomutable, groeiende matrices, zoals in de bovenstaande Hallo voorbeeld publisher-document. 

Overschakelen van dingen rond een bits zou resulteren in een model dat nog steeds vertegenwoordigt dezelfde gegevens nu Hallo voorkomt deze grote veranderlijke verzamelingen.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

In Hallo hierboven voorbeeld hebben we verwijderd Hallo unbounded verzameling op Hallo publisher-document. In plaats daarvan we zojuist hebben een verwijzing toohello uitgever op elk document adresboek.

### <a name="how-do-i-model-manymany-relationships"></a>Hoe ik veel: veel-relaties model?
In een relationele database *veel:* relaties zijn vaak gemodelleerd met join-tabellen die records uit andere tabellen NET samenvoegen. 

![Tabellen samenvoegen](./media/documentdb-modeling-data/join-table.png)

U mogelijk geneigd tooreplicate Hallo met behulp van dezelfde ding documenten en een gegevensmodel dat vergelijkbare toohello volgende lijkt te produceren.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

Dit zou werken. Echter, ofwel een auteur met hun books laden of het laden van een rapport met de auteur zou moet altijd ten minste twee extra query's op Hallo-database. Een query toohello document en vervolgens een andere query toofetch Hallo werkelijke document wordt toegevoegd. 

Als deze tabel join wordt alleen is lijmen samen twee soorten gegevens waarom niet vermeld het dan niet volledig?
Houd rekening met de volgende Hallo.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Nu als ik had een auteur, ik onmiddellijk weet welke boeken deze geschreven en als ik een boekdocument geladen had zou ik omgekeerd Hallo-id van Hallo auteur (s) kent. Hiermee slaat u die tussenliggende query op Hallo join-tabel beperken Hallo van server aantal retouren uw toepassing toomake heeft. 

## <a id="WrapUp"></a>Hybride gegevensmodellen
We nu hebt bekeken insluiten (of denormalizing) en gegevens van verwijzende (of normaliseren), hebben elk hun upsides en elk compromissen hebben, zoals we hebben gezien. 

Het niet altijd toobe ofwel heeft of, niet Blazende toomix dingen enigszins worden. 

Op basis van de specifieke gebruikspatronen en werkbelastingen die mogelijk zijn er gevallen waarbij de combinatie van ingesloten van uw toepassing en gegevens waarnaar wordt verwezen is wel zinvol en kan lead toosimpler toepassingslogica met minder server retouren tegelijkertijd nog steeds een goede niveau van de prestaties van .

Overweeg het volgende JSON Hallo. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

Hier hebt we Hallo ingesloten model, waarbij gegevens uit andere entiteiten zijn ingesloten in op het hoogste niveau document hello, maar andere gegevens wordt verwezen (voornamelijk) gevolgd. 

Als u Hallo adresboek document bekijkt, ziet u enkele interessante velden wanneer we hello matrix van auteurs bekijkt. Er is een *id* veld die is hello gebruiken we toorefer back tooan auteur document, standaard Oefening in een genormaliseerde model, maar vervolgens is ook het veld hebben *naam* en *thumbnailUrl*. Kan we zojuist hebt vastgelopen met *id* en links Hallo toepassing tooget eventuele aanvullende informatie nodig uit Hallo respectieve auteur document met Hallo "link", maar omdat de naam van de auteur van het Hallo onze toepassing worden weergegeven en een miniatuur met elke adresboek weergegeven we kunt opslaan een round trip toohello server per rapport in een lijst door denormalizing **sommige** gegevens van Hallo auteur.

Controleer of, als de naam van de auteur van het Hallo gewijzigd of dat ze hun photo tooupdate wilden we zou hebben toogo een update elk rapport ze ooit gepubliceerd, maar voor de toepassing, gebaseerd op Hallo veronderstelling dat auteurs niet hun namen vaak veranderen, is dit een acceptabele ontwerp besluit.  

In het Hallo-voorbeeld zijn er **vooraf berekende aggregaties** toosave dure verwerking op een leesbewerking waarden. In voorbeeld Hallo zijn Hallo-gegevens in Hallo auteur document ingesloten gegevens die tijdens de uitvoering wordt berekend. Telkens wanneer een nieuw rapport is gepubliceerd, wordt een boekdocument gemaakt **en** hello countOfBooks veld tooa berekende waarde op basis van het aantal documenten adresboek die beschikbaar zijn voor een bepaalde auteur Hallo is ingesteld. Deze optimalisatie zou zijn goede in lezen zware systemen waar we betaalbare toodo berekeningen bij het schrijven in volgorde toooptimize leest.

Hallo mogelijkheid toohave een model met vooraf berekende velden mogelijk gemaakt wordt omdat Azure Cosmos DB ondersteunt **transacties met meerdere documenten**. Veel NoSQL-opslag kunnen doen transacties meerdere documenten en daarom pleiten ontwerpbeslissingen, zoals 'altijd insluiten alles', vanwege toothis beperking. U kunt met Azure Cosmos DB serverzijde triggers of opgeslagen procedures, die books invoegen en auteurs allemaal binnen een ACID-transactie bijwerken gebruiken. Nu u geen **hebben** tooembed alles in tooone document alleen toobe u ervoor zorgen dat de gegevens consistent blijft.

## <a name="NextSteps"></a>Volgende stappen
Hallo grootste takeaways uit dit artikel is toounderstand dat gegevens in een wereld zonder schema modelleren als ooit net zo belangrijk is. 

Net als er geen eenduidige manier toorepresent een stukje informatie op een scherm is, zijn er geen enkele manier toomodel uw gegevens. U moet toounderstand uw toepassing en hoe deze wordt produceert, gebruiken en Hallo gegevens verwerken. Richtlijnen die hier voorgesteld en u kunnen vervolgens door toe te passen aantal Hallo instellen over het maken van een model die zijn gericht op Hallo onmiddellijke behoeften van uw toepassing. Wanneer uw toepassingen toochange moeten, kunt u gebruikmaken van Hallo flexibiliteit van een database zonder schema tooembrace die wijzigen en het gegevensmodel van uw eenvoudig ontwikkelen. 

toolearn meer informatie over Azure Cosmos DB toohello-service verwijzen [documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina. 

toounderstand hoe tooshard van uw gegevens over meerdere partities verwijzen te[partitioneren van gegevens in Azure Cosmos DB](documentdb-partition-data.md). 
