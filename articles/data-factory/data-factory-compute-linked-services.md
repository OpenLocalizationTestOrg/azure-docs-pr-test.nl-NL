---
title: aaaCompute omgevingen wordt ondersteund door Azure Data Factory | Microsoft Docs
description: Meer informatie over de compute-omgevingen die u in Azure Data Factory-pijplijnen (zoals Azure HDInsight) tootransform of proces-gegevens gebruiken kunt.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>COMPUTE omgevingen wordt ondersteund door Azure Data Factory
Dit artikel wordt uitgelegd verschillende berekeningsomgevingen tooprocess gebruiken of gegevens transformeren. Het bevat ook informatie over verschillende configuraties (op aanvraag versus bring uw eigen) die door Data Factory worden ondersteund bij het configureren van de gekoppelde services koppelt deze compute omgevingen tooan Azure-gegevensfactory.

Hallo bevat volgende tabel een overzicht van compute-omgevingen wordt ondersteund door de Data Factory en Hallo activiteiten die kunnen worden uitgevoerd op deze. 

| Compute-omgeving | activities |
| --- | --- |
| [HDInsight-cluster op aanvraag](#azure-hdinsight-on-demand-linked-service) of [uw eigen HDInsight-cluster](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop-Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Machine Learning-activiteiten: batchuitvoering en resources bijwerken](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics-linked-service) |[Data Lake Analytics U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL datawarehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Opgeslagen procedure](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Ondersteunde versies van HDInsight in Azure Data Factory
Azure HDInsight biedt ondersteuning voor meerdere versies van Hadoop-cluster die op elk gewenst moment kunnen worden geïmplementeerd. Elke versie keuze maakt een specifieke versie van de distributie van Hallo Hortonworks Data Platform HDP () en een reeks onderdelen die deel uitmaken van dit distributiepunt. Microsoft houdt Hallo lijst met ondersteunde versies van HDInsight tooprovide nieuwste Hadoop-ecosysteem onderdelen en correcties bijgewerkt. Hallo HDInsight 3.2 is op 1 April 2017 afgeschaft. Zie voor gedetailleerde informatie [ondersteunde versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Dit heeft gevolgen voor bestaande Azure Data Factory activiteiten uitgevoerd tegen 3.2 HDInsight-clusters. We raden u aan gebruikers toofollow Hallo richtlijnen in de volgende sectie tooupdate Hallo Hallo betrokken Data Factory:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Voor de gekoppelde Services aan te wijzen tooyour eigen HDInsight-clusters
* **Gekoppelde Services van HDInsight tooyour wijzen eigenaar HDInsight 3.2 of hieronder clusters:**

  Azure Data Factory ondersteunt verzenden taken tooyour eigen HDInsight-clusters van HDI 3.1 te[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). U kunt echter niet langer maken 3.2 HDInsight-cluster na 1 April 2017 op basis van Hallo afschaffing beleid gedocumenteerd in [ondersteunde versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Aanbevelingen:** 
  * Uitvoeren van tests tooensure Hallo compatibiliteit Hallo activiteiten die deze gekoppelde Services te verwijzen naar[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) met gegevens die worden beschreven in [beschikbaar met Hadoop-onderdelen verschillende versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) en [Hortonworks release-opmerkingen die zijn gekoppeld aan de versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Uw HDInsight-3.2-cluster te upgraden[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Hallo nieuwste onderdelen voor Hadoop-ecosysteem en oplossingen. 

* **Gekoppelde Services van HDInsight tooyour wijzen eigenaar HDInsight 3.3 of hoger clusters:**

  Azure Data Factory ondersteunt verzenden taken tooyour eigen HDInsight-clusters van HDI 3.1 te[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Aanbevelingen:** 
  * Er is geen actie vereist vanuit het perspectief van de Data Factory. Echter, als u zich op een lagere versie van HDInsight, nog steeds aangeraden te[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Hallo nieuwste onderdelen voor Hadoop-ecosysteem en oplossingen.

### <a name="for-hdinsight-on-demand-linked-services"></a>Voor HDInsight On-Demand gekoppelde Services
* **Versie 3.2 of hieronder is opgegeven in HDInsight On Demand gekoppelde Services JSON-definitie:**
  
  Azure Data Factory wordt ondersteuning voor het maken van On-Demand HDInsight-clusters van versie 3.3 of meer objecten uit **15-05/2017** en hoger. En Hallo einde van ondersteuning voor bestaande op aanvraag HDInsight 3.2 gekoppelde services te wordt uitgebreid**15-07/2017**.  

  **Aanbevelingen:** 
  * Uitvoeren van tests tooensure Hallo compatibiliteit Hallo activiteiten die deze gekoppelde Services te verwijzen naar [Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) met gegevens die worden beschreven in [beschikbaar met Hadoop-onderdelen verschillende versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) en [Hortonworks release-opmerkingen die zijn gekoppeld aan de versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Voordat u **15-07/2017**, Hallo versie eigenschap in op aanvraag HDI gekoppelde Service JSON-definitie bijwerken[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Hallo nieuwste Hadoop-ecosysteem onderdelen en corrigeert. Raadpleeg voor gedetailleerde JSON-definitie toohello [Azure HDInsight On Demand Linked Service voorbeeld](#azure-hdinsight-on-demand-linked-service). 

* **De versie niet is opgegeven in de On-Demand HDInsight gekoppelde Services:**
  
  Azure Data Factory wordt ondersteuning voor het maken van HDInsight-clusters op aanvraag van versie 3.3 of meer objecten uit **15-05/2017** en hoger. En het Hallo-einde van ondersteuning tooexisting op aanvraag HDInsight 3.2 gekoppelde services te uitgebreid**15-07/2017**. 

  Voordat u **15-07/2017**, als dit leeg laat, Hallo standaardwaarden voor versie en eigenschappen voor het besturingssysteemtype zijn: 

  | Eigenschap | Standaardwaarde | Vereist |
  | --- | --- | --- |
  Versie   | HDI 3.1 voor Windows-cluster en HDI 3.2 voor Linux-cluster.| Nee
  besturingssysteemtype | Hallo standaardwaarde is Windows | Nee

  Na **15-07/2017**, als dit leeg laat, Hallo standaardwaarden voor versie en eigenschappen voor het besturingssysteemtype zijn:

  | Eigenschap | Standaardwaarde | Vereist |
  | --- | --- | --- |
  Versie   | 3.3 HDI voor Windows-cluster en 3.5 voor Linux-cluster.    | Nee
  besturingssysteemtype | Hallo standaardwaarde is Linux   | Nee

  **Aanbevelingen:** 
  * Voordat u **15-07/2017**, uitvoeren van tests tooensure Hallo compatibiliteit Hallo activiteiten die deze gekoppelde Services te verwijzen naar[Hallo laatste ondersteund HDInsight versie](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) met informatie beschreven in [Hadoop-onderdelen met verschillende versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) en [Hortonworks release-opmerkingen die zijn gekoppeld aan de versies van HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Na **15-07/2017**, zorg ervoor dat u expliciet besturingssysteemtype en versie waarden opgeven als u toooverride Hallo standaardinstellingen wilt. 

>[!Note]
>Azure Data Factory biedt momenteel geen ondersteuning voor HDInsight-clusters met behulp van Azure Data Lake Store als primaire archief. Azure Storage gebruiken als primaire winkel voor HDInsight-clusters. 
>  
>  

## <a name="on-demand-compute-environment"></a>Op aanvraag compute-omgeving
In dit type configuratie, wordt de computeromgeving Hallo volledig beheerd door hello Azure Data Factory-service. Het is automatisch gemaakt door Hallo Data Factory-service voordat u een taak wordt verzonden tooprocess gegevens en verwijderd wanneer het Hallo-taak is voltooid. U kunt een gekoppelde service voor Hallo op aanvraag compute-omgeving maken, configureren en gedetailleerde instellingen voor het uitvoeren van taak Clusterbeheer en acties uitvoeren van de bootstrap beheren.

> [!NOTE]
> Hallo-op-verzoek-configuratie wordt momenteel alleen ondersteund voor Azure HDInsight-clusters.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight On-Demand gekoppelde Service
Hello Azure Data Factory-service kan een Windows, Linux-gebaseerde bellen op HDInsight-cluster tooprocess gegevens automatisch worden gemaakt. Hallo-cluster wordt gemaakt in dezelfde regio bevinden als Hallo storage-account (de eigenschap linkedServiceName in Hallo JSON) die zijn gekoppeld aan cluster Hallo Hallo. Hallo storage-account moet een algemeen standaard Azure-opslagaccount. 

Let op de volgende Hallo **belangrijke** punten met betrekking tot HDInsight op aanvraag gekoppelde service:

* U ziet geen Hallo op aanvraag HDInsight-cluster gemaakt in uw Azure-abonnement. Hello Azure Data Factory-service beheert Hallo op demand HDInsight-cluster namens jou.
* Hallo logboeken voor taken die worden uitgevoerd op een op aanvraag HDInsight cluster zijn gekopieerd toohello storage-account gekoppeld Hallo HDInsight-cluster. U kunt deze logboeken openen vanaf hello Azure-portal op Hallo **Details uitvoering van activiteit** blade. Zie [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.
* Worden in rekening gebracht voor Hallo tijd wanneer Hallo HDInsight-cluster is en taken die worden uitgevoerd.

> [!IMPORTANT]
> Het duurt meestal **20 minuten** of meer tooprovision een Azure HDInsight-cluster op aanvraag.
> 
> 

### <a name="example"></a>Voorbeeld
Hallo volgende JSON definieert een service op aanvraag een gekoppelde HDInsight op basis van Linux. Hallo Data Factory-service maakt automatisch een **op basis van Linux** HDInsight-cluster bij het verwerken van een gegevenssegment. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

toouse HDInsight op basis van Windows-cluster instellen **besturingssysteemtype** te**windows** of gebruik geen Hallo eigenschap als standaardwaarde Hallo is: windows.  

> [!IMPORTANT]
> Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment toobe verwerkt moet, tenzij er een bestaand livecluster is (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid. 
> 
> Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers een patroon volgen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.
> 
> 

### <a name="properties"></a>Eigenschappen
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**HDInsightOnDemand**. |Ja |
| De clustergrootte |Aantal knooppunten in cluster Hallo worker/gegevens. Hallo HDInsight-cluster wordt gemaakt met 2 hoofdknooppunten samen met het aantal worker-knooppunten die u voor deze eigenschap opgeeft Hallo. Hallo-knooppunten zijn met een grootte van Standard_D3 met 4 kernen, zodat een cluster met 4 worker-knooppunten 24 kernen duurt (4\*4 = 16 cores voor worker-knooppunten plus 2\*4 = 8 cores voor hoofdknooppunten). Zie [maken Linux gebaseerde Hadoop-clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over Hallo Standard_D3 laag. |Ja |
| TimeToLive |Hallo toegestane niet-actieve tijd voor Hallo bellen op HDInsight-cluster. Hiermee geeft u op hoe lang Hallo bellen op HDInsight-cluster na voltooiing van een activiteit die wordt uitgevoerd als er geen actieve taken in het cluster Hallo actief blijft.<br/><br/>Bijvoorbeeld, als een activiteit die wordt uitgevoerd, 6 minuten en timetolive duurt is ingesteld too5 minuten, Hallo cluster blijft actief gedurende vijf minuten na Hallo 6 minuten van de verwerking van Hallo activiteit die wordt uitgevoerd. Als een andere activiteit die wordt uitgevoerd met Hallo 6 minuten venster wordt uitgevoerd, wordt verwerkt door Hallo hetzelfde cluster.<br/><br/>Maken van een HDInsight-cluster op aanvraag is een dure bewerking (kan even duren), dus gebruik deze instelling als de prestaties van een gegevensfactory nodig tooimprove door een HDInsight-cluster op aanvraag opnieuw te gebruiken.<br/><br/>Als u timetolive waarde too0 instelt, wordt Hallo cluster wordt verwijderd zodra Hallo activiteit die wordt uitgevoerd is voltooid. Dat, als u een hoge waarde instelt, kan Hallo cluster niet-actieve onnodig wat resulteert in hoge kosten blijven. Het is daarom belangrijk dat u Hallo geschikte waarde op basis van uw behoeften.<br/><br/>Als de waarde van de eigenschap timetolive Hallo op de juiste wijze is ingesteld, kunnen meerdere pijplijnen Hallo exemplaar van Hallo bellen op HDInsight-cluster te delen.  |Ja |
| Versie |De versie van Hallo HDInsight-cluster. de standaardwaarde Hallo is 3.1 voor Windows-cluster en 3.2 voor Linux-cluster. |Nee |
| linkedServiceName | Een gekoppelde Azure Storage-service toobe door Hallo op aanvraag cluster gebruikt voor het opslaan en verwerken van gegevens. Hallo HDInsight-cluster wordt gemaakt in Hallo dezelfde regio bevinden als dit Azure Storage-account.<p>Op dit moment kunt maken u een HDInsight-cluster op aanvraag die gebruikmaakt van een Azure Data Lake Store als Hallo opslag niet. Als u toostore Hallo resultaatgegevens uit HDInsight worden verwerkt in een Azure Data Lake Store wilt, gebruikt u een Kopieeractiviteit toocopy Hallo gegevens van hello Azure Blob Storage toohello Azure Data Lake Store. </p>  | Ja |
| additionalLinkedServiceNames |Hiermee geeft u extra opslagaccounts voor Hallo HDInsight gekoppelde service zodat Hallo Data Factory-service namens jou registreren kunt. Deze opslagaccounts moet Hallo dezelfde regio bevinden als de HDInsight-cluster hello, die wordt gemaakt in Hallo dezelfde regio bevinden als Hallo storage-account is opgegeven door linkedServiceName. |Nee |
| besturingssysteemtype |Type besturingssysteem. Toegestane waarden zijn: (standaard) voor Windows en Linux |Nee |
| hcatalogLinkedServiceName |Hallo-naam van de Azure SQL gekoppelde service die punt toohello HCatalog-database. Hallo bellen op HDInsight-cluster is gemaakt met behulp van hello Azure SQL-database als Hallo metastore. |Nee |

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON-voorbeeld

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Geavanceerde eigenschappen
U kunt ook de volgende eigenschappen voor de gedetailleerde configuratie van Hallo bellen op HDInsight-cluster Hallo Hallo opgeven.

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| coreConfiguration |Hiermee geeft u Hallo core configuratieparameters (zoals in core site.xml) voor Hallo HDInsight-cluster toobe gemaakt. |Nee |
| hBaseConfiguration |Hiermee geeft u Hallo HBase configuratieparameters (hbase-site.xml) voor Hallo HDInsight-cluster. |Nee |
| hdfsConfiguration |Hiermee geeft u Hallo HDFS configuratieparameters (hdfs-site.xml) voor Hallo HDInsight-cluster. |Nee |
| hiveConfiguration |Hiermee geeft u Hallo hive configuratieparameters (hive-site.xml) voor Hallo HDInsight-cluster. |Nee |
| mapReduceConfiguration |Hiermee geeft u Hallo MapReduce configuratieparameters (mapred-site.xml) voor Hallo HDInsight-cluster. |Nee |
| oozieConfiguration |Hiermee geeft u Hallo Oozie configuratieparameters (oozie-site.xml) voor Hallo HDInsight-cluster. |Nee |
| stormConfiguration |Hiermee geeft u Hallo Storm configuratieparameters (storm-site.xml) voor Hallo HDInsight-cluster. |Nee |
| yarnConfiguration |Hiermee geeft u Hallo Yarn configuratieparameters (yarn-site.xml) voor Hallo HDInsight-cluster. |Nee |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Voorbeeld: configuratie van de On-demand HDInsight-cluster met geavanceerde eigenschappen

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Knooppuntgrootten
U kunt Hallo grootten van head, gegevens en zookeeper-knooppunten met behulp van de volgende eigenschappen Hallo opgeven: 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| headNodeSize |Hiermee wordt de grootte Hallo van Hallo hoofdknooppunt. de standaardwaarde Hallo is: Standard_D3. Zie Hallo **knooppuntgrootten geven** sectie voor meer informatie. |Nee |
| dataNodeSize |Geeft de grootte Hallo van Hallo gegevensknooppunt. de standaardwaarde Hallo is: Standard_D3. |Nee |
| zookeeperNodeSize |Hiermee wordt de grootte Hallo van Hallo dierenverzorger knooppunt. de standaardwaarde Hallo is: Standard_D3. |Nee |

#### <a name="specifying-node-sizes"></a>Knooppuntgrootten opgeven
Zie Hallo [grootten van virtuele Machines](../virtual-machines/linux/sizes.md) artikel voor tekenreekswaarden u toospecify voor vermeld in de vorige sectie Hallo Hallo-eigenschappen moet. Hallo-waarden moeten tooconform toohello **CMDLETs & API's** waarnaar wordt verwezen in Hallo artikel. Zoals u in Hallo artikel ziet, heeft Hallo gegevensknooppunt met een grootte van de grote (standaard) 7 GB geheugen, wat mogelijk niet goed voor uw scenario. 

Als u toocreate D4 grootte hoofdknooppunten en worker-knooppunten wilt, geef **Standard_D4** als Hallo-waarde voor headNodeSize en dataNodeSize-eigenschappen. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Als u een onjuiste waarde voor deze eigenschappen opgeeft, krijgt u de volgende Hallo **fout:** toocreate-cluster is mislukt. Uitzondering: Kan geen toocomplete Hallo cluster Maakbewerking. Bewerking is mislukt met code 400. Cluster heeft status: 'Fout'. Bericht: 'PreClusterCreationValidationFailure'. Wanneer u deze fout ontvangt, controleert u of u Hallo **CMDLET & API's** naam uit de tabel Hallo in Hallo [grootten van virtuele Machines](../virtual-machines/linux/sizes.md) artikel.  

## <a name="bring-your-own-compute-environment"></a>Breng uw eigen compute-omgeving
Gebruikers kunnen met dit type configuratie, een al bestaande computeromgeving registreren als een gekoppelde service in de Data Factory. Hallo computeromgeving wordt beheerd door de gebruiker Hallo en Hallo Data Factory-service gebruikt deze tooexecute Hallo activiteiten.

Dit type configuratie wordt ondersteund voor Hallo volgende omgevingen COMPUTE:

* Azure HDInsight
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure HDInsight gekoppelde Service
U kunt een gekoppelde HDInsight-service tooregister uw eigen HDInsight-cluster maken met Data Factory.

### <a name="example"></a>Voorbeeld

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Eigenschappen
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**HDInsight**. |Ja |
| clusterUri |Hallo-URI van Hallo HDInsight-cluster. |Ja |
| gebruikersnaam |Geef het Hallo-naam van Hallo gebruiker toobe tooconnect tooan bestaand HDInsight-cluster gebruikt. |Ja |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo opgeven. |Ja |
| linkedServiceName | Naam van Hallo gekoppelde Azure Storage-service die toohello Azure blob-opslag verwijst gebruikt door Hallo HDInsight-cluster. <p>Op dit moment kunt opgeven u niet dat een Azure Data Lake Store gekoppelde service voor deze eigenschap. Als Hallo HDInsight-cluster toegang tot toohello Data Lake Store heeft, kan u toegang tot gegevens in Azure Data Lake Store Hallo van Hive/Pig-scripts. </p>  |Ja |

## <a name="azure-batch-linked-service"></a>Gekoppelde Service van Azure Batch
U kunt een Azure Batch gekoppelde service tooregister een Batch-pool van virtuele machines (VM's) tooa gegevensfactory maken. U kunt aangepaste .NET-activiteiten met behulp van Azure Batch of Azure HDInsight kunt uitvoeren.

Zie de volgende onderwerpen als u nieuwe tooAzure Batch-service:

* [Basisbeginselen van Azure Batch](../batch/batch-technical-overview.md) voor een overzicht van hello Azure Batch-service.
* [Nieuwe AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate Azure Batch-account (of) [Azure-portal](../batch/batch-account-create-portal.md) toocreate hello Azure Batch-account met Azure portal. Zie [met behulp van PowerShell toomanage Azure Batch-Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) onderwerp voor gedetailleerde instructies over het gebruik van Hallo-cmdlet.
* [Nieuwe-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate een Azure Batch-pool.

### <a name="example"></a>Voorbeeld

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Append '**.\< regionaam\>**' toohello-naam van uw batch-account voor Hallo **accountName** eigenschap. Voorbeeld:

```json
"accountName": "mybatchaccount.eastus"
```

Een andere optie is tooprovide hello batchUri eindpunt zoals weergegeven in Hallo voorbeeld te volgen:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Eigenschappen
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**AzureBatch**. |Ja |
| Accountnaam |Naam van hello Azure Batch-account. |Ja |
| accessKey |De toegangssleutel voor hello Azure Batch-account. |Ja |
| Groepsnaam |Naam van het Hallo-pool van virtuele machines. |Ja |
| linkedServiceName |Naam van Hallo gekoppelde Azure Storage-service die is gekoppeld aan deze gekoppelde Azure-Batch-service. Deze gekoppelde service wordt gebruikt voor tijdelijke bestanden toorun Hallo activiteit en opslaan van logboekbestanden voor het uitvoeren van activiteit Hallo vereist. |Ja |

## <a name="azure-machine-learning-linked-service"></a>Azure Machine Learning gekoppelde Service
Hebt u een Azure Machine Learning gekoppelde service tooregister een Machine Learning score-eindpunt tooa data factory.

### <a name="example"></a>Voorbeeld

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Eigenschappen
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Type |Hallo type eigenschap moet worden ingesteld op: **AzureML**. |Ja |
| mlEndpoint |Hallo URL voor batchscores. |Ja |
| apiKey |Hallo gepubliceerde werkruimtemodel op de API. |Ja |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics gekoppelde Service
U maakt een **Azure Data Lake Analytics** gekoppelde service toolink een Azure Data Lake Analytics compute-service tooan Azure data factory. Hallo Data Lake Analytics U-SQL-activiteit in de pijplijn Hallo verwijst toothis gekoppelde service. 

Hallo bevat volgende tabel beschrijvingen van Hallo generieke eigenschappen die worden gebruikt in Hallo JSON-definitie. U kunt verder tussen service-principal en verificatie van gebruikersreferenties.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| **type** |Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeAnalytics**. |Ja |
| **Accountnaam** |Azure Data Lake Analytics-accountnaam. |Ja |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics-URI. |Nee |
| **abonnements-id** |Azure-abonnement-id |Nee (als dit niet is opgegeven, abonnement van Hallo data factory wordt gebruikt). |
| **resourceGroupName** |Naam van een Azure-resourcegroep |Nee (als dit niet is opgegeven, brongroep van Hallo data factory wordt gebruikt). |

### <a name="service-principal-authentication-recommended"></a>Verificatie van de service principal (aanbevolen)
toouse service principal verificatie, de registratie een Toepassingsentiteit in Azure Active Directory (Azure AD) en verleen het Hallo toegang krijgen tot de tooData Lake Store. Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Noteer Hallo waarden, waarin u volgende toodefine Hallo gekoppelde service:
* Toepassings-id
* Sleutel van toepassing 
* Tenant-id

Verificatie van de service-principal door te geven van de volgende eigenschappen hello gebruiken:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **servicePrincipalId** | Geef Hallo van client-id op. | Ja |
| **servicePrincipalKey** | De sleutel van de toepassing hello opgeven. | Ja |
| **tenant** | Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt. U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal. | Ja |

**Voorbeeld: Service-principal-verificatie**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Verificatie van gebruikersreferenties
Ook kunt u verificatie van gebruikersreferenties voor Data Lake Analytics door te geven Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **autorisatie** | Klik op Hallo **autoriseren** knop op Hallo Data Factory-Editor en voer uw referenties die Hallo automatisch gegenereerde autorisatie-URL toothis eigenschap toewijst. | Ja |
| **sessie-id** | OAuth-sessie-ID van Hallo OAuth-autorisatie-sessie. Elke sessie-ID is uniek en kan slechts één keer worden gebruikt. Deze instelling wordt automatisch gegenereerd wanneer u Hallo Data Factory-Editor. | Ja |

**Voorbeeld: Verificatie van gebruikersreferenties**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Verlopen van het token
Hallo autorisatiecode die u hebt gegenereerd met Hallo **autoriseren** knop verloopt na enige tijd opnieuw. Zie de volgende tabel voor Hallo verlopen tijden voor verschillende soorten gebruikersaccounts Hallo. Mogelijk ziet u Hallo volgende foutbericht weergegeven wanneer Hallo verificatie **-token verloopt**: referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties. AADSTS70008: Hallo opgegeven toegangsmachtiging is verlopen of ingetrokken. Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21:09:31Z

| Gebruikerstype | Verloopt na |
|:--- |:--- |
| Gebruikersaccounts die niet worden beheerd door Azure Active Directory (@hotmail.com, @live.com, enz.) |12 uur |
| Gebruikersaccounts die worden beheerd door Azure Active Directory (AAD) |het is 14 dagen na de laatste segment Hallo worden uitgevoerd. <br/><br/>negentig dagen weergegeven, als een segment op basis van de gekoppelde service op basis van OAuth ten minste eenmaal in de 14 dagen wordt uitgevoerd. |

tooavoid/los deze fout, opnieuw autoriseren hello met **autoriseren** wanneer hello **-token verloopt** en implementeer gekoppelde Hallo-service opnieuw. U kunt ook de waarden voor genereren **sessionId** en **autorisatie** eigenschappen programmatisch met code als volgt:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Zie [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [AuthorizationSessionGetResponse klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen voor meer informatie informatie over Hallo Data Factory-klassen in Hallo code gebruikt. Voeg een verwijzing naar: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll voor Hallo WindowsFormsWebAuthenticationDialog klasse. 

## <a name="azure-sql-linked-service"></a>Azure SQL gekoppelde Service
U een Azure SQL gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. Zie [Azure SQL-Connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze gekoppelde service.

## <a name="azure-sql-data-warehouse-linked-service"></a>Azure SQL gekoppelde Service van datawarehouse
U een Azure SQL Data Warehouse gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. Zie [Azure SQL Data Warehouse Connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) voor meer informatie over deze gekoppelde service.

## <a name="sql-server-linked-service"></a>Gekoppelde Service van SQL Server
U een SQL Server gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. Zie [SQL Server-connector](data-factory-sqlserver-connector.md#linked-service-properties) voor meer informatie over deze gekoppelde service.

