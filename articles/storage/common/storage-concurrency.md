---
title: aaaManaging gelijktijdigheid in Microsoft Azure Storage
description: Hoe toomanage concurrency voor services Blob, Queue, Table en File Hallo
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 5b8efbe0a9ebc881ded8f3abef5f138e0385f7c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Gelijktijdigheid beheren in Microsoft Azure Storage
## <a name="overview"></a>Overzicht
Moderne internetgebaseerde toepassingen hebben meestal meerdere gebruikers weergeven en gegevens tegelijkertijd bijwerken. Hiervoor moet toepassing ontwikkelaars toothink zorgvuldig over hoe tooprovide een voorspelbare ervaring voor eindgebruikers tootheir, met name voor scenario's waarin meerdere gebruikers kunnen bijwerken Hallo dezelfde gegevens. Er zijn drie belangrijkste gegevens gelijktijdigheidsstrategieën die ontwikkelaars doorgaans overwegen:  

1. Optimistische gelijktijdigheid: een toepassing uitvoeren van die een update als onderdeel van de update controleert of Hallo gegevens is gewijzigd sinds de toepassing hello laatste die gegevens lezen. Bijvoorbeeld, als twee gebruikers die een pagina wiki een update toohello pagina dezelfde vervolgens Hallo wiki platform moet dat Hallo tweede update niet de eerste update hallo – overschreven en zowel gebruikers begrijpen of de update voltooid is. Deze strategie wordt meestal gebruikt in webtoepassingen.
2. Volledige vergrendeling: een toepassing die op zoek tooperform een update duurt een vergrendeling op een object zo wordt voorkomen dat andere gebruikers bijwerken Hallo gegevens tot Hallo vergrendeling is vrijgegeven. Bijvoorbeeld in een master/slave gegevens replicatiescenario waarbij alleen Hallo master updates voert wordt Hallo master doorgaans houdt een exclusieve vergrendeling voor langere tijd op Hallo gegevens tooensure geen een andere gebruiker kunt bijwerken.
3. Laatste schrijver wins – een methode waarmee alle bewerkingen update tooproceed zonder te controleren als een andere toepassing hello gegevens is bijgewerkt sinds de toepassing hello eerst Hallo-gegevens lezen. Deze strategie (of het ontbreken van een strategie voor een formele) wordt meestal gebruikt waarbij de gegevens zijn gepartitioneerd zodanig dat er geen kans dat meerdere gebruikers toegang hebben tot Hallo is dezelfde gegevens. Dit kan ook nuttig zijn wanneer tijdelijke gegevensstromen wordt verwerkt.  

Dit artikel bevat een overzicht van hoe hello Azure Storage platform vereenvoudigt ook de ontwikkeling eerste-klas door ondersteuning te bieden voor alle drie deze strategieën gelijktijdigheid van taken.  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure Storage: vereenvoudigt ook de ontwikkeling van de Cloud
Hello Azure storage-service ondersteunt alle drie strategieën, hoewel het onderscheidende in de mogelijkheid tooprovide volledige ondersteuning voor de optimistische en volledige gelijktijdigheid omdat deze ontworpen tooembrace een sterke consistentie model waarborgt u dat wanneer Hallo opslag service doorvoeracties een gegevens invoegen of bijwerken van de bewerking alle verdere toegang krijgt tot toothat gegevens ziet Hallo meest recente update. Opslagplatforms die gebruikmaken van een model uiteindelijke consistentie hebben een vertraging tussen wanneer een schrijfbewerking door één gebruiker wordt uitgevoerd en wanneer Hallo bijgewerkt gegevens zijn zichtbaar voor andere gebruikers dus complicerende ontwikkeling van clienttoepassingen in volgorde tooprevent inconsistenties van eindgebruikers kunnen beïnvloeden.  

Bovendien tooselecting een juiste gelijktijdigheid strategie ontwikkelaars ook moet rekening houden met hoe wijzigingen – vooral wijzigingen toohello dezelfde via transacties object Hiermee isoleert u een opslag-platform. Hello Azure storage-service maakt gebruik van snapshot-isolatie tooallow lezen bewerkingen toohappen als schrijfbewerkingen binnen één partitie. In tegenstelling tot andere isolatieniveaus snapshot-isolatie wordt gegarandeerd dat alle leesbewerkingen een consistente momentopname van Hallo gegevens zien terwijl updates worden gegeven – in wezen door Hallo laatste doorgevoerd waarden geretourneerd tijdens het verwerken van een update-transactie.  

## <a name="managing-concurrency-in-blob-storage"></a>Gelijktijdigheid van taken in Blob storage beheren
U kunt ervoor kiezen toouse ofwel optimistische of volledige gelijktijdigheid toomanage toegang tooblobs modellen en containers in Hallo blob-service. Als u een strategie niet expliciet opgeeft laatste schrijft wins Hallo standaardwaarde is.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Optimistische gelijktijdigheid voor blobs en containers
Hallo Storage-service wijst een id tooevery object is opgeslagen. Deze id wordt telkens bijgewerkt wanneer een updatebewerking wordt uitgevoerd op een object. Hallo-id geretourneerd toohello client als onderdeel van een HTTP GET-antwoord met behulp van hello (entiteitscode) ETag-header die is gedefinieerd binnen Hallo HTTP-protocol. Een gebruiker uitvoeren van een update op een dergelijk object kunt verzenden in Hallo oorspronkelijke ETag samen met een voorwaardelijke kop tooensure die een update wordt alleen uitgevoerd als een bepaalde voorwaarde is voldaan: in dit geval Hallo-voorwaarde een header 'If-Match', waarvoor Hallo opslag vereist is Service tooensure Hallo-waarde van ETag die is opgegeven in de updateaanvraag Hallo is hetzelfde als dat wordt opgeslagen in Hallo opslagservice Hallo Hallo.  

Hallo-overzicht van dit proces is als volgt:  

1. Ophalen van een blob uit opslagservice hello, Hallo-antwoord bevat een HTTP-ETag-Header-waarde die Hallo huidige versie van Hallo-object in Hallo storage-service aangeeft.
2. Wanneer u Hallo blob bijwerkt, omvatten Hallo ETag-waarde u in stap 1 van Hallo ontvangen **If-Match** voorwaardelijke kop van Hallo aanvraag verzenden van toohello-service.
3. Hallo service vergelijkt Hallo ETag-waarde in Hallo-aanvraag met de huidige ETag-waarde Hallo van Hallo blob.
4. Als de huidige ETag-waarde Hallo van Hallo blob heeft een verschillende versie dan ETag in Hallo Hallo **If-Match** voorwaardelijke kop in Hallo aanvraag, Hallo-service retourneert een 412 fout toohello-client. Hiermee wordt aangegeven dat een ander proces Hallo blob is bijgewerkt sinds deze Hallo client opgehaald toohello-client.
5. Als Hallo huidige ETag-van de blob Hallo waarde Hallo dezelfde versie als de ETag Hallo in Hallo **If-Match** voorwaardelijke kop in Hallo aanvraag, Hallo-service voert Hallo aangevraagd bewerking en updates huidige ETag-waarde van de blob Hallo Hallo tooshow dat deze een nieuwe versie gemaakt.  

Hallo volgende C#-fragment (met Storage-clientbibliotheek 4.2.0 Hallo) is een eenvoudig voorbeeld van hoe tooconstruct een **If-Match AccessCondition** op basis van Hallo ETag-waarde die toegankelijk is vanuit de eigenschappen van een blob die was Hallo eerder opgehaalde noch ingevoegd. Vervolgens wordt Hallo **AccessCondition** object tijdens het bijwerken van Hallo blob: Hallo **AccessCondition** Hallo-object toevoegen **If-Match** header toohello aanvraag. Als een ander proces Hallo blob geüpdatet, retourneert Hallo blob-service een statusbericht HTTP 412 (voorwaarde is mislukt). U kunt de volledige voorbeeld Hallo hier downloaden: [beheren gelijktijdigheid van taken met behulp van Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Hallo Storage-Service biedt ook ondersteuning voor extra voorwaardelijke kopteksten, zoals **If-Modified-Since**, **If-Unmodified-Since** en **If-None-Match** , evenals combinaties daarvan. Zie voor meer informatie [voorwaardelijke Headers opgeven voor Blob-servicebewerkingen](http://msdn.microsoft.com/library/azure/dd179371.aspx) op MSDN.  

Hallo volgende tabel ziet u Hallo container bewerkingen die voorwaardelijke kop, zoals accepteren **If-Match** retourneren in Hallo-aanvraag en die een ETag-waarde in het Hallo-antwoord.  

| Bewerking | Container ETag-waarde retourneert | Voorwaardelijke kop accepteert |
|:--- |:--- |:--- |
| Container maken |Ja |Nee |
| Eigenschappen van Container ophalen |Ja |Nee |
| Container metagegevens ophalen |Ja |Nee |
| Metagegevens van de Container instellen |Ja |Ja |
| Container-ACL ophalen |Ja |Nee |
| Container-ACL instellen |Ja |Ja (*) |
| Verwijderen van Container |Nee |Ja |
| Lease-Container |Ja |Ja |
| Lijst met BLOB 's |Nee |Nee |

Hallo machtigingen (*) die zijn gedefinieerd door SetContainerACL in de cache zijn opgeslagen en updates toothese machtigingen 30 seconden toopropagate tijdens de periode waarin updates kunnen niet worden gegarandeerd toobe consistent duren.  

Hallo volgende tabel ziet u Hallo blob bewerkingen die voorwaardelijke kop, zoals accepteren **If-Match** retourneren in Hallo-aanvraag en die een ETag-waarde in het Hallo-antwoord.

| Bewerking | ETag-waarde retourneert | Voorwaardelijke kop accepteert |
|:--- |:--- |:--- |
| Blob plaatsen |Ja |Ja |
| Ophalen van Blob |Ja |Ja |
| Blob-eigenschappen ophalen |Ja |Ja |
| Blob-eigenschappen instellen |Ja |Ja |
| Blobmetagegevens ophalen |Ja |Ja |
| Blobmetagegevens instellen |Ja |Ja |
| Lease-Blob (*) |Ja |Ja |
| Momentopname Blob |Ja |Ja |
| Blob kopiëren |Ja |Ja (voor een bron- en doelserver blob) |
| Blob kopiëren afbreken |Nee |Nee |
| Verwijderen van Blob |Nee |Ja |
| Blok plaatsen |Nee |Nee |
| Lijst met geblokkeerde websites plaatsen |Ja |Ja |
| Lijst met geblokkeerde websites ophalen |Ja |Nee |
| Pagina plaatsen |Ja |Ja |
| Get-paginabereiken |Ja |Ja |

(*) Lease Blob Hallo ETag op een blob niet gewijzigd.  

### <a name="pessimistic-concurrency-for-blobs"></a>Volledige vergrendeling voor blobs
een blob voor exclusief gebruik toolock, kunt u aanschaffen een [lease](http://msdn.microsoft.com/library/azure/ee691972.aspx) erop. Wanneer u een lease aanschaft, u opgeven hoe lang u de lease moet Hallo: dit kan zijn voor tussen 15 too60 seconden of oneindige, die tooan exclusieve vergrendeling bedragen. U kunt een eindige lease tooextend en u kunt een lease vrijgeven wanneer u klaar met het bent vernieuwen. Hallo blob-service wordt automatisch eindig leases versies wanneer ze zijn verlopen.  

Leases schakelen verschillende synchronisatie strategieën toobe ondersteund, met inbegrip van exclusieve schrijven / lezen, exclusieve schrijven gedeeld / exclusief lezen en schrijven gedeeld / exclusief lezen. Wanneer een lease bestaat Hallo storage-service wordt afgedwongen exclusief schrijfbewerkingen (plaatsen, instellen en verwijderbewerkingen) echter gezorgd exclusiviteit voor leesbewerkingen vereist Hallo developer tooensure dat alle clienttoepassingen een lease-ID en die slechts één client tegelijk gebruiken heeft een geldige lease-ID. Leesbewerkingen die een lease-ID-resultaat niet in gedeelde leest opnemen.  

Hallo toont volgende C#-fragment een voorbeeld van een exclusieve lease verkrijgen gedurende 30 seconden op een blob, inhoud van de blob Hallo Hallo bijwerken en vervolgens Hallo lease los te laten. Als er al een geldige lease op Hallo blob wanneer u een nieuwe lease tooacquire, retourneert Hallo blob-service een resultaat van de status 'Conflict HTTP (409)'. Hallo volgende fragment maakt gebruik van een **AccessCondition** tooencapsulate Hallo leasegegevens object wanneer een aanvraag tooupdate Hallo blob in opslagservice Hallo maakt.  U kunt de volledige voorbeeld Hallo hier downloaden: [beheren gelijktijdigheid van taken met behulp van Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Als u een schrijfbewerking voor een geleaste blob probeert zonder het doorgeven van een lease-ID hello, mislukt de Hallo-aanvraag met een 412 fout. Opmerking dat als hello lease is verlopen voordat u aanroept Hallo **UploadText** methode, maar u nog steeds Hallo lease-ID doorgeven, Hallo aanvraag ook mislukt met een **412** fout. Zie voor meer informatie over het beheren van verlopen leaseduur en lease id's, Hallo [Lease Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) REST-documentatie.  

Hallo kunnen volgende blob bewerkingen gebruiken leases toomanage volledige vergrendeling:  

* Blob plaatsen
* Ophalen van Blob
* Blob-eigenschappen ophalen
* Blob-eigenschappen instellen
* Blobmetagegevens ophalen
* Blobmetagegevens instellen
* Verwijderen van Blob
* Blok plaatsen
* Lijst met geblokkeerde websites plaatsen
* Lijst met geblokkeerde websites ophalen
* Pagina plaatsen
* Get-paginabereiken
* Momentopname Blob - lease-ID is optioneel als er een lease bestaat
* Blob - lease ID is vereist als een lease op Hallo bestemmings-blob bestaat kopiëren
* Afbreken kopie Blob - ID van de lease is vereist als er een oneindige lease op Hallo bestemmings-blob bestaat
* Lease Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Volledige vergrendeling voor containers
Leases voor containers Hallo dezelfde synchronisatie strategieën toobe ondersteund als op blobs inschakelen (exclusief voor schrijven / lezen, exclusieve schrijven gedeeld / exclusief lezen en schrijven gedeeld / lezen exclusief) maar in tegenstelling tot blobs Hallo storage-service alleen wordt afgedwongen exclusiviteit op de delete-bewerkingen. een container met een actieve reservering geldt toodelete, een client moet bevatten Hallo actieve lease-ID met Hallo delete-aanvraag. Alle andere container bewerkingen slaagt in een container geleaste Hallo lease-ID waaronder operations in dat geval ze worden gedeeld. Als exclusiviteit van update (put of set) of leesbewerkingen vereist vervolgens moet ontwikkelaars dat alle clients gebruiken een lease-ID en die alleen één client tegelijk een geldige lease-ID. heeft  

Hallo kunnen volgende container bewerkingen gebruiken leases toomanage volledige vergrendeling:  

* Verwijderen van Container
* Eigenschappen van Container ophalen
* Container metagegevens ophalen
* Metagegevens van de Container instellen
* Container-ACL ophalen
* Container-ACL instellen
* Lease-Container  

Zie voor meer informatie:  

* [Voorwaardelijke kop opgeven voor bewerkingen van de Blob-Service](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Lease-Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Lease Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Gelijktijdigheid van taken beheren in Hallo Tabelservice
Hallo tabel-service gebruikt optimistische gelijktijdigheid controleert als standaardgedrag Hallo wanneer u werkt met entiteiten, in tegenstelling tot Hallo blob-service waarbij u expliciet tooperform optimistische gelijktijdigheid controles moet kiezen. Hallo andere verschil tussen Hallo tabel en de blob-services is dat u alleen Hallo gelijktijdigheid gedrag van entiteiten beheren kunt terwijl met Hallo blob-service kunt u Hallo gelijktijdigheid van zowel containers en blobs beheren.  

Optimistische gelijktijdigheid toouse en toocheck als een ander proces een entiteit gewijzigd, omdat u deze uit Hallo table storage-service opgehaald, kunt u Hallo ETag-waarde wordt wanneer Hallo tabel-service een entiteit retourneert. Hallo-overzicht van dit proces is als volgt:  

1. Een entiteit ophalen uit de tabelservice opslag hello, Hallo-antwoord bevat een ETag-waarde die aangeeft van de huidige Hallo-id die is gekoppeld aan deze entiteit in Hallo storage-service.
2. Tijdens het bijwerken van entiteit Hallo Hallo ETag-waarde u in stap 1 van verplichte Hallo ontvangen omvatten **If-Match** koptekst van Hallo aanvraag verzenden van toohello-service.
3. Hallo service vergelijkt Hallo ETag-waarde in Hallo-aanvraag met de huidige ETag-waarde Hallo van Hallo entiteit.
4. Als Hallo huidige ETag-waarde van de entiteit Hallo verschilt van Hallo ETag in Hallo verplichte **If-Match** header in Hallo aanvraag, Hallo-service retourneert een 412 fout toohello-client. Hiermee wordt aangegeven dat een ander proces Hallo entiteit is bijgewerkt sinds deze Hallo client opgehaald toohello-client.
5. Als Hallo huidige ETag-waarde van de entiteit Hallo is hetzelfde als de ETag in verplichte Hallo HALLO hallo **If-Match** header in Hallo aanvraag of Hallo **If-Match** header bevat Hallo jokerteken (*) Hallo-service voert Hallo aangevraagd bewerking en updates Hallo huidige ETag-waarde van Hallo entiteit tooshow dat deze is bijgewerkt.  

Opmerking dat de service van de tabel Hallo in tegenstelling tot Hallo blob-service, Hallo client tooinclude vereist een **If-Match** header in updateaanvragen. Het is echter mogelijk tooforce een onvoorwaardelijke bijwerken (laatste schrijver strategie voor wins) en gelijktijdigheid controles overslaan als Hallo client ingesteld Hallo **If-Match** header toohello jokerteken (*) in Hallo-aanvraag.  

Hallo volgende C#-fragment toont klantentiteit die eerder gemaakt of opgehaald met hun e-mailadres dat is bijgewerkt. Hallo initiële invoegen of bewerking winkels Hallo ETag-waarde in Hallo klant-object ophalen en omdat het Hallo-voorbeeld gebruikt hello hetzelfde exemplaar van het object bij het uitvoeren van Hallo vervangen is, verzendt automatisch Hallo ETag-waarde back toohello tabel-service Hallo service toocheck voor schendingen van gelijktijdigheid inschakelen. Als een ander proces Hallo entiteit in de table storage geüpdatet, stuurt Hallo-service een statusbericht HTTP 412 (voorwaarde is mislukt).  U kunt de volledige voorbeeld Hallo hier downloaden: [beheren gelijktijdigheid van taken met behulp van Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly hello gelijktijdigheidscontrole uitschakelen, moet u instellen dat Hallo **ETag** eigenschap Hallo **werknemer** object te ' * ' voordat u de vervangingsbewerking Hallo uitvoert.  

```csharp
customer.ETag = "*";  
```

Hallo volgende tabel ziet u hoe de entiteit tabelbewerkingen Hallo ETag waarden gebruiken:

| Bewerking | ETag-waarde retourneert | Aanvraag-header If-Match vereist |
|:--- |:--- |:--- |
| Query-entiteiten |Ja |Nee |
| Entiteit invoegen |Ja |Nee |
| Bijwerken van entiteit |Ja |Ja |
| Samenvoegen van entiteit |Ja |Ja |
| Entiteit verwijderen |Nee |Ja |
| Invoegen of vervangen van entiteit |Ja |Nee |
| Invoegen of samenvoegen van entiteit |Ja |Nee |

Houd er rekening mee dat Hallo **invoegen of vervangen entiteit** en **invoegen of samenvoegen entiteit** bewerkingen uitvoeren *niet* gelijktijdigheid controles uitvoeren, omdat ze een toohello ETag-waarde niet verzenden tabelservice.  

In het algemeen verstandig ontwikkelaars met tabellen optimistische gelijktijdigheid van taken bij het ontwikkelen van schaalbare toepassingen. Als volledige vergrendeling is vereist, kunnen de ontwikkelaars een manier worden wanneer toegang tot tabellen tooassign een aangewezen blob voor elke tabel wordt en de tootake een lease op Hallo blob probeert voordat het besturingssysteem op Hallo tabel. Deze aanpak Hallo toepassing tooensure vereist dat alle gegevenstoegang paden Hallo lease voorafgaande toooperating op Hallo tabel verkrijgen. Vergeet niet dat is de minimale leasetijd Hallo 15 seconden die moet zorgvuldig gebeuren voor schaalbaarheid.  

Zie voor meer informatie:  

* [Bewerkingen op entiteiten](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Gelijktijdigheid van taken beheren in Hallo Queue-Service
Een scenario die in welke gelijktijdigheid van taken een probleem in Hallo queueing-service is is waar meerdere clients zijn bij het ophalen van berichten uit een wachtrij. Wanneer een bericht wordt opgehaald uit de wachtrij hello, omvat antwoord Hallo Hallo-bericht en een ontvangstwaarde pop, dit vereiste toodelete Hallo-bericht is. Hallo-bericht wordt niet automatisch verwijderd uit de wachtrij hello, maar nadat zijn opgehaald, is niet zichtbaar tooother clients voor het tijdsinterval Hallo door Hallo visibilitytimeout parameter opgegeven. Hallo-client die het Hallo-bericht opgehaald is verwachte toodelete Hallo-bericht nadat deze is verwerkt en voordat Hallo tijd door opgegeven Hallo TimeNextVisible-element van het Hallo-antwoord dat wordt berekend op basis van de Hallo van Hallo visibilitytimeout parameter. Hallo-waarde van visibilitytimeout wordt toegevoegd aan de toohello tijd op welke Hallo bericht is toodetermine Hallo-waarde van TimeNextVisible opgehaald.  

Hallo queue-service heeft geen ondersteuning voor volledige noch optimistische gelijktijdigheid, en voor deze berichten worden verwerkt op een manier idempotent van reden clients verwerken van berichten die zijn opgehaald uit een wachtrij moet. Een strategie voor wins van laatste schrijver wordt gebruikt voor de update-bewerkingen zoals SetQueueServiceProperties, SetQueueMetaData, SetQueueACL en UpdateMessage.  

Zie voor meer informatie:  

* [REST-API van wachtrij](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Berichten ophalen](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Gelijktijdigheid van taken beheren in Hallo File-Service
Hallo file-service zijn toegankelijk via twee verschillende protocoleindpunten – SMB en REST. Hallo REST-service biedt geen ondersteuning voor beperkte vergrendeling of volledige vergrendeling en alle updates moeten een strategie voor wins van laatste schrijver volgen. Bestand vergrendelingsfout mechanismen toomanage toegang tooshared systeembestanden – inclusief Hallo mogelijkheid tooperform volledige vergrendeling kunnen gebruikmaken van SMB-clients die bestandsshares koppelen. Wanneer een SMB-client een bestand opent, wordt hiermee aangegeven Hallo bestandstoegang en -share modus. Instellen van een optie toegang tot het bestand van 'Schrijven' of ' Lezen/schrijven' samen met een bestandsshare-modus van 'None' leidt tot Hallo-bestand wordt vergrendeld door een SMB-client zolang Hallo-bestand is gesloten. Als de REST-bewerking wordt uitgevoerd op een bestand waarin een SMB-client vergrendeld Hallo-bestand heeft worden Hallo REST-service statuscode 409 (Conflict) met foutcode SharingViolation geretourneerd.  

Wanneer een bestand om te verwijderen van een SMB-client wordt geopend, Hiermee Hallo bestand gemarkeerd als in behandeling verwijderen tot de SMB-client open ingangen in dat bestand gesloten. Wanneer een bestand is gemarkeerd als in behandeling verwijderen, wordt een REST-bewerking op dat bestand statuscode 409 (Conflict) met foutcode SMBDeletePending geretourneerd. Statuscode 404 (niet gevonden) wordt niet geretourneerd omdat het is mogelijk Hallo SMB-client tooremove Hallo in afwachting van verwijdering vlag voorafgaande tooclosing Hallo-bestand. Met andere woorden, worden statuscode 404 (niet gevonden) alleen verwacht bij het Hallo-bestand is verwijderd. Houd er rekening mee dat terwijl een bestand SMB verwijderen status in behandeling wordt, deze worden niet opgenomen in de lijst bestanden resulteert Hallo. Merk ook op dat Hallo REST-bestand verwijderen en REST verwijderen Directory operations moment toegepast zijn en niet in een status in afwachting van verwijdering resulteren.  

Zie voor meer informatie:  

* [Hiermee vergrendelt u het beheer van bestand](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Samenvatting en de volgende stappen
Hallo ontworpen Microsoft Azure Storage-service is toomeet Hallo behoeften van de meest complexe onlinetoepassingen Hallo zonder ontwikkelaars toocompromise of denken over belangrijke ontwerp veronderstellingen zoals gelijktijdigheid van taken en gegevens consistentie dat ze afkomstig tootake zijn voor verleend.  

Voer voor Hallo voorbeeldtoepassing waarnaar wordt verwezen in deze blog:  

* [Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Voor meer informatie over Azure Storage-Zie:  

* [Startpagina van Microsoft Azure Storage](https://azure.microsoft.com/services/storage/)
* [Inleiding tooAzure opslag](storage-introduction.md)
* Opslag aan de slag voor [Blob](../blobs/storage-dotnet-how-to-use-blobs.md), [tabel](../../cosmos-db/table-storage-how-to-use-dotnet.md), [wachtrijen](../storage-dotnet-how-to-use-queues.md), en [bestanden](../storage-dotnet-how-to-use-files.md)
* Opslagarchitectuur – [Azure Storage: een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

