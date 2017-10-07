---
title: aaaUse Hadoop Pig met extern bureaublad in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Pig opdracht toorun Pig Latin-instructies uit een extern bureaublad verbinding tooa Hadoop op basis van Windows-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Pig-taken uitvoeren vanaf een extern bureaublad-verbinding
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Dit document bevat een overzicht voor het gebruik van Hallo Pig opdracht toorun Pig Latin-instructies uit een extern bureaublad verbinding tooa HDInsight op basis van Windows-cluster. Pig Latin kunt u toocreate MapReduce-toepassingen door te beschrijven gegevenstransformaties, in plaats van toewijzen en functies te beperken.

> [!IMPORTANT]
> Extern bureaublad is alleen beschikbaar op HDInsight-clusters die Windows hello besturingssysteem gebruiken. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Voor HDInsight 3.4 of hoger, Zie [Pig gebruiken met HDInsight en SSH](hdinsight-hadoop-use-pig-ssh.md) voor informatie over het interactief uitvoeren Pig-taken rechtstreeks op Hallo cluster van een opdrachtregel.

## <a id="prereq"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo.

* Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)
* Een clientcomputer met Windows 10, Windows 8 of Windows 7

## <a id="connect"></a>Verbinding maken met extern bureaublad
Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Hallo Pig-opdracht gebruiken
1. Nadat u een verbinding met extern bureaublad hebt, start u Hallo **Hadoop-opdrachtregel** met behulp van Hallo-pictogram op Hallo bureaublad.
2. Hallo na toostart Hallo Pig-opdracht gebruiken:

        %pig_home%\bin\pig

    U krijgt een `grunt>` prompt.
3. Voer Hallo-instructie:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Met deze opdracht laadt Hallo inhoud van Hallo sample.log bestand in het Hallo LOGBOEKEN-bestand. U kunt inhoud Hallo van Hallo-bestand met behulp van de volgende opdracht Hallo bekijken:

        DUMP LOGS;
4. Hallo-gegevens door het toepassen van een reguliere expressie tooextract alleen Hallo registratieniveau uit elke record transformeren:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    U kunt **DUMP** tooview Hallo gegevens na de transformatie Hallo. In dit geval `DUMP LEVELS;`.
5. Blijven transformaties toepassen met behulp van Hallo instructies te volgen. Gebruik `DUMP` tooview Hallo resultaat van Hallo transformatie na elke stap.

    <table>
    <tr>
    <th>Instructie</th><th>Wat het doet</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER TOEPASSINGSNIVEAU LOGLEVEL niet null is.</td><td>Hiermee verwijdert u de rijen met een null-waarde voor het logboekniveau Hallo en slaat Hallo resultaten in FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = groep FILTEREDLEVELS door LOGLEVEL;</td><td>Groepen Hallo rijen door logboekniveau en slaat Hallo resultaten in GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENTIES foreach = GROUPEDLEVELS groep genereren als LOGLEVEL, COUNT (FILTEREDLEVELS. LOGLEVEL) zoals tellen;</td><td>Maakt een nieuwe set van gegevens in elk logboek unieke waarde en hoe vaak het optreedt. Dit bestand bevindt zich in de FREQUENTIES</td>
    </tr>
    <tr>
    <td>RESULTAAT = volgorde FREQUENTIES door aantal desc;</td><td>Hallo-logboekniveaus op aantal (aflopend) en slaat de orders in resultaat</td>
    </tr>
    </table>
6.U kunt ook de resultaten van een transformatie Hallo opslaan met behulp van Hallo `STORE` instructie. Bijvoorbeeld Hallo volgende opdracht slaat Hallo `RESULT` toohello **/example/data/pigout** map in Hallo standaardopslagcontainer voor uw cluster:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Hallo-gegevens worden opgeslagen in de opgegeven map Hallo in bestanden met de naam **onderdeel nnnnn**. Als het Hallo-map al bestaat, ontvangt u een foutbericht weergegeven.
   >
   >
7. tooexit hello knorvis vragen, Voer Hallo-instructie.

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin batch-bestanden
U kunt ook Hallo Pig opdracht toorun Pig Latin die is opgenomen in een bestand.

1. Open na het afsluiten van Hallo knorvis prompt **Kladblok** en maak een nieuw bestand met de naam **pigbatch.pig** in Hallo **% PIG_HOME %** directory.
2. Type of plakken Hallo volgende regels in Hallo **pigbatch.pig** bestand en sla het:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Gebruik Hallo na toorun hello **pigbatch.pig** -bestand met Hallo pig-opdracht.

        pig %PIG_HOME%\pigbatch.pig

    Wanneer Hallo batch-job is voltooid, ziet u Hallo na uitvoer, die moet worden Hallo hetzelfde als wanneer u gebruikt `DUMP RESULT;` in de vorige stappen Hallo:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Samenvatting
Zoals u zien kunt, kunt u Hallo Pig opdracht toointeractively MapReduce-bewerkingen uitvoeren of Pig Latin taken uitvoeren die zijn opgeslagen in een batch-bestand.

## <a id="nextsteps"></a>Volgende stappen
Voor algemene informatie over Pig in HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)
