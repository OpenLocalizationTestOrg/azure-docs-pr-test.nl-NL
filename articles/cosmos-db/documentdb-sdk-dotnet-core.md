---
title: aaaAzure Cosmos DB .NET Core API SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo .NET Core API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Azure Cosmos DB .NET Core SDK: Releaseopmerkingen en resources
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET-Feed van wijzigen](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST-resourceprovider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK downloaden**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**API-documentatie**</td><td>[.NET API-naslagdocumentatie](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Voorbeelden**</td><td>[.NET-codevoorbeelden](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Aan de slag**</td><td>[Aan de slag met hello Azure Cosmos DB .NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Zelfstudie voor web-app**</td><td>[Ontwikkeling van webtoepassing met Azure Cosmos-DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Huidige ondersteunde framework**</td><td>[.NET standaard 1.6 en .NET standaard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Releaseopmerkingen

Hello Azure Cosmos DB .NET Core SDK heeft functie pariteit met de meest recente versie Hallo Hallo [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Hello Azure Cosmos DB .NET Core SDK is nog niet compatibel met Universal Windows Platform (UWP)-apps. Als u geïnteresseerd in Hallo .NET Core SDK die ondersteuning biedt voor UWP-apps bent, e-mail sturen te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Ondersteuning toegevoegd voor PartitionKeyRangeId als een FeedOption voor het vaststellen van de query resultaten tooa specifieke sleutel partitiebereikwaarde. 
* Ondersteuning toegevoegd voor StartTime als een ChangeFeedOption toostart Hallo wijzigingen zoekt na dit tijdstip. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Een probleem opgelost in Hallo JsonSerializable-klasse die een stackoverloopuitzondering kan veroorzaken.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Toegevoegde ondersteuning voor het opgeven van aangepaste JsonSerializerSettings tijdens het instantiëren van een [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) exemplaar.

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Ondersteuning voor .NET standaard 1.5 als een van de doel-frameworks Hallo.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Een probleem dat van invloed op een x64 vaste machines die geen SSE4 instructie ondersteunen en genereert SEHException bij het uitvoeren van query's Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.
*   Ondersteuning toegevoegd voor query metrische gegevens voor afzonderlijke partities.
*   Ondersteuning toegevoegd voor het beperken van de grootte van de Hallo van Hallo vervolgtoken voor query's.
*   Ondersteuning toegevoegd voor meer gedetailleerde tracering van mislukte aanvragen.
*   Een aantal verbeteringen aangebracht in Hallo SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Een probleem dat genegeerd Hallo PartitionKey waarde die is opgegeven in FeedOptions voor cumulatieve query's opgelost.
* Een probleem opgelost in transparante verwerking van de partitie management tijdens de vlucht halverwege cross-partitie Order By queryuitvoering.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Een probleem waardoor impassen in een aantal asynchrone Hallo API's bij gebruik binnen de context van ASP.NET opgelost.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Toomake SDK corrigeert meer robuuste tooautomatic failover onder bepaalde omstandigheden.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Herstel voor een probleem dat soms een WebException veroorzaakt: Hallo externe naam kan niet worden omgezet.
* Hallo toegevoegde ondersteuning voor het rechtstreeks lezen van een getypt document door nieuwe overloads tooReadDocumentAsync API toe te voegen.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Toegevoegde ondersteuning voor LINQ voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).
* Herstel voor een probleem geheugen-geheugenlek voor Hallo ConnectionPolicy object veroorzaakt door Hallo gebruik van gebeurtenis-handler.
* Herstel voor een probleem waarbij de UpsertAttachmentAsync niet werkt is wanneer ETag is gebruikt.
* Herstel voor een probleem waarin cross partitie volgorde door de voortzetting van de query niet werken is bij het sorteren van tekenreeksveld.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem). Zie [aggregatie ondersteuning](documentdb-sql-query.md#Aggregates).
* Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK kunt u toobuild snel, platformoverschrijdende [ASP.NET Core](https://www.asp.net/core) en [.NET Core](https://www.microsoft.com/net/core#windows) toorun apps op Windows, Mac en Linux. Hallo meest recente versie van hello Azure Cosmos DB .NET Core SDK is volledig [Xamarin](https://www.xamarin.com) compatibel en gebruikte toobuild toepassingen die zijn gericht op iOS-, Android- en Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-Preview

Hello Azure Cosmos DB .NET Core Preview SDK kunt u toobuild snel, platformoverschrijdende [ASP.NET Core](https://www.asp.net/core) en [.NET Core](https://www.microsoft.com/net/core#windows) toorun apps op Windows, Mac en Linux.

Hello Azure Cosmos DB .NET Core Preview SDK heeft functie pariteit met de meest recente versie Hallo Hallo [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) en ondersteunt de volgende Hallo:
* Alle [verbindingsmodus](performance-tips.md#networking): Gateway-modus, Direct TCP- en HTTPs Direct. 
* Alle [consistentieniveaus](consistency-levels.md): sterke, sessie, gebonden veroudering en Eventual.
* [Gepartitioneerde verzamelingen](partition-data.md). 
* [Meerdere landen/regio database accounts en geo-replicatie](distribute-data-globally.md).

Als u vragen gerelateerde toothis SDK hebt, te posten[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), of het bestand is een probleem in Hallo [github-opslagplaats](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Release & buiten gebruik stellen datums

| Versie | Releasedatum | Vervaldatum |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 augustus 2017 |--- | 
| [1.4.1](#1.4.1) |07 augustus 2017 |--- |
| [1.4.0](#1.4.0) |02 augustus 2017 |--- |
| [1.3.2](#1.3.2) |12 juni 2017 |--- |
| [1.3.1](#1.3.1) |23 mei 2017 |--- |
| [1.3.0](#1.3.0) |10 mei 2017 |--- |
| [1.2.2](#1.2.2) |19 april 2017 |--- |
| [1.2.1](#1.2.1) |29 maart 2017 |--- |
| [1.2.0](#1.2.0) |25 maart 2017 |--- |
| [1.1.2](#1.1.2) |20 maart 2017 |--- |
| [1.1.1](#1.1.1) |14 maart 2017 |--- |
| [1.1.0](#1.1.0) |16 februari 2017 |--- |
| [1.0.0](#1.0.0) |21 december 2016 |--- |
| [0.1.0-Preview](#0.1.0-preview) |15 november 2016 |31 december 2016 |

## <a name="see-also"></a>Zie ook
Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service. 

