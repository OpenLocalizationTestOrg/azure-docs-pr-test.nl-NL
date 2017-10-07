---
title: aaaHue met Hadoop op HDInsight Linux-clusters - Azure | Microsoft Docs
description: Informatie over hoe tooinstall Hue op HDInsight-clusters en tunneling tooroute Hallo aanvragen tooHue gebruiken. Hue toobrowse opslag gebruiken en Hive of Pig uitvoeren.
keywords: HUE hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Installeren en gebruiken van Hue op HDInsight Hadoop-clusters

Informatie over hoe tooinstall Hue op HDInsight-clusters en tunneling tooroute Hallo aanvragen tooHue gebruiken.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="what-is-hue"></a>Wat is Hue?
HUE is dat een set van webtoepassingen toointeract gebruikt met een Hadoop-cluster. U kunt Hue toobrowse Hallo opslag die is gekoppeld aan een Hadoop-cluster (in geval van HDInsight-clusters Hallo WASB) gebruiken, uitvoeren van Hive-taken en Pig-scripts, enzovoort. Hallo zijn volgende onderdelen beschikbaar met Hue-installaties op een HDInsight Hadoop-cluster.

* Bijenwas Hive-Editor
* Pig
* Metastore manager
* Oozie
* FileBrowser (die wordt gesproken standaardcontainer tooWASB)
* Taak Browser

> [!WARNING]
> Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support zal helpen tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.
>
> Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen. Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Met behulp van scriptacties Hue installeren

Hallo script tooinstall Hue op een Linux gebaseerde HDInsight-cluster is beschikbaar op https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. U kunt dit script tooinstall Hue op clusters met Azure Storage-Blobs (WASB) of Azure Data Lake Store als standaard opslag gebruiken.

Deze sectie bevat instructies over hoe toouse script Hallo bij het inrichten van Hallo-cluster met behulp van hello Azure-portal.

> [!NOTE]
> Gebruikte tooapply scriptacties kunnen ook worden door Azure PowerShell, hello Azure CLI, Hallo HDInsight .NET SDK of Azure Resource Manager-sjablonen. U kunt ook script acties tooalready actieve clusters toepassen. Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Start met het inrichten van een cluster met behulp van de stappen in Hallo [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md), maar inrichting niet voltooid.

   > [!NOTE]
   > Hue tooinstall op HDInsight-clusters, hello headnode aanbevolen grootte is ten minste A4 (8 kerngeheugens, 14 GB geheugen).
   >
   >
2. Op Hallo **optionele configuratie** blade Selecteer **scriptacties**, en Hallo informatie te bieden, zoals hieronder wordt weergegeven:

    ![Script actieparameters bieden voor Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "script actieparameters bieden voor Hue")

   * **NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.
   * **SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: Schakel deze optie
   * **WERKNEMER**: leeg laten.
   * **ZOOKEEPER**: leeg laten.
   * **PARAMETERS**: leeg laten.
3. Hallo Hallo onderaan in **scriptacties**, hello gebruiken **Selecteer** knop toosave Hallo configuratie. Gebruik tot slot Hallo **Selecteer** knop onderin Hallo Hallo **optionele configuratie** blade toosave Hallo optionele configuratie-informatie.
4. Doorgaan Hallo cluster inrichten, zoals beschreven in [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Hue gebruiken met HDInsight-clusters

SSH-Tunneling is Hallo alleen manier-tooaccess Hue op Hallo cluster zodra deze wordt uitgevoerd. Hallo verkeer toogo via SSH-tunneling worden kunnen rechtstreeks toohello headnode Hallo cluster waarop Hue wordt uitgevoerd. Nadat het Hallo cluster inrichten is voltooid, gebruikt u Hallo stappen toouse Hue te volgen op een HDInsight Linux-cluster.

> [!NOTE]
> Wordt u aangeraden Firefox web browser toofollow Hallo onderstaande instructies.
>
>

1. Hallo-informatie in [SSH-Tunneling gebruiken tooaccess Ambari web-UI, ResourceManager JobHistory, NameNode, Oozie en andere Webgebruikersinterface](hdinsight-linux-ambari-ssh-tunnel.md) toocreate een SSH tunnel uit uw client system toohello HDInsight-cluster en vervolgens configureren uw Web browser toouse Hallo SSH-tunnel als een proxy.

2. Zodra u hebt een SSH-tunnel gemaakt en uw browser tooproxy verkeer via deze geconfigureerd, moet u Hallo-hostnaam van de primaire hoofdknooppunt Hallo zoeken. U kunt dit doen door verbinding te maken via SSH op poort 22 toohello-cluster. Bijvoorbeeld: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` waar **gebruikersnaam** uw SSH-gebruikersnaam en **CLUSTERNAME** Hallo-naam van uw cluster.

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

3. Eenmaal zijn verbonden, gebruikt u Hallo opdracht tooobtain Hallo volledig gekwalificeerde domeinnaam van de primaire headnode hello te volgen:

        hostname -f

    Hiermee herstelt u een naam vergelijkbare toohello volgende:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Dit is Hallo hostnaam van de primaire headnode Hallo waar Hallo Hue website zich bevindt.
4. Gebruik http://HOSTNAME:8888 Hallo browser tooopen Hallo Hue-portal. HOSTNAME vervangen door Hallo-naam die u hebt verkregen in de vorige stap Hallo.

   > [!NOTE]
   > Wanneer u zich aanmeldt voor Hallo eerst, kunt u zich na vragen aan gebruiker toocreate een account toolog in toohello Hue-portal. Hallo-referenties die u hier opgeeft, wordt beperkt toohello portal en zijn geen verwante toohello admin of SSH-gebruikersreferenties die u hebt opgegeven tijdens het Hallo-cluster inrichten.
   >
   >

    ![Aanmelding toohello Hue-portal](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Geef referenties op voor de Hue-portal")

### <a name="run-a-hive-query"></a>Een Hive-query uitvoeren
1. Hallo Hue-portal, klik op **Query Editors**, en klik vervolgens op **Hive** tooopen Hallo Hive-editor.

    ![Hive gebruiken](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Hive gebruiken")
2. Op Hallo **helpen** tabblad onder **Database**, ziet u **hivesampletable**. Dit is een voorbeeldtabel dat bij alle Hadoop-clusters in HDInsight wordt geleverd. Voer een voorbeeldquery in het rechterdeelvenster Hallo en Hallo uitvoer zien op Hallo **resultaten** tabblad in deelvenster Hallo hieronder, zoals wordt weergegeven in de schermopname Hallo.

    ![Uitvoeren van Hive-query](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "uitvoeren Hive-query")

    U kunt ook Hallo **grafiek** tabblad toosee een visuele representatie van Hallo resultaat.

### <a name="browse-hello-cluster-storage"></a>Hallo clusteropslag bladeren
1. Hallo Hue-portal, klik op **bestandsbrowser** in Hallo rechterbovenhoek van de menubalk Hallo.
2. Standaard Hallo bestandsbrowser wordt geopend op Hallo **/gebruiker/myuser** directory. Klik op een slash Hallo aan vóór de gebruikerslijst Hallo in Hallo pad toogo toohello hoofdmap van hello Azure storage-container die is gekoppeld aan het Hallo-cluster.

    ![Gebruik de Verkenner](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "gebruik bestandsbrowser")
3. Klik met de rechtermuisknop op een bestand of map toosee Hallo beschikbare bewerkingen. Gebruik Hallo **uploaden** knop in Hallo rechterhoek tooupload bestanden toohello huidige map. Gebruik Hallo **nieuw** knop toocreate nieuwe bestanden of mappen.

> [!NOTE]
> Hallo Hue-bestandsbrowser kan alleen Hallo-inhoud van Hallo standaardcontainer die zijn gekoppeld aan de HDInsight-cluster Hallo weergeven. Geen extra opslagruimte accounts/containers die u mogelijk hebt gekoppeld aan het Hallo-cluster meer niet toegankelijk met Hallo bestandsbrowser. Hallo extra containers die zijn gekoppeld aan het Hallo-cluster wordt echter altijd zijn toegankelijk voor Hallo Hive-taken. Bijvoorbeeld, als u de opdracht Hallo `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` in Hallo Hive-editor, ziet u Hallo inhoud van evenals aanvullende containers. In deze opdracht **newcontainer** is geen standaardcontainer Hallo die zijn gekoppeld aan een cluster.
>
>

## <a name="important-considerations"></a>Belangrijke overwegingen
1. Hallo-script waarmee tooinstall Hue installeert deze alleen op primaire headnode Hallo van Hallo-cluster.

2. Tijdens de installatie worden meerdere Hadoop-services (HDFS, YARN, MR2, Oozie) voor het bijwerken van de configuratie van de Hallo opnieuw gestart. Nadat het Hallo-script is voltooid Hue installeren, kan het enige tijd voor andere services Hadoop toostart duren. Dit mogelijk invloed op de prestaties van de Hue in eerste instantie. Nadat alle services worden gestart, wordt Hue volledig functioneel zijn.
3. HUE begrijpt niet Tez-taken, de huidige standaardinstelling Hallo voor Hive. Als u toouse MapReduce wilt als de engine voor het uitvoeren van Hive hello, update Hallo script toouse Hallo opdracht in uw script te volgen:

        set hive.execution.engine=mr;

4. U kunt een scenario waar uw services worden uitgevoerd op de primaire headnode Hallo terwijl Hallo Resource Manager kan worden uitgevoerd op de secundaire Hallo hebben met Linux-clusters. Dit scenario kan leiden tot fouten (Zie hieronder) wanneer u Hue tooview details van de taken die wordt uitgevoerd op Hallo-cluster. U kunt echter Hallo Taakdetails weergeven wanneer Hallo-taak is voltooid.

   ![HUE-portal fout](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "portal Hue-fout")

   Dit komt doordat tooa bekend probleem. Als tijdelijke oplossing Ambari zodanig aanpassen dat hello active Resource Manager wordt ook uitgevoerd op de primaire headnode Hallo.
5. HUE begrijpt WebHDFS bij gebruik maken van HDInsight-clusters met behulp van Azure Storage `wasb://`. Hallo aangepaste scripts die worden gebruikt met scriptactie installeert dus WebWasb een WebHDFS compatibele-service voor tooWASB communiceren. Ja, hoewel Hallo Hue-portal HDFS op plaatsen zegt (zoals wanneer u de muisaanwijzer over Hallo **bestandsbrowser**), moet dit worden beschouwd als WASB.

## <a name="next-steps"></a>Volgende stappen
* [Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md). Cluster aanpassing tooinstall die giraph op HDInsight Hadoop-clusters gebruiken. Giraph kunt u tooperform grafiek verwerken met Hadoop en deze kan worden gebruikt met Azure HDInsight.
* [Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md). Cluster aanpassing tooinstall die solr op HDInsight Hadoop-clusters gebruiken. Solr kunt u krachtige zoekopdrachten tooperform opgeslagen gegevens.
* [R installeren op HDInsight-clusters](hdinsight-hadoop-r-scripts-linux.md). Cluster aanpassing tooinstall R op HDInsight Hadoop-clusters gebruiken. R is een open source-taal en de omgeving voor statistische computing. Het biedt honderden ingebouwde statistische functies en een eigen programmeertaal die aspecten van het functionele en objectgeoriënteerd programmeren combineert. Het bevat ook uitgebreide grafische mogelijkheden.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
