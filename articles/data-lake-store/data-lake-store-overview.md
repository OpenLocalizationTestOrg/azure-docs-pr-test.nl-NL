---
title: aaaOverview van Azure Data Lake Store | Microsoft Docs
description: Begrijpen wat is Azure Data Lake Store en Hallo waarde die dit ten opzichte van andere gegevensarchieven biedt
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Overzicht van Azure Data Lake Store
Azure Data Lake Store is een ondernemingsbrede opslagplaats op hyperschaal voor analytische workloads van big data. Azure Data Lake kunt u toocapture gegevens van elke grootte, type en opnamesnelheid snelheid in één enkele locatie voor operationele en experimentele analyses.

> [!TIP]
> Gebruik Hallo [leertraject van Data Lake Store](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart verkennen hello Azure Data Lake Store-service.
> 
> 

Azure Data Lake Store kan worden geopend via Hadoop (beschikbaar met HDInsight-cluster) met behulp van Hallo WebHDFS compatibele REST-API's. Het is speciaal ontworpen tooenable analytics op Hallo opgeslagen gegevens en is afgestemd op prestaties voor scenario's met gegevensanalyses. Out of box hello, die deze bevat alle mogelijkheden van de Hallo bedrijfsniveau: beveiliging, beheerbaarheid, schaalbaarheid, betrouwbaarheid en beschikbaarheid: essentieel voor zakelijke gebruiksvoorbeelden.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Sommige van de belangrijkste mogelijkheden Hallo van hello Azure Data Lake bevatten Hallo volgende.

### <a name="built-for-hadoop"></a>Gebouwd voor Hadoop
Hello Azure Data Lake store is een Apache Hadoop-bestandssysteem die compatibel is met Hadoop Distributed File System (HDFS) en werkt met Hallo Hadoop-ecosysteem.  Uw bestaande HDInsight-toepassingen of services die gebruikmaken van Hallo API WebHDFS kunnen eenvoudig worden geïntegreerd met Data Lake Store. Data Lake Store bevat ook een met WebHDFS compatibele REST-interface voor toepassingen

Gegevens die zijn opgeslagen in Data Lake Store kunnen eenvoudig worden geanalyseerd met analytische frameworks van Hadoop zoals MapReduce of Hive. Microsoft Azure HDInsight-clusters kunnen worden ingericht en geconfigureerd toodirectly toegang tot gegevens opgeslagen in Data Lake Store.

### <a name="unlimited-storage-petabyte-files"></a>Onbeperkte opslag, bestanden ter grootte van petabytes
Azure Data Lake Store biedt onbeperkte opslag en is geschikt voor het opslaan van een verscheidenheid aan gegevens voor analyses. Het legt beperkingen met betrekking tot account grootten, grootte of Hallo hoeveelheid gegevens die kunnen worden opgeslagen in een data lake. Afzonderlijke bestanden kan uiteenlopen van toopetabytes kB groot waardoor het een uitstekende keuze toostore elk type gegevens. Gegevens worden blijvend opgeslagen door meerdere kopieën te maken en er is geen limiet voor Hallo tijdsduur voor welke Hallo gegevens kunnen worden opgeslagen in Hallo data lake.

### <a name="performance-tuned-for-big-data-analytics"></a>Prestaties zijn afgestemd op big data-analyses
Azure Data Lake Store is gebouwd voor het uitvoeren van grootschalige analytische systemen waarvoor grote doorvoer tooquery vereisen en analyseren van grote hoeveelheden gegevens. Hallo data lake verspreidt delen van een bestand over een aantal afzonderlijke opslagservers. Dit verbetert de Hallo doorvoer lezen bij het lezen van bestand Hallo parallel voor het uitvoeren van gegevensanalyse.

### <a name="enterprise-ready-highly-available-and-secure"></a>Enterprise-ready: hoge beschikbaarheid en veiligheid
Azure Data Lake Store biedt industriestandaard beschikbaarheid en betrouwbaarheid. Uw gegevensassets worden blijvend opgeslagen door het maken van redundante exemplaren tooguard tegen onverwachte fouten. Ondernemingen kunnen Azure Data Lake bij hun oplossingen gebruiken als een belangrijk onderdeel van hun bestaande gegevensplatform.

Data Lake Store biedt ook bedrijfsniveau beveiliging voor Hallo opgeslagen gegevens. Zie voor meer informatie [Gegevens beveiligen in Azure Data Lake Store](#DataLakeStoreSecurity).

### <a name="all-data"></a>Alle gegevens
In Azure Data Lake Store kunnen alle gegevens worden opgeslagen in de oorspronkelijke indeling, zoals ze gemaakt zijn, en het is niet nodig om de gegevens eerst om te zetten. Data Lake Store niet vereisen een schema toobe gedefinieerd voordat het Hallo-gegevens zijn geladen, waardoor deze de toohello afzonderlijke analytische framework toointerpret Hallo gegevens en een schema definiëren op Hallo tijdstip van de Hallo analyse. Bestanden van verschillende groottes en indelingen kunnen toostore wordt, maakt het mogelijk voor Data Lake Store toohandle gestructureerde, semi-gestructureerde en ongestructureerde gegevens.

Containers voor gegevens van Azure Data Lake Store zijn eigenlijk mappen en bestanden. U werkt met Hallo opgeslagen gegevens met behulp van SDK's, Azure Portal en Azure Powershell. Als u uw gegevens in Hallo-archief met deze interfaces en de juiste containers Hallo plaatst, kunt u allerlei soorten gegevens opslaan. Data Lake Store voert geen speciale verwerking van gegevens op basis van Hallo type gegevens dat wordt opgeslagen.

## <a name="DataLakeStoreSecurity"></a>Gegevens beveiligen in Azure Data Lake Store
Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie en toegangsbeheerlijsten (ACL's) toomanage access tooyour-gegevens.

| Functie | Beschrijving |
| --- | --- |
| Authentication |Azure Data Lake Store integreert met Azure Active Directory (AAD) voor identiteits- en toegangsbeheer voor alle Hallo gegevens opgeslagen in Azure Data Lake Store. Als gevolg van het Hallo-integratie voordelen van Azure Data Lake van alle AAD-functies, zoals multi-factor authentication-server, voorwaardelijke toegang, op rollen gebaseerde toegangsbeheer, gebruik bewaking, beveiligingsbewaking en waarschuwingen, enzovoort. Azure Data Lake Store ondersteunt Hallo OAuth 2.0-protocol voor verificatie in Hallo REST-interface. |
| Toegangsbeheer |Azure Data Lake Store biedt toegangsbeheer door ondersteuning POSIX-machtigingen die worden weergegeven door Hallo protocol WebHDFS. In Hallo openbare Preview van Data Lake Store (Hallo huidige release), kunnen de ACL's worden ingeschakeld in de hoofdmap hello, submappen en afzonderlijke bestanden. Zie voor meer informatie over de werking van ACL's in de context van Data Lake Store [Toegangsbeheer in Data Lake Store](data-lake-store-access-control.md). |
| Versleuteling |Data Lake Store biedt ook versleuteling voor gegevens die zijn opgeslagen in Hallo-account. U opgeven Hallo versleutelingsinstellingen tijdens het maken van een Data Lake Store-account. U hebt gekozen toohave uw gegevens versleuteld of kiezen voor geen versleuteling. Voor meer informatie over het tooprovide versleuteling-gerelateerde configuratie, Zie [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md). |

Meer over het beveiligen van gegevens in Data Lake Store toolearn wilt. Volg de onderstaande koppelingen voor Hallo.

* Voor instructies over het toosecure gegevens in Data Lake Store Zie [gegevens beveiligen in Azure Data Lake Store](data-lake-store-secure-data.md).
* Kijkt u liever naar video’s? [Bekijk deze video](https://mix.office.com/watch/1q2mgzh9nn5lx) op hoe toosecure gegevens in Data Lake Store opgeslagen.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Toepassingen die compatibel zijn met Azure Data Lake Store
Azure Data Lake Store is compatibel met de meeste open source-onderdelen in Hallo Hadoop-ecosysteem. Het kan ook goed worden geïntegreerd in andere Azure-services. Hierdoor is Data Lake Store een perfecte optie voor uw opslagbehoeften. Volg onderstaande toolearn meer informatie over hoe Data Lake Store kan worden gebruikt met open source-onderdelen, evenals andere Azure-services Hallo-koppelingen.

* Zie [Toepassingen en services die compatibel zijn met Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md) voor een lijst met open-sourcetoepassingen die compatibel zijn met Data Lake Store.
* Zie [integreren met andere Azure-services](data-lake-store-integrate-with-other-services.md) toounderstand hoe Data Lake Store kan worden gebruikt met andere Azure services tooenable een breed scala aan scenario's.
* Zie [scenario's voor het gebruik van Data Lake Store](data-lake-store-data-scenarios.md) toolearn hoe toouse Data Lake opslaan in scenario's zoals het ophalen van gegevens, verwerking van gegevens, downloaden van gegevens en gegevens te visualiseren.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Wat is het bestandssysteem van Azure Data Lake Store (adl://)?
Data Lake Store is toegankelijk via het nieuwe bestandssysteem hello, Hallo AzureDataLakeFilesystem (adl: / /), in Hadoop-omgevingen (beschikbaar met HDInsight-cluster). Toepassingen en services die gebruikmaken van adl: / / tootake kunnen profiteren van verdere optimalisatie van de prestaties die zijn momenteel niet beschikbaar in WebHDFS. Als gevolg hiervan Data Lake Store biedt u de flexibiliteit tooeither Hallo de beste prestaties Hallo gebruik Hello aanbevolen optie adl: / / of bestaande code rechtstreeks door de bewerking wordt voortgezet toouse hello WebHDFS API te beheren. Azure HDInsight maakt volledig gebruik van Hallo AzureDataLakeFilesystem tooprovide Hallo optimale prestaties op Data Lake Store.

U kunt toegang tot uw gegevens in Data Lake Store met behulp van Hallo `adl://<data_lake_store_name>.azuredatalakestore.net`. Zie voor meer informatie over hoe tooaccess gegevens in Data Lake Store Hallo Hallo [weergave eigenschappen van Hallo opgeslagen gegevens](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Hoe begin ik met het gebruiken van Azure Data Lake Store?
Zie [aan de slag met Data Lake Store met behulp van Azure Portal Hallo](data-lake-store-get-started-portal.md), op hoe een Data Lake Store met tooprovision hello Azure-Portal. Wanneer u Azure Data Lake hebt ingericht, leert u hoe toouse big data-oplossingen zoals Azure Data Lake Analytics of Azure HDInsight met Data Lake Store. U kunt ook een Azure Data Lake Store-account voor een toocreate .NET-toepassing maken en uitvoeren van bewerkingen zoals het van uploadgegevens, downloaden van gegevens, enzovoort.

* [Aan de slag met Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Aan de slag met Azure Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Video’s over Data Lake Store
Als u liever video's toolearn bekijken, biedt Data Lake Store video's op een breed scala aan functies.

* [Een Azure Data Lake Store-account maken](https://mix.office.com/watch/1k1cycy4l4gen)
* [Gebruik Hallo Data Explorer tooManage gegevens in Azure Data Lake Store](https://mix.office.com/watch/icletrxrh6pc)
* [Verbinding maken met Azure Data Lake Analytics tooAzure Data Lake Store](https://mix.office.com/watch/qwji0dc9rx9k)
* [Toegang tot Azure Data Lake Store via Data Lake Analytics](https://mix.office.com/watch/1n0s45up381a8)
* [Verbinding maken met Azure HDInsight tooAzure Data Lake Store](https://mix.office.com/watch/l93xri2yhtp2)
* [Toegang tot Azure Data Lake Store via Hive en Pig](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [DistCp (Hadoop Distributed Copy) toocopy gegevens tooand gebruiken uit Azure Data Lake Store](https://mix.office.com/watch/1liuojvdx6sie)
* [Apache Sqoop toomove gegevens tussen relationele bronnen en Azure Data Lake Store gebruiken](https://mix.office.com/watch/1butcdjxmu114)
* [Organisatie van gegevens met behulp van Azure Data Factory voor Azure Data Lake Store](https://mix.office.com/watch/1oa7le7t2u4ka)
* [De beveiliging van gegevens in hello Azure Data Lake Store](https://mix.office.com/watch/1q2mgzh9nn5lx)

