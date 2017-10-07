---
title: aaaStorm starter-voorbeelden op Apache Storm op HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toodo big data-analyses en gegevens in realtime verwerken met behulp van Apache Storm en Hallo storm starter-voorbeelden in HDInsight.
keywords: storm-starter, apache storm voorbeeld
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Aan de slag met Apache Storm op HDInsight met behulp van Hallo storm starter-voorbeelden

Meer informatie over hoe toouse Apache Storm in HDInsight met behulp Hallo storm starter-voorbeelden.

Apache Storm is een gedistribueerd, schaalbaar, fouttolerant en realtime berekeningssysteem voor het verwerken van gegevensstromen. Met Storm in Azure HDInsight kunt u een op een cloud gebaseerd Storm-cluster maken dat in realtime big data-analyses uitvoert.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Kennis van SSH en SCP**. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

## <a name="create-a-storm-cluster"></a>Een Storm-cluster maken

Gebruik Hallo stappen toocreate een Storm op HDInsight-cluster te volgen:

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer **+ nieuw**, **Intelligence en analyse**, en selecteer vervolgens **HDInsight**.

    ![Een HDInsight-cluster maken](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Van Hallo **basisbeginselen** blade Voer Hallo volgende informatie:

    * **Clusternaam**: Hallo-naam van Hallo HDInsight-cluster.
    * **Abonnement**: Hallo abonnement toouse selecteren.
    * **Gebruikersnaam voor aanmelding cluster** en **Cluster aanmeldingswachtwoord**: Hallo aanmelding bij het openen van Hallo-cluster via HTTPS. U gebruikt deze referenties tooaccess services zoals Hallo Ambari-Webgebruikersinterface of REST-API.
    * **Secure Shell (SSH) gebruikersnaam**: Hallo-aanmeldingsnaam die wordt gebruikt bij het openen van Hallo-cluster via SSH. Standaard is Hallo wachtwoord Hallo hetzelfde als Hallo aanmelding het wachtwoord van het cluster.
    * **Resourcegroep**: Hallo resource groep toocreate Hallo cluster in.
    * **Locatie**: hello Azure-regio toocreate Hallo cluster in.

    ![Abonnement selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Selecteer **type Cluster**, en vervolgens Hallo set waarden op Hallo **clusterconfiguratie** blade:

    * **Clustertype**: Storm

    * **Besturingssysteem**: Linux

    * **Versie**: Storm 1.1.0 (HDI 3.6)

    * **Clusterlaag**: standaard

    Gebruik tot slot Hallo **Selecteer** knop toosave instellingen.

    ![Clustertype selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Gebruik na het selecteren van clustertype Hallo Hallo __Selecteer__ knoptype tooset Hallo-cluster. Gebruik vervolgens Hallo __volgende__ knop toofinish basisconfiguratie.

5. Van Hallo **opslag** blade selecteren of een opslagaccount maken. Voor Hallo stappen in dit document, laat u Hallo andere velden op deze blade Hallo standaardwaarden. Gebruik Hallo __volgende__ knop toosave opslagconfiguratie.

    ![Hallo-opslag-accountinstellingen voor HDInsight instellen](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Van Hallo **samenvatting** blade Hallo-configuratie controleren voor Hallo-cluster. Gebruik Hallo __bewerken__ koppelingen toochange alle instellingen die onjuist zijn. Gebruik tot slot the__Create__ knop toocreate Hallo cluster.

    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Too20 minuten toocreate Hallo cluster kan duren.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Een Storm Starter-voorbeeld uitvoeren in HDInsight

1. Verbinding maken met toohello HDInsight-cluster via SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Als u een wachtwoord toosecure uw SSH gebruikersaccount gebruikt, bent u na vragen aan gebruiker tooenter deze. Als u een openbare sleutel gebruikt, kunt u moet gebruiken Hallo `-i` parameter toospecify Hallo overeenkomende persoonlijke sleutel. Bijvoorbeeld `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Gebruik Hallo opdracht toostart een voorbeeldtopologie te volgen:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > In eerdere versies van HDInsight Hallo klassenaam van Hallo-topologie is `storm.starter.WordCountTopology` in plaats van `org.apache.storm.starter.WordCountTopology`.

    Deze opdracht start Hallo WordCount-voorbeeldtopologie Hallo-cluster met een beschrijvende naam voor 'wordcount'. Deze genereert willekeurig zinnen en aantal Hallo exemplaar van elk woord in Hallo zinnen.

    > [!NOTE]
    > Bij het indienen van uw eigen topologieën toohello-cluster, moet u eerst Hallo jar-bestand met de Hallo cluster voordat u Hallo kopiëren `storm` opdracht. Gebruik Hallo `scp` opdrachtbestand toocopy Hallo. Bijvoorbeeld: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > Hallo WordCount-voorbeeld en andere storm starter-voorbeelden zijn al opgenomen in uw cluster op `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Als u geïnteresseerd bent in Hallo bron voor de storm starter-voorbeelden Hallo weergeven, kunt u vinden Hallo code aan [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Deze koppeling is voor Storm 1.1.x, geleverd bij HDInsight 3.6. Gebruik voor andere versies van Storm Hallo __vertakking__ knop Hallo Hallo pagina tooselect bovenaan in een andere versie van Storm.

## <a name="monitor-hello-topology"></a>Monitor Hallo-topologie

Hallo Storm-gebruikersinterface biedt een webinterface voor het werken met actieve topologieën en is opgenomen op uw HDInsight-cluster.

Hallo stappen toomonitor Hallo topologie Hallo Storm-gebruikersinterface met volgende gebruiken:

1. toodisplay hello Storm-gebruikersinterface, opent u een web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Vervang **CLUSTERNAME** met Hallo-naam van het cluster.

    > [!NOTE]
    > Als u wordt gevraagd tooprovide een gebruikersnaam en wachtwoord, Voer Hallo Clusterbeheerder (admin) en het wachtwoord dat u hebt gebruikt toen maken Hallo-cluster.

2. Onder **Topology summary**, selecteer Hallo **wordcount** vermelding in Hallo **naam** kolom. Informatie over het Hallo-topologie wordt weergegeven.

    ![Storm-dashboard met informatie over de Storm-Starter WordCount-topologie.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Deze pagina bevat Hallo volgende informatie:

    * **Topology stats** -basisinformatie over Hallo topologieprestaties, geordend in tijdvensters.

        > [!NOTE]
        > Als u een specifiek tijdstip venster wijzigingen Hallo tijdvenster voor informatie die wordt weergegeven in andere gedeelten van Hallo pagina selecteert.

    * **Spouts** -basisinformatie over spouts, met inbegrip van Hallo laatste fout die door elke spout is geretourneerd.

    * **Bolts**: basisinformatie over bolts.

    * **Topologieconfiguratie** -gedetailleerde informatie over de configuratie van de Hallo-topologie.

    Deze pagina bevat ook de acties die kunnen worden uitgevoerd op Hallo-topologie:

    * **Activate**: de verwerking van een gedeactiveerde topologie wordt hervat.

    * **Deactivate**: een actieve topologie wordt onderbroken.

    * **Opnieuw verdelen** -Hallo parallelle uitvoering van Hallo-topologie wordt aangepast. Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen. Parallelle uitvoering toocompensate voor Hallo toegenomen/afgenomen aantal knooppunten in cluster Hallo herverdeling worden aangepast. Zie voor meer informatie [begrijpen Hallo parallelle uitvoering van een Storm-topologie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kill** -beëindigt een Storm-topologie nadat Hallo time-out opgegeven.

3. Op deze pagina, selecteert u een vermelding uit Hallo **Spouts** of **Bolts** sectie. Informatie over het geselecteerde onderdeel hello wordt weergegeven.

    ![Storm-dashboard met informatie over de geselecteerde onderdelen.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Deze pagina wordt weergegeven Hallo volgende informatie:

    * **Spout/Bolt stats** -basisinformatie over de prestaties van de component hello, geordend in tijdvensters.

        > [!NOTE]
        > Als u een specifiek tijdstip venster wijzigingen Hallo tijdvenster voor informatie die wordt weergegeven in andere gedeelten van Hallo pagina selecteert.

    * **Input stats** (alleen Bolts): informatie over onderdelen die gegevens die worden gebruikt door de bolt Hallo produceren.

    * **Output stats**: informatie over gegevens die door deze bolt zijn gegenereerd.

    * **Executors**: informatie over exemplaren van dit onderdeel.

    * **Errors**: fouten die door dit onderdeel zijn gegenereerd.

4. Wanneer u bekijkt hello details van een spout of bolt, selecteert u een vermelding uit Hallo **poort** kolom in Hallo **Executor** sectie tooview details voor een specifiek exemplaar van het Hallo-onderdeel.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    In dit voorbeeld Hallo word **zeven** 1493957 keer voorkwam. Dit aantal is het aantal keren Hallo woord is gevonden sinds deze topologie is gestart.

## <a name="stop-hello-topology"></a>Hallo-topologie stoppen

Toohello retourneren **Topology summary** pagina voor Hallo word-count-topologie en selecteer vervolgens Hallo **Kill** knop van Hallo **Topology actions** sectie. Wanneer u wordt gevraagd, voert u 10 voor Hallo seconden toowait voordat Hallo-topologie wordt gestopt. Na het Hallo-time-outperiode Hallo topologie niet meer wordt weergegeven wanneer u Hallo **Storm-gebruikersinterface** sectie van het Hallo-dashboard.

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u een probleem ondervindt met het maken van een HDInsight-cluster.

## <a id="next"></a>Volgende stappen

In deze zelfstudie voor Apache Storm, hebt u geleerd Hallo basisbeginselen van het werken met Storm op HDInsight. Vervolgens leert u hoe te[ontwikkelen van Java gebaseerde topologieën met Maven](hdinsight-storm-develop-java-topology.md).

Als u al bekend bent met het ontwikkelen van Java gebaseerde topologieën en een bestaande topologie tooHDInsight toodeploy, Zie [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Als u .NET-ontwikkelaar bent, kunt u C#- of hybride C#-/Java-topologieën maken met Visual Studio. Zie [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Hadoop-hulpprogramma's voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) voor meer informatie.

Zie voor voorbeeldtopologieën die kunnen worden gebruikt met Storm op HDInsight Hallo volgen voorbeelden:

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
