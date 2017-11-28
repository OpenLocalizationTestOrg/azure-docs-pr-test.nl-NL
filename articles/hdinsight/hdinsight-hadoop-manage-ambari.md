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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="6f33e-104">HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6f33e-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="6f33e-105">Apache Ambari vereenvoudigt het Hallo-beheer en bewaking van een Hadoop-cluster met een eenvoudig toouse web UI en REST-API.</span><span class="sxs-lookup"><span data-stu-id="6f33e-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="6f33e-106">Ambari is opgenomen op Linux gebaseerde HDInsight-clusters en gebruikte toomonitor Hallo cluster uit en maak configuratiewijzigingen is.</span><span class="sxs-lookup"><span data-stu-id="6f33e-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="6f33e-107">In dit document leert u hoe toouse Ambari-Webgebruikersinterface Hallo met een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="6f33e-108"><a id="whatis"></a>Wat is Ambari?</span><span class="sxs-lookup"><span data-stu-id="6f33e-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="6f33e-109">[Apache Ambari](http://ambari.apache.org) vereenvoudigt Hadoop-beheer door de webgebruikersinterface van een eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f33e-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="6f33e-110">Kunt u Ambari maken, beheren en bewaken van Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f33e-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="6f33e-111">Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van Hallo [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="6f33e-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="6f33e-112">Hallo Ambari-Webgebruikersinterface standaard met HDInsight-clusters die gebruikmaken van Hallo Linux-besturingssysteem is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f33e-113">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6f33e-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6f33e-114">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6f33e-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="6f33e-115">Connectiviteit</span><span class="sxs-lookup"><span data-stu-id="6f33e-115">Connectivity</span></span>

<span data-ttu-id="6f33e-116">Hallo Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op HTTPS://CLUSTERNAME.azurehdidnsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f33e-117">Verbinding maken met tooAmbari op HDInsight HTTPS is vereist.</span><span class="sxs-lookup"><span data-stu-id="6f33e-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="6f33e-118">Wanneer u om verificatie wordt gevraagd, gebruik Hallo admin-accountnaam en wachtwoord die u hebt opgegeven tijdens het Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f33e-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="6f33e-119">SSH-tunnel (proxy)</span><span class="sxs-lookup"><span data-stu-id="6f33e-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="6f33e-120">Terwijl de Ambari voor uw cluster toegankelijk is rechtstreeks via Internet hello, Hallo enkele koppelingen van Hallo Ambari-Webgebruikersinterface (zoals toohello JobTracker) worden niet weergegeven op internet.</span><span class="sxs-lookup"><span data-stu-id="6f33e-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="6f33e-121">tooaccess deze services, moet u een SSH-tunnel maken.</span><span class="sxs-lookup"><span data-stu-id="6f33e-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="6f33e-122">Zie voor meer informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="6f33e-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="6f33e-123">Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6f33e-123">Ambari Web UI</span></span>

<span data-ttu-id="6f33e-124">Wanneer u verbinding maakt toohello Ambari-Webgebruikersinterface, zijn na vragen aan gebruiker tooauthenticate toohello pagina.</span><span class="sxs-lookup"><span data-stu-id="6f33e-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="6f33e-125">Gebruik Hallo cluster admin-gebruiker (standaard Admin) en het wachtwoord waarmee u tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="6f33e-126">Let op Hallo balk Hallo boven wanneer Hallo pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6f33e-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="6f33e-127">Deze balk bevat Hallo volgende informatie en besturingselementen:</span><span class="sxs-lookup"><span data-stu-id="6f33e-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="6f33e-129">**Ambari-logo** -wordt geopend Hallo dashboard, dat gebruikt toomonitor Hallo-cluster worden kan.</span><span class="sxs-lookup"><span data-stu-id="6f33e-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="6f33e-130">**Naam # ops cluster** -geeft het aantal actieve Ambari bewerkingen Hallo weer.</span><span class="sxs-lookup"><span data-stu-id="6f33e-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="6f33e-131">Naam van de cluster te selecteren Hallo of **# ops** geeft een lijst met bewerkingen op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6f33e-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="6f33e-132">**waarschuwingen voor #** -waarschuwingen of kritieke waarschuwingen weergeven, indien aanwezig, voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="6f33e-133">**Dashboard** -geeft Hallo dashboard.</span><span class="sxs-lookup"><span data-stu-id="6f33e-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="6f33e-134">**Services** -gegevens en configuratie-instellingen voor Hallo-services in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="6f33e-135">**Hosts** -gegevens en configuratie-instellingen voor Hallo knooppunten in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="6f33e-136">**Waarschuwingen** -een logboek van informatie, waarschuwingen en kritieke waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="6f33e-137">**Beheerder** -Software stack/services die zijn geïnstalleerd op het Hallo-cluster, informatie over serviceaccounts en Kerberos-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="6f33e-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="6f33e-138">**Knop Admin** -Ambari beheer, gebruikersinstellingen en meld u af.</span><span class="sxs-lookup"><span data-stu-id="6f33e-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="6f33e-139">Bewaking</span><span class="sxs-lookup"><span data-stu-id="6f33e-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="6f33e-140">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="6f33e-140">Alerts</span></span>

<span data-ttu-id="6f33e-141">Hallo bevat volgende lijst Hallo algemene waarschuwing statussen die worden gebruikt door Ambari:</span><span class="sxs-lookup"><span data-stu-id="6f33e-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="6f33e-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="6f33e-142">**OK**</span></span>
* <span data-ttu-id="6f33e-143">**Waarschuwing**</span><span class="sxs-lookup"><span data-stu-id="6f33e-143">**Warning**</span></span>
* <span data-ttu-id="6f33e-144">**KRITIEKE**</span><span class="sxs-lookup"><span data-stu-id="6f33e-144">**CRITICAL**</span></span>
* <span data-ttu-id="6f33e-145">**ONBEKEND**</span><span class="sxs-lookup"><span data-stu-id="6f33e-145">**UNKNOWN**</span></span>

<span data-ttu-id="6f33e-146">Anders dan waarschuwingen **OK** veroorzaken Hallo **# waarschuwingen** vermelding bovenaan Hallo Hallo pagina toodisplay Hallo aantal waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="6f33e-147">Als u dit item wordt weergegeven, Hallo waarschuwingen en hun status.</span><span class="sxs-lookup"><span data-stu-id="6f33e-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="6f33e-148">Waarschuwingen worden ingedeeld in verschillende standaardgroepen die kunnen worden bekeken in Hallo **waarschuwingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="6f33e-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![pagina waarschuwingen](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="6f33e-150">U kunt groepen Hallo beheren met behulp van Hallo **acties** menu en selecteer **waarschuwing groepen beheren**.</span><span class="sxs-lookup"><span data-stu-id="6f33e-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![dialoogvenster Waarschuwing groepen beheren](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="6f33e-152">U kunt ook waarschuwingen methoden beheren en waarschuwingsmeldingen van Hallo **acties** menu door te selecteren __waarschuwing meldingen beheren__.</span><span class="sxs-lookup"><span data-stu-id="6f33e-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="6f33e-153">Huidige meldingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-153">Any current notifications are displayed.</span></span> <span data-ttu-id="6f33e-154">U kunt ook meldingen van hieruit maken.</span><span class="sxs-lookup"><span data-stu-id="6f33e-154">You can also create notifications from here.</span></span> <span data-ttu-id="6f33e-155">Meldingen kunnen worden verzonden **e** of **SNMP** wanneer specifieke waarschuwing/ernst combinaties optreden.</span><span class="sxs-lookup"><span data-stu-id="6f33e-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="6f33e-156">U kunt bijvoorbeeld een e-mailbericht wanneer een van de waarschuwingen Hallo op Hallo verzenden **YARN standaard** groep te ingesteld**Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="6f33e-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![Waarschuwing dialoogvenster maken](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="6f33e-158">Ten slotte selecteren __Waarschuwingsinstellingen beheren__ van Hallo __acties__ menu kunt u tooset Hallo aantal keren dat een waarschuwing optreden moet voordat een melding wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="6f33e-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="6f33e-159">Deze instelling kan worden gebruikt tooprevent meldingen voor tijdelijke fouten.</span><span class="sxs-lookup"><span data-stu-id="6f33e-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="6f33e-160">Cluster</span><span class="sxs-lookup"><span data-stu-id="6f33e-160">Cluster</span></span>

<span data-ttu-id="6f33e-161">Hallo **metrische gegevens** van Hallo dashboard bevat een reeks widgets om het eenvoudig toomonitor Hallo status van het cluster in één oogopslag.</span><span class="sxs-lookup"><span data-stu-id="6f33e-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="6f33e-162">Verschillende widgets zoals **CPU-gebruik**, vindt u aanvullende informatie wanneer geklikt.</span><span class="sxs-lookup"><span data-stu-id="6f33e-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard met metrische gegevens](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="6f33e-164">Hallo **Heatmaps** tabblad metrische gegevens worden weergegeven als gekleurde heatmaps, van groen toored.</span><span class="sxs-lookup"><span data-stu-id="6f33e-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![dashboard met heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="6f33e-166">Selecteer voor meer informatie over Hallo knooppunten binnen Hallo cluster **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="6f33e-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="6f33e-167">Selecteer de specifieke knooppunt Hallo die u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="6f33e-167">Then select hello specific node you are interested in.</span></span>

![details van de host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="6f33e-169">Services</span><span class="sxs-lookup"><span data-stu-id="6f33e-169">Services</span></span>

<span data-ttu-id="6f33e-170">Hallo **Services** zijbalk op Hallo dashboard biedt snel inzicht in Hallo status van Hallo services die worden uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="6f33e-171">Verschillende pictogrammen zijn gebruikte tooindicate status of acties die moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6f33e-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="6f33e-172">Een gele recyclen symbool wordt bijvoorbeeld weergegeven als een service nodig toobe gerecycled heeft.</span><span class="sxs-lookup"><span data-stu-id="6f33e-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![Services Zijmarge](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="6f33e-174">Hallo-services weergegeven verschillen van HDInsight-clustertypen en versies.</span><span class="sxs-lookup"><span data-stu-id="6f33e-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="6f33e-175">Hallo-services wordt hier weergegeven mogelijk anders dan Hallo services die worden weergegeven voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="6f33e-176">Selecteren van een service, geeft meer gedetailleerde informatie op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6f33e-176">Selecting a service displays more detailed information on hello service.</span></span>

![samenvattende informatie van service](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="6f33e-178">Snelkoppelingen</span><span class="sxs-lookup"><span data-stu-id="6f33e-178">Quick links</span></span>

<span data-ttu-id="6f33e-179">Sommige services weer een **snelkoppelingen** koppeling bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="6f33e-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="6f33e-180">Dit kan gebruikte tooaccess servicespecifieke web UI, zoals zijn:</span><span class="sxs-lookup"><span data-stu-id="6f33e-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="6f33e-181">**Taakgeschiedenis** -geschiedenis van MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="6f33e-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="6f33e-182">**Resource Manager** -gebruikersinterface van YARN ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="6f33e-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="6f33e-183">**NameNode** -Hadoop Distributed File System (HDFS) NameNode gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6f33e-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="6f33e-184">**Oozie-webgebruikersinterface** -Oozie-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6f33e-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="6f33e-185">Wanneer u een van de volgende koppelingen, wordt een nieuw tabblad geopend in uw browser, die Hallo geselecteerde pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="6f33e-186">Selecteren Hallo **snelkoppelingen** vermelding voor een service een fout 'de server is niet gevonden' retourneert.</span><span class="sxs-lookup"><span data-stu-id="6f33e-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="6f33e-187">Als deze fout optreedt, moet u een SSH-tunnel gebruiken wanneer u Hallo **snelkoppelingen** post voor deze service.</span><span class="sxs-lookup"><span data-stu-id="6f33e-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="6f33e-188">Zie voor informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="6f33e-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="6f33e-189">Beheer</span><span class="sxs-lookup"><span data-stu-id="6f33e-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="6f33e-190">Ambari-gebruikers, groepen en machtigingen</span><span class="sxs-lookup"><span data-stu-id="6f33e-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="6f33e-191">Werken met gebruikers, groepen en machtigingen worden ondersteund wanneer een [verbonden met het domein](hdinsight-domain-joined-introduction.md) HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="6f33e-192">Zie voor meer informatie over het gebruik van Hallo Ambari Management gebruikersinterface op een cluster domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f33e-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="6f33e-193">Hallo-wachtwoord van Hallo Ambari watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6f33e-194">Hallo wachtwoord einden wijzigen Hallo mogelijkheid toouse scriptacties of vergroten/verkleinen bewerkingen uitvoeren met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="6f33e-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="6f33e-195">Hosts</span></span>

<span data-ttu-id="6f33e-196">Hallo **Hosts** pagina geeft een lijst van alle hosts in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="6f33e-197">toomanage hosts, volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-197">toomanage hosts, follow these steps.</span></span>

![hosts pagina](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="6f33e-199">Toe te voegen, uit bedrijf nemen en een host recommissioning mag niet worden gebruikt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f33e-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="6f33e-200">Selecteer desgewenst toomanage Hallo-host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="6f33e-201">Gebruik Hallo **acties** menu tooselect Hallo actie gewenst tooperform:</span><span class="sxs-lookup"><span data-stu-id="6f33e-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="6f33e-202">**Start alle onderdelen** -Start alle onderdelen op Hallo-host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="6f33e-203">**Stopt alle onderdelen** -stopt alle onderdelen op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="6f33e-204">**Alle onderdelen opnieuw** - stoppen en starten van alle onderdelen op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="6f33e-205">**Onderhoudsmodus inschakelen** -onderdrukt waarschuwingen voor Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="6f33e-206">Deze modus moet worden ingeschakeld als u bij het uitvoeren van acties die waarschuwingen genereren.</span><span class="sxs-lookup"><span data-stu-id="6f33e-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="6f33e-207">Bijvoorbeeld, een service starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="6f33e-208">**De onderhoudsmodus uitschakelen** -retourneert Hallo host toonormal waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="6f33e-209">**Stop** -stopt DataNode of NodeManagers op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="6f33e-210">**Start** -DataNode wordt gestart of NodeManagers op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="6f33e-211">**Opnieuw opstarten** -wordt gestopt en gestart DataNode of NodeManagers op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6f33e-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="6f33e-212">**Buiten gebruik stellen** -Hiermee verwijdert u een host uit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6f33e-213">Deze actie niet gebruiken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f33e-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="6f33e-214">**Recommission** -voegt een eerder buiten gebruik gestelde toohello hostcluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6f33e-215">Deze actie niet gebruiken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f33e-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="6f33e-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="6f33e-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="6f33e-217">Van Hallo **Dashboard** of **Services** pagina, gebruikt u Hallo **acties** knop Hallo Hallo lijst met services toostop onderaan in en start alle services.</span><span class="sxs-lookup"><span data-stu-id="6f33e-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![serviceacties](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="6f33e-219">Terwijl **Service toevoegen** wordt vermeld in dit menu mag niet gebruikte tooadd services toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f33e-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="6f33e-220">Nieuwe services moeten worden toegevoegd met behulp van een scriptactie tijdens de clusterinrichting.</span><span class="sxs-lookup"><span data-stu-id="6f33e-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="6f33e-221">Zie voor meer informatie over het gebruik van scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6f33e-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="6f33e-222">Tijdens het Hallo **acties** knop kunt alle services opnieuw starten, vaak wilt u toostart, stoppen of opnieuw opstarten van een specifieke service.</span><span class="sxs-lookup"><span data-stu-id="6f33e-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="6f33e-223">Gebruik van de volgende stappen tooperform activiteiten op een afzonderlijke service Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f33e-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="6f33e-224">Van Hallo **Dashboard** of **Services** pagina, selecteert u een service.</span><span class="sxs-lookup"><span data-stu-id="6f33e-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="6f33e-225">Vanaf de bovenkant Hallo Hallo **samenvatting** tabblad, gebruikt u Hallo **serviceacties** knop en selecteer Hallo actie tootake.</span><span class="sxs-lookup"><span data-stu-id="6f33e-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="6f33e-226">Hallo-service op alle knooppunten opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="6f33e-226">This restarts hello service on all nodes.</span></span>

    ![serviceactie](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="6f33e-228">Sommige services opnieuw te starten tijdens het Hallo-cluster wordt uitgevoerd, kan waarschuwingen genereren.</span><span class="sxs-lookup"><span data-stu-id="6f33e-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="6f33e-229">tooavoid van waarschuwingen, kunt u Hallo **serviceacties** knop tooenable **onderhoudsmodus** voor Hallo service voordat u Hallo opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6f33e-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="6f33e-230">Wanneer een actie is geselecteerd, Hallo **op #** vermelding bovenaan Hallo Hallo pagina stappen tooshow een achtergrondbewerking optreedt.</span><span class="sxs-lookup"><span data-stu-id="6f33e-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="6f33e-231">Als toodisplay is geconfigureerd, wordt Hallo lijst met bewerkingen op de achtergrond weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6f33e-232">Als u ingeschakeld **onderhoudsmodus** Hallo-service, houd er rekening mee toodisable deze met behulp van Hallo **serviceacties** knop zodra het Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f33e-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="6f33e-233">een service tooconfigure gebruiken Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6f33e-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="6f33e-234">Van Hallo **Dashboard** of **Services** pagina, selecteert u een service.</span><span class="sxs-lookup"><span data-stu-id="6f33e-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="6f33e-235">Selecteer Hallo **Configs** tabblad Hallo huidige configuratie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="6f33e-236">Een lijst met vorige configuraties wordt ook weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f33e-236">A list of previous configurations is also displayed.</span></span>

    ![Configuraties](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="6f33e-238">Hallo velden weergegeven toomodify Hallo configuratie gebruikt en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f33e-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="6f33e-239">Of Selecteer een configuratie van de vorige en selecteert u **instellen als huidige** tooroll back toohello vorige instellingen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="6f33e-240">Ambari-weergaven</span><span class="sxs-lookup"><span data-stu-id="6f33e-240">Ambari views</span></span>

<span data-ttu-id="6f33e-241">Ambari-weergaven kunnen ontwikkelaars tooplug UI-elementen in de Ambari-Webgebruikersinterface Hallo Hallo met [Ambari-weergaven Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="6f33e-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="6f33e-242">HDInsight biedt de volgende weergaven met Hadoop-clustertypen Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f33e-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="6f33e-243">Yarn Queue Manager: Hallo wachtrij manager biedt een eenvoudige gebruikersinterface voor het weergeven en wijzigen van YARN-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="6f33e-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="6f33e-244">Hive-weergave: Hallo Hive-weergave kunt u toorun Hive-query's rechtstreeks vanuit uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="6f33e-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="6f33e-245">U kunt query's opslaan, resultaten weergeven, het opslaan van resultaten toohello clusteropslag of resultaten tooyour lokaal systeem te downloaden.</span><span class="sxs-lookup"><span data-stu-id="6f33e-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="6f33e-246">Zie voor meer informatie over het gebruik van Hive-weergaven [Hive-weergaven gebruiken met HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="6f33e-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="6f33e-247">Tez weergave: Hallo Tez weergave kunt u toobetter begrijpen en taken te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="6f33e-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="6f33e-248">U kunt informatie weergeven over hoe Tez-taken worden uitgevoerd en welke bronnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6f33e-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
