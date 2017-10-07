---
title: aaaInstall en gebruik Giraph op Hadoop-clusters in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-cluster met Giraph en hoe toouse Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Installeren en gebruiken van Giraph op Windows gebaseerde HDInsight-clusters

Meer informatie over hoe Windows toocustomize gebaseerd HDInsight-cluster met Giraph met behulp van de scriptactie en hoe toouse Giraph tooprocess grootschalige grafieken. Zie voor meer informatie over het gebruik van Giraph met een cluster op basis van Linux [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Voor meer informatie over tooinstall Giraph op Linux gebaseerde HDInsight-cluster Zie [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).


U kunt Giraph installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*. Een voorbeeld script tooinstall Giraph op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). Hallo-voorbeeldscript werkt alleen met HDInsight-cluster versie 3.1. Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).

**Verwante artikelen**

* [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>Wat is Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> kunt u tooperform grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight. Grafieken model relaties tussen de objecten, zoals Hallo-verbindingen tussen routers op een grote netwerk, zoals Hallo Internet, of relaties tussen mensen op sociale netwerken (soms waarnaar wordt verwezen tooas sociale grafiek). Grafiek verwerking kunt u tooreason over Hallo relaties tussen de objecten in een grafiek, zoals:

* Identificeren van mogelijke vrienden op basis van uw huidige relaties.
* Identificerende Hallo kortste afstand tussen twee computers in een netwerk.
* Berekenen Hallo pagina positie van webpagina's.

## <a name="install-giraph-using-portal"></a>Giraph met portal installeren
1. Beginnen met het maken van een cluster met behulp van Hallo **aangepast maken** optie, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-provision-clusters.md).
2. Op Hallo **scriptacties** pagina van wizard hello, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:

    ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize scriptactie gebruik een cluster")

    <table border='1'>
        <tr><th>Eigenschap</th><th>Waarde</th></tr>
        <tr><td>Naam</td>
            <td>Geef een naam voor de scriptactie Hallo. Bijvoorbeeld: <b>installeren Giraph</b>.</td></tr>
        <tr><td>Script-URI</td>
            <td>Geef Hallo Uniform Resource Identifier (URI) toohello script is aangeroepen toocustomize Hallo-cluster. Bijvoorbeeld: <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Soort knooppunt</td>
            <td>Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd. U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b>.
        <tr><td>Parameters</td>
            <td>Geef parameters op Hallo, indien vereist door het Hallo-script. Hallo script tooinstall Giraph vereist geen parameters, zodat u kunt dit leeg laten.</td></tr>
    </table>

    U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster. Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart Hallo cluster maken.

## <a name="use-giraph"></a>Giraph gebruiken
We gebruiken Hallo SimpleShortestPathsComputation voorbeeld toodemonstrate Hallo basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementatie voor het vinden van Hallo kortste pad tussen de objecten in een grafiek. Gebruik hello te volgen stappen tooupload Hallo voorbeeld gegevens en Hallo voorbeeld jar, een taak uitvoert met behulp van Hallo SimpleShortestPathsComputation voorbeeld en Hallo-resultaten weergeven.

1. Upload een sample data bestand tooAzure Blob-opslag. Maak een nieuw bestand met de naam op uw lokale werkstation **tiny_graph.txt**. Hallo volgende regels moet bevatten:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Upload Hallo tiny_graph.txt toohello primaire bestandsopslag voor uw HDInsight-cluster. Voor instructies over het tooupload van gegevens, Zie [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).

    Deze gegevens beschrijft de relatie tussen de objecten in een gerichte grafiek, met behulp van notatie Hallo [bron\_-id, de bron\_waarde [[dest\_id], [rand\_waarde],...]]. Elke regel vertegenwoordigt een relatie tussen een **bron\_id** object en een of meer **dest\_id** objecten. Hallo **rand\_waarde** (of gewicht) kunnen worden beschouwd als Hallo sterkte of de afstand van de verbinding tussen Hallo **source_id** en **dest\_id**.

    Getekend, en het Hallo-waarde (of gewicht) gebruikt als Hallo afstand tussen de objecten, Hallo boven gegevens als volgt uitzien:

    ![tiny_graph.txt getekend als cirkels met verschillende afstand tussen regels](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Hallo SimpleShortestPathsComputation voorbeeld uitvoert. Gebruik hello Azure PowerShell-cmdlets toorun Hallo voorbeeld te volgen met behulp van Hallo tiny_graph.txt bestand als invoer.

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Vervang in Hallo hierboven voorbeeld **clustername** met Hallo-naam van uw HDInsight-cluster met Giraph geïnstalleerd.
3. Hallo resultaten weergeven. Zodra het Hallo-taak is voltooid, Hallo resultaten worden opgeslagen in twee uitvoerbestanden in Hallo **wasb: / / / voorbeeld/out/shotestpaths** map. Hallo-bestanden worden genoemd **onderdeel-m-00001** en **onderdeel-m-00002**. Volgende stappen toodownload en bekijkt hello uitvoer Hallo uitvoeren:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Hiermee maakt u Hallo **uitvoer-voorbeeld/shortestpaths** directorystructuur in de huidige map op uw werkstation en download Hallo twee bestanden toothat uitvoerlocatie Hallo.

    Gebruik Hallo **Cat** cmdlet toodisplay Hallo inhoud van Hallo-bestanden:

        Cat example/output/shortestpaths/part*

    Hallo-uitvoer moet vergelijkbaar toohello volgende weergegeven:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Hallo SimpleShortestPathComputation voorbeeld is vastgelegde toostart met object-ID 1 en Hallo kortste pad tooother objecten zoeken. Dus Hallo uitvoer moet worden gelezen als `destination_id distance`, waarbij afstand Hallo waarde (of gewicht) van Hallo randen afgelegd tussen object-ID 1 en Hallo doel-ID.

    U kunt dit visualiseren, Hallo resultaten controleren door onderweg Hallo kortste paden tussen de 1-ID en alle andere objecten. Let op: Hallo kortste pad tussen ID 1 en 4-ID is 5. Dit is de totale afstand Hallo tussen <span style="color:orange">ID 1 en 3</span>, en vervolgens <span style="color:red">ID 3 en 4</span>.

    ![Tekenen van objecten als cirkels met de kortste paden tussen getekend](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Giraph met Aure PowerShell installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Giraph met .NET SDK installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Zie ook
* [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).
* [Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark.
* [R installeren op HDInsight-clusters][hdinsight-install-r]: scriptactie voorbeeld over het installeren van R.
* [Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install.md): scriptactie voorbeeld over het installeren van Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
