---
title: aaaApache gestructureerde Streaming van Spark met Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Spark (DStream) tooget streaminggegevens van of naar Apache Kafka. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Gestructureerde Streaming van Spark met Kafka (preview) op HDInsight gebruiken

Meer informatie over hoe toouse tooread gegevens gestructureerde Spark-Streaming van Apache Kafka in Azure HDInsight.

Spark gestructureerd streaming is een stream-verwerkingsengine gebouwd op Spark SQL. Hiermee kunt dat u tooexpress streaming berekeningen Hallo hetzelfde als batch berekening op statische gegevens. Zie voor meer informatie over het gestructureerde Streaming Hallo [gestructureerde Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) op Apache.org.

> [!IMPORTANT]
> In dit voorbeeld gebruikt 2.1 Spark in HDInsight 3.6. Gestructureerde Streaming wordt beschouwd als __alpha__ op Spark 2.1.
>
> Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Spark-cluster toodirectly communiceren met de Hallo Kafka-cluster.
>
> Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.

## <a name="create-hello-clusters"></a>Hallo-clusters maken

Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo. Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster. Bijvoorbeeld, bevinden zowel hello Kafka- en Spark-clusters zich in een Azure-netwerk. Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Hallo Kafka-service is beperkt toocommunication in Hallo virtuele netwerk. Andere services op Hallo cluster Hallo zoals SSH en Ambari, toegankelijk is via internet. Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).

U kunt een Azure-netwerk, Kafka en Spark clusters handmatig maken, is het eenvoudiger toouse een Azure Resource Manager-sjabloon. Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Spark-clusters tooyour Azure-abonnement.

1. Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Met deze sjabloon maakt Hallo resources te volgen:

    * Een Kafka op 3.5 HDInsight-cluster.
    * Een Spark in HDInsight 3.6 cluster.
    * Een virtueel netwerk in Azure die Hallo HDInsight-clusters bevat.

    > [!IMPORTANT]
    > Hallo gestructureerde streaming-notebook gebruikt in dit voorbeeld vereist Spark in HDInsight 3.6. Als u een eerdere versie van Spark in HDInsight, er fouten als Hallo notebook.

2. Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Resourcegroep**: Maak een groep of een bestaande set selecteren. Deze groep bevat Hallo HDInsight-cluster.

    * **Locatie**: Selecteer een locatie geografisch sluiten tooyou.

    * **Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor Hallo Spark en Kafka clusters Hallo. Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.

    * **Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Spark en Kafka-clusters.

    * **Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Spark en Kafka-clusters.

    * **SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Spark en Kafka-clusters.

    * **SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Spark en Kafka-clusters.

3. Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.

4. Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**. Het duurt ongeveer 20 minuten toocreate Hallo-clusters.

Zodra het Hallo-resources zijn gemaakt, bent u omgeleide toohello resourcegroepblade.

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon. U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.

## <a name="get-hello-kafka-brokers"></a>Hallo Kafka beleggingsmakelaars ophalen

Hallo code in dit voorbeeld maakt verbinding toohello Kafka-hosts in Hallo Kafka cluster broker. toofind hello Kafka broker hosts, gebruikt u Hallo PowerShell- of Bash voorbeeld te volgen:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> In dit voorbeeld verwacht `$PASSWORD` toocontain Hallo wachtwoord voor aanmelding Hallo-cluster, en `$CLUSTERNAME` toocontain Hallo naam Hallo Kafka-cluster.
>
> In dit voorbeeld wordt Hallo [jq](https://stedolan.github.io/jq/) hulpprogramma tooparse gegevens buiten Hallo JSON-document.

Hallo uitvoer is vergelijkbaar toohello de volgende tekst:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Deze gegevens niet opslaan omdat het wordt gebruikt in de volgende secties van dit document Hallo.

## <a name="get-hello-notebooks"></a>Hallo-laptops ophalen

Hallo code Hallo zoals beschreven in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Hallo-laptops uploaden

Volgende stappen tooupload Hallo notitieblokken uit Hallo project tooyour Spark in HDInsight-cluster hello gebruiken:

1. In uw webbrowser verbinding toohello Jupyter-notebook in Spark-cluster. Hallo-URL, na Vervang in `CLUSTERNAME` met de naam van uw cluster Kafka Hallo:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Voer desgevraagd Hallo cluster aanmeldingsnaam (admin) en het wachtwoord die worden gebruikt wanneer u Hallo cluster hebt gemaakt.

2. Gebruik vanaf Hallo bovenste rechts Hallo pagina, Hallo __uploaden__ knop tooupload hello __stroom Tweets To_Kafka.ipynb__ toohello bestandscluster. Selecteer __Open__ toostart Hallo uploaden.

    ![Hallo uploaden knop tooselect gebruiken en een laptop te uploaden](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Hallo KafkaStreaming.ipynb bestand selecteren](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Hallo zoeken __stroom Tweets To_Kafka.ipynb__ vermelding in de lijst Hallo van notitieblokken en selecteer __uploaden__ knop ernaast.

    ![Gebruik Hallo uploaden knop naast Hallo KafkaStreaming.ipynb vermelding tooupload het toohello notebook server](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Herhaal stap 1-3 tooload hello __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ notebook.

## <a name="load-tweets-into-kafka"></a>Tweets in Kafka laden

Zodra het Hallo-bestanden zijn geüpload, selecteert u Hallo __stroom Tweets To_Kafka.ipynb__ vermelding tooopen Hallo notebook. Stappen Hallo in Hallo notebook tooload tweets in Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Proces tweets met gestructureerde Spark-Streaming

Hallo Jupyter-Notebook startpagina, selecteer Hallo __Spark-gestructureerd-Streaming-van-Kafka.ipynb__ vermelding. Stappen Hallo in Hallo notebook tooload tweets van Kafka met gestructureerde Spark-Streaming.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse Spark gestructureerde Streaming Hallo documenten toolearn meer over het werken met Spark en Kafka volgende zien:

* [Hoe toouse streaming (DStream) met Kafka Spark](hdinsight-apache-spark-with-kafka.md).
* [Beginnen met Jupyter-Notebook en Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)