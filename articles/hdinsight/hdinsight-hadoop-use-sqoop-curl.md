---
title: aaaUse Hadoop Sqoop met Curl in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooremotely Sqoop taken tooHDInsight met Curl verzenden.
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Sqoop taken uitvoeren met Hadoop in HDInsight met Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Meer informatie over hoe toouse Curl toorun Sqoop taken op een Hadoop-cluster in HDInsight.

CURL is gebruikte toodemonstrate hoe u met HDInsight werken kunt met behulp van onbewerkte HTTP-aanvragen toorun, bewaken en ophalen Hallo resultaten van Sqoop taken. Dit werkt met behulp van Hallo WebHCat REST-API (voorheen bekend als Templeton) geleverd door uw HDInsight-cluster.

> [!NOTE]
> Als u al bekend bent met Hadoop op basis van Linux-servers gebruiken, maar nieuwe tooHDInsight zijn, raadpleegt u [informatie over het gebruik van HDInsight op Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

* Een Hadoop op HDInsight-cluster (Linux of op basis van Windows)
* [CURL](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Sqoop taken verzenden met behulp van Curl
> [!NOTE]
> Wanneer u Curl of andere REST-communicatie met WebHCat, moet u Hallo aanvragen verifiëren door het Hallo-gebruikersnaam en wachtwoord voor Hallo HDInsight Clusterbeheer. Als onderdeel van Hallo Uniform Resource Identifier (URI) toosend Hallo aanvragen toohello server gebruikt, moet u de clusternaam hello gebruiken.
> 
> Hallo-opdrachten in deze sectie, vervangt u **gebruikersnaam** met Hallo gebruiker tooauthenticate toohello cluster en vervang **wachtwoord** met wachtwoord voor gebruikersaccount Hallo Hallo. Vervang **CLUSTERNAME** met Hallo-naam van het cluster.
> 
> Hallo REST API is beveiligd via [basisverificatie](http://en.wikipedia.org/wiki/Basic_access_authentication). U moet aanvragen altijd maken met behulp van beveiligde HTTP (HTTPS) toohelp ervoor te zorgen dat uw referenties veilig toohello server worden verzonden.
> 
> 

1. Gebruik vanaf een opdrachtregel Hallo opdracht tooverify dat u verbinding tooyour HDInsight-cluster maken kunt te volgen:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    U ontvangt een reactie vergelijkbaar toohello volgende:
   
        {"status":"ok","version":"v1"}
   
    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:
   
   * **-u** -Hallo-gebruikersnaam en wachtwoord tooauthenticate Hallo aanvraag gebruikt.
   * **-G**: hiermee wordt aangegeven dat dit een GET-aanvraag is.
     
     Hallo begin van het Hallo-URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, worden dezelfde Hallo voor alle aanvragen. Hallo-pad, **/status**, geeft aan dat verzoek Hallo tooreturn status WebHCat (ook wel bekend als Templeton) voor Hallo-server. 
2. Hallo na toosubmit een taak sqoop gebruiken:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Hallo-parameters die worden gebruikt in deze opdracht zijn als volgt:

    * **-d** - sinds `-G` niet wordt gebruikt, Hallo aanvraag standaard toohello POST-methode. `-d`Hiermee geeft u Hallo waarden die worden verzonden met Hallo-aanvraag.

        * **User.name** -Hallo-gebruiker die het Hallo-opdracht wordt uitgevoerd.

        * **opdracht** -Hallo Sqoop opdracht tooexecute.

        * **statusdir** -Hallo-map die de status voor deze taak Hallo naar worden geschreven.

    Met deze opdracht moet een taak-ID die gebruikt toocheck Hallo status van Hallo taak worden kan retourneren.

        {"id":"job_1415651640909_0026"}

1. toocheck Hallo status van taak hello, gebruik Hallo na de opdracht. Vervang **JOBID** met Hallo-waarde geretourneerd in de vorige stap Hallo. Bijvoorbeeld, als hello retourneert de waarde is `{"id":"job_1415651640909_0026"}`, klikt u vervolgens **JOBID** zou `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Als het Hallo-taak is voltooid, Hallo status worden **geslaagd**.
   
   > [!NOTE]
   > Deze aanvraag Curl retourneert een notatie JSON (JavaScript Object)-document met informatie over het Hallo-taak jq wordt gebruikt tooretrieve Hallo alleen statuswaarde.
   > 
   > 
2. Zodra het Hallo-status van taak hello te is gewijzigd**geslaagd**, kunt u resultaten van de taak Hallo Hallo ophalen uit Azure Blob-opslag. Hallo `statusdir` parameter doorgegeven aan Hallo query bevat Hallo locatie van het uitvoerbestand Hallo; in dit geval **wasb: / / / voorbeeld/curl**. Dit adres Hallo-uitvoer van Hallo taak opslaat in Hallo **voorbeeld/curl** directory op Hallo standaardopslagcontainer die wordt gebruikt door uw HDInsight-cluster.
   
    U kunt de lijst en deze bestanden downloaden met behulp van Hallo [Azure CLI](../cli-install-nodejs.md). Bijvoorbeeld toolist bestanden **voorbeeld/curl**, Hallo volgende opdracht gebruiken:
   
        azure storage blob list <container-name> example/curl
   
    toodownload een bestand, gebruikt u de volgende Hallo:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > U moet opgeven Hallo opslagaccountnaam Hallo blob bevat met behulp van Hallo `-a` en `-k` parameters of set Hallo **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_toegang\_sleutel** omgevingsvariabelen. Zie < een href = "hdinsight-upload-data.md" target = "_blank" voor meer informatie.
   > 
   > 

## <a name="limitations"></a>Beperkingen
* Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.
* Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen wordt uitgevoerd.

## <a name="summary"></a>Samenvatting
Zoals wordt beschreven in dit document, kunt u een onbewerkte HTTP-aanvraag toorun, bewaken en Hallo resultaten weergeven met Sqoop taken op uw HDInsight-cluster.

Zie voor meer informatie over Hallo REST-interface gebruikt in dit artikel Hallo <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST-API-handleiding</a>.

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


