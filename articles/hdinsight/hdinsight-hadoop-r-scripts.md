---
title: aaaUse R clusters in HDInsight toocustomize - Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall R met behulp van scripts en gebruik R op HDInsight-clusters.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>R installeren en gebruiken op HDInsight Hadoop-clusters

Informatie over hoe Windows toocustomize op basis van HDInsight-cluster met R met behulp van de scriptactie en hoe toouse R op HDInsight-clusters. Hallo [HDInsight aanbieding](https://azure.microsoft.com/pricing/details/hdinsight/) R Server als onderdeel van uw HDInsight-cluster bevat. Hierdoor kan R scripts toouse MapReduce en Spark toorun gedistribueerd berekeningen. Zie [Aan de slag met R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md) voor meer informatie. Zie voor meer informatie over het gebruik van R met een cluster op basis van Linux [installeert en gebruikt R op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).

U kunt R installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*. Een voorbeeld script tooinstall R op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Verwante artikelen**

* [Installeren en gebruiken van R op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): algemene informatie over het maken van HDInsight-clusters
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Wat is R?
Hallo <a href="http://www.r-project.org/" target="_blank">R-Project voor statistische Computing</a> is een open source-taal en de omgeving voor statistische computing. R biedt honderden build in statistische functies en een eigen programmeertaal die aspecten van het functionele en objectgeoriënteerd programmeren combineert. Het bevat ook uitgebreide grafische mogelijkheden. R is Hallo voorkeur programmeeromgeving voor de meeste professionele statistici en verzameld in een groot aantal velden.

R is compatibel met Azure Blob Storage (WASB) zodat er opgeslagen gegevens kunnen worden verwerkt met behulp van R op HDInsight.  

## <a name="install-r"></a>R installeren
Een [voorbeeldscript](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R op een HDInsight-cluster is beschikbaar via een alleen-lezen blob in Azure Storage. Deze sectie bevat instructies over hoe toouse voorbeeldscript Hallo tijdens het Hallo-cluster met behulp van hello Azure Portal maken.

> [!NOTE]
> Hallo-voorbeeldscript is geïntroduceerd in HDInsight-cluster versie 3.1. Zie voor meer informatie over de versies van HDInsight-cluster [versies van HDInsight-cluster](hdinsight-component-versioning.md).
>
>

1. Wanneer u een HDInsight-cluster van Hallo Portal maakt, klikt u op **optionele configuratie**, en klik vervolgens op **scriptacties**.
2. Op Hallo **scriptacties** pagina, voert u Hallo volgende waarden:

    ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize scriptactie gebruik een cluster")

    <table border='1'>
        <tr><th>Eigenschap</th><th>Waarde</th></tr>
        <tr><td>Naam</td>
            <td>Geef een naam voor de scriptactie hello, bijvoorbeeld <b>R installeren</b>.</td></tr>
        <tr><td>Script-URI</td>
            <td>Geef Hallo URI toohello script op dat is aangeroepen toocustomize Hallo cluster, bijvoorbeeld <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Soort knooppunt</td>
            <td>Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd. U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b> alleen.
        <tr><td>Parameters</td>
            <td>Geef parameters op Hallo, indien vereist door het Hallo-script. Hallo script tooinstall R is echter geen parameters, vereist zodat u kunt dit leeg laten.</td></tr>
    </table>

    U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster. Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart crating Hallo-cluster.

U kunt ook Hallo script tooinstall R gebruiken in HDInsight met behulp van Azure PowerShell of Hallo HDInsight .NET SDK. Instructies voor deze procedures vindt u verderop in dit artikel.

## <a name="run-r-scripts"></a>R-scripts uitvoeren
Deze sectie beschrijft hoe toorun een R-script op Hallo Hadoop-cluster met HDInsight.

1. **Een cluster toohello van extern bureaublad-verbinding tot stand brengen**: vanaf Hallo Portal, extern bureaublad inschakelen voor Hallo cluster die u hebt gemaakt met R is geïnstalleerd en vervolgens verbinding toohello cluster. Zie voor instructies [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Open Hallo R console**: Hallo R-installatie plaatst u een koppeling toohello R-console op Hallo bureaublad van Hallo hoofdknooppunt. Klik op het tooopen Hallo R-console.
3. **Hallo R-script uitvoeren**: Hallo R-script rechtstreeks vanuit Hallo R-console kan worden uitgevoerd door plakken, te selecteren en op ENTER te drukken. Hier volgt een eenvoudig voorbeeld-script dat Hallo getallen van 1 too100 genereert en vervolgens wordt vermenigvuldigd met 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Hallo eerste twee regels aanroep Hallo RHadoop bibliotheken zijn geïnstalleerd met R. Hallo laatste regel afdrukken bestellen Hallo resultaten toohello console. Hallo-uitvoer ziet er als volgt:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>R met Aure PowerShell installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>R met .NET SDK installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Zie ook
* [Installeren en gebruiken van R op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): algemene informatie over het maken van HDInsight-clusters
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md)
* [Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark
* [Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install.md): scriptactie voorbeeld over het installeren van Giraph
* [Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md): scriptactie voorbeeld over het installeren van Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
