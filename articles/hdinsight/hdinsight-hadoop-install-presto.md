---
title: aaaInstall functie in Azure HDInsight Linux-clusters | Microsoft Docs
description: Meer informatie over hoe tooinstall functie en Airpal op Linux gebaseerde HDInsight Hadoop-clusters met behulp van scriptacties.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Installeren en gebruiken Presto op HDInsight Hadoop-clusters

In dit onderwerp leert u hoe tooinstall functie op HDInsight Hadoop-clusters met behulp van de scriptactie. U leert ook hoe tooinstall Airpal op een bestaand Presto HDInsight-cluster.

> [!IMPORTANT]
> Hallo stappen in dit document vereisen een **HDInsight 3.5 Hadoop-cluster** die gebruikmaakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [versies van HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>Wat is Presto?
[Presto](https://prestodb.io/overview.html) is een snelle gedistribueerde SQL query-engine voor big data. Functie is geschikt voor petabytes aan gegevens interactieve query's naar. Zie voor meer informatie over Hallo onderdelen van de functie en hoe ze samenwerken [Presto concepten](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support zal helpen tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.
> 
> Aangepaste onderdelen, zoals de functie, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Met behulp van de scriptactie functie installeren

Deze sectie bevat instructies over hoe toouse Hallo voorbeeldscript bij het maken van een nieuw cluster met behulp van hello Azure-portal. 

1. Start met het inrichten van een cluster met behulp van de stappen in Hallo [Provision Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md). Zorg ervoor dat u met behulp van Hallo Hallo-cluster maakt **aangepaste** stroom voor het maken van het cluster. U moet ervoor zorgen dat Hallo-cluster dat u maakt aan Hallo volgens de vereisten voldoet.

    a. Het moet een Hadoop-cluster met HDInsight versie 3.5.

    b. Azure Storage moet als gegevensarchief Hallo gebruiken. Met Presto op een cluster die gebruikmaakt van Azure Data Lake Store als opslagoptie Hallo is nog niet ondersteund. 

    ![Maken van het HDInsight-cluster met aangepaste opties](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. Op Hallo **geavanceerde instellingen** blade Selecteer **scriptacties**, en geef Hallo informatie hieronder:
   
   * **NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.
   * **Bash-script-URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**: Schakel deze optie
   * **WERKNEMER**: Schakel deze optie
   * **ZOOKEEPER**: Schakel dit selectievakje
   * **PARAMETERS**: dit veld leeg laten


3. Hallo Hallo onderaan in **scriptacties** blade, klikt u op Hallo **selecteren** knop toosave Hallo configuratie. Tot slot op Hallo **Selecteer** knop onderin Hallo Hallo **geavanceerde instellingen** blade toosave Hallo configuratie-informatie.

4. Doorgaan Hallo cluster inrichten, zoals beschreven in [Provision Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Gebruikte tooapply scriptacties kunnen ook worden door Azure PowerShell, hello Azure CLI, Hallo HDInsight .NET SDK of Azure Resource Manager-sjablonen. U kunt ook script acties tooalready actieve clusters toepassen. Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Functie gebruiken met HDInsight

Voer Hallo stappen toouse functie in een HDInsight-cluster te volgen nadat u hebt geïnstalleerd met behulp van Hallo stappen die hierboven worden beschreven.

1. Verbinding maken met toohello HDInsight-cluster via SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.
     

2. Hallo Presto shell met behulp van de volgende opdracht Hallo starten.
   
        presto --schema default

3. Een query uitvoeren op een voorbeeldtabel **hivesampletable**, die beschikbaar zijn op alle HDInsight-clusters standaard is.
   
        select count (*) from hivesampletable;
   
    Standaard [Hive](https://prestodb.io/docs/current/connector/hive.html) en [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors voor de functie al zijn geconfigureerd. Hive-connector is geconfigureerde toouse Hallo standaard geïnstalleerd Hive installatie, zodat alle Hallo tabellen vanuit Hive wordt automatisch zichtbaar in de functie.

    Zie voor een gedetailleerde beschrijving van hoe u de functie kunt gebruiken, [Presto documentatie](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Airpal gebruiken met de functie

[Airpal](https://github.com/airbnb/airpal#airpal) is een open source web gebaseerde QueryInterface voor de functie. Zie voor meer informatie over Airpal [Airpal documentatie](https://github.com/airbnb/airpal#airpal).

In dit gedeelte kijken we Hallo stappen te**Airpal installeren op Hallo edgenode** van een HDInsight Hadoop-cluster dat al functie heeft geïnstalleerd. Dit zorgt ervoor dat Hallo Airpal webinterface query beschikbaar is via Hallo Internet.

1. Gebruik van SSH verbinding toohello headnode van Hallo HDInsight-cluster met Presto zijn geïnstalleerd:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Nadat u verbonden bent, Hallo volgende opdracht worden uitgevoerd.

        sudo slider registry  --name presto1 --getexp presto 
   
    Hier ziet u uitvoer Hallo volgende:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Houd er rekening mee Hallo-waarde voor Hallo van Hallo uitvoer **waarde** eigenschap. U moet dit tijdens het installeren van Airpal op Hallo cluster edgenode. Is van de uitvoer Hallo boven Hallo-waarde die u moet **10.0.0.12:9090**.

4. Hallo-sjabloon gebruiken  **[hier](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate een HDInsight cluster edgenode en Hallo waarden opgeven, zoals wordt weergegeven in de volgende schermafbeelding Hallo.

    ![HDInsight installatie Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Klik op **Kopen**.

6. Als de Hallo wijzigingen zijn toegepast toohello clusterconfiguratie, kunt u Hallo Airpal webinterface openen met behulp van Hallo stappen te volgen.

    a. Cluster-blade hello, klikt u op **toepassingen**.

    ![HDInsight starten Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. Van Hallo **geïnstalleerde Apps** blade, klikt u op **Portal** tegen airpal.

    ![HDInsight starten Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Voer desgevraagd Hallo-referenties die u hebt opgegeven tijdens het maken van Hallo HDInsight Hadoop-cluster.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>De installatie van een Presto op HDInsight-cluster aanpassen

Nadat u de functie op een HDInsight Hadoop-cluster hebt geïnstalleerd, kunt u Hallo installatie toomake wijzigingen zoals het update-geheugeninstellingen aanpassen, wijzigt connectors, enzovoort. Voer Hallo dus toodo stappen te volgen.

1. Gebruik van SSH verbinding toohello headnode van Hallo HDInsight-cluster met Presto zijn geïnstalleerd:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. De configuratiewijzigingen aanbrengen in Hallo bestand `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Zie voor meer informatie over Presto configuratie [Presto configuratie voor YARN gebaseerde clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).

3. Stop en kill Hallo actieve sessie van de functie.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Start een nieuw exemplaar van de functie met Hallo aanpassing.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Wacht tot Hallo nieuwe exemplaar toobe gereed en noteer het adres van presto coördinator.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Benchmark-gegevens voor HDInsight-clusters met Presto genereren

TPC DS is Hallo industriestandaard voor het meten van de prestaties van veel besluit ondersteuning voor systemen, met inbegrip van big-datasystemen Hallo. U kunt Presto op HDInsight-clusters toogenerate gegevens gebruiken en evalueren hoe worden vergeleken met uw eigen HDInsight benchmark-gegevens. Zie voor meer informatie [hier](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Zie ook
* [Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md). HUE is een webgebruikersinterface waardoor u eenvoudig toocreate, uitvoeren en sla Pig en Hive-taken, ook als bladeren Hallo standaard opslag voor uw HDInsight-cluster.

* [Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md). Cluster aanpassing tooinstall die giraph op HDInsight Hadoop-clusters gebruiken. Giraph kunt u tooperform grafiek verwerken met behulp van Hadoop, en kan worden gebruikt met Azure HDInsight.

* [Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md). Cluster aanpassing tooinstall die solr op HDInsight Hadoop-clusters gebruiken. Solr kunt u krachtige zoekopdrachten tooperform opgeslagen gegevens.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
