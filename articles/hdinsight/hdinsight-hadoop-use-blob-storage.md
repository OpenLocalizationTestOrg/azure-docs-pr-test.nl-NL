---
title: aaaQuery gegevens uit HDFS-compatibele Azure-opslag - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooquery gegevens uit Azure storage en Azure Data Lake Store toostore resultaten van de analyse.
keywords: blob storage, hdfs, gestructureerde gegevens, ongestructureerde gegevens, data lake store, Hadoop-invoer, Hadoop-uitvoer, hadoop-opslag, hdfs-invoer, hdfs-uitvoer, hdfs-opslag, wasb azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Azure-opslag gebruiken met Azure HDInsight-clusters

tooanalyze gegevens in HDInsight-cluster, kunt u Hallo gegevens in Azure Storage of Azure Data Lake Store opslaan. Beide opties voor opslag kunnen u toosafely verwijdert u het die hdinsight-clusters worden gebruikt voor berekeningen zonder verlies van gebruikersgegevens.

Hadoop ondersteunt een notatie van het standaardbestandssysteem Hallo. Hallo standaardbestandssysteem impliceert een standaardschema en instantie. Het kan ook gebruikte tooresolve relatieve paden zijn. Tijdens het Hallo-proces voor het HDInsight-cluster maken, kunt u een blob-container in Azure Storage als het standaardbestandssysteem Hallo of met HDInsight 3.5, kunt u Azure Storage of Azure Data Lake Store als Hallo bestanden van het systeem met een paar uitzonderingen. Zie voor Hallo ondersteuningsmogelijkheden van het gebruik van Data Lake Store als Hallo standaard en gekoppelde opslag, [beschikbaarheid van HDInsight-cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

In dit artikel wordt uitgelegd hoe Azure Storage werkt met HDInsight-clusters. toolearn hoe Data Lake Store werkt met HDInsight-clusters, Zie [gebruik Azure Data Lake Store met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md). Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.

Azure Storage is een robuuste, algemene opslagoplossing die naadloos kan worden geïntegreerd met HDInsight. HDInsight kunt gebruiken een blob-container in Azure Storage als het standaardbestandssysteem Hallo voor Hallo-cluster. Hallo volledige set onderdelen in HDInsight kan via een Hadoop distributed file system (HDFS)-interface werken rechtstreeks op gestructureerde of ongestructureerde gegevens als blobs worden opgeslagen.

> [!WARNING]
> Er zijn verschillende opties beschikbaar bij het maken van een Azure Storage-account. Hallo volgende tabel bevat informatie over welke opties worden ondersteund met HDInsight:
> 
> | Type opslagaccount | Opslaglaag | Ondersteund met HDInsight |
> | ------- | ------- | ------- |
> | Storage-account voor algemeen gebruik | Standard | __Ja__ |
> | &nbsp; | Premium | Nee |
> | Blob Storage-account | Warm | Nee |
> | &nbsp; | Koud | Nee |

We raden niet Hallo standaard blob-container te gebruiken voor het opslaan van bedrijfsgegevens. Hallo standaard blob-container verwijderen na elke tooreduce gebruik is opslagkosten een goede gewoonte. Opmerking die standaardcontainer Hallo bevat toepassings- en Logboeken. Zorg ervoor tooretrieve Hallo logboeken voordat Hallo container worden verwijderd.

Het delen van een blobcontainer voor meerdere clusters wordt niet ondersteund.

## <a name="hdinsight-storage-architecture"></a>HDInsight-opslagarchitectuur
Hallo volgende diagram biedt een abstracte weergave van Hallo HDInsight-opslagarchitectuur van het gebruik van Azure Storage:

![Hadoop-clusters Hallo HDFS API tooaccess gebruik en opslaan van gestructureerde en ongestructureerde gegevens in Blob-opslag. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight-opslagarchitectuur")

HDInsight biedt toegang toohello distributed file system dat lokaal is gekoppeld toohello rekenknooppunten. Dit bestandssysteem toegankelijk zijn voor het gebruik van volledig gekwalificeerde URI, bijvoorbeeld Hallo:

    hdfs://<namenodehost>/<path>

Bovendien kunt HDInsight u tooaccess gegevens die zijn opgeslagen in Azure Storage. Hallo-syntaxis is:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Hier volgen enkele overwegingen bij het gebruik van een Azure Storage-account met HDInsight-clusters.

* **Containers in opslagaccounts Hallo die verbonden tooa cluster zijn:** omdat het Hallo-accountnaam en de sleutel gekoppeld aan cluster Hallo tijdens het maken zijn, hebt u volledige toegang toohello blobs in deze containers.

* **Openbare containers of openbare blobs in opslagaccounts die niet zijn verbonden tooa cluster:** hebt u alleen-lezen toegang toohello blobs in Hallo-containers.
  
  > [!NOTE]
  > Openbare containers kunt u een lijst met alle blobs die zijn beschikbaar in de container en containermetagegevens tooget. Openbare blobs kunnen u tooaccess Hallo blobs alleen als u Hallo exacte URL weet. Zie voor meer informatie <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">toegang toocontainers en blobs beperken</a>.
  > 
  > 
* **Persoonlijke containers in opslagaccounts die niet verbonden tooa cluster:** Hallo blobs in Hallo containers niet meer toegankelijk tenzij u Hallo opslagaccount definieert wanneer u Hallo WebHCat-taken verzendt. Dit wordt verderop in dit artikel uitgelegd.

Hallo storage-accounts die zijn gedefinieerd in het proces voor het maken van Hallo en de sleutels worden opgeslagen in %HADOOP_HOME%/conf/core-site.xml op Hallo clusterknooppunten. Hallo standaardgedrag van HDInsight is gedefinieerd in de bestand core site.xml Hallo van toouse Hallo storage-accounts. U kunt deze instelling wijzigen instellen met [Ambari](./hdinsight-hadoop-manage-ambari.md)

Meerdere WebHCat-taken, waaronder Hive, MapReduce, Hadoop-streaming en Pig, kunnen een beschrijving van opslagaccounts en metagegevens bevatten. (Dit werkt momenteel voor Pig met opslagaccounts, maar niet voor metagegevens.) Zie [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Een HDInsight-cluster gebruiken met alternatieve opslagaccounts en metastores) voor meer informatie.

Blobs kunnen worden gebruikt voor gestructureerde en ongestructureerde gegevens. De gegevens in blobcontainers worden opgeslagen als sleutel-waardeparen en er is geen maphiërarchie. Maar Hallo slash-teken (/) kan worden gebruikt binnen Hallo toomake van sleutelnaam deze weergegeven als een bestand wordt opgeslagen in een mapstructuur. De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn. Er is niet echt *invoer* directory bestaat, maar vanwege de aanwezigheid van de toohello van Hallo slash-teken in naam van de hello, heeft Hallo vormgeving van een bestandspad.

## <a id="benefits"></a>Voordelen van Azure Storage
Hallo geïmpliceerde kosten als gevolg van elkaar niet plaatsen rekenclusters en opslagbronnen wordt verholpen door Hallo manier Hallo rekenclusters sluiten toohello opslagbronnen account in Azure-regio waar Hallo snel netwerk het maakt Hallo efficiënte rekenknooppunten hello tooaccess Hallo gegevens in Azure storage.

Er zijn enkele voordelen Hallo gegevens opslaan in Azure storage in plaats van HDFS:

* **Gegevens hergebruik en delen:** Hallo-gegevens in HDFS is te vinden in Hallo compute cluster. Alleen Hallo-toepassingen waarvoor toegang toohello compute cluster Hallo gegevens met HDFS API's kunt gebruiken. Hallo-gegevens in Azure storage zijn toegankelijk via Hallo HDFS API's of via Hallo [Blob Storage REST-API's][blob-storage-restAPI]. Dus een grotere set toepassingen (inclusief andere HDInsight-clusters) en hulpprogramma's worden gebruikt tooproduce en Hallo gegevens gebruiken.
* **Gegevensarchivering:** opslaan van gegevens in Azure-opslag kunt Hallo HDInsight-clusters gebruikt voor berekeningen toobe veilig worden verwijderd zonder verlies van gebruikersgegevens.
* **Opslagkosten voor gegevens:** opslaan van gegevens in DFS voor de lange termijn Hallo duurder is dan de Hallo gegevens opslaan in Azure-opslag omdat Hallo kosten van een rekencluster hoger dan Hallo kosten van Azure-opslag is. Bovendien omdat Hallo gegevens geen toobe geladen voor elk rekencluster dat wordt gegenereerd heeft, bespaart u kosten voor het laden van gegevens.
* **Elastisch uitbreiden:** Hoewel HDFS u met een uitgebreid bestandssysteem biedt, Hallo schaal bepaald door Hallo aantal knooppunten dat u voor uw cluster maakt. Hallo schaal wijzigen, kan worden een complexer proces dan te vertrouwen op Hallo elastische schalingsmogelijkheden waarover u automatisch in Azure-opslag.
* **Geo-replicatie:** uw Azure-opslag kan geografisch worden gerepliceerd. Hoewel dit u geografisch herstel en gegevensredundantie biedt, een failover toohello geografisch gerepliceerde locatie grote invloed zijn op de prestaties van uw en deze mogelijk extra kosten. U wordt daarom aangeraden toochoose Hallo geo-replicatie goed en alleen als de waarde Hallo van Hallo gegevens waard Hallo extra kosten.

Bepaalde MapReduce-taken en pakketten kunnen tussenliggende resultaten die u echt toostore in Azure-opslag niet wilt maken. In dat geval kunt u aangeven of toostore Hallo gegevens in Hallo lokale HDFS. HDInsight gebruikt DFS voor verschillende tussenliggende resultaten in Hive-taken en andere processen.

> [!NOTE]
> De meeste HDFS-opdrachten (bijvoorbeeld <b>ls</b>, <b>copyFromLocal</b> en <b>mkdir</b>) blijven gewoon naar verwachting werken. Alleen opdrachten die specifieke toohello systeemeigen HDFS-implementatie (dit is bedoeld tooas DFS), zoals Hallo <b>fschk</b> en <b>dfsadmin</b>, vertonen afwijkend gedrag in Azure storage.
> 
> 

## <a name="create-blob-containers"></a>Blob-containers maken
toouse blobs, maakt u eerst een [Azure Storage-account][azure-storage-create]. Als onderdeel hiervan geeft u een Azure-regio waar Hallo storage-account wordt gemaakt. Hallo-cluster en Hallo storage-account moeten worden gehost in Hallo dezelfde regio. SQL Server-database voor Hallo Hive metastore en Oozie-metastore SQL Server-database ook moet zich bevinden in Hallo dezelfde regio.

Ongeacht de locatie wordt door elke blob die u maakt tooa-container in uw Azure Storage-account hoort. Deze container kan een bestaande blob zijn die buiten HDInsight is gemaakt. Het kan echter ook een container zijn die is gemaakt voor een HDInsight-cluster.

Hallo standaard Blob-container wordt clusterspecifieke informatie zoals de taakgeschiedenis en logboekbestanden opgeslagen. Deel een standaard blob-container niet met meerdere HDInsight-clusters. Hierdoor kan de taakgeschiedenis beschadigd raken. Het verdient aanbeveling toouse een andere container voor elk cluster en de gedeelde gegevens op een gekoppelde storage-account opgegeven in de implementatie van alle relevante clusters in plaats van het standaardopslagaccount Hallo plaatsen. Zie [HDInsight-clusters maken][hdinsight-creation] voor meer informatie over het configureren van gekoppelde opslagaccounts. U kunt een standaardopslagcontainer echter hergebruiken nadat Hallo oorspronkelijke HDInsight-cluster is verwijderd. Voor HBase-clusters, kunt u daadwerkelijk Hallo HBase-tabelschema en gegevens behouden door het maken van een nieuw HBase-cluster met Hallo standaard blob-container die wordt gebruikt door een HBase-cluster dat is verwijderd.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal
Wanneer u een HDInsight-cluster van Hallo Portal maakt, kunt u accountdetails Hallo opties (zoals hieronder wordt weergegeven) tooprovide Hallo opslag hebben. U kunt ook opgeven of u wilt een extra storage-account die is gekoppeld aan het Hallo-cluster, en zo ja, kiezen uit Data Lake Store of een andere Azure Storage-blob als Hallo extra opslagruimte.

![Gegevensbron voor het maken van HDInsight Hadoop](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.


### <a name="use-azure-powershell"></a>Azure PowerShell gebruiken
Als u [geïnstalleerd en geconfigureerd Azure PowerShell][powershell-install], kunt u Hallo van hello Azure PowerShell-prompt toocreate een opslagaccount en container te volgen:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Azure CLI gebruiken

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Als u hebt [geïnstalleerd en geconfigureerd hello Azure CLI](../cli-install-nodejs.md), Hallo volgende opdracht kan worden gebruikt tooa opslagaccount en container.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Hallo `--type` parameter geeft aan hoe Hallo storage-account worden gerepliceerd. Zie [Azure Storage-replicatie](../storage/storage-redundancy.md) voor meer informatie. U kunt ZRS beter niet gebruiken, aangezien ZRS de pagina-blob, het bestand, de tabel of de wachtrij niet ondersteunt.
> 
> 

U bent na vragen aan gebruiker toospecify Hallo geografische regio waarin Hallo storage-account is gemaakt. U kunt Hallo storage-account maken in Hallo dezelfde regio die u van plan bent over het maken van uw HDInsight-cluster.

Zodra het Hallo storage-account is gemaakt, gebruikt u Hallo opdracht tooretrieve hello opslagaccountsleutels te volgen:

    azure storage account keys list <storageaccountname>

toocreate een container Hallo volgende opdracht gebruiken:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Bestanden in Azure Storage adresseren
Hallo-URI-schema voor toegang tot bestanden in Azure storage vanuit HDInsight is:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

Hallo-URI-schema biedt niet-versleutelde toegang (Hello *wasb:* voorvoegsel) en SSL-versleutelde toegang (met *wasbs*). Wordt u aangeraden *wasbs* waar mogelijk, zelfs wanneer toegang tot gegevens die zich in dezelfde regio in Azure Hallo.

Hallo &lt;BlobStorageContainerName&gt; identificeert Hallo-naam van Hallo blob-container in Azure-opslag.
Hallo &lt;StorageAccountName&gt; hello Azure Storage-accountnaam identificeert. Een FQDN (Fully Qualified Domain Name) is vereist.

Als geen van beide &lt;BlobStorageContainerName&gt; noch &lt;StorageAccountName&gt; is opgegeven, Hallo standaardbestandssysteem wordt gebruikt. Hallo-bestanden op het standaardbestandssysteem hello, kunt u een relatief pad of een absoluut pad. Bijvoorbeeld, Hallo *hadoop-mapreduce-examples.jar* -bestand dat wordt geleverd met HDInsight-clusters kan worden waarnaar wordt verwezen tooby met behulp van een van de volgende Hallo:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Hallo-bestandsnaam is <i>hadoop examples.jar</i> in HDInsight versie 2.1- en 1.6-clusters.
> 
> 

Hallo &lt;pad&gt; Hallo bestand of map HDFS-padnaam is. Aangezien containers in Azure Storage gewoon sleutel-waardearchieven zijn, is er geen echt hiërarchisch bestandssysteem. Een slash (/) in een blob-sleutel wordt geïnterpreteerd als een teken voor mapscheiding. Bijvoorbeeld, Hallo blob-naam *hadoop-mapreduce-examples.jar* is:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Als u werkt buiten HDInsight met blobs, hulpprogramma's voor de meeste niet herkent de indeling WASB hello en in plaats daarvan een standaardpadindeling zoals verwacht `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Toegang tot blobs 


### <a name="access-blobs-using-azure-powershell"></a> Azure PowerShell gebruiken
> [!NOTE]
> Hallo-opdrachten in deze sectie bieden een eenvoudige voorbeeld van het gebruik van PowerShell tooaccess gegevens opgeslagen in blobs. Zie voor een uitgebreider voorbeeld dat is aangepast voor het werken met HDInsight hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Gebruik Hallo volgende opdracht toolist Hallo blob-gerelateerde cmdlets:

    Get-Command *blob*

![Lijst met blob-gerelateerde PowerShell-cmdlets.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Bestanden uploaden
Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Bestanden downloaden
Hallo downloadt volgende script een blok-blob toohello huidige map. Voordat Hallo-script wordt uitgevoerd, moet u Hallo tooa map waar u schrijfmachtigingen hebt.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Hallo Resourcegroepnaam en de clusternaam Hallo geven, kunt u Hallo volgende code gebruiken:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Bestanden verwijderen
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Bestanden in een lijst weergeven
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Hive-query's uitvoeren met een niet-gedefinieerd opslagaccount
Dit voorbeeld toont hoe toolist een map van de storage-account is niet gedefinieerd tijdens het creatieproces Hallo.
$clusterName = <HDInsightClusterName>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Azure CLI gebruiken
Gebruik Hallo volgende opdracht toolist Hallo blob-gerelateerde opdrachten:

    azure storage blob

**Voorbeeld van het gebruik van Azure CLI tooupload een bestand**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Voorbeeld van het gebruik van Azure CLI toodownload een bestand**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Voorbeeld van het gebruik van Azure CLI toodelete een bestand**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Voorbeeld van het gebruik van Azure CLI toolist bestanden**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Extra opslagaccounts gebruiken

Tijdens het maken van een HDInsight-cluster, moet u Hallo gewenste tooassociate aan Azure Storage-account opgeven. Bovendien toothis storage-account, kunt u toevoegen extra opslagaccounts van Hallo dezelfde Azure-abonnement of verschillende Azure-abonnementen tijdens het maken van een Hallo of nadat een cluster is gemaakt. Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor instructies over het toevoegen van extra opslagaccounts.

> [!WARNING]
> Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse HDFS-compatibele Azure storage met HDInsight. Hiermee kunt u toobuild schaalbare, op lange termijn, archiveren voor gegevensverzameling en gebruik HDInsight toounlock Hallo informatie binnen Hallo opgeslagen gestructureerde en ongestructureerde gegevens.

Zie voor meer informatie:

* [Aan de slag met Azure HDInsight][hdinsight-get-started]
* [Aan de slag met Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [Azure Storage Shared Access Signatures toorestrict toegang toodata gebruiken met HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
