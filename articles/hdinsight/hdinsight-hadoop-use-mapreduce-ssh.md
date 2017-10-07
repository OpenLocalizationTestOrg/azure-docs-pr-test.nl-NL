---
title: aaaMapReduce en SSH-verbinding met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse SSH toorun MapReduce taken met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>MapReduce gebruiken met Hadoop op HDInsight met SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Meer informatie over hoe toosubmit MapReduce taken van een tooHDInsight Secure Shell (SSH)-verbinding.

> [!NOTE]
> Als u al bekend bent met het gebruik van Hadoop op basis van Linux-servers, maar u nieuwe tooHDInsight zijn, raadpleegt u [Linux gebaseerde HDInsight tips](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Vereisten

* Een cluster op basis van Linux HDInsight (Hadoop in HDInsight)

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een SSH-client. Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a id="ssh"></a>Verbinding maken met SSH

Toohello-cluster via SSH verbinding. Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met tooa cluster met de naam **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Als u een certificaatsleutel voor SSH-verificatie**, moet u mogelijk toospecify Hallo locatie van de persoonlijke sleutel Hallo op uw clientsysteem, bijvoorbeeld:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Als u een wachtwoord voor de SSH-verificatie**, moet u tooprovide Hallo wachtwoord wanneer u wordt gevraagd.

Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Hadoop-opdrachten gebruiken

1. Nadat u verbonden toohello HDInsight-cluster bent, gebruikt u Hallo opdracht toostart een MapReduce-taak na:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Deze opdracht start Hallo `wordcount` klasse, die is opgenomen in Hallo `hadoop-mapreduce-examples.jar` bestand. Hierbij Hallo `/example/data/gutenberg/davinci.txt` document als invoer en uitvoer is opgeslagen op `/example/data/WordCountOutput`.

    > [!NOTE]
    > Zie voor meer informatie over deze gegevens MapReduce-taak en Hallo voorbeeld [gebruik MapReduce in Hadoop op HDInsight](hdinsight-use-mapreduce.md).

2. Hallo taak verzendt gegevens worden verwerkt en wordt informatie vergelijkbare toohello tekst volgen wanneer Hallo-taak is voltooid:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Wanneer Hallo-taak is voltooid, gebruikt u Hallo opdracht toolist Hallo uitvoerbestanden te volgen:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Deze opdracht weer twee bestanden: `_SUCCESS` en `part-r-00000`. Hallo `part-r-00000` bestand bevat een Hallo uitvoer voor deze taak.

    > [!NOTE]
    > Bepaalde MapReduce-taken kunnen Hallo resultaten gesplitst over meerdere **onderdeel-r-###** bestanden. Als dit het geval is, gebruikt u Hallo ### achtervoegsel tooindicate Hallo volgorde van Hallo-bestanden.

4. Hallo tooview uitvoer Hallo volgende opdracht gebruiken:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Deze opdracht geeft een lijst met Hallo woorden die zijn opgenomen in Hallo **wasb://example/data/gutenberg/davinci.txt** bestands- en Hallo aantal keren dat elk woord is opgetreden. Hallo is volgende tekst een voorbeeld van Hallo-gegevens die zijn opgenomen in Hallo-bestand:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Samenvatting

Zoals u ziet, Hadoop-opdrachten bieden een eenvoudige manier toorun MapReduce-taken in een HDInsight-cluster en weergave Hallo taakuitvoer.

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over MapReduce-taken in HDInsight:

* [Gebruik MapReduce op HDInsight Hadoop](hdinsight-use-mapreduce.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
