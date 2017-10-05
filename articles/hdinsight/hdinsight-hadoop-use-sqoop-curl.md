---
title: Hadoop Sqoop gebruiken met Curl in HDInsight - Azure | Microsoft Docs
description: Informatie over het op afstand Sqoop om taken te verzenden naar HDInsight met Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Sqoop taken uitvoeren met Hadoop in HDInsight met Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Informatie over het gebruik van Curl Sqoop taken uitvoeren op een Hadoop-cluster in HDInsight.

CURL wordt gebruikt om u te laten zien hoe u kunt werken met HDInsight met behulp van onbewerkte HTTP-aanvragen worden uitgevoerd, controleren en ophalen van de resultaten van Sqoop taken. Dit werkt met behulp van de WebHCat REST-API (voorheen bekend als Templeton) geleverd door uw HDInsight-cluster.

> [!NOTE]
> Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar niet bekend met HDInsight bent, raadpleegt u [informatie over het gebruik van HDInsight op Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Vereisten
Voor het voltooien van de stappen in dit artikel, moet u het volgende:

* Een Hadoop op HDInsight-cluster (Linux of op basis van Windows)
* [CURL](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Sqoop taken verzenden met behulp van Curl
> [!NOTE]
> Wanneer u Curl of een andere REST-communicatie gebruikt met WebHCat, moet u de aanvragen verifiëren door de gebruikersnaam en het wachtwoord voor de beheerder van het HDInsight-cluster op te geven. U moet ook de clusternaam gebruiken als onderdeel van de URI (Uniform Resource Identifier) die wordt gebruikt om de aanvragen naar de server te verzenden.
> 
> Voor de opdrachten in deze sectie vervangt u **USERNAME** door de gebruiker die moet worden geverifieerd bij het cluster en vervangt u **PASSWORD** door het wachtwoord voor het gebruikersaccount. Vervang **CLUSTERNAME** door de naam van uw cluster.
> 
> De REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). U moet aanvragen altijd uitvoeren via een beveiligde HTTP-verbinding (HTTPS). Zo zorgt u ervoor dat uw referenties veilig worden verzonden naar de server.
> 
> 

1. Gebruik een opdrachtregel met de volgende opdracht om te controleren of u verbinding met uw HDInsight-cluster kunt maken:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Het antwoord dat u ontvangt, is vergelijkbaar met het volgende antwoord:
   
        {"status":"ok","version":"v1"}
   
    In deze opdracht worden de volgende parameters gebruikt:
   
   * **-u**: de gebruikersnaam en het wachtwoord voor het verifiëren van de aanvraag.
   * **-G**: hiermee wordt aangegeven dat dit een GET-aanvraag is.
     
     Het begin van de URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hetzelfde voor alle aanvragen. Het pad **/status**, geeft aan dat de aanvraag is de status van WebHCat (ook wel bekend als Templeton) voor de server. 
2. Gebruik de volgende voor het verzenden van een taak sqoop:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    In deze opdracht worden de volgende parameters gebruikt:

    * **-d** - sinds `-G` niet wordt gebruikt, de aanvraag wordt standaard ingesteld op de POST-methode. `-d`Hiermee geeft u de waarden die worden verzonden met de aanvraag.

        * **User.name** -de gebruiker die de opdracht wordt uitgevoerd.

        * **opdracht** -Sqoop van de opdracht wordt uitgevoerd.

        * **statusdir** -de map die de status voor deze taak om te worden geschreven.

    Met deze opdracht moet een taak-ID die kan worden gebruikt om te controleren van de status van de taak retourneren.

        {"id":"job_1415651640909_0026"}

1. Gebruik de volgende opdracht om te controleren van de status van de taak. Vervang **JOBID** met de waarde die wordt geretourneerd in de vorige stap. Bijvoorbeeld, als de retourwaarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Als de taak is voltooid, worden de status **geslaagd**.
   
   > [!NOTE]
   > Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over de taak. jq wordt gebruikt voor het ophalen van de waarde van de status.
   > 
   > 
2. Zodra de status van de taak is gewijzigd in **geslaagd**, kunt u de resultaten van de taak ophalen uit Azure Blob-opslag. De `statusdir` parameter doorgegeven aan de query bevat de locatie van het uitvoerbestand; in dit geval **wasb: / / / voorbeeld/curl**. Dit adres slaat de uitvoer van de taak in de **voorbeeld/curl** directory op de standaard storage-container die wordt gebruikt door uw HDInsight-cluster.
   
    U kunt de lijst en deze bestanden downloaden met behulp van de [Azure CLI](../cli-install-nodejs.md). Bijvoorbeeld naar de lijst met bestanden in **voorbeeld/curl**, gebruik de volgende opdracht:
   
        azure storage blob list <container-name> example/curl
   
    U kunt een bestand downloaden, gebruikt u het volgende:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > U moet opgeven de opslagaccountnaam die de blob met behulp van bevat de `-a` en `-k` parameters of stel de **AZURE\_opslag\_ACCOUNT** en **AZURE \_Opslag\_toegang\_sleutel** omgevingsvariabelen. Zie < een href = "hdinsight-upload-data.md" target = "_blank" voor meer informatie.
   > 
   > 

## <a name="limitations"></a>Beperkingen
* Bulksgewijs export - met Linux gebaseerde HDInsight, de Sqoop-connector gebruikt voor het exporteren van gegevens naar Microsoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.
* Batchverwerking - met HDInsight op basis van Linux, wanneer u de `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van de bewerkingen insert batchverwerking wordt uitgevoerd.

## <a name="summary"></a>Samenvatting
Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag uitvoeren, bewaken en bekijk de resultaten van Sqoop taken op uw HDInsight-cluster.

Zie voor meer informatie over de REST-interface in dit artikel gebruikt de <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST-API-handleiding</a>.

## <a name="next-steps"></a>Volgende stappen
Voor algemene informatie over Hive met HDInsight:

* [Sqoop gebruiken met Hadoop in HDInsight](hdinsight-use-sqoop.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

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


