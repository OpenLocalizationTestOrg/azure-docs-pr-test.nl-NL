---
title: Gids voor opslag tabel aaaAzure | Microsoft Docs
description: Ontwerp schaalbare en zodat tabellen in de Azure-tabelopslag
services: cosmos-db
documentationcenter: na
author: mimig1
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 059f05a1d20e4d9537034b7ca133c5334bbefa04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Ontwerphandleiding voor Azure Storage-tabel: Het ontwerpen van schaalbare en de zodat tabellen
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign schaalbare en zodat tabellen moet u rekening houden met een aantal factoren, zoals prestaties, schaalbaarheid en kosten. Als u eerder schema's voor relationele databases hebt ontworpen, zijn deze overwegingen bekend tooyou, maar er zijn een aantal overeenkomsten tussen hello Azure Table storage servicemodel en relationele modellen, maar er zijn ook veel belangrijk de verschillen. Deze verschillen leiden doorgaans toovery verschillende ontwerpen die lijkt erg intuïtief of onjuiste toosomeone bekend bent met relationele databases, maar maak die zinvol als u voor een NoSQL-sleutel/waarde-archief zoals hello Azure Table-service ontwerpt. Veel van de verschillen in het ontwerp geeft Hallo feit dat de tabelservice Hallo ontworpen toosupport cloud-toepassingen met miljarden entiteiten (rijen in een relationele database-terminologie) van gegevens of voor gegevenssets die zeer hoge moet ondersteunen transactie-volumes: daarom moet toothink anders over hoe u uw gegevens opslaat en begrijpen hoe Hallo tabelservice werkt. Een goed ontworpen NoSQL-gegevensarchief kunt uw oplossing tooscale inschakelen veel meer (en, tegen lagere kosten) dan een oplossing die gebruikmaakt van een relationele database. Deze handleiding helpt u met deze onderwerpen.  

## <a name="about-hello-azure-table-service"></a>Over hello Azure Table-service
Deze sectie worden enkele Hallo belangrijkste functies van de tabelservice Hallo die vooral relevant toodesigning voor prestaties en schaalbaarheid. Als u nieuwe tooAzure opslag en Hallo tabelservice, lees eerst [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md) en [aan de slag met Azure Table Storage met .NET](table-storage-how-to-use-dotnet.md) voordat het lezen van de rest van dit Hallo artikel. Hoewel de focus Hallo van deze handleiding op Hallo tabelservice, bevat deze sommige bespreking van hello Azure Queue en services Blob, en hoe u ze samen met de Hallo service van de tabel in een oplossing mogelijk gebruiken.  

Wat is tabelservice Hallo? Zoals u van Hallo-naam verwachten zou, gebruikt Hallo tabelservice een tabelindeling toostore-gegevens. Elke rij van de tabel Hallo een entiteit vertegenwoordigt in standaard Hallo-terminologie en Hallo kolommen store Hallo verschillende eigenschappen van die entiteit. Elke entiteit heeft een paar sleutels toouniquely worden geïdentificeerd en een timestamp-kolom die de tabelservice Hallo tootrack gebruikt wanneer Hallo entiteit voor het laatst is bijgewerkt (dit gebeurt automatisch en Hallo tijdstempel kan niet handmatig worden overschreven met een willekeurige waarde). Hallo tabelservice maakt gebruik van deze optimistische gelijktijdigheid van laatste wijziging tijdstempel (LMT) toomanage.  

> [!NOTE]
> Hallo tabel servicebewerkingen REST API ook retourneren een **ETag** waarde die deze is afgeleid van Hallo last-modified tijdstempel (LMT). In dit document we gebruiken Hallo termen ETag en LMT door elkaar omdat ze toohello verwijzen dezelfde onderliggende gegevens.  
> 
> 

Hallo volgende voorbeeld ziet u een eenvoudige tabel ontwerp toostore entiteiten werknemer en afdeling. Veel van Hallo voorbeelden die verderop in deze handleiding zijn gebaseerd op dit eenvoudige ontwerp.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>tijdstempel</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Jan</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Jun</td>
<td>CaO</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Afdeling</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Verkoop</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Tot nu toe, ziet deze eruit vergelijkbaar tooa tabel in een relationele database met Hallo belangrijke verschillen wordt Hallo verplichte kolommen en hello mogelijkheid toostore meerdere entiteit van het type in Hallo dezelfde tabel. Bovendien elk van de gebruiker gedefinieerde eigenschappen zoals Hallo **FirstName** of **leeftijd** heeft een gegevenstype, zoals geheel getal of tekenreeks, net zoals een kolom in een relationele database. Hoewel in tegenstelling tot in een relationele database Hallo schema minder aard van Hallo tabel-service betekent dat een eigenschap moet geen Hallo hetzelfde gegevenstype voor elke entiteit. toostore complexe gegevenstypen in één eigenschap, moet u een zoals JSON of XML-serialisatie-indeling. Zie voor meer informatie over Hallo tabel-service, zoals ondersteunde gegevenstypen, ondersteunde datumbereiken naamgevingsregels en beperkingen voor [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Zoals u ziet, uw keuze van **PartitionKey** en **RowKey** fundamentele toogood tabelontwerp is. Elke entiteit die is opgeslagen in een tabel moet een unieke combinatie van **PartitionKey** en **RowKey**. Net als bij de sleutels in een relationele database, Hallo **PartitionKey** en **RowKey** waarden zijn geïndexeerde toocreate een geclusterde index waarmee u snel te zoeken; echter Hallo service tabel maakt geen een secundaire indexen, zodat deze Hallo slechts twee geïndexeerde eigenschappen (aantal Hallo patronen verderop tonen hoe u deze duidelijk beperking kunt omzeilen).  

Een tabel bestaat uit een of meer partities en zoals u ziet, veel Hallo beslissingen die u zal worden rond het kiezen van een geschikte ontwerp **PartitionKey** en **RowKey** toooptimize uw oplossing. Een oplossing kan bestaan uit slechts één tabel die de entiteiten die zijn onderverdeeld in partities bevat, maar doorgaans een oplossing heeft meerdere tabellen. Tabellen kunt u toologically ordenen uw entiteiten, u helpt toegang toohello gegevens met toegangsbeheerlijsten en u kunt een hele tabel met een één opslag-bewerking neerzetten.  

### <a name="table-partitions"></a>Tabelpartities
Hallo-accountnaam, de tabelnaam en **PartitionKey** Hallo partitie in opslagservice Hallo waar tabelservice Hallo Hallo entiteit opgeslagen samen te identificeren. Onderdeel van Hallo adresschema voor entiteiten zijn, partities een bereik voor transacties definiëren (Zie [entiteit groepstransacties](#entity-group-transactions) hieronder), en formulier Hallo op basis van hoe Hallo tabelservice schaalt. Zie voor meer informatie over partities [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md).  

Een afzonderlijke knooppunten services in Hallo service tabel, een of meer partities voltooien en service schaalt door dynamisch taakverdeling Hallo partities over knooppunten. Als een knooppunt belast wordt, Hallo tabelservice kunt *splitsen* Hallo bereik van partities wordt onderhouden door dat knooppunt op verschillende knooppunten; wanneer verkeer subsidies, Hallo-service kan *samenvoegen* Hallo partitie variërend van stille knooppunten terug op één knooppunt.  

Voor meer informatie over Hallo interne details van Hallo Tabelservice en in het bijzonder hoe Hallo service partities beheert, Zie Hallo papier [Microsoft Azure Storage: een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Entiteit groep transacties
In Hallo tabel-service zijn transacties entiteit (EGTs) Hallo alleen ingebouwde mechanisme voor het uitvoeren van atomaire updates tussen meerdere entiteiten. Er zijn ook EGTs waarnaar wordt verwezen tooas *batch transacties* in sommige documentatie. EGTs werkt alleen voor entiteiten die zijn opgeslagen in Hallo dezelfde partitie (share Hallo dezelfde partitiesleutel in een bepaalde tabel), telkens wanneer u atomic transactionele gedrag tussen meerdere entiteiten moet er daarom tooensure die deze entiteiten in Hallo dezelfde partitie. Dit is vaak een reden voor het behouden van meerdere Entiteitstypen in Hallo dezelfde tabel (en partitie) en meerdere tabellen voor verschillende Entiteitstypen niet gebruiken. Een enkele EGT kan werken op maximaal 100 entiteiten.  Als u meerdere gelijktijdige EGTs indienen voor verwerking van het is belangrijk tooensure werkt deze EGTs niet op de entiteiten die voor EGTs gelden zoals anders verwerking kan worden vertraagd.

EGTs ook een mogelijke waarde voor tooevaluate in uw ontwerp geïntroduceerd: Hallo schaalbaarheid van uw toepassing met behulp van meer partities wordt verhoogd omdat Azure heeft meer mogelijkheden voor aanvragen voor taakverdeling over de knooppunten, maar dit Hallo mogelijk beperken de mogelijkheid van uw toepassing tooperform-atomic transacties en sterke consistentie voor uw gegevens onderhouden. Bovendien de schaalbaarheidsdoelen van specifieke op Hallo niveau van een partitie die Hallo doorvoer van transacties die u voor één knooppunt verwachten kunt kan beperken er zijn: voor meer informatie over Hallo schaalbaarheidsdoelen voor Azure storage-accounts en Hallo tabel service, raadpleegt [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md). Latere secties van deze handleiding worden verschillende ontwerp strategieën die u helpen bij verschillen zoals deze beheren en optimale toochoose uw partitiesleutel op basis van specifieke vereisten van uw clienttoepassing hello bespreken.  

### <a name="capacity-considerations"></a>Overwegingen voor capaciteitsplanning
Hallo bevat volgende tabel enkele Hallo sleutelwaarden toobe op de hoogte van tijdens het ontwerpen van een oplossing voor tabel-service:  

| Totale capaciteit van een Azure storage-account | 500 TB |
| --- | --- |
| Aantal tabellen in een Azure storage-account |Alleen beperkt door het Hallo-capaciteit van Hallo storage-account |
| Aantal partities in een tabel |Alleen beperkt door het Hallo-capaciteit van Hallo storage-account |
| Aantal entiteiten in een partitie |Alleen beperkt door het Hallo-capaciteit van Hallo storage-account |
| Grootte van een afzonderlijke entiteit |Omhoog too1 MB van maximaal 255 eigenschappen (inclusief Hallo **PartitionKey**, **RowKey**, en **tijdstempel**) |
| Grootte van Hallo **PartitionKey** |Een tekenreeks van too1 KB groot |
| Grootte van Hallo **RowKey** |Een tekenreeks van too1 KB groot |
| Grootte van een entiteit groep-transactie |Een transactie kan maximaal 100 entiteiten bevatten en Hallo nettolading moet minder dan 4 MB groot. Een EGT kan slechts eenmaal bijwerken een entiteit. |

Zie voor meer informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Kosten overwegingen
Tabelopslag relatief goedkope is, maar moet u kosten maakt een schatting voor beide capaciteit gebruiks- en Hallo aantal transacties opnemen als onderdeel van de evaluatie van een oplossing die gebruikmaakt van Hallo tabel-service. In veel scenario's voor het opslaan van gedenormaliseerd of dubbele gegevens in de volgorde tooimprove Hallo is prestaties en schaalbaarheid van uw oplossing echter een tootake geldig benadering. Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Richtlijnen voor het tabelontwerp van de
Deze lijsten samenvatten aantal Hallo sleutel richtlijnen die u rekening houden moet bij het ontwerpen van uw tabellen en deze handleiding los deze allemaal in meer detail later in. Deze richtlijnen zijn heel verschillend van Hallo richtlijnen die u doorgaans als voor het ontwerp van relationele database volgt.  

Het ontwerpen van uw tabel-service-oplossing toobe *lezen* efficiënt:

* ***Ontwerpen voor het uitvoeren van toepassingen waarin lezen veel query's.*** Tijdens het ontwerpen van uw tabellen nadenken over Hallo query's (met name Hallo latentie gevoelig die) die zal worden uitgevoerd voordat u nadenken over hoe u uw entiteiten wordt bijgewerkt. Dit leidt meestal tot een efficiënte en zodat oplossing.  
* ***Geef zowel PartitionKey en RowKey in uw query's.*** *Query's wijst* zoals deze zijn Hallo meest efficiënt tabel service query's.  
* ***Houd rekening met dubbele exemplaren van entiteiten opslaan.*** Tabelopslag is goedkope moet dezelfde entiteit meerdere keren (met verschillende sleutels) opslaan Hallo tooenable efficiënter query's.  
* ***U kunt uw gegevens denormalizing.*** Tabelopslag goedkope is dus Overweeg denormalizing van uw gegevens. Samenvatting entiteiten bijvoorbeeld opslaan zodat query's voor statistische gegevens slechts één entiteit tooaccess hoeft.  
* ***Gebruik de samengestelde sleutel komt.*** Hallo alleen sleutels die u hebt zijn **PartitionKey** en **RowKey**. Gebruik bijvoorbeeld samengestelde sleutelwaarden tooenable alternatieve sleutelhash toegang paden tooentities.  
* ***Query-projectie gebruiken.*** U kunt verkleinen Hallo hoeveelheid gegevens die u via Hallo netwerk overbrengen met behulp van query's die alleen Hallo velden, u moet selecteert.  

Het ontwerpen van uw tabel-service-oplossing toobe *schrijven* efficiënt:  

* ***Maak geen hot partities.*** Kies toetsen waarmee u toospread uw aanvragen over meerdere partities op elk moment.  
* ***Vermijd pieken in het verkeer.*** Hallo-verkeer via een redelijke periode vloeiend en pieken in het verkeer worden vermeden.
* ***Niet per se een afzonderlijke tabel voor elk type entiteit maken.*** Wanneer u atomische transacties op Entiteitstypen vereisen, slaat u deze meerdere Entiteitstypen in dezelfde partitie in Hallo Hallo dezelfde tabel.
* ***U kunt de maximale doorvoer Hallo die moeten worden gerealiseerd.*** U moet rekening houden met de Hallo schaalbaarheidsdoelen voor Hallo tabelservice en zorg ervoor dat uw ontwerp niet u tooexceed tot leidt ze.  

Als u deze handleiding leest, ziet u voorbeelden die al deze principes in de praktijk geplaatst.  

## <a name="design-for-querying"></a>Ontwerp voor het uitvoeren van query 's
Oplossingen voor tabel-service kunnen worden gelezen intensief, schrijven intensief of een combinatie van Hallo twee. In deze sectie richt zich op Hallo dingen toobear in rekening wanneer u uw tabel service toosupport leesbewerkingen efficiënt ontwerpt. Een ontwerp dat ondersteunt lees-en schrijfopdrachten efficiënt is meestal ook efficiënt voor schrijfbewerkingen. Er zijn echter aanvullende overwegingen toobear in rekening wanneer ontwerpen toosupport schrijfbewerkingen, die wordt besproken in de volgende sectie hello, [ontwerp voor wijziging van gegevens](#design-for-data-modification).

Een goed uitgangspunt voor het ontwerpen van uw tooenable tabel-service-oplossing u tooread gegevens efficiënt is tooask "welke query wordt mijn nodig tooexecute tooretrieve Hallo toepassingsgegevens uit de tabelservice Hallo moet?"  

> [!NOTE]
> Met de Hallo tabelservice, is het belangrijk tooget Hallo ontwerp juiste vooraf omdat het is moeilijk en kostbaar proces toochange later. Bijvoorbeeld in een relationele database, is het vaak mogelijk tooaddress prestatieproblemen gewoon door toe te voegen de bestaande database tooan indexeert: dit is geen optie Hello tabel-service.  
> 
> 

Deze sectie legt de nadruk op Hallo sleutel die u houden moet bij het ontwerpen van uw tabellen voor het uitvoeren van query's. Hallo-onderwerpen in deze sectie zijn onder andere:

* [Hoe uw keuze van PartitionKey en RowKey van invloed is op prestaties van query 's](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Een juiste PartitionKey kiezen](#choosing-an-appropriate-partitionkey)
* [Query's voor Hallo tabelservice optimaliseren](#optimizing-queries-for-the-table-service)
* [Sorteren van gegevens in Hallo tabelservice](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Hoe uw keuze van PartitionKey en RowKey van invloed is op prestaties van query 's
Hallo volgende voorbeelden wordt ervan uitgegaan dat het opslaan van tabelservice Hallo is werknemer entiteiten met Hallo structuur te volgen (Hallo voorbeelden de meeste weglaten Hallo **tijdstempel** eigenschap voor de duidelijkheid):  

| *Kolomnaam* | *Gegevenstype* |
| --- | --- |
| **PartitionKey** (naam van de afdeling) |Tekenreeks |
| **RowKey** (werknemer-Id) |Tekenreeks |
| **Voornaam** |Tekenreeks |
| **Achternaam** |Tekenreeks |
| **Leeftijd** |Geheel getal |
| **EmailAddress** |Tekenreeks |

Hallo eerdere sectie [overzicht van de service Azure Table](#overview) beschrijft een aantal Hallo belangrijkste functies van hello Azure Table-service waarvoor een directe invloed op ontwerpen voor query. Deze leiden tot Hallo algemene richtlijnen voor het ontwerpen van query's tabel-service. Houd er rekening mee dat Hallo filtersyntaxis in onderstaande Hallo voorbeelden gebruikt uit Hallo tabelservice REST API, Zie voor meer informatie [Query entiteiten](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* Een ***punt Query*** Hallo meest efficiënt lookup toouse en wordt aanbevolen toobe gebruikt voor zoekopdrachten met hoog volume of zoekacties laagste latentie vereisen. Dergelijke query kan zeer efficiënt Hallo indexen toolocate een afzonderlijke entiteit gebruiken door op te geven beide Hallo **PartitionKey** en **RowKey** waarden. Bijvoorbeeld: $filter = (PartitionKey eq 'Sales') en (RowKey eq '2')  
* Tweede in de rij is een ***Bereikquery*** die gebruikmaakt van Hallo **PartitionKey** en filters op een reeks **RowKey** waarden tooreturn meer dan één entiteit. Hallo **PartitionKey** waarde identificeert een specifieke partitie en Hallo **RowKey** waarden een subset van Hallo entiteiten in de betreffende partitie identificeren. Bijvoorbeeld: $filter = PartitionKey eq 'Verkoop en de RowKey ge' en RowKey lt t '  
* Derde beste is een ***partitie scannen*** die gebruikmaakt van Hallo **PartitionKey** en filters op een andere niet-sleutelkenmerk eigenschap en die mogelijk meer dan één entiteit geretourneerd. Hallo **PartitionKey** waarde identificeert een specifieke partitie en Hallo eigenschap waarden selecteren voor een subset van Hallo entiteiten in de betreffende partitie. Bijvoorbeeld: $filter = PartitionKey eq 'Verkoop' en LastName eq 'Smith'  
* Een ***tabel scannen*** omvat geen Hallo **PartitionKey** en zeer inefficiënte omdat alle partities Hallo die gezamenlijk uw tabel voor de overeenkomende entiteiten op zijn beurt wordt doorzocht. Wordt uitgevoerd om een tabelscan ongeacht of het filter Hallo gebruikt **RowKey**. Bijvoorbeeld: $filter = LastName eq 'Jones'  
* Query's die meerdere entiteiten retourneren retourneren ze gesorteerd **PartitionKey** en **RowKey** volgorde. tooavoid sorteren Hallo entiteiten in Hallo-client, kies een **RowKey** Hallo meest voorkomende sorteervolgorde te definiëren.  

Houd er rekening mee dat als u met een '**of**' toospecify een filter op basis van **RowKey** waarden resulteert in een partitie scan en wordt niet behandeld als een bereikquery. U moet daarom query's die worden gebruikt, zoals filters: $filter = PartitionKey eq 'Sales' (RowKey eq '121' of een RowKey eq '322')  

Zie voor voorbeelden van clientcode die gebruikmaken van Hallo Storage-clientbibliotheek tooexecute efficiënt query's:  

* [Uitvoeren van een punt-query Hallo Storage-clientbibliotheek](#executing-a-point-query-using-the-storage-client-library)
* [Bij het ophalen van meerdere entiteiten met behulp van LINQ](#retrieving-multiple-entities-using-linq)
* [Projectie-serverzijde](#server-side-projection)  

Voor voorbeelden van clientcode dat meerdere entiteit kan verwerken typen opgeslagen in Hallo dezelfde tabel, Zie:  

* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Een juiste PartitionKey kiezen
Uw keuze van **PartitionKey** moeten worden verdeeld Hallo nodig tooenables Hallo gebruik van EGTs (consistentie van tooensure) tegen Hallo vereiste toodistribute uw entiteiten meerdere partities (tooensure schaalbare oplossing).  

Aan één extreme u alle entiteiten in uw kan opslaan in een enkele partitie, maar dit Hallo schaalbaarheid van uw oplossing kan beperken en zou verhinderen Hallo tabelservice kunnen tooload-aanvragen. Op Hallo andere extreme, kunt u één entiteit per partitie, die wel uiterst schaalbare en waardoor Hallo tabel serviceaanvragen tooload saldo, maar dat zou voorkomen dat u entiteitstransacties opslaan.  

Een ideaal **PartitionKey** is een waarmee u toouse efficiënt query's en die voldoende partities tooensure heeft uw oplossing schaalbaar is. Normaal gesproken zult u merken dat uw entiteiten een geschikte eigenschap die de entiteiten over voldoende partities verdeelt hebben.

> [!NOTE]
> Bijvoorbeeld in een systeem dat wordt informatie over gebruikers- of werknemers opgeslagen, gebruikers-id is mogelijk een goede PartitionKey. Mogelijk hebt u verschillende entiteiten die een opgegeven gebruikers-id als partitiesleutel hello gebruiken. Elke entiteit die gegevens over een gebruiker opslaat in een enkele partitie worden gegroepeerd en dus deze entiteiten zijn toegankelijk via entiteit groepstransacties, terwijl u nog steeds zeer schaalbaar.
> 
> 

Er zijn aanvullende overwegingen bij de keuze van **PartitionKey** die betrekking hebben toohow wordt u invoegen, bijwerken en verwijderen van entiteiten: Zie de sectie Hallo [ontwerp voor wijziging van gegevens](#design-for-data-modification) hieronder.  

### <a name="optimizing-queries-for-hello-table-service"></a>Query's voor Hallo tabelservice optimaliseren
Hallo tabelservice indexeert automatisch de entiteiten met Hallo **PartitionKey** en **RowKey** waarden in een enkele geclusterde index daarom reden dat punt query's efficiëntste toouse zijn Hallo Hallo . Er zijn echter geen indexen dan die op een geclusterde index op Hallo Hallo **PartitionKey** en **RowKey**.

Veel ontwerpen moeten voldoen aan vereisten tooenable lookup entiteiten op basis van meerdere criteria. Bijvoorbeeld zoeken naar werknemer entiteiten op basis van e-mailadres werknemer-id of achternaam op. Hallo volgende patronen in de sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) deze typen vereiste op te lossen en manieren om te werken om Hallo feit Hallo tabel-service biedt geen secundaire indexen te beschrijven:  

* [Intra-partitie secundaire index patroon](#intra-partition-secondary-index-pattern) -opslaan meerdere exemplaren van elke entiteit met behulp van verschillende **RowKey** waarden (in Hallo dezelfde partitie) tooenable snelle en efficiënte zoekacties en alternatieve sorteren orders door gebruik te maken andere **RowKey** waarden.  
* [Secundaire tussen partitioneren van index patroon](#inter-partition-secondary-index-pattern) : opslaan van meerdere exemplaren van elke entiteit met verschillende waarden voor de RowKey in afzonderlijke partities of afzonderlijke tabellen tooenable snel en efficiënt zoekacties en alternatieve sorteren orders met behulp van verschillende **RowKey** waarden.  
* [Index entiteiten patroon](#index-entities-pattern) -onderhouden entiteiten tooenable efficiënt zoekacties in de index die lijsten van entiteiten retourneren.  

### <a name="sorting-data-in-hello-table-service"></a>Sorteren van gegevens in Hallo tabelservice
Hallo tabelservice retourneert entiteiten in oplopende volgorde op basis van gesorteerd **PartitionKey** en vervolgens op **RowKey**. Deze sleutels worden tekenreekswaarden en tooensure die numerieke waarden correct sorteren die u moet deze tooa vaste lengte converteren en ze worden opgevuld met nullen. Bijvoorbeeld, als hello werknemer-id-waarde u als Hallo **RowKey** is een geheel getal, moet u de werknemer-id converteren **123** te**00000123**.  

Veel toepassingen hebben vereisten toouse gegevens gesorteerd in verschillende volgorden: werknemers bijvoorbeeld sorteren op naam of door datum. Hallo volgende patronen in de sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) adres hoe tooalternate sorteervolgorde van de entiteiten:  

* [Intra-partitie secundaire index patroon](#intra-partition-secondary-index-pattern) -meerdere exemplaren van elke entiteit met verschillende waarden voor de RowKey opslaan (in Hallo dezelfde partitie) tooenable snelle en efficiënte zoekacties en alternatieve sorteren orders met behulp van verschillende RowKey waarden.  
* [Secundaire tussen partitioneren van index patroon](#inter-partition-secondary-index-pattern) : opslaan van meerdere exemplaren van elke entiteit met behulp van verschillende waarden voor de RowKey in afzonderlijke partities in afzonderlijke tabellen tooenable snel en efficiënt zoekacties en alternatieve sorteren orders met behulp van verschillende RowKey waarden.
* [Logboek tail patroon](#log-tail-pattern) -ophalen Hallo  *n*  tooa partitie entiteiten meest recent toegevoegd met behulp van een **RowKey** waarde die in omgekeerde datum en tijd volgorde worden gesorteerd.  

## <a name="design-for-data-modification"></a>Ontwerp voor wijziging van gegevens
Deze sectie richt zich op Hallo ontwerpoverwegingen voor het optimaliseren van toevoegingen, updates, en worden verwijderd. In sommige gevallen moet u tooevaluate Hallo compromis tussen ontwerpen die voor een query op modellen die voor wijziging van gegevens, optimaliseren net als in ontwerpen voor relationele databases (Hoewel Hallo technieken voor het beheren van ontwerp Hallo optimaliseren verschillen zijn verschillend in een relationele database). sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) sommige gedetailleerde ontwerppatronen voor Hallo service tabel wordt beschreven en worden enkele deze verschillen. In de praktijk vindt u veel ontwerpen die zijn geoptimaliseerd voor het uitvoeren van query's entiteiten ook geschikt voor entiteiten wijzigen.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Hallo prestaties optimaliseren van invoegen, bijwerken en verwijderen bewerkingen
tooupdate of een entiteit verwijderen, moet u kunnen tooidentify deze met behulp van Hallo **PartitionKey** en **RowKey** waarden. In dit opzicht van uw keuze **PartitionKey** en **RowKey** voor het wijzigen van entiteiten moet volgen vergelijkbare criteria tooyour keuze toosupport wijst u query's omdat u wilt dat tooidentify entiteiten als efficiënt mogelijk. U niet wilt dat een inefficiënte partitie of tabel scan toolocate een entiteit in volgorde toodiscover hello toouse **PartitionKey** en **RowKey** waarden tooupdate of u deze verwijderen.  

Hallo volgende patronen in de sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) adres optimaliseren Hallo prestaties of uw invoegen, bijwerken en verwijderen van bewerkingen:  

* [Hoog volume patroon verwijderen](#high-volume-delete-pattern) -Enable Hallo verwijdering van een groot aantal entiteiten doordat alle Hallo-entiteiten voor gelijktijdige verwijdering in hun eigen afzonderlijke tabel; u Hallo entiteiten verwijderen door Hallo tabel te verwijderen.  
* [Patroon van de reeks gegevens](#data-series-pattern) -Store voltooid gegevensreeksen in een enkele entiteit toominimize Hallo aantal aanvragen die u aanbrengt.  
* [Wide entiteiten patroon](#wide-entities-pattern) -gebruik van meerdere fysieke entiteiten toostore logische entiteiten met meer dan 252 eigenschappen.  
* [Grote entiteiten patroon](#large-entities-pattern) -gebruik blob storage toostore grote eigenschapswaarden.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Uw opgeslagen entiteiten consistent te houden
andere belangrijke factor waarmee uw keuze van sleutels voor het optimaliseren van gegevenswijzigingen is Hallo hoe tooensure consistentie met behulp van atomische transacties. U kunt alleen een toooperate EGT gebruiken voor entiteiten die zijn opgeslagen in Hallo dezelfde partitie.  

Hallo volgende patronen in de sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) adres consistentie beheren:  

* [Intra-partitie secundaire index patroon](#intra-partition-secondary-index-pattern) -opslaan meerdere exemplaren van elke entiteit met behulp van verschillende **RowKey** waarden (in Hallo dezelfde partitie) tooenable snelle en efficiënte zoekacties en alternatieve sorteren orders door gebruik te maken andere **RowKey** waarden.  
* [Secundaire tussen partitioneren van index patroon](#inter-partition-secondary-index-pattern) : opslaan van meerdere exemplaren van elke entiteit met verschillende waarden voor de RowKey in afzonderlijke partities of afzonderlijke tabellen tooenable snel en efficiënt zoekacties en alternatieve sorteren orders met behulp van verschillende **RowKey** waarden.  
* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern) -uiteindelijk consistent gedrag over grenzen van partities of opslag system grenzen inschakelen met behulp van Azure wachtrijen.
* [Index entiteiten patroon](#index-entities-pattern) -onderhouden entiteiten tooenable efficiënt zoekacties in de index die lijsten van entiteiten retourneren.  
* [Denormalization patroon](#denormalization-pattern) -combineren van de bijbehorende gegevens samen in een enkele entiteit tooenable tooretrieve u alle gegevens die u met een query één punt moet Hallo.  
* [Patroon van de reeks gegevens](#data-series-pattern) -Store voltooid gegevensreeksen in een enkele entiteit toominimize Hallo aantal aanvragen die u aanbrengt.  

Zie voor informatie over entiteit groepstransacties Hallo sectie [entiteit groepstransacties](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Uw ontwerp voor efficiënte wijzigingen gezorgd vereenvoudigt efficiënt query 's
Een ontwerp voor een efficiënte query resulteert in efficiënt wijzigingen, maar u moet altijd in veel gevallen evalueren of dit Hallo-aanvraag voor uw specifieke scenario. Aantal van patronen in de sectie Hallo Hallo [ontwerppatronen voor tabel](#table-design-patterns) expliciet evalueren verschillen tussen het uitvoeren van query's en entiteiten wijzigen en u moet altijd rekening gehouden Hallo het nummer van elk type bewerking.  

Hallo volgende patronen in de sectie Hallo [ontwerppatronen voor tabel](#table-design-patterns) adres verschillen tussen ontwerpen voor efficiënt query's en ontwerpen voor wijziging van efficiënte gegevens:  

* [Samengestelde sleutelpatroon](#compound-key-pattern) -gebruik samengestelde **RowKey** waarden tooenable een client toolookup gerelateerde gegevens met een query één punt.  
* [Logboek tail patroon](#log-tail-pattern) -ophalen Hallo  *n*  tooa partitie entiteiten meest recent toegevoegd met behulp van een **RowKey** waarde die in omgekeerde datum en tijd volgorde worden gesorteerd.  

## <a name="encrypting-table-data"></a>Versleuteling van tabelgegevens
Hallo .NET Azure Storage-clientbibliotheek ondersteunt de versleuteling van entiteitseigenschappen tekenreeks voor invoegen en vervang bewerkingen. Hallo versleutelde tekenreeksen op Hallo-service worden opgeslagen als binaire eigenschappen en ze back toostrings na de decodering worden omgezet.    

Voor tabellen bovendien toohello versleutelingsbeleid, gebruikers moeten opgeven Hallo eigenschappen toobe versleuteld. Dit kan worden gedaan door een kenmerk [EncryptProperty] (voor POCO-entiteiten die zijn afgeleid van TableEntity) of een omzetter versleuteling in de aanvraag-opties. Een oplossing versleuteling is een gemachtigde die ervoor zorgt dat een partitiesleutel, rijsleutel en de naam van eigenschap retourneert een Booleaanse waarde die aangeeft of de eigenschap die moet worden versleuteld. Hallo-clientbibliotheek gebruiken tijdens het versleutelen kan deze informatie toodecide toe of een eigenschap tijdens het schrijven van toohello kabel moet worden versleuteld. Hallo gemachtigde biedt ook de mogelijkheid Hallo van logica over hoe eigenschappen zijn gecodeerd. (Bijvoorbeeld als X, vervolgens versleutelen eigenschap A; anders versleutelen eigenschappen A en B.) Houd er rekening mee dat deze is niet nodig tooprovide deze informatie tijdens het lezen of het uitvoeren van query's entiteiten.

Houd er rekening mee dat samenvoegen wordt momenteel niet ondersteund. Omdat een subset van eigenschappen mogelijk zijn versleuteld eerder met een andere sleutel, leidt gewoon samenvoegen Hallo nieuwe eigenschappen en bijwerken van Hallo metagegevens tot verlies van gegevens. Samenvoegen van een vereist extra service waardoor tooread Hallo vooraf bestaande entiteit aanroepen vanaf Hallo service of met een nieuwe sleutel per eigenschap, die beide zijn niet geschikt voor betere prestaties.     

Zie voor meer informatie over het coderen van tabelgegevens [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](../storage/common/storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Modellering van relaties
Ontwikkelen van domeinmodellen is een belangrijke stap in de ontwerp Hallo van complexe systemen. Normaal gesproken gebruikt u Hallo modellering proces tooidentify entiteiten en relaties tussen deze als een manier toounderstand Hallo Hallo business-domein en Hallo ontwerp van uw systeem te informeren. Deze sectie richt zich op hoe Vertaal Hallo voorkomende relatie typen gevonden in domein modellen toodesigns voor Hallo tabel-service. Hallo wordt-toewijzing van een logische-gegevensmodel tooa fysieke gebaseerd NoSQL-gegevensmodel sterk verschilt van die gebruikt bij het ontwerpen van een relationele database. Relationele databases ontwerp neemt doorgaans een gegevens-normalisatie-proces geoptimaliseerd voor het minimaliseren van redundantie – en een declaratieve opvragen capaciteit die samenvattingen Hallo hoe implementatie van de werking van Hallo-database.  

### <a name="one-to-many-relationships"></a>Een-op-veel-relaties
Een-op-veel-relaties tussen bedrijven domeinobjecten heel vaak gebeuren: één afdeling heeft bijvoorbeeld veel werknemers. Er zijn verschillende manieren tooimplement een-op-veel-relaties in Hallo tabelservice, elk met de voor- en nadelen die mogelijk relevant toohello bepaald scenario.  

Bekijk Hallo voorbeeld van een grote onderneming met meerdere nationale met tienduizenden afdelingen en werknemer entiteiten waar elke afdeling heeft veel werknemers en elke werknemer die gekoppeld is aan een bepaalde afdeling. Een aanpak is toostore afzonderlijke afdeling en entiteiten van de werknemer zoals deze:  

![][1]

Dit voorbeeld ziet u een impliciete een-op-veel-relatie tussen Hallo typen op basis van Hallo **PartitionKey** waarde. Elke afdeling kan veel werknemers hebben.  

In dit voorbeeld toont ook een entiteit afdeling en de gerelateerde werknemer entiteiten in dezelfde partitie Hallo. U kunt verschillende partities toouse, tabellen of zelfs storage-accounts voor de verschillende Entiteitstypen Hallo.  

Een alternatieve methode is toodenormalize zoals weergegeven in het volgende voorbeeld Hallo uw gegevens en store enige werknemer entiteiten met gedenormaliseerd afdelingsgegevens. In dit specifieke scenario gedenormaliseerd hiervan mogelijk niet Hallo aanbevolen als u een vereiste toobe kunnen toochange Hallo details van een afdelingsmanager hebt omdat toodo dit u tooupdate moet elke werknemer in het Hallo-afdeling.  

![][2]

Zie voor meer informatie, Hallo [Denormalization patroon](#denormalization-pattern) verderop in deze handleiding.  

Hallo volgende tabel ziet u Hallo-voor- en nadelen van elke Hallo benaderingen die hierboven worden beschreven voor het opslaan van de werknemer en afdeling entiteiten met een-op-veel-relatie een. U moet ook overwegen hoe vaak verwacht u dat tooperform verschillende bewerkingen: acceptabele toohave een ontwerp waarin een dure bewerking als die voor deze bewerking alleen zelden gebeurt kan zijn.  

<table>
<tr>
<th>Benadering</th>
<th>Professionals</th>
<th>Nadelen</th>
</tr>
<tr>
<td>Afzonderlijke Entiteitstypen, dezelfde partitie, dezelfde tabel</td>
<td>
<ul>
<li>U kunt een entiteit afdeling bijwerken met één bewerking.</li>
<li>U kunt een EGT toomaintain consistentie als er een vereiste toomodify een entiteit afdeling wanneer u update, invoegen, verwijderen een werknemer entiteit. Bijvoorbeeld als u een aantal afdelingen medewerkers voor elke afdeling onderhouden.</li>
</ul>
</td>
<td>
<ul>
<li>Mogelijk moet u tooretrieve een werknemer en een entiteit van de afdeling voor sommige activiteiten van de client.</li>
<li>Opslagbewerkingen gebeuren in Hallo dezelfde partitie. Hoge transactie volumes, kan dit resulteren in een hotspot.</li>
<li>U kunt het nieuwe afdeling van een werknemer tooa met behulp van een EGT niet verplaatsen.</li>
</ul>
</td>
</tr>
<tr>
<td>Afzonderlijke Entiteitstypen, verschillende partities of tabellen of storage-accounts</td>
<td>
<ul>
<li>U kunt een entiteit van de afdeling of de werknemer entiteit bijwerken met één bewerking.</li>
<li>Op hoog transactie volumes, kunnen hierdoor verspreiding Hallo load meerdere meer partities.</li>
</ul>
</td>
<td>
<ul>
<li>Mogelijk moet u tooretrieve een werknemer en een entiteit van de afdeling voor sommige activiteiten van de client.</li>
<li>U kunt EGTs toomaintain consistentie niet gebruiken wanneer u update, invoegen, verwijderen van een werknemer en update een afdeling. Een aantal werknemers in een entiteit afdeling bijvoorbeeld wordt bijgewerkt.</li>
<li>U kunt het nieuwe afdeling van een werknemer tooa met behulp van een EGT niet verplaatsen.</li>
</ul>
</td>
</tr>
<tr>
<td>Denormalize in één entiteitstype</td>
<td>
<ul>
<li>U kunt alle met één aanvraag benodigde Hallo-gegevens ophalen.</li>
</ul>
</td>
<td>
<ul>
<li>Consistentie van dure toomaintain kan zijn als u tooupdate afdeling informatie (Hiermee vereist u tooupdate alle Hallo werknemers in een afdeling).</li>
</ul>
</td>
</tr>
</table>

Hoe u kiezen tussen deze opties en welke van Hallo-professionals en nadelen van de meest significante zijn afhankelijk van uw specifieke toepassingsscenario's. Bijvoorbeeld, hoe vaak u Wijzig afdeling entiteiten; moeten alle werknemers-query's meer afdelingen informatie Hallo; hoe dicht weet u toohello limieten voor schaalbaarheid van de partities of uw storage-account?  

### <a name="one-to-one-relationships"></a>-Op-een-relaties
Domeinmodellen kunnen-op-een-relaties tussen entiteiten bevatten. Als u een-op-een relatie in service tabel Hallo tooimplement moet, moet u ook kiezen hoe toolink twee gerelateerde entiteiten Hallo wanneer u tooretrieve ze beide nodig. Deze koppeling kan impliciete, op basis van een conventie in Hallo sleutelwaarden of expliciete worden door het opslaan van een koppeling in de vorm van Hallo **PartitionKey** en **RowKey** waarden in elke entiteit tooits gerelateerde entiteit. Gerelateerde entiteiten voor een beschrijving van de of Hallo moeten worden opgeslagen in dezelfde partitie Hallo, Zie de sectie Hallo [een-op-veel relaties](#one-to-many-relationships).  

Houd er rekening mee dat er zijn ook overwegingen bij de implementatie die, u tooimplement-op-een-relaties in de tabelservice Hallo leiden kunnen:  

* Verwerking van grote entiteiten (Zie voor meer informatie [grote entiteiten patroon](#large-entities-pattern)).  
* Toegangsbeheer implementeren (Zie voor meer informatie [beheren van toegang met Shared Access Signatures](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Deelnemen aan Hallo-client
Hoewel er manieren toomodel relaties in Hallo tabelservice zijn, moet u niet vergeet dat Hallo twee belangrijkste redenen voor het gebruik van de tabelservice Hallo schaalbaarheid en prestaties zijn. Als u dat u veel-relaties die een bedreiging Hallo prestaties en schaalbaarheid van uw oplossing vormen zijn modellering vindt, vraagt u uzelf dat als het benodigde toobuild Hallo alle relaties tussen gegevens in uw tabelontwerp voor een. U kunt kunnen toosimplify Hallo ontwerp worden en verbeteren Hallo schaalbaarheid en prestaties van uw oplossing als u toestaat dat de clienttoepassing alle benodigde joins uitvoeren.  

Bijvoorbeeld, hebt u een kleine tabellen die gegevens bevatten die niet vaak veranderen, kunt vervolgens u deze gegevens eenmaal ophalen en cache te plaatsen op Hallo-client. Dit kan voorkomen herhaalde interactie tooretrieve Hallo dezelfde gegevens. In de voorbeelden Hallo die we in deze handleiding hebt bekeken, is hello reeks afdelingen in een kleine organisatie waarschijnlijk toobe klein en wijzig zelden waardoor het een goede kandidaat voor de gegevens eenmaal in client-toepassing kan worden gedownload en cache als opzoeken van gegevens.  

### <a name="inheritance-relationships"></a>Relaties voor overname
Als u de clienttoepassing gebruikmaakt van een set klassen die deel van een relatie voor overname toorepresent bedrijfsentiteiten uitmaken, kunt u eenvoudig deze entiteiten in Hallo tabelservice bewaard. Bijvoorbeeld, u wellicht Hallo set klassen gedefinieerd in uw clienttoepassing te volgen waarbij **persoon** is een abstracte klasse.

![][3]

U kunt deze persistent maken exemplaren van Hallo twee concrete klassen in Hallo service van de tabel met één personentabel met entiteiten in die zijn opgemaakt als volgt:  

![][4]

Zie voor meer informatie over het werken met meerdere Entiteitstypen in dezelfde tabel in de clientcode Hallo Hallo sectie [werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types) verderop in deze handleiding. Dit vindt u voorbeelden van hoe toorecognize Hallo entiteitstype in clientcode.  

## <a name="table-design-patterns"></a>Ontwerppatronen voor tabel
U hebt een aantal uitgebreide informatie over hoe toooptimize uw tabel ontwerpen voor beide entiteitsgegevens op te halen met behulp van query's en voor het invoegen, bijwerken en verwijderen van entiteitsgegevens gezien in de vorige secties. Deze sectie beschrijft een aantal patronen geschikt voor gebruik met oplossingen voor tabel-service. Bovendien ziet u hoe u bepaalde Hallo problemen en verschillen die eerder in deze handleiding wordt geactiveerd op vrijwel kunt oplossen. Hallo volgende diagram geeft een overzicht van Hallo relaties tussen de verschillende patronen Hallo:  

![][5]

Hallo patroon kaart hierboven licht sommige relaties tussen patronen (blauw) en anti patronen (oranje) die in deze handleiding worden beschreven. Er zijn natuurlijk veel andere patronen die moeten overwogen worden. Een van de Hallo belangrijke scenario's voor tabel-Service is bijvoorbeeld toouse hello [gematerialiseerd weergave patroon](https://msdn.microsoft.com/library/azure/dn589782.aspx) van Hallo [opdracht Query verantwoordelijkheid scheiding (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) patroon.  

### <a name="intra-partition-secondary-index-pattern"></a>Intra-partitie secundaire index patroon
Opslaan van meerdere exemplaren van elke entiteit met behulp van verschillende **RowKey** waarden (in Hallo dezelfde partitie) tooenable snelle en efficiënte zoekacties en alternatieve sorteren orders met behulp van verschillende **RowKey** waarden. Updates tussen kopieën consistent kunnen worden gehouden met behulp van EGT.  

#### <a name="context-and-problem"></a>Context en probleem
Hallo tabelservice indexeert automatisch entiteiten met Hallo **PartitionKey** en **RowKey** waarden. Hierdoor kan een client toepassing tooretrieve een entiteit efficiënt gebruik maakt van deze waarden. Bijvoorbeeld, met Hallo tabelstructuur hieronder wordt weergegeven, een clienttoepassing kunt gebruiken een punt query tooretrieve een afzonderlijke werknemer entiteit met behulp van de naam van de afdeling Hallo en Hallo werknemer-id (Hallo **PartitionKey** en  **RowKey** waarden). Een client kan ook gesorteerd op werknemer-id binnen elke afdeling entiteiten ophalen.

![][6]

Als u wilt dat ook toobe kunnen toofind een werknemer entiteit gebaseerd op Hallo-waarde van een andere eigenschap, zoals e-mailadres, moet u een minder efficiënte partitie scan toofind een overeenkomst. Dit is omdat Hallo tabel-service geen secundaire indexen biedt. Er is bovendien geen optie toorequest een lijst met werknemers gesorteerd in een andere volgorde dan **RowKey** volgorde.  

#### <a name="solution"></a>Oplossing
toowork rond Hallo gebrek aan secundaire indexen, kunt u meerdere exemplaren van elke entiteit bij elk exemplaar met een andere opslaan **RowKey** waarde. Als u een entiteit met Hallo structuren hieronder opslaat, kunt u efficiënt werknemer entiteiten op basis van e-adres of de werknemer-id ophalen. voorvoegsel waarden voor Hallo Hallo **RowKey**, 'empid_' en 'email_' kunt u tooquery voor één werknemer of een bereik van werknemers met behulp van een bereik van e-mailadressen of werknemer-id's.  

![][7]

Hallo na twee filtercriteria (één opzoeken op basis van de werknemer-id en een opzoeken op basis van e-mailadres) Geef beide punt query's:  

* $filter = (PartitionKey eq 'Sales') en (RowKey eq 'empid_000223')  
* $filter = (PartitionKey eq 'Sales') en (RowKey eq 'email_jonesj@contoso.com')  

Als u een query voor een bereik van de werknemer entiteiten uitvoert, kunt u een bereik gesorteerd in volgorde van de werknemer-id of een bereik in e-mailadres volgorde gesorteerd op basis van een query uitvoert voor entiteiten met het juiste voorvoegsel in Hallo Hallo **RowKey**.  

* toofind alle Hallo werknemers in de afdeling verkoop Hallo met een werknemer-id in Hallo bereik 000100 too000199 gebruiken: $filter = (PartitionKey eq 'Sales') en (RowKey ge 'empid_000100') en (RowKey RP 'empid_000199')  
* alle werknemers in de afdeling verkoop Hallo Hallo met een e-mailadres begint met de Hallo toofind letter "a" gebruik: $filter = (PartitionKey eq 'Sales') en (RowKey ge 'email_a') en (RowKey lt 'email_b')  
  
  Houd er rekening mee dat Hallo filtersyntaxis gebruikt in de bovenstaande voorbeelden van Hallo uit Hallo tabelservice REST API, Zie voor meer informatie [Query entiteiten](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Table storage is relatief goedkope toouse Hallo kosten overhead voor het opslaan van dubbele gegevens mag geen groot belang. U moet echter altijd geëvalueerd Hallo kosten van het ontwerp op basis van de vereisten van uw verwachting benodigde opslag en alleen toevoegen dubbele entiteiten toosupport Hallo query's die de clienttoepassing wordt uitgevoerd.  
* Omdat Hallo secundaire index entiteiten worden opgeslagen in dezelfde partitie als de oorspronkelijke entiteiten Hallo hello, moet u ervoor zorgen dat u de schaalbaarheidsdoelen Hallo voor een afzonderlijke partitie niet overschrijden.  
* U kunt uw dubbele entiteiten consistent zijn met elkaar houden met behulp van EGTs tooupdate Hallo twee exemplaren van de entiteit Hallo moment. Dit betekent dat u alle exemplaren van een entiteit moet opslaan in Hallo dezelfde partitie. Zie voor meer informatie, Hallo sectie [entiteitstransacties met behulp van](#entity-group-transactions).  
* waarde die wordt gebruikt voor Hallo Hallo **RowKey** moet uniek zijn voor elke entiteit. Overweeg het gebruik van de samengestelde sleutel komt.  
* Numerieke waarden Hallo opvulling **RowKey** (bijvoorbeeld Hallo werknemer-id 000223), kunt sorteren en filteren op basis van hoofdletters en de ondergrenzen corrigeren.  
* Hoeft u niet per se tooduplicate alle Hallo-eigenschappen van uw entiteit. Bijvoorbeeld, als hello query's die e-lookup Hallo entiteiten met Hallo adres uit Hallo **RowKey** nooit moet de leeftijd van de werknemer hello, deze entiteiten kunnen Hallo structuur te volgen:

![][8]

* Het is doorgaans beter toostore dubbele gegevens en ervoor te zorgen dat u alle Hallo-gegevens die u nodig hebt met één query kunt ophalen, dan toouse één query toolocate een entiteit en een andere toolookup Hallo gegevens vereist.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Dit patroon gebruiken wanneer u de clienttoepassing moet tooretrieve entiteiten met een aantal verschillende sleutels wanneer de client tooretrieve entiteiten in verschillende sorteervolgorde moet en waar u elke entiteit met een aantal unieke waarden kunt identificeren. U moet echter zeker limieten voor schaalbaarheid van Hallo partitie niet te overschrijden wanneer u de entiteit zoekacties met behulp van verschillende Hallo uitvoert **RowKey** waarden.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Secundaire tussen partitioneren van index patroon](#inter-partition-secondary-index-pattern)
* [Samengestelde sleutel patroon](#compound-key-pattern)
* [Entiteit groep transacties](#entity-group-transactions)
* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Secundaire tussen partitioneren van index patroon
Opslaan van meerdere exemplaren van elke entiteit met behulp van verschillende **RowKey** waarden in afzonderlijke partities of in afzonderlijke tabellen tooenable snelle en efficiënte zoekacties en alternatieve sorteervolgorde met behulp van verschillende **RowKey**waarden.  

#### <a name="context-and-problem"></a>Context en probleem
Hallo tabelservice indexeert automatisch entiteiten met Hallo **PartitionKey** en **RowKey** waarden. Hierdoor kan een client toepassing tooretrieve een entiteit efficiënt gebruik maakt van deze waarden. Bijvoorbeeld, met Hallo tabelstructuur hieronder wordt weergegeven, een clienttoepassing kunt gebruiken een punt query tooretrieve een afzonderlijke werknemer entiteit met behulp van de naam van de afdeling Hallo en Hallo werknemer-id (Hallo **PartitionKey** en  **RowKey** waarden). Een client kan ook gesorteerd op werknemer-id binnen elke afdeling entiteiten ophalen.  

![][9]

Als u wilt dat ook toobe kunnen toofind een werknemer entiteit gebaseerd op Hallo-waarde van een andere eigenschap, zoals e-mailadres, moet u een minder efficiënte partitie scan toofind een overeenkomst. Dit is omdat Hallo tabel-service geen secundaire indexen biedt. Er is bovendien geen optie toorequest een lijst met werknemers gesorteerd in een andere volgorde dan **RowKey** volgorde.  

U bent anticiperen op een zeer groot aantal transacties tegen deze entiteiten en toominimize Hallo risico Hallo tabelservice beperking van de client wilt.  

#### <a name="solution"></a>Oplossing
toowork rond Hallo gebrek aan secundaire indexen, kunt u meerdere exemplaren van elke entiteit met het gebruik van elk exemplaar andere opslaan **PartitionKey** en **RowKey** waarden. Als u een entiteit met Hallo structuren hieronder opslaat, kunt u efficiënt werknemer entiteiten op basis van e-adres of de werknemer-id ophalen. voorvoegsel waarden voor Hallo Hallo **PartitionKey**, 'empid_' en 'email_', kunt u tooidentify die index die u wilt dat toouse voor een query.  

![][10]

Hallo na twee filtercriteria (één opzoeken op basis van de werknemer-id en een opzoeken op basis van e-mailadres) Geef beide punt query's:  

* $filter = (PartitionKey eq ' empid_Sales') en (RowKey eq '000223')
* $filter = (PartitionKey eq ' email_Sales') en (RowKey eq 'jonesj@contoso.com')  

Als u een query voor een bereik van de werknemer entiteiten uitvoert, kunt u een bereik gesorteerd in volgorde van de werknemer-id of een bereik in e-mailadres volgorde gesorteerd op basis van een query uitvoert voor entiteiten met het juiste voorvoegsel in Hallo Hallo **RowKey**.  

* alle werknemers in Hallo toofind Hallo verkoopafdeling met een werknemer-id in Hallo bereik **000100** te**000199** in gebruik door werknemers-id volgorde gesorteerd: $filter = (PartitionKey eq ' empid_Sales') en (RowKey ge ' 000100') en (RowKey RP '000199')  
* toofind alle Hallo werknemers in Hallo verkoopafdeling met een e-mailadres dat begint met "a" gesorteerde in e-mailadres volgorde van gebruik: $filter = (PartitionKey eq ' email_Sales') en (RowKey ge "a") en (RowKey lt "b")  

Houd er rekening mee dat Hallo filtersyntaxis gebruikt in de bovenstaande voorbeelden van Hallo uit Hallo tabelservice REST API, Zie voor meer informatie [Query entiteiten](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Kunt u uw dubbele entiteiten uiteindelijk consistent is met elkaar via Hallo [uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern) toomaintain Hallo primaire en secundaire index entiteiten.  
* Table storage is relatief goedkope toouse Hallo kosten overhead voor het opslaan van dubbele gegevens mag geen groot belang. U moet echter altijd geëvalueerd Hallo kosten van het ontwerp op basis van de vereisten van uw verwachting benodigde opslag en alleen toevoegen dubbele entiteiten toosupport Hallo query's die de clienttoepassing wordt uitgevoerd.  
* waarde die wordt gebruikt voor Hallo Hallo **RowKey** moet uniek zijn voor elke entiteit. Overweeg het gebruik van de samengestelde sleutel komt.  
* Numerieke waarden Hallo opvulling **RowKey** (bijvoorbeeld Hallo werknemer-id 000223), kunt sorteren en filteren op basis van hoofdletters en de ondergrenzen corrigeren.  
* Hoeft u niet per se tooduplicate alle Hallo-eigenschappen van uw entiteit. Bijvoorbeeld, als hello query's die e-lookup Hallo entiteiten met Hallo adres uit Hallo **RowKey** nooit moet de leeftijd van de werknemer hello, deze entiteiten kunnen Hallo structuur te volgen:
  
  ![][11]
* Is het doorgaans beter toostore dubbele gegevens en ervoor te zorgen dat u alle Hallo-gegevens die u nodig hebt met één query dan een entiteit met behulp van toouse één query toolocate Hallo secundaire index kunt ophalen en een andere toolookup vereiste gegevens in de primaire index Hallo Hallo.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Dit patroon gebruiken wanneer u de clienttoepassing moet tooretrieve entiteiten met een aantal verschillende sleutels wanneer de client tooretrieve entiteiten in verschillende sorteervolgorde moet en waar u elke entiteit met een aantal unieke waarden kunt identificeren. Dit patroon gebruiken als u wilt dat tooavoid Hallo partitie schaalbaarheidslimieten van meer dan wanneer u de entiteit zoekacties met behulp van verschillende Hallo uitvoert **RowKey** waarden.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern)  
* [Intra-partitie secundaire index patroon](#intra-partition-secondary-index-pattern)  
* [Samengestelde sleutel patroon](#compound-key-pattern)  
* [Entiteit groep transacties](#entity-group-transactions)  
* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Uiteindelijk consistent transacties patroon
Uiteindelijk consistent gedrag over grenzen van partities of opslag system grenzen inschakelen met behulp van Azure wachtrijen.  

#### <a name="context-and-problem"></a>Context en probleem
EGTs inschakelen atomische transacties tussen meerdere entiteiten die Hallo delen dezelfde partitiesleutel. Voor betere prestaties en schaalbaarheid u besluiten toostore entiteiten met vereisten voor consistentie in afzonderlijke partities of in een afzonderlijke opslagsysteem: in een dergelijk scenario u EGTs toomaintain consistentie niet gebruiken. Stel, hebt u een vereiste toomaintain uiteindelijke consistentie tussen:  

* Entiteiten die zijn opgeslagen in twee verschillende partities in dezelfde tabel in verschillende tabellen in verschillende opslagaccounts Hallo.  
* Een entiteit die zijn opgeslagen in Hallo tabel-service en een blob in Hallo opgeslagen Blob-service.  
* Een entiteit in de tabelservice hello en een bestand opgeslagen in een bestandssysteem.  
* Een entiteit opslaan in Hallo tabelservice nog geïndexeerd met hello Azure Search-service.  

#### <a name="solution"></a>Oplossing
U kunt een oplossing die zorgt voor uiteindelijke consistentie tussen twee of meer partities of opslagsystemen implementeren met behulp van Azure wachtrijen.
tooillustrate dit benadert, wordt ervan uitgegaan dat u hebt een vereiste toobe kunnen tooarchive oude werknemer entiteiten. Oude werknemer entiteiten zelden worden opgevraagd en van alle activiteiten die betrekking op de huidige werknemers hebben moeten worden uitgesloten. tooimplement deze vereiste voor het opslaan van de actieve werknemers in Hallo **huidige** tabel en oude werknemers in Hallo **archief** tabel. Een werknemer wilt archiveren, moet u toodelete Hallo entiteit van de Hallo **huidige** tabel en voeg Hallo entiteit toohello **archief** tabel, maar niet gebruiken een tooperform EGT deze twee bewerkingen. tooavoid hello risico dat een fout zorgt ervoor een entiteit tooappear in beide of geen van beide tabellen dat, Hallo archiveringsbewerking moet uiteindelijk consistent zijn. Hallo volgende reeksdiagram geeft een overzicht van Hallo stappen in deze bewerking. Meer details is opgegeven voor de uitzondering paden in Hallo tekst na.  

![][12]

Een client initieert Hallo archiveringsbewerking door het plaatsen van een bericht op een Azure-wachtrij in dit voorbeeld tooarchive werknemer #456. Een werkrol worden opgevraagd Hallo wachtrij voor nieuwe berichten; Wanneer er een is gevonden, wordt het Hallo-bericht gelezen en wordt een verborgen kopie op Hallo wachtrij. een kopie van de entiteit Hallo Hallo werkrol vervolgens haalt uit Hallo **huidige** tabel, voegt u een kopie in Hallo **archief** tabel en verwijderingen Hallo oorspronkelijke van Hallo **huidige**tabel. Ten slotte, als er geen fouten uit de vorige stappen Hallo zijn, verwijdert Hallo werkrol verborgen het Hallo-bericht uit Hallo wachtrij.  

Stap 4 wordt in dit voorbeeld Hallo werknemer ingevoegd in Hallo **archief** tabel. Het kan Hallo werknemer tooa blob in Hallo Blob-service of een bestand toevoegen in een bestandssysteem.  

#### <a name="recovering-from-failures"></a>Herstellen van fouten
Het is belangrijk dat bewerkingen in stappen Hallo **4** en **5** moet *idempotent* voor het geval de werkrol hello toorestart Hallo archiveringsbewerking. Als u de tabelservice Hallo voor stap **4** moet u een bewerking "invoegen of vervangen"; voor de stap **5** moet u een ' verwijderen als bestaat ' bewerking in Hallo-clientbibliotheek die u gebruikt. Als u een andere opslagsysteem gebruikt, moet u een geschikte idempotent-bewerking.  

Als de werkrol Hallo nooit stap voltooit **6**, vervolgens nadat er een time-out voor het Hallo-bericht opnieuw wordt weergegeven in de wachtrij Hallo klaar te maken voor Hallo worker-rol tootry tooreprocess deze. Hallo-werkrol kunt controleren hoe vaak een bericht op Hallo wachtrij is gelezen en, indien nodig, is een 'poison'-bericht voor onderzoek door ze tooa vlag wachtrij scheiden. Voor meer informatie over het lezen van berichten in wachtrij plaatsen en het controleren van Hallo in wachtrij count, Zie [berichten ophalen](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Er zijn fouten van Hallo Table en Queue-services zijn tijdelijke fouten en uw clienttoepassing geschikte opnieuw logica toohandle bevatten ze.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Deze oplossing biedt geen voor het isoleren van de transactie. Een client kan bijvoorbeeld de Hallo lezen **huidige** en **archief** tabellen wanneer de werkrol Hallo werd tussen stappen **4** en **5**, en zien een inconsistente weergave van Hallo-gegevens. Houd er rekening mee dat Hallo gegevens zal consistent uiteindelijk.  
* U moet ervoor dat de stappen 4 en 5 idempotent in volgorde tooensure uiteindelijke consistentie.  
* Hallo-oplossing kunt u met behulp van meerdere wachtrijen en rolinstanties worker schalen.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon als u wilt tooguarantee uiteindelijke consistentie tussen entiteiten die aanwezig zijn in verschillende partities of tabellen. U kunt dit patroon tooensure uiteindelijke consistentie voor bewerkingen Hallo tabelservice als Hallo Blob-service en andere Azure Storage-gegevensbronnen zoals database of Hallo bestandssysteem uitbreiden.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Entiteit groep transacties](#entity-group-transactions)  
* [Samenvoegen of vervangen](#merge-or-replace)  

> [!NOTE]
> Als de isolatie van de transactie belangrijk tooyour oplossing is, moet u opnieuw ontwerpen van uw tooenable tabellen u toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Index entiteiten patroon
Onderhouden entiteiten tooenable efficiënt zoekacties in de index die lijsten van entiteiten retourneren.  

#### <a name="context-and-problem"></a>Context en probleem
Hallo tabelservice indexeert automatisch entiteiten met Hallo **PartitionKey** en **RowKey** waarden. Hierdoor kan een client toepassing tooretrieve een entiteit efficiënt gebruik maakt van een punt-query. Bijvoorbeeld met behulp van Hallo tabelstructuur hieronder wordt weergegeven, een clienttoepassing kunt efficiënt een afzonderlijke werknemer entiteit ophalen met behulp van de naam van de afdeling Hallo en Hallo werknemer-id (Hallo **PartitionKey** en **RowKey** ).  

![][13]

Als u wilt ook toobe kunnen tooretrieve een lijst met entiteiten van de werknemer op basis van Hallo-waarde van een ander niet-unieke eigenschap, zoals hun achternaam, moet u een minder efficiënte partitie toofind komt overeen met scan in plaats van met behulp van een index toolook ze rechtstreeks omhoog. Dit is omdat Hallo tabel-service geen secundaire indexen biedt.  

#### <a name="solution"></a>Oplossing
tooenable lookup op achternaam met de structuur van de entiteit Hallo hierboven, moet u een lijst met werknemer-id's onderhouden. Als u wilt dat tooretrieve Hallo werknemer entiteiten met een bepaalde achternaam, zoals Peeters, moet u eerst Hallo lijst met werknemer-id vinden voor werknemers met Jones als hun achternaam en vervolgens deze werknemer entiteiten worden opgehaald. Er zijn drie manieren voor het opslaan van Hallo lijsten met werknemer-id's:  

* Blob storage gebruiken.  
* Maak index entiteiten in dezelfde partitie als Hallo werknemer entiteiten Hallo.  
* Maak index entiteiten in een afzonderlijke partitie of de tabel.  

<u>Optie #1: Gebruik blob storage</u>  

Voor de eerste optie hello, u een blob voor elke unieke achternaam en in elke blob-store een lijst maken van Hallo **PartitionKey** (afdeling) en **RowKey** waarden voor werknemers die in dat laatste hebben (werknemer-id) de naam. Bij het toevoegen of verwijderen van een werknemer moet u ervoor zorgen dat Hallo-inhoud van de relevante Hallo-blob uiteindelijk consistent is met de Hallo werknemer entiteiten is.  

<u>Optie #2:</u> Create index entiteiten in dezelfde partitie Hallo  

Gebruik voor Hallo tweede optie, index-entiteiten die Hallo volgt gegevens opslaan:  

![][14]

Hallo **EmployeeIDs** eigenschap bevat een lijst van de werknemer-id's voor werknemers met Hallo achternaam opgeslagen in Hallo **RowKey**.  

Hallo volgende stappen wordt uitgelegd u volgen moet wanneer u een nieuwe werknemer toevoegen wilt als u van de tweede optie Hallo gebruikmaakt Hallo-proces. In dit voorbeeld toevoegen we een werknemer met Id 000152 en een achternaam Jones in de afdeling verkoop Hallo:  

1. Ophalen van Hallo index entiteit met een **PartitionKey** waarde 'Verkoop' en Hallo **RowKey** waarde "Jones." Hallo ETag van deze entiteit toouse opslaan in stap 2.  
2. Maken van een entiteit groep transactie (dat wil zeggen, een batchbewerking) dat wordt ingevoegd Hallo nieuwe werknemer entiteit (**PartitionKey** waarde 'Verkoop' en **RowKey** waarde '000152'), en updates Hallo index entiteit ( **PartitionKey** waarde 'Verkoop' en **RowKey** waarde 'Jones') door toe te voegen Hallo id toohello lijst met nieuwe werknemers in Hallo EmployeeIDs veld. Zie voor meer informatie over entiteit groepstransacties [entiteit groepstransacties](#entity-group-transactions).  
3. Als Hallo entiteit groep transactie mislukt vanwege een optimistische gelijktijdigheid-fout (iemand anders is zojuist gewijzigd Hallo index entiteit), moet u toostart via bij stap 1 opnieuw.  

U kunt een soortgelijke benadering toodeleting een werknemer gebruiken als u van de tweede optie Hallo gebruikmaakt. Wijzigen van de achternaam van een werknemer is iets ingewikkelder omdat moet u een entiteit groep transactie die updates drie entiteiten tooexecute: werknemer entiteit en Hallo index entiteit voor de oude achternaam Hallo Hallo index entiteit voor de nieuwe achternaam Hallo Hallo. Voordat u wijzigingen aanbrengt in volgorde tooretrieve Hallo ETag waarden die u gebruikt optimistische gelijktijdigheid van tooperform Hallo updates vervolgens kunt gebruiken, moet u elke entiteit ophalen.  

Hallo volgende stappen wordt uitgelegd u volgen moet wanneer u toolook van alle Hallo werknemers met een bepaalde achternaam in een afdeling nodig als u van de tweede optie Hallo gebruikmaakt Hallo-proces. In dit voorbeeld zijn er alle Hallo werknemers met achternaam Jones in de afdeling verkoop Hallo opzoeken:  

1. Ophalen van Hallo index entiteit met een **PartitionKey** waarde 'Verkoop' en Hallo **RowKey** waarde "Jones."  
2. Hallo-lijst van de werknemer-id's in Hallo EmployeeIDs veld parseren.  
3. Als u meer informatie over elk van deze werknemers (zoals hun e-mailadressen), ophalen elk Hallo werknemer entiteiten met **PartitionKey** waarde 'Verkoop' en **RowKey** waarden van Hallo-lijst van werknemers die u hebt verkregen in stap 2.  

<u>Optie #3:</u> index entiteiten in een afzonderlijke partitie of een tabel maken  

Gebruik voor Hallo derde optie, index-entiteiten die Hallo volgt gegevens opslaan:  

![][15]

Hallo **EmployeeIDs** eigenschap bevat een lijst van de werknemer-id's voor werknemers met Hallo achternaam opgeslagen in Hallo **RowKey**.  

Hallo derde optie, u EGTs toomaintain consistentie niet gebruiken omdat Hallo index entiteiten in een afzonderlijke partitie van Hallo werknemer entiteiten. U moet ervoor zorgen dat Hallo index entiteiten uiteindelijk consistent is met de Hallo werknemer entiteiten.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Deze oplossing vereist ten minste twee query's tooretrieve overeenkomende entiteiten: één tooquery Hallo index entiteiten tooobtain Hallo lijst met **RowKey** waarden en vervolgens een query tooretrieve elke entiteit in de lijst Hallo.  
* Gezien het feit dat een afzonderlijke entiteit heeft een maximale grootte van 1 MB, optie #2 en de optie #3 in Hallo oplossing wordt ervan uitgegaan dat Hallo lijst met werknemer-id's voor een bepaalde achternaam is nooit groter dan 1 MB. Als Hallo-lijst van de werknemer-id's waarschijnlijk toobe groter is dan 1 MB groot is, gebruik van optie #1 en Hallo indexgegevens opslaan in blob-opslag.  
* Als u de optie #2 gebruikt moet (met behulp van EGTs toohandle toevoegen en verwijderen van werknemers en het wijzigen van de achternaam van een werknemer) u nagaan of Hallo volume van transacties Hallo limieten voor schaalbaarheid in een bepaalde partitie wordt benaderen. Als dit Hallo geval is, moet u rekening houden met een uiteindelijk consistent oplossing (optie &#1; of optie #3) die gebruikmaakt van wachtrijen toohandle Hallo update aanvraagt en kunt u toostore uw index entiteiten in een afzonderlijke partitie van Hallo werknemer entiteiten.  
* Optie #2 in deze oplossing wordt ervan uitgegaan dat u toolook binnen een afdeling op achternaam wilt: u kunt bijvoorbeeld tooretrieve een lijst met werknemers met een achternaam Jones in de afdeling verkoop Hallo. Als u kunnen toolook toobe van alle Hallo werknemers met een achternaam Jones binnen de hele organisatie hello wilt, optie #1 of optie #3 gebruiken.
* U kunt een oplossing op basis van wachtrijen die zorgt voor uiteindelijke consistentie implementeren (Zie Hallo [uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern) voor meer informatie).  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon als u wilt dat een aantal entiteiten dat alle een gemeenschappelijke eigenschapswaarde, zoals alle werknemers met Hallo achternaam Jones delen toolookup.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Samengestelde sleutel patroon](#compound-key-pattern)  
* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern)  
* [Entiteit groep transacties](#entity-group-transactions)  
* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Denormalization patroon
Gerelateerde gegevens samen in een enkele entiteit tooenable combineren tooretrieve u alle gegevens die u met een query één punt moet Hallo.  

#### <a name="context-and-problem"></a>Context en probleem
In een relationele database, moet u doorgaans tooremove gegevensontdubbeling, wat resulteert in query's die gegevens uit meerdere tabellen ophalen normaliseren. Als u uw gegevens in Azure-tabellen normaliseren, moet u meerdere retouren van Hallo client toohello server tooretrieve uw gerelateerde gegevens maken. Bijvoorbeeld, met de structuur van de tabel Hallo hieronder u moet twee afronden reizen tooretrieve Hallo details voor een afdeling: één toofetch Hallo afdeling entiteit die van de manager van het Hallo-id en vervolgens een andere aanvraag toofetch Hallo van manager details in een werknemer bevat de entiteit.  

![][16]

#### <a name="solution"></a>Oplossing
In plaats van het Hallo-gegevens worden opgeslagen in twee afzonderlijke entiteiten, denormalize Hallo gegevens en bewaar een kopie van de details van Hallo manager op Hallo afdeling entiteit. Bijvoorbeeld:  

![][17]

Met de afdeling entiteiten met deze eigenschappen worden opgeslagen, kunt u nu alle Hallo details, moet u over een afdeling in een query punt ophalen.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Er is enige kosten overhead die is gekoppeld aan twee keer sommige gegevens op te slaan. Hallo prestatievoordelen (die voortvloeien uit minder aanvragen toohello storage-service) doorgaans belangrijker is dan Hallo marginale toename opslagkosten (en deze kosten is gedeeltelijk gecompenseerd door een vermindering van het aantal transacties Hallo u toofetch Hallo informatie is vereist van een afdeling).  
* Hallo consistentie van Hallo twee entiteiten die informatie over managers opslaat, moet u onderhouden. U kunt verwerkt Hallo consistentie probleem met behulp van EGTs tooupdate meerdere entiteiten in één transactie atomic: in dit geval Hallo afdeling entiteits- en Hallo werknemer entiteit voor Hallo afdelingsmanager worden opgeslagen in Hallo dezelfde partitie.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
U kunt dit patroon vaak toolook gerelateerde informatie. Dit patroon vermindert Hallo aantal query's voor die de client moet aanbrengen tooretrieve Hallo gegevens vereist.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Samengestelde sleutel patroon](#compound-key-pattern)  
* [Entiteit groep transacties](#entity-group-transactions)  
* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Samengestelde sleutel patroon
Gebruik samengestelde **RowKey** waarden tooenable een client toolookup gerelateerde gegevens met een query één punt.  

#### <a name="context-and-problem"></a>Context en probleem
In een relationele database, is het erg natuurlijke toouse joins in query's tooreturn soorten gegevens toohello client in één query gerelateerd. U kunt bijvoorbeeld Hallo werknemer-id toolook van een lijst van gerelateerde entiteiten die prestaties bevatten en gegevens voor die werknemer bekijken.  

Stel dat u bij het opslaan van entiteiten van de werknemer in service Hallo-tabel met Hallo structuur te volgen:  

![][18]

Moet u ook toostore historische gegevens over tooreviews en prestaties voor elk jaar Hallo werknemer heeft gewerkt voor uw organisatie en u toobe kunnen tooaccess moet deze informatie per jaar. Een optie toocreate is een andere tabel waarmee entiteiten worden opgeslagen met Hallo structuur te volgen:  

![][19]

Merk op dat met deze benadering u besluiten tooduplicate sommige gegevens (zoals de voornaam en achternaam) in de nieuwe entiteit tooenable hello tooretrieve u uw gegevens met één aanvraag. U kan niet echter sterke consistentie onderhouden omdat u een EGT tooupdate Hallo twee entiteiten moment niet kan gebruiken.  

#### <a name="solution"></a>Oplossing
Een nieuwe entiteitstype opslaan in de oorspronkelijke tabel met behulp van de entiteiten met Hallo structuur te volgen:  

![][20]

U ziet hoe Hallo **RowKey** nu een samengestelde sleutel bestaat uit Hallo werknemer-id en het Hallo jaar van Hallo revisie gegevens waarmee u tooretrieve Hallo van werknemer prestaties en het controleren van gegevens met één aanvraag voor één entiteit.  

Hallo volgende voorbeeld bevat een overzicht van hoe u alle Hallo revisie gegevens kunt ophalen voor een bepaalde werknemer (zoals werknemer 000123 in de afdeling verkoop Hallo):  

$filter = (PartitionKey eq 'Sales') en (RowKey ge 'empid_000123') en (RowKey lt 'empid_000124') & $select = RowKey, beoordeling door Manager, beoordeling van de Peer, opmerkingen  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Moet u een geschikte scheidingsteken dat het eenvoudig tooparse hello maakt **RowKey** waarde: bijvoorbeeld **000123_2012**.  
* U ook deze entiteit opslaat in dezelfde partitie als andere entiteiten met verwante gegevens voor Hallo Hallo dezelfde werknemer, wat betekent dat u sterke consistentie voor EGTs toomaintain kunt gebruiken.
* U moet overwegen hoe vaak u een query uit op Hallo gegevens toodetermine of dit patroon geschikt is.  Bijvoorbeeld als u toegang tot gegevens controleren zelden Hallo en Hallo belangrijkste werknemersgegevens vaak die u ze als afzonderlijke entiteiten houden moet.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon wanneer u toostore een moet of meer entiteiten die query u vaak gerelateerde.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Entiteit groep transacties](#entity-group-transactions)  
* [Werken met heterogene Entiteitstypen](#working-with-heterogeneous-entity-types)  
* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Patroon voor logboekbestand staart
Hallo ophalen  *n*  tooa partitie entiteiten meest recent toegevoegd met behulp van een **RowKey** waarde die in omgekeerde datum en tijd volgorde worden gesorteerd.  

#### <a name="context-and-problem"></a>Context en probleem
Een algemene vereiste is niet kunnen tooretrieve Hallo meest recent gemaakte entiteiten, bijvoorbeeld Hallo tien meest recente onkosten claims ingediend door een werknemer zijn. Tabel ondersteuning vraagt een **$top** bewerking tooreturn Hallo eerst query  *n*  entiteiten uit een set: Er is geen equivalent query bewerking tooreturn Hallo laatste n entiteiten in een set.  

#### <a name="solution"></a>Oplossing
Store Hallo entiteiten met een **RowKey** dat natuurlijk sorteren in omgekeerde volgorde datum/tijd volgorde door gebruik te maken zodat de meest recente item Hallo altijd Hallo eerste certificaat in het Hallo-tabel.  

Bijvoorbeeld: toobe kunnen tooretrieve Hallo tien meest recente onkosten claims die zijn ingediend door een werknemer, kunt u de waarde van een omgekeerde maatstreepjes afgeleid van Hallo huidige datum en tijd. Hallo volgende C# codevoorbeeld ziet eenrichtingssessie toocreate een geschikte waarde 'omgekeerde ticks' voor een **RowKey** die sorteren van de meest recente toohello Hallo oudste:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

U kunt terug met behulp van de volgende code Hallo datum-tijdwaarde voor toohello krijgen:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

Hallo tabelquery ziet er als volgt:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* U krijgt een Hallo omgekeerde maatstreepjes waarde met nullen toonaangevende tooensure Hallo tekenreekswaarde sorteert zoals verwacht.  
* U moet rekening houden met de schaalbaarheidsdoelen Hallo op Hallo niveau van een partitie. Wees voorzichtig hotspot partities niet maken.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon wanneer moet u tooaccess entiteiten in volgorde van de omgekeerde datum/tijd of wanneer u tooaccess Hallo meest recent moet toegevoegd entiteiten.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Toevoegen / antivirusprogramma patroon toevoegen](#prepend-append-anti-pattern)  
* [Entiteiten ophalen](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Patroon voor grote volumes verwijderen
Hallo verwijderen van een groot aantal entiteiten inschakelen door het opslaan van alle Hallo-entiteiten voor gelijktijdige verwijdering in hun eigen afzonderlijke tabel. u verwijderen Hallo entiteiten door Hallo tabel te verwijderen.  

#### <a name="context-and-problem"></a>Context en probleem
Veel toepassingen Verwijder oude gegevens die niet langer de toepassing van de client beschikbare tooa toobe moet of die toepassing hello tooanother opslagmedium is gearchiveerd. U doorgaans dergelijke gegevens identificeren met een datum: er bijvoorbeeld voor een vereiste toodelete-records van alle aanmeldingsaanvragen voor die meer dan 60 dagen oud.  

Een mogelijke ontwerp is toouse Hallo datum en tijd van Hallo aanmeldingsaanvraag in Hallo **RowKey**:  

![][21]

Deze aanpak voorkomt partitie hotspots omdat de toepassing hello kan invoegen en verwijderen van aanmelding entiteiten voor elke gebruiker in een afzonderlijke partitie. Echter mogelijk is deze benadering kostbare tijd in beslag nemen als u een groot aantal entiteiten hebt omdat u eerst tooperform moet een tabel scannen in volgorde tooidentify alle Hallo entiteiten toodelete en vervolgens moet u elke oude entiteit verwijderen. Houd er rekening mee dat u het aantal retouren toohello server vereist toodelete Hallo oude entiteiten Hallo verkleinen kunt door meerdere delete-aanvragen in EGTs batchverwerking.  

#### <a name="solution"></a>Oplossing
Een afzonderlijke tabel gebruiken voor elke dag van aanmeldingspogingen. U kunt Hallo entiteit ontwerp hierboven tooavoid hotspots entiteiten invoegen en verwijderen van oude entiteiten is nu gewoon een vraag van het verwijderen van één tabel elke dag (een enkele opslagbewerking) in plaats van zoeken en verwijderen van honderden of duizenden afzonderlijke aanmelding entiteiten elke dag.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Uw ontwerp biedt ondersteuning voor andere manieren Hallo gegevens zoals het opzoeken van specifieke entiteiten, koppelen aan andere gegevens of genereren verzamelde gegevens zullen worden gebruikt door uw toepassing?  
* Uw ontwerp hotspots voorkomen tijdens het invoegen van nieuwe entiteiten  
* Verwacht een vertraging optreden als u wilt dat tooreuse Hallo dezelfde tabelnaam na het verwijderen. Het is beter tooalways unieke Tabelnamen gebruiken.  
* Verwachten dat sommige beperking wanneer u eerst een nieuwe tabel terwijl Hallo tabelservice hello toegangspatronen leert en Hallo partities over knooppunten verdeelt. U moet bepalen hoe vaak toocreate nieuwe tabellen.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Dit patroon gebruiken wanneer u een groot aantal entiteiten die u op Hallo verwijderen moet hetzelfde moment.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Entiteit groep transacties](#entity-group-transactions)
* [Entiteiten wijzigen](#modifying-entities)  

### <a name="data-series-pattern"></a>Patroon van de reeks gegevens
Store voltooid gegevensreeksen in een enkele entiteit toominimize Hallo aantal aanvragen die u aanbrengt.  

#### <a name="context-and-problem"></a>Context en probleem
Een gebruikelijk scenario is voor een toepassing toostore een reeks vereiste gegevens dat doorgaans tooretrieve in één keer. Uw toepassing kan bijvoorbeeld hoeveel elke werknemer elk uur IM-berichten vastleggen en gebruik vervolgens deze informatie tooplot hoeveel berichten elke gebruiker worden verzonden via Hallo voorgaande 24 uur. Een ontwerp mogelijk toostore 24 entiteiten voor elke werknemer:  

![][22]

Bij dit ontwerp kunt u eenvoudig vinden en Hallo entiteit tooupdate voor elke werknemer bijwerken als de toepassing hello aantalwaarde voor tooupdate Hallo-bericht moet. Echter tooretrieve Hallo informatie tooplot een grafiek van de activiteit Hallo voor Hallo voorafgaande 24 uur, moet u 24 entiteiten ophalen.  

#### <a name="solution"></a>Oplossing
Ontwerp met een aantal afzonderlijke eigenschap toostore Hallo-berichten te volgen voor elk uur hello gebruiken:  

![][23]

Bij dit ontwerp kunt u een aantal samenvoegen bewerking tooupdate Hallo berichten voor een werknemer voor een specifiek uur. U kunt nu alle benodigde tooplot Hallo grafiek met behulp van een aanvraag voor een enkele entiteit Hallo-gegevens ophalen.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Als de volledige reeks past niet in één entiteit (een entiteit kan hebben eigenschappen too252), gebruikt u een alternatieve gegevensarchief, zoals een blob.  
* Als u meerdere clients tegelijkertijd bijwerken van een entiteit hebt, moet u toouse hello **ETag** tooimplement optimistische gelijktijdigheid. Als u veel clients hebt, kunt u hoge conflicten ondervinden.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon wanneer u tooupdate nodig hebt en een gegevensreeks die zijn gekoppeld aan een afzonderlijke entiteit ophalen.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Grote entiteiten patroon](#large-entities-pattern)  
* [Samenvoegen of vervangen](#merge-or-replace)  
* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern) (als u Hallo gegevensreeks in een blob opslaat)  

### <a name="wide-entities-pattern"></a>Wide entiteiten patroon
Gebruik van meerdere fysieke entiteiten toostore logische entiteiten met meer dan 252 eigenschappen.  

#### <a name="context-and-problem"></a>Context en probleem
Een afzonderlijke entiteit kan maximaal 252 eigenschappen (met uitzondering van de verplichte Systeemeigenschappen Hallo) en kan niet meer dan 1 MB aan gegevens opslaan in totaal. In een relationele database, doorgaans krijgt u ronde beperkingen met betrekking tot Hallo grootte van een rij bij het toevoegen van een nieuwe tabel en een 1-op-1-relatie tussen deze twee afdwingen.  

#### <a name="solution"></a>Oplossing
Hallo tabel-service gebruikt, kunt u meerdere entiteiten toorepresent een object één grote bedrijven met meer dan 252 eigenschappen opslaan. Bijvoorbeeld, als u wilt dat een aantal Hallo IM berichten die worden verzonden door elke werknemer voor Hallo afgelopen 365 dagen toostore, kunt u gebruiken Hallo ontwerp die gebruikmaakt van twee entiteiten met verschillende schema's te volgen:  

![][24]

U kunt een EGT gebruiken als u een wijziging die moet worden bijgewerkt beide entiteiten tookeep ze met elkaar gesynchroniseerd toomake nodig. Anders kunt u een aantal van één samenvoegen bewerking tooupdate Hallo berichten voor een specifieke dag. alle gegevens voor een afzonderlijke werknemer moet u beide entiteiten, kunt u doen met twee efficiënte aanvragen die gebruikmaken van beide ophalen Hallo tooretrieve een **PartitionKey** en een **RowKey** waarde.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Bij het ophalen van een volledige logische entiteit ten minste twee opslagtransacties omvat: één tooretrieve fysieke entiteit.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Gebruik dit patroon wanneer nodig toostore entiteiten waarvan de grootte van of het aantal eigenschappen overschrijdt de Hallo limieten voor een afzonderlijke entiteit in Hallo Tabelservice.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Entiteit groep transacties](#entity-group-transactions)
* [Samenvoegen of vervangen](#merge-or-replace)

### <a name="large-entities-pattern"></a>Grote entiteiten patroon
Gebruik blob storage toostore grote eigenschapswaarden.  

#### <a name="context-and-problem"></a>Context en probleem
Een afzonderlijke entiteit kan niet meer dan 1 MB aan gegevens opslaan in totaal. Als een of meer van de eigenschappen van uw waarden zijn waardoor de totale grootte van uw entiteit tooexceed Hallo deze waarde opslaat, kunt u niet geheel Hallo opslaan in Hallo tabel-service.  

#### <a name="solution"></a>Oplossing
Als uw entiteit 1 MB groot overschrijdt omdat een of meer eigenschappen een grote hoeveelheid gegevens bevatten, kunt u gegevens opslaan op Hallo Blob-service en Hallo-adres van de blob Hallo op te slaan in een eigenschap in Hallo entiteit. Bijvoorbeeld Hallo foto van een werknemer opslaan in blob-opslag en een koppeling toohello foto opslaan in Hallo **Photo** eigenschap van de werknemer entiteit:  

![][25]

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* toomaintain uiteindelijke consistentie tussen Hallo entiteit in Hallo tabelservice en Hallo-gegevens in Hallo Blob-service gebruiken Hallo [uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern) toomaintain uw entiteiten.
* Bij het ophalen van een volledige entiteit ten minste twee opslagtransacties omvat: één tooretrieve Hallo entiteit en één tooretrieve Hallo blob-gegevens.  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Dit patroon gebruikt als u toostore entiteiten waarvan de grootte overschrijdt de Hallo limieten voor een afzonderlijke entiteit in de tabelservice Hallo.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Uiteindelijk consistent transacties patroon](#eventually-consistent-transactions-pattern)  
* [Wide entiteiten patroon](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Antivirusprogramma patroon toevoegen/toevoegen
Schaalbaarheid vergroten wanneer u een groot aantal invoegingen hebt met het Hallo voegt verspreid over meerdere partities.  

#### <a name="context-and-problem"></a>Context en probleem
Voorafgaand of entiteiten tooyour opgeslagen entiteiten doorgaans voegen resulteert in het Hallo-toepassing eerst toe te voegen nieuwe entiteiten toohello of laatste partitie van een reeks van partities. In dit geval worden alle Hallo ingevoegd op elk moment plaatsvinden in dezelfde partitie, het maken van een hotspot dat verhindert dat de tabelservice Hallo taakverdeling wordt ingevoegd op meerdere knooppunten Hallo en mogelijk veroorzaakt door uw toepassing toohit Hallo schaalbaarheid doelen voor de partitie. Bijvoorbeeld, als u een toepassing hebt die Logboeken netwerk- en resource door werknemers openen, en vervolgens de structuur van een entiteit zoals hieronder wordt weergegeven, tot leiden kan Hallo huidige uur partitie steeds een hotspot als Hallo volume van transacties Hallo schaalbaarheid doel voor bereikt een afzonderlijke partitie:  

![][26]

#### <a name="solution"></a>Oplossing
Hallo voorkomt volgende alternatieve entiteit structuur een hotspot op een bepaalde partitie als Hallo toepassing Logboeken gebeurtenissen:  

![][27]

Met dit voorbeeld ziet hoe beide Hallo **PartitionKey** en **RowKey** samengestelde sleutels. Hallo **PartitionKey** gebruikt zowel Hallo afdeling en werknemer-id toodistribute Hallo logboekregistratie op meerdere partities.  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten wanneer u beslist Hallo hoe tooimplement dit patroon:  

* Biedt Hallo alternatieve sleutelstructuur die voorkomt hot partities maken voor de ondersteuning Hallo-query's op voegt efficiënt maakt voor uw clienttoepassing?  
* Betekent het verwachte aantal transacties dat u waarschijnlijk tooreach hello schaalbaarheidsdoelen voor een afzonderlijke partitie en worden beperkt door Hallo storage-service?  

#### <a name="when-toouse-this-pattern"></a>Wanneer toouse dit patroon
Vermijd antivirusprogramma patroon Hallo toevoegen/toevoegen als het volume van transacties waarschijnlijk tooresult is in beperkingen door Hallo storage-service wanneer u een hot partitie.  

#### <a name="related-patterns-and-guidance"></a>Verwante patronen en richtlijnen
Hallo volgende patronen en richtlijnen mogelijk ook relevante bij het implementeren van dit patroon:  

* [Samengestelde sleutel patroon](#compound-key-pattern)  
* [Patroon voor logboekbestand staart](#log-tail-pattern)  
* [Entiteiten wijzigen](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Antivirusprogramma patroon voor logboekbestand gegevens
Normaal gesproken moet u Hallo Blob-service in plaats van Hallo tabel service toostore logboekgegevens.  

#### <a name="context-and-problem"></a>Context en probleem
Als u een algemeen gebruiksvoorbeeld voor logboekgegevens tooretrieve een selectie van vermeldingen in het logboek voor een specifieke datum/tijd-bereik is: u kunt bijvoorbeeld toofind alle fout- en kritieke berichten die uw toepassing vastgelegd tussen 15:04 en 15:06 op een specifieke datum Hallo. U niet wilt dat toouse Hallo datum en tijd van Hallo logboek bericht toodetermine Hallo partitie opslaan van entiteiten logboek: dat resulteert in een hot partitie omdat op elk gewenst alle Hallo logboek entiteiten delen Hallo dezelfde **PartitionKey** waarde (Zie de sectie Hallo [antivirusprogramma patroon Prepend/append](#prepend-append-anti-pattern)). Hallo entiteit schema voor een logboekbericht na resulteert bijvoorbeeld in een hot partitie omdat Hallo-toepassing alle logboekberichten toohello partitie voor Hallo huidige datum en uur schrijft:  

![][28]

In dit voorbeeld Hallo **RowKey** bevat Hallo datum en tijd van Hallo logboek bericht tooensure dat logboekberichten worden opgeslagen in datum/tijd-volgorde gesorteerd en bevat een bericht-id als meerdere logboekberichten delen Hallo dezelfde datum en tijd.  

Een andere benadering toouse is een **PartitionKey** die ervoor zorgt dat de toepassing hello berichten over een reeks partities schrijft. Bijvoorbeeld, als Hallo bron van het logboek Hallo-bericht een manier toodistribute berichten over veel partities biedt, kan u Hallo entiteit schema te volgen:  

![][29]

Hallo probleem met dit schema is echter dat alle berichten in het logboek voor een bepaalde periode moet u zoeken Hallo tooretrieve elke partitie in de tabel Hallo.

#### <a name="solution"></a>Oplossing
Hallo vorige sectie gemarkeerde Hallo probleem van toouse probeert tabel service toostore logboekvermeldingen Hallo en twee onvoldoende voorgesteld, ontwerpen. Een oplossing geleid tooa hot partitie met Hallo risico slechte prestaties schrijven logboekberichten; Hallo andere oplossing heeft geresulteerd in slechte queryprestaties vanwege Hallo vereiste tooscan elke partitie in Hallo tabel tooretrieve berichten in het logboek voor een bepaalde periode. BLOB storage biedt een betere oplossing voor dit soort scenario en dit is hoe Azure Storage Analytics winkels Hallo logboekgegevens worden verzameld.  

Deze sectie geeft een overzicht van hoe opslag Analytics logboekgegevens opslaat in de blob-opslag ter illustratie van deze benadering toostoring gegevens die u doorgaans een query voor het bereik.  

Storage Analytics slaat logboekberichten in een indeling met scheidingstekens in meerdere blobs. Hallo gescheiden indeling kunt u gemakkelijk voor een client toepassingsgegevens tooparse Hallo in logboek het Hallo-bericht.  

Storage Analytics maakt gebruik van een naamgevingsconventie voor blobs waarmee u toolocate Hallo-blob (of BLOB's) die bevatten Hallo logboekberichten die u zoekt. Een blob met de naam 'queue/2014/07/31/1800/000001.log' bevat bijvoorbeeld logboekberichten die betrekking hebben toohello queue-service voor Hallo uur om 18:00 uur op 31 juli 2014 wordt gestart. Hallo '000001' geeft aan dat dit de eerste logboekbestand Hallo voor deze periode. Storage Analytics registreert ook eerst Hallo tijdstempels Hallo en meld u laatste berichten die in Hallo-bestand wordt opgeslagen als onderdeel van de metagegevens van het Hallo-blob. Hallo API voor blob-opslag kunt u blobs niet in een container op basis van een voorvoegsel vinden: toolocate alle Hallo blobs die wachtrij bevatten meld gegevens voor Hallo uur om 18:00 uur wordt gestart, kunt u Hallo voorvoegsel 'wachtrij/2014/07/31/1800."  

Storage Analytics logboekberichten intern buffert en werkt de juiste blob Hallo periodiek of maakt een nieuw bestand met de meest recente batch Hallo van logboekvermeldingen. Hierdoor Hallo aantal schrijfbewerkingen deze toohello blob-service moet uitvoeren.  

Als u een vergelijkbare oplossing in uw eigen toepassing implementeert, moet u overwegen hoe toomanage compromis tussen betrouwbaarheid (elke opslag voor toepassingslogboeken vermelding tooblob schrijven als dit gebeurt) en de kosten en schaalbaarheid Hallo (buffer updates in uw toepassing en schrijven van deze tooblob opslag in batches).  

#### <a name="issues-and-considerations"></a>Problemen en overwegingen
Overweeg de volgende punten bij het bepalen hoe de gegevens voor het vastleggen van toostore Hallo:  

* Als u een tabelontwerp dat potentiële hot partities voorkomt maakt, merkt u dat u geen toegang uw logboekgegevens efficiënt tot.  
* tooprocess gegevens vastleggen, een client moet vaak tooload veel records.  
* Hoewel logboekgegevens is vaak opgebouwd, kan de blob-opslag een betere oplossing zijn.  

### <a name="implementation-considerations"></a>Overwegingen bij de implementatie
Deze sectie worden enkele Hallo overwegingen toobear rekening besproken wanneer u Hallo patronen die zijn beschreven in de vorige secties Hallo implementeert. De meeste van deze sectie bevat voorbeelden geschreven in C# en die gebruikmaken van Hallo Storage-clientbibliotheek (versie 4.3.0 op Hallo moment van schrijven).  

### <a name="retrieving-entities"></a>Entiteiten ophalen
Zoals beschreven in de sectie Hallo [ontwerp voor het uitvoeren van query's](#design-for-querying), Hallo meest efficiënt query is een punt-query. Echter, in sommige gevallen moet u mogelijk tooretrieve meerdere entiteiten. Deze sectie beschrijft een aantal algemene benaderingen tooretrieving entiteiten Hallo Storage-clientbibliotheek gebruiken.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Uitvoeren van een punt-query Hallo Storage-clientbibliotheek
Hallo gemakkelijkste manier tooexecute een punt-query is toouse hello **ophalen** bewerking tabel, zoals wordt weergegeven in de volgende C#-codefragment Hallo die ophaalt van een entity met een **PartitionKey** van de waarde 'verkoop' en een  **RowKey** van de waarde '212':  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

U ziet hoe in dit voorbeeld Hallo entiteit verwacht het ophalen van toobe van het type **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Bij het ophalen van meerdere entiteiten met behulp van LINQ
U kunt meerdere entiteiten ophalen met behulp van LINQ met Storage-clientbibliotheek en het opgeven van een query met een **waar** component. een tabelscan tooavoid, moet u altijd Hallo opnemen **PartitionKey** waarde in Hallo waar component, en indien mogelijk Hallo **RowKey** tooavoid tabel en partitie scans waarde. Hallo tabelservice ondersteunt een beperkte set vergelijking operators (groter dan groter dan of gelijk is, minder dan, kleiner dan of gelijk zijn, gelijk en niet gelijk) toouse in Hallo waar component. Hallo volgende C#-codefragment vindt alle Hallo werknemers waarvan de laatste naam begint met "B" (ervan uitgaande dat Hallo **RowKey** winkels Hallo achternaam) van de verkoopafdeling Hallo (ervan uitgaande dat Hallo **PartitionKey** slaat de naam van de afdeling Hallo):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

U ziet hoe Hallo-query is zowel een **RowKey** en een **PartitionKey** tooensure betere prestaties.  

Hallo volgende codevoorbeeld toont dezelfde functionaliteit Hallo beheersen API gebruiken (Zie voor meer informatie over beheersen API's in het algemeen [aanbevolen procedures voor het ontwerpen van een beheersen API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> Hallo voorbeeld worden genest meerdere **CombineFilters** methoden tooinclude Hallo drie filtervoorwaarden.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Groot aantal entiteiten ophalen uit een query
Een optimale query retourneert een afzonderlijke entiteit op basis van een **PartitionKey** waarde en een **RowKey** waarde. Echter, in sommige scenario's wellicht hebt u een vereiste tooreturn veel entiteiten van Hallo dezelfde partitie of zelfs van veel partities.  

In dergelijke gevallen moet u altijd volledig Hallo prestaties van uw toepassing testen.  

Een query op Hallo tabelservice kan maximaal 1000 entiteiten in één keer worden geretourneerd en wordt uitgevoerd voor een maximum van vijf seconden. Als hello resultatenset bevat meer dan 1000 entiteiten, als Hallo-query is niet voltooid binnen vijf seconden, of als Hallo query grens van de partitie hello overschrijdt, Hallo tabel-service retourneert een voortzetting token tooenable toorequest Hallo van client-toepassing hello volgende set van entiteiten. Zie voor meer informatie over hoe voortzetting werk tokens [querytime-out en paginering](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Als u Hallo Storage-clientbibliotheek gebruikt, kan automatisch verwerken voortzetting tokens voor u als deze entiteiten van Hallo tabel-service retourneert. Hallo verwerkt C# codevoorbeeld Hallo Storage-clientbibliotheek automatisch met voortzetting tokens als Hallo tabelservice ze in een antwoord geretourneerd:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Hallo volgende C#-code voortzetting tokens expliciet worden verwerkt:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Voortzetting tokens expliciet gebruikt, kunt u bepalen wanneer uw toepassing hello volgende segment van de gegevens opgehaald. Bijvoorbeeld, als u de clienttoepassing kan gebruikers toopage via Hallo entiteiten die zijn opgeslagen in een tabel, kan een gebruiker besluiten niet toopage via alle Hallo entiteiten opgehaald door Hallo query zodat uw toepassing zou een voortzetting token tooretrieve Hallo alleen naast gebruiken segment wanneer Hallo gebruiker paging via alle Hallo entiteiten in het huidige segment Hallo was voltooid. Deze methode biedt verschillende voordelen:  

* Hiermee kunt u toolimit Hallo hoeveelheid gegevens tooretrieve van Hallo tabelservice en via Hallo netwerk te verplaatsen.  
* Hiermee kunt u tooperform asynchrone i/o in .NET.  
* Hiermee kunt u tooserialize Hallo voortzetting token toopersistent opslag zodat u kunt doorgaan in Hallo-gebeurtenis van een toepassing is vastgelopen.  

> [!NOTE]
> Een vervolgtoken retourneert doorgaans een segment met 1000 entiteiten, hoewel deze mogelijk minder. Dit is ook Hallo geval als u het aantal vermeldingen met behulp van een query retourneert Hallo beperken **nemen** tooreturn Hallo eerste n entiteiten die voldoen aan uw criteria lookup: Hallo tabel-service kan een segment met minder dan n entiteiten langs retourneren met een token tooenable voortzetting Hallo u tooretrieve resterende entiteiten.  
> 
> 

Hallo ziet volgende C#-code u hoe toomodify Hallo aantal entiteiten dat is geretourneerd binnen een segment:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Projectie-serverzijde
Één entiteit kunt too255 eigenschappen en too1 MB groot zijn. Wanneer u een query uitvoeren op tabel Hallo en entiteiten ophalen, u niet alle Hallo eigenschappen nodig en kunt voorkomen dat de gegevensoverdracht onnodig (toohelp verminderen en de kosten van latentie). U kunt serverzijde projectie tootransfer alleen Hallo-eigenschappen die u nodig hebt. Hallo volgende voorbeeld is er Hallo NET haalt **e** eigenschap (samen met **PartitionKey**, **RowKey**, **tijdstempel**, en  **ETag**) van Hallo entiteiten die zijn geselecteerd door Hallo-query.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

U ziet hoe Hallo **RowKey** waarde is beschikbaar, zelfs als deze niet is opgenomen in de lijst van eigenschappen tooretrieve Hallo.  

### <a name="modifying-entities"></a>Entiteiten wijzigen
Hallo Storage-clientbibliotheek kunt u toomodify uw entiteiten in de tabelservice Hallo door invoegen opgeslagen, verwijderen en bijwerken entiteiten. U kunt EGTs toobatch meerdere insert, update en delete-bewerkingen samen tooreduce Hallo aantal retouren vereist en de prestaties van uw oplossing Hallo verbeteren.  

Rekening mee dat uitzonderingen wanneer Hallo Storage-clientbibliotheek wordt uitgevoerd een EGT doorgaans Hallo index van Hallo-entiteit die Hallo batch toofail veroorzaakt. Dit is handig wanneer u code die gebruikmaakt van EGTs foutopsporing.  

U moet ook overwegen hoe uw ontwerp is van invloed op hoe de clienttoepassing gelijktijdigheid van taken en updatebewerkingen verwerkt.  

#### <a name="managing-concurrency"></a>Gelijktijdigheid van taken beheren
Standaard Hallo tabelservice implementeert optimistische gelijktijdigheid controleert op Hallo niveau van afzonderlijke entiteiten voor de **invoegen**, **samenvoegen**, en **verwijderen** -bewerkingen Hoewel het mogelijk voor een client tooforce Hallo tabel service toobypass deze controles. Zie voor meer informatie over hoe de tabelservice Hallo gelijktijdigheid beheert [gelijktijdigheid beheren in Microsoft Azure Storage](../storage/common/storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Samenvoegen of vervangen
Hallo **vervangen** methode Hallo **TableOperation** klasse altijd Hallo volledige entiteit in Hallo tabelservice vervangt. Als u geen een eigenschap in Hallo aanvraag wanneer deze eigenschap in Hallo opgeslagen entiteit bestaat, verwijdert Hallo aanvraag dat eigenschap uit Hallo entiteit opgeslagen. Tenzij u een eigenschap van een opgeslagen entiteit expliciet tooremove wilt, moet u elke eigenschap opnemen in Hallo-aanvraag.  

U kunt Hallo **samenvoegen** methode Hallo **TableOperation** klasse tooreduce Hallo hoeveelheid gegevens die u toohello tabelservice verzendt als u wilt dat tooupdate een entiteit. Hallo **samenvoegen** methode vervangt alle eigenschappen in Hallo opgeslagen entiteit met eigenschapswaarden van Hallo entiteit in Hallo aanvraag opgenomen, maar blijft intact alle eigenschappen in Hallo opgeslagen entiteit die niet zijn opgenomen in het Hallo-aanvraag. Dit is handig als u grote entiteiten en hoeft alleen tooupdate een klein aantal eigenschappen in een aanvraag.  

> [!NOTE]
> Hallo **vervangen** en **samenvoegen** twee methoden mislukken als Hallo entiteit niet bestaat. Als alternatief kunt u Hallo **InsertOrReplace** en **InsertOrMerge** methoden die nieuwe entiteit maken als deze niet bestaat.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Werken met heterogene Entiteitstypen
Hallo tabel-service is een *schema minder* tabel archief dat betekent dat één tabel entiteiten van meerdere typen bieden geweldige flexibiliteit in uw ontwerp kunt opslaan. Hallo wordt volgende voorbeeld een tabel die het opslaan van zowel werknemer en entiteiten van de afdeling:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>tijdstempel</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Denk eraan dat elke entiteit moet nog steeds **PartitionKey**, **RowKey**, en **tijdstempel** waarden, maar mogelijk elke gewenste set eigenschappen. Bovendien, er is niets tooindicate Hallo Typ van een entiteit, tenzij u toostore ergens die informatie. Er zijn twee opties voor het entiteitstype Hallo identificeren:  

* Toevoegen van Hallo entiteit type toohello **RowKey** (of mogelijk Hallo **PartitionKey**). Bijvoorbeeld: **EMPLOYEE_000123** of **DEPARTMENT_SALES** als **RowKey** waarden.  
* Gebruik een afzonderlijke eigenschap toorecord Hallo entiteitstype zoals weergegeven in onderstaande tabel voor Hallo.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>tijdstempel</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Werknemer</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Werknemer</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Afdeling</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Voornaam</th>
<th>Achternaam</th>
<th>Leeftijd</th>
<th>E-mail</th>
</tr>
<tr>
<td>Werknemer</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Hallo eerste optie voorafgaand Hallo entiteit type toohello **RowKey**, is handig als er twee entiteiten met verschillende typen wellicht Hallo mogelijkheid dezelfde sleutelwaarde. Deze groepen ook entiteiten van het Hallo dezelfde Typ samen in Hallo-partitie.  

Hallo technieken die worden besproken in deze sectie zijn vooral van belang toohello discussie [relaties voor overname](#inheritance-relationships) eerder in deze handleiding in de sectie Hallo [modellering relaties](#modelling-relationships).  

> [!NOTE]
> U moet overwegen een versienummer in Hallo entiteit waarde tooenable client toepassingen tooevolve POCO objecten van het type en werken met verschillende versies.  
> 
> 

Hallo rest van deze sectie beschrijft een aantal van Hallo-functies in Hallo Storage-clientbibliotheek waarmee u eenvoudiger werken met meerdere Entiteitstypen in Hallo dezelfde tabel.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Heterogene Entiteitstypen ophalen
Als u van Hallo Storage-clientbibliotheek gebruikmaakt, hebt u drie opties voor het werken met meerdere Entiteitstypen.  

Als u Hallo type Hallo entiteit opgeslagen met een specifieke weet **RowKey** en **PartitionKey** waarden, daarna u het entiteitstype Hallo opgeven kunt wanneer u Hallo entiteit ophalen, zoals wordt weergegeven in de vorige twee Hallo voorbeelden waarmee entiteiten van het type opgehaald **EmployeeEntity**: [uitvoeren van een punt-query Hallo Storage-clientbibliotheek](#executing-a-point-query-using-the-storage-client-library) en [bij het ophalen van meerdere entiteiten met behulp van LINQ](#retrieving-multiple-entities-using-linq).  

de tweede optie Hallo is toouse hello **DynamicTableEntity** type (een eigenschappenverzameling) in plaats van een concreet type zijn POCO entiteit (deze optie kan ook de prestaties verbeteren omdat er geen noodzaak tooserialize en Hallo entiteit te deserialiseren. NET typen). Hallo C#-code mogelijk na meerdere entiteiten met verschillende typen opgehaald uit de tabel hello, maar retourneert alle entiteiten als **DynamicTableEntity** exemplaren. Vervolgens wordt Hallo **EntityType** toodetermine Hallo eigenschapstype van elke entiteit:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Houd er rekening mee dat tooretrieve andere eigenschappen moet u Hallo **TryGetValue** methode op Hallo **eigenschappen** eigenschap Hallo **DynamicTableEntity** klasse.  

Een derde optie is toocombine met Hallo **DynamicTableEntity** type en een **EntityResolver** exemplaar. Hiermee kunt u tooresolve toomultiple POCO typen in Hallo dezelfde query. In dit voorbeeld Hallo **EntityResolver** gemachtigde met behulp van Hallo **EntityType** eigenschap toodistinguish tussen Hallo twee soorten entiteit die Hallo query retourneert. Hallo **los** methode maakt gebruik van Hallo **resolver** delegeren tooresolve **DynamicTableEntity** exemplaren te**TableEntity** exemplaren.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Heterogene Entiteitstypen wijzigen
U hoeft niet tooknow Hallo-type van een entiteit toodelete en u altijd weet Hallo-type van een entiteit wanneer u het invoegen. U kunt echter **DynamicTableEntity** typt u een entiteit tooupdate zonder te weten van het type en zonder gebruik van een POCO-entiteitsklasse. Hallo codevoorbeeld één entiteit worden opgehaald en wordt gecontroleerd Hallo **EmployeeCount** eigenschap bestaat voordat u het bijwerkt.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Beheren van toegang met handtekeningen voor gedeelde toegang
U kunt gebruikt Shared Access Signature (SAS) tokens tooenable client toepassingen toomodify (en query's) tabelentiteiten rechtstreeks zonder Hallo nodig tooauthenticate rechtstreeks met de service Hallo-tabel. Er zijn in principe drie belangrijke voordelen toousing SAS in uw toepassing:  

* U hoeft geen toodistribute uw opslag rekening sleutel tooan onbeveiligde platform (zoals een mobiel apparaat) in de volgorde tooallow die tooaccess apparaat en entiteiten in Hallo service tabel wijzigen.  
* U kunt offload Hallo werk dat web en werkrollen uitvoeren bij het beheren van uw apparaten entiteiten tooclient zoals eindgebruikers, computers en mobiele apparaten.  
* U kunt een beperkte toewijzen en tijd beperkt set machtigingen tooa client (zoals het toestaan van alleen-lezen toegang toospecific resources).  

Zie voor meer informatie over het gebruik van SAS-tokens met Hallo tabelservice [met behulp van Shared Access Signatures (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).  

Echter, moet u nog steeds Hallo SAS-tokens die een client toepassing toohello entiteiten in de tabelservice Hallo verlenen genereren: u moet dit doen in een omgeving die toegang tot de opslagaccountsleutels tooyour heeft beveiligde. Meestal gebruikt u een web- of worker-rol toogenerate Hallo SAS-tokens en bieden ze toohello clienttoepassingen die toegang moeten hebben tot tooyour entiteiten. Omdat er nog steeds een overhead voor het genereren en SAS-tokens tooclients leveren, moet u het beste tooreduce deze overhead, met name in grootschalige scenario's.  

Het is mogelijk toogenerate een SAS-token dat verleent toegang tooa subset van Hallo entiteiten in een tabel tot. U maakt standaard een SAS-token voor een hele tabel, maar het is ook mogelijk toospecify die Hallo SAS-token verlenen toegang tooeither een reeks **PartitionKey** waarden of een bereik van **PartitionKey** en  **RowKey** waarden. U kunt ervoor kiezen toogenerate SAS-tokens voor afzonderlijke gebruikers van uw systeem dat elke gebruiker SAS-token kan ze alleen toegang tootheir eigen entiteiten in Hallo tabelservice.  

### <a name="asynchronous-and-parallel-operations"></a>Asynchrone en parallelle bewerkingen
Mits u kunt uw verzoeken om te worden verspreid over meerdere partities, kunt u de doorvoer en client reactiesnelheid verbeteren met behulp van asynchrone of parallelle query's.
U wellicht bijvoorbeeld twee of meer werkprocessen rolinstanties toegang krijgen tot uw tabellen parallel. U kunt afzonderlijke werkrollen die verantwoordelijk zijn voor bepaalde sets van partities hebben of hoeven er meerdere exemplaren van worker-rol, elke kunnen tooaccess alle partities in een tabel Hallo.  

U kunt binnen een clientexemplaar doorvoer verbeteren door opslagbewerkingen asynchroon uitgevoerd. Hallo Storage-clientbibliotheek kunt u eenvoudig toowrite asynchrone query's en wijzigingen. U kunt bijvoorbeeld beginnen met Hallo de synchrone methode die alle Hallo entiteiten in een partitie ophalen, zoals wordt weergegeven in de volgende C#-code Hallo:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

U kunt deze code eenvoudig wijzigen zodat deze query hello wordt asynchroon als volgt uitgevoerd:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

In dit voorbeeld asynchrone ziet u Hallo volgende wijzigingen uit Hallo synchrone versie:  

* Hallo methodehandtekening bevat nu Hallo **asynchrone** aanpassingsfunctie en retourneert een **taak** exemplaar.  
* In plaats van aanroepen Hallo **ExecuteSegmented** methode tooretrieve resultaten, Hallo methode nu aanroepen Hallo **ExecuteSegmentedAsync** methode en maakt gebruik van Hallo **await** Wijzigingsfunctie tooretrieve asynchroon resulteert.  

Hallo-clienttoepassing kan deze methode niet aanroepen meerdere keren (met verschillende waarden voor Hallo **afdeling** parameter), en elke query wordt uitgevoerd op een afzonderlijke thread.  

Houd er rekening mee dat er geen asynchrone versie Hallo is **Execute** methode in Hallo **TableQuery** klasse omdat Hallo **IEnumerable** interface ondersteunt geen asynchrone opsomming.  

U kunt invoegen, bijwerken en verwijderen van entiteiten asynchroon. Hallo volgende C#-voorbeeld ziet u een eenvoudige, synchrone methode tooinsert of vervangen van een werknemer entiteit:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

U kunt deze code eenvoudig wijzigen zodat Hallo update wordt asynchroon als volgt uitgevoerd:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

In dit voorbeeld asynchrone ziet u Hallo volgende wijzigingen uit Hallo synchrone versie:  

* Hallo methodehandtekening bevat nu Hallo **asynchrone** aanpassingsfunctie en retourneert een **taak** exemplaar.  
* In plaats van aanroepen Hallo **Execute** methode tooupdate Hallo entiteit, Hallo methode nu aanroepen Hallo **ExecuteAsync** methode en maakt gebruik van Hallo **await** aanpassingsfunctie tooretrieve asynchroon resultaat.  

Hallo-clienttoepassing kan meerdere asynchrone methoden zoals deze aanroepen en elke methodeaanroep wordt uitgevoerd op een afzonderlijke thread.  

### <a name="credits"></a>Tegoed
Willen we graag toothank Hallo volgende leden van het team van Azure voor hun bijdragen Hallo: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah en Serdar Ozler evenals Tom Hollander van Microsoft DX. 

Willen we graag ook toothank Hallo volgende Microsoft-MVP voor hun waardevolle feedback in revisie runs: Igor Papirov en Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

