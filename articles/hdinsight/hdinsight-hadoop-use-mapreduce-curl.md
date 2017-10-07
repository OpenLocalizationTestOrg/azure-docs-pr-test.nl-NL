---
title: aaaUse MapReduce en Curl met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely uitvoeren MapReduce-taken met Hadoop op HDInsight met Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>MapReduce-taken uitvoeren met Hadoop op HDInsight met behulp van REST

Meer informatie over hoe toouse hello WebHCat REST-API toorun MapReduce taken op een Hadoop op HDInsight-cluster. CURL is gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen toorun MapReduce-taken.

> [!NOTE]
> Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar u staat op het nieuwe tooHDInsight, Zie Hallo [wat u moet tooknow over Hadoop op basis van Linux in HDInsight](hdinsight-hadoop-linux-information.md) document.


## <a id="prereq"></a>Vereisten

* Een Hadoop op HDInsight-cluster
* [CURL](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>MapReduce-taken met Curl uitvoeren

> [!NOTE]
> Wanneer u Curl of andere REST-communicatie met WebHCat gebruikt, moet u Hallo aanvragen verifiëren door te geven Hallo HDInsight-cluster administrator-gebruikersnaam en wachtwoord. Als onderdeel van Hallo URI die gebruikte toosend Hallo aanvragen toohello server, moet u de clusternaam hello gebruiken.
>
> Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo. Vervang **CLUSTERNAME** met Hallo-naam van het cluster.
>
> Hallo REST API is beveiligd met behulp van [basistoegang verificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). U moet aanvragen altijd maken met behulp van HTTPS tooensure dat uw referenties veilig toohello server worden verzonden.


1. Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    U ontvangt een reactie vergelijkbaar toohello JSON te volgen:

        {"status":"ok","version":"v1"}

    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

   * **-u**: Hiermee geeft u Hallo-gebruikersnaam en wachtwoord gebruikt tooauthenticate Hallo aanvraag
   * **-G**: geeft aan dat deze bewerking een GET-aanvraag

     Hallo vanaf Hallo URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen.

2. toosubmit MapReduce-taak Hallo volgende opdracht gebruiken:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    Hallo-einde van Hallo URI (mapreduce/jar) ziet WebHCat of er een MapReduce-taak op deze aanvraag wordt gestart van een klasse in een jar-bestand. Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

   * **-d**: `-G` niet wordt gebruikt, dus Hallo aanvraag standaard toohello POST-methode. `-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.
    * **User.name**: Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd
    * **JAR**: Hallo-locatie van Hallo jar-bestand waarin de klasse toobe uitgevoerd
    * **klasse**: klasse met Hallo MapReduce logica Hallo
    * **arg**: Hallo argumenten toobe doorgegeven toohello MapReduce-taak. In dit geval invoer Hallo tekst bestands- en Hallo directory die worden gebruikt voor het Hallo-uitvoer

     Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren:

       {{'id': "job_1415651640909_0026"}

3. toocheck Hallo status van taak hello, gebruik Hallo volgende opdracht:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Vervang Hallo **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo. Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, vervolgens Hallo JOBID zou worden `job_1415651640909_0026`.

    Als het Hallo-taak is voltooid, Hallo status geretourneerd is `SUCCEEDED`.

   > [!NOTE]
   > Deze aanvraag Curl retourneert een JSON-document met informatie over het Hallo-taak. Jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.

4. Wanneer de status van taak Hallo Hallo te is gewijzigd`SUCCEEDED`, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag. Hallo `statusdir` parameter die wordt doorgegeven met Hallo query Hallo locatie van het uitvoerbestand Hallo bevat. In dit voorbeeld is Hallo locatie `/example/curl`. Dit adres Hallo-uitvoer van Hallo taak opslaat in Hallo-clusters standaard opslag op `/example/curl`.

U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Zie voor meer informatie over het werken met blobs uit hello Azure CLI Hallo [Using hello Azure CLI 2.0 met Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over MapReduce-taken in HDInsight:

* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

Zie voor meer informatie over Hallo REST-interface die wordt gebruikt in dit artikel, Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
