---
title: 'Gegevenstransformatie: De transformatie & verwerken gegevens | Microsoft Docs'
description: Meer informatie over hoe tootransform gegevens of procesgegevens in Azure Data Factory met Hadoop, Machine Learning of Azure Data Lake Analytics.
keywords: gegevenstransformatie, gegevens over het installatieproces, gegevens, transformatieactiviteit transformeren
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Transformeer gegevens in Azure Data Factory
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Opgeslagen procedure](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL](data-factory-usql-activity.md)
> * [Aangepaste .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Overzicht
Dit artikel wordt uitgelegd activiteiten voor gegevenstransformatie in Azure Data Factory kunt tootransform uit te voeren en de onbewerkte gegevens worden verwerkt in de voorspellingen en inzichten. Een transformatieactiviteit wordt uitgevoerd in een computeromgeving zoals Azure HDInsight-cluster of een Azure-Batch. Deze biedt koppelingen tooarticles gedetailleerde informatie over elke transformatieactiviteit.

Data Factory ondersteunt Hallo activiteiten voor gegevenstransformatie die te kunnen worden toegevoegd na[pijplijnen](data-factory-create-pipelines.md) ofwel afzonderlijk of gekoppeld met een andere activiteit.

> [!NOTE]
> Zie voor een overzicht met stapsgewijze instructies [een pijplijn maken met Hive-transformatie](data-factory-build-your-first-pipeline.md) artikel.  
> 
> 

## <a name="hdinsight-hive-activity"></a>HDInsight Hive-activiteit
Hallo HDInsight Hive-activiteit in een Data Factory-pijplijn voert Hive-query's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster. Zie [Hive-activiteit](data-factory-hive-activity.md) voor meer informatie over deze activiteit. 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig-activiteit
Hallo HDInsight Pig-activiteit in een Data Factory-pijplijn voert Pig-query's in uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster. Zie [Pig activiteit](data-factory-pig-activity.md) voor meer informatie over deze activiteit. 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce-activiteit
Hallo HDInsight MapReduce-activiteit in een Data Factory-pijplijn voert MapReduce-programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster. Zie [MapReduce-activiteit](data-factory-map-reduce.md) voor meer informatie over deze activiteit.

## <a name="hdinsight-streaming-activity"></a>HDInsight-streamingactiviteit
Hallo Streaming HDInsight-activiteit in een Data Factory-pijplijn voert Hadoop-Streaming programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster. Zie [HDInsight streamingactiviteit](data-factory-hadoop-streaming-activity.md) voor meer informatie over deze activiteit.

## <a name="hdinsight-spark-activity"></a>HDInsight Spark-activiteit
Hallo HDInsight Spark-activiteit in een Data Factory-pijplijn Spark-programma's op uw eigen HDInsight-cluster wordt uitgevoerd. Zie voor meer informatie [aanroepen Spark-programma's van Azure Data Factory](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Machine Learning-activiteiten
Azure Data Factory kunt u tooeasily maken pijplijnen die gebruikmaken van een gepubliceerde Azure Machine Learning-webservice voor predictive analytics. Met behulp van Hallo [Batchuitvoeringsactiviteit](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) in een Azure Data Factory-pijplijn, kunt u een Machine Learning web service toomake voorspellingen op Hallo-gegevens in een batch aanroept.

Na verloop van tijd invoer Hallo voorspellende modellen in Machine Learning-score experimenten moeten toobe retrained met nieuwe Hallo gegevenssets. Wanneer u klaar bent met de retraining, wilt u tooupdate Hallo score berekenen voor webservice Hello retrained Machine Learning-model. U kunt Hallo [Resourceactiviteit voor Update](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) tooupdate Hallo-webservice met Hallo zojuist getrainde model.  

Zie [gebruiken Machine Learning-activiteiten](data-factory-azure-ml-batch-execution-activity.md) voor meer informatie over deze Machine Learning-activiteiten. 

## <a name="stored-procedure-activity"></a>De activiteit opgeslagen procedure
U kunt activiteit van de SQL Server opgeslagen Procedure hello gebruiken in een Data Factory-pijplijn tooinvoke een opgeslagen procedure in een van volgende gegevensarchieven Hallo: Azure SQL Database, Azure SQL Data Warehouse, SQL Server-Database in uw onderneming of een Azure VM. Zie [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) artikel voor meer informatie.  

## <a name="data-lake-analytics-u-sql-activity"></a>U-SQL-activiteit van Data Lake Analytics
Data Lake Analytics U-SQL-activiteit wordt een U-SQL-script uitgevoerd op een Azure Data Lake Analytics-cluster. Zie [Analytics U-SQL-activiteit gegevens](data-factory-usql-activity.md) artikel voor meer informatie. 

## <a name="net-custom-activity"></a>Aangepaste .NET-activiteit
Als u gegevens op een manier die niet wordt ondersteund door Data Factory tootransform moet, kunt u een aangepaste activiteit maken met uw eigen logica gegevensverwerking en Hallo activiteit in de pijplijn hello gebruiken. U kunt Hallo aangepaste .NET activiteit toorun met behulp van een Azure Batch-service of een Azure HDInsight-cluster configureren. Zie [aangepaste activiteiten gebruiken](data-factory-use-custom-activities.md) artikel voor meer informatie. 

U kunt een aangepaste activiteit toorun R scripts maken op uw HDInsight-cluster met R is geïnstalleerd. Zie [R-script uitvoeren met behulp van Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>COMPUTE-omgevingen
U een gekoppelde service voor Hallo compute-omgeving maken en gebruik vervolgens Hallo gekoppelde service bij het definiëren van een transformatieactiviteit. Er zijn twee soorten berekeningsomgevingen die door Data Factory worden ondersteund. 

1. **On-Demand**: In dit geval Hallo computeromgeving volledig wordt beheerd door de Data Factory. Het is automatisch gemaakt door Hallo Data Factory-service voordat u een taak wordt verzonden tooprocess gegevens en verwijderd wanneer het Hallo-taak is voltooid. U kunt configureren en gedetailleerde Hallo op aanvraag compute-omgeving voor het uitvoeren van taak Clusterbeheer en acties uitvoeren van de bootstrap-instellingen beheren. 
2. **Bring Your Own**: In dit geval kunt u uw eigen computeromgeving (bijvoorbeeld een HDInsight-cluster) registreren als een gekoppelde service in de Data Factory. Hallo computeromgeving wordt beheerd door uzelf en Hallo Data Factory-service gebruikt deze tooexecute Hallo activiteiten. 

Zie [gekoppelde Services berekenen](data-factory-compute-linked-services.md) toolearn artikel over compute services die door Data Factory worden ondersteund. 

## <a name="summary"></a>Samenvatting
Azure Data Factory ondersteunt Hallo activiteiten voor gegevenstransformatie te volgen en Hallo berekeningsomgevingen voor Hallo activiteiten. activiteiten voor gegevenstransformatie Hallo kunnen toegevoegde toopipelines ofwel afzonderlijk of gekoppeld met een andere activiteit.

| Activiteiten voor gegevenstransformatie | Compute-omgeving |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Machine Learning-activiteiten: batchuitvoering en resources bijwerken](data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [Opgeslagen procedure](data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse of SQL Server |
| [Data Lake Analytics U-SQL](data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] of Azure Batch |

