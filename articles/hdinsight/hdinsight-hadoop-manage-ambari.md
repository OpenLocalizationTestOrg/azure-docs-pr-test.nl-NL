---
title: Bewaken en beheren van Azure HDInsight met behulp van de Ambari-Webgebruikersinterface | Microsoft Docs
description: Informatie over het Ambari gebruiken om te controleren en beheren van Linux gebaseerde HDInsight-clusters. In dit document leert u hoe u de Ambari-Webgebruikersinterface opgenomen met HDInsight-clusters.
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
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="6c693-104">HDInsight-clusters beheren met behulp van de Ambari-Webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6c693-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="6c693-105">Apache Ambari vereenvoudigt het beheer en bewaking van een Hadoop-cluster met een eenvoudige web-UI en REST-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c693-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="6c693-106">Ambari is opgenomen op Linux gebaseerde HDInsight-clusters en wordt gebruikt om te controleren van het cluster en configuratiewijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="6c693-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="6c693-107">In dit document leert u hoe u de Ambari-Webgebruikersinterface met een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="6c693-108"><a id="whatis"></a>Wat is Ambari?</span><span class="sxs-lookup"><span data-stu-id="6c693-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="6c693-109">[Apache Ambari](http://ambari.apache.org) vereenvoudigt Hadoop-beheer door de webgebruikersinterface van een eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c693-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="6c693-110">Kunt u Ambari maken, beheren en bewaken van Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="6c693-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="6c693-111">Ontwikkelaars kunnen deze mogelijkheden integreren in hun toepassingen met behulp van de [Ambari REST-API's](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="6c693-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="6c693-112">De Ambari-Webgebruikersinterface is standaard met HDInsight-clusters die gebruikmaken van de Linux-besturingssysteem opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c693-113">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6c693-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c693-114">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c693-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="6c693-115">Connectiviteit</span><span class="sxs-lookup"><span data-stu-id="6c693-115">Connectivity</span></span>

<span data-ttu-id="6c693-116">De Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op HTTPS://CLUSTERNAME.azurehdidnsight.net, waarbij **CLUSTERNAME** is de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c693-117">Verbinding maken met Ambari op HDInsight HTTPS is vereist.</span><span class="sxs-lookup"><span data-stu-id="6c693-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="6c693-118">Wanneer u om verificatie wordt gevraagd, gebruikt de admin-accountnaam en het wachtwoord die u hebt opgegeven toen het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6c693-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="6c693-119">SSH-tunnel (proxy)</span><span class="sxs-lookup"><span data-stu-id="6c693-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="6c693-120">Terwijl de Ambari voor uw cluster rechtstreeks via Internet toegankelijk is, worden sommige koppelingen van de Ambari-Webgebruikersinterface (zoals het de JobTracker) niet weergegeven op het internet.</span><span class="sxs-lookup"><span data-stu-id="6c693-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="6c693-121">Voor toegang tot deze services, moet u een SSH-tunnel maken.</span><span class="sxs-lookup"><span data-stu-id="6c693-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="6c693-122">Zie voor meer informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="6c693-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="6c693-123">Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6c693-123">Ambari Web UI</span></span>

<span data-ttu-id="6c693-124">Bij het verbinden met de Ambari-Webgebruikersinterface, wordt u gevraagd om de pagina te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="6c693-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="6c693-125">Gebruik de gebruiker met beheerdersrechten cluster (standaard Admin) en het wachtwoord waarmee u tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="6c693-126">Wanneer de pagina wordt geopend, noteert u de balk aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="6c693-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="6c693-127">Deze balk bevat de volgende informatie en besturingselementen:</span><span class="sxs-lookup"><span data-stu-id="6c693-127">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="6c693-129">**Ambari-logo** -Hiermee opent u het dashboard, die kan worden gebruikt voor het bewaken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="6c693-130">**Naam # ops cluster** -geeft het aantal actieve Ambari-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6c693-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="6c693-131">Naam van het cluster te selecteren of **# ops** geeft een lijst met bewerkingen op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6c693-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="6c693-132">**waarschuwingen voor #** -waarschuwingen of kritieke waarschuwingen weergeven, indien aanwezig, voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="6c693-133">**Dashboard** -het dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="6c693-134">**Services** -gegevens en configuratie-instellingen voor de services in het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="6c693-135">**Hosts** -gegevens en configuratie-instellingen voor de knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="6c693-136">**Waarschuwingen** -een logboek van informatie, waarschuwingen en kritieke waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6c693-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="6c693-137">**Beheerder** -Software stack/services die zijn geïnstalleerd op de cluster-serviceaccount en Kerberos-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="6c693-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="6c693-138">**Knop Admin** -Ambari beheer, gebruikersinstellingen en meld u af.</span><span class="sxs-lookup"><span data-stu-id="6c693-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="6c693-139">Bewaking</span><span class="sxs-lookup"><span data-stu-id="6c693-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="6c693-140">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="6c693-140">Alerts</span></span>

<span data-ttu-id="6c693-141">De volgende lijst bevat de algemene waarschuwing statussen die worden gebruikt door Ambari:</span><span class="sxs-lookup"><span data-stu-id="6c693-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="6c693-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="6c693-142">**OK**</span></span>
* <span data-ttu-id="6c693-143">**Waarschuwing**</span><span class="sxs-lookup"><span data-stu-id="6c693-143">**Warning**</span></span>
* <span data-ttu-id="6c693-144">**KRITIEKE**</span><span class="sxs-lookup"><span data-stu-id="6c693-144">**CRITICAL**</span></span>
* <span data-ttu-id="6c693-145">**ONBEKEND**</span><span class="sxs-lookup"><span data-stu-id="6c693-145">**UNKNOWN**</span></span>

<span data-ttu-id="6c693-146">Anders dan waarschuwingen **OK** ertoe leiden dat de **# waarschuwingen** vermelding aan de bovenkant van de pagina om het aantal waarschuwingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6c693-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="6c693-147">Als u dit item wordt weergegeven, de waarschuwingen en hun status.</span><span class="sxs-lookup"><span data-stu-id="6c693-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="6c693-148">Waarschuwingen worden ingedeeld in verschillende standaardgroepen die kunnen worden bekeken in de **waarschuwingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="6c693-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![pagina waarschuwingen](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="6c693-150">U kunt de groepen beheren met behulp van de **acties** menu en selecteer **waarschuwing groepen beheren**.</span><span class="sxs-lookup"><span data-stu-id="6c693-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![dialoogvenster Waarschuwing groepen beheren](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="6c693-152">U kunt ook waarschuwingen methoden beheren en meldingen van waarschuwingen van de **acties** menu door te selecteren __waarschuwing meldingen beheren__.</span><span class="sxs-lookup"><span data-stu-id="6c693-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="6c693-153">Huidige meldingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-153">Any current notifications are displayed.</span></span> <span data-ttu-id="6c693-154">U kunt ook meldingen van hieruit maken.</span><span class="sxs-lookup"><span data-stu-id="6c693-154">You can also create notifications from here.</span></span> <span data-ttu-id="6c693-155">Meldingen kunnen worden verzonden **e** of **SNMP** wanneer specifieke waarschuwing/ernst combinaties optreden.</span><span class="sxs-lookup"><span data-stu-id="6c693-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="6c693-156">U kunt bijvoorbeeld een e-mailbericht wanneer een van de waarschuwingen in verzenden de **YARN standaard** groep is ingesteld op **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="6c693-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![Waarschuwing dialoogvenster maken](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="6c693-158">Ten slotte selecteren __Waarschuwingsinstellingen beheren__ van de __acties__ menu kunt u instellen hoe vaak een waarschuwing optreden moet voordat een melding wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="6c693-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="6c693-159">Deze instelling kan worden gebruikt om te voorkomen dat meldingen voor tijdelijke fouten.</span><span class="sxs-lookup"><span data-stu-id="6c693-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="6c693-160">Cluster</span><span class="sxs-lookup"><span data-stu-id="6c693-160">Cluster</span></span>

<span data-ttu-id="6c693-161">De **metrische gegevens** van het dashboard bevat een reeks widgets om gemakkelijk om de status van het cluster in één oogopslag te controleren.</span><span class="sxs-lookup"><span data-stu-id="6c693-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="6c693-162">Verschillende widgets zoals **CPU-gebruik**, vindt u aanvullende informatie wanneer geklikt.</span><span class="sxs-lookup"><span data-stu-id="6c693-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![dashboard met metrische gegevens](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="6c693-164">De **Heatmaps** tabblad metrische gegevens als gekleurde heatmaps, gaan van groen in rood weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![dashboard met heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="6c693-166">Voor meer informatie over de knooppunten in het cluster, selecteert u **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="6c693-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="6c693-167">Selecteer het specifieke knooppunt dat u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="6c693-167">Then select the specific node you are interested in.</span></span>

![details van de host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="6c693-169">Services</span><span class="sxs-lookup"><span data-stu-id="6c693-169">Services</span></span>

<span data-ttu-id="6c693-170">De **Services** zijbalk op het dashboard biedt snel inzicht in de status van de services die worden uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="6c693-171">Verschillende pictogrammen worden gebruikt om aan te geven, status of acties die moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c693-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="6c693-172">Een gele recyclen symbool wordt bijvoorbeeld weergegeven als een service moet worden gerecycled.</span><span class="sxs-lookup"><span data-stu-id="6c693-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![Services Zijmarge](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="6c693-174">De services die worden weergegeven verschillen van HDInsight-clustertypen en versies.</span><span class="sxs-lookup"><span data-stu-id="6c693-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="6c693-175">De services die worden hier weergegeven mogelijk anders dan de services die worden weergegeven voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="6c693-176">Selecteren van een service geeft meer gedetailleerde informatie weer voor de service.</span><span class="sxs-lookup"><span data-stu-id="6c693-176">Selecting a service displays more detailed information on the service.</span></span>

![samenvattende informatie van service](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="6c693-178">Snelkoppelingen</span><span class="sxs-lookup"><span data-stu-id="6c693-178">Quick links</span></span>

<span data-ttu-id="6c693-179">Sommige services weer een **snelkoppelingen** koppeling aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="6c693-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="6c693-180">Dit kan worden gebruikt om te openen, servicespecifieke web UI, zoals:</span><span class="sxs-lookup"><span data-stu-id="6c693-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="6c693-181">**Taakgeschiedenis** -geschiedenis van MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="6c693-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="6c693-182">**Resource Manager** -gebruikersinterface van YARN ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="6c693-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="6c693-183">**NameNode** -Hadoop Distributed File System (HDFS) NameNode gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6c693-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="6c693-184">**Oozie-webgebruikersinterface** -Oozie-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6c693-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="6c693-185">Wanneer u een van de volgende koppelingen, wordt een nieuw tabblad geopend in uw browser, die de geselecteerde pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="6c693-186">Als u de **snelkoppelingen** vermelding voor een service een fout 'de server is niet gevonden' retourneert.</span><span class="sxs-lookup"><span data-stu-id="6c693-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="6c693-187">Als deze fout optreedt, moet u een SSH-tunnel gebruiken wanneer u de **snelkoppelingen** post voor deze service.</span><span class="sxs-lookup"><span data-stu-id="6c693-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="6c693-188">Zie voor informatie [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="6c693-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="6c693-189">Beheer</span><span class="sxs-lookup"><span data-stu-id="6c693-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="6c693-190">Ambari-gebruikers, groepen en machtigingen</span><span class="sxs-lookup"><span data-stu-id="6c693-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="6c693-191">Werken met gebruikers, groepen en machtigingen worden ondersteund wanneer een [verbonden met het domein](hdinsight-domain-joined-introduction.md) HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="6c693-192">Zie voor meer informatie over het gebruik van de Ambari-Management-gebruikersinterface op een cluster domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c693-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="6c693-193">Wijzig het wachtwoord van de Ambari-watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster niet.</span><span class="sxs-lookup"><span data-stu-id="6c693-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6c693-194">Het wachtwoord wilt wijzigen, verbreekt de mogelijkheid voor het gebruik van scriptacties of vergroten/verkleinen bewerkingen uitvoeren met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="6c693-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="6c693-195">Hosts</span></span>

<span data-ttu-id="6c693-196">De **Hosts** pagina geeft een lijst van alle hosts in het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="6c693-197">Volg deze stappen voor het beheren van hosts.</span><span class="sxs-lookup"><span data-stu-id="6c693-197">To manage hosts, follow these steps.</span></span>

![hosts pagina](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="6c693-199">Toe te voegen, uit bedrijf nemen en een host recommissioning mag niet worden gebruikt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6c693-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="6c693-200">Selecteer de host die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="6c693-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="6c693-201">Gebruik de **acties** om te selecteren van de actie die u wilt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6c693-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="6c693-202">**Start alle onderdelen** -alle onderdelen die zijn gestart op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="6c693-203">**Stopt alle onderdelen** -stopt alle onderdelen op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="6c693-204">**Alle onderdelen opnieuw** - stoppen en starten van alle onderdelen op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="6c693-205">**Onderhoudsmodus inschakelen** -waarschuwingen onderdrukt voor de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="6c693-206">Deze modus moet worden ingeschakeld als u bij het uitvoeren van acties die waarschuwingen genereren.</span><span class="sxs-lookup"><span data-stu-id="6c693-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="6c693-207">Bijvoorbeeld, een service starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="6c693-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="6c693-208">**De onderhoudsmodus uitschakelen** -retourneert de host de normale waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="6c693-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="6c693-209">**Stop** -stopt DataNode of NodeManagers op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="6c693-210">**Start** -DataNode wordt gestart of NodeManagers op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="6c693-211">**Opnieuw opstarten** -wordt gestopt en gestart DataNode of NodeManagers op de host.</span><span class="sxs-lookup"><span data-stu-id="6c693-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="6c693-212">**Buiten gebruik stellen** -Hiermee verwijdert u een host uit het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6c693-213">Deze actie niet gebruiken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6c693-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="6c693-214">**Recommission** -voegt een eerder buiten gebruik gestelde host aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6c693-215">Deze actie niet gebruiken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6c693-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="6c693-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="6c693-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="6c693-217">Van de **Dashboard** of **Services** pagina, gebruikt u de **acties** knop aan de onderkant van de lijst met services stoppen en starten van alle services.</span><span class="sxs-lookup"><span data-stu-id="6c693-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![serviceacties](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="6c693-219">Terwijl **Service toevoegen** wordt vermeld in dit menu deze moet niet worden gebruikt voor nieuwe services toegevoegd aan het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6c693-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="6c693-220">Nieuwe services moeten worden toegevoegd met behulp van een scriptactie tijdens de clusterinrichting.</span><span class="sxs-lookup"><span data-stu-id="6c693-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="6c693-221">Zie voor meer informatie over het gebruik van scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6c693-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="6c693-222">Terwijl de **acties** knop kunt alle services opnieuw starten, vaak u wilt starten, stoppen of opnieuw opstarten van een specifieke service.</span><span class="sxs-lookup"><span data-stu-id="6c693-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="6c693-223">Gebruik de volgende stappen voor het uitvoeren van acties op een afzonderlijke service:</span><span class="sxs-lookup"><span data-stu-id="6c693-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="6c693-224">Van de **Dashboard** of **Services** pagina, selecteert u een service.</span><span class="sxs-lookup"><span data-stu-id="6c693-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="6c693-225">Vanaf de bovenkant van de **samenvatting** tabblad, gebruikt u de **serviceacties** knop en selecteer de actie te ondernemen.</span><span class="sxs-lookup"><span data-stu-id="6c693-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="6c693-226">De service op alle knooppunten opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="6c693-226">This restarts the service on all nodes.</span></span>

    ![serviceactie](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="6c693-228">Sommige services opnieuw te starten, terwijl het cluster wordt uitgevoerd, kan waarschuwingen genereren.</span><span class="sxs-lookup"><span data-stu-id="6c693-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="6c693-229">Om waarschuwingen te voorkomen, kunt u de **serviceacties** knop om in te schakelen **onderhoudsmodus** voor de service voordat u de computer opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6c693-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="6c693-230">Wanneer een actie is geselecteerd, de **op #** vermelding aan de bovenkant van de pagina stapsgewijs verhoogd om weer te geven dat een achtergrondbewerking is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6c693-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="6c693-231">Als geconfigureerd om weer te geven, wordt de lijst met bewerkingen op de achtergrond weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6c693-232">Als u ingeschakeld **onderhoudsmodus** voor de service, moet u dit programma uitschakelen met de **serviceacties** knop nadat de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6c693-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="6c693-233">Gebruik de volgende stappen voor het configureren van een service:</span><span class="sxs-lookup"><span data-stu-id="6c693-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="6c693-234">Van de **Dashboard** of **Services** pagina, selecteert u een service.</span><span class="sxs-lookup"><span data-stu-id="6c693-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="6c693-235">Selecteer de **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6c693-235">Select the **Configs** tab.</span></span> <span data-ttu-id="6c693-236">De huidige configuratie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-236">The current configuration is displayed.</span></span> <span data-ttu-id="6c693-237">Een lijst met vorige configuraties wordt ook weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6c693-237">A list of previous configurations is also displayed.</span></span>

    ![Configuraties](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="6c693-239">Gebruik de velden weergegeven om te wijzigen van de configuratie en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6c693-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="6c693-240">Of Selecteer een configuratie van de vorige en selecteert u **instellen als huidige** kunt terugkeren naar de vorige instellingen.</span><span class="sxs-lookup"><span data-stu-id="6c693-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="6c693-241">Ambari-weergaven</span><span class="sxs-lookup"><span data-stu-id="6c693-241">Ambari views</span></span>

<span data-ttu-id="6c693-242">Ambari-weergaven kunnen ontwikkelaars plug-UI-elementen in de Ambari-Webgebruikersinterface met behulp van de [Ambari-weergaven Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="6c693-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="6c693-243">HDInsight biedt de volgende weergaven met Hadoop-clustertypen:</span><span class="sxs-lookup"><span data-stu-id="6c693-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="6c693-244">Yarn Queue Manager: queue manager biedt een eenvoudige gebruikersinterface voor het weergeven en wijzigen van YARN-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="6c693-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="6c693-245">Hive-weergave: De Hive-weergave kunt u het uitvoeren van Hive-query's rechtstreeks vanuit uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="6c693-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="6c693-246">U kunt query's opslaan, resultaten weergeven, resultaten opslaan in de clusteropslag of resultaten downloaden naar het lokale systeem.</span><span class="sxs-lookup"><span data-stu-id="6c693-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="6c693-247">Zie voor meer informatie over het gebruik van Hive-weergaven [Hive-weergaven gebruiken met HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="6c693-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="6c693-248">Tez weergave: De Tez-weergave kunt u beter te begrijpen en taken te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="6c693-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="6c693-249">U kunt informatie weergeven over hoe Tez-taken worden uitgevoerd en welke bronnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c693-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
