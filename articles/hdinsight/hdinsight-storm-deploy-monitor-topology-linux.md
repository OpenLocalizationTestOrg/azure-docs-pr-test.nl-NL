---
title: "aaaDeploy en beheren van Apache Storm-topologieën op Linux gebaseerde HDInsight | Microsoft Docs"
description: "Ontdek hoe toodeploy, bewaken en beheren van Apache Storm-topologieën Hallo Storm-Dashboard met op Linux gebaseerde HDInsight. Hadoop-hulpprogramma's voor Visual Studio gebruiken."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Implementeren en beheren van Apache Storm-topologieën op HDInsight

Informatie over Hallo basisprincipes van beheer en controle van Storm-topologieën uitgevoerd op Storm op HDInsight-clusters in dit document.

> [!IMPORTANT]
> Hallo moet stappen in dit artikel een op Linux gebaseerde Storm op HDInsight-cluster. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. 
>
> Zie voor informatie over het implementeren en bewaken van topologieën op HDInsight op basis van Windows, [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Vereisten

* **Een op Linux gebaseerde Storm op HDInsight-cluster**: Zie [aan de slag met Apache Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) voor stapsgewijze instructies voor het maken van een cluster

* (Optioneel) **Kennis van SSH en SCP**: Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Optioneel) **Visual Studio**: Azure SDK 2.5.1 of hoger en hello Data Lake Tools voor Visual Studio. Zie voor meer informatie [aan de slag met Data Lake Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Een van de volgende versies van Visual Studio Hallo:

  * Visual Studio 2012 met [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 met [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (alle versies)

  * Visual Studio 2017 (alle versies). Data Lake Tools voor Visual Studio 2017 worden geïnstalleerd als onderdeel van hello Azure werkbelasting.

## <a name="submit-a-topology-visual-studio"></a>Verzenden van een topologie: Visual Studio

Hallo HDInsight-hulpprogramma's kunnen worden gebruikt toosubmit C# of hybride topologieën tooyour Storm-cluster. Hallo stappen te volgen, gebruiken een voorbeeldtoepassing. Zie voor meer informatie over het maken van uw eigen topologieën met behulp van Hallo HDInsight Tools [C#-topologieën ontwikkelen met Hallo HDInsight Tools voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Als u hebt niet is gebeurd Hallo meest recente versie van Hallo Data Lake tools voor Visual Studio, Zie [aan de slag met Data Lake Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hallo Data Lake Tools voor Visual Studio werden voorheen Hallo HDInsight Tools voor Visual Studio.
    >
    > Data Lake Tools voor Visual Studio zijn opgenomen in Hallo __Azure werkbelasting__ voor Visual Studio 2017.

2. Open Visual Studio, selecteer **bestand** > **nieuw** > **Project**.

3. In Hallo **nieuw Project** dialoogvenster Vouw **geïnstalleerde** > **sjablonen**, en selecteer vervolgens **HDInsight**. Selecteer in de lijst met sjablonen Hallo **Storm voorbeeld**. Typ een naam voor de toepassing hello Hallo onderaan in het dialoogvenster voor Hallo in.

    ![Afbeelding](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.

   > [!NOTE]
   > Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement. Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.

5. Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**. U kunt controleren of Hallo verzending is voltooid met Hallo **uitvoer** venster.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Verzenden van een topologie: SSH en hello Storm-opdracht

1. SSH tooconnect toohello HDInsight-cluster gebruiken. Vervang **gebruikersnaam** Hallo-naam van uw SSH-aanmelding. Vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Voor meer informatie over het gebruik van SSH tooconnect tooyour HDInsight-cluster, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Gebruik Hallo opdracht toostart een voorbeeldtopologie te volgen:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Deze opdracht start Hallo WordCount-voorbeeldtopologie op Hallo-cluster. Deze topologie genereren willekeurig zinnen en aantal Hallo exemplaar van elk woord in Hallo zinnen.

   > [!NOTE]
   > Bij het indienen van topologie toohello cluster, moet u eerst Hallo jar-bestand met de Hallo cluster voordat u Hallo kopiëren `storm` opdracht. toocopy hello toohello bestandscluster, kunt u Hallo `scp` opdracht. Bijvoorbeeld: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > Hallo WordCount-voorbeeld en andere storm starter-voorbeelden zijn al opgenomen in uw cluster op `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Verzenden van een topologie: programmatisch

U kunt een topologie tooStorm op HDInsight programmatisch implementeren met communiceren met de Hallo Nimbus service die wordt gehost in uw cluster. [https://github.com/Azure-Samples/hdinsight-Java-Deploy-storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) bevat een voorbeeld van Java-toepassing die u laat zien hoe toodeploy en een topologie via Hallo Nimbus-service te starten.

## <a name="monitor-and-manage-visual-studio"></a>Bewaken en beheren: Visual Studio

Wanneer een topologie is verzonden met behulp van Visual Studio, Hallo **Storm-topologieën** weergeven voor Hallo cluster weer te geven. Selecteer Hallo-topologie in Hallo lijst tooview informatie over Hallo topologie wordt uitgevoerd.

![monitor voor Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> U kunt ook weergeven **Storm-topologieën** van **Server Explorer** door het uitbreiden van **Azure** > **HDInsight**, en klik vervolgens met de rechtermuisknop op een Storm op HDInsight-cluster en het selecteren van **weergave Storm-topologieën**.

Selecteer Hallo shape voor Hallo spouts of bolts tooview informatie over deze onderdelen. Er wordt een nieuw venster geopend voor elk item geselecteerd.

### <a name="deactivate-and-reactivate"></a>Deactiveren en opnieuw activeren

Een topologie deactiveren onderbreekt het totdat dit is afgesloten of opnieuw geactiveerd. tooperform deze bewerkingen gebruik Hallo __deactiveren__ en __opnieuw activeren__ knoppen bovenaan Hallo Hallo __Topology Summary__.

### <a name="rebalance"></a>Opnieuw verdelen

Herverdeling van een topologie kunt Hallo system toorevise Hallo parallelle uitvoering van Hallo topologie. Als u hebt het formaat gewijzigd Hallo cluster tooadd meer notities, kan herverdeling bijvoorbeeld een topologie toosee Hallo nieuwe knooppunten.

een topologie toorebalance gebruiken Hallo __opnieuw verdelen__ knop bovenaan Hallo Hallo __Topology Summary__.

> [!WARNING]
> Eerst een topologie herverdeling Hallo-topologie, deactiveert opnieuw werknemers gelijkmatig verdeeld over Hallo cluster vervolgens, tot slot wordt Hallo topologie toohello staat voordat herverdeling is opgetreden. Dus als Hallo topologie actief was, wordt het actieve opnieuw. Als deze is uitgeschakeld, blijft deze gedeactiveerd.

### <a name="kill-a-topology"></a>Een topologie voor afsluiten

Storm-topologieën blijft in uitvoering totdat ze zijn gestopt of Hallo cluster wordt verwijderd. een topologie toostop gebruiken Hallo __Kill__ knop bovenaan Hallo Hallo __Topology Summary__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Bewaken en beheren: SSH en hello Storm-opdracht

Hallo `storm` hulpprogramma kunt u toowork met actieve topologieën vanaf de opdrachtregel Hallo. Gebruik `storm -h` voor een volledige lijst met opdrachten.

### <a name="list-topologies"></a>Lijst met topologieën

Hallo opdracht toolist na alle actieve topologieën gebruiken:

    storm list

Met deze opdracht retourneert informatie vergelijkbare toohello volgende tekst:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Deactiveren en opnieuw activeren

Een topologie deactiveren onderbreekt het totdat dit is afgesloten of opnieuw geactiveerd. Gebruik Hallo opdracht toodeactivate te volgen en opnieuw activeren:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Voor het afsluiten van een actieve topologie

Storm-topologieën, na het starten, gaat u verder uitgevoerd totdat deze wordt gestopt. toostop een topologie Hallo volgende opdracht gebruiken:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Opnieuw verdelen

Herverdeling van een topologie kunt Hallo system toorevise Hallo parallelle uitvoering van Hallo topologie. Als u hebt het formaat gewijzigd Hallo cluster tooadd meer notities, kan herverdeling bijvoorbeeld een topologie toosee Hallo nieuwe knooppunten.

> [!WARNING]
> Eerst een topologie herverdeling Hallo-topologie, deactiveert opnieuw werknemers gelijkmatig verdeeld over Hallo cluster vervolgens, tot slot wordt Hallo topologie toohello staat voordat herverdeling is opgetreden. Dus als Hallo topologie actief was, wordt het actieve opnieuw. Als deze is uitgeschakeld, blijft deze gedeactiveerd.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Bewaken en beheren: Storm-gebruikersinterface

Hallo Storm-gebruikersinterface biedt een webinterface voor het werken met actieve topologieën en is opgenomen op uw HDInsight-cluster. tooview hello Storm-gebruikersinterface, gebruikt u een web browser tooopen **https://CLUSTERNAME.azurehdinsight.NET/stormui**, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.

> [!NOTE]
> Als u wordt gevraagd tooprovide een gebruikersnaam en wachtwoord, Voer Hallo Clusterbeheerder (admin) en het wachtwoord dat u hebt gebruikt toen maken Hallo-cluster.

### <a name="main-page"></a>Hoofdpagina

Hallo hoofdpagina Hallo Storm-gebruikersinterface biedt Hallo volgende informatie:

* **Cluster samenvatting**: algemene informatie over Hallo Storm-cluster.
* **Topologie samenvatting**: een lijst met actieve topologieën. Hallo-koppelingen in deze sectie tooview meer informatie over specifieke topologieën gebruiken.
* **Supervisor samenvatting**: informatie over Hallo Storm supervisor.
* **Nimbus configuratie**: Nimbus-configuratie voor Hallo-cluster.

### <a name="topology-summary"></a>Topologie samenvatting

Wanneer u een koppeling van Hallo **Topology summary** sectie vindt u informatie over het Hallo-topologie na Hallo:

* **Topologie samenvatting**: algemene informatie over het Hallo-topologie.
* **Topologie acties**: acties die u voor Hallo-topologie uitvoeren kunt.

  * **Activeren**: verwerking van een gedeactiveerde topologie wordt hervat.
  * **Deactiveren**: een actieve topologie wordt onderbroken.
  * **Opnieuw verdelen**: Hallo parallelle uitvoering van Hallo-topologie wordt aangepast. Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen. Deze bewerking kunt Hallo topologie tooadjust parallelle uitvoering toocompensate voor Hallo verhoogd of verlaagd aantal knooppunten in het Hallo-cluster.

    Zie voor meer informatie <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">begrijpen Hallo parallelle uitvoering van een Storm-topologie</a>.
  * **Kill**: een Storm-topologie wordt beëindigd nadat Hallo time-out opgegeven.
* **Topology stats**: statistieken over Hallo-topologie. tooset Hallo periode Hallo resterend posten op Hallo pagina, gebruik Hallo koppelingen in Hallo **venster** kolom.
* **Spouts**: Hallo spouts die wordt gebruikt door het Hallo-topologie. Hallo-koppelingen in deze sectie tooview meer informatie over specifieke spouts gebruiken.
* **Bolts**: Hallo bolts gebruikt door het Hallo-topologie. Gebruik Hallo koppelingen in deze sectie tooview meer informatie over specifieke bolts.
* **Topologieconfiguratie**: Hallo configuratie van de topologie Hallo geselecteerd.

### <a name="spout-and-bolt-summary"></a>Spout en Bolt samenvatting

Selecteren van een spout in Hallo **Spouts** of **Bolts** secties Hallo volgende informatie over Hallo geselecteerd item wordt weergegeven:

* **Overzicht van onderdelen**: algemene informatie over Hallo spout of bolt.
* **Spout/Bolt stats**: statistieken over Hallo spout of Bolts. tooset Hallo periode Hallo resterend posten op Hallo pagina, gebruik Hallo koppelingen in Hallo **venster** kolom.
* **Input stats** (alleen Bolts): informatie over Hallo invoerstromen verbruikt door Hallo bolt.
* **Output stats**: informatie over Hallo stromen die door dit spout of Bolts.
* **Executor**: informatie over het Hallo-exemplaren van Hallo spout of bolt. Selecteer Hallo **poort** vermelding voor een specifieke executor tooview een logboek van diagnostische gegevens geproduceerd voor dit exemplaar.
* **Fouten**: alle informatie over de fout voor deze spout of Bolts.

## <a name="monitor-and-manage-rest-api"></a>Bewaken en beheren: REST-API

Hallo Storm-gebruikersinterface is gebaseerd op Hallo REST API, zodat u kunt vergelijkbare management en de controlefunctionaliteit met behulp van Hallo REST-API. U kunt Hallo REST-API toocreate aangepaste hulpprogramma's gebruiken voor het beheren en controleren van Storm-topologieën.

Zie voor meer informatie [Storm UI REST-API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Hallo is volgende informatie specifiek toousing Hallo REST-API met Apache Storm op HDInsight.

> [!IMPORTANT]
> Hallo Storm REST-API is niet openbaar beschikbaar Hallo internet, en moet worden geopend met behulp van een SSH-tunnel toohello HDInsight-cluster hoofdknooppunt. Zie voor meer informatie over het maken en gebruiken van een SSH-tunnel [SSH-Tunneling gebruiken tooaccess Ambari web-UI, ResourceManager JobHistory, NameNode, Oozie en andere web-UI](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>Basis-URI

Hallo basis-URI voor Hallo REST-API op Linux gebaseerde HDInsight-clusters is beschikbaar op Hallo hoofdknooppunt op **https://HEADNODEFQDN:8744/api/v1/**. Hallo-domeinnaam van het hoofdknooppunt Hallo wordt gegenereerd tijdens het maken van het cluster en is niet statisch.

Hallo volledig gekwalificeerde domeinnaam (FQDN) voor het hoofdknooppunt van de cluster Hallo vindt u op verschillende manieren:

* **Tijdens een SSH-sessie**: Gebruik de opdracht Hallo `headnode -f` van een SSH-sessie toohello cluster.
* **Vanaf Ambari Web**: Selecteer **Services** van Hallo bovenaan pagina hello, selecteer **Storm**. Van Hallo **samenvatting** tabblad **Storm UI Server**. Hallo FQDN-naam van het Hallo-knooppunt dat Hallo Storm-gebruikersinterface en REST-API wordt uitgevoerd is bovenaan Hallo Hallo pagina.
* **Van de Ambari REST-API**: Gebruik de opdracht Hallo `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informatie over het Hallo-knooppunt dat Hallo Storm-gebruikersinterface en REST-API worden uitgevoerd op. Vervang **wachtwoord** met Hallo beheerderswachtwoord voor Hallo-cluster. Vervang **CLUSTERNAME** met de naam van de cluster Hallo. Hallo-antwoord wordt bevat Hallo 'hostnaam' vermelding Hallo FQDN-naam van het Hallo-knooppunt.

### <a name="authentication"></a>Authentication

Aanvragen toohello REST-API moet gebruiken **basisverificatie**, zodat u Hallo HDInsight-cluster beheerdersnaam en het wachtwoord gebruiken.

> [!NOTE]
> Omdat basisverificatie wordt verzonden met behulp van de versleutelde tekst, moet u **altijd** toosecure-HTTPS-communicatie met de Hallo-cluster gebruiken.

### <a name="return-values"></a>Waarden geretourneerd

Informatie die wordt geretourneerd vanaf Hallo REST-API is mogelijk alleen bruikbaar uit binnen Hallo cluster of virtuele machines op Hallo hetzelfde virtuele Azure-netwerk als Hallo-cluster. Hallo volledig gekwalificeerde domeinnaam (FQDN) geretourneerd voor Zookeeper servers is bijvoorbeeld niet worden toegankelijk is vanaf Internet Hallo.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe toodeploy en monitor topologieën met behulp van Storm-Dashboard hello, kunt u nagaan hoe te[ontwikkelen van Java gebaseerde topologieën met Maven](hdinsight-storm-develop-java-topology.md).

Zie voor een lijst van meer voorbeeldtopologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).
