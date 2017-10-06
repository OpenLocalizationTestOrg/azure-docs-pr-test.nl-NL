---
title: aaaInstall en Giraph op HDInsight (Hadoop) - Azure gebruiken | Microsoft Docs
description: Meer informatie over hoe tooinstall Giraph op Linux gebaseerde HDInsight-clusters met behulp van scriptacties. Scriptacties kunnen u toocustomize Hallo cluster tijdens het maken, door het wijzigen van de configuratie van het cluster of het installeren van hulpprogramma's en services.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Giraph installeren op HDInsight Hadoop-clusters en Giraph tooprocess grootschalige grafieken gebruiken

Meer informatie over hoe tooinstall Apache Giraph op een HDInsight-cluster. Hallo script actie functie van HDInsight kunt u toocustomize uw cluster een bash-script uit te voeren. Scripts kunnen gebruikte toocustomize clusters worden tijdens en na het maken van het cluster.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="whatis"></a>Wat is Giraph

[Apache Giraph](http://giraph.apache.org/) kunt u tooperform grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight. Grafieken model relaties tussen objecten. Hallo-verbindingen tussen routers op een groot netwerk, zoals Internet Hallo of relaties tussen mensen op sociale netwerken. Grafiek verwerking kunt u tooreason over Hallo relaties tussen de objecten in een grafiek, zoals:

* Identificeren van mogelijke vrienden op basis van uw huidige relaties.

* Identificerende Hallo kortste afstand tussen twee computers in een netwerk.

* Berekenen Hallo pagina positie van webpagina's.

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund: Microsoft Support helpt tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.
>
> Aangepaste onderdelen, zoals Giraph, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Microsoft Support mogelijk kunnen tooresolving Hallo probleem. Als dat niet het geval is, moet u contact opnemen met open-source community's waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>Welke Hallo script doet

Dit script voert Hallo van de volgende activiteiten:

* Giraph te worden geïnstalleerd`/usr/hdp/current/giraph`

* Kopieën Hallo `giraph-examples.jar` bestandsopslag toodefault (WASB) voor uw cluster:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Giraph met behulp van scriptacties installeren

Een voorbeeld script tooinstall Giraph op een HDInsight-cluster is beschikbaar op Hallo locatie te volgen:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Deze sectie bevat instructies over hoe toouse voorbeeldscript Hallo tijdens het Hallo-cluster maken met behulp van hello Azure-portal.

> [!NOTE]
> Een scriptactie kan worden toegepast met behulp van een Hallo volgende methoden:
> * Azure PowerShell
> * Hello Azure CLI
> * Hallo HDInsight .NET SDK
> * Azure Resource Manager-sjablonen
> 
> U kunt ook script acties tooalready actieve clusters toepassen. Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).

1. Beginnen met het maken van een cluster met behulp van de stappen in Hallo [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md), maar niet maken uitvoert.

2. Op Hallo **optionele configuratie** blade Selecteer **scriptacties**, en geef Hallo volgende informatie:

   * **NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.

   * **SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: deze vermelding controleren

   * **WERKNEMER**: laat u dit item niet ingeschakeld

   * **ZOOKEEPER**: laat u dit item niet ingeschakeld

   * **PARAMETERS**: dit veld leeg laten

3. Hallo Hallo onderaan in **scriptacties**, hello gebruiken **Selecteer** knop toosave Hallo configuratie. Gebruik tot slot Hallo **Selecteer** knop onderin Hallo Hallo **optionele configuratie** blade toosave Hallo optionele configuratie-informatie.

4. Doorgaan met het Hallo-cluster maken, zoals beschreven in [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Hoe gebruik Giraph in HDInsight?

Zodra Hallo-cluster is gemaakt, gebruikt u Hallo stappen toorun hello SimpleShortestPathsComputation voorbeeld is opgenomen in Giraph te volgen. In dit voorbeeld wordt Hallo basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementatie voor het vinden van Hallo kortste pad tussen de objecten in een grafiek.

1. Verbinding maken met toohello HDInsight-cluster via SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Gebruik Hallo volgende opdracht toocreate uit een bestand met de naam **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Deze gegevens beschrijft de relatie tussen de objecten in een gerichte grafiek, met behulp van notatie Hallo `[source_id, source_value,[[dest_id], [edge_value],...]]`. Elke regel vertegenwoordigt een relatie tussen een `source_id` object en een of meer `dest_id` objecten. Hallo `edge_value` kunnen worden beschouwd als Hallo sterkte of de afstand van de verbinding tussen Hallo `source_id` en `dest\_id`.

    Getekend, en met Hallo waarde (gewicht) als Hallo afstand tussen de objecten, Hallo gegevens als volgt uitzien Hallo-diagram te volgen:

    ![tiny_graph.txt getekend als cirkels met verschillende afstand tussen regels](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. Gebruik-bestand Hallo toosave **Ctrl + X**, vervolgens **Y**, en tot slot **Enter** tooaccept Hallo-bestandsnaam.

4. Gebruik Hallo toostore Hallo gegevens naar de primaire opslag voor uw HDInsight-cluster te volgen:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Hallo SimpleShortestPathsComputation voorbeeld met behulp van de volgende opdracht Hallo uitvoeren:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    Hallo-parameters die worden gebruikt met deze opdracht worden beschreven in de volgende tabel Hallo:

   | Parameter | Wat het doet |
   | --- | --- |
   | `jar` |Hallo jar-bestand met de Hallo voorbeelden. |
   | `org.apache.giraph.GiraphRunner` |Hallo klasse gebruikt toostart Hallo voorbeelden. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |Hallo-voorbeeld dat wordt gebruikt. In dit voorbeeld wordt de kortste pad Hallo tussen ID 1 en alle andere id's in de grafiek Hallo berekend. |
   | `-ca mapred.job.tracker` |Hallo headnode voor Hallo-cluster. |
   | `-vif` |Hallo invoerindeling toouse voor Hallo invoergegevens. |
   | `-vip` |Hallo invoergegevens bestand. |
   | `-vof` |Hallo uitvoer-indeling. In dit voorbeeld-ID en -waarde als tekst zonder opmaak. |
   | `-op` |Hallo uitvoerlocatie. |
   | `-w 2` |Hallo aantal werknemers toouse. In dit voorbeeld 2. |

    Zie voor meer informatie over deze en andere parameters gebruikt met Giraph voorbeelden Hallo [Giraph Quick Start](http://giraph.apache.org/quick_start.html).

6. Zodra het Hallo-taak is voltooid, Hallo resultaten worden opgeslagen in Hallo **/example/out/shotestpaths** directory. Hallo uitvoer bestandsnamen beginnen met **onderdeel-m -** en eindigen met een getal dat aangeeft Hallo eerst tweede, enzovoort-bestand. Hallo opdrachtuitvoer tooview Hallo volgende gebruiken:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    Hallo-uitvoer moet worden weergegeven vergelijkbaar toohello volgende tekst:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Hallo SimpleShortestPathComputation voorbeeld is vastgelegde toostart met object-ID 1 en Hallo kortste pad tooother objecten zoeken. Hallo-uitvoer is in de indeling van Hallo `destination_id` en `distance`. Hallo `distance` Hallo waarde (of gewicht) van Hallo randen afgelegd ligt tussen object-ID 1 en Hallo doel-ID.

    U kunt deze gegevens te visualiseren, Hallo resultaten controleren door onderweg Hallo kortste paden tussen de 1-ID en alle andere objecten. Hallo kortste pad tussen ID 1 en 4-ID is 5. Deze waarde is de totale afstand Hallo tussen <span style="color:orange">ID 1 en 3</span>, en vervolgens <span style="color:red">ID 3 en 4</span>.

    ![Tekenen van objecten als cirkels met de kortste paden tussen getekend](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Volgende stappen

* [Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).

* [Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).
