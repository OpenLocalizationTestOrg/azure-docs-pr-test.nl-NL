---
title: aaaUse Hadoop Pig met SSH op een HDInsight-cluster - Azure | Microsoft Docs
description: Meer informatie over hoe tooa Linux gebaseerde Hadoop-cluster verbinding te maken met SSH, en vervolgens gebruik Hallo Pig opdracht toorun Pig Latin instructies interactief of als een batch taken.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Pig-taken uitvoeren op een cluster op basis van Linux met Hallo Pig-opdracht (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Meer informatie over hoe toointeractively Pig-taken uitvoeren vanaf een SSH-verbinding tooyour HDInsight-cluster. Hallo Pig Latin programmeertaal kunt u toodescribe transformaties die toegepast toohello invoer gegevens tooproduce Hallo gewenst uitgevoerd worden.

> [!IMPORTANT]
> Hallo moet stappen in dit document een Linux gebaseerde HDInsight-cluster. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a id="ssh"></a>Verbinding maken met SSH

SSH tooconnect tooyour HDInsight-cluster gebruiken. Hallo volgende voorbeeld maakt verbinding met de naam tooa-cluster **myhdinsight** als Hallo rekening met de naam **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Als u een certificaatsleutel voor SSH-verificatie hebt opgegeven** wanneer u Hallo HDInsight-cluster gemaakt, moet u wellicht toospecify Hallo locatie van de persoonlijke sleutel Hallo op uw clientsysteem.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Als u een wachtwoord voor de SSH-verificatie opgegeven** tijdens het maken van HDInsight-cluster Hallo Hallo wachtwoord desgevraagd opgeven.

Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Hallo Pig-opdracht gebruiken

1. Eenmaal zijn verbonden, start u met behulp van de volgende opdracht Hallo Hallo Pig-opdrachtregelinterface (CLI):

        pig

    Na korte tijd, ziet u een `grunt>` prompt.

2. Voer Hallo-instructie:

        LOGS = LOAD '/example/data/sample.log';

    Met deze opdracht laadt Hallo inhoud van Hallo sample.log bestand in LOGBOEKEN. U kunt inhoud Hallo van Hallo-bestand met behulp van de volgende instructie Hallo bekijken:

        DUMP LOGS;

3. Vervolgens Hallo gegevens transformeren door het toepassen van een reguliere expressie tooextract alleen Hallo registratieniveau uit elke record met behulp van de volgende instructie Hallo:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    U kunt **DUMP** tooview Hallo gegevens na de transformatie Hallo. In dit geval gebruiken `DUMP LEVELS;`.

4. Doorgaan transformaties toepassen door middel van Hallo-instructies in de volgende tabel Hallo:

    | Pig Latin-instructie | Welke Hallo-instructie doet |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Hiermee verwijdert u de rijen met een null-waarde voor het logboekniveau Hallo en slaat Hallo resultaten in `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Groepen Hallo rijen door logboekniveau en slaat Hallo resultaten in `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Hiermee maakt u een van de gegevens die elke unieke logboek bevat waarde en hoe vaak het optreedt. Hallo-gegevensset wordt opgeslagen in `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Hallo-logboekniveaus orders op het aantal (aflopend) en opgeslagen in `RESULT`. |

    > [!TIP]
    > Gebruik `DUMP` tooview Hallo resultaat van Hallo transformatie na elke stap.

5. U kunt ook de resultaten van een transformatie Hallo opslaan met behulp van Hallo `STORE` instructie. Bijvoorbeeld Hallo-instructie Hallo bespaart `RESULT` toohello `/example/data/pigout` directory op Hallo standaard opslagruimte voor uw cluster:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Hallo-gegevens worden opgeslagen in de opgegeven map Hallo in bestanden met de naam `part-nnnnn`. Als het Hallo-map al bestaat, ontvangt u een fout opgetreden.

6. tooexit hello knorvis vragen, Voer Hallo-instructie:

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin batch-bestanden

U kunt ook Hallo Pig opdracht toorun Pig Latin opgenomen in een bestand.

1. Na het afsluiten van Hallo knorvis prompt gebruik Hallo volgende toopipe STDIN naar een bestand met de naam opdracht `pigbatch.pig`. Dit bestand is gemaakt in de basismap Hallo voor Hallo SSH gebruikersaccount.

        cat > ~/pigbatch.pig

2. Typ of plak de volgende regels Hallo en gebruik vervolgens Ctrl + D na voltooiing.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Gebruik Hallo volgende opdracht toorun hello `pigbatch.pig` bestand met behulp van Hallo Pig-opdracht.

        pig ~/pigbatch.pig

    Nadat het Hallo batch-job is voltooid, ziet u Hallo volgende uitvoer:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Volgende stappen

Raadpleeg voor algemene informatie over Pig in HDInsight Hallo document te volgen:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

Zie voor meer informatie over andere manieren toowork met Hadoop op HDInsight Hallo documenten te volgen:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)
