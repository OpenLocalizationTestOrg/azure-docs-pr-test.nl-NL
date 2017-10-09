---
title: aaaUse Hadoop Hive met Curl in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely indienen Pig tooHDInsight met Curl taken.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Hive-query's uitvoeren met Hadoop in HDInsight met behulp van REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Meer informatie over hoe toouse hello WebHCat REST-API toorun Hive query's met Hadoop op Azure HDInsight-cluster.

[CURL](http://curl.haxx.se/) gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen is. Hallo [jq](http://stedolan.github.io/jq/) hulpprogramma gebruikte tooprocess Hallo JSON-gegevens geretourneerd van de REST-aanvragen is.

> [!NOTE]
> Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u Hallo [wat u moet tooknow over Hadoop op Linux gebaseerde HDInsight](hdinsight-hadoop-linux-information.md) document.

## <a id="curl"></a>Hive-query's uitvoeren

> [!NOTE]
> Wanneer u cURL of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer.
>
> Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en vervang **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo. Vervang **CLUSTERNAME** met Hallo-naam van het cluster.
>
> Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp ervoor te zorgen dat uw referenties veilig toohello server verzonden, altijd aanvragen indienen via HTTP Secure (HTTPS).

1. Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    U ontvangt een reactie vergelijkbaar toohello volgende tekst:

        {"status":"ok","version":"v1"}

    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

   * **-u** -Hallo-gebruikersnaam en wachtwoord tooauthenticate Hallo aanvraag gebruikt.
   * **-G** -geeft aan dat deze aanvraag een GET-bewerking.

     Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is dezelfde Hallo voor alle aanvragen. Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn status WebHCat (ook wel bekend als Templeton) voor Hallo-server. U kunt ook Hallo-versie van Hive met behulp van de volgende opdracht Hallo aanvragen:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Deze aanvraag retourneert een reactie vergelijkbaar toohello volgende tekst:

       {{'module': 'hive', 'versie': "0.13.0.2.1.6.0-2103"}

2. Gebruik Hallo na een tabel met de naam toocreate **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Hallo parameters voor deze aanvraag te volgen:

   * **-d** - sinds `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode. `-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.

     * **User.name** -Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd.
     * **uitvoeren van** -HiveQL-instructies tooexecute Hallo.
     * **statusdir** -Hallo-map die de status voor deze taak Hallo naar worden geschreven.

     Deze instructies uitvoeren Hallo volgende acties:
   * **DROP TABLE** -als Hallo tabel al bestaat, wordt deze verwijderd.
   * **EXTERNE tabel maken** -maakt een nieuwe 'extern' tabel in Hive. Alleen de tabeldefinitie Hallo opslaan externe tabellen in Hive. Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent. Bijvoorbeeld, een uploadproces geautomatiseerde gegevens of een andere MapReduce-bewerking.
     >
     > Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.

   * **INDELING van de rij** : hoe Hallo gegevens zijn opgemaakt. Hallo-velden in elk logboek worden gescheiden door een spatie.
   * **AS TEXTFILE locatie opgeslagen** - Hallo gegevens worden opgeslagen (directory Hallo bijvoorbeeld/gegevens) en dat deze is opgeslagen als tekst.
   * **Selecteer** -selecteert een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**. Deze instructie retourneert een waarde van **3** omdat er zijn drie rijen met deze waarde.

     > [!NOTE]
     > U ziet dat Hallo spaties tussen HiveQL-instructies worden vervangen door Hallo `+` gebruikt in combinatie met Curl teken. Tussen aanhalingstekens waarden met een spatie, zoals het Hallo-scheidingsteken mag niet worden vervangen door `+`.

   * **INPUT__FILE__NAME zoals '% 25.log'** - deze instructie limieten Hallo tooonly gebruik zoekbestanden eindigt op. log.

     > [!NOTE]
     > Hallo `%25` is Hallo URL gecodeerde vorm van %, waardoor u Hallo werkelijke conditie `like '%.log'`. Hallo % heeft toobe URL gecodeerd, zoals dit beschouwd als een speciaal teken in URL's.

     Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren.

       {{'id': "job_1415651640909_0026"}

3. toocheck Hallo status van taak hello, gebruik Hallo volgende opdracht:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Vervang **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo. Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.

    Als het Hallo-taak is voltooid, is het Hallo-status **geslaagd**.

   > [!NOTE]
   > Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over het Hallo-taak. Jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.

4. Zodra het Hallo-status van taak hello te is gewijzigd**geslaagd**, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag. Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval **voorbeeld/curl**. Dit adres Hallo uitvoer opslaat in Hallo **voorbeeld/curl** map in het Hallo-clusters standaard opslag.

    U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Zie voor meer informatie over het gebruik van Azure CLI Hallo met Azure Storage Hallo [2.0 voor Azure CLI gebruiken met Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.

5. Gebruik Hallo na toocreate instructies een nieuwe 'interne' tabel met de naam **foutenlogboeken**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Deze instructies uitvoeren Hallo volgende acties:

   * **MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat. Deze instructie maakt u een interne tabel die is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.

     > [!NOTE]
     > In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.

   * **OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling. ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.
   * **INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.
   * **Selecteer** -selecteert alle rijen uit Hallo nieuwe **foutenlogboeken** tabel.

6. Gebruik Hallo taak-ID toocheck Hallo status van Hallo taak geretourneerd. Gebruik hello Azure CLI zoals hierboven beschreven toodownload en bekijkt hello resultaten zodra deze is voltooid. Hallo-uitvoer moet drie regels, die allemaal bevatten bevatten **[fout]**.

## <a id="nextsteps"></a>Volgende stappen

Voor algemene informatie over Hive met HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo volgende documenten voor het opsporen van informatie:

* [Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken](hdinsight-debug-ambari-tez-view.md)

Zie voor meer informatie over Hallo REST-API die wordt gebruikt in dit document Hallo [WebHCat verwijzing](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


