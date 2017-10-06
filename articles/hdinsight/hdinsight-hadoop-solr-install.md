---
title: aaaUse scriptactie tooinstall Solr op Hadoop-cluster - Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-cluster met Solr met behulp van de scriptactie.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Installeren en gebruiken van Solr op Windows gebaseerde HDInsight-clusters

Meer informatie over hoe toocustomize HDInsight op basis van Windows-cluster met Solr met behulp van de scriptactie en hoe toouse Solr toosearch gegevens.

> [!IMPORTANT]
> Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor meer informatie over het gebruik van Solr met een cluster op basis van Linux [installeert en gebruikt Solr op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).


U kunt Solr installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*. Een voorbeeld script tooinstall Solr op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

Hallo-voorbeeldscript werkt alleen met HDInsight-cluster versie 3.1. Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).

een cluster Solr op basis van Windows maakt Hello voorbeeldscript gebruikt in dit onderwerp met een specifieke configuratie. Als u wilt tooconfigure hello Solr cluster met verschillende verzamelingen, shards, schema's, replica's, enz., moet u Hallo script en Solr binaire bestanden dienovereenkomstig wijzigen.

**Verwante artikelen**

* [Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>Wat is Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens. Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr zoekmogelijkheden Hallo tooquickly ophalen Hallo gegevens.

## <a name="install-solr-using-portal"></a>Solr met portal installeren
1. Beginnen met het maken van een cluster met behulp van Hallo **aangepast maken** optie, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-provision-clusters.md).
2. Op Hallo **scriptacties** pagina van wizard hello, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:

    ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize scriptactie gebruik een cluster")

    <table border='1'>
        <tr><th>Eigenschap</th><th>Waarde</th></tr>
        <tr><td>Naam</td>
            <td>Geef een naam voor de scriptactie Hallo. Bijvoorbeeld: <b>installeren Solr</b>.</td></tr>
        <tr><td>Script-URI</td>
            <td>Geef Hallo Uniform Resource Identifier (URI) toohello script is aangeroepen toocustomize Hallo-cluster. Bijvoorbeeld: <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Soort knooppunt</td>
            <td>Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd. U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b>.
        <tr><td>Parameters</td>
            <td>Geef parameters op Hallo, indien vereist door het Hallo-script. Hallo script tooinstall Solr vereist geen parameters, zodat u kunt dit leeg laten.</td></tr>
    </table>

    U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster. Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart Hallo cluster maken.

## <a name="use-solr"></a>Solr gebruiken
U moet beginnen met het indexeren Solr met enkele gegevensbestanden. U kunt vervolgens Solr toorun zoekquery's op Hallo geïndexeerde gegevens. Voer Hallo stappen toouse Solr in een HDInsight-cluster te volgen:

1. **Remote Desktop Protocol (RDP) tooremote in Hallo HDInsight-cluster gebruiken met Solr geïnstalleerd**. Van hello Azure-portal, moet u extern bureaublad inschakelen voor u met Solr hello geïnstalleerd en vervolgens afstand verbinding met cluster gemaakt Hallo-cluster. Zie voor instructies [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Index Solr door gegevensbestanden uploaden**. Wanneer u de index Solr, plaatst u documenten in die u wellicht toosearch op. tooindex Solr, gebruik RDP tooremote Hallo-cluster met toohello bureaublad navigeren, opent u Hallo Hadoop vanaf de opdrachtregel en navigeer te**C:\apps\dist\solr-4.7.2\example\exampledocs**. Hallo volgende opdracht uitvoeren:

        java -jar post.jar solr.xml monitor.xml

    Hier ziet u uitvoer volgen op Hallo console Hallo:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hallo post.jar hulpprogramma Solr met twee voorbeelddocumenten indexeert **solr.xml** en **monitor.xml**. Hallo post.jar hulpprogramma en Hallo voorbeelddocumenten zijn beschikbaar met Solr installatie.
3. **Gebruik Hallo Solr dashboard toosearch binnen Hallo geïndexeerde documenten**. In Hallo RDP-sessie toohello HDInsight-cluster, opent u Internet Explorer en openen Hallo Solr-dashboard **solr-http://headnodehost:8983 / #/**. Vanuit linkerdeelvenster Hallo van Hallo **Core Selector** vervolgkeuzelijst, selecteer **collection1**, en binnen die, op **Query**. Als een voorbeeld, tooselect en terug bieden alle Hallo documenten in de Solr, Hallo volgende waarden:

   * In Hallo **q** tekst Voer  **\*:**\*. Hiermee wordt alle Hallo-documenten die zijn geïndexeerd in Solr retourneren. Als u toosearch voor een specifieke tekenreeks binnen Hallo documenten wilt, kunt u hier die tekenreeks.
   * In Hallo **wt** tekstvak, selecteer Hallo uitvoerindeling. Standaard is **json**. Klik op **-Query uitvoeren**.

     ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "een query uitvoeren op Solr dashboard")

     Hallo uitvoer retourneert Hallo twee documenten die we voor indexering Solr gebruikt. Hallo uitvoer lijkt op Hallo volgende:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Aanbevolen: Back-up Hallo geïndexeerde gegevens van Solr tooAzure Blob-opslag die is gekoppeld aan de HDInsight-cluster Hallo**. Als een goede gewoonte back u-up Hallo geïndexeerde gegevens vanaf Hallo Solr clusterknooppunten naar Azure Blob-opslag. Voer Hallo dus toodo stappen te volgen:

   1. Open Internet Explorer en punt toohello volgende URL in Hallo RDP-sessie:

           http://localhost:8983/solr/replication?command=backup

       U ziet een antwoord als volgt:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. In de externe sessie hello, te navigeren {SOLR_HOME}\{verzameling} \data. Voor Hallo-cluster is gemaakt via het voorbeeldscript hello, moet dit **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. Op deze locatie ziet u een momentopnamemap is gemaakt met een naam vergelijkbaar te**momentopname.* tijdstempel***.
   3. ZIP-snapshotmap hello en upload het tooAzure Blob-opslag. Navigeer toohello locatie van de snapshotmap Hallo met behulp van de volgende opdracht Hallo vanaf Hallo Hadoop-opdrachtregel:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Met deze opdracht kopieën te/voorbeeld/momentopnamegegevens Hallo/onder Hallo-container binnen Hallo standaard Storage-account die is gekoppeld aan het Hallo-cluster.

## <a name="install-solr-using-aure-powershell"></a>Solr met Aure PowerShell installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Solr met .NET SDK installeren
Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK. U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Zie ook
* [Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.
* [HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.
* [Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).
* [Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark.
* [R installeren op HDInsight-clusters][hdinsight-install-r]: scriptactie voorbeeld over het installeren van R.
* [Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install.md): scriptactie voorbeeld over het installeren van Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
