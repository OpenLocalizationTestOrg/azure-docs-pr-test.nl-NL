---
title: aaaUse scriptactie tooinstall Solr op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall Solr op Linux gebaseerde HDInsight Hadoop-clusters met behulp van scriptacties.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Installeren en gebruiken van Solr op HDInsight Hadoop-clusters

Meer informatie over hoe tooinstall Solr in Azure HDInsight met behulp van de scriptactie. Solr is een krachtige search-platform en biedt zoekmogelijkheden op bedrijfsniveau op gegevens die worden beheerd door Hadoop.

> [!IMPORTANT]
    > Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

> [!IMPORTANT]
> Solr 4.9 installeert Hallo voorbeeldscript in dit document gebruikt met een specifieke configuratie. Als u wilt tooconfigure hello Solr cluster met verschillende verzamelingen, shards, schema's, replica's, enz., moet u Hallo script en Solr binaire bestanden wijzigen.

## <a name="whatis"></a>Wat is Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens. Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr zoekmogelijkheden Hallo tooquickly ophalen Hallo gegevens.

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund door Microsoft.
>
> Aangepaste onderdelen, zoals Solr, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Microsoft ondersteuning mogelijk niet kunnen tooresolve problemen met aangepaste onderdelen. U moet mogelijk tooengage Hallo open-source community's voor ondersteuning. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>Welke Hallo script doet

Dit script maakt Hallo wijzigingen toohello HDInsight-cluster te volgen:

* Solr 4.9 in geïnstalleerd`/usr/hdp/current/solr`
* Hiermee maakt u een gebruiker **solrusr**, namelijk gebruikte toorun hello Solr service
* Sets **solruser** als eigenaar van Hallo`/usr/hdp/current/solr`
* Voegt een [Upstart](http://upstart.ubuntu.com/) configuratie die Solr automatisch wordt gestart.

## <a name="install"></a>Installeren met behulp van scriptacties Solr

Een voorbeeld script tooinstall Solr op een HDInsight-cluster is beschikbaar op Hallo locatie te volgen:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

een cluster met Solr geïnstalleerd toocreate, gebruik Hallo stappen in Hallo [HDInsight-clusters maken](hdinsight-hadoop-create-linux-clusters-portal.md) document. Gebruik tijdens het Hallo maken, Hallo stappen tooinstall Solr te volgen:

1. Van Hallo __Cluster samenvatting__ blade, select__Advanced settings__, klikt u vervolgens __acties Script__. Hallo toopopulate Hallo formulier volgende gebruiken:

   * **NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.
   * **SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: Schakel deze optie
   * **WERKNEMER**: Schakel deze optie
   * **ZOOKEEPER**: Schakel deze optie tooinstall op Hallo Zookeeper knooppunt
   * **PARAMETERS**: dit veld leeg laten

2. Hallo Hallo onderaan in **acties Script** blade, gebruik Hallo **Selecteer** knop toosave Hallo configuratie. Gebruik tot slot Hallo **volgende** knop tooreturn toohello __Cluster samenvatting__

3. Van Hallo __Cluster samenvatting__ pagina __maken__ toocreate Hallo-cluster.

## <a name="usesolr"></a>Hoe gebruik Solr in HDInsight

> [!IMPORTANT]
> Hallo stappen in deze sectie laten zien basisfunctionaliteit Solr. Zie voor meer informatie over het gebruik van Solr hello [Apache Solr site](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Indexgegevens

Hallo te volgen stappen tooadd voorbeeld gegevens tooSolr gebruiken en deze vervolgens een query:

1. Verbinding maken met toohello HDInsight-cluster via SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

     > [!IMPORTANT]
     > Stappen verderop in dit document wordt een SSL-tunnel tooconnect toohello Solr webgebruikersinterface gebruikt. toouse deze stappen, moet u een met SSL maken tunnel en configureer vervolgens uw browser toouse deze.
     >
     > Zie voor meer informatie, Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

2. Gebruik Hallo opdrachten toohave Solr index-voorbeeldgegevens te volgen:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Hallo volgende uitvoergegevens toohello console:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hallo `post.jar` hulpprogramma voegt Hallo **solr.xml** en **monitor.xml** documenten toohello index.
  
3. Gebruik Hallo opdracht tooquery hello Solr REST-API te volgen:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Met deze opdracht wordt gezocht **collection1** voor documenten die overeenkomen met  **\*:\***  (gecodeerd als \*% 3A\* in de queryreeks Hallo). Hallo volgende JSON-document is een voorbeeld van een antwoord Hallo:

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

### <a name="using-hello-solr-dashboard"></a>Met behulp van Hallo Solr dashboard

Hallo Solr dashboard is een webgebruikersinterface waarmee u toowork met Solr via uw webbrowser. Hallo Solr dashboard is niet beschikbaar gemaakt rechtstreeks op Hallo Internet van uw HDInsight-cluster. U kunt een SSH-tunnel tooaccess deze. Zie voor meer informatie over het gebruik van een SSH-tunnel Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

Wanneer u een SSH-tunnel hebt ingesteld, gebruikt u Hallo stappen toouse hello Solr dashboard te volgen:

1. Hallo-hostnaam voor de primaire headnode Hallo bepalen:

   1. Gebruik SSH tooconnect toohello cluster hoofdknooppunt. Bijvoorbeeld `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Zie voor meer informatie over het gebruik van SSH Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Gebruik Hallo opdracht tooget Hallo volledig gekwalificeerde hostnaam te volgen:

        ```bash
        hostname -f
        ```

        Met deze opdracht retourneert een waarde van een vergelijkbare toohello hostnaam te volgen:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Hallo-waarde geretourneerd, niet opslaan omdat het wordt later gebruikt.

2. In uw browser te verbinden**solr-http://HOSTNAME:8983 / #/**, waarbij **hostnaam** is Hallo-naam die u in de vorige stappen Hallo bepaald.

    Hallo-aanvraag wordt doorgestuurd via Hallo SSH-tunnel toohello Solr webgebruikersinterface op uw cluster. Hallo-pagina wordt weergegeven vergelijkbaar toohello installatiekopie te volgen:

    ![Afbeelding van Solr dashboard](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. Gebruik vanuit het linkerdeelvenster Hallo Hallo **Core Selector** vervolgkeuzelijst tooselect **collection1**. Meerdere vermeldingen moeten ze worden weergegeven onder **collection1**.

4. Hallo vermeldingen onderstaande **collection1**, selecteer **Query**. Hallo waarden toopopulate Hallo zoekpagina volgende gebruiken:

   * In Hallo **q** tekst Voer  **\*:**\*. Deze query retourneert alle Hallo-documenten die zijn geïndexeerd in Solr. Als u toosearch voor een specifieke tekenreeks binnen Hallo documenten wilt, kunt u hier die tekenreeks.
   * In Hallo **wt** tekstvak, selecteer Hallo uitvoerindeling. Standaard is **json**.

     Tot slot selecteert Hallo **zoekopdracht uitvoeren** knop Hallo Hallo zoeken pate onderaan in.

     ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     Hallo uitvoer retourneert Hallo twee documenten dat u toohello toegevoegd eerder index. Hallo uitvoer is vergelijkbaar toohello volgende JSON-document:

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

### <a name="starting-and-stopping-solr"></a>Starten en stoppen Solr

Hallo opdrachten toomanually stoppen en starten Solr volgende gebruiken:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Back-upgegevens van de geïndexeerde

Gebruik Hallo tooback up Solr toohello standaard gegevensopslag voor uw cluster stappen te volgen:

1. Toohello-cluster via SSH verbinding en voer vervolgens Hallo opdracht tooget Hallo-hostnaam voor het hoofdknooppunt Hallo volgende gebruiken:

    ```bash
    hostname -f
    ```

2. Gebruik Hallo opdracht toocreate een momentopname van Hallo geïndexeerde gegevens te volgen. Vervang **hostnaam** met geretourneerd van de vorige opdracht Hallo Hallo-naam:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    Hallo-antwoord is vergelijkbaar toohello XML te volgen:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Wijzig de mappen te`/usr/hdp/current/solr/example/solr`. Er is een submap voor elke verzameling. De map voor elke verzameling bevat een `data` directory met Hallo-momentopname voor Hallo-verzameling.

4. toocreate een gecomprimeerd archief van snapshotmap hello, gebruik Hallo volgende opdracht:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Vervang Hallo `snapshot.20150806185338855` waarden met de naam van de Hallo van Hallo-momentopname voor uw verzameling.

    Deze opdracht maakt u een archief met de naam **snapshot.20150806185338855.tgz**, die inhoud Hallo Hallo bevat **snapshot.20150806185338855** directory.

5. U kunt vervolgens Hallo archief toohello van primaire clusteropslag met behulp van de volgende opdracht Hallo opslaan:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Zie voor meer informatie over het werken met Solr back-up en herstelbewerkingen [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Volgende stappen

* [Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md). Cluster aanpassing tooinstall die giraph op HDInsight Hadoop-clusters gebruiken. Giraph kunt u tooperform grafiek verwerken met behulp van Hadoop, en kan worden gebruikt met Azure HDInsight.

* [Hue installeren op HDInsight-clusters](hdinsight-hadoop-hue-linux.md). Cluster aanpassing tooinstall Hue op HDInsight Hadoop-clusters gebruiken. HUE is dat een set van webtoepassingen toointeract gebruikt met een Hadoop-cluster.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
