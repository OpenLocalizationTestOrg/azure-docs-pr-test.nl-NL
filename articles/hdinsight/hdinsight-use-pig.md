---
title: aaaUse Hadoop Pig in HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse varkens met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Pig gebruiken met Hadoop in HDInsight

Meer informatie over hoe toouse [Apache Pig](http://pig.apache.org/) met HDInsight...

Pig is een platform voor het maken van programma's voor Hadoop met behulp van een procedurele taal bekend als *Pig Latin*. Pig is een alternatieve tooJava voor het maken van *MapReduce* oplossingen en deze is opgenomen in Azure HDInsight. Gebruik Hallo tabel toodiscover Hallo verschillende manieren waarop Pig kan worden gebruikt met HDInsight te volgen:

| **Gebruik deze** als u wilt dat... | .. .an **interactieve** shell | ... **batch** verwerken | .. .door dit **cluster-besturingssysteem** | .. .from dit **clientbesturingssysteem** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X of Windows |
| [REST API](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux- of Windows |Linux, Unix, Mac OS X of Windows |
| [.NET-SDK voor Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux- of Windows |Windows (voor nu) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux- of Windows |Windows |
| [Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a id="why"></a>Waarom Pig gebruiken

Een van Hallo uitdagingen bij het verwerken van gegevens met behulp van MapReduce in Hadoop is uw verwerking logica implementeren met behulp van alleen een kaart en een functie verminderen. Voor complexe verwerking, u vaak keten toobreak verwerken in meerdere MapReduce-bewerkingen die zijn samengesteld tooachieve Hallo gewenst resultaat.

Pig kunt u toodefine verwerken als een reeks transformaties die Hallo gegevensoverdrachten via tooproduce Hallo gewenste uitvoer.

Hallo Pig Latin taal kunt u toodescribe Hallo gegevensstroom uit onbewerkte invoer, via een of meer transformaties tooproduce Hallo gewenste uitvoer. Pig Latin-programma's volgen deze algemene patroon:

* **Load**: gegevens toobe ingesteld van het bestandssysteem Hallo lezen

* **Transformeren**: Hallo gegevens bewerken

* **Dump of opgeslagen**: gegevens toohello scherm uitvoer of opgeslagen voor verwerking

### <a name="user-defined-functions"></a>Gebruiker gedefinieerde functies

Pig Latin ondersteunt ook gebruiker gedefinieerde functies (UDF), waarmee u tooinvoke externe onderdelen die logica die is moeilijk toomodel in Pig Latin implementeren.

Zie voor meer informatie over Pig Latin [Pig Latin verwijzing handmatige 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) en [Pig Latin verwijzing handmatige 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Zie voor een voorbeeld van het gebruik van UDF's met Pig Hallo documenten te volgen:

* [Gebruik DataFu met Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu is een verzameling nuttig UDF's die worden beheerd door de Apache
* [Gebruik van Python met Pig en Hive in HDInsight](hdinsight-python.md)
* [Gebruik C# met Hive en Pig in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Voorbeeldgegevens

HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in Hallo `/example/data` en `/HdiSamples` mappen. Deze mappen zich in Hallo standaard opslagruimte voor uw cluster. Hallo Pig voorbeeld in dit document wordt Hallo *log4j* bestand van `/example/data/sample.log`.

Elk logboek in Hallo-bestand bestaat uit een line-of velden met een `[LOG LEVEL]` veld tooshow Hallo type en Hallo ernst, bijvoorbeeld:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

In het vorige voorbeeld Hallo is Hallo logboekniveau fout.

> [!NOTE]
> U kunt ook een log4j-bestand genereren met behulp van Hallo [Apache-Log4j](http://en.wikipedia.org/wiki/Log4j) hulpprogramma logboekregistratie en vervolgens uploaden bestand tooyour blob. Zie [gegevens uploaden tooHDInsight](hdinsight-upload-data.md) voor instructies. Zie voor meer informatie over het gebruik van blobs in Azure storage met HDInsight [Azure Blob Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Voorbeeld van de taak

Hallo volgende Pig Latin-taak wordt geladen Hallo `sample.log` -bestand uit Hallo standaard opslag voor uw HDInsight-cluster. Vervolgens voert een reeks transformaties die in een aantal van hoe vaak elk logboek niveau opgetreden in Hallo-invoergegevens resulteren uit. Hallo resultaten worden tooSTDOUT geschreven.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Hallo toont volgende afbeelding een overzicht van wat elke transformatie toohello gegevens biedt.

![Grafische weergave van Hallo transformaties][image-hdi-pig-data-transformation]

## <a id="run"></a>Hallo Pig Latin taak uitvoeren

HDInsight kunt Pig Latin taken uitvoeren met behulp van een aantal methoden. Gebruik Hallo tabel toodecide methode die geschikt voor u is te volgen en Hallo-koppeling voor de procedure volgen.

| **Gebruik deze** als u wilt dat... | .. .an **interactieve** shell | ... **batch** verwerken | .. .door dit **cluster-besturingssysteem** | .. .from dit **client** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X of Windows |
| [CURL](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux- of Windows |Linux, Unix, Mac OS X of Windows |
| [.NET-SDK voor Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux- of Windows |Windows (voor nu) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux- of Windows |Windows |
| [Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="pig-and-sql-server-integration-services"></a>Pig- en SQL Server integratieservices

U kunt SQL Server Integration Services (SSIS) toorun Pig-taak. Hello Azure Feature Pack voor SSIS biedt Hallo onderdelen die met Pig-taken in HDInsight werken te volgen.

* [Azure HDInsight Pig-taak][pigtask]

* [Azure abonnement Verbindingsbeheer][connectionmanager]

Meer informatie over Azure Feature Pack Hallo voor SSIS [hier][ssispack].

## <a id="nextsteps"></a>Volgende stappen
U hebt geleerd hoe toouse Pig met HDInsight, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.

* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop.md)
* [Oozie gebruiken met HDInsight](hdinsight-use-oozie.md)
* [MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
