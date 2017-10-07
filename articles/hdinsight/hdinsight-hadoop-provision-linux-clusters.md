---
title: setup aaaCluster voor Hadoop, Spark, HBase, Kafka of R Server - Azure HDInsight | Microsoft Docs
description: Instellen van Hadoop, Kafka, Spark, HBase, R Server of Storm-clusters voor HDInsight vanuit een browser, hello Azure CLI, Azure PowerShell, REST of SDK.
keywords: setup van hadoop-cluster, kafka configuratie van een cluster, spark-cluster setup, wat is hadoop-cluster
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Clusters in HDInsight met Hadoop, Spark en Kafka instellen

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Meer informatie over hoe tooset boven en clusters in HDInsight met Hadoop, Spark, Kafka, interactieve Hive, HBase, R Server of Storm configureren. Ook informatie over hoe toocustomize-clusters en beveiliging toevoegen door ze te verbinden tooa domein.

Een Hadoop-cluster bestaat uit meerdere virtuele machines (knooppunten) die worden gebruikt voor gedistribueerde verwerking van taken. Azure HDInsight verwerkt implementatiegegevens van de installatie en configuratie van afzonderlijke knooppunten, hoeft u alleen tooprovide Algemeen configuratie-informatie. 

> [!IMPORTANT]
>HDInsight-cluster omdat facturering begint zodra een cluster wordt gemaakt en stopt wanneer het Hallo-cluster is verwijderd. Facturering is pro rato per minuut, dus u uw cluster altijd verwijderen moet wanneer deze niet langer in gebruik. Meer informatie over hoe te[verwijderen van een cluster.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Cluster setup-methoden
Hallo volgende tabel toont Hallo verschillende methoden dat kunt u tooset van een HDInsight-cluster.

| Clusters die zijn gemaakt met | Webbrowser | Opdrachtregel | REST API | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Azure Portal](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Azure-CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Azure Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Snelle invoer: Basic clusterinstallatie
Dit artikel begeleidt u bij de instellingen in Hallo [Azure-portal](https://portal.azure.com), waarin kunt u een HDInsight-cluster gebruikt *snelle invoer* of *aangepaste*. 

Volg de instructies op Hallo scherm toodo een basic clusterinstallatie duurt. Details worden hieronder:

* [De naam van resourcegroep](#resource-group-name)
* [Clustertypen en configuratie](#cluster-types) 
* [Cluster-aanmelding en SSH-gebruikersnaam](#cluster-login-and-ssh-username)
* [Locatie](#location)

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [HDInsight 3.3 buiten gebruik stellen](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>De naam van resourcegroep 

[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) helpt u werkt met Hallo resources in uw toepassing als een groep waarnaar wordt verwezen tooas een Azure-resourcegroep. U kunt implementeren, bijwerken, bewaken of verwijderen van alle Hallo resources voor uw toepassing in een enkele, gecoördineerde bewerking.

## <a name="cluster-types"></a>Clustertypen en configuratie
Azure HDInsight biedt momenteel Hallo volgende cluster typen, elk met een reeks onderdelen tooprovide bepaalde functionaliteiten.

> [!IMPORTANT]
> HDInsight-clusters zijn beschikbaar in verschillende typen, elk voor een enkele workload of technologie. Er is geen ondersteunde methode toocreate van een cluster waarin meerdere typen zoals Storm en HBase op één cluster. Als uw oplossing technologieën die worden verdeeld over meerdere HDInsight-clustertypen vereist een [virtuele Azure-netwerk](https://docs.microsoft.com/azure/virtual-network) verbinding kunnen maken van clustertypen Hallo vereist. 
>
>

| Clustertype | Functionaliteit |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Batch-query's en analyse van opgeslagen gegevens |
| [HBase](hdinsight-hbase-overview.md) |Voor grote hoeveelheden schemaloos, NoSQL-gegevens verwerken |
| [Storm](hdinsight-storm-overview.md) |Gebeurtenissen in realtime verwerken |
| [Spark](hdinsight-apache-spark-overview.md) |In-memory verwerking, interactieve query's micro batch stroom verwerken |
| [Kafka (preview)](hdinsight-apache-kafka-introduction.md) | Een gedistribueerde streaming-platform die gebruikt toobuild realtime streaming gegevens pipelines en toepassingen worden kan |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Diverse big data-statistieken, voorspellende modellen en machine learning-mogelijkheden |
| [Interactieve Hive (Preview)](hdinsight-hadoop-use-interactive-hive.md) |In-memory caching voor interactieve en sneller Hive-query 's |

### <a name="number-of-nodes-for-each-cluster-type"></a>Het aantal knooppunten voor elk clustertype
Elk clustertype heeft een eigen aantal knooppunten, terminologie voor knooppunten en standaard VM-grootte. In Hallo volgende tabel, is het aantal knooppunten voor elk knooppunttype Hallo tussen haakjes.

| Type | Knooppunten | Diagram |
| --- | --- | --- |
| Hadoop |Hoofdknooppunt (2), gegevensknooppunt (1 +) |![Clusterknooppunten HDInsight Hadoop](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |HEAD-server (2), de regio-server (1 +) master/ZooKeeper-knooppunt (3) |![Clusterknooppunten HDInsight HBase](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nimbus-knooppunt (2), supervisor server (1 +), ZooKeeper-knooppunt (3) |![HDInsight Storm clusterknooppunten](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Hoofdknooppunt (2), werkrolknooppunt (1 +), ZooKeeper-knooppunt (3) (gratis voor A1 ZooKeeper VM-grootte) |![HDInsight Spark clusterknooppunten](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Zie voor meer informatie [standaard configuratie en de virtuele machine knooppuntgrootten voor clusters](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) in "What are Hallo Hadoop-onderdelen en -versies in HDInsight?"

### <a name="hdinsight-version"></a>HDInsight-versie
Selecteer Hallo-versie van HDInsight voor dit cluster. Zie voor meer informatie [versies van HDInsight ondersteund](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Cluster-laag: Servicelagen HDInsight

Azure HDInsight biedt Hallo big data-oplossingen voor cloud in twee Servicelagen: Standard en Premium.  Zie voor meer informatie [HDInsight Standard en HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Hallo toont volgende schermafbeelding hello Azure portal-informatie voor het kiezen van de clustertypen.

![HDInsight premium configuratie](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Cluster-aanmelding en SSH-gebruikersnaam
Met HDInsight-clusters, kunt u twee gebruikersaccounts configureren tijdens het maken van het cluster:

* HTTP-gebruiker: Hallo standaardgebruikersnaam is *admin*. Hallo-basisconfiguratie wordt gebruikt op Hallo Azure-portal. Dit wordt wel "Cluster gebruiker."
* SSH-gebruiker (Linux-clusters): gebruikte tooconnect toohello cluster via SSH. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

## <a name="location"></a>Locatie (regio's) voor clusters en opslag

Hoeft u niet toospecify Hallo cluster locatie expliciet: Hallo Hallo cluster wordt dezelfde locatie als Hallo standaard opslag. Voor een lijst met ondersteunde regio's, klikt u op Hallo **regio** vervolgkeuzelijst op [HDInsight prijzen](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Opslag-eindpunten voor clusters

Hoewel een lokale installatie van Hadoop hello Hadoop Distributed File System (HDFS) voor opslag op Hallo cluster gebruikt, in Hallo verbonden cloud u opslag eindpunten toocluster. HDInsight-clusters gebruiken [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) of [blobs in Azure Storage](hdinsight-hadoop-use-blob-storage.md). Azure Storage of de Data Lake Store gebruikt, dat kunt u veilig verwijderen Hallo HDInsight-clusters gebruikt voor berekeningen terwijl uw gegevens blijven behouden. 

> [!WARNING]
> Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.

Tijdens de configuratie voor Hallo opslag standaardeindpunt geeft u een blob-container van een Azure Storage-account of een Data Lake Store. Hallo standaard storage bevat toepassings- en Logboeken. Desgewenst kunt u aanvullende gekoppelde Azure Storage-accounts en Data Lake Store-accounts die Hallo cluster toegang hebben. Hallo HDInsight-cluster en het Hallo afhankelijke storage accounts moeten in Hallo dezelfde Azure-locatie.

![Instellingen voor de opslag van cluster: HDFS-compatibele eindpunten van opslag](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Optionele metastores
U kunt optioneel Hive of Oozie metastores kunt maken. Niet alle clustertypen ondersteunen metastores echter en Azure SQL Data Warehouse is niet compatibel met metastores. 

> [!IMPORTANT]
> Wanneer u een aangepaste metastore maakt, gebruik geen streepjes, streepjes of spaties in Hallo databasenaam. Hierdoor kan Hallo cluster maken van het proces toofail.

### <a name="use-hiveoozie-metastore"></a>Hive-metastore

Als u tooretain uw Hive-tabellen wilt nadat u een HDInsight-cluster hebt verwijderd, gebruikt u een aangepaste metastore. Vervolgens koppelt u Hallo metastore tooanother HDInsight-cluster.

Een HDInsight-metastore die is gemaakt voor een HDInsight-cluster versie kan niet worden gedeeld tussen verschillende versies van HDInsight-cluster. Zie voor een lijst met versies van HDInsight, [versies van HDInsight ondersteund](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Oozie-metastore

tooincrease prestaties bij gebruik van Oozie, gebruikt u een aangepaste metastore. Een metastore biedt ook toegang tot tooOozie taakgegevens nadat u uw cluster hebt verwijderd. 

> [!IMPORTANT]
> U kunt een aangepaste Oozie-metastore niet opnieuw gebruiken. een aangepaste Oozie-metastore toouse, moet u de een leeg Azure SQL Database opgeven bij het maken van Hallo HDInsight-cluster.

## <a name="configure-cluster-size"></a>De clustergrootte van het configureren

U wordt gefactureerd voor gebruik van knooppunt voor zolang Hallo cluster bestaat. Omdat facturering begint wanneer een cluster wordt gemaakt en stopt wanneer het Hallo-cluster is verwijderd. Clusters niet ongedaan worden toegewezen of in de wachtstand plaatsen.

Hallo kosten van het HDInsight-clusters wordt bepaald door Hallo aantal knooppunten en grootten van virtuele machines Hallo voor Hallo knooppunten. 

Verschillende clustertypen hebben verschillende knooppunttypen, aantal knooppunten en knooppuntgrootten:
* Standaardtype voor Hadoop-cluster: 
    * Twee *hoofdknooppunten*  
    * Vier *gegevensknooppunten*
* Standaardtype storm-cluster: 
    * Twee *Nimbus-knooppunten*
    * Drie *ZooKeeper-knooppunten*
    * Vier *supervisor knooppunten* 

Als u alleen uit HDInsight probeert, raden wij dat u één gegevensknooppunt gebruiken. Zie voor meer informatie over prijzen voor HDInsight [HDInsight prijzen](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> limiet voor de clustergrootte Hallo verschilt per Azure-abonnementen. Neem contact op met [ondersteuning voor facturering aan Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease Hallo limiet.
>

Wanneer u hello Azure portal tooconfigure Hallo cluster gebruikt, de grootte van de Hallo-knooppunt is beschikbaar via Hallo **knooppunt Prijscategorieën** blade. In de portal hello, ziet u ook kosten in verband met de verschillende knooppuntgrootten Hallo Hallo. 

![HDInsight VM knooppuntgrootten](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Grootten van virtuele machines 
Wanneer u clusters implementeert, kiest u rekenresources die zijn gebaseerd op Hallo-oplossing u van plan bent toodeploy. Hallo die volgende virtuele machines worden gebruikt voor HDInsight-clusters:
* A en D1 4 reeks VMs: [General-purpose Linux VM-grootten](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* D11 14 reeks VM: [geoptimaliseerd voor geheugen Linux VM-grootten](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind uit welke u waarde moet gebruiken toospecify tijdens het maken van een cluster met een VM-grootte Hallo verschillende SDK's of tijdens het gebruik van Azure PowerShell, Zie [VM-groottes toouse voor HDInsight-clusters](../cloud-services/cloud-services-sizes-specs.md#size-tables). In dit artikel gekoppelde, gebruikt u Hallo waarde in Hallo **grootte** kolom met tabellen Hallo.

> [!IMPORTANT]
> Als u meer dan 32 worker-knooppunten in een cluster, moet u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.
>
>

Zie voor meer informatie [grootten voor virtuele machines](../virtual-machines/windows/sizes.md). Zie voor meer informatie over prijzen Hallo verschillende grootten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Aangepaste installatie
Aangepaste cluster setup bouwt voort op Hallo snelle instellingen maken en voegt Hallo volgende opties:
- [HDInsight-toepassingen](#hdinsight-applications)
- [De clustergrootte van het](#cluster-size)
- Geavanceerde instellingen
  - [Scriptacties](#customize-clusters-using-script-action)
  - [Virtueel netwerk](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>HDInsight-toepassingen installeren op clusters

Een HDInsight-toepassing is een toepassing die gebruikers kunnen installeren op een op Linux gebaseerd HDInsight-cluster. U kunt toepassingen gebruiken, mits door Microsoft, derden of die u zelf. Zie voor meer informatie [Hadoop-toepassingen van derden installeren op Azure HDInsight](hdinsight-apps-install-applications.md).

De meeste Hallo HDInsight-toepassingen zijn geïnstalleerd op een lege edge-knooppunt.  Een leeg edge-knooppunt is een virtuele Linux-machine Hello hulpprogramma's voor dezelfde client geïnstalleerd en geconfigureerd zoals Hallo hoofdknooppunt in. U kunt Hallo edge-knooppunt gebruiken voor toegang tot cluster hello, testen van uw clienttoepassingen en die als host fungeert voor uw clienttoepassingen. Zie voor meer informatie [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Geavanceerde instellingen: Script acties

U kunt extra onderdelen installeren of clusterconfiguratie aanpassen met behulp van scripts tijdens het maken van. Deze scripts worden aangeroepen **scriptactie**, dit is een configuratieoptie die kan worden gebruikt vanuit hello Azure-portal, HDInsight Windows PowerShell-cmdlets of Hallo HDInsight .NET SDK. Zie voor meer informatie [aanpassen HDInsight-cluster via scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

Sommige systeemeigen Java-onderdelen, zoals Mahout en trapsgewijze, kunnen worden uitgevoerd op Hallo cluster als Java-archief (JAR)-bestanden. Deze JAR-bestanden kunnen gedistribueerde tooAzure opslag en tooHDInsight clusters met Hadoop taak verzending mechanismen verzonden. Zie voor meer informatie [Hadoop verzenden via een programma taken](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> Als u problemen met het implementeren van de JAR-bestanden tooHDInsight clusters hebt, of het aanroepen van de JAR-bestanden op HDInsight-clusters, neem contact op met [Microsoft Support](https://azure.microsoft.com/support/options/).
>
> Trapsgewijze bewerking wordt niet ondersteund door HDInsight en is niet in aanmerking komen voor Microsoft Support. Zie voor een lijst met ondersteunde onderdelen, [wat is er nieuw in Hallo-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).
>
>

Soms wilt u tooconfigure Hallo configuratiebestanden tijdens het maken van een hello te volgen:

* clusterIdentity.xml
* Core-site.xml
* gateway.XML
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Zie voor meer informatie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Geavanceerde instellingen: clusters met een virtueel netwerk uitbreiden
Als uw oplossing technologieën die worden verdeeld over meerdere HDInsight-clustertypen vereist een [virtuele Azure-netwerk](https://docs.microsoft.com/azure/virtual-network) verbinding kunnen maken van clustertypen Hallo vereist. Deze configuratie toestaat Hallo-clusters en alle code die u implementeert toothem, toodirectly met elkaar communiceren.

Zie voor meer informatie over het gebruik van een virtuele Azure-netwerk met HDInsight [HDInsight uitbreiden met virtuele netwerken van Azure](hdinsight-extend-hadoop-virtual-network.md).

Zie voor een voorbeeld van het gebruik van twee clustertypen binnen een virtuele Azure-netwerk [analyseren van sensorgegevens met Storm en HBase](hdinsight-storm-sensor-data-analysis.md). Zie voor meer informatie over het gebruik van HDInsight met een virtueel netwerk, met inbegrip van specifieke configuratievereisten voor het virtuele netwerk hello, [mogelijkheden uitbreiden HDInsight met behulp van Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Besturingselement toegangsproblemen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

- [Wat zijn HDInsight Hadoop-ecosysteem Hallo en Hadoop-clusters?](hdinsight-hadoop-introduction.md)
- [Aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Werken in Hadoop in HDInsight via Windows-PC](hdinsight-hadoop-windows-tools.md)
