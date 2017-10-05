---
title: Inleiding tot Azure Storage | Microsoft Docs
description: Een overzicht van Azure Storage, online gegevensopslag van Microsoft in de cloud. Informatie over het gebruik van de beste oplossing voor cloudopslag in uw toepassingen.
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
ms.openlocfilehash: 98670b60daca7091e09ce2ab03cf2eaff015070e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-microsoft-azure-storage"></a>Inleiding tot Microsoft Azure Storage

## <a name="overview"></a>Overzicht
Azure Storage is de oplossing voor opslag in de cloud voor moderne toepassingen die afhankelijk zijn van duurzaamheid, beschikbaarheid en schaalbaarheid om te voldoen aan de behoeften van klanten. In dit artikel lezen ontwikkelaars, IT-professionals en zakelijke besluitvormers meer over het volgende:

* Wat is Azure Storage en hoe gebruikt u dit in uw cloud en met uw mobiele, server- en bureaubladtoepassingen?
* Welke typen gegevens kunt u opslaan met de Azure Storage-services: blobgegevens (object), NoSQL-tabelgegevens, wachtrijberichten en bestandsshares.
* Hoe wordt de toegang tot uw gegevens in Azure Storage beheerd?
* Hoe worden uw Azure Storage-gegevens duurzaam gemaakt aan de hand van redundantie en replicatie?
* Waar bouwt u uw eerste Azure Storage-toepassing?

<!-- after our quick starts are available, replace this link with a link to one of those. 
Had to remove this article, it refers to the VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- To get up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Zie [Volgende stappen](#next-steps) hieronder voor meer informatie over de hulpprogramma's, bibliotheken en andere bronnen voor het gebruik van Azure Storage.

## <a name="what-is-azure-storage"></a>Wat is Azure Storage?
Cloud computing maakt nieuwe scenario's mogelijk voor toepassingen die schaalbare, duurzame en maximaal beschikbare opslag voor hun gegevens vereisen. En dit is precies waarom Microsoft Azure Storage heeft ontwikkeld. Azure Storage maakt het ontwikkelaars mogelijk om grootschalige toepassingen te bouwen die nieuwe scenario's ondersteunen. Daarnaast levert Azure Storage de opslagbasis voor Azure Virtual Machines, waardoor de robuustheid van het systeem nog eens wordt onderstreept.

Azure Storage is zeer schaalbaar. U kunt honderden terabytes aan gegevens opslaan en verwerken ter ondersteuning van de big data-scenario's die u nodig hebt voor toepassingen die u gebruikt voor wetenschap, financiële analyse en media. Ook de kleine hoeveelheden gegevens die u nodig hebt voor een kleine zakelijke website kunt u opslaan. Wat u ook nodig hebt, u betaalt alleen voor de gegevens die u opslaat. Momenteel zijn er tientallen biljoenen unieke klantobjecten opgeslagen in Azure Storage. Daarnaast worden er gemiddeld miljoenen aanvragen per seconde verwerkt.

Azure Storage is elastisch. U kunt toepassingen ontwerpen voor een grote wereldwijde doelgroep en deze toepassingen naar behoefte schalen, zowel wat betreft de hoeveelheid opgeslagen gegevens als het aantal aanvragen dat wordt verwerkt. U betaalt alleen voor wat u gebruikt, wanneer u het gebruikt.

Azure Storage maakt gebruik van automatische partitionering, waardoor automatisch taakverdelingen van uw gegevens worden uitgevoerd op basis van het verkeer. Dit betekent dat naarmate er steeds meer gebruik van uw toepassing wordt gemaakt, Azure Storage automatisch de juiste resources toewijst om aan de vraag te voldoen.

Azure Storage is overal ter wereld toegankelijk vanuit elk type toepassing, of het nu wordt uitgevoerd in de cloud, op het bureaublad, op een on-premises server of op een mobiele telefoon of tablet. U kunt Azure Storage gebruiken in mobiele scenario's waarin de toepassing een subset van de gegevens op het apparaat opslaat en synchroniseert met een volledige set gegevens die is opgeslagen in de cloud.

Voor extra gemak bij de ontwikkeling biedt Azure Storage ondersteuning voor clients die gebruikmaken van verschillende besturingssystemen (waaronder Windows en Linux) en programmeertalen (waaronder .NET, Java, Node.js, Python, Ruby, PHP en C++ en mobiele programmeertalen). Azure Storage biedt ook gegevensresources via eenvoudige REST-API's, die beschikbaar zijn voor elke client die gegevens kan verzenden en ontvangen via HTTP/HTTPS.

Azure Premium Storage levert schijfondersteuning met hoge prestaties en lage latentie voor I/O-intensieve werkbelastingen op Azure Virtual Machines. Met Azure Premium Storage kunt u meerdere permanente gegevensschijven koppelen aan een virtuele machine en deze configureren om ervoor te zorgen dat deze aan uw prestatievereisten voldoen. Voor maximale I/O-prestaties wordt elke gegevensschijf ondersteund door een SSD-schijf in Azure Premium Storage. Zie [Premium Storage: krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md) voor meer informatie.

## <a name="introducing-the-azure-storage-services"></a>Introductie van de Azure Storage-services
Azure Storage biedt de volgende vier services: Blob Storage, Table Storage, Queue Storage en File Storage.

* Met Blob Storage worden ongestructureerde objectgegevens opgeslagen. Een blob kan elk type tekst of binaire gegevens zijn, zoals een document, mediabestand of toepassingsinstallatieprogramma. U kunt Blob Storage zien als een vorm van objectopslag.
* Met Table Storage worden gestructureerde gegevenssets opgeslagen. Table Storage is een gegevensarchief met NoSQL-sleutelkenmerk, waarmee snelle ontwikkeling en snelle toegang tot grote hoeveelheden gegevens mogelijk is.
* Queue Storage biedt betrouwbare berichten voor de verwerking van de werkstroom en voor communicatie tussen onderdelen van Cloud Services.
* File Storage biedt gedeelde opslag voor oudere toepassingen met behulp van het standaard SMB-protocol. Azure Virtual Machines en Cloud Services kunnen bestandsgegevens via gekoppelde shares delen tussen toepassingsonderdelen en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via de bestandsservice REST-API.

Een Azure Storage-account is een veilig account dat u toegang biedt tot services in Azure Storage. Uw opslagaccount biedt een unieke naamruimte voor uw opslagresources. In onderstaande afbeelding ziet u de relaties tussen de Azure Storage-resources in een opslagaccount:

![Azure Storage-resources](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob Storage
Blob Storage vormt een rendabele en schaalbare oplossing voor gebruikers met grote hoeveelheden ongestructureerde objectgegevens die in de cloud worden opgeslagen. U kunt Blob Storage gebruiken voor het opslaan van inhoud zoals:

* Documenten
* Sociale gegevens, zoals foto's, video's, muziek en blogs
* Back-ups van bestanden, computers, databases en apparaten
* Afbeeldingen en tekst voor webtoepassingen
* Configuratiegegevens voor cloudtoepassingen
* Big data, zoals logboeken en andere grote gegevenssets

Elke blob is georganiseerd in een container. Containers bieden ook een handige manier om beveiligingsbeleid toe te wijzen aan groepen objecten. Een opslagaccount kan een onbeperkt aantal containers bevatten en een container kan een onbeperkt aantal blobs bevatten, tot de capaciteitslimiet van 500 TB van het opslagaccount is bereikt.

Blob Storage biedt drie typen blobs: blok-blobs, toevoeg-blobs en pagina-blobs (schijven).

* Blok-blobs zijn geoptimaliseerd voor streaming en opslag van cloudobjecten en zijn een goede keuze voor het opslaan van documenten, mediabestanden, back-ups enzovoort.
* Toevoeg-blobs zijn vergelijkbaar met blok-blobs, maar deze zijn geoptimaliseerd voor toevoegbewerkingen. Een toevoeg-blob kan alleen worden bijgewerkt door een nieuw blok aan het eind toe te voegen. Toevoeg-blobs zijn een goede keuze voor scenario's zoals logboekregistratie, waarbij alleen aan het eind van de blob nieuwe gegevens moeten worden geschreven.
* Pagina-blobs zijn geoptimaliseerd voor de vertegenwoordiging van IaaS-schijven en de ondersteuning van willekeurige schrijfbewerkingen. Deze kunnen maximaal 1 TB groot zijn. Een op een Azure Virtual Machine-netwerk aangesloten IaaS-schijf is een VHD die is opgeslagen als pagina-blob.

Voor zeer grote gegevenssets waarbij netwerkbeperkingen het downloaden of uploaden van gegevens van of naar Blob Storage via de kabel onrealistisch maken, kunt u een vaste schijf naar Microsoft verzenden om gegevens rechtstreeks via het datacentrum te importeren en exporteren. Zie [De Microsoft Azure Import/Export-service gebruiken om gegevens over te brengen naar Blob Storage](storage-import-export-service.md).

## <a name="table-storage"></a>Table Storage

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Moderne toepassingen vereisen vaak gegevensopslag met meer schaalbaarheid en flexibiliteit dan vorige softwaregeneraties vereisten. Table Storage biedt maximaal beschikbare, sterk schaalbare opslag, zodat uw toepassing automatisch kan schalen om aan de behoeften van de gebruiker te voldoen. Table Storage is de NoSQL-sleutelkenmerkopslag van Microsoft. Deze service heeft een ontwerp zonder schema, wat deze opslag onderscheidt van traditionele relationele databases. Met een schemaloze gegevensopslag kunt u uw gegevens eenvoudig aanpassen als de behoeften van uw toepassing veranderen. Table Storage is eenvoudig te gebruiken, zodat ontwikkelaars snel toepassingen kunnen maken. De toegang tot gegevens verloopt snel en kostenefficiënt voor alle soorten toepassingen.  Table Storage is doorgaans aanzienlijk goedkoper dan traditionele SQL voor vergelijkbare gegevensvolumes.

Table Storage is een sleutelkenmerkopslag, wat betekent dat elke waarde in een tabel wordt opgeslagen met een getypeerde eigenschapsnaam. De naam van de eigenschap kan worden gebruikt om te filteren en selectiecriteria op te geven. Een verzameling eigenschappen en hun waarden vormen samen een entiteit. Omdat Table Storage schemaloos is, kunnen twee entiteiten in dezelfde tabel verschillende verzamelingen eigenschappen hebben. Dit kunnen verschillende typen eigenschappen zijn.

U kunt Table Storage gebruiken voor het opslaan van flexibele gegevenssets, zoals gebruikersgegevens voor webtoepassingen, adresboeken, apparaatgegevens en alle overige typen metagegevens die uw service nodig heeft.  In elke tabel kunt u een willekeurig aantal entiteiten opslaan. Een opslagaccount kan een onbeperkt aantal tabellen bevatten, tot de maximale capaciteit van het opslagaccount.

Zoals ook het geval is bij Blob Storage en Queue Storage, kunnen ontwikkelaars Table Storage beheren en openen met standaard REST-protocollen. Table Storage biedt echter ook ondersteuning voor een subset van het OData-protocol, waardoor geavanceerde querymogelijkheden worden vereenvoudigd en JSON- en AtomPub-indelingen (op basis van XML) mogelijk worden gemaakt.

Voor de huidige internetgebaseerde toepassingen bieden NoSQL-databases zoals Table Storage een populaire alternatief voor traditionele relationele databases.

## <a name="queue-storage"></a>Queue Storage
Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald. Queue Storage biedt een betrouwbare berichtenoplossing voor asynchrone communicatie tussen toepassingsonderdelen, of deze nu worden uitgevoerd in de cloud, op een desktopcomputer, op een on-premises server of op een mobiel apparaat. Queue Storage biedt ook ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.

Een opslagaccount kan een onbeperkt aantal wachtrijen bevatten. Een wachtrij kan een onbeperkt aantal berichten bevatten, tot de capaciteitslimiet van het opslagaccount is bereikt. Afzonderlijke berichten kunnen maximaal 64 kB groot zijn.

## <a name="file-storage"></a>File Storage
De Azure Files-service stelt u in staat om zeer beschikbare netwerkbestandsshares in te stellen die toegankelijk zijn via het standaard SMB-protocol (Server Message Block). Dit betekent dat meerdere VM's dezelfde bestanden kunnen delen met zowel lees- als schrijftoegang. U kunt de bestanden ook lezen met behulp van de REST-interface of de opslagclientbibliotheken.

Eén ding dat Azure File Storage onderscheidt van bestanden in een zakelijke bestandsshare is het feit dat u overal ter wereld toegang hebt tot de bestanden via een URL die verwijst naar het bestand, en een SAS-token (Shared Access Signature) bevat. U kunt SAS-tokens genereren. Met deze tokens hebt u gedurende een opgegeven tijdperiode toegang tot een specifiek privéasset.

Bestandsshares kunnen worden gebruikt voor veelvoorkomende scenario's:

* Veel on-premises toepassingen maken gebruik van bestandsshares. Met deze functie kunt u gemakkelijker toepassingen die gegevens delen, migreren naar Azure. Als u de bestandsshare koppelt aan dezelfde stationsletter die wordt gebruikt voor de on-premises toepassing, werkt het gedeelte van de toepassing dat toegang heeft tot de bestandsshare, (vrijwel) ongewijzigd.

* Configuratiebestanden kunnen worden opgeslagen in een bestandsshare en zijn toegankelijk vanaf meerdere VM's. Hulpprogramma's en hulpmiddelen die worden gebruikt door meerdere ontwikkelaars in een groep, kunnen worden opgeslagen in een bestandsshare. Hierdoor kan iedereen ze vinden en maakt iedereen ook gebruik van dezelfde versie.

* Diagnostische logboeken, metrische gegevens en crashdumps zijn slechts drie voorbeelden van gegevens die naar een bestandsshare kunnen worden geschreven, en later verwerkt of geanalyseerd.

Op dit moment worden verificatie op basis van Active Directory en toegangsbeheerlijsten (ACL's) niet ondersteund, maar ondersteuning hiervan wordt in de toekomst beschikbaar. De opslagaccountreferenties worden gebruikt voor verificatie voor toegang tot de bestandsshare. Dit betekent dat iedereen met de gekoppelde share volledige lees-/schrijftoegang tot de share heeft.

## <a name="access-to-blob-table-queue-and-file-resources"></a>Toegang tot Blob-, Table-, Queue- en File-resources
Standaard heeft alleen de eigenaar van het opslagaccount toegang tot resources in het opslagaccount. Voor de beveiliging van uw gegevens moet elke aanvraag die bij resources in uw account wordt gedaan, worden geverifieerd. De verificatie is afhankelijk van een gedeelde-sleutelmodel. Blobs kunnen ook worden geconfigureerd om anonieme verificatie te ondersteunen.

Wanneer uw opslagaccount wordt gemaakt, worden er twee sleutels voor persoonlijke toegang aan toegewezen die worden gebruikt voor verificatie. Doordat u twee sleutels hebt, blijft de toepassing beschikbaar wanneer u de sleutels uit veiligheidsoverwegingen regelmatig opnieuw genereert.

Als u beheerde toegang tot uw opslagresources moet toestaan voor uw gebruikers, kunt u een Shared Access Signature maken. Een Shared Access Signature (SAS) is een token die kan worden toegevoegd aan een URL waarmee gedelegeerde toegang tot een opslagresource mogelijk wordt gemaakt. Iedereen die de token in zijn bezit heeft, heeft gedurende de geldigheidsperiode toegang tot de resource waarnaar de token verwijst met de voor de token opgegeven machtigingen. Vanaf versie 2015-04-05 ondersteunt Azure Storage twee soorten gedeelde handtekeningen voor toegang: service-SAS en account-SAS.

De service-SAS biedt toegang tot een resource in slechts een van de opslagservices: de Blob-, Queue-, Tabel- of File-service.

Een account-SAS delegeert toegang tot resources in een of meer van de opslagservices. U kunt toegang tot serviceniveaubewerkingen die niet beschikbaar zijn bij een service-SAS delegeren. U kunt ook toegang tot het lezen, schrijven en verwijderen van bewerkingen delegeren voor blobcontainers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan bij een service-SAS.

Tot slot kunt u opgeven dat een container en de bijbehorende blobs of een specifieke blob beschikbaar zijn voor openbare toegang. Wanneer u opgeeft dat een container of blob openbaar is, kan iedereen deze anoniem lezen. Er is dan geen verificatie vereist.  Openbare containers en blobs zijn nuttig voor de weergave van resources, zoals media en documenten die worden gehost op websites.  Om de netwerklatentie voor een globale doelgroep te reduceren, kunt u de blobgegevens die worden gebruikt door websites met Azure CDN in de cache opslaan.

Zie [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) voor meer informatie over handtekeningen voor gedeelde toegang. Zie [Anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md) en [Verificatie voor de Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179428.aspx) voor meer informatie over veilige toegang tot uw Storage-account.

## <a name="replication-for-durability-and-high-availability"></a>Replicatie voor duurzaamheid en maximale beschikbaarheid
De gegevens in uw Microsoft Azure Storage-account worden altijd gerepliceerd om duurzaamheid en hoge beschikbaarheid te garanderen. Met replicatie worden al uw gegevens gekopieerd, in hetzelfde datacentrum of naar een tweede datacentrum, afhankelijk van welke replicatieoptie u kiest. Replicatie beschermt uw gegevens en handhaaft de beschikbaarheid van uw toepassing in het geval van een tijdelijke hardwarefout. Als uw gegevens naar een tweede datacentrum worden gerepliceerd, zijn uw gegevens ook beschermd tegen een catastrofale fout op de primaire locatie.

Replicatie zorgt ervoor dat uw opslagaccount voldoet aan de [Service-Level Agreement (SLA) voor opslag](https://azure.microsoft.com/support/legal/sla/storage/), zelfs wanneer er fouten optreden. Raadpleeg de SLA voor informatie over de garanties van Azure Storage voor duurzaamheid en beschikbaarheid.

Wanneer u een opslagaccount maakt, kunt u een van de volgende replicatieopties selecteren:

* **Lokaal redundante opslag (LRS).** Lokaal redundante opslag onderhoudt drie kopieën van uw gegevens. LRS wordt binnen één datacentrum in één regio driemaal gerepliceerd. LRS beschermt uw gegevens tegen normale hardwarefouten, maar niet tegen het uitvallen van één datacentrum.

    LRS wordt aangeboden met korting. Voor maximale duurzaamheid wordt aanbevolen dat u geografisch redundante opslag gebruikt, zoals hieronder wordt beschreven.
* **Zone-redundante opslag (ZRS).** Zone-redundante opslag onderhoudt drie kopieën van uw gegevens. ZRS wordt binnen twee of drie faciliteiten in één regio of tussen twee regio's driemaal gerepliceerd en biedt een hogere duurzaamheid dan LRS. ZRS houdt uw gegevens duurzaam binnen één regio.

    ZRS biedt een hoger duurzaamheidsniveau dan LRS. Voor maximale duurzaamheid wordt echter het gebruik van geografisch redundante opslag aanbevolen. Deze vorm wordt hieronder beschreven.

  > [!NOTE]
  > ZRS is momenteel alleen beschikbaar voor blok-blobs en wordt alleen ondersteund voor versie 2014-02-14 en hoger.
  >
  > Nadat u uw opslagaccount hebt gemaakt en ZRS hebt geselecteerd, kunt u het niet omzetten naar ander type replicatie. Ook kunt u niet meer overstappen naar ZRS als u al een ander type hebt geselecteerd.
  >
  >
* **Geografisch redundante opslag (GRS)**. GRS onderhoudt zes kopieën van uw gegevens. Met GRS worden uw gegevens driemaal gerepliceerd binnen de primaire regio en driemaal in een secundaire regio op honderden kilometers afstand van de primaire regio. Zo biedt deze service het hoogste duurzaamheidsniveau. Als er een storing optreedt in de primaire regio, wordt er door Azure Storage een failover naar de secundaire regio uitgevoerd. GRS houdt uw gegevens duurzaam binnen twee afzonderlijke regio's.

    Zie [Azure-regio’s](https://azure.microsoft.com/regions/) voor meer informatie over de primaire en secundaire koppelingen per regio.
* **Geografisch redundante opslag met leestoegang (RA-GRS)**. Met geografisch redundante opslag met leestoegang worden uw gegevens gerepliceerd naar een secundaire geografische locatie en hebt u leestoegang tot uw gegevens op de secundaire locatie. Met geografisch redundante opslag met leestoegang hebt u toegang tot uw gegevens vanaf de primaire of de secundaire locatie als er één locatie niet beschikbaar is. Wanneer u een opslagaccount maakt, wordt geografisch redundante opslag met leestoegang standaard ingeschakeld.

  > [!IMPORTANT]
  > U kunt wijzigen hoe uw gegevens worden gerepliceerd nadat uw opslagaccount is gemaakt, tenzij u ZRS hebt opgegeven tijdens het maken van het account. Er worden mogelijk eenmalig extra kosten in rekening gebracht voor de overdracht van gegevens als u overschakelt van LRS naar GRS of RA-GRS.
  >
  >

Zie [Azure Storage-replicatie](storage-redundancy.md) voor meer informatie over opties voor de replicatie van opslag.

Zie [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor informatie over de prijzen van de replicatie van opslagaccounts. Zie [Azure-regio’s](https://azure.microsoft.com/regions/#services) voor meer informatie over welke services beschikbaar zijn in elke regio.

Zie [SOSP-document - Azure Storage: een maximaal beschikbare cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx) (Engelstalig) voor architecturale informatie over duurzaamheid met Azure Storage.

## <a name="transferring-data-to-and-from-azure-storage"></a>Gegevens overbrengen van en naar Azure Storage
U kunt het opdrachtregelhulpprogramma AzCopy gebruiken om blob-, bestands- en tabelgegevens binnen uw opslagaccount of tussen opslagaccounts te kopiëren. Zie [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md) voor meer informatie.

AzCopy is gebouwd boven op de [Azure-bibliotheek voor gegevensverplaatsing](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), die momenteel beschikbaar is als voorbeeld.

De service Azure Import/Export biedt een manier voor het importeren of exporteren van blobgegevens van/naar uw storage-account via een harde schijf, verzonden naar het Azure Datacenter. Zie [De Microsoft Azure Import/Export-service gebruiken om gegevens over te brengen naar Blob Storage](storage-import-export-service.md) voor meer informatie over de Import/Export-service.

## <a name="pricing"></a>Prijzen
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Storage-API's, -bibliotheken en -hulpprogramma's
Azure Storage-resources zijn toegankelijk voor elke taal waarvoor HTTP/HTTPS-aanvragen mogelijk zijn. Daarnaast biedt Azure Storage programmeringsbibliotheken voor verschillende veelgebruikte talen. Deze bibliotheken vereenvoudigen veel aspecten van het werken met Azure Storage door details zoals synchrone en asynchrone aanroepafhandeling, batchverwerking van bewerkingen, uitzonderingsbeheer, automatische nieuwe pogingen, werking enzovoort. Bibliotheken zijn momenteel beschikbaar voor de volgende talen en platformen (deze lijst wordt in de toekomst uitgebreid):

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
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.
* [Azure Storage-clienthulpprogramma’s](storage-explorers.md)
* [Azure-SDK's en -hulpprogramma's](https://azure.microsoft.com/tools/)
* [Azure-opslagemulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy-opdrachtregelprogramma](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie over Azure Storage:

### <a name="documentation"></a>Documentatie
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Een opslagaccount maken](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link to one of those. 
Had to remove this article, it refers to the VS quickstarts, and they've stopped publishing them. Robin --> 
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
* [Blob Storage gebruiken met Java](storage-java-how-to-use-blob-storage.md)
* [Table Storage gebruiken met Java](storage-java-how-to-use-table-storage.md)
* [Queue Storage gebruiken met Java](storage-java-how-to-use-queue-storage.md)
* [File Storage gebruiken met Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Voor Node.js-ontwikkelaars
* [Blob Storage gebruiken met Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Table Storage gebruiken met Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Queue Storage gebruiken met Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Voor PHP-ontwikkelaars
* [Blob Storage gebruiken met PHP](storage-php-how-to-use-blobs.md)
* [Table Storage gebruiken met PHP](storage-php-how-to-use-table-storage.md)
* [Queue Storage gebruiken met PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Voor Ruby-ontwikkelaars
* [Blob Storage gebruiken met Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Table Storage gebruiken met Ruby](storage-ruby-how-to-use-table-storage.md)
* [Queue Storage gebruiken met Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Voor Python-ontwikkelaars
* [Blob Storage gebruiken met Python](storage-python-how-to-use-blob-storage.md)
* [Table Storage gebruiken met Python](storage-python-how-to-use-table-storage.md)
* [Queue Storage gebruiken met Python](storage-python-how-to-use-queue-storage.md)
* [File Storage gebruiken met Python](storage-python-how-to-use-file-storage.md)
