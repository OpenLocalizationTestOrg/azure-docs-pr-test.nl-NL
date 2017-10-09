Azure Data Factory ondersteunt Hallo activiteiten voor gegevenstransformatie die kunnen worden toegevoegd toopipelines ofwel afzonderlijk of gekoppeld met een andere activiteit te volgen.

| Activiteiten voor gegevenstransformatie | Compute-omgeving |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Machine Learning-activiteiten: batchuitvoering en resources bijwerken](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [Opgeslagen procedure](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse of SQL Server |
| [Data Lake Analytics U-SQL](../articles/data-factory/data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] of Azure Batch |

> [!NOTE]
> U kunt de MapReduce-activiteit toorun Spark programma's op uw HDInsight Spark-cluster. Zie [Spark-programma's aanroepen vanuit Azure Data Factory](../articles/data-factory/data-factory-spark.md) voor meer informatie.
> U kunt een aangepaste activiteit toorun R scripts maken op uw HDInsight-cluster met R is geïnstalleerd. Zie [R-script uitvoeren met behulp van Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).
> 
> 

