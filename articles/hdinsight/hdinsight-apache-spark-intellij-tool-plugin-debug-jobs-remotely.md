---
title: Toolkit voor IntelliJ - toepassingen voor foutopsporing op afstand op HDInsight Spark aaaAzure | Microsoft Docs
description: Meer informatie over hoe HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ tooremotely foutopsporing toepassingen die worden uitgevoerd op HDInsight Spark-clusters via VPN-verbinding gebruiken.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="b9a41-103">Gebruik Azure Toolkit voor IntelliJ toodebug toepassingen op afstand op HDInsight Spark via VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="b9a41-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="b9a41-104">Het wordt aangeraden de Hallo manier voor foutopsporing spark applicaltion op afstand via ssh.</span><span class="sxs-lookup"><span data-stu-id="b9a41-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="b9a41-105">Zie voor instructies [op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="b9a41-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="b9a41-106">Dit artikel bevat stapsgewijze instructies over hoe toouse hello HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toosubmit een taak Spark in HDInsight Spark-cluster en op afstand debug vanaf uw computer.</span><span class="sxs-lookup"><span data-stu-id="b9a41-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="b9a41-107">toodo geval is, moet u Hallo volgende geavanceerde stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b9a41-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="b9a41-108">Maak een site-naar-site of een punt-naar-site Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="b9a41-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="b9a41-109">Hallo stappen in dit document wordt ervan uitgegaan dat u een site-naar-site-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b9a41-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="b9a41-110">Een Spark-cluster maken in Azure HDInsight die deel uitmaakt van Hallo site-naar-site Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="b9a41-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="b9a41-111">Controleer de Hallo connectiviteit tussen Hallo cluster headnode en uw bureaublad.</span><span class="sxs-lookup"><span data-stu-id="b9a41-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="b9a41-112">Een toepassing Scala in IntelliJ IDEA maken en configureren voor foutopsporing op afstand.</span><span class="sxs-lookup"><span data-stu-id="b9a41-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="b9a41-113">Voer en fouten opsporen in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9a41-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9a41-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9a41-114">Prerequisites</span></span>
* <span data-ttu-id="b9a41-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b9a41-115">An Azure subscription.</span></span> <span data-ttu-id="b9a41-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b9a41-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b9a41-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9a41-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b9a41-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b9a41-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b9a41-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="b9a41-119">Oracle Java Development kit.</span></span> <span data-ttu-id="b9a41-120">Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b9a41-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b9a41-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b9a41-121">IntelliJ IDEA.</span></span> <span data-ttu-id="b9a41-122">In dit artikel gebruikt versie 2017.1.</span><span class="sxs-lookup"><span data-stu-id="b9a41-122">This article uses version 2017.1.</span></span> <span data-ttu-id="b9a41-123">Kunt u het installeren van [hier](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b9a41-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="b9a41-124">HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9a41-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b9a41-125">HDInsight tools voor IntelliJ beschikbaar zijn als onderdeel van hello Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9a41-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b9a41-126">Zie voor instructies over hoe tooinstall Azure Toolkit hello, [installeren hello Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="b9a41-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="b9a41-127">Meld u aan bij uw Azure-abonnement van IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b9a41-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="b9a41-128">Volg de instructies Hallo [hier](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b9a41-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="b9a41-129">Tijdens het uitvoeren van Spark Scala-toepassing voor foutopsporing op afstand op een Windows-computer, krijgt u mogelijk een uitzondering zoals toegelicht in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) dit het geval is vanwege het ontbreken van tooa WinUtils.exe in Windows.</span><span class="sxs-lookup"><span data-stu-id="b9a41-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="b9a41-130">toowork om deze fout, moet u [Hallo uitvoerbare downloaden vanaf hier](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie, zoals **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="b9a41-131">Vervolgens moet u een omgevingsvariabele toevoegen **HADOOP_HOME** en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="b9a41-132">Stap 1: Een Azure-netwerk maken</span><span class="sxs-lookup"><span data-stu-id="b9a41-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="b9a41-133">Hallo instructies volgt in Hallo onderstaande koppelingen toocreate een Azure-netwerk en controleer vervolgens of Hallo connectiviteit tussen Hallo bureaublad en Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="b9a41-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="b9a41-134">Maak een VNet met een site-naar-site VPN-verbinding met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b9a41-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="b9a41-135">Maak een VNet met een site-naar-site VPN-verbinding met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a41-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="b9a41-136">Configureren van een punt-naar-site-verbinding tooa virtueel netwerk met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a41-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="b9a41-137">Stap 2: Een HDInsight Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="b9a41-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="b9a41-138">U moet ook een Apache Spark-cluster maken op Azure HDInsight die deel uitmaakt van hello Azure Virtual Network die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9a41-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="b9a41-139">Gebruik Hallo-informatie beschikbaar op [clusters in HDInsight op basis van Linux maken](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b9a41-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="b9a41-140">Selecteer hello Azure Virtual Network die u in de vorige stap Hallo gemaakt als onderdeel van de optionele configuratie.</span><span class="sxs-lookup"><span data-stu-id="b9a41-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="b9a41-141">Stap 3: Controleren of de Hallo verbinding tussen Hallo cluster headnode en uw bureaublad</span><span class="sxs-lookup"><span data-stu-id="b9a41-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="b9a41-142">Hallo IP-adres van Hallo headnode ophalen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="b9a41-143">Open Ambari UI voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9a41-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="b9a41-144">Cluster-blade hello, klikt u op **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="b9a41-146">Hallo Ambari UI van rechterbovenhoek hello, klik op **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="b9a41-148">U ziet een lijst met headnodes worker-knooppunten en zookeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b9a41-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="b9a41-149">Hallo headnodes hebben Hallo **hn*** voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="b9a41-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="b9a41-150">Klik op de eerste headnode Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9a41-150">Click hello first headnode.</span></span>

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="b9a41-152">Hallo Hallo pagina die wordt geopend, van Hallo onderaan in **samenvatting** vak kopie Hallo IP-adres van Hallo headnode en Hallo-hostnaam.</span><span class="sxs-lookup"><span data-stu-id="b9a41-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="b9a41-154">Hallo IP-adres en hostnaam Hallo van Hallo headnode toohello **hosts** bestand op de computer Hallo van waar toorun en foutopsporing op afstand Hallo Spark taken.</span><span class="sxs-lookup"><span data-stu-id="b9a41-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="b9a41-155">Hierdoor kunt u toocommunicate met Hallo headnode met Hallo IP-adres zoals Hallo hostnaam.</span><span class="sxs-lookup"><span data-stu-id="b9a41-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="b9a41-156">Open een Kladblok met verhoogde machtigingen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="b9a41-157">Hallo bestandsmenu en klik op **Open** en navigeer vervolgens toohello locatie van Hallo hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="b9a41-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="b9a41-158">Op een Windows-computer is `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="b9a41-159">Hallo na toohello toevoegen **hosts** bestand.</span><span class="sxs-lookup"><span data-stu-id="b9a41-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="b9a41-160">Controleer of dat u beide Hallo headnodes met Hallo IP-adres zoals Hallo hostnaam kunt pingen vanaf de computer Hallo waarmee u verbonden toohello virtuele Azure-netwerk dat wordt gebruikt door Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9a41-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="b9a41-161">SSH in Hallo cluster headnode Hallo-instructies op [Connect tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b9a41-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="b9a41-162">Ping Hallo IP-adres van de desktopcomputer Hallo van Hallo cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="b9a41-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="b9a41-163">U moet verbinding tooboth Hallo IP-adressen toegewezen toohello computer, één voor de netwerkverbinding Hallo testen en Hallo andere voor hello Azure Virtual Network die Hallo van computer is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="b9a41-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="b9a41-164">Herhaal stappen Hallo voor Hallo ook andere headnode.</span><span class="sxs-lookup"><span data-stu-id="b9a41-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="b9a41-165">Stap 4: Een Spark Scala-toepassing hello HDInsight Tools met in Azure Toolkit voor IntelliJ maken en configureren voor foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="b9a41-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="b9a41-166">IntelliJ IDEA Start en een nieuw project maken.</span><span class="sxs-lookup"><span data-stu-id="b9a41-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b9a41-167">Controleer in Hallo het dialoogvenster new project, Hallo volgende keuzes en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Spark Scala-toepassing maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="b9a41-169">Selecteer in het linkerdeelvenster Hallo **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="b9a41-170">Selecteer in het rechterdeelvenster Hallo **Spark in HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="b9a41-171">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-171">Click **Next**.</span></span>
2. <span data-ttu-id="b9a41-172">Geef in het volgende venster Hallo Hallo volgende projectdetails, en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="b9a41-173">Geef een naam van het project en de projectlocatie.</span><span class="sxs-lookup"><span data-stu-id="b9a41-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="b9a41-174">Voor **Project SDK**, Java 1.8 voor spark-cluster 2.x, Java 1.7 voor spark 1.x-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9a41-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="b9a41-175">Voor **Spark versie**, Scala-wizard voor het maken van project integreert de juiste versie voor Spark SDK en Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="b9a41-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="b9a41-176">Als Hallo spark-cluster versie 2.0 lager is, kiest u 1.x spark.</span><span class="sxs-lookup"><span data-stu-id="b9a41-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="b9a41-177">Selecteer anders spark2.x.</span><span class="sxs-lookup"><span data-stu-id="b9a41-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="b9a41-178">In dit voorbeeld wordt Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="b9a41-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="b9a41-179">![Spark Scala-toepassing maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="b9a41-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="b9a41-180">Hallo Spark project wordt automatisch een artefact voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9a41-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="b9a41-181">toosee hello artefacten, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="b9a41-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="b9a41-182">Van Hallo **bestand** menu, klikt u op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="b9a41-183">In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** toosee Hallo standaard artefacten die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9a41-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="b9a41-184">![JAR maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="b9a41-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="b9a41-185">U kunt ook uw eigen artefacten maken te klikken op Hallo bly  **+**  pictogram, gemarkeerd in Hallo afbeelding hierboven.</span><span class="sxs-lookup"><span data-stu-id="b9a41-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="b9a41-186">Bibliotheken tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-186">Add libraries tooyour project.</span></span> <span data-ttu-id="b9a41-187">tooadd een bibliotheek met de rechtermuisknop op de projectnaam Hallo in de structuur van de Hallo-project en klik vervolgens op **Open Module-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="b9a41-188">In Hallo **projectstructuur** in het dialoogvenster in het linkerdeelvenster hello, klikt u op **bibliotheken**hello (+)-symbool op en klik vervolgens op **van Maven**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Bibliotheek toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="b9a41-190">In Hallo **bibliotheek downloaden uit de opslagplaats Maven** dialoogvenster, zoeken en toe te voegen Hallo bibliotheken te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="b9a41-191">Kopiëren `yarn-site.xml` en `core-site.xml` van Hallo headnode cluster en voeg deze toohello project.</span><span class="sxs-lookup"><span data-stu-id="b9a41-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="b9a41-192">Hallo volgende opdrachten toocopy Hallo bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9a41-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="b9a41-193">U kunt [Cygwin](https://cygwin.com/install.html) toorun Hallo volgende `scp` toocopy Hallo-bestanden van Hallo cluster headnodes-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="b9a41-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="b9a41-194">Omdat we Hallo cluster headnode IP-adres en de hostnamen voor Hallo hosts-bestand op Hallo bureaublad al hebt toegevoegd, kunnen we hello gebruiken **scp** opdrachten in Hallo manier te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="b9a41-195">Deze bestanden tooyour-project toevoegen door deze te kopiëren onder Hallo **/src** map in de projectstructuur van uw, bijvoorbeeld `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="b9a41-196">Update Hallo `core-site.xml` toomake Hallo wijzigingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="b9a41-197">`core-site.xml`Hallo versleuteld sleutel toohello storage-account gekoppeld Hallo cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="b9a41-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="b9a41-198">In Hallo `core-site.xml` dat u toohello project vervangen Hallo versleutelde sleutel met de werkelijke opslagsleutel Hallo die zijn gekoppeld aan het standaardopslagaccount Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b9a41-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="b9a41-199">Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b9a41-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="b9a41-200">Verwijderen van de volgende vermeldingen uit Hallo Hallo `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="b9a41-201">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="b9a41-201">Save hello file.</span></span>
7. <span data-ttu-id="b9a41-202">Hallo Main-klasse voor uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-202">Add hello Main class for your application.</span></span> <span data-ttu-id="b9a41-203">Van Hallo **Projectverkenner**, met de rechtermuisknop op **src**, wijst u te**nieuw**, en klik vervolgens op **Scala klasse**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Broncode toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="b9a41-205">In Hallo **nieuwe Scala klasse maken** dialoogvenster Geef een naam voor **soort** Selecteer **Object**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Broncode toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="b9a41-207">In Hallo `MyClusterAppMain.scala` bestand, plak Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="b9a41-208">Deze code maakt Hallo Spark context en start een `executeJob` methode van Hallo `SparkSample` object.</span><span class="sxs-lookup"><span data-stu-id="b9a41-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="b9a41-209">Herhaal stap 8 en 9 boven een nieuw Scala-object aangeroepen tooadd `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="b9a41-210">toothis klasse toevoegen Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-210">toothis class add hello following code.</span></span> <span data-ttu-id="b9a41-211">Deze code Hallo gegevens leest uit Hallo HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zevende kolom in Hallo CSV en schrijft Hallo uitvoer te**/HVACOut** onder Hallo-standaard Storage-container voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b9a41-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="b9a41-212">Herhaal stap 8 en 9 hierboven tooadd aangeroepen voor een nieuwe klasse `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="b9a41-213">Deze klasse implementeert Hallo Spark testframework die wordt gebruikt voor het opsporen van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9a41-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="b9a41-214">Hallo na code toohello toevoegen `RemoteClusterDebugging` klasse.</span><span class="sxs-lookup"><span data-stu-id="b9a41-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="b9a41-215">Het paar belangrijke zaken toonote hier:</span><span class="sxs-lookup"><span data-stu-id="b9a41-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="b9a41-216">Voor `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, zorg ervoor dat Hallo Spark assembly JAR is beschikbaar op de clusteropslag Hallo op Hallo opgegeven pad.</span><span class="sxs-lookup"><span data-stu-id="b9a41-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="b9a41-217">Voor `setJars`, geef Hallo-locatie waar Hallo artefact jar wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9a41-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="b9a41-218">Dit is meestal `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="b9a41-219">In Hallo `RemoteClusterDebugging` klasse, met de rechtermuisknop op Hallo `test` sleutelwoord en selecteer **RemoteClusterDebugging configuratie maken**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="b9a41-221">In het dialoogvenster hello, Geef een naam op voor de configuratie van Hallo en selecteer Hallo **testen soort** als **testnaam**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="b9a41-222">Laat alle andere waarden als standaard, klikt u op **toepassen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="b9a41-224">U ziet nu een **extern uitvoeren** configuratie vervolgkeuzelijst in de menubalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9a41-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="b9a41-226">Stap 5: Hallo toepassing uitvoeren in de foutopsporingsmodus</span><span class="sxs-lookup"><span data-stu-id="b9a41-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="b9a41-227">Open in uw project IntelliJ IDEA `SparkSample.scala` en maak een onderbrekingspunt volgende too'val rdd1'.</span><span class="sxs-lookup"><span data-stu-id="b9a41-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="b9a41-228">Selecteer in het pop-upmenu voor het maken van een onderbrekingspunt Hallo **regel in de functie executeJob**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Een onderbrekingspunt toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="b9a41-230">Klik op Hallo **foutopsporing uitvoeren** knop volgende toohello **extern uitvoeren** configuratie vervolgkeuzelijst toostart Hallo toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b9a41-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="b9a41-232">Wanneer de programma-uitvoering Hallo Hallo onderbrekingspunt bereikt, ziet u een **foutopsporingsprogramma** tabblad in Hallo onderste deelvenster.</span><span class="sxs-lookup"><span data-stu-id="b9a41-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="b9a41-234">Klik op Hallo (**+**) pictogram tooadd een controle zoals weergegeven in onderstaande Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="b9a41-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="b9a41-236">Omdat de toepassing hello heeft overschreden voordat Hallo variabele hier `rdd1` is gemaakt met behulp van deze controle we zien wat zijn de eerste 5 rijen in de variabele Hallo Hallo `rdd`.</span><span class="sxs-lookup"><span data-stu-id="b9a41-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="b9a41-237">Druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b9a41-237">Press **ENTER**.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="b9a41-239">Wat u ziet in Hallo afbeelding hierboven is dat terrabytes van gegevens en foutopsporing tijdens runtime kan opvragen hoe de voortgang van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9a41-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="b9a41-240">Bijvoorbeeld in Hallo uitvoer wordt weergegeven in Hallo afbeelding hierboven, ziet u dat Hallo eerste rij van Hallo uitvoer is een koptekst.</span><span class="sxs-lookup"><span data-stu-id="b9a41-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="b9a41-241">Op basis hiervan kunt u uw toepassing code tooskip Hallo veldnamenrij wijzigen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b9a41-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="b9a41-242">U kunt nu klikken op Hallo **hervatten programma** pictogram tooproceed met uw toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9a41-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="b9a41-244">Als de toepassing hello voltooid is, ziet u uitvoer Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="b9a41-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="b9a41-246"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="b9a41-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b9a41-247">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9a41-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="b9a41-248">Demo</span><span class="sxs-lookup"><span data-stu-id="b9a41-248">Demo</span></span>
* <span data-ttu-id="b9a41-249">Scala-Project (Video) te maken: [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b9a41-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="b9a41-250">Foutopsporing op afstand (Video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight-Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b9a41-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="b9a41-251">Scenario's</span><span class="sxs-lookup"><span data-stu-id="b9a41-251">Scenarios</span></span>
* [<span data-ttu-id="b9a41-252">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="b9a41-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b9a41-253">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="b9a41-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b9a41-254">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9a41-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b9a41-255">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="b9a41-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b9a41-256">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9a41-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b9a41-257">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b9a41-257">Create and run applications</span></span>
* [<span data-ttu-id="b9a41-258">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="b9a41-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b9a41-259">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="b9a41-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b9a41-260">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="b9a41-260">Tools and extensions</span></span>
* [<span data-ttu-id="b9a41-261">HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor IntelliJ toocreate en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b9a41-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b9a41-262">Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH</span><span class="sxs-lookup"><span data-stu-id="b9a41-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="b9a41-263">Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="b9a41-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="b9a41-264">HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b9a41-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="b9a41-265">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9a41-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b9a41-266">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9a41-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b9a41-267">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="b9a41-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b9a41-268">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="b9a41-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b9a41-269">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="b9a41-269">Manage resources</span></span>
* [<span data-ttu-id="b9a41-270">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9a41-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b9a41-271">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="b9a41-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
