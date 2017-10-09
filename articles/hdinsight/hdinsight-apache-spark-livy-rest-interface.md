---
title: aaaUse Livy Spark toosubmit taken tooSpark-cluster in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Spark REST-API toosubmit Spark taken die op afstand tooan Azure HDInsight-cluster.
keywords: Apache spark rest-api, spark livy
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Apache Spark REST-API toosubmit externe taken tooan HDInsight Spark-cluster gebruiken

Meer informatie over hoe toouse Livy, Hallo Apache Spark REST API, namelijk gebruikte toosubmit externe taken tooan Azure HDInsight Spark-cluster. Zie voor gedetailleerde documentatie [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

U kunt gebruiken Livy toorun interactieve Spark houders of batch-taken toobe uitvoeren op Spark verzenden. In dit artikel wordt gesproken over met behulp van Livy toosubmit batchtaken. Hallo codefragmenten in dit artikel gebruiken cURL toomake REST API-aanroepen toohello Livy Spark-eindpunt.

**Vereisten:**

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). Dit artikel wordt cURL toodemonstrate hoe toomake REST-API met een HDInsight Spark-cluster aanroept.

## <a name="submit-a-livy-spark-batch-job"></a>Een batchtaak Livy Spark verzenden
Voordat u een batch-job indienen, moet u Hallo toepassing jar op Hallo clusteropslag die is gekoppeld aan cluster Hallo uploaden. U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdrachtregelprogramma, toodo zodat. Er zijn verschillende andere clients kunt u tooupload gegevens. U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Voorbeelden**:

* Als Hallo jar-bestand zich op Hallo cluster storage (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Als u wilt toopass Hallo jar filename en classname Hallo als onderdeel van een bestand voor invoer (in dit voorbeeld input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Informatie over Livy Spark batches uitgevoerd op Hallo-cluster
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Voorbeelden**:

* Als u wilt dat tooretrieve alle Hallo Livy Spark batches uitgevoerd op Hallo-cluster:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Als u wilt dat een specifieke batch met een bepaalde batchId tooretrieve
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Een batch-job Livy Spark verwijderen
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Voorbeeld**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark en hoge beschikbaarheid
Livy biedt hoge beschikbaarheid voor Spark taken uitgevoerd op Hallo-cluster. Hier volgt een aantal voorbeelden.

* Als Hallo Livy-service wordt uitgeschakeld nadat u een taak op afstand hebt verzonden tooa Spark-cluster, hello taak toorun op Hallo achtergrond blijft. Hier wordt een back-up, wordt Hallo status van taak Hallo en rapporten weer hersteld.
* Jupyter-notebooks voor HDInsight worden van stroom voorzien door Livy in Hallo back-end. Als een laptop een Spark-taak wordt uitgevoerd en Hallo Livy-service opnieuw wordt gestart, blijft de notebook Hallo toorun Hallo code cellen. 

## <a name="show-me-an-example"></a>Een voorbeeld weergeven
In deze sectie we kijken voorbeelden toouse Livy Spark toosubmit batch-job Hallo voortgang van de taak Hallo en vervolgens te verwijderen. Hallo-toepassing in dit voorbeeld we gebruiken is een ontwikkeld in Hallo artikel Hallo [maken van een zelfstandige Scala toepassing en toorun op HDInsight Spark-cluster](hdinsight-apache-spark-create-standalone-application.md). Hier Hallo stappen wordt ervan uitgegaan dat:

* U hebt al Hallo toepassing jar toohello storage-account die is gekoppeld aan cluster Hallo gekopieerd.
* U hebt geïnstalleerd op Hallo-computer waarop u deze stappen probeert CuRL.

Voer Hallo stappen te volgen:

1. Laat het ons moet u eerst controleren of Livy Spark op Hallo cluster wordt uitgevoerd. We kunnen dit doen door het ophalen van een lijst van het uitvoeren van batches. Als u een taak met behulp van Livy voor Hallo eerst uitvoert, moet Hallo uitvoer nul retourneren.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Deze krijgt u een vergelijkbare uitvoer-toohello codefragment te volgen:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    U ziet hoe de laatste regel in de uitvoer van de Hallo Hallo zegt **totaal: 0**, die geen actieve batches wordt voorgesteld.

2. Laten we nu een batch-job indienen. Hallo volgende codefragment maakt gebruik van een bestand voor invoer (input.txt) toopass Hallo jar naam en klassenaam Hallo als parameters. Als u deze stappen vanuit een Windows-computer uitvoert, is met behulp van een bestand voor invoer Hallo aanbevolen benadering.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    parameters in bestand Hallo Hallo **input.txt** als volgt gedefinieerd:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    U ziet hoe de laatste regel van uitvoer Hallo Hallo zegt **status: vanaf**. Ook wordt, **-id: 0**. Hier **0** Hallo batch-id is.

3. U kunt nu ophalen Hallo status van deze specifieke batch Hallo batch-id.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hallo output wordt nu weergegeven **status: geslaagd**, die wordt voorgesteld die Hallo-taak is voltooid.

4. Als u wilt, kunt u nu Hallo batch verwijderen.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hallo laatste regel van Hallo uitvoer toont dat die Hallo-batch is verwijderd. Verwijderen van een taak, terwijl deze wordt uitgevoerd, ook is funest Hallo-taak. Als u een taak die is voltooid, is of anderszins verwijdert worden verwijderd Hallo taakinformatie volledig.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Gebruik van Livy Spark in HDInsight 3.5 clusters

3.5 HDInsight-cluster, schakelt het gebruik van bestanden lokaal bestand paden tooaccess met voorbeeldgegevens of potten standaard. We raden u toouse hello `wasb://` pad in plaats daarvan tooaccess potten of voorbeeldgegevens bestanden van Hallo-cluster. Als u dat het lokale pad toouse wilt, moet u dienovereenkomstig Hallo Ambari configuratie bijwerken. toodo zodat:

1. Ga toohello Ambari-portal voor Hallo-cluster. Hallo Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op https://**CLUSTERNAME**. azurehdidnsight.net, waarbij CLUSTERNAME Hallo-naam van het cluster is.

2. Hallo linkernavigatiebalk, klik op **Livy**, en klik vervolgens op **Configs**.

3. Onder **livy-standaard** Hallo eigenschapsnaam toevoegen `livy.file.local-dir-whitelist` en stel de waarde te**'/'** als u tooallow volledige toegang toofile systeem wilt. Als u tooallow toegang alleen tooa specifieke map wilt, geeft u Hallo pad toothat directory Hallo-waarde.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Verzenden van Livy taken voor een cluster binnen een virtuele Azure-netwerk

Als u verbinding maakt met tooan HDInsight Spark-cluster uit een Azure-netwerk, kunt u rechtstreeks tooLivy op Hallo-cluster. In dat geval Hallo URL voor Livy-eindpunt is `http://<IP address of hello headnode>:8998/batches`. Hier **8998** Hallo poort waarop Livy op Hallo cluster headnode wordt uitgevoerd. Zie voor meer informatie over de toegang tot services op niet-openbaar poorten [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Problemen oplossen

Hier volgen enkele problemen beschreven die u tegenkomen kunt tijdens het gebruik van Livy voor externe taak verzending tooSpark clusters.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Gebruik een externe jar van Hallo extra opslagruimte wordt niet ondersteund

**Probleem:** als uw job Livy Spark verwijst naar een externe jar vanuit Hallo extra opslagaccount die is gekoppeld aan cluster hello, Hallo-taak is mislukt.

**Oplossing:** Zorg ervoor dat Hallo jar gewenste toouse is beschikbaar in Hallo standaard opslag die is gekoppeld aan Hallo HDInsight-cluster.





## <a name="next-step"></a>Volgende stap

* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

