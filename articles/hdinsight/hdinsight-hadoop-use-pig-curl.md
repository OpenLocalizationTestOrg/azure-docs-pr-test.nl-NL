---
title: aaaUse Pig met REST in HDInsight - Azure Hadoop | Microsoft Docs
description: Meer informatie over hoe toouse REST toorun Pig Latin taken op een Hadoop-cluster in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Pig-taken uitvoeren met Hadoop in HDInsight met behulp van REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Meer informatie over hoe toorun Pig Latin taken doordat REST aanvragen tooan Azure HDInsight-cluster. CURL is gebruikte toodemonstrate hoe u kunt werken met HDInsight met behulp van Hallo WebHCat REST-API.

> [!NOTE]
> Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u [Linux gebaseerde HDInsight Tips](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Vereisten

* Een Azure HDInsight (Hadoop in HDInsight)-cluster (op basis van Linux of op basis van Windows)

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* [CURL](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Pig-taken uitvoeren met behulp van Curl

> [!NOTE]
> Hallo REST API is beveiligd via [basistoegang verificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). Altijd aanvragen indienen via HTTP Secure (HTTPS) tooensure dat uw referenties veilig toohello server worden verzonden.
>
> Wanneer met Hallo-opdrachten in deze sectie vervangt `USERNAME` met Hallo gebruiker tooauthenticate toohello cluster en vervang `PASSWORD` met wachtwoord voor gebruikersaccount Hallo Hallo. Vervang `CLUSTERNAME` met Hallo-naam van het cluster.
>


1. Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    U ontvangt Hallo volgende JSON-antwoord:

        {"status":"ok","version":"v1"}

    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

    * **-u**: Hallo-gebruikersnaam en wachtwoord gebruikt tooauthenticate Hallo aanvraag
    * **-G**: geeft aan dat deze aanvraag een aanvraag voor ophalen

     Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen. Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn Hallo status van WebHCat (ook wel bekend als Templeton) voor Hallo-server.

2. Hallo code toosubmit een Pig Latin taak toohello cluster volgende gebruiken:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

    * **-d**: omdat `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode. `-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.

    * **User.name**: Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd
    * **uitvoeren van**: Hallo Pig Latin instructies tooexecute
    * **statusdir**: Hallo-map die Hallo status voor deze taak wordt geschreven naar

    > [!NOTE]
    > U ziet dat Hallo spaties in Pig Latin-instructies worden vervangen door Hallo `+` gebruikt in combinatie met Curl teken.

    Met deze opdracht als resultaat moet een taak-ID die gebruikte toocheck Hallo status van Hallo taak, bijvoorbeeld kan zijn:

        {"id":"job_1415651640909_0026"}

3. status van de toocheck Hallo van Hallo taak, gebruik Hallo na de opdracht

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Vervang `JOBID` met Hallo-waarde geretourneerd in de vorige stap Hallo. Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens `JOBID` is `job_1415651640909_0026`.

    Als het Hallo-taak is voltooid, is het Hallo-status **geslaagd**.

    > [!NOTE]
    > Deze retourneert een JavaScript Object Notation JSON ()-document met informatie over het Hallo-taak en jq is gebruikte tooretrieve Curl-aanvraag Hallo alleen statuswaarde.

## <a id="results"></a>Resultaten weergeven

Wanneer de status van taak Hallo Hallo te is gewijzigd**geslaagd**, kunt u de resultaten van de taak Hallo Hallo ophalen. Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval `/example/pigcurl`.

HDInsight kunt gebruiken Azure Storage of Azure Data Lake Store als Hallo standaard gegevensarchief. Er zijn verschillende manieren tooget op Hallo-gegevens die zijn afhankelijk van wat u gebruikt. Zie voor meer informatie, opslagsectie staat Hallo Hallo [Linux gebaseerde HDInsight-informatie](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.

## <a id="summary"></a>Samenvatting

Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag toorun, bewaken en Hallo-resultaten van Pig-taken weergeven op uw HDInsight-cluster.

Zie voor meer informatie over Hallo REST-interface gebruikt in dit artikel, Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over Pig op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)
