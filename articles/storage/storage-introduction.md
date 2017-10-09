---
title: aaaIntroduction tooAzure Storage | Microsoft Docs
description: Een overzicht van Azure Storage, online gegevensopslag van Microsoft in Hallo cloud. Meer informatie over hoe toouse Hallo aanbevolen oplossing voor cloudopslag in uw toepassingen.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Inleiding tooMicrosoft Azure Storage

## <a name="overview"></a>Overzicht
Azure-opslag is Hallo cloud opslagoplossing voor moderne toepassingen die afhankelijk van duurzaamheid, beschikbaarheid en schaalbaarheid toomeet Hallo behoeften van klanten zijn. In dit artikel lezen ontwikkelaars, IT-professionals en zakelijke besluitvormers meer over het volgende:

* Wat is Azure Storage en hoe gebruikt u dit in uw cloud en met uw mobiele, server- en bureaubladtoepassingen?
* Welke typen gegevens kunt u opslaan met hello Azure Storage-services: blob-gegevens (object), NoSQL-tabelgegevens, Wachtrijberichten en bestandsshares.
* Hoe toegang tooyour gegevens in Azure Storage wordt beheerd
* Hoe worden uw Azure Storage-gegevens duurzaam gemaakt aan de hand van redundantie en replicatie?
* Wanneer de volgende toobuild toogo uw eerste Azure Storage-toepassing

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Zie [Volgende stappen](#next-steps) hieronder voor meer informatie over de hulpprogramma's, bibliotheken en andere bronnen voor het gebruik van Azure Storage.

## <a name="what-is-azure-storage"></a>Wat is Azure Storage?
Cloud computing maakt nieuwe scenario's mogelijk voor toepassingen die schaalbare, duurzame en maximaal beschikbare opslag voor hun gegevens vereisen. En dit is precies waarom Microsoft Azure Storage heeft ontwikkeld. In aanvulling toomaking het mogelijk dat ontwikkelaars toobuild grootschalige toepassingen toosupport nieuwe scenario's, Azure Storage biedt ook Hallo opslagbasis voor Azure Virtual Machines, een verdere testament tooits robuustheid.

Azure Storage is zeer schaalbaar, zodat u kunt opslaan en verwerken van honderden terabytes aan gegevens toosupport Hallo big data scenario's vereist zijn voor wetenschap, financiële analyse en mediatoepassingen. Of u Hallo kleine hoeveelheden gegevens die nodig zijn voor een klein bedrijf website kunt opslaan. Wat u ook nodig, betaalt u alleen voor Hallo gegevens die u opslaat. Momenteel zijn er tientallen biljoenen unieke klantobjecten opgeslagen in Azure Storage. Daarnaast worden er gemiddeld miljoenen aanvragen per seconde verwerkt.

Azure Storage is elastisch, zodat u kunt toepassingen voor een grote wereldwijde doelgroep ontwerpen en schalen van deze toepassingen naar behoefte - beide in termen van de hoeveelheid opgeslagen gegevens Hallo en Hallo aantal aanvragen dat wordt verwerkt. U betaalt alleen voor wat u gebruikt, wanneer u het gebruikt.

Azure Storage maakt gebruik van automatische partitionering, waardoor automatisch taakverdelingen van uw gegevens worden uitgevoerd op basis van het verkeer. Dit betekent dat als Hallo behoefte aan uw toepassing wordt gemaakt, Azure Storage automatisch Hallo juiste resources toomeet toegewezen ze.

Azure-opslag is toegankelijk vanaf een willekeurige plaats in Hallo wereld van elk type toepassing, of deze wordt uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiele telefoon of Tablet. U kunt Azure Storage gebruiken in mobiele scenario's waarbij Hallo toepassing een subset van gegevens op Hallo apparaat opslaat en synchroniseert met een volledige set gegevens die zijn opgeslagen in de cloud Hallo.

Voor extra gemak bij de ontwikkeling biedt Azure Storage ondersteuning voor clients die gebruikmaken van verschillende besturingssystemen (waaronder Windows en Linux) en programmeertalen (waaronder .NET, Java, Node.js, Python, Ruby, PHP en C++ en mobiele programmeertalen). Azure Storage ook gegevensresources via eenvoudige REST-API's, die beschikbaar tooany client kan verzenden en ontvangen van gegevens via HTTP/HTTPS zijn.

Azure Premium Storage levert schijfondersteuning met hoge prestaties en lage latentie voor I/O-intensieve werkbelastingen op Azure Virtual Machines. Met Azure Premium-opslag, kunt u meerdere permanente gegevens schijven tooa virtuele machine te koppelen en configureren toomeet uw prestatievereisten voldoen. Voor maximale I/O-prestaties wordt elke gegevensschijf ondersteund door een SSD-schijf in Azure Premium Storage. Zie [Premium Storage: krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md) voor meer informatie.

## <a name="introducing-hello-azure-storage-services"></a>Inleiding tot hello Azure Storage-services
Azure storage biedt Hallo volgende vier services: Blob storage, Table storage, Queue storage en File storage.

* Met Blob Storage worden ongestructureerde objectgegevens opgeslagen. Een blob kan elk type tekst of binaire gegevens zijn, zoals een document, mediabestand of toepassingsinstallatieprogramma. BLOB-opslag is ook bedoeld tooas opslag van objecten.
* Met Table Storage worden gestructureerde gegevenssets opgeslagen. Table storage is een NoSQL-sleutelkenmerk gegevensarchief, waarmee snelle ontwikkeling en snelle toegang toolarge hoeveelheden gegevens.
* Queue Storage biedt betrouwbare berichten voor de verwerking van de werkstroom en voor communicatie tussen onderdelen van Cloud Services.
* File Storage biedt gedeelde opslag voor oudere toepassingen met behulp van Hallo standaard SMB-protocol. Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via Hallo bestandsservice REST-API.

Een Azure storage-account is een veilig account waarmee u toegang tot tooservices in Azure Storage. Uw opslagaccount biedt Hallo unieke naamruimte voor uw opslagresources. Hallo in onderstaande afbeelding ziet u Hallo relaties tussen hello Azure storage-resources in een opslagaccount:

![Azure Storage-resources](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob Storage
Voor gebruikers met grote hoeveelheden ongestructureerde object gegevens toostore in de cloud Hallo vormt Blob storage een rendabele en schaalbare oplossing. U kunt Blob storage toostore inhoud zoals:

* Documenten
* Sociale gegevens, zoals foto's, video's, muziek en blogs
* Back-ups van bestanden, computers, databases en apparaten
* Afbeeldingen en tekst voor webtoepassingen
* Configuratiegegevens voor cloudtoepassingen
* Big data, zoals logboeken en andere grote gegevenssets

Elke blob is georganiseerd in een container. Containers bieden ook een handige manier tooassign security-beleid toogroups van objecten. Een opslagaccount kan een onbeperkt aantal containers bevatten en een container kan een onbeperkt aantal blobs up toohello capaciteitslimiet van 500 TB van Hallo opslagaccount bevatten.

Blob Storage biedt drie typen blobs: blok-blobs, toevoeg-blobs en pagina-blobs (schijven).

* Blok-blobs zijn geoptimaliseerd voor streaming en opslag van cloudobjecten en zijn een goede keuze voor het opslaan van documenten, mediabestanden, back-ups enzovoort.
* Toevoeg-blobs zijn vergelijkbaar tooblock blobs, maar zijn geoptimaliseerd voor toevoegbewerkingen. Een toevoeg-blob kan alleen door het toevoegen van een nieuw blok toohello end worden bijgewerkt. Toevoeg-blobs zijn een goede keuze voor scenario's zoals logboekregistratie, waarbij nieuwe gegevens moeten toobe alleen toohello einde van Hallo blob geschreven.
* Pagina-blobs zijn geoptimaliseerd voor de vertegenwoordiging van IaaS-schijven en ondersteuning van willekeurige schrijfbewerkingen en mogelijk up too1 TB groot. Een op een Azure Virtual Machine-netwerk aangesloten IaaS-schijf is een VHD die is opgeslagen als pagina-blob.

Voor zeer grote gegevenssets waarbij netwerkbeperkingen uploaden of tooBlob gegevensopslag downloaden via Hallo kabel onrealistisch maken, kunt u een harde schijf tooMicrosoft tooimport verzenden of gegevens rechtstreeks vanuit het datacenter Hallo exporteren. Zie [Hallo Microsoft Azure Import/Export-Service tooTransfer gegevens tooBlob opslag gebruiken](storage-import-export-service.md).

## <a name="table-storage"></a>Table Storage

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Moderne toepassingen vereisen vaak gegevensopslag met meer schaalbaarheid en flexibiliteit dan vorige softwaregeneraties vereisten. Table storage biedt maximaal beschikbare, sterk schaalbare opslag, zodat uw toepassing kunt toomeet gebruikersvraag automatisch schalen. Table Storage is de NoSQL-sleutelkenmerkopslag van Microsoft. Deze service heeft een ontwerp zonder schema, wat deze opslag onderscheidt van traditionele relationele databases. Met een schemaloze gegevensopslag is het eenvoudig tooadapt uw gegevens als Hallo van uw toepassing veranderen behoeften. Table storage is eenvoudig toouse ontwikkelaars snel toepassingen kunnen maken. Toegang toodata is snel en kostenefficiënt voor alle soorten toepassingen.  Table Storage is doorgaans aanzienlijk goedkoper dan traditionele SQL voor vergelijkbare gegevensvolumes.

Table Storage is een sleutelkenmerkopslag, wat betekent dat elke waarde in een tabel wordt opgeslagen met een getypeerde eigenschapsnaam. naam van de eigenschap Hallo kan worden gebruikt voor filteren en selectiecriteria op te geven. Een verzameling eigenschappen en hun waarden vormen samen een entiteit. Omdat Table storage schemaloos is, Hallo twee entiteiten in dezelfde tabel verschillende verzamelingen eigenschappen kan bevatten en deze eigenschappen van verschillende typen kunnen zijn.

U kunt Table storage toostore flexibele gegevenssets, zoals gebruikersgegevens voor webtoepassingen, adresboeken, apparaatgegevens en alle overige typen metagegevens die uw service nodig.  U kunt een willekeurig aantal entiteiten opslaan in een tabel en een opslagaccount kan een onbeperkt aantal tabellen up toohello capaciteitslimiet van Hallo opslagaccount bevatten.

Zoals Blobs en wachtrijen kunnen ontwikkelaars beheren en toegang tot Table storage met standaard REST-protocollen, maar tabel opslag ook ondersteunt een subset van de OData-protocol hello, vereenvoudigen geavanceerde querymogelijkheden en JSON-en AtomPub (op basis van XML) indelingen.

Voor de huidige internetgebaseerde toepassingen bieden NoSQL-databases zoals Table storage een populaire alternatief tootraditional relationele databases.

## <a name="queue-storage"></a>Queue Storage
Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald. Queue storage biedt een betrouwbare berichtenoplossing voor asynchrone communicatie tussen toepassingsonderdelen, of ze worden uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiel apparaat. Queue Storage biedt ook ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.

Een opslagaccount kan een onbeperkt aantal wachtrijen bevatten. Een wachtrij kan een onbeperkt aantal berichten van toohello capaciteitslimiet van Hallo opslagaccount bevatten. Afzonderlijke berichten mogelijk up too64 KB groot zijn.

## <a name="file-storage"></a>File Storage
Hello Azure Files service kunt u tooset van maximaal beschikbare netwerkbestandsshares die toegankelijk zijn via Hallo standaard Server Message Block (SMB)-protocol. Dat betekent dat meerdere virtuele machines kunnen delen dezelfde Hallo bestanden met lees- en schrijftoegang. U kunt ook Hallo bestanden lezen met Hallo REST-interface of Hallo-opslag-clientbibliotheken.

Één ding dat Azure File storage van bestanden op een zakelijke bestandsshare onderscheidt is dat u toegang hebt tot Hallo bestanden vanaf elke locatie in Hallo wereld met een URL die verwijst toohello-bestand en bevat een shared access signature (SAS)-token. U kunt genereren van SAS-tokens; ze toestaan specifieke toegang tooa persoonlijke asset voor een specifieke hoeveelheid tijd.

Bestandsshares kunnen worden gebruikt voor veelvoorkomende scenario's:

* Veel on-premises toepassingen maken gebruik van bestandsshares. Deze functie kunt u gemakkelijker toomigrate die toepassingen die gegevens tooAzure delen. Als u koppelen hello file share toohello dezelfde stationsletter die Hallo lokale toepassing gebruikt, Hallo-onderdeel van uw toepassing die toegang heeft tot de bestandsshare Hallo moet samenwerken met minimale eventuele wijzigingen worden aangebracht.

* Configuratiebestanden kunnen worden opgeslagen in een bestandsshare en zijn toegankelijk vanaf meerdere VM's. Hulpprogramma's en hulpmiddelen die worden gebruikt door meerdere ontwikkelaars in een groep kunnen worden opgeslagen op een bestandsshare ervoor te zorgen dat iedereen deze vindt, en dat ze gebruiken Hallo dezelfde versie.

* Diagnostische logboeken, meetgegevens en crashdumps zijn slechts drie voorbeelden van gegevens die kunnen worden geschreven tooa bestandsshare en verwerkt of geanalyseerd later.

Op dit moment, verificatie op basis van Active Directory en de toegang niet toegangsbeheerlijsten (ACL's) worden ondersteund, maar ze zich op een bepaald moment in toekomstige Hallo. Hallo opslagaccountreferenties zijn gebruikte tooprovide verificatie voor toegang tot toohello bestandsshare. Dit betekent dat iedereen met Hallo share gekoppeld volledige lezen/schrijven toegang toohello share.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Toegang tooBlob, tabel, wachtrijen en bestand bronnen
Standaard kan alleen Hallo eigenaar van het opslagaccount toegang tot bronnen in Hallo storage-account. Voor beveiliging van uw gegevens Hallo moet elk verzoek op basis van bronnen in uw account worden geverifieerd. De verificatie is afhankelijk van een gedeelde-sleutelmodel. BLOBs kunnen ook worden geconfigureerd toosupport anonieme verificatie.

Wanneer uw opslagaccount wordt gemaakt, worden er twee sleutels voor persoonlijke toegang aan toegewezen die worden gebruikt voor verificatie. Met twee sleutels, zorgt u ervoor dat uw toepassing beschikbaar blijft wanneer u regelmatig Hallo sleutels uit veiligheidsoverwegingen algemene Sleutelbeheer opnieuw genereert.

Als u tooallow beheerd gebruikers toegang tooyour storage-resources hoeft, kunt u een shared access signature maken. Een shared access signature (SAS) is een token dat zijn kan dat hiermee toegang tooa opslagresource gedelegeerde toegevoegde tooa-URL. Iedereen die in Hallo token bezit Hallo resource verwijst opgegeven toowith Hallo machtigingen kunt krijgen, Hallo periode dat deze geldig is. Vanaf versie 2015-04-05 ondersteunt Azure Storage twee soorten gedeelde handtekeningen voor toegang: service-SAS en account-SAS.

Hallo-service-SAS gemachtigden toegang tot tooa resource in slechts één van de opslagservices Hallo: Hallo Blob, Queue, Table of bestand service.

Een account-SAS delegeert toegang tooresources in een of meer van de opslagservices Hallo. U kunt toegang tooservice-serviceniveaubewerkingen die niet beschikbaar met een service-SAS delegeren. U kunt ook toegang tooread-, schrijf- en delete-bewerkingen op de blob-containers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan als een service-SAS delegeren.

Tot slot kunt u opgeven dat een container en de bijbehorende blobs of een specifieke blob beschikbaar zijn voor openbare toegang. Wanneer u opgeeft dat een container of blob openbaar is, kan iedereen deze anoniem lezen. Er is dan geen verificatie vereist.  Openbare containers en blobs zijn nuttig voor de weergave van resources, zoals media en documenten die worden gehost op websites.  toodecrease netwerklatentie voor een globale doelgroep, u kunt blob-gegevens die door websites Hello Azure CDN cache.

Zie [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) voor meer informatie over handtekeningen voor gedeelde toegang. Zie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md) en [verificatie voor hello Azure Storage-Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) voor meer informatie over veilige toegang tooyour storage-account.

## <a name="replication-for-durability-and-high-availability"></a>Replicatie voor duurzaamheid en maximale beschikbaarheid
Hallo-gegevens in uw Microsoft Azure storage-account altijd is gerepliceerd tooensure duurzaamheid en maximale beschikbaarheid. Replicatie wordt gekopieerd uw gegevens zich binnen de Hallo hetzelfde Datacenter of tooa tweede Datacenter, afhankelijk van welke replicatieoptie u kiest. Replicatie beschermt u uw gegevens en behoudt uw toepassing beschikbaarheid in Hallo-gebeurtenis van tijdelijke hardwarefouten. Als uw gegevens worden gerepliceerd tweede datacentrum tooa, die ook beschermt u uw gegevens tegen een onherstelbare fout op Hallo primaire locatie.

Replicatie zorgt ervoor dat uw storage-account voldoet aan Hallo [Service Level Agreement (SLA) voor opslag](https://azure.microsoft.com/support/legal/sla/storage/) zelfs in Hallo face van fouten. Zie Hallo SLA voor informatie over Azure Storage wordt gegarandeerd dat voor duurzaamheid en beschikbaarheid.

Wanneer u een opslagaccount maakt, kunt u een Hallo volgende replicatieopties selecteren:

* **Lokaal redundante opslag (LRS).** Lokaal redundante opslag onderhoudt drie kopieën van uw gegevens. LRS wordt binnen één datacentrum in één regio driemaal gerepliceerd. LRS beschermt u uw gegevens tegen normale hardwarefouten, maar niet tegen Hallo uitvallen van één datacenter.

    LRS wordt aangeboden met korting. Voor maximale duurzaamheid wordt aanbevolen dat u geografisch redundante opslag gebruikt, zoals hieronder wordt beschreven.
* **Zone-redundante opslag (ZRS).** Zone-redundante opslag onderhoudt drie kopieën van uw gegevens. ZRS wordt gerepliceerd driemaal tussen twee toothree faciliteiten in één regio of tussen twee regio's, biedt een hogere duurzaamheid dan LRS. ZRS houdt uw gegevens duurzaam binnen één regio.

    ZRS biedt een hoger duurzaamheidsniveau dan LRS. Voor maximale duurzaamheid wordt echter het gebruik van geografisch redundante opslag aanbevolen. Deze vorm wordt hieronder beschreven.

  > [!NOTE]
  > ZRS is momenteel alleen beschikbaar voor blok-blobs en wordt alleen ondersteund voor versie 2014-02-14 en hoger.
  >
  > Zodra u hebt uw storage-account gemaakt en ZRS hebt geselecteerd, u niet met de conversie toouse tooany andere typen van replicatie, en vice versa.
  >
  >
* **Geografisch redundante opslag (GRS)**. GRS onderhoudt zes kopieën van uw gegevens. Met GRS worden uw gegevens driemaal gerepliceerd binnen de primaire regio Hallo en is ook driemaal gerepliceerd in een secundaire regio op honderden mijl weg Hallo primaire regio, Hallo hoogste niveau van duurzaamheid bieden. In geval van een storing optreedt in de primaire regio Hallo Hallo wordt Azure Storage failover toohello secundaire regio. GRS houdt uw gegevens duurzaam binnen twee afzonderlijke regio's.

    Zie [Azure-regio’s](https://azure.microsoft.com/regions/) voor meer informatie over de primaire en secundaire koppelingen per regio.
* **Geografisch redundante opslag met leestoegang (RA-GRS)**. Geografisch redundante opslag met leestoegang worden gerepliceerd van uw gegevens tooa secundaire geografische locatie en biedt ook leestoegang tooyour gegevens op de secundaire locatie Hallo. Geografisch redundante opslag met leestoegang kunt u tooaccess uw gegevens van Hallo primaire of secundaire locatie hello, in één locatie uitvalt Hallo-gebeurtenis. Geografisch redundante opslag met leestoegang is de standaardoptie Hallo voor uw opslagaccount standaard wanneer u dit hebt gemaakt.

  > [!IMPORTANT]
  > U kunt wijzigen hoe uw gegevens worden gerepliceerd nadat uw storage-account is gemaakt, tenzij u ZRS hebt opgegeven toen u Hallo-account hebt gemaakt. Houd er echter rekening mee dat u een extra eenmalige gegevensoverdracht kosten als u van LRS tooGRS of RA-GRS overschakelt mogelijk kosten.
  >
  >

Zie [Azure Storage-replicatie](storage-redundancy.md) voor meer informatie over opties voor de replicatie van opslag.

Zie [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor informatie over de prijzen van de replicatie van opslagaccounts. Zie [Azure-regio’s](https://azure.microsoft.com/regions/#services) voor meer informatie over welke services beschikbaar zijn in elke regio.

Zie [SOSP-document - Azure Storage: een maximaal beschikbare cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx) (Engelstalig) voor architecturale informatie over duurzaamheid met Azure Storage.

## <a name="transferring-data-tooand-from-azure-storage"></a>Overdracht van gegevens tooand van Azure Storage
U kunt Hallo AzCopy-opdrachtregelprogramma toocopy blob-, bestands- en tabelgegevens binnen uw opslagaccount of tussen opslagaccounts. Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) voor meer informatie.

AzCopy is gebouwd boven op Hallo [Azure-bibliotheek voor gegevensverplaatsing](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), die momenteel beschikbaar is in preview.

Hello Azure Import/Export-service biedt een manier tooimport blob-gegevens in of exporteren van blobgegevens van uw storage-account via een harde schijf, verzonden toohello Azure-Datacenter. Zie voor meer informatie over Hallo Import/Export-service, [Hallo Microsoft Azure Import/Export-Service tooTransfer gegevens tooBlob opslag gebruiken](storage-import-export-service.md).

## <a name="pricing"></a>Prijzen
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Storage-API's, -bibliotheken en -hulpprogramma's
Azure Storage-resources zijn toegankelijk voor elke taal waarvoor HTTP/HTTPS-aanvragen mogelijk zijn. Daarnaast biedt Azure Storage programmeringsbibliotheken voor verschillende veelgebruikte talen. Deze bibliotheken vereenvoudigen veel aspecten van het werken met Azure Storage door details zoals synchrone en asynchrone aanroepafhandeling, batchverwerking van bewerkingen, uitzonderingsbeheer, automatische nieuwe pogingen, werking enzovoort. Bibliotheken zijn momenteel beschikbaar voor Hallo volgende talen en platforms met anderen in Hallo pijplijn:

### <a name="azure-storage-data-services"></a>Azure Storage-gegevensservices
* [REST-API voor Storage-services](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Opslagclientbibliotheek voor .NET, Windows Phone en Windows Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Opslagclientbibliotheek voor C++](https://github.com/Azure/azure-storage-cpp)
* [Opslagclientbibliotheek voor Java/Android](https://azure.microsoft.com/develop/java/)
* [Opslagclientbibliotheek voor Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Opslagclientbibliotheek voor PHP](https://azure.microsoft.com/develop/php/)
* [Opslagclientbibliotheek voor Ruby](https://azure.microsoft.com/develop/ruby/)
* [Opslagclientbibliotheek voor Python](https://azure.microsoft.com/develop/python/)
* [Opslag-cmdlets voor PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Azure Storage-beheerservices
* [REST API-verwijzing van opslagresourceprovider](/rest/api/storagerp/)
* [Clientbibliotheek van opslagresourceprovider voor .NET](/dotnet/api/microsoft.azure.management.storage)
* [Cdmlets van opslagresourceprovider voor PowerShell 1.0](/powershell/module/azure.storage)
* [REST API van opslagservicebeheer (klassiek)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Azure Storage-services voor gegevensverplaatsing
* [REST-API van Storage Import/Export-service](storage-import-export-service.md)
* [Clientbibliotheek van opslaggegevensverplaatsing voor .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Hulpprogramma's
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Azure Storage-clienthulpprogramma’s](storage-explorers.md)
* [Azure-SDK's en -hulpprogramma's](https://azure.microsoft.com/tools/)
* [Azure-opslagemulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy-opdrachtregelprogramma](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure Storage, bekijk deze resources:

### <a name="documentation"></a>Documentatie
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Een opslagaccount maken](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Voor beheerders
* [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md)
* [Azure CLI gebruiken met Azure Storage](storage-azure-cli.md)

### <a name="for-net-developers"></a>Voor .NET-ontwikkelaars
* [Aan de slag met Azure Blob Storage met .NET](storage-dotnet-how-to-use-blobs.md)
* [Aan de slag met Azure Table Storage met .NET](storage-dotnet-how-to-use-tables.md)
* [Aan de slag met Azure Queue Storage met .NET](storage-dotnet-how-to-use-queues.md)
* [Aan de slag met Azure File Storage in Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Voor Java/Android-ontwikkelaars
* [Hoe toouse Blob-opslag met Java](storage-java-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Java](storage-java-how-to-use-table-storage.md)
* [Hoe toouse Queue storage met Java](storage-java-how-to-use-queue-storage.md)
* [Hoe toouse File storage met Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Voor Node.js-ontwikkelaars
* [Hoe toouse Blob-opslag met Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Hoe toouse Queue storage met Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Voor PHP-ontwikkelaars
* [Hoe toouse Blob-opslag met PHP](storage-php-how-to-use-blobs.md)
* [Hoe toouse Table storage met PHP](storage-php-how-to-use-table-storage.md)
* [Hoe toouse Queue storage met PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Voor Ruby-ontwikkelaars
* [Hoe toouse Blob-opslag met Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Ruby](storage-ruby-how-to-use-table-storage.md)
* [Hoe toouse Queue storage met Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Voor Python-ontwikkelaars
* [Hoe toouse Blob-opslag met Python](storage-python-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Python](storage-python-how-to-use-table-storage.md)
* [Hoe toouse Queue storage met Python](storage-python-how-to-use-queue-storage.md)
* [Hoe toouse File storage met Python](storage-python-how-to-use-file-storage.md)
