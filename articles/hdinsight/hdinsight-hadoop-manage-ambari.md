---
title: aaaMonitor en beheren van Azure HDInsight met behulp van de Ambari-Webgebruikersinterface | Microsoft Docs
description: Meer informatie over hoe toouse Ambari toomonitor en Linux gebaseerde HDInsight-clusters beheren. In dit document leert u hoe toouse hello Ambari-Webgebruikersinterface opgenomen met HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari vereenvoudigt het Hallo-beheer en bewaking van een Hadoop-cluster met een eenvoudig toouse web UI en REST-API. Ambari is opgenomen op Linux gebaseerde HDInsight-clusters en gebruikte toomonitor Hallo cluster uit en maak configuratiewijzigingen is.

In dit document leert u hoe toouse Ambari-Webgebruikersinterface Hallo met een HDInsight-cluster.

## <a id="whatis"></a>Wat is Ambari?

[Apache Ambari](http://ambari.apache.org) vereenvoudigt Hadoop-beheer door de webgebruikersinterface van een eenvoudig te gebruiken. Kunt u Ambari maken, beheren en bewaken van Hadoop-clusters. Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van Hallo [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Hallo Ambari-Webgebruikersinterface standaard met HDInsight-clusters die gebruikmaken van Hallo Linux-besturingssysteem is opgegeven.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. 

## <a name="connectivity"></a>Connectiviteit

Hallo Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op HTTPS://CLUSTERNAME.azurehdidnsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.

> [!IMPORTANT]
> Verbinding maken met tooAmbari op HDInsight HTTPS is vereist. Wanneer u om verificatie wordt gevraagd, gebruik Hallo admin-accountnaam en wachtwoord die u hebt opgegeven tijdens het Hallo-cluster is gemaakt.

## <a name="ssh-tunnel-proxy"></a>SSH-tunnel (proxy)

Terwijl de Ambari voor uw cluster toegankelijk is rechtstreeks via Internet hello, Hallo enkele koppelingen van Hallo Ambari-Webgebruikersinterface (zoals toohello JobTracker) worden niet weergegeven op internet. tooaccess deze services, moet u een SSH-tunnel maken. Zie voor meer informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Ambari-webgebruikersinterface

Wanneer u verbinding maakt toohello Ambari-Webgebruikersinterface, zijn na vragen aan gebruiker tooauthenticate toohello pagina. Gebruik Hallo cluster admin-gebruiker (standaard Admin) en het wachtwoord waarmee u tijdens het maken van het cluster.

Let op Hallo balk Hallo boven wanneer Hallo pagina wordt geopend. Deze balk bevat Hallo volgende informatie en besturingselementen:

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Ambari-logo** -wordt geopend Hallo dashboard, dat gebruikt toomonitor Hallo-cluster worden kan.

* **Naam # ops cluster** -geeft het aantal actieve Ambari bewerkingen Hallo weer. Naam van de cluster te selecteren Hallo of **# ops** geeft een lijst met bewerkingen op de achtergrond.

* **waarschuwingen voor #** -waarschuwingen of kritieke waarschuwingen weergeven, indien aanwezig, voor Hallo-cluster.

* **Dashboard** -geeft Hallo dashboard.

* **Services** -gegevens en configuratie-instellingen voor Hallo-services in het Hallo-cluster.

* **Hosts** -gegevens en configuratie-instellingen voor Hallo knooppunten in Hallo-cluster.

* **Waarschuwingen** -een logboek van informatie, waarschuwingen en kritieke waarschuwingen.

* **Beheerder** -Software stack/services die zijn geïnstalleerd op het Hallo-cluster, informatie over serviceaccounts en Kerberos-beveiliging.

* **Knop Admin** -Ambari beheer, gebruikersinstellingen en meld u af.

## <a name="monitoring"></a>Bewaking

### <a name="alerts"></a>Waarschuwingen

Hallo bevat volgende lijst Hallo algemene waarschuwing statussen die worden gebruikt door Ambari:

* **OK**
* **Waarschuwing**
* **KRITIEKE**
* **ONBEKEND**

Anders dan waarschuwingen **OK** veroorzaken Hallo **# waarschuwingen** vermelding bovenaan Hallo Hallo pagina toodisplay Hallo aantal waarschuwingen. Als u dit item wordt weergegeven, Hallo waarschuwingen en hun status.

Waarschuwingen worden ingedeeld in verschillende standaardgroepen die kunnen worden bekeken in Hallo **waarschuwingen** pagina.

![pagina waarschuwingen](./media/hdinsight-hadoop-manage-ambari/alerts.png)

U kunt groepen Hallo beheren met behulp van Hallo **acties** menu en selecteer **waarschuwing groepen beheren**.

![dialoogvenster Waarschuwing groepen beheren](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

U kunt ook waarschuwingen methoden beheren en waarschuwingsmeldingen van Hallo **acties** menu door te selecteren __waarschuwing meldingen beheren__. Huidige meldingen worden weergegeven. U kunt ook meldingen van hieruit maken. Meldingen kunnen worden verzonden **e** of **SNMP** wanneer specifieke waarschuwing/ernst combinaties optreden. U kunt bijvoorbeeld een e-mailbericht wanneer een van de waarschuwingen Hallo op Hallo verzenden **YARN standaard** groep te ingesteld**Kritiek**.

![Waarschuwing dialoogvenster maken](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Ten slotte selecteren __Waarschuwingsinstellingen beheren__ van Hallo __acties__ menu kunt u tooset Hallo aantal keren dat een waarschuwing optreden moet voordat een melding wordt verzonden. Deze instelling kan worden gebruikt tooprevent meldingen voor tijdelijke fouten.

### <a name="cluster"></a>Cluster

Hallo **metrische gegevens** van Hallo dashboard bevat een reeks widgets om het eenvoudig toomonitor Hallo status van het cluster in één oogopslag. Verschillende widgets zoals **CPU-gebruik**, vindt u aanvullende informatie wanneer geklikt.

![dashboard met metrische gegevens](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Hallo **Heatmaps** tabblad metrische gegevens worden weergegeven als gekleurde heatmaps, van groen toored.

![dashboard met heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Selecteer voor meer informatie over Hallo knooppunten binnen Hallo cluster **Hosts**. Selecteer de specifieke knooppunt Hallo die u geïnteresseerd bent in.

![details van de host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Services

Hallo **Services** zijbalk op Hallo dashboard biedt snel inzicht in Hallo status van Hallo services die worden uitgevoerd op Hallo-cluster. Verschillende pictogrammen zijn gebruikte tooindicate status of acties die moeten worden uitgevoerd. Een gele recyclen symbool wordt bijvoorbeeld weergegeven als een service nodig toobe gerecycled heeft.

![Services Zijmarge](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> Hallo-services weergegeven verschillen van HDInsight-clustertypen en versies. Hallo-services wordt hier weergegeven mogelijk anders dan Hallo services die worden weergegeven voor uw cluster.

Selecteren van een service, geeft meer gedetailleerde informatie op Hallo-service.

![samenvattende informatie van service](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Snelkoppelingen

Sommige services weer een **snelkoppelingen** koppeling bovenaan Hallo Hallo pagina. Dit kan gebruikte tooaccess servicespecifieke web UI, zoals zijn:

* **Taakgeschiedenis** -geschiedenis van MapReduce-taak.
* **Resource Manager** -gebruikersinterface van YARN ResourceManager.
* **NameNode** -Hadoop Distributed File System (HDFS) NameNode gebruikersinterface.
* **Oozie-webgebruikersinterface** -Oozie-gebruikersinterface.

Wanneer u een van de volgende koppelingen, wordt een nieuw tabblad geopend in uw browser, die Hallo geselecteerde pagina wordt weergegeven.

> [!NOTE]
> Selecteren Hallo **snelkoppelingen** vermelding voor een service een fout 'de server is niet gevonden' retourneert. Als deze fout optreedt, moet u een SSH-tunnel gebruiken wanneer u Hallo **snelkoppelingen** post voor deze service. Zie voor informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)

## <a name="management"></a>Beheer

### <a name="ambari-users-groups-and-permissions"></a>Ambari-gebruikers, groepen en machtigingen

Werken met gebruikers, groepen en machtigingen worden ondersteund wanneer een [verbonden met het domein](hdinsight-domain-joined-introduction.md) HDInsight-cluster. Zie voor meer informatie over het gebruik van Hallo Ambari Management gebruikersinterface op een cluster domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Hallo-wachtwoord van Hallo Ambari watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster niet wijzigen. Hallo wachtwoord einden wijzigen Hallo mogelijkheid toouse scriptacties of vergroten/verkleinen bewerkingen uitvoeren met uw cluster.

### <a name="hosts"></a>Hosts

Hallo **Hosts** pagina geeft een lijst van alle hosts in Hallo-cluster. toomanage hosts, volg deze stappen.

![hosts pagina](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> Toe te voegen, uit bedrijf nemen en een host recommissioning mag niet worden gebruikt met HDInsight-clusters.

1. Selecteer desgewenst toomanage Hallo-host.

2. Gebruik Hallo **acties** menu tooselect Hallo actie gewenst tooperform:

   * **Start alle onderdelen** -Start alle onderdelen op Hallo-host.

   * **Stopt alle onderdelen** -stopt alle onderdelen op Hallo host.

   * **Alle onderdelen opnieuw** - stoppen en starten van alle onderdelen op Hallo host.

   * **Onderhoudsmodus inschakelen** -onderdrukt waarschuwingen voor Hallo host. Deze modus moet worden ingeschakeld als u bij het uitvoeren van acties die waarschuwingen genereren. Bijvoorbeeld, een service starten en stoppen.

   * **De onderhoudsmodus uitschakelen** -retourneert Hallo host toonormal waarschuwingen.

   * **Stop** -stopt DataNode of NodeManagers op Hallo host.

   * **Start** -DataNode wordt gestart of NodeManagers op Hallo host.

   * **Opnieuw opstarten** -wordt gestopt en gestart DataNode of NodeManagers op Hallo host.

   * **Buiten gebruik stellen** -Hiermee verwijdert u een host uit Hallo-cluster.

     > [!NOTE]
     > Deze actie niet gebruiken op HDInsight-clusters.

   * **Recommission** -voegt een eerder buiten gebruik gestelde toohello hostcluster.

     > [!NOTE]
     > Deze actie niet gebruiken op HDInsight-clusters.

### <a id="service"></a>Services

Van Hallo **Dashboard** of **Services** pagina, gebruikt u Hallo **acties** knop Hallo Hallo lijst met services toostop onderaan in en start alle services.

![serviceacties](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Terwijl **Service toevoegen** wordt vermeld in dit menu mag niet gebruikte tooadd services toohello HDInsight-cluster. Nieuwe services moeten worden toegevoegd met behulp van een scriptactie tijdens de clusterinrichting. Zie voor meer informatie over het gebruik van scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).

Tijdens het Hallo **acties** knop kunt alle services opnieuw starten, vaak wilt u toostart, stoppen of opnieuw opstarten van een specifieke service. Gebruik van de volgende stappen tooperform activiteiten op een afzonderlijke service Hallo:

1. Van Hallo **Dashboard** of **Services** pagina, selecteert u een service.

2. Vanaf de bovenkant Hallo Hallo **samenvatting** tabblad, gebruikt u Hallo **serviceacties** knop en selecteer Hallo actie tootake. Hallo-service op alle knooppunten opnieuw is opgestart.

    ![serviceactie](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Sommige services opnieuw te starten tijdens het Hallo-cluster wordt uitgevoerd, kan waarschuwingen genereren. tooavoid van waarschuwingen, kunt u Hallo **serviceacties** knop tooenable **onderhoudsmodus** voor Hallo service voordat u Hallo opnieuw uitvoert.

3. Wanneer een actie is geselecteerd, Hallo **op #** vermelding bovenaan Hallo Hallo pagina stappen tooshow een achtergrondbewerking optreedt. Als toodisplay is geconfigureerd, wordt Hallo lijst met bewerkingen op de achtergrond weergegeven.

   > [!NOTE]
   > Als u ingeschakeld **onderhoudsmodus** Hallo-service, houd er rekening mee toodisable deze met behulp van Hallo **serviceacties** knop zodra het Hallo-bewerking is voltooid.

een service tooconfigure gebruiken Hallo stappen te volgen:

1. Van Hallo **Dashboard** of **Services** pagina, selecteert u een service.

2. Selecteer Hallo **Configs** tabblad Hallo huidige configuratie wordt weergegeven. Een lijst met vorige configuraties wordt ook weergegeven.

    ![Configuraties](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Hallo velden weergegeven toomodify Hallo configuratie gebruikt en selecteer vervolgens **opslaan**. Of Selecteer een configuratie van de vorige en selecteert u **instellen als huidige** tooroll back toohello vorige instellingen.

## <a name="ambari-views"></a>Ambari-weergaven

Ambari-weergaven kunnen ontwikkelaars tooplug UI-elementen in de Ambari-Webgebruikersinterface Hallo Hallo met [Ambari-weergaven Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). HDInsight biedt de volgende weergaven met Hadoop-clustertypen Hallo:

* Yarn Queue Manager: Hallo wachtrij manager biedt een eenvoudige gebruikersinterface voor het weergeven en wijzigen van YARN-wachtrijen.

* Hive-weergave: Hallo Hive-weergave kunt u toorun Hive-query's rechtstreeks vanuit uw webbrowser. U kunt query's opslaan, resultaten weergeven, het opslaan van resultaten toohello clusteropslag of resultaten tooyour lokaal systeem te downloaden. Zie voor meer informatie over het gebruik van Hive-weergaven [Hive-weergaven gebruiken met HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* Tez weergave: Hallo Tez weergave kunt u toobetter begrijpen en taken te optimaliseren. U kunt informatie weergeven over hoe Tez-taken worden uitgevoerd en welke bronnen worden gebruikt.
