---
title: aaaIntegrating Data Lake Store met andere Azure-Services | Microsoft Docs
description: Begrijpen hoe Data Lake Store integreert met andere Azure-services
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Data Lake Store met andere Azure-services integreren
Azure Data Lake Store kan worden gebruikt in combinatie met andere Azure-services tooenable een breed scala aan scenario's. Hallo volgende artikel vindt u Hallo-services die Data Lake Store kan worden geïntegreerd met.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Gebruik Data Lake Store met Azure HDInsight
U kunt inrichten een [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) cluster dat gebruik maakt van Data Lake Store als Hallo HDFS-compatibele opslag. Voor deze release kunt voor Hadoop en Storm-clusters op Windows en Linux, u Data Lake Store als extra opslag alleen. Azure Storage (WASB) dergelijke clusters nog steeds gebruiken als Hallo standaard opslag. Voor HBase-clusters op Windows- en Linux, kunt u Data Lake Store echter gebruiken als Hallo standaard opslag, en/of de extra opslagruimte.

Zie voor instructies over hoe tooprovision een HDInsight-cluster met Data Lake Store.:

* [Een HDInsight-cluster inrichten met Data Lake Store met Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Het inrichten van een HDInsight-cluster met Data Lake Store als standaard opslag met Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Richt een HDInsight-cluster met Data Lake Store als extra opslagruimte met Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Gebruik Data Lake Store met Azure Data Lake Analytics
[Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-overview.md) kunt u toowork met Big Data in de cloud. Dynamisch resources inricht en kunt u doen analytics van terabytes- of zelfs exabytes-aan gegevens die kunnen worden opgeslagen in een aantal ondersteunde gegevensbronnen, een van hen Data Lake Store. Data Lake Analytics is speciaal geoptimaliseerd toowork met Azure Data Lake Store - bieden Hallo hoogste niveau van prestaties, doorvoer en garandeert u big data-werkbelastingen.

Voor instructies over het toouse Data Lake Analytics met Data Lake Store Zie [aan de slag met Data Lake Analytics met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Gebruik Data Lake Store met Azure Data Factory
U kunt [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest gegevens van Azure-tabellen, Azure SQL Database, Azure SQL DataWarehouse, Azure Storage-Blobs en on-premises-databases. Eerste-klas staatsburger in hello Azure ecosysteem kan, Azure Data Factory worden gebruikt tooorchestrate Hallo opname van gegevens uit deze bron tooAzure Data Lake Store.

Voor instructies over hoe toouse Azure Data Factory met Data Lake Store zien [tooand gegevens verplaatsen van Data Lake Store met Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Gegevens kopiëren van Azure Storage-Blobs in Data Lake Store
Azure Data Lake Store biedt een opdrachtregelprogramma, AdlCopy, waarmee u gegevens uit Azure Blob Storage toocopy naar een Data Lake Store-account. Zie voor meer informatie [gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Gegevens worden gekopieerd tussen Azure SQL Database- en Data Lake Store
U kunt tooimport Apache Sqoop gebruiken en exporteren van gegevens tussen Azure SQL Database- en Data Lake Store. Zie voor meer informatie [kopiëren van gegevens tussen Data Lake Store en Azure SQL database met behulp van Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Gebruik Data Lake Store met Stream Analytics
U kunt Data Lake Store kunt gebruiken, zoals een Hallo gestreamd met Azure Stream Analytics toostore-gegevens levert. Zie voor meer informatie [Stream gegevens uit Azure Storage-Blob in Data Lake Store met Azure Stream Analytics](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Gebruik Data Lake Store met Power BI
U kunt Power BI tooimport gegevens uit een Data Lake Store-account tooanalyze gebruiken en Hallo gegevens visualiseren. Zie voor meer informatie [analyseren van gegevens in Data Lake Store met Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Gebruik Data Lake Store met Data Catalog
U kunt gegevens in Data Lake Store in Azure Data Catalog toomake Hallo gegevens kunnen worden gedetecteerd in de gehele organisatie Hallo Hallo registreren. Zie voor meer informatie [gegevens van Data Lake Store registreren in Azure Data Catalog](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Gebruik Data Lake Store met SQL Server integratieservices (SSIS)
U kunt hello Azure Data Lake Store-Verbindingsbeheer gebruiken in SSIS tooconnect een SSIS-pakket met Azure Data Lake Store. Zie voor meer informatie [gebruik Data Lake Store met SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Gebruik Data Lake Store met SQL datawarehouse
U kunt PolyBase tooload gegevens uit Azure Data Lake Store in SQL Data Warehouse. Zie voor meer informatie [gebruik Data Lake Store met SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [Aan de slag met Data Lake Store met de Portal](data-lake-store-get-started-portal.md)
* [Aan de slag met Data Lake Store met behulp van PowerShell](data-lake-store-get-started-powershell.md)  

