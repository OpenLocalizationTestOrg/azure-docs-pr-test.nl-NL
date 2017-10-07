---
title: aaaUpload gegevens voor Hadoop-taken in HDInsight | Microsoft Docs
description: Meer informatie over hoe tooupload en toegang tot gegevens voor Hadoop-taken in HDInsight met behulp van Azure CLI, Azure Storage Explorer, Azure PowerShell, Hallo Hadoop vanaf de opdrachtregel of Sqoop Hallo.
keywords: etl-hadoop-gegevens ophalen van gegevens in hadoop, hadoop laden
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Upload gegevens voor Hadoop-taken in HDInsight
Azure HDInsight biedt een complete Hadoop distributed file system (HDFS) via Azure Blob-opslag. Is bedoeld als een HDFS-extensie tooprovide een naadloze ervaring toocustomers. Kan de volledige set Hallo van onderdelen in Hallo Hadoop-ecosysteem toooperate rechtstreeks op Hallo gegevens beheert. Azure Blob storage en HDFS zijn afzonderlijke bestandssystemen die zijn geoptimaliseerd voor de opslag van gegevens en berekeningen van die gegevens. Zie voor meer informatie over Hallo voordelen van het gebruik van Azure Blob storage [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].

**Vereisten**

Houd er rekening mee Hallo vereiste volgen voordat u begint:

* Een Azure HDInsight-cluster. Zie voor instructies [aan de slag met Azure HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].

## <a name="why-blob-storage"></a>Waarom blobopslag?
Azure HDInsight-clusters doorgaans zijn geïmplementeerd toorun MapReduce-taken en Hallo clusters worden verwijderd nadat deze taken hebt voltooid. Behouden van Hallo-gegevens in HDFS-clusters Hallo nadat berekeningen voltooid zijn worden een toostore dure manier deze gegevens. Azure Blob storage is een maximaal beschikbare, sterk schaalbare, hoge capaciteit, lage kosten en deelbaar opslagoptie voor gegevens die toobe verwerkt met behulp van HDInsight is. Opslaan van gegevens in een blob kunt Hallo HDInsight-clusters die worden gebruikt voor berekeningen toobe veilig vrijgegeven zonder verlies van gegevens.

### <a name="directories"></a>Mappen
Azure Blob storage-containers opslaan van gegevens als sleutel-waardeparen en er is geen maphiërarchie. Echter Hallo '/' teken kan worden gebruikt binnen Hallo sleutelnaam toomake deze weergegeven als een bestand wordt opgeslagen in een mapstructuur. HDInsight ziet deze alsof het werkelijke mappen.

De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn. Er bestaat geen daadwerkelijke 'invoer' map, maar vanwege de aanwezigheid van Hallo toohello teken '/' hello sleutelnaam, is Hallo vormgeving van een bestandspad.

Als gevolg hiervan, als u Azure Explorer hulpprogramma merkt u bepaalde bestanden 0 bytes. Deze bestanden een tweeledig doel:

* Als er lege mappen, worden ze van Hallo bestaan van de map Hallo markeren. Azure Blob-opslag is slimme genoeg tooknow als een blob foo/balk aangeroepen bestaat, er is een map met de naam **foo**. Maar de enige manier toosignify een lege map genaamd Hallo **foo** is door in plaats dit bestand speciale 0 bytes.
* Ze hebben speciale metagegevens die nodig is door Hallo Hadoop bestand systeem, met name machtigingen Hallo en eigenaren voor Hallo mappen.

## <a name="command-line-utilities"></a>Opdrachtregelprogramma 's
Microsoft biedt de volgende hulpprogramma's toowork met Azure Blob storage Hallo:

| Hulpprogramma | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Azure-opdrachtregelinterface][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Hadoop-opdracht](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Terwijl hello Azure CLI, Azure PowerShell en AzCopy kunnen alle worden gebruikt vanuit buiten Azure, Hallo Hadoop-opdracht is alleen beschikbaar op Hallo HDInsight-cluster en kunt alleen het laden van gegevens uit het lokale bestandssysteem Hallo in Azure Blob-opslag.
>
>

### <a id="xplatcli"></a>Azure CLI
Hello Azure CLI is een hulpprogramma voor meerdere platforms waarmee u toomanage Azure services. Hallo te volgen stappen tooupload gegevens tooAzure Blob-opslag gebruiken:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Installeer en configureer hello Azure CLI voor Mac, Linux en Windows](../cli-install-nodejs.md).
2. Open een opdrachtprompt, bash of andere shell en gebruik Hallo tooauthenticate tooyour Azure-abonnement te volgen.

        azure login

    Wanneer u wordt gevraagd, typt u Hallo-gebruikersnaam en wachtwoord voor uw abonnement.
3. Voer Hallo opdracht toolist Hallo storage-accounts voor uw abonnement te volgen:

        azure storage account list
4. Selecteer opslagaccount Hallo Hallo blob toowork met gewenste bevat en voer vervolgens Hallo na de opdracht tooretrieve Hallo sleutel voor dit account gebruiken:

        azure storage account keys list <storage-account-name>

    Dit moet retourneren **primaire** en **secundaire** sleutels. Kopiëren Hallo **primaire** sleutelwaarde omdat deze wordt gebruikt in de volgende stappen Hallo.
5. Hallo na de opdracht tooretrieve een lijst met blobcontainers in Hallo storage-account gebruiken:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Gebruik Hallo opdrachten tooupload te volgen en bestanden toohello blobs downloaden:

   * een bestand tooupload:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * een bestand toodownload:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Als u altijd met Hallo dezelfde werkt storage-account, stelt u Hallo omgevingsvariabelen in plaats van het opgeven van Hallo rekening te volgen en sleutel voor elke opdracht:
>
> * **AZURE\_opslag\_ACCOUNT**: Hallo opslagaccountnaam
> * **AZURE\_opslag\_toegang\_sleutel**: Hallo opslagaccountsleutel
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell is een scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw workloads in Azure. Zie voor meer informatie over het configureren van uw werkstation toorun Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload een lokaal bestand tooAzure Blob-opslag**

1. Open hello Azure PowerShell-console volgens de instructies in [installeren en configureren van Azure PowerShell](/powershell/azure/overview).
2. Hallo-waarden van Hallo eerste vijf variabelen in het volgende script Hallo instellen:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Hallo plakken wordt script in hello Azure PowerShell-console toorun toocopy Hallo-bestand is ingesteld.

Bijvoorbeeld toowork van PowerShell-scripts die zijn gemaakt met HDInsight, Zie [HDInsight tools](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy is een opdrachtregelprogramma dat is ontworpen toosimplify Hallo taak van het overbrengen van gegevens naar en van een Azure Storage-account. U kunt gebruiken als een zelfstandige tool of gebruikmaken van dit hulpprogramma in een bestaande toepassing. [Downloaden van AzCopy][azure-azcopy-download].

Hallo AzCopy syntaxis is:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Zie voor meer informatie [AzCopy - bestanden voor Azure Blobs uploaden/downloaden][azure-azcopy].

### <a id="commandline"></a>Hadoop-opdrachtregel
Hallo Hadoop vanaf de opdrachtregel is alleen nuttig voor het opslaan van gegevens naar de blobopslag Hallo gegevens is al aanwezig op het hoofdknooppunt Hallo-cluster.

In de volgorde toouse Hallo Hadoop-opdracht, moet u eerst toohello headnode met een van de volgende methoden Hallo verbinden:

* **HDInsight op basis van Windows**: [verbinding maken met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight op basis van Linux**: verbinding maken met behulp van SSH ([Hallo SSH-opdracht](hdinsight-hadoop-linux-use-ssh-unix.md) of [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Eenmaal zijn verbonden, kunt u Hallo syntaxis tooupload een bestand toostorage te volgen.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Bijvoorbeeld: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Omdat Hallo standaardbestandssysteem voor HDInsight in Azure Blob-opslag, zich /example/data.txt in Azure Blob-opslag. U kunt ook toohello-bestand als verwijzen:

    wasb:///example/data/data.txt

of

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Zie voor een lijst met andere Hadoop die werken met bestanden opdrachten, [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Op de HBase-clusters Hallo Standaardblokgrootte gebruikt bij het schrijven van gegevens is 256KB. Hoewel dit goed met HBase APIs of REST-API's werkt, met behulp van Hallo `hadoop` of `hdfs dfs` opdrachten toowrite gegevens groter zijn dan ~ 12 GB in een fout resulteert. Zie Hallo [uitzondering om te schrijven op blob storage](#storageexception) sectie hieronder voor meer informatie.
>
>

## <a name="graphical-clients"></a>Grafische clients
Er zijn ook enkele toepassingen die een grafische interface bieden voor het werken met Azure Storage. Hallo Hier volgt een lijst met enkele van deze toepassingen:

| Client | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure-opslagverkenner](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud-opslag Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio-hulpprogramma's voor HDInsight
Zie voor meer informatie [navigeren Hallo gekoppelde resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Azure Opslagverkenner
*Azure Storage Explorer* is een nuttig hulpmiddel om te bekijken en wijzigen van Hallo-gegevens in BLOB's. Het is een gratis, open source-hulpprogramma dat kan worden gedownload vanaf [http://storageexplorer.com/](http://storageexplorer.com/). Hallo broncode is beschikbaar via deze koppeling ook.

Voordat u Hallo-hulpprogramma gebruiken, moet u weten Azure naam en sleutel van uw opslagaccount. Zie voor instructies over het ophalen van deze informatie Hallo ' How to: toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren ' sectie van [maken, beheren of verwijderen van een opslagaccount][azure-create-storage-account].

1. Azure Storage Explorer uitvoeren. Als dit Hallo eerst u Hallo Opslagverkenner hebt uitgevoerd, wordt u gevraagd om Hallo **_Storage accountnaam** en **opslagaccountsleutel**. Als u het eerder hebt uitgevoerd, gebruikt u Hallo **toevoegen** knop tooadd naam van een nieuw opslagaccount en de sleutel.

    Voer Hallo naam en sleutel voor Hallo storage-account die wordt gebruikt door uw HDInsight-cluster en selecteert u vervolgens **opslaan en openen**.

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. Klik in de lijst van de Hallo van containers toohello links van Hallo interface, op Hallo-naam van Hallo-container die is gekoppeld aan uw HDInsight-cluster. Standaard kunt dit Hallo-naam van Hallo HDInsight-cluster is, maar mogelijk anders als u een specifieke naam hebt ingevoerd bij het maken van Hallo-cluster.
3. Selecteer in de werkbalk hello, Hallo uploaden pictogram.

    ![Werkbalk met uploaden pictogram gemarkeerd](./media/hdinsight-upload-data/toolbar.png)
4. Geef een bestand tooupload en klik vervolgens op **Open**. Wanneer u wordt gevraagd, selecteert u **uploaden** tooupload Hallo bestand toohello hoofdmap van Hallo storage-container. Als u wilt dat tooupload hello tooa specifieke bestandspad, voert u Hallo pad in Hallo **bestemming** veld en selecteer vervolgens **uploaden**.

    ![Bestand uploaden dialoogvenster](./media/hdinsight-upload-data/fileupload.png)

    Zodra het Hallo-bestand is klaar met uploaden, kunt u deze uit taken op Hallo HDInsight-cluster.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Azure Blob-opslag als lokale schijf koppelen
Zie [koppelpunt Azure Blob Storage als lokaal station](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Services
### <a name="azure-data-factory"></a>Azure Data Factory
Hello Azure Data Factory-service is een volledig beheerde service voor het opstellen van services voor opslag, verwerking van gegevens en gegevens gegevensverplaatsing in productie met gestroomlijnde, schaalbare en betrouwbare gegevenspijplijnen.

Azure Data Factory kan gebruikte toomove gegevens in Azure Blob-opslag of toocreate gegevenspijplijnen dat rechtstreeks HDInsight functies zoals Hive en varkens.

Zie voor meer informatie, Hallo [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop is een hulpprogramma waarmee u tootransfer gegevens tussen Hadoop en relationele databases. U kunt deze tooimport gegevens uit een relationele databasebeheersysteem (RDBMS), zoals SQL Server, MySQL of Oracle in Hallo Hadoop distributed file system (HDFS) gegevens in Hadoop met MapReduce of Hive Hallo transformeren en vervolgens exporteren Hallo gegevens terug in een RDBMS.

Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>Ontwikkeling van SDK 's
Azure Blob-opslag kan ook worden geopend met een Azure-SDK van Hallo programmeertalen te volgen:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Zie voor meer informatie over het installeren van hello Azure-SDK's [Azure downloads](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Problemen oplossen
### <a id="storageexception"></a>Uitzondering voor schrijven in blob Storage
**Symptomen**: bij gebruik van Hallo `hadoop` of `hdfs dfs` opdrachten toowrite bestanden die zijn ~ 12 GB of groter op een HBase-cluster kunnen Hallo volgende fout optreden:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Oorzaak**: HBase op HDInsight-clusters standaard tooa blokgrootte van 256 KB bij het schrijven van tooAzure opslag. Terwijl dit voor HBase APIs of REST-API's werkt, het zal leiden tot een fout opgetreden bij het gebruik van Hallo `hadoop` of `hdfs dfs` opdrachtregelprogramma's.

**Resolutie**: Gebruik `fs.azure.write.request.size` toospecify een groter blok. U kunt dit doen op basis van per gebruik met behulp van Hallo `-D` parameter. Hallo Hieronder volgt een voorbeeld met deze parameter Hello `hadoop` opdracht:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

U kunt ook de waarde van Hallo vergroten `fs.azure.write.request.size` globaal via Ambari. Hallo volgende stappen kunnen worden gebruikt toochange Hallo waarde in Hallo Ambari-Webgebruikersinterface:

1. Ga in uw browser toohello Ambari-Webgebruikersinterface voor uw cluster. Dit is https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.

    Voer desgevraagd Hallo beheerder naam en het wachtwoord voor Hallo-cluster.
2. Selecteer in het Hallo-zijde van welkomstscherm links, **HDFS**, en selecteer vervolgens Hallo **Configs** tabblad.
3. In Hallo **Filter...**  veld `fs.azure.write.request.size`. Hiermee wordt de Hallo veld en de huidige waarde in het midden van de Hallo van Hallo pagina weergegeven.
4. Hallo-waarde van 262144 (256KB) toohello nieuwe waarde wijzigen. Bijvoorbeeld: 4194304 (4MB).

![Afbeelding van het Hallo-waarde via Ambari-Webgebruikersinterface wijzigen](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Zie voor meer informatie over het gebruik van Ambari [beheren HDInsight-clusters met Ambari-Webgebruikersinterface Hallo](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Volgende stappen
Nu dat u begrijpt hoe tooget gegevens in HDInsight, lees Hallo artikelen toolearn hoe na tooperform analyse:

* [Aan de slag met Azure HDInsight][hdinsight-get-started]
* [Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
