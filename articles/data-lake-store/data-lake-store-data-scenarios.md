---
title: aaaData scenario's met betrekking tot Data Lake Store | Microsoft Docs
description: Hallo verschillende scenario's en hulpprogramma's met behulp van welke gegevens kunnen begrijpen ingenomen, verwerkt, gedownload en weergegeven in een Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Met behulp van Azure Data Lake Store voor big data-vereisten
Er zijn vier belangrijke fasen in grote gegevensverwerking:

* Het opnemen van grote hoeveelheden gegevens in een gegevensarchief aan realtime of in batches
* Hallo verwerken van gegevens
* Hallo gegevens downloaden
* Hallo-gegevens te visualiseren

In dit artikel kijken we deze fasen met opzicht tooAzure Data Lake Store toounderstand Hallo opties en hulpprogramma's beschikbaar toomeet de behoeften van uw big data.

## <a name="ingest-data-into-data-lake-store"></a>Opnemen van gegevens in Data Lake Store
Deze sectie worden de verschillende bronnen Hallo van gegevens en Hallo verschillende manieren waarop die gegevens naar een Data Lake Store-account mag worden ingenomen.

![Opnemen van gegevens in Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "opnemen van gegevens in Data Lake Store")

### <a name="ad-hoc-data"></a>Ad-hoc gegevens
Dit staat voor kleinere gegevenssets die worden gebruikt voor het maken van een prototype een big data-toepassing. Er zijn verschillende manieren van ad-hoc gegevens afhankelijk van Hallo gegevensbron Hallo opnemen.

| Gegevensbron | Met behulp van opnemen |
| --- | --- |
| Lokale computer |<ul> <li>[Azure Portal](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Azure platformoverschrijdende CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Met behulp van Data Lake Tools voor Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Azure Storage-Blob |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[AdlCopy hulpprogramma](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp uitgevoerd op HDInsight-cluster](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Gestroomde gegevens
Hiermee worden gegevens die kunnen worden gegenereerd met verschillende bronnen zoals toepassingen, apparaten, sensoren, enzovoort. Deze gegevens kan door verschillende hulpprogramma's in een Data Lake Store worden ingenomen. Deze hulpprogramma's worden meestal vastleggen en verwerken Hallo gegevens op basis van door gebeurtenis in realtime, en schrijf vervolgens Hallo gebeurtenissen in batches in Data Lake Store zodat ze verder kunnen worden verwerkt.

Hieronder vindt u hulpprogramma's die u kunt gebruiken:

* [Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -gebeurtenissen ingenomen in Event Hubs kunnen worden geschreven tooAzure Data Lake met behulp van de uitvoer van een Azure Data Lake Store.
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -kunt u gegevens direct tooData Lake Store uit Hallo Storm-cluster.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – u kunt ontvangen van gebeurtenissen van Event Hubs en vervolgens het tooData Lake Store met schrijven Hallo [Data Lake Store .NET SDK](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Relationele gegevens
U kunt ook brongegevens van relationele databases. Gedurende een periode verzamelen relationele databases van grote hoeveelheden gegevens die belangrijke inzichten bieden kan als verwerkt via een pijplijn big data. U kunt Hallo toomove in hulpprogramma's na dergelijke gegevens in Data Lake Store.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Web server-logboekgegevens (uploaden met behulp van aangepaste toepassingen)
Dit type dataset wordt specifiek genoemd, omdat analyse van de logboekgegevens van web server een algemene gebruiksvoorbeeld voor big data-toepassingen is en grote hoeveelheden logboek bestanden toobe geüpload toohello Data Lake Store is vereist. U kunt een van de volgende hulpprogramma's voor toowrite Hallo uw eigen tooupload scripts of toepassingen die gegevens.

* [Azure platformoverschrijdende CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake Store .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

Voor het uploaden van web server-logboekgegevens, en ook voor andere soorten gegevens (bijvoorbeeld sociale patronen gegevens) uploaden, is een goede benadering toowrite uw eigen aangepaste scripts/toepassingen omdat u uw gegevens uploaden onderdeel als onderdeel van flexibiliteit tooinclude Hallo van uw groter big data-toepassing. In sommige gevallen kan deze code Hallo vorm van een script of een eenvoudig opdrachtregelprogramma duren. In andere gevallen mogelijk Hallo code gebruikte toointegrate big gegevensverwerking in een zakelijke toepassing of oplossing.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Gegevens die zijn gekoppeld aan Azure HDInsight-clusters
De meeste HDInsight-clustertypen (Hadoop, HBase, Storm) ondersteuning voor Data Lake Store als een gegevens-opslagplaats. HDInsight-clusters toegang tot gegevens uit Azure Storage BLOB's (WASB). Voor betere prestaties kunt u Hallo gegevens uit WASB kopiëren naar een Data Lake Store-account die is gekoppeld aan het Hallo-cluster. U kunt Hallo extra toocopy Hallo gegevens te volgen.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [AdlCopy-Service](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Gegevens opgeslagen in de on-premises of IaaS Hadoop-clusters
Grote hoeveelheden gegevens kunnen worden opgeslagen in de bestaande Hadoop-clusters, lokaal op machines met HDFS. Hallo Hadoop-clusters mogelijk in een on-premises implementatie of mogelijk binnen een IaaS-cluster in Azure. Er zijn vereisten toocopy dergelijke gegevens tooAzure Data Lake Store voor een eenmalige benadering of op een terugkerende wijze. Er zijn verschillende opties waarmee u tooachieve dit kunt. Hieronder volgt een lijst met alternatieven en Hallo bijbehorende-en nadelen.

| Benadering | Details | Voordelen | Overwegingen |
| --- | --- | --- | --- |
| Gebruik van Azure Data Factory (ADF) toocopy gegevens rechtstreeks vanuit Hadoop clusters tooAzure Data Lake Store |[ADF ondersteunt HDFS als een gegevensbron](../data-factory/data-factory-hdfs-connector.md) |ADF biedt out-of-the-box-ondersteuning voor HDFS en eerste klas end-to-end-beheer en controle |Vereist Data Management Gateway toobe geïmplementeerd lokaal of in Hallo IaaS-cluster |
| Gegevens exporteren uit Hadoop als bestanden. Kopieer Hallo bestanden tooAzure Data Lake Store met geschikt mechanisme. |U kunt kopiëren bestanden tooAzure Data Lake Store gebruiken: <ul><li>[Azure PowerShell voor Windows-besturingssysteem](data-lake-store-get-started-powershell.md)</li><li>[Azure platformoverschrijdende CLI 2.0 voor niet - Windows-besturingssysteem](data-lake-store-get-started-cli-2.0.md)</li><li>Aangepaste app met behulp van een Data Lake Store SDK</li></ul> |Snelle tooget gestart. Aangepaste uploads kunt doen |Meerdere stappen proces waarbij meerdere technologieën. Beheer en controle zal toobe een challenge toenemen via de opgegeven tijd Hallo aangepast aard van Hallo-hulpprogramma 's |
| Distcp toocopy gegevens uit Hadoop tooAzure opslag gebruiken. Gegevens kopiëren van Azure Storage tooData Lake Store met de juiste mechanisme. |U kunt gegevens kopiëren van het gebruik van Azure Storage tooData Lake Store: <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[AdlCopy hulpprogramma](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Apache DistCp uitgevoerd op HDInsight-clusters](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |U kunt de open-source hulpprogramma's gebruiken. |Meerdere stappen proces waarbij meerdere technologieën |

### <a name="really-large-datasets"></a>Grote gegevenssets
Voor het uploaden van gegevenssets die van meerdere terabytes variëren kan met behulp van de hierboven beschreven methoden voor Hallo soms worden langzaam en kostbaar. In dergelijke gevallen kunt u onderstaande Hallo-opties.

* **Met behulp van Azure ExpressRoute**. Azure ExpressRoute kunt u particuliere verbindingen maken tussen Azure-datacenters en infrastructuur on-premises. Dit biedt een betrouwbare optie voor het overbrengen van grote hoeveelheden gegevens. Zie voor meer informatie [Azure ExpressRoute documentatie](../expressroute/expressroute-introduction.md).
* **'Offline' het uploaden van gegevens**. Als u met behulp van Azure ExpressRoute is niet haalbaar om welke reden, kunt u [Azure Import/Export-service](../storage/common/storage-import-export-service.md) tooship harde schijven met uw gegevens tooan Azure-Datacenter. Uw gegevens is de eerste geüploade tooAzure Storage-Blobs. Vervolgens kunt u [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) of [AdlCopy hulpprogramma](data-lake-store-copy-data-azure-storage-blob.md) toocopy gegevens uit Azure Storage Blobs tooData Lake Store.

  > [!NOTE]
  > Tijdens het gebruik van hello Import/Export-service, mag Hallo bestandsgrootten op Hallo schijven dat u tooAzure data verzendt center niet langer dan 195 GB.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Verwerken van gegevens die zijn opgeslagen in Data Lake Store
Zodra het Hallo-gegevens zijn beschikbaar in Data Lake Store kunt u analyse uitvoeren op dat gegevens met behulp van Hallo ondersteund big data-toepassingen is. Op dit moment kunt u Azure HDInsight en Azure Data Lake Analytics toorun gegevens analysis taken op Hallo opgeslagen gegevens in Data Lake Store.

![Gegevens analyseren in Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "analyseren van gegevens in Data Lake Store")

U kunt zoeken op Hallo volgen voorbeelden.

* [Een HDInsight-cluster maken met Data Lake Store als opslag](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Gegevens in Data Lake Store downloaden
U kunt ook toodownload of verplaatsen van gegevens uit Azure Data Lake Store voor scenario's zoals:

* Gegevens tooother opslagplaatsen toointerface met uw bestaande gegevensverwerking pijplijnen verplaatsen. Bijvoorbeeld, u kunt toomove gegevens van Data Lake Store tooAzure SQL-Database of on-premises SQL Server.
* Gegevens tooyour lokale computer voor de verwerking van de IDE-omgevingen tijdens het bouwen van prototypen downloaden.

![Uitgaande gegevens van Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "uitgaande gegevens van Data Lake Store")

In dergelijke gevallen kunt kunt u Hallo volgend opties gebruiken:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

U kunt ook Hallo methoden toowrite na uw eigen script toodownload toepassingsgegevens gebruiken van Data Lake Store.

* [Azure platformoverschrijdende CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake Store .NET SDK](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Visualiseer gegevens in Data Lake Store
U kunt een combinatie van services toocreate visuele weergaven van gegevens die zijn opgeslagen in Data Lake Store.

![Gegevens in Data Lake Store visualiseren](./media/data-lake-store-data-scenarios/visualize-data.png "visualiseren van gegevens in Data Lake Store")

* U kunt starten met behulp van [Azure Data Factory toomove gegevens van Data Lake Store tooAzure SQL Data Warehouse](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Daarna kunt u [Power BI integreren met Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate visuele representatie van Hallo-gegevens.
