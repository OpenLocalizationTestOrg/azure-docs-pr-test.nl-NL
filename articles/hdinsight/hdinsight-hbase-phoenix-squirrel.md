---
title: aaaUse Apache Phoenix en SQuirreL met op basis van Windows Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Phoenix in HDInsight, en hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight.
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
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="2c952-103">Apache Phoenix en SQuirreL gebruiken met HBase op basis van Windows-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c952-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="2c952-104">Meer informatie over hoe toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, en hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c952-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="2c952-105">Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="2c952-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="2c952-106">Zie voor Hallo Phoenix grammatica, [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="2c952-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="2c952-107">Zie voor Hallo Phoenix versie-informatie in HDInsight, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2c952-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="2c952-108">Hallo stappen in dit document alleen werk voor op Windows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="2c952-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2c952-109">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="2c952-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="2c952-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2c952-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2c952-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c952-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="2c952-112">Zie voor meer informatie over het gebruik van Phoenix op Linux gebaseerde HDInsight [gebruik Apache Phoenix met HBase op basis van Linux-clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2c952-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="2c952-113">Gebruik SQLLine</span><span class="sxs-lookup"><span data-stu-id="2c952-113">Use SQLLine</span></span>
<span data-ttu-id="2c952-114">[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregel-hulpprogramma tooexecute SQL.</span><span class="sxs-lookup"><span data-stu-id="2c952-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2c952-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c952-115">Prerequisites</span></span>
<span data-ttu-id="2c952-116">Voordat u SQLLine gebruiken kunt, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="2c952-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="2c952-117">**Een HBase-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2c952-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="2c952-118">Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2c952-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="2c952-119">**Verbinding maken met HBase-cluster via remote desktop protocol Hallo toohello**.</span><span class="sxs-lookup"><span data-stu-id="2c952-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="2c952-120">Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van de klassieke Azure-Portal Hallo][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="2c952-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="2c952-121">**toofind uit Hallo-hostnaam**</span><span class="sxs-lookup"><span data-stu-id="2c952-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="2c952-122">Open **Hadoop-opdrachtregel** vanaf Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="2c952-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="2c952-123">Voer Hallo opdracht tooget Hallo DNS-achtervoegsel te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c952-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="2c952-124">Noteer **verbindingsspecifieke DNS-achtervoegsel**.</span><span class="sxs-lookup"><span data-stu-id="2c952-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="2c952-125">Bijvoorbeeld: *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="2c952-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="2c952-126">Als u verbinding tooan HBase-cluster, moet u tooconnect tooone van Hallo Zookeepers met FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="2c952-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="2c952-127">Elke HDInsight-cluster heeft 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="2c952-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="2c952-128">Ze zijn *zookeeper0*, *zookeeper1*, en *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="2c952-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="2c952-129">Hallo FQDN is ongeveer *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="2c952-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="2c952-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="2c952-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="2c952-131">Open **Hadoop-opdrachtregel** vanaf Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="2c952-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="2c952-132">Voer Hallo opdrachten tooopen SQLLine te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c952-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![Phoenix sqlline van HDInsight hbase][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="2c952-134">Hallo-opdrachten in het Hallo-voorbeeld gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2c952-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="2c952-135">Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="2c952-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="2c952-136">SQuirreL gebruiken</span><span class="sxs-lookup"><span data-stu-id="2c952-136">Use SQuirreL</span></span>
<span data-ttu-id="2c952-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is een grafische Java-programma dat kunt u tooview Hallo structuur van een JDBC compatibele database, gegevens hello in tabellen bladeren, voert u SQL-opdrachten enzovoort. Het kan gebruikte tooconnect tooApache Phoenix in HDInsight zijn.</span><span class="sxs-lookup"><span data-stu-id="2c952-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="2c952-138">Deze sectie leest u hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight via VPN.</span><span class="sxs-lookup"><span data-stu-id="2c952-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2c952-139">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c952-139">Prerequisites</span></span>
<span data-ttu-id="2c952-140">Voordat u Hallo procedures uitvoert, moet u Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="2c952-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="2c952-141">Een HBase-cluster geïmplementeerd tooan virtuele Azure-netwerk met een DNS-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c952-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="2c952-142">Zie voor instructies [maken HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="2c952-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="2c952-143">Hallo HBase-cluster cluster verbindingsspecifiek DNS-achtervoegsel worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2c952-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="2c952-144">tooget het RDP in Hallo-cluster, en voer vervolgens IPConfig.</span><span class="sxs-lookup"><span data-stu-id="2c952-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="2c952-145">Hallo DNS-achtervoegsel is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="2c952-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="2c952-146">Download en installeer [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="2c952-147">U moet makecert van Hallo pakket toocreate uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="2c952-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="2c952-148">Download en installeer [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="2c952-149">SQuirreL SQL clientversie 3.0 en hoger vereist JRE 1.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2c952-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="2c952-150">Een punt-naar-Site VPN-verbinding toohello virtuele Azure-netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="2c952-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="2c952-151">Er zijn 3 stappen voor het configureren van een punt-naar-site VPN-verbinding:</span><span class="sxs-lookup"><span data-stu-id="2c952-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="2c952-152">Een virtueel netwerk en een gateway voor dynamische routering configureren</span><span class="sxs-lookup"><span data-stu-id="2c952-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="2c952-153">Uw certificaten maken</span><span class="sxs-lookup"><span data-stu-id="2c952-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="2c952-154">Uw VPN-client configureren</span><span class="sxs-lookup"><span data-stu-id="2c952-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="2c952-155">Zie [configureren van een punt-naar-Site VPN-verbinding tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c952-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="2c952-156">Een virtueel netwerk en een gateway voor dynamische routering configureren</span><span class="sxs-lookup"><span data-stu-id="2c952-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="2c952-157">U hebt een HBase-cluster in virtueel netwerk van Azure ingericht zorgen (Zie Hallo-vereisten voor deze sectie).</span><span class="sxs-lookup"><span data-stu-id="2c952-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="2c952-158">de volgende stap Hallo is tooconfigure een punt-naar-site-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2c952-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="2c952-159">**tooconfigure hello punt-naar-site-connectiviteit**</span><span class="sxs-lookup"><span data-stu-id="2c952-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="2c952-160">Meld u aan toohello [klassieke Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2c952-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="2c952-161">Klik aan de linkerkant Hallo op **netwerken**.</span><span class="sxs-lookup"><span data-stu-id="2c952-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="2c952-162">Klik op Hallo virtuele netwerk dat u hebt gemaakt (Zie [inrichten HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="2c952-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="2c952-163">Klik op **configureren** van Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="2c952-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="2c952-164">In Hallo **punt-naar-site-connectiviteit** sectie **punt-naar-site-connectiviteit configureren**.</span><span class="sxs-lookup"><span data-stu-id="2c952-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="2c952-165">Configureer **IP-BEGINADRES** en **CIDR** toospecify Hallo IP-adresbereik waarvan uw VPN-clients een IP-adres ontvangen wanneer verbonden adres.</span><span class="sxs-lookup"><span data-stu-id="2c952-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="2c952-166">Hallo bereik kan niet overlappen met Hallo bereiken in uw on-premises netwerk en Hallo u verbinding met virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c952-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="2c952-167">Bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2c952-167">For example.</span></span> <span data-ttu-id="2c952-168">Als u 10.0.0.0/20 voor Hallo virtueel netwerk hebt geselecteerd, kunt u 10.1.0.0/24 voor Hallo client-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="2c952-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="2c952-169">Zie Hallo [punt-naar-Site-connectiviteit] [ vnet-point-to-site-connectivity] pagina voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c952-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="2c952-170">Klik in Hallo virtueel netwerk adres spaties sectie op **gatewaysubnet toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2c952-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="2c952-171">Klik op **opslaan** op Hallo onder aan Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="2c952-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="2c952-172">Klik op **Ja** tooconfirm Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2c952-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="2c952-173">Wacht totdat het Hallo-systeem Hallo wijzigen voordat u doorgaat met de volgende procedure toohello heeft aangebracht.</span><span class="sxs-lookup"><span data-stu-id="2c952-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="2c952-174">**toocreate een gateway voor dynamische routering**</span><span class="sxs-lookup"><span data-stu-id="2c952-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="2c952-175">Hallo klassieke Azure-Portal, klik op **DASHBOARD** van Hallo Hallo pagina bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2c952-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="2c952-176">Klik op **GATEWAY maken** van Hallo onder Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c952-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="2c952-177">Klik op **Ja** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2c952-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="2c952-178">Wacht totdat het Hallo-gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c952-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="2c952-179">Klik op **DASHBOARD** van Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="2c952-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="2c952-180">Hier ziet u een diagram van het virtuele netwerk Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c952-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Virtuele Azure-netwerk punt-naar-site-diagram][img-vnet-diagram]

    <span data-ttu-id="2c952-182">Hallo diagram toont 0 clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="2c952-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="2c952-183">Nadat u een verbinding toohello virtueel netwerk, wordt Hallo aantal bijgewerkte tooone zijn.</span><span class="sxs-lookup"><span data-stu-id="2c952-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="2c952-184">Uw certificaten maken</span><span class="sxs-lookup"><span data-stu-id="2c952-184">Create your certificates</span></span>
<span data-ttu-id="2c952-185">Eenzijdige toocreate een X.509-certificaat is via Hallo certificaat hulpprogramma voor het maken (makecert.exe) die wordt geleverd met [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c952-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="2c952-186">**een zelfondertekend basiscertificaat toocreate**</span><span class="sxs-lookup"><span data-stu-id="2c952-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="2c952-187">Open een opdrachtpromptvenster vanuit uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="2c952-188">Navigeer map toohello Visual Studio-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2c952-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="2c952-189">Hallo volgende opdracht in Hallo in het volgende voorbeeld maakt en installeer een basiscertificaat in Hallo persoonlijke certificaatarchief op uw werkstation en ook maken een cer-bestand dat u later toohello klassieke Azure-Portal gaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="2c952-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="2c952-190">Toohello map die u Hallo .cer-bestand toobe bevinden zich wilt in, waarbij HBaseVnetVPNRootCertificate Hallo naam dat u toouse voor Hallo certificaat wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2c952-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="2c952-191">Sluit de opdrachtprompt Hallo niet.</span><span class="sxs-lookup"><span data-stu-id="2c952-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="2c952-192">U moet deze in de volgende procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c952-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2c952-193">Omdat u een basiscertificaat op basis waarvan clientcertificaten worden gegenereerd hebt gemaakt, kunt u tooexport wilt dat dit certificaat samen met de persoonlijke sleutel en sla het tooa veilige locatie waar deze kunnen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="2c952-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="2c952-194">**een clientcertificaat toocreate**</span><span class="sxs-lookup"><span data-stu-id="2c952-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="2c952-195">Van Hallo dezelfde opdrachtprompt (toobe op Hallo heeft dezelfde computer waarop u Hallo basiscertificaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c952-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="2c952-196">Hallo-clientcertificaat moet worden gegenereerd vanuit Hallo basiscertificaat), voer hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c952-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="2c952-197">HBaseVnetVPNRootCertificate is certificaatnaam Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="2c952-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="2c952-198">Toomatch hello hoofdnaam certificaat heeft.</span><span class="sxs-lookup"><span data-stu-id="2c952-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="2c952-199">Zowel Hallo-basiscertificaat en clientcertificaat Hallo worden opgeslagen in uw persoonlijke certificaatarchief op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2c952-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="2c952-200">Gebruik certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="2c952-200">Use certmgr.msc tooverify.</span></span>

    ![Virtuele Azure-netwerk punt-naar-site VPN-certificaat][img-certificate]

    <span data-ttu-id="2c952-202">Een clientcertificaat moet worden geïnstalleerd op elke computer die u wilt dat tooconnect toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c952-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="2c952-203">U wordt aangeraden dat u unieke client certificaten voor elke computer maken die u wilt dat tooconnect toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c952-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="2c952-204">Hallo clientcertificaten tooexport certmgr.msc gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c952-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="2c952-205">**tooupload hello root certificate toohello klassieke Azure-Portal**</span><span class="sxs-lookup"><span data-stu-id="2c952-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="2c952-206">Hallo klassieke Azure-Portal, klik op **netwerk** op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="2c952-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="2c952-207">Klik op Hallo virtueel netwerk waar uw HBase-cluster wordt geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="2c952-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="2c952-208">Klik op **certificaten** van Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="2c952-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="2c952-209">Klik op **uploaden** van Hallo onderzijde en u hebt gemaakt in procedure vóór laatste Hallo Hallo basiscertificaatbestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c952-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="2c952-210">Wacht totdat het Hallo-certificaat hebt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="2c952-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="2c952-211">Klik op **DASHBOARD** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2c952-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="2c952-212">Hallo virtuele diagram toont Hallo status.</span><span class="sxs-lookup"><span data-stu-id="2c952-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="2c952-213">Uw VPN-client configureren</span><span class="sxs-lookup"><span data-stu-id="2c952-213">Configure your VPN client</span></span>
<span data-ttu-id="2c952-214">**toodownload en installeer Hallo VPN-clientpakket**</span><span class="sxs-lookup"><span data-stu-id="2c952-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="2c952-215">Klik op een van de dashboardpagina Hallo Hallo virtueel netwerk in Hallo snelle weergave sectie **downloaden Hallo 64-bits VPN-clientpakket** of **downloaden Hallo 32-bits VPN-clientpakket** op basis van uw werkstation OS-versie.</span><span class="sxs-lookup"><span data-stu-id="2c952-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="2c952-216">Klik op **uitvoeren** tooinstall Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="2c952-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="2c952-217">Hallo wordt weergegeven, klikt u op **meer info**, en klik vervolgens op **toch uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="2c952-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="2c952-218">Klik op **Ja** twee keer.</span><span class="sxs-lookup"><span data-stu-id="2c952-218">Click **Yes** twice.</span></span>

<span data-ttu-id="2c952-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="2c952-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="2c952-220">Klik op Hallo netwerken pictogram op de taakbalk Hallo op Hallo-bureaublad van uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="2c952-221">U ziet een VPN-verbinding met de naam van uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c952-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="2c952-222">Klik op de naam van Hallo VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2c952-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="2c952-223">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="2c952-223">Click **Connect**.</span></span>

<span data-ttu-id="2c952-224">**tootest hello naamomzetting van VPN-verbinding en het domein**</span><span class="sxs-lookup"><span data-stu-id="2c952-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="2c952-225">Open een opdrachtprompt op Hallo-werkstation en ping Hallo na namen Hallo HBase-cluster van DNS-achtervoegsel is myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="2c952-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="2c952-226">Installeren en configureren van SQuirreL op uw werkstation</span><span class="sxs-lookup"><span data-stu-id="2c952-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="2c952-227">**tooinstall SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="2c952-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="2c952-228">Hallo SQuirreL SQL client jar bestand downloaden via [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="2c952-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="2c952-229">Hallo openen/uitvoeren jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="2c952-229">Open/run hello jar file.</span></span> <span data-ttu-id="2c952-230">Hiervoor Hallo [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="2c952-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="2c952-231">Klik op **volgende** twee keer.</span><span class="sxs-lookup"><span data-stu-id="2c952-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="2c952-232">Geef een pad op waar u Hallo schrijftoegang en klik vervolgens op hebt **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2c952-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2c952-233">Hallo standaardinstallatiemap is Hallo C:\Program Files\squirrel-sql-3.6 map.</span><span class="sxs-lookup"><span data-stu-id="2c952-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="2c952-234">In de volgorde toowrite toothis pad moet Hallo installatieprogramma Hallo administrator-bevoegdheden worden toegekend.</span><span class="sxs-lookup"><span data-stu-id="2c952-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="2c952-235">U kunt open een opdrachtprompt als beheerder, navigeer tooJava de bin-map en voer vervolgens:</span><span class="sxs-lookup"><span data-stu-id="2c952-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="2c952-236">Java.exe-jar [pad Hallo van Hallo SQuirreL jar-bestand]</span><span class="sxs-lookup"><span data-stu-id="2c952-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="2c952-237">Klik op **OK** tooconfirm Hallo doelmap maken.</span><span class="sxs-lookup"><span data-stu-id="2c952-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="2c952-238">de standaardinstelling Hallo is tooinstall Hallo basis en standaard pakketten.</span><span class="sxs-lookup"><span data-stu-id="2c952-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="2c952-239">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="2c952-239">Click **Next**.</span></span>
7. <span data-ttu-id="2c952-240">Klik op **volgende** tweemaal, en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="2c952-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="2c952-241">**tooinstall hello Phoenix stuurprogramma**</span><span class="sxs-lookup"><span data-stu-id="2c952-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="2c952-242">Hallo phoenix stuurprogramma jar-bestand bevindt zich op Hallo HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c952-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="2c952-243">Hallo-pad is vergelijkbaar toohello volgende op basis van Hallo-versies:</span><span class="sxs-lookup"><span data-stu-id="2c952-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="2c952-244">U moet toocopy het werkstation tooyour onder Hallo [SQuirreL-installatiemap] / lib pad.</span><span class="sxs-lookup"><span data-stu-id="2c952-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="2c952-245">Hallo gemakkelijkst tooRDP in Hallo-cluster en gebruik bestand kopiëren en plakken (CTRL + C en CTRL + V) toocopy het tooyour werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="2c952-246">**een stuurprogramma Phoenix tooSQuirreL tooadd**</span><span class="sxs-lookup"><span data-stu-id="2c952-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="2c952-247">Open SQuirreL SQL-Client op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="2c952-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="2c952-248">Klik op Hallo **stuurprogramma** tabblad op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="2c952-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="2c952-249">Van Hallo **stuurprogramma's** menu, klikt u op **nieuw stuurprogramma**.</span><span class="sxs-lookup"><span data-stu-id="2c952-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="2c952-250">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="2c952-250">Enter hello following information:</span></span>

   * <span data-ttu-id="2c952-251">**Naam**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="2c952-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="2c952-252">**Voorbeeld-URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="2c952-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="2c952-253">**Klassenaam**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="2c952-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="2c952-254">Gebruiker alle kleine letters in Hallo voorbeeld-URL.</span><span class="sxs-lookup"><span data-stu-id="2c952-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="2c952-255">U kunt gebruiken ze volledig zookeeper quorum als een ervan is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2c952-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="2c952-256">Hallo hostnamen zijn zookeeper0, zookeeper1 en zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="2c952-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-driver]
5. <span data-ttu-id="2c952-258">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c952-258">Click **OK**.</span></span>

<span data-ttu-id="2c952-259">**toocreate een alias toohello HBase-cluster**</span><span class="sxs-lookup"><span data-stu-id="2c952-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="2c952-260">Klik op Hallo van SQuirreL, **aliassen** tabblad op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="2c952-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="2c952-261">Van Hallo **aliassen** menu, klikt u op **Alias voor nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="2c952-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="2c952-262">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="2c952-262">Enter hello following information:</span></span>

   * <span data-ttu-id="2c952-263">**Naam**: Hallo-naam van Hallo HBase-cluster of een willekeurige naam die u liever.</span><span class="sxs-lookup"><span data-stu-id="2c952-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="2c952-264">**Stuurprogramma**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="2c952-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="2c952-265">Dit moet overeenkomen met de naam stuurprogramma Hallo die u hebt gemaakt in de laatste procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c952-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="2c952-266">**URL**: Hallo-URL is gekopieerd uit uw stuurprogrammaconfiguratie van het.</span><span class="sxs-lookup"><span data-stu-id="2c952-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="2c952-267">Zorg ervoor dat toouser alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="2c952-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="2c952-268">**Gebruikersnaam**: deze tekst kan worden.</span><span class="sxs-lookup"><span data-stu-id="2c952-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="2c952-269">Omdat u hier VPN-verbinding gebruiken, wordt helemaal Hallo gebruikersnaam niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2c952-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="2c952-270">**Wachtwoord**: deze tekst kan worden.</span><span class="sxs-lookup"><span data-stu-id="2c952-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-alias]
4. <span data-ttu-id="2c952-272">Klik op **Test**.</span><span class="sxs-lookup"><span data-stu-id="2c952-272">Click **Test**.</span></span>
5. <span data-ttu-id="2c952-273">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="2c952-273">Click **Connect**.</span></span> <span data-ttu-id="2c952-274">Wanneer het Hallo-verbinding maakt, wordt de SQuirreL ziet:</span><span class="sxs-lookup"><span data-stu-id="2c952-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="2c952-276">**een test toorun**</span><span class="sxs-lookup"><span data-stu-id="2c952-276">**toorun a test**</span></span>

1. <span data-ttu-id="2c952-277">Klik op Hallo **SQL** tabblad rechts volgende toohello **objecten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2c952-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="2c952-278">Kopieer en plak de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c952-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="2c952-279">Klik op Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c952-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="2c952-281">Overschakelen back toohello **objecten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2c952-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="2c952-282">Vouw de aliasnaam Hallo uit en vouw vervolgens **tabel**.</span><span class="sxs-lookup"><span data-stu-id="2c952-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="2c952-283">U ziet de nieuwe tabel Hallo vermeld in.</span><span class="sxs-lookup"><span data-stu-id="2c952-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c952-284">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c952-284">Next steps</span></span>
<span data-ttu-id="2c952-285">In dit artikel hebt u geleerd hoe toouse Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c952-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="2c952-286">toolearn meer, Zie</span><span class="sxs-lookup"><span data-stu-id="2c952-286">toolearn more, see</span></span>

* <span data-ttu-id="2c952-287">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="2c952-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="2c952-288">[HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden dat toepassingen met communiceren kunnen Rechtstreeks HBase.</span><span class="sxs-lookup"><span data-stu-id="2c952-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="2c952-289">[Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): meer informatie over hoe tooconfigure HBase-replicatie tussen twee Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="2c952-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="2c952-290">[Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe toodo realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c952-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
