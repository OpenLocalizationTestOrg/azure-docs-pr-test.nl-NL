---
title: aaaMapReduce en extern bureaublad met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse extern bureaublad tooconnect tooHadoop op HDInsight en MapReduce-taken uitvoeren.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>MapReduce in Hadoop in HDInsight met extern bureaublad gebruiken
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

In dit artikel leert u leert hoe tooconnect tooa Hadoop op HDInsight-cluster met behulp van extern bureaublad en vervolgens MapReduce-taken uitvoeren met behulp van Hallo Hadoop-opdracht.

> [!IMPORTANT]
> Extern bureaublad is alleen beschikbaar op Windows gebaseerde HDInsight-clusters. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Voor HDInsight 3.4 of hoger, Zie [MapReduce gebruikt met SSH](hdinsight-hadoop-use-mapreduce-ssh.md) voor informatie over het verbinden van toohello HDInsight-cluster en het MapReduce-taken uitvoeren.

## <a id="prereq"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

* Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)
* Een clientcomputer met Windows 10, Windows 8 of Windows 7

## <a id="connect"></a>Verbinding maken met extern bureaublad
Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Hallo Hadoop-opdracht gebruiken
Wanneer u verbonden toohello bureaublad voor Hallo HDInsight-cluster bent, gebruik Hallo volgende stappen toorun een MapReduce-taak met behulp van Hallo Hadoop-opdracht:

1. Hallo HDInsight bureaublad starten Hallo **Hadoop-opdrachtregel**. Hiermee opent u een nieuwe prompt in Hallo **c:\apps\dist\hadoop-&lt;versienummer >** directory.

   > [!NOTE]
   > Hallo-versienummer verandert als Hadoop wordt bijgewerkt. Hallo **HADOOP_HOME** omgevingsvariabele kan worden gebruikt toofind Hallo pad. Bijvoorbeeld: `cd %HADOOP_HOME%` wijzigingen mappen toohello Hadoop directory, zonder dat u tooknow Hallo versienummer.
   >
   >
2. Hallo toouse **Hadoop** toorun MapReduce-taak van een voorbeeld van de opdracht, Hallo volgende opdracht gebruiken:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Hiermee start u Hallo **wordcount** klasse, die is opgenomen in Hallo **hadoop-mapreduce-examples.jar** bestanden in de huidige map Hallo. Als invoer, hierbij Hallo **wasb://example/data/gutenberg/davinci.txt** document en uitvoer is opgeslagen in: **wasb: / / / voorbeeld/data/WordCountOutput**.

   > [!NOTE]
   > Zie voor meer informatie over deze gegevens MapReduce-taak en Hallo voorbeeld <a href="hdinsight-use-mapreduce.md">gebruik MapReduce in HDInsight Hadoop</a>.
   >
   >
3. Hallo taak verzendt details, zoals deze wordt verwerkt en informatie vergelijkbare toohello volgende retourneert bij het Hallo-taak is voltooid:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Wanneer het Hallo-taak is voltooid, gebruiken Hallo volgende opdracht toolist Hallo uitvoerbestanden opgeslagen in **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Dit moet worden weergegeven in twee bestanden: **_SUCCESS** en **onderdeel-r-00000**. Hallo **onderdeel-r-00000** bestand bevat een Hallo uitvoer voor deze taak.

   > [!NOTE]
   > Bepaalde MapReduce-taken kunnen Hallo resultaten gesplitst over meerdere **onderdeel-r-###** bestanden. Als dit het geval is, gebruikt u Hallo ### achtervoegsel tooindicate Hallo volgorde van Hallo-bestanden.
   >
   >
5. Hallo tooview uitvoer Hallo volgende opdracht gebruiken:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Hiermee wordt een lijst met Hallo woorden die zijn opgenomen in Hallo **wasb://example/data/gutenberg/davinci.txt** bestand samen met de Hallo aantal malen dat elk woord heeft plaatsgevonden. Hallo Hieronder volgt een voorbeeld van Hallo-gegevens die worden opgenomen in het Hallo-bestand:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Samenvatting
Zoals u ziet, biedt Hallo Hadoop opdracht een eenvoudige manier toorun MapReduce-taken op een HDInsight-cluster en klik vervolgens op weergave Hallo taakuitvoer.

## <a id="nextsteps"></a>Volgende stappen
Voor algemene informatie over MapReduce-taken in HDInsight:

* [Gebruik MapReduce op HDInsight Hadoop](hdinsight-use-mapreduce.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
