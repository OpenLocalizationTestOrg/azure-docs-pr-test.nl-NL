---
title: aaaIntroduction tooAzure Storage | Microsoft Docs
description: Inleiding tooAzure opslag, de gegevensopslag van Microsoft in Hallo cloud.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Inleiding tooMicrosoft Azure Storage

Microsoft Azure Storage is een door Microsoft beheerde cloudservice waarmee u toegang krijgt tot opslag met een zeer hoge beschikbaarheid die daarnaast veilig, duurzaam, schaalbaar en redundant is. Microsoft zorgt voor het onderhoud en handelt kritieke problemen voor u af. 

Azure Storage omvat drie gegevensservices: Blob Storage, File Storage en Queue Storage. BLOB storage ondersteunt standard en premium-opslag, met premium-opslag met alleen SSD's voor Hallo snelste prestaties mogelijk. Een andere functie is cool opslag, zodat u toostorage grote hoeveelheden zelden gebruikte gegevens tegen lagere kosten.

In dit artikel leert u Hallo volgende:
* Hello Azure Storage-services
* Hallo typen opslagaccounts
* toegang tot blobs, wachtrijen en bestanden
* versleuteling
* replicatie 
* gegevens overbrengen van of naar opslag
* Hallo veel opslagclientbibliotheken beschikbaar. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Inleiding tot hello Azure Storage-services

toouse hello services geleverd door Azure Storage - Blob-opslag, File storage en Queue storage--u eerst een opslagaccount maken en vervolgens kunt u gegevens uit een specifieke service in het opslagaccount overbrengen. 

## <a name="blob-storage"></a>Blob Storage

Blobs zijn eigenlijk net bestanden zoals u die opslaat op uw computer (of tablet, mobiele apparaat, enzovoort). Ze kunnen afbeeldingen bevatten, Microsoft Excel-bestanden, HTML-bestanden, virtuele harde schijven (VHD's), big data zoals logboeken, back-ups van databases, eigenlijk bijna alles. BLOBs worden opgeslagen in containers voor vergelijkbare toofolders. 

Na het opslaan van bestanden in Blob storage, kunt u ze openen vanaf elke locatie in met behulp van URL's Hallo wereld Hallo REST-interface of een van de clientbibliotheken van Hallo-SDK van Azure storage. Deze clientbibliotheken zijn beschikbaar voor meerdere talen, waaronder Node.js, Java, PHP, Ruby, Python en .NET. 

Er zijn drie typen blobs: blok-blobs, toevoeg-blobs en pagina-blobs (gebruikt voor VHD-schijven).

* Blok-blobs zijn gewone bestanden van de gebruikte toohold up tooabout 4,7 TB. 
* Pagina-blobs zijn gebruikte toohold willekeurige toegang verkrijgen tot bestanden van too8 TB groot. Deze worden gebruikt voor Hallo VHD-bestanden die back-virtuele machines.
* Toevoeg-BLOB's bestaan uit blokken zoals Hallo blok-blobs, maar zijn geoptimaliseerd voor toevoegbewerkingen. Deze worden gebruikt voor items zoals logboekregistratie informatie toohello dezelfde blob uit meerdere virtuele machines.

U kunt voor zeer grote gegevenssets waarbij netwerkbeperkingen uploaden of tooBlob gegevensopslag downloaden via Hallo kabel onrealistisch maken, een reeks schijven tooMicrosoft tooimport verzenden of gegevens rechtstreeks vanuit het datacenter Hallo exporteren. Zie [Hallo Microsoft Azure Import/Export-Service tooTransfer gegevens tooBlob opslag gebruiken](../storage-import-export-service.md).

## <a name="file-storage"></a>File Storage

Hello Azure Files service kunt u tooset van maximaal beschikbare netwerkbestandsshares die toegankelijk zijn via Hallo standaard Server Message Block (SMB)-protocol. Dat betekent dat meerdere virtuele machines kunnen delen dezelfde Hallo bestanden met lees- en schrijftoegang. U kunt ook Hallo bestanden lezen met Hallo REST-interface of Hallo-opslag-clientbibliotheken. 

Één ding dat Azure File storage van bestanden op een zakelijke bestandsshare onderscheidt is dat u toegang hebt tot Hallo bestanden vanaf elke locatie in Hallo wereld met een URL die verwijst toohello-bestand en bevat een shared access signature (SAS)-token. U kunt genereren van SAS-tokens; ze toestaan specifieke toegang tooa persoonlijke asset voor een specifieke hoeveelheid tijd. 

Bestandsshares kunnen worden gebruikt voor veelvoorkomende scenario's: 

* Veel on-premises toepassingen maken gebruik van bestandsshares. Deze functie kunt u gemakkelijker toomigrate die toepassingen die gegevens tooAzure delen. Als u koppelen hello file share toohello dezelfde stationsletter die Hallo lokale toepassing gebruikt, Hallo-onderdeel van uw toepassing die toegang heeft tot de bestandsshare Hallo moet samenwerken met minimale eventuele wijzigingen worden aangebracht.

* Configuratiebestanden kunnen worden opgeslagen in een bestandsshare en zijn toegankelijk vanaf meerdere VM's. Hulpprogramma's en hulpmiddelen die worden gebruikt door meerdere ontwikkelaars in een groep kunnen worden opgeslagen op een bestandsshare ervoor te zorgen dat iedereen deze vindt, en dat ze gebruiken Hallo dezelfde versie.

* Diagnostische logboeken, meetgegevens en crashdumps zijn slechts drie voorbeelden van gegevens die kunnen worden geschreven tooa bestandsshare en verwerkt of geanalyseerd later.

Op dit moment, verificatie op basis van Active Directory en de toegang niet toegangsbeheerlijsten (ACL's) worden ondersteund, maar ze zich op een bepaald moment in toekomstige Hallo. Hallo opslagaccountreferenties zijn gebruikte tooprovide verificatie voor toegang tot toohello bestandsshare. Dit betekent dat iedereen met Hallo share gekoppeld volledige lezen/schrijven toegang toohello share.

## <a name="queue-storage"></a>Queue Storage

Hello Azure Queue-service is toostore en ophalen die zijn gebruikt. Berichten in wachtrij plaatsen kunnen up too64 KB groot, en een wachtrij kan miljoenen berichten bevatten. Wachtrijen zijn in het algemeen gebruikte toostore lijsten met berichten toobe asynchroon verwerkt. 

Stel dat u wilt dat uw klanten toobe kunnen tooupload afbeeldingen en u wilt dat toocreate miniaturen voor elke afbeelding. U kunt uw klant wacht u toocreate Hallo miniaturen tijdens het uploaden van afbeeldingen Hallo kunnen hebben. Een alternatief is toouse een wachtrij. Schrijven naar een berichtenwachtrij toohello wanneer Hallo klant zijn uploaden is voltooid. Vervolgens hebben een Azure-functie Hallo-bericht ophalen uit de wachtrij Hallo en Hallo miniaturen maken. Elk van de onderdelen van deze verwerking Hallo kan worden geschaald afzonderlijk, waardoor u meer controle wanneer deze afstemming voor uw gebruik.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Table Storage
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
De Standard-versie van Azure Table Storage maakt nu deel uit van Cosmos DB. Er is ook een premium-versie van Azure Table Storage beschikbaar, met tabellen die voor doorvoer zijn geoptimaliseerd, globale distributie en automatische secundaire indexen. meer toolearn en proberen Hallo nieuwe premium ervaring check [Azure Cosmos DB: tabel API](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>File Storage

Hello Azure Storage team bezit tevens schijven, waaronder alle Hallo beheerde en onbeheerde schijf mogelijkheden die worden gebruikt door virtuele machines. Zie voor meer informatie over deze functies Hallo [documentatie Compute Service](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Typen opslagaccounts 

Deze tabel ziet u verschillende soorten storage-accounts en welke objecten kunnen worden gebruikt met elke Hallo.

|**Type opslagaccount**|**Algemeen Standard**|**Algemeen Premium**|**Blob-opslag, 'hot' en 'cool' toegangslagen**|
|-----|-----|-----|-----|
|**Ondersteunde services**| Blob-, File- en Queue-services | Blob-service | Blob-service|
|**Typen ondersteunde blobs**|Blok-blobs, pagina-blobs en toevoeg-blobs | Pagina-blobs | Blok-blobs en toevoeg-blobs|

### <a name="general-purpose-storage-accounts"></a>Opslagaccounts voor algemeen gebruik

Er zijn twee soorten opslagaccounts voor algemeen gebruik. 

#### <a name="standard-storage"></a>Standard Storage 

Hallo meest gebruikte storage-accounts zijn standaard storage-accounts, die kunnen worden gebruikt voor alle typen gegevens. Standard-opslagaccounts worden magnetische media toostore gegevens gebruikt.

#### <a name="premium-storage"></a>Premium Storage

Premium-opslag biedt krachtige opslag voor pagina-blobs, die voornamelijk worden gebruikt voor VHD-bestanden. Premium-opslagaccounts worden SSD toostore gegevens gebruikt. Microsoft adviseert om Premium Storage te gebruiken voor al uw VM's.

### <a name="blob-storage-accounts"></a>Blob Storage-accounts

Hallo Blob Storage-account is een gespecialiseerd opslagaccount gebruikt toostore blok-blobs en toevoeg-blobs. U kunt geen pagina-blobs opslaan in deze accounts en dus ook geen VHD-bestanden. Deze accounts kunt u een laag toegang tooHot tooset of Coolbar; Hallo-laag kan op elk gewenst moment worden gewijzigd. 

Hallo hot toegangslaag wordt gebruikt voor bestanden die regelmatig worden geopend--betaalt u een hogere kosten voor opslag, maar Hallo kosten van de toegang tot blobs Hallo veel lager is. Voor blobs die zijn opgeslagen in de cool toegangslaag hello, betaalt u een hogere kosten voor toegang tot blobs Hallo maar Hallo kosten voor opslag is veel lager.

## <a name="accessing-your-blobs-files-and-queues"></a>Toegang tot blobs, bestanden en wachtrijen

Elk opslagaccount heeft twee verificatiesleutels, die allebei voor elke bewerking kunnen worden gebruikt. Er zijn twee sleutels, zodat u altijd kunt terugdraaien via Hallo-codes van tijd tot tijd tooenhance beveiliging. Het is essentieel dat deze sleutels worden beveiligd omdat hun bezit, samen met de naam van Hallo, kunt onbeperkte toegang tot tooall gegevens in Hallo storage-account. 

Deze sectie ziet er twee manieren toosecure Hallo storage-account en de bijbehorende gegevens. Zie voor gedetailleerde informatie over het beveiligen van uw opslagaccount en uw gegevens Hallo [Azure Storage-beveiligingshandleiding](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Toegang beveiligen met behulp van Azure AD toostorage-accounts

Eenzijdige toosecure toegang tooyour opslaggegevens zijn door toegang toohello toegangscodes voor opslag te beheren. Met resourcemanager op rollen gebaseerd toegangsbeheer (RBAC), kunt u rollen toousers, groepen of toepassingen kunt toewijzen. Deze rollen zijn gekoppeld tooa specifieke set acties die worden toegestaan of niet is toegestaan. Met RBAC verwerkt toogrant toegang tooa storage-account alleen Hallo-beheerbewerkingen voor dat opslagaccount, zoals het wijzigen van de toegangslaag Hallo. U kunt RBAC toogrant toegang toodata objecten zoals een specifieke container of de bestandsshare niet gebruiken. U kunt echter RBAC toogrant toegang toohello toegangscodes voor opslag, die vervolgens gebruikte tooread Hallo-gegevensobjecten kunnen worden gebruiken. 

### <a name="securing-access-using-shared-access-signatures"></a>Toegang beveiligen met handtekeningen voor gedeelde toegang 

U kunt handtekeningen voor gedeelde toegang en opgeslagen toegang beleid toosecure uw gegevensobjecten. Een shared access signature (SAS) is een tekenreeks met een beveiligingstoken dat kan worden gekoppeld toohello URI voor een asset waarmee u toodelegate toegang toospecific opslagobjecten en toospecify beperkingen zoals machtigingen en Hallo datum/tijd-bereik van toegang. Deze functie heeft uitgebreide mogelijkheden. Voor gedetailleerde informatie te verwijzen[met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Openbare toegang tooblobs

Hallo Blob-Service kunt u tooprovide openbare toegang tooa container en de bijbehorende blobs of een specifieke blob. Wanneer u opgeeft dat een container of blob openbaar is, kan iedereen deze anoniem lezen. Er is dan geen verificatie vereist. Een voorbeeld van wanneer u toodo zou willen dit is wanneer u een website die van installatiekopieën, video- of documenten van Blob-opslag gebruikmaakt. Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Versleuteling

Er zijn een paar eenvoudige typen versleuteling beschikbaar zijn voor Hallo Storage-services. 

### <a name="encryption-at-rest"></a>Versleuteling 'at rest' 

U kunt versleuteling voor opslag-Service (SSE) op beide Hallo bestanden service (preview) of Hallo Blob-service voor een Azure storage-account. Indien ingeschakeld, worden alle gegevens die zijn geschreven toohello specifieke service versleuteld voordat geschreven. Wanneer u Hallo gegevens gelezen, wordt dit ontsleuteld voordat geretourneerd. 

### <a name="client-side-encryption"></a>Clientversleuteling

Hallo opslagclientbibliotheken hebben methoden die u kunt aanroepen tooprogrammatically gegevens versleutelen voordat het wordt verzonden via de kabel Hallo van Hallo client tooAzure. De gegevens worden versleuteld opgeslagen, wat betekent dat ze ook 'at rest' zijn versleuteld. Bij het lezen van gegevens terug Hallo ontsleutelen Hallo informatie na ontvangst. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Versleuteling tijdens overdracht met Azure-bestandsshares

Zie [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) voor meer informatie over handtekeningen voor gedeelde toegang. Zie [anonieme leestoegang toocontainers en blobs beheren](../blobs/storage-manage-access-to-resources.md) en [verificatie voor hello Azure Storage-Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) voor meer informatie over veilige toegang tooyour storage-account.

Zie voor meer informatie over het beveiligen van uw opslagaccount en versleuteling Hallo [Azure Storage-beveiligingshandleiding](storage-security-guide.md).

## <a name="replication"></a>Replicatie

In de volgorde tooensure dat uw gegevens duurzaam is, Azure Storage heeft Hallo mogelijkheid tookeep (en beheren) meerdere kopieën van uw gegevens. Dit wordt replicatie genoemd, en soms redundantie. Als u uw opslagaccount gaat instellen, selecteert u het type replicatie. In de meeste gevallen kan deze instelling kan worden gewijzigd nadat Hallo storage-account is ingesteld. 

Alle opslagaccounts hebben **lokaal redundante opslag (LRS)**. Dit betekent dat drie kopieën van uw gegevens worden beheerd door Azure Storage in het datacenter Hallo opgegeven wanneer het Hallo-storage-account is ingesteld. Wanneer wijzigingen zijn doorgevoerd tooone kopiëren, hello andere twee kopieën worden bijgewerkt voordat er wordt teruggekeerd geslaagd. Dit betekent dat Hallo drie replica's zijn altijd gesynchroniseerd. Ook drie kopieën van Hallo zich bevinden in domeinen met afzonderlijke fouten en upgradedomeinen, wat betekent dat de gegevens beschikbaar is, zelfs als een opslagknooppunt die uw gegevens is mislukt of wordt genomen offline toobe bijgewerkt. 

**Lokaal redundante opslag (LRS)**

Zoals hierboven is uitgelegd, beschikt u met LRS over drie kopieën van uw gegevens in één datacenter. Dit verwerkt probleem Hallo van gegevens niet langer beschikbaar is als een opslagknooppunt is mislukt of offline toobe bijgewerkt wordt genomen, maar niet Hallo geval van een hele datacenter niet langer beschikbaar is.

**Zone-redundante opslag (ZRS)**

Zone-redundante opslag (ZRS) onderhoudt Hallo drie lokale kopieën van uw gegevens en een andere set van drie kopieën van uw gegevens. Hallo is tweede reeks drie kopieën asynchroon gerepliceerd in datacenters binnen één of twee regio's. ZRS is alleen beschikbaar voor blok-blobs in opslagaccounts voor algemeen gebruik. Ook, nadat u hebt uw storage-account gemaakt en ZRS hebt geselecteerd, u deze niet converteren toouse tooany andere typen van replicatie, en vice versa.

ZRS-accounts bieden een hogere duurzaamheid dan LRS, maar ZRS-accounts ondersteunen geen metrische gegevens of logboekregistratie. 

**Geografisch redundante opslag (GRS)**

Geografisch redundante opslag (GRS) onderhoudt Hallo drie lokale kopieën van uw gegevens in een primaire regio plus een andere set van drie kopieën van uw gegevens in een secundaire regio op honderden mijl weg Hallo primaire regio. In geval van een storing optreedt in de primaire regio Hallo hello is Azure Storage failover de secundaire regio toohello. 

**Geografisch redundante opslag met leestoegang (RA-GRS)** 

Geografisch redundante opslag met leestoegang is precies zoals GRS, behalve dat u leestoegang toohello gegevens op de secundaire locatie Hallo. Als het primaire Datacenter Hallo tijdelijk niet beschikbaar is, kunt u tooread Hallo gegevens vanaf de secundaire locatie Hallo blijven. Dit kan zeer nuttig zijn. Bijvoorbeeld, kan er een webtoepassing die wijzigingen in de modus alleen-lezen en wijst toohello secundaire kopiëren, sommige toegang toe te staan, zelfs als er updates zijn niet beschikbaar. 

> [!IMPORTANT]
> U kunt wijzigen hoe uw gegevens worden gerepliceerd nadat uw storage-account is gemaakt, tenzij u ZRS hebt opgegeven toen u Hallo-account hebt gemaakt. Houd er echter rekening mee dat u een extra eenmalige gegevensoverdracht kosten als u van LRS tooGRS of RA-GRS overschakelt mogelijk kosten.
>

Zie [Azure Storage-replicatie](storage-redundancy.md) voor meer informatie over replicatie.

Zie voor herstelinformatie na noodgevallen [welke toodo als een Azure Storage-storing optreedt,](storage-disaster-recovery-guidance.md).

Voor een voorbeeld van hoe tooleverage RA-GRS opslag tooensure hoge beschikbaarheid, Zie [ontwerpen van maximaal beschikbare toepassingen met behulp van RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Overdracht van gegevens tooand van Azure Storage

U kunt Hallo AzCopy-opdrachtregelprogramma toocopy blob en bestandsgegevens binnen uw opslagaccount of tussen opslagaccounts. Zie een van de volgende Hallo artikelen voor hulp bij:

* [Transfer data with the AzCopy on Windows](storage-use-azcopy.md) (Gegevens overdragen met AzCopy voor Windows)
* [Transfer data with AzCopy on Linux](storage-use-azcopy-linux.md) (Gegevens overdragen met AzCopy voor Linux)

AzCopy is gebouwd boven op Hallo [Azure-bibliotheek voor gegevensverplaatsing](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), die momenteel beschikbaar is in preview.

Hello Azure Import/Export-service kan worden gebruikt tooimport- of exportbewerking grote hoeveelheden tooor van blob-gegevens van uw opslagaccount. U voorbereiden en e-meerdere harde schijven tooan Azure Datacenter, waar ze worden overgebracht Hallo gegevens van Hallo harde schijven en terugsturen Hallo harde schijven tooyou. Zie voor meer informatie over Hallo Import/Export-service, [Hallo Microsoft Azure Import/Export-Service tooTransfer gegevens tooBlob opslag gebruiken](../storage-import-export-service.md).

## <a name="pricing"></a>Prijzen

Zie voor gedetailleerde informatie over prijzen voor Azure Storage Hallo [prijzen pagina](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>Storage-API's, -bibliotheken en -hulpprogramma's
Azure Storage-resources zijn toegankelijk voor elke taal waarvoor HTTP/HTTPS-aanvragen mogelijk zijn. Daarnaast biedt Azure Storage programmeringsbibliotheken voor verschillende veelgebruikte talen. Deze bibliotheken vereenvoudigen veel aspecten van het werken met Azure Storage door bewerkingen zoals synchrone en asynchrone aanroepafhandeling, batchverwerking van bewerkingen, uitzonderingsbeheer, automatische nieuwe pogingen, werking, enzovoort, voor hun rekening te nemen. Bibliotheken zijn momenteel beschikbaar voor Hallo volgende talen en platforms met anderen in Hallo pijplijn:

### <a name="azure-storage-data-services"></a>Azure Storage-gegevensservices
* [REST-API voor Storage-services](/rest/api/storageservices/)
* [Opslagclientbibliotheek voor .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Opslagclientbibliotheek voor C++](https://github.com/Azure/azure-storage-cpp)
* [Opslagclientbibliotheek voor Java/Android](https://azure.microsoft.com/develop/java/)
* [Opslagclientbibliotheek voor Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Opslagclientbibliotheek voor PHP](https://azure.microsoft.com/develop/php/)
* [Opslagclientbibliotheek voor Python](https://azure.microsoft.com/develop/python/)
* [Opslagclientbibliotheek voor Ruby](https://azure.microsoft.com/develop/ruby/)
* [Opslag-cmdlets voor PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Opslagopdrachten voor CLI 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over Blob Storage](../blobs/storage-blobs-introduction.md)
* [Meer informatie over File Storage](../storage-files-introduction.md)
* [Meer informatie over Queue Storage](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Voor beheerders
* [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md)
* [Azure CLI gebruiken met Azure Storage](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Voor .NET-ontwikkelaars
* [Aan de slag met Azure Blob Storage met .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Aan de slag met Azure Table Storage met .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Aan de slag met Azure Queue Storage met .NET](../storage-dotnet-how-to-use-queues.md)
* [Aan de slag met Azure File Storage in Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Voor Java/Android-ontwikkelaars
* [Hoe toouse Blob-opslag met Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Hoe toouse Queue storage met Java](../storage-java-how-to-use-queue-storage.md)
* [Hoe toouse File storage met Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Voor Node.js-ontwikkelaars
* [Hoe toouse Blob-opslag met Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Hoe toouse Queue storage met Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Voor PHP-ontwikkelaars
* [Hoe toouse Blob-opslag met PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Hoe toouse Table storage met PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Hoe toouse Queue storage met PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Voor Ruby-ontwikkelaars
* [Hoe toouse Blob-opslag met Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Hoe toouse Queue storage met Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Voor Python-ontwikkelaars
* [Hoe toouse Blob-opslag met Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Hoe toouse Table storage met Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Hoe toouse Queue storage met Python](../storage-python-how-to-use-queue-storage.md)   
* [Hoe toouse File storage met Python](../storage-python-how-to-use-file-storage.md) 
-->