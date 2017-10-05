---
title: Gebruik van Apache Phoenix en SQuirreL met Azure HDInsight op basis van Windows | Microsoft Docs
description: Informatie over het gebruik van Apache Phoenix in HDInsight en het installeren en configureren van SQuirreL op uw werkstation verbinding maken met een HBase-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="19dd1-103">Apache Phoenix en SQuirreL gebruiken met HBase op basis van Windows-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="19dd1-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="19dd1-104">Informatie over het gebruik [Apache Phoenix](http://phoenix.apache.org/) in HDInsight en het installeren en configureren van SQuirreL op uw werkstation verbinding maken met een HBase-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19dd1-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="19dd1-105">Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="19dd1-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="19dd1-106">Zie voor de grammatica Phoenix [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="19dd1-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="19dd1-107">Zie voor de versie-informatie voor Phoenix in HDInsight, [wat is er nieuw in de Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="19dd1-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="19dd1-108">De stappen in dit document werkt alleen voor Windows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="19dd1-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="19dd1-109">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="19dd1-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="19dd1-110">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="19dd1-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19dd1-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19dd1-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="19dd1-112">Zie voor meer informatie over het gebruik van Phoenix op Linux gebaseerde HDInsight [gebruik Apache Phoenix met HBase op basis van Linux-clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="19dd1-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="19dd1-113">Gebruik SQLLine</span><span class="sxs-lookup"><span data-stu-id="19dd1-113">Use SQLLine</span></span>
<span data-ttu-id="19dd1-114">[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregelprogramma SQL uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="19dd1-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="19dd1-115">Prerequisites</span></span>
<span data-ttu-id="19dd1-116">Voordat u SQLLine gebruiken kunt, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="19dd1-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="19dd1-117">**Een HBase-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="19dd1-118">Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="19dd1-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="19dd1-119">**Verbinding maken met de HBase-cluster via remote desktop protocol**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="19dd1-120">Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van de klassieke Azure Portal][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="19dd1-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="19dd1-121">**Om erachter te komen de hostnaam**</span><span class="sxs-lookup"><span data-stu-id="19dd1-121">**To find out the host name**</span></span>

1. <span data-ttu-id="19dd1-122">Open **Hadoop-opdrachtregel** vanaf het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="19dd1-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="19dd1-123">Voer de volgende opdracht om op te halen van het DNS-achtervoegsel:</span><span class="sxs-lookup"><span data-stu-id="19dd1-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="19dd1-124">Noteer **verbindingsspecifieke DNS-achtervoegsel**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="19dd1-125">Bijvoorbeeld: *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="19dd1-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="19dd1-126">Wanneer u verbinding met een HBase-cluster maakt, moet u verbinding maken met een van de Zookeepers met FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="19dd1-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="19dd1-127">Elke HDInsight-cluster heeft 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="19dd1-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="19dd1-128">Ze zijn *zookeeper0*, *zookeeper1*, en *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="19dd1-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="19dd1-129">De FQDN-naam is ongeveer *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="19dd1-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="19dd1-130">**SQLLine gebruiken**</span><span class="sxs-lookup"><span data-stu-id="19dd1-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="19dd1-131">Open **Hadoop-opdrachtregel** vanaf het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="19dd1-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="19dd1-132">Voer de volgende opdrachten SQLLine openen:</span><span class="sxs-lookup"><span data-stu-id="19dd1-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![Phoenix sqlline van HDInsight hbase][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="19dd1-134">De opdrachten in de steekproef:</span><span class="sxs-lookup"><span data-stu-id="19dd1-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="19dd1-135">Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="19dd1-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="19dd1-136">SQuirreL gebruiken</span><span class="sxs-lookup"><span data-stu-id="19dd1-136">Use SQuirreL</span></span>
<span data-ttu-id="19dd1-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is een grafische Java-programma waarmee u kunt de structuur van een JDBC compatibele database weergeven, de gegevens in tabellen bladeren, voert u SQL-opdrachten enzovoort. Het kan worden gebruikt om met Apache Phoenix op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19dd1-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="19dd1-138">Deze sectie leest u hoe installeren en configureren van SQuirreL op uw werkstation verbinding maken met een HBase-cluster in HDInsight via VPN.</span><span class="sxs-lookup"><span data-stu-id="19dd1-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="19dd1-139">Vereisten</span><span class="sxs-lookup"><span data-stu-id="19dd1-139">Prerequisites</span></span>
<span data-ttu-id="19dd1-140">Voordat u de procedures uitvoert, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="19dd1-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="19dd1-141">Een HBase-cluster is geïmplementeerd op een virtuele Azure-netwerk met een DNS-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="19dd1-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="19dd1-142">Zie voor instructies [maken HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="19dd1-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="19dd1-143">Haal het HBase-cluster cluster verbindingsspecifiek DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="19dd1-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="19dd1-144">Om toegang te krijgen, RDP in het cluster, en voer vervolgens IPConfig.</span><span class="sxs-lookup"><span data-stu-id="19dd1-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="19dd1-145">Het DNS-achtervoegsel is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="19dd1-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="19dd1-146">Download en installeer [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="19dd1-147">U moet makecert van het pakket om het certificaat te maken.</span><span class="sxs-lookup"><span data-stu-id="19dd1-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="19dd1-148">Download en installeer [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="19dd1-149">SQuirreL SQL clientversie 3.0 en hoger vereist JRE 1.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="19dd1-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="19dd1-150">Een punt-naar-Site VPN-verbinding met het Azure-netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="19dd1-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="19dd1-151">Er zijn 3 stappen voor het configureren van een punt-naar-site VPN-verbinding:</span><span class="sxs-lookup"><span data-stu-id="19dd1-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="19dd1-152">Een virtueel netwerk en een gateway voor dynamische routering configureren</span><span class="sxs-lookup"><span data-stu-id="19dd1-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="19dd1-153">Uw certificaten maken</span><span class="sxs-lookup"><span data-stu-id="19dd1-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="19dd1-154">Uw VPN-client configureren</span><span class="sxs-lookup"><span data-stu-id="19dd1-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="19dd1-155">Zie [punt-naar-Site VPN-verbinding geconfigureerd met een Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19dd1-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="19dd1-156">Een virtueel netwerk en een gateway voor dynamische routering configureren</span><span class="sxs-lookup"><span data-stu-id="19dd1-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="19dd1-157">U hebt een HBase-cluster in virtueel netwerk van Azure ingericht zorgen (Zie de vereisten voor deze sectie).</span><span class="sxs-lookup"><span data-stu-id="19dd1-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="19dd1-158">De volgende stap is het configureren van een punt-naar-site-verbinding.</span><span class="sxs-lookup"><span data-stu-id="19dd1-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="19dd1-159">**Voor het configureren van de punt-naar-site-connectiviteit**</span><span class="sxs-lookup"><span data-stu-id="19dd1-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="19dd1-160">Aanmelden bij de [klassieke Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="19dd1-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="19dd1-161">Klik aan de linkerkant op **netwerken**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="19dd1-162">Klik op het virtuele netwerk dat u hebt gemaakt (Zie [inrichten HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="19dd1-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="19dd1-163">Klik op **configureren** vanaf de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="19dd1-164">In de **punt-naar-site-connectiviteit** sectie **punt-naar-site-connectiviteit configureren**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="19dd1-165">Configureer **IP-BEGINADRES** en **CIDR** om op te geven van het IP-adresbereik waarvan uw VPN-clients een IP-adres wanneer verbinding wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="19dd1-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="19dd1-166">Het bereik kan niet overlappen met een van de bereiken die zich op uw on-premises netwerk en het Azure-netwerk dat u verbinding met.</span><span class="sxs-lookup"><span data-stu-id="19dd1-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="19dd1-167">Bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="19dd1-167">For example.</span></span> <span data-ttu-id="19dd1-168">Als u 10.0.0.0/20 voor het virtuele netwerk hebt geselecteerd, kunt u 10.1.0.0/24 voor de adresruimte van de client.</span><span class="sxs-lookup"><span data-stu-id="19dd1-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="19dd1-169">Zie de [punt-naar-Site-connectiviteit] [ vnet-point-to-site-connectivity] pagina voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19dd1-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="19dd1-170">Klik in de sectie virtueel netwerk adres spaties **gatewaysubnet toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="19dd1-171">Klik op **opslaan** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="19dd1-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="19dd1-172">Klik op **Ja** de wijziging te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="19dd1-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="19dd1-173">Wacht totdat de wijziging aan te brengen voordat u met de volgende procedure doorgaat van het systeem is voltooid.</span><span class="sxs-lookup"><span data-stu-id="19dd1-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="19dd1-174">**Een gateway voor dynamische routering maken**</span><span class="sxs-lookup"><span data-stu-id="19dd1-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="19dd1-175">Klik in de klassieke Azure-Portal op **DASHBOARD** vanaf de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="19dd1-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="19dd1-176">Klik op **GATEWAY maken** van de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="19dd1-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="19dd1-177">Klik op **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="19dd1-177">Click **YES** to confirm.</span></span> <span data-ttu-id="19dd1-178">Wacht totdat de gateway is aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="19dd1-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="19dd1-179">Klik op **DASHBOARD** vanaf de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="19dd1-180">Hier ziet u een diagram van het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="19dd1-180">You will see a visual diagram of the virtual network:</span></span>

    ![Virtuele Azure-netwerk punt-naar-site-diagram][img-vnet-diagram]

    <span data-ttu-id="19dd1-182">Het diagram toont 0 clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="19dd1-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="19dd1-183">Nadat u een verbinding met het virtuele netwerk, wordt het aantal bijgewerkt naar een.</span><span class="sxs-lookup"><span data-stu-id="19dd1-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="19dd1-184">Uw certificaten maken</span><span class="sxs-lookup"><span data-stu-id="19dd1-184">Create your certificates</span></span>
<span data-ttu-id="19dd1-185">Een manier voor het maken van een X.509-certificaat is door het hulpprogramma voor het certificaat maken (makecert.exe) die wordt geleverd met [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="19dd1-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="19dd1-186">**Maken van een zelfondertekend basiscertificaat**</span><span class="sxs-lookup"><span data-stu-id="19dd1-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="19dd1-187">Open een opdrachtpromptvenster vanuit uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="19dd1-188">Navigeer naar de map Visual Studio-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="19dd1-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="19dd1-189">De volgende opdracht in het volgende voorbeeld maakt en installeer een basiscertificaat in het persoonlijke certificaatarchief op uw werkstation en ook maken een cer-bestand dat u later naar de klassieke Azure-Portal gaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="19dd1-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="19dd1-190">Ga naar de map die u wilt dat het cer-bestand zich bevinden in, waarbij HBaseVnetVPNRootCertificate is de naam die u wilt gebruiken voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="19dd1-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="19dd1-191">Sluit de opdrachtprompt niet.</span><span class="sxs-lookup"><span data-stu-id="19dd1-191">Don't close the command prompt.</span></span>  <span data-ttu-id="19dd1-192">U moet deze in de volgende procedure.</span><span class="sxs-lookup"><span data-stu-id="19dd1-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19dd1-193">Omdat u een basiscertificaat hebt gemaakt op basis waarvan clientcertificaten worden gegenereerd, wilt u dit certificaat misschien samen met de persoonlijke sleutel exporteren en opslaan op een veilige locatie vanaf waar deze kunnen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="19dd1-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="19dd1-194">**Een certificaat maken**</span><span class="sxs-lookup"><span data-stu-id="19dd1-194">**To create a client certificate**</span></span>

* <span data-ttu-id="19dd1-195">Vanaf de dezelfde opdrachtprompt (er moet op dezelfde computer waarop u het basiscertificaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19dd1-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="19dd1-196">Het clientcertificaat moet worden gegenereerd vanuit het basiscertificaat), voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="19dd1-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="19dd1-197">HBaseVnetVPNRootCertificate is de naam van het root-certificaat.</span><span class="sxs-lookup"><span data-stu-id="19dd1-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="19dd1-198">Deze moet overeenkomen met de naam van het root-certificaat.</span><span class="sxs-lookup"><span data-stu-id="19dd1-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="19dd1-199">Zowel het basiscertificaat als het clientcertificaat worden opgeslagen in uw persoonlijke certificaatarchief op uw computer.</span><span class="sxs-lookup"><span data-stu-id="19dd1-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="19dd1-200">Gebruik certmgr.msc om te controleren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-200">Use certmgr.msc to verify.</span></span>

    ![Virtuele Azure-netwerk punt-naar-site VPN-certificaat][img-certificate]

    <span data-ttu-id="19dd1-202">U moet een clientcertificaat installeren op elke computer die u met het virtueel netwerk wilt verbinden.</span><span class="sxs-lookup"><span data-stu-id="19dd1-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="19dd1-203">U wordt geadviseerd om unieke clientcertificaten te maken voor elke computer die u wilt verbinden met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="19dd1-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="19dd1-204">Gebruik voor het exporteren van de clientcertificaten certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="19dd1-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="19dd1-205">**Het basiscertificaat uploaden naar de klassieke Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="19dd1-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="19dd1-206">Klik in de klassieke Azure-Portal op **netwerk** aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="19dd1-207">Klik op het virtuele netwerk waar uw HBase-cluster wordt geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="19dd1-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="19dd1-208">Klik op **certificaten** vanaf de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="19dd1-209">Klik op **uploaden** van de onderkant en u hebt gemaakt in de procedure vóór laatste bestand voor het basiscertificaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="19dd1-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="19dd1-210">Wacht totdat het certificaat hebt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="19dd1-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="19dd1-211">Klik op **DASHBOARD** bovenaan.</span><span class="sxs-lookup"><span data-stu-id="19dd1-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="19dd1-212">Het virtuele diagram toont de status.</span><span class="sxs-lookup"><span data-stu-id="19dd1-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="19dd1-213">Uw VPN-client configureren</span><span class="sxs-lookup"><span data-stu-id="19dd1-213">Configure your VPN client</span></span>
<span data-ttu-id="19dd1-214">**Downloaden en installeren van het VPN-clientpakket**</span><span class="sxs-lookup"><span data-stu-id="19dd1-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="19dd1-215">Klik op de pagina DASHBOARD van het virtuele netwerk, in de sectie snelle weergave **de 64-bits VPN-clientpakket downloaden** of **de 32-bits VPN-clientpakket downloaden** op basis van uw werkstation OS Versie.</span><span class="sxs-lookup"><span data-stu-id="19dd1-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="19dd1-216">Klik op **uitvoeren** om het pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="19dd1-217">Klik bij de beveiligingsprompt **meer info**, en klik vervolgens op **toch uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="19dd1-218">Klik op **Ja** twee keer.</span><span class="sxs-lookup"><span data-stu-id="19dd1-218">Click **Yes** twice.</span></span>

<span data-ttu-id="19dd1-219">**Verbinding maken met VPN**</span><span class="sxs-lookup"><span data-stu-id="19dd1-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="19dd1-220">Klik op het pictogram netwerken op de taakbalk op het bureaublad van uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="19dd1-221">U ziet een VPN-verbinding met de naam van uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="19dd1-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="19dd1-222">Klik op de naam van de VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="19dd1-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="19dd1-223">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-223">Click **Connect**.</span></span>

<span data-ttu-id="19dd1-224">**De VPN-verbinding en het domein naamomzetting te testen**</span><span class="sxs-lookup"><span data-stu-id="19dd1-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="19dd1-225">Open een opdrachtprompt vanuit het werkstation en ping een van de volgende namen opgegeven van de HBase-cluster DNS-achtervoegsel is myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="19dd1-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="19dd1-226">Installeren en configureren van SQuirreL op uw werkstation</span><span class="sxs-lookup"><span data-stu-id="19dd1-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="19dd1-227">**SQuirreL installeren**</span><span class="sxs-lookup"><span data-stu-id="19dd1-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="19dd1-228">Download het SQuirreL SQL client jar-bestand van [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="19dd1-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="19dd1-229">Het jar-bestand openen/uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-229">Open/run the jar file.</span></span> <span data-ttu-id="19dd1-230">Vereist de [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="19dd1-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="19dd1-231">Klik op **volgende** twee keer.</span><span class="sxs-lookup"><span data-stu-id="19dd1-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="19dd1-232">Geef een pad op waar u de machtiging schrijven, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="19dd1-233">De standaardinstallatiemap is in de map C:\Program Files\squirrel-sql-3.6.</span><span class="sxs-lookup"><span data-stu-id="19dd1-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="19dd1-234">Om te schrijven naar dit pad, moet het installatieprogramma de administrator-bevoegdheden worden verleend.</span><span class="sxs-lookup"><span data-stu-id="19dd1-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="19dd1-235">U kunt open een opdrachtprompt als beheerder, gaat u naar de map bin van Java en voer vervolgens:</span><span class="sxs-lookup"><span data-stu-id="19dd1-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="19dd1-236">Java.exe-jar [het pad naar het jar-bestand SQuirreL]</span><span class="sxs-lookup"><span data-stu-id="19dd1-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="19dd1-237">Klik op **OK** om te bevestigen dat het maken van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="19dd1-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="19dd1-238">De standaardinstelling is de basis en standaard pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="19dd1-239">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-239">Click **Next**.</span></span>
7. <span data-ttu-id="19dd1-240">Klik op **volgende** tweemaal, en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="19dd1-241">**Het stuurprogramma Phoenix installeren**</span><span class="sxs-lookup"><span data-stu-id="19dd1-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="19dd1-242">Het phoenix stuurprogramma jar-bestand bevindt zich op de HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="19dd1-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="19dd1-243">Het pad is vergelijkbaar met het volgende op basis van de versies:</span><span class="sxs-lookup"><span data-stu-id="19dd1-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="19dd1-244">U moet dit te kopiëren naar uw werkstation onder de [SQuirreL-installatiemap] / lib pad.</span><span class="sxs-lookup"><span data-stu-id="19dd1-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="19dd1-245">De eenvoudigste manier is het RDP in het cluster, en gebruik vervolgens bestand kopiëren en plakken (CTRL + C en CTRL + V) om deze te kopiëren naar uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="19dd1-246">**Een Phoenix stuurprogramma wilt toevoegen aan SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="19dd1-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="19dd1-247">Open SQuirreL SQL-Client op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="19dd1-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="19dd1-248">Klik op de **stuurprogramma** tabblad aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="19dd1-249">Van de **stuurprogramma's** menu, klikt u op **nieuw stuurprogramma**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="19dd1-250">Voer de volgende informatie in:</span><span class="sxs-lookup"><span data-stu-id="19dd1-250">Enter the following information:</span></span>

   * <span data-ttu-id="19dd1-251">**Naam**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="19dd1-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="19dd1-252">**Voorbeeld-URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="19dd1-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="19dd1-253">**Klassenaam**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="19dd1-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="19dd1-254">Gebruiker alle kleine letters in de voorbeeld-URL.</span><span class="sxs-lookup"><span data-stu-id="19dd1-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="19dd1-255">U kunt gebruiken ze volledig zookeeper quorum als een ervan is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="19dd1-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="19dd1-256">De hostnamen zijn zookeeper0, zookeeper1 en zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="19dd1-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-driver]
5. <span data-ttu-id="19dd1-258">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-258">Click **OK**.</span></span>

<span data-ttu-id="19dd1-259">**Een alias aan de HBase-cluster maken**</span><span class="sxs-lookup"><span data-stu-id="19dd1-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="19dd1-260">SQuirreL, klik op de **aliassen** tabblad aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="19dd1-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="19dd1-261">Van de **aliassen** menu, klikt u op **Alias voor nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="19dd1-262">Voer de volgende informatie in:</span><span class="sxs-lookup"><span data-stu-id="19dd1-262">Enter the following information:</span></span>

   * <span data-ttu-id="19dd1-263">**Naam**: de naam van de HBase-cluster of een willekeurige naam die u liever.</span><span class="sxs-lookup"><span data-stu-id="19dd1-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="19dd1-264">**Stuurprogramma**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="19dd1-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="19dd1-265">Dit moet overeenkomen met de naam van het stuurprogramma die u in de laatste procedure hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19dd1-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="19dd1-266">**URL**: de URL van de configuratie van uw stuurprogramma gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="19dd1-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="19dd1-267">Zorg ervoor dat aan gebruiker alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="19dd1-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="19dd1-268">**Gebruikersnaam**: deze tekst kan worden.</span><span class="sxs-lookup"><span data-stu-id="19dd1-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="19dd1-269">Omdat u hier VPN-verbinding gebruiken, wordt de gebruikersnaam niet helemaal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19dd1-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="19dd1-270">**Wachtwoord**: deze tekst kan worden.</span><span class="sxs-lookup"><span data-stu-id="19dd1-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-alias]
4. <span data-ttu-id="19dd1-272">Klik op **Test**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-272">Click **Test**.</span></span>
5. <span data-ttu-id="19dd1-273">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-273">Click **Connect**.</span></span> <span data-ttu-id="19dd1-274">Wanneer de verbinding maakt, wordt de SQuirreL ziet:</span><span class="sxs-lookup"><span data-stu-id="19dd1-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="19dd1-276">**Een test uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="19dd1-276">**To run a test**</span></span>

1. <span data-ttu-id="19dd1-277">Klik op de **SQL** tabblad rechts naast de **objecten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="19dd1-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="19dd1-278">Kopieer en plak de volgende code:</span><span class="sxs-lookup"><span data-stu-id="19dd1-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="19dd1-279">Klik op uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19dd1-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="19dd1-281">Ga terug naar de **objecten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="19dd1-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="19dd1-282">Vouw de aliasnaam uit en vouw vervolgens **tabel**.</span><span class="sxs-lookup"><span data-stu-id="19dd1-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="19dd1-283">U ziet de nieuwe tabel vermeld in.</span><span class="sxs-lookup"><span data-stu-id="19dd1-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19dd1-284">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19dd1-284">Next steps</span></span>
<span data-ttu-id="19dd1-285">In dit artikel hebt u geleerd hoe u van Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19dd1-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="19dd1-286">Zie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19dd1-286">To learn more, see</span></span>

* <span data-ttu-id="19dd1-287">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="19dd1-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="19dd1-288">[HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: door de integratie van virtueel netwerk, HBase-clusters kunnen worden geïmplementeerd op hetzelfde virtuele netwerk als uw toepassingen zodat toepassingen met HBase communiceren kunnen rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="19dd1-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="19dd1-289">[Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): informatie over het configureren van HBase-replicatie tussen twee Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="19dd1-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="19dd1-290">[Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe u realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19dd1-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
