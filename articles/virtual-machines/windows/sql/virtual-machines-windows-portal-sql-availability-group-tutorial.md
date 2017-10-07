---
title: aaaSQL Server-beschikbaarheidsgroepen - virtuele Machines van de Azure - zelfstudie | Microsoft Docs
description: Deze zelfstudie laat zien hoe toocreate een SQL Server altijd op beschikbaarheidsgroep op Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="b20fc-103">Configureren AlwaysOn-beschikbaarheidsgroep in Azure VM handmatig</span><span class="sxs-lookup"><span data-stu-id="b20fc-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="b20fc-104">Deze zelfstudie laat zien hoe toocreate een SQL Server altijd op beschikbaarheidsgroep op Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="b20fc-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="b20fc-105">Hallo voltooid zelfstudie maakt een beschikbaarheidsgroep met een databasereplica op twee SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="b20fc-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="b20fc-106">**Tijd schatting**: duurt ongeveer 30 minuten toocomplete als Hallo vereisten is voldaan.</span><span class="sxs-lookup"><span data-stu-id="b20fc-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="b20fc-107">Hallo diagram ziet u wat u in de zelfstudie Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="b20fc-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b20fc-109">Prerequisites</span></span>

<span data-ttu-id="b20fc-110">Hallo-zelfstudie wordt ervan uitgegaan dat u basiskennis van SQL Server altijd op beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="b20fc-111">Als u meer informatie, Zie [overzicht van AlwaysOn-beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="b20fc-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="b20fc-112">Hallo bevat volgende tabel dat u toocomplete nodig hebt voordat u deze zelfstudie Hallo-vereisten:</span><span class="sxs-lookup"><span data-stu-id="b20fc-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="b20fc-113">Vereiste</span><span class="sxs-lookup"><span data-stu-id="b20fc-113">Requirement</span></span> |<span data-ttu-id="b20fc-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b20fc-114">Description</span></span> |
|----- |----- |----- |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="b20fc-116">Twee SQL-Servers</span><span class="sxs-lookup"><span data-stu-id="b20fc-116">Two SQL Servers</span></span> | <span data-ttu-id="b20fc-117">-In een Azure beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="b20fc-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="b20fc-118">-In één domein</span><span class="sxs-lookup"><span data-stu-id="b20fc-118">- In a single domain</span></span> <br/> <span data-ttu-id="b20fc-119">-Met de functie Failover Clustering is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="b20fc-119">- With Failover Clustering feature installed</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="b20fc-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="b20fc-121">Windows Server</span></span> | <span data-ttu-id="b20fc-122">Bestandsshare voor cluster-witness</span><span class="sxs-lookup"><span data-stu-id="b20fc-122">File share for cluster witness</span></span> |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b20fc-124">SQL Server-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="b20fc-124">SQL Server service account</span></span> | <span data-ttu-id="b20fc-125">Domeinaccount</span><span class="sxs-lookup"><span data-stu-id="b20fc-125">Domain account</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b20fc-127">SQL Server Agent-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="b20fc-127">SQL Server Agent service account</span></span> | <span data-ttu-id="b20fc-128">Domeinaccount</span><span class="sxs-lookup"><span data-stu-id="b20fc-128">Domain account</span></span> |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b20fc-130">Firewall-poorten</span><span class="sxs-lookup"><span data-stu-id="b20fc-130">Firewall ports open</span></span> | <span data-ttu-id="b20fc-131">-SQL Server: **1433** voor het standaardexemplaar</span><span class="sxs-lookup"><span data-stu-id="b20fc-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="b20fc-132">-Eindpunt voor databasespiegeling: **5022** of een beschikbare poort</span><span class="sxs-lookup"><span data-stu-id="b20fc-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="b20fc-133">-Azure load balancer-test: **59999** of een beschikbare poort</span><span class="sxs-lookup"><span data-stu-id="b20fc-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b20fc-135">Toevoegen van de functie Failoverclustering</span><span class="sxs-lookup"><span data-stu-id="b20fc-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="b20fc-136">Deze functie nodig hebben voor zowel SQL-Servers</span><span class="sxs-lookup"><span data-stu-id="b20fc-136">Both SQL Servers require this feature</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b20fc-138">Installatieaccount van het domein</span><span class="sxs-lookup"><span data-stu-id="b20fc-138">Installation domain account</span></span> | <span data-ttu-id="b20fc-139">-Lokale beheerder zijn op elke SQL Server</span><span class="sxs-lookup"><span data-stu-id="b20fc-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="b20fc-140">-Lid is van SQL Server vaste serverrol sysadmin voor elk exemplaar van SQL Server</span><span class="sxs-lookup"><span data-stu-id="b20fc-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="b20fc-141">Voordat u met Hallo zelfstudie begint, moet u deze te[voldoen aan vereisten voor het maken van AlwaysOn-beschikbaarheidsgroepen in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="b20fc-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="b20fc-142">Als deze vereiste onderdelen zijn al voltooid, kunt u gaan te[Cluster maken](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="b20fc-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="b20fc-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="b20fc-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="b20fc-144">Na Hallo vereisten zijn voltooid, is de eerste stap Hallo toocreate een Windows Server-failovercluster met twee SQL-servers en een witness-server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="b20fc-145">RDP-toohello eerste SQL-Server met behulp van een domeinaccount met een Administrator op SQL-Servers en Hallo witness-server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="b20fc-146">Als u Hallo gevolgd [vereisten document](virtual-machines-windows-portal-sql-availability-group-prereq.md), u hebt gemaakt met een account met de naam **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="b20fc-147">Dit account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b20fc-147">Use this account.</span></span>

2. <span data-ttu-id="b20fc-148">In Hallo **Serverbeheer** dashboard, selecteer **extra**, en klik vervolgens op **Failoverclusterbeheer**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="b20fc-149">Klik in het linkerdeelvenster Hallo met de rechtermuisknop op **Failoverclusterbeheer**, en klik vervolgens op **maken van een Cluster**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="b20fc-150">![Cluster maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="b20fc-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="b20fc-151">In Hallo Wizard Cluster maken, een cluster met één knooppunt maken door het Hallo-pagina's met instellingen in de volgende tabel Hallo Hallo doorlopen:</span><span class="sxs-lookup"><span data-stu-id="b20fc-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="b20fc-152">Pagina</span><span class="sxs-lookup"><span data-stu-id="b20fc-152">Page</span></span> | <span data-ttu-id="b20fc-153">Instellingen</span><span class="sxs-lookup"><span data-stu-id="b20fc-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="b20fc-154">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b20fc-154">Before You Begin</span></span> |<span data-ttu-id="b20fc-155">Standaardinstellingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="b20fc-155">Use defaults</span></span> |
   | <span data-ttu-id="b20fc-156">Servers selecteren</span><span class="sxs-lookup"><span data-stu-id="b20fc-156">Select Servers</span></span> |<span data-ttu-id="b20fc-157">Type Hallo eerste SQL-Server in de naam **Enter servernaam** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="b20fc-158">Van validatiewaarschuwing</span><span class="sxs-lookup"><span data-stu-id="b20fc-158">Validation Warning</span></span> |<span data-ttu-id="b20fc-159">Selecteer **nr. ik geen ondersteuning van Microsoft nodig hebt voor dit cluster, en daarom niet wilt dat toorun Hallo validatie wordt getest. Als ik op Volgende klikt, doorgaan met het Hallo-cluster maken**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="b20fc-160">Toegangspunt voor beheer Hallo Cluster</span><span class="sxs-lookup"><span data-stu-id="b20fc-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="b20fc-161">Typ de naam van een cluster, zoals **SQLAGCluster1** in **clusternaam**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="b20fc-162">Bevestiging</span><span class="sxs-lookup"><span data-stu-id="b20fc-162">Confirmation</span></span> |<span data-ttu-id="b20fc-163">Gebruik de standaardwaarden tenzij u van opslagruimten gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="b20fc-164">Zie Hallo opmerking onder deze tabel.</span><span class="sxs-lookup"><span data-stu-id="b20fc-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="b20fc-165">Hallo cluster-IP-adres instellen</span><span class="sxs-lookup"><span data-stu-id="b20fc-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="b20fc-166">In **Failoverclusterbeheer**, schuif naar beneden te**Clusterkernresources** en vouw Hallo clusterdetails.</span><span class="sxs-lookup"><span data-stu-id="b20fc-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="b20fc-167">Ziet u beide Hallo **naam** en Hallo **IP-adres** bronnen in Hallo **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="b20fc-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="b20fc-168">Hallo bron van het IP-adres kan niet online worden gebracht omdat Hallo-cluster is toegewezen Hallo dezelfde IP-adres als Hallo machine zelf, is een dubbel adres.</span><span class="sxs-lookup"><span data-stu-id="b20fc-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="b20fc-169">Klik met de rechtermuisknop Hallo mislukt **IP-adres** bron en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Eigenschappen van cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="b20fc-171">Selecteer **statisch IP-adres** en geef een beschikbaar adres van waarbij Hallo SQL Server in het tekstvak voor het Hallo is-subnet.</span><span class="sxs-lookup"><span data-stu-id="b20fc-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="b20fc-172">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="b20fc-173">In Hallo **Clusterkernresources** sectie, met de rechtermuisknop op de clusternaam van het en klik op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="b20fc-174">Vervolgens wacht u totdat beide bronnen online zijn.</span><span class="sxs-lookup"><span data-stu-id="b20fc-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="b20fc-175">Wanneer de naam clusterbron Hallo online wordt gezet, Hallo DC-server wordt bijgewerkt met een nieuw AD-account.</span><span class="sxs-lookup"><span data-stu-id="b20fc-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="b20fc-176">Gebruik deze AD-account toorun hello later beschikbaarheidsgroep geclusterde service.</span><span class="sxs-lookup"><span data-stu-id="b20fc-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="b20fc-177"><a name="addNode"></a>Voeg andere SQL Server-toocluster Hallo</span><span class="sxs-lookup"><span data-stu-id="b20fc-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="b20fc-178">Voeg andere SQL Server-cluster toohello Hallo.</span><span class="sxs-lookup"><span data-stu-id="b20fc-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="b20fc-179">In de boomstructuur Hallo browser met de rechtermuisknop op het Hallo-cluster en klikt u op **knooppunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Knooppunt toohello Cluster toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="b20fc-181">In Hallo **Wizard knooppunt toevoegen**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="b20fc-182">In Hallo **Servers selecteren** pagina, het toevoegen van Hallo tweede SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="b20fc-183">Type Hallo-servernaam in **Enter servernaam** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="b20fc-184">Wanneer u klaar bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="b20fc-185">In Hallo **Validation Warning** pagina, klikt u op **Nee** (in een productiescenario u moet uitvoeren Hallo validatietests).</span><span class="sxs-lookup"><span data-stu-id="b20fc-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="b20fc-186">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="b20fc-187">In Hallo **bevestiging** pagina als u met opslagruimten kunt wissen Hallo selectievakje **Voeg alle in aanmerking komende opslag toohello cluster.**</span><span class="sxs-lookup"><span data-stu-id="b20fc-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Knooppunt bevestiging toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="b20fc-189">Als u met behulp van opslagruimten en niet doen schakelt **Voeg alle in aanmerking komende opslag toohello cluster**, Windows hello virtuele schijven losgekoppeld tijdens Hallo clustering proces.</span><span class="sxs-lookup"><span data-stu-id="b20fc-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="b20fc-190">Als gevolg hiervan worden niet weergegeven in Schijfbeheer of Explorer totdat Hallo opslagruimten zijn verwijderd uit de cluster Hallo en opnieuw gekoppeld met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b20fc-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="b20fc-191">Opslagruimten gegroepeerd op meerdere schijven in toostorage groepen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="b20fc-192">Zie voor meer informatie [opslagruimten](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="b20fc-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="b20fc-193">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-193">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-194">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-194">Click **Finish**.</span></span>

   <span data-ttu-id="b20fc-195">Failover Cluster Manager blijkt dat het cluster een nieuw knooppunt heeft en wordt weergegeven in Hallo **knooppunten** container.</span><span class="sxs-lookup"><span data-stu-id="b20fc-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="b20fc-196">Afmelding Hallo extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="b20fc-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="b20fc-197">Toevoegen van een clusterquorum-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="b20fc-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="b20fc-198">In dit voorbeeld gebruikt Hallo Windows-cluster een bestandsshare toocreate een clusterquorum.</span><span class="sxs-lookup"><span data-stu-id="b20fc-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="b20fc-199">Deze zelfstudie maakt gebruik van een knooppunt en bestandssharemeerderheid quorum.</span><span class="sxs-lookup"><span data-stu-id="b20fc-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="b20fc-200">Zie voor meer informatie [Quorumconfiguraties in een failovercluster](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="b20fc-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="b20fc-201">Toohello bestandsshare-witness lid bestandsserver verbinden met een extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="b20fc-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="b20fc-202">Op **Serverbeheer**, klikt u op **extra**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="b20fc-203">Open **Computerbeheer**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="b20fc-204">Klik op **gedeelde mappen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="b20fc-205">Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="b20fc-207">Gebruik **Wizard gedeelde map maken** toocreate een share.</span><span class="sxs-lookup"><span data-stu-id="b20fc-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="b20fc-208">Op **mappad**, klikt u op **Bladeren** en niet vinden of een pad voor de gedeelde map Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="b20fc-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="b20fc-209">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-209">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-210">In **naam, beschrijving en instellingen** Hallo sharenaam en het pad controleren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="b20fc-211">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-211">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-212">Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="b20fc-213">Klik op **aangepaste...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="b20fc-214">Op **machtigingen aanpassen**, klikt u op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="b20fc-215">Zorg ervoor dat Hallo account gebruikt toocreate Hallo cluster volledig beheer heeft.</span><span class="sxs-lookup"><span data-stu-id="b20fc-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="b20fc-217">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-217">Click **OK**.</span></span>

1. <span data-ttu-id="b20fc-218">In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="b20fc-219">Klik op **voltooien** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b20fc-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="b20fc-220">Meld u af bij Hallo-server</span><span class="sxs-lookup"><span data-stu-id="b20fc-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="b20fc-221">Clusterquorum configureren</span><span class="sxs-lookup"><span data-stu-id="b20fc-221">Configure cluster quorum</span></span>

<span data-ttu-id="b20fc-222">Vervolgens stelt u het clusterquorum Hallo.</span><span class="sxs-lookup"><span data-stu-id="b20fc-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="b20fc-223">Het eerste clusterknooppunt toohello verbinding met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="b20fc-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="b20fc-224">In **Failoverclusterbeheer**, met de rechtermuisknop op het Hallo-cluster, wijst u te**meer acties**, en klik op **Clusterquoruminstellingen configureren...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="b20fc-226">In **Wizard clusterquorum configureren**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="b20fc-227">In **optie voor quorumconfiguratie**, kies **hello quorumwitness selecteren**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="b20fc-228">Op **Quorumwitness selecteren**, klikt u op **een bestandssharewitness configureren**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="b20fc-229">Windows Server 2016 biedt ondersteuning voor een cloud-witness.</span><span class="sxs-lookup"><span data-stu-id="b20fc-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="b20fc-230">Als u dit soort witness kiest, hoeft u niet een bestand witness delen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="b20fc-231">Zie voor meer informatie [een witness cloud voor een failover-Cluster implementeren](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="b20fc-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="b20fc-232">Deze zelfstudie maakt gebruik van een bestandssharewitness wordt ondersteund door eerdere besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="b20fc-233">Op **bestandssharewitness configureren**, tekst hello pad voor Hallo-share die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="b20fc-234">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-234">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-235">Hallo-instellingen te controleren op **bevestiging**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="b20fc-236">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-236">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-237">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-237">Click **Finish**.</span></span>

<span data-ttu-id="b20fc-238">Hallo clusterkernresources zijn geconfigureerd met een bestandssharewitness.</span><span class="sxs-lookup"><span data-stu-id="b20fc-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="b20fc-239">Beschikbaarheidsgroepen inschakelen</span><span class="sxs-lookup"><span data-stu-id="b20fc-239">Enable Availability Groups</span></span>

<span data-ttu-id="b20fc-240">Schakel vervolgens Hallo **AlwaysOn Availability Groups** functie.</span><span class="sxs-lookup"><span data-stu-id="b20fc-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="b20fc-241">Voer deze stappen uit op beide SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="b20fc-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="b20fc-242">Van Hallo **Start** scherm, starten **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="b20fc-243">Klik in de structuur van de browser Hallo op **SQL Server-Services**, vervolgens met de rechtermuisknop op Hallo **SQL Server (MSSQLSERVER)** service en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="b20fc-244">Klik op Hallo **AlwaysOn hoge beschikbaarheid** tabblad en selecteer vervolgens **Schakel AlwaysOn Availability Groups**als volgt:</span><span class="sxs-lookup"><span data-stu-id="b20fc-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn-beschikbaarheidsgroepen inschakelen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="b20fc-246">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-246">Click **Apply**.</span></span> <span data-ttu-id="b20fc-247">Klik op **OK** in Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="b20fc-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="b20fc-248">Hallo SQL Server-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="b20fc-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="b20fc-249">Herhaal deze stappen op Hallo van andere SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="b20fc-250">Een database maakt op Hallo eerste SQL-Server</span><span class="sxs-lookup"><span data-stu-id="b20fc-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="b20fc-251">Start Hallo RDP-bestand toohello eerste SQL-Server met een domein-account dat lid is van sysadmin vaste serverrol.</span><span class="sxs-lookup"><span data-stu-id="b20fc-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="b20fc-252">Open SQL Server Management Studio en maak verbinding toohello eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="b20fc-253">In **Objectverkenner**, met de rechtermuisknop op **Databases** en klik op **nieuwe Database**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="b20fc-254">In **databasenaam**, type **MyDB1**, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="b20fc-255"><a name="backupshare"></a>Maak een back-share</span><span class="sxs-lookup"><span data-stu-id="b20fc-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="b20fc-256">Hallo eerste SQL-Server in op **Serverbeheer**, klikt u op **extra**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="b20fc-257">Open **Computerbeheer**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="b20fc-258">Klik op **gedeelde mappen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="b20fc-259">Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="b20fc-261">Gebruik **Wizard gedeelde map maken** toocreate een share.</span><span class="sxs-lookup"><span data-stu-id="b20fc-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="b20fc-262">Op **mappad**, klikt u op **Bladeren** en vinden of een pad voor de gedeelde map voor Hallo database back-up te maken.</span><span class="sxs-lookup"><span data-stu-id="b20fc-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="b20fc-263">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-263">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-264">In **naam, beschrijving en instellingen** Hallo sharenaam en het pad controleren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="b20fc-265">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-265">Click **Next**.</span></span>

1. <span data-ttu-id="b20fc-266">Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="b20fc-267">Klik op **aangepaste...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="b20fc-268">Op **machtigingen aanpassen**, klikt u op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="b20fc-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="b20fc-269">Zorg ervoor dat SQL Server en SQL Server Agent-serviceaccounts Hallo voor beide servers volledig beheer hebben.</span><span class="sxs-lookup"><span data-stu-id="b20fc-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="b20fc-271">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-271">Click **OK**.</span></span>

1. <span data-ttu-id="b20fc-272">In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="b20fc-273">Klik op **voltooien** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b20fc-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="b20fc-274">Een volledige back-up van database Hallo duren</span><span class="sxs-lookup"><span data-stu-id="b20fc-274">Take a full backup of hello database</span></span>

<span data-ttu-id="b20fc-275">U moet tooback Hallo nieuwe database tooinitialize Hallo logboekketen van.</span><span class="sxs-lookup"><span data-stu-id="b20fc-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="b20fc-276">Als u een back-up van de nieuwe database Hallo pas van kracht worden, kan deze kan niet worden opgenomen in een beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b20fc-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="b20fc-277">In **Objectverkenner**, met de rechtermuisknop op het Hallo-database, wijs het te**taken...** , klikt u op **Back-Up**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="b20fc-278">Klik op **OK** tootake een volledige back-up toohello standaard back-uplocatie.</span><span class="sxs-lookup"><span data-stu-id="b20fc-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="b20fc-279">Hallo beschikbaarheidsgroep maken</span><span class="sxs-lookup"><span data-stu-id="b20fc-279">Create hello Availability Group</span></span>
<span data-ttu-id="b20fc-280">U bent nu klaar tooconfigure een beschikbaarheidsgroep met Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b20fc-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="b20fc-281">Een database maakt op Hallo eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="b20fc-282">Neem een volledige back-up en de een transactielogboek van Hallo-database</span><span class="sxs-lookup"><span data-stu-id="b20fc-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="b20fc-283">Restore Hallo volledige en logboek back-ups toohello tweede SQL Server Hello **NORECOVERY** optie</span><span class="sxs-lookup"><span data-stu-id="b20fc-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="b20fc-284">Hallo beschikbaarheidsgroep maken (**AG1**) met synchrone doorvoer en automatische failover leesbare secundaire replica's</span><span class="sxs-lookup"><span data-stu-id="b20fc-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="b20fc-285">Hallo beschikbaarheidsgroep maken:</span><span class="sxs-lookup"><span data-stu-id="b20fc-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="b20fc-286">Op de extern bureaublad-sessiehost toohello eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="b20fc-287">In **Objectverkenner** SSMS, met de rechtermuisknop op **AlwaysOn hoge beschikbaarheid** en klik op **nieuwe Wizard beschikbaarheidsgroep**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![De Wizard Nieuwe beschikbaarheidsgroep starten](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="b20fc-289">In Hallo **inleiding** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="b20fc-290">In Hallo **naam van de beschikbaarheidsgroep opgeven** pagina, typ een naam voor Hallo beschikbaarheidsgroep, bijvoorbeeld **AG1**in **naam van de beschikbaarheidsgroep**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="b20fc-291">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-291">Click **Next**.</span></span>

    ![Wizard Nieuwe AG AG-naam opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="b20fc-293">In Hallo **Databases selecteren** pagina, selecteer uw database en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b20fc-294">Hallo database voldoet Hallo-vereisten voor een beschikbaarheidsgroep aan omdat u ten minste één volledige back-up hebt uitgevoerd op Hallo beoogde primaire replica.</span><span class="sxs-lookup"><span data-stu-id="b20fc-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Wizard Nieuwe AG Databases selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="b20fc-296">In Hallo **replica's opgeven** pagina, klikt u op **Replica toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Wizard Nieuwe AG replica's opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="b20fc-298">Hallo **tooServer verbinding** dialoogvenster verschijnt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="b20fc-299">Hallo-typenaam van de tweede server Hallo in **servernaam**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="b20fc-300">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-300">Click **Connect**.</span></span>

   <span data-ttu-id="b20fc-301">Terug in Hallo **replica's opgeven** pagina u ziet nu de tweede server Hallo die worden vermeld in **Beschikbaarheidsreplica**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="b20fc-302">Hallo-replica's als volgt configureren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-302">Configure hello replicas as follows.</span></span>

   ![Wizard Nieuwe AG replica's (voltooid) opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="b20fc-304">Klik op **eindpunten** toosee Hallo eindpunt voor databasespiegeling voor deze beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b20fc-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="b20fc-305">Gebruik Hallo dezelfde poort die u hebt gebruikt bij het instellen van Hallo [firewallregel voor databasespiegeling eindpunten](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="b20fc-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="b20fc-307">In Hallo **eerste gegevenssynchronisatie selecteren** pagina **volledige** en geef een gedeelde netwerklocatie.</span><span class="sxs-lookup"><span data-stu-id="b20fc-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="b20fc-308">Gebruiken voor de locatie van Hallo Hallo [back-upshare die u hebt gemaakt](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="b20fc-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="b20fc-309">In voorbeeld van Hallo was, **\\\\\<eerste SQL-Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="b20fc-310">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b20fc-311">Volledige synchronisatie duurt een volledige back-up van de database op het eerste exemplaar van SQL Server Hallo Hallo en toohello tweede exemplaar te herstellen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="b20fc-312">Voor grote databases worden volledige synchronisatie wordt niet aanbevolen omdat het kan lang duren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="b20fc-313">U kunt deze tijd verkorten door handmatig een back-up van database Hallo duurt en herstellen van deze met `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="b20fc-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="b20fc-314">Als het Hallo-database is al teruggezet met `NO RECOVERY` op Hallo tweede SQL Server voordat u Hallo beschikbaarheidsgroep configureert, kies **alleen deelnemen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="b20fc-315">Als u back-up van tootake Hallo na het Hallo-beschikbaarheidsgroep configureren, kiest **eerste gegevenssynchronisatie overslaan**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="b20fc-317">In Hallo **validatie** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="b20fc-318">Deze pagina ziet vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b20fc-318">This page should look similar toohello following image:</span></span>

    ![Wizard Nieuwe AG, validatie](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="b20fc-320">Er is een waarschuwing voor de configuratie van de listener Hallo omdat u een beschikbaarheidsgroep-listener niet hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b20fc-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="b20fc-321">Omdat u op de virtuele Azure-machines na het maken van hello Azure load balancer Hallo listener maken, kunt u deze waarschuwing negeren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="b20fc-322">In Hallo **samenvatting** pagina, klikt u op **voltooien**, en vervolgens een ogenblik geduld terwijl Hallo wizard configureert u Hallo nieuwe beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b20fc-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="b20fc-323">In Hallo **voortgang** pagina, klikt u op **meer details** tooview Hallo gedetailleerde uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b20fc-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="b20fc-324">Zodra het Hallo-wizard is voltooid, controleert u Hallo **resultaten** pagina tooverify die Hallo beschikbaarheidsgroep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Wizard Nieuwe AG resulteert](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="b20fc-326">Klik op **sluiten** tooexit Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="b20fc-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="b20fc-327">Hallo beschikbaarheidsgroep controleren</span><span class="sxs-lookup"><span data-stu-id="b20fc-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="b20fc-328">In **Objectverkenner**, vouw **AlwaysOn hoge beschikbaarheid**, vouw vervolgens **beschikbaarheidsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="b20fc-329">U ziet nu Hallo nieuwe Availability Group in deze container.</span><span class="sxs-lookup"><span data-stu-id="b20fc-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="b20fc-330">Met de rechtermuisknop op Hallo Availability Group en klik op **Dashboard weergeven**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![AG-Dashboard weergeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="b20fc-332">Uw **AlwaysOn Dashboard** vergelijkbare toothis moet worden gezocht.</span><span class="sxs-lookup"><span data-stu-id="b20fc-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![AG-Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="b20fc-334">Hallo-replica's Hallo failover-modus van de synchronisatiestatus van elke replica en hello, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="b20fc-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="b20fc-335">In **Failoverclusterbeheer**, klikt u op het cluster.</span><span class="sxs-lookup"><span data-stu-id="b20fc-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="b20fc-336">Selecteer **rollen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-336">Select **Roles**.</span></span> <span data-ttu-id="b20fc-337">Hallo beschikbaarheidsgroep naam die u gebruikt, is een rol op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b20fc-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="b20fc-338">Deze beschikbaarheidsgroep heeft geen een IP-adres voor clientverbindingen, omdat u niet een listener hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b20fc-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="b20fc-339">U configureert Hallo listener nadat u een Azure load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="b20fc-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="b20fc-341">Probeer niet toofail via Hallo Availability Group uit Hallo Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b20fc-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="b20fc-342">Alle failover-bewerkingen moeten worden uitgevoerd vanuit **AlwaysOn Dashboard** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="b20fc-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="b20fc-343">Zie voor meer informatie [beperkingen op met Failover Cluster Manager met beschikbaarheidsgroepen Hallo](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="b20fc-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="b20fc-344">U hebt op dit moment een beschikbaarheidsgroep met replica's op twee exemplaren van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b20fc-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="b20fc-345">U kunt Hallo beschikbaarheidsgroep verplaatsen tussen exemplaren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="b20fc-346">U kunt toohello beschikbaarheidsgroep nog kan geen verbinding omdat u niet over een listener.</span><span class="sxs-lookup"><span data-stu-id="b20fc-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="b20fc-347">Hallo-listener vereist in virtuele machines in Azure, een load balancer.</span><span class="sxs-lookup"><span data-stu-id="b20fc-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="b20fc-348">de volgende stap Hallo is toocreate Hallo load balancer in Azure.</span><span class="sxs-lookup"><span data-stu-id="b20fc-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="b20fc-349">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="b20fc-349">Create an Azure load balancer</span></span>

<span data-ttu-id="b20fc-350">Op virtuele machines in Azure vereist een SQL Server-beschikbaarheidsgroep een load balancer.</span><span class="sxs-lookup"><span data-stu-id="b20fc-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="b20fc-351">Hallo load balancer bevat Hallo IP-adres voor de beschikbaarheidsgroep-listener Hallo.</span><span class="sxs-lookup"><span data-stu-id="b20fc-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="b20fc-352">Deze sectie ziet u hoe de toocreate Hallo load balancer in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b20fc-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="b20fc-353">Ga in de Azure-portal hello, toohello resourcegroep waar uw SQL-Servers zijn en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="b20fc-354">Zoeken naar **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="b20fc-355">Kies Hallo load balancer gepubliceerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b20fc-355">Choose hello load balancer published by Microsoft.</span></span>

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="b20fc-357">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-357">Click **Create**.</span></span>
3. <span data-ttu-id="b20fc-358">Hallo volgende parameters voor Hallo load balancer configureren.</span><span class="sxs-lookup"><span data-stu-id="b20fc-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="b20fc-359">Instelling</span><span class="sxs-lookup"><span data-stu-id="b20fc-359">Setting</span></span> | <span data-ttu-id="b20fc-360">Veld</span><span class="sxs-lookup"><span data-stu-id="b20fc-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="b20fc-361">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b20fc-361">**Name**</span></span> |<span data-ttu-id="b20fc-362">Gebruik een naam voor de Hallo load balancer, zoals **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="b20fc-363">**Type**</span><span class="sxs-lookup"><span data-stu-id="b20fc-363">**Type**</span></span> |<span data-ttu-id="b20fc-364">interne</span><span class="sxs-lookup"><span data-stu-id="b20fc-364">Internal</span></span> |
   | <span data-ttu-id="b20fc-365">**Virtueel netwerk**</span><span class="sxs-lookup"><span data-stu-id="b20fc-365">**Virtual network**</span></span> |<span data-ttu-id="b20fc-366">Hallo-naam van Hallo virtuele Azure-netwerk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b20fc-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="b20fc-367">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="b20fc-367">**Subnet**</span></span> |<span data-ttu-id="b20fc-368">Gebruik Hallo-naam van die virtuele machine Hallo Hallo subnet is in.</span><span class="sxs-lookup"><span data-stu-id="b20fc-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="b20fc-369">**IP-adrestoewijzing**</span><span class="sxs-lookup"><span data-stu-id="b20fc-369">**IP address assignment**</span></span> |<span data-ttu-id="b20fc-370">Statisch</span><span class="sxs-lookup"><span data-stu-id="b20fc-370">Static</span></span> |
   | <span data-ttu-id="b20fc-371">**IP-adres**</span><span class="sxs-lookup"><span data-stu-id="b20fc-371">**IP address**</span></span> |<span data-ttu-id="b20fc-372">Gebruik een beschikbaar adres van subnet.</span><span class="sxs-lookup"><span data-stu-id="b20fc-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="b20fc-373">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="b20fc-373">**Subscription**</span></span> |<span data-ttu-id="b20fc-374">Gebruik Hallo hetzelfde abonnement als Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b20fc-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="b20fc-375">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="b20fc-375">**Location**</span></span> |<span data-ttu-id="b20fc-376">Gebruik Hallo dezelfde locatie als Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b20fc-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="b20fc-377">Hello Azure portalblade moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="b20fc-377">hello Azure portal blade should look like this:</span></span>

   ![Load Balancer maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="b20fc-379">Klik op **maken**, toocreate Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b20fc-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="b20fc-380">tooconfigure hello load balancer, moet u een back-endpool toocreate, een test en set Hallo load-balancingregels.</span><span class="sxs-lookup"><span data-stu-id="b20fc-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="b20fc-381">Voer deze in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b20fc-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="b20fc-382">Back-endpool toevoegen</span><span class="sxs-lookup"><span data-stu-id="b20fc-382">Add backend pool</span></span>

1. <span data-ttu-id="b20fc-383">Ga in hello Azure-portal, tooyour beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b20fc-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="b20fc-384">Mogelijk moet u taakverdeler toorefresh Hallo weergave toosee Hallo nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Load Balancer niet vinden in de resourcegroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="b20fc-386">Hallo load balancer op, klik op **back-endpools**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="b20fc-387">Hallo back-endpool als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="b20fc-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="b20fc-388">Instelling</span><span class="sxs-lookup"><span data-stu-id="b20fc-388">Setting</span></span> | <span data-ttu-id="b20fc-389">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b20fc-389">Description</span></span> | <span data-ttu-id="b20fc-390">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b20fc-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b20fc-391">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b20fc-391">**Name**</span></span> | <span data-ttu-id="b20fc-392">Typ een naam</span><span class="sxs-lookup"><span data-stu-id="b20fc-392">Type a text name</span></span> | <span data-ttu-id="b20fc-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="b20fc-393">SQLLBBE</span></span>
   | <span data-ttu-id="b20fc-394">**Gekoppeld aan**</span><span class="sxs-lookup"><span data-stu-id="b20fc-394">**Associated to**</span></span> | <span data-ttu-id="b20fc-395">Kies uit de lijst</span><span class="sxs-lookup"><span data-stu-id="b20fc-395">Pick from list</span></span> | <span data-ttu-id="b20fc-396">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="b20fc-396">Availability set</span></span>
   | <span data-ttu-id="b20fc-397">**Beschikbaarheidsset**</span><span class="sxs-lookup"><span data-stu-id="b20fc-397">**Availability set**</span></span> | <span data-ttu-id="b20fc-398">Gebruik een naam van de beschikbaarheidsset Hallo die uw SQL Server-VM's in</span><span class="sxs-lookup"><span data-stu-id="b20fc-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="b20fc-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="b20fc-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="b20fc-400">**Virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="b20fc-400">**Virtual machines**</span></span> |<span data-ttu-id="b20fc-401">Hallo twee namen van de virtuele machine in Azure SQL-Server</span><span class="sxs-lookup"><span data-stu-id="b20fc-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="b20fc-402">SQL Server-0, SQL Server-1</span><span class="sxs-lookup"><span data-stu-id="b20fc-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="b20fc-403">Typ de naam Hallo voor Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="b20fc-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="b20fc-404">Klik op **+ toevoegen van een virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="b20fc-405">Voor Hallo beschikbaarheidsset kiezen Hallo beschikbaarheidsset die Hallo SQL-Servers bevinden zich in.</span><span class="sxs-lookup"><span data-stu-id="b20fc-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="b20fc-406">Voor virtuele machines zijn beide Hallo SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="b20fc-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="b20fc-407">Neem geen share Hallo-witness bestandsserver.</span><span class="sxs-lookup"><span data-stu-id="b20fc-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="b20fc-408">Klik op **OK** toocreate Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="b20fc-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="b20fc-409">Set Hallo test</span><span class="sxs-lookup"><span data-stu-id="b20fc-409">Set hello probe</span></span>

1. <span data-ttu-id="b20fc-410">Hallo load balancer op, klik op **statuscontroles**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="b20fc-411">Hallo health test als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="b20fc-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="b20fc-412">Instelling</span><span class="sxs-lookup"><span data-stu-id="b20fc-412">Setting</span></span> | <span data-ttu-id="b20fc-413">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b20fc-413">Description</span></span> | <span data-ttu-id="b20fc-414">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b20fc-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b20fc-415">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b20fc-415">**Name**</span></span> | <span data-ttu-id="b20fc-416">Tekst</span><span class="sxs-lookup"><span data-stu-id="b20fc-416">Text</span></span> | <span data-ttu-id="b20fc-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="b20fc-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="b20fc-418">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="b20fc-418">**Protocol**</span></span> | <span data-ttu-id="b20fc-419">Kies TCP</span><span class="sxs-lookup"><span data-stu-id="b20fc-419">Choose TCP</span></span> | <span data-ttu-id="b20fc-420">TCP</span><span class="sxs-lookup"><span data-stu-id="b20fc-420">TCP</span></span> |
   | <span data-ttu-id="b20fc-421">**Poort**</span><span class="sxs-lookup"><span data-stu-id="b20fc-421">**Port**</span></span> | <span data-ttu-id="b20fc-422">Een niet-gebruikte poort</span><span class="sxs-lookup"><span data-stu-id="b20fc-422">Any unused port</span></span> | <span data-ttu-id="b20fc-423">59999</span><span class="sxs-lookup"><span data-stu-id="b20fc-423">59999</span></span> |
   | <span data-ttu-id="b20fc-424">**Interval**</span><span class="sxs-lookup"><span data-stu-id="b20fc-424">**Interval**</span></span>  | <span data-ttu-id="b20fc-425">Hallo hoeveelheid tijd tussen test probeert (in seconden)</span><span class="sxs-lookup"><span data-stu-id="b20fc-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="b20fc-426">5</span><span class="sxs-lookup"><span data-stu-id="b20fc-426">5</span></span> |
   | <span data-ttu-id="b20fc-427">**Drempelwaarde voor onjuiste status**</span><span class="sxs-lookup"><span data-stu-id="b20fc-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="b20fc-428">het aantal opeenvolgende testfouten dat moet worden uitgevoerd voor een virtuele machine toobe niet in orde beschouwd Hallo</span><span class="sxs-lookup"><span data-stu-id="b20fc-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="b20fc-429">2</span><span class="sxs-lookup"><span data-stu-id="b20fc-429">2</span></span> |

1. <span data-ttu-id="b20fc-430">Klik op **OK** tooset Hallo health test.</span><span class="sxs-lookup"><span data-stu-id="b20fc-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="b20fc-431">Hallo taakverdelingsregels instellen</span><span class="sxs-lookup"><span data-stu-id="b20fc-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="b20fc-432">Hallo load balancer op, klik op **Taakverdelingsregels**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="b20fc-433">Hallo load-balancingregels als volgt instellen.</span><span class="sxs-lookup"><span data-stu-id="b20fc-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="b20fc-434">Instelling</span><span class="sxs-lookup"><span data-stu-id="b20fc-434">Setting</span></span> | <span data-ttu-id="b20fc-435">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b20fc-435">Description</span></span> | <span data-ttu-id="b20fc-436">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b20fc-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b20fc-437">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b20fc-437">**Name**</span></span> | <span data-ttu-id="b20fc-438">Tekst</span><span class="sxs-lookup"><span data-stu-id="b20fc-438">Text</span></span> | <span data-ttu-id="b20fc-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="b20fc-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="b20fc-440">**Frontend IP-adres**</span><span class="sxs-lookup"><span data-stu-id="b20fc-440">**Frontend IP address**</span></span> | <span data-ttu-id="b20fc-441">Kies een adres</span><span class="sxs-lookup"><span data-stu-id="b20fc-441">Choose an address</span></span> |<span data-ttu-id="b20fc-442">Gebruik Hallo-adres dat u hebt gemaakt tijdens het maken van Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b20fc-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="b20fc-443">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="b20fc-443">**Protocol**</span></span> | <span data-ttu-id="b20fc-444">Kies TCP</span><span class="sxs-lookup"><span data-stu-id="b20fc-444">Choose TCP</span></span> |<span data-ttu-id="b20fc-445">TCP</span><span class="sxs-lookup"><span data-stu-id="b20fc-445">TCP</span></span> |
   | <span data-ttu-id="b20fc-446">**Poort**</span><span class="sxs-lookup"><span data-stu-id="b20fc-446">**Port**</span></span> | <span data-ttu-id="b20fc-447">Hallo-poort gebruiken voor Hallo SQL Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b20fc-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="b20fc-448">1433</span><span class="sxs-lookup"><span data-stu-id="b20fc-448">1433</span></span> |
   | <span data-ttu-id="b20fc-449">**Back-Endpoort**</span><span class="sxs-lookup"><span data-stu-id="b20fc-449">**Backend Port**</span></span> | <span data-ttu-id="b20fc-450">Dit veld wordt niet gebruikt wanneer zwevend IP is ingesteld voor direct server return</span><span class="sxs-lookup"><span data-stu-id="b20fc-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="b20fc-451">1433</span><span class="sxs-lookup"><span data-stu-id="b20fc-451">1433</span></span> |
   | <span data-ttu-id="b20fc-452">**Test**</span><span class="sxs-lookup"><span data-stu-id="b20fc-452">**Probe**</span></span> |<span data-ttu-id="b20fc-453">Hallo-naam die u hebt opgegeven voor de test Hallo</span><span class="sxs-lookup"><span data-stu-id="b20fc-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="b20fc-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="b20fc-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="b20fc-455">**Sessiepersistentie**</span><span class="sxs-lookup"><span data-stu-id="b20fc-455">**Session Persistence**</span></span> | <span data-ttu-id="b20fc-456">Vervolgkeuzelijst</span><span class="sxs-lookup"><span data-stu-id="b20fc-456">Drop down list</span></span> | <span data-ttu-id="b20fc-457">**Geen**</span><span class="sxs-lookup"><span data-stu-id="b20fc-457">**None**</span></span> |
   | <span data-ttu-id="b20fc-458">**Time-out voor inactiviteit**</span><span class="sxs-lookup"><span data-stu-id="b20fc-458">**Idle Timeout**</span></span> | <span data-ttu-id="b20fc-459">Minuten tookeep een TCP-verbinding openen</span><span class="sxs-lookup"><span data-stu-id="b20fc-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="b20fc-460">4</span><span class="sxs-lookup"><span data-stu-id="b20fc-460">4</span></span> |
   | <span data-ttu-id="b20fc-461">**Zwevend IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="b20fc-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="b20fc-462">Ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="b20fc-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="b20fc-463">Direct server return is ingesteld tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="b20fc-463">Direct server return is set during creation.</span></span> <span data-ttu-id="b20fc-464">Deze kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b20fc-464">It cannot be changed.</span></span>

1. <span data-ttu-id="b20fc-465">Klik op **OK** tooset Hallo load-balancingregels.</span><span class="sxs-lookup"><span data-stu-id="b20fc-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="b20fc-466"><a name="configure-listener"></a>Hallo-listener configureren</span><span class="sxs-lookup"><span data-stu-id="b20fc-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="b20fc-467">de volgende dingen toodo Hello is tooconfigure een beschikbaarheidsgroep-listener op Hallo failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="b20fc-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b20fc-468">Deze zelfstudie laat zien hoe toocreate één listener - met een ILB IP adres.</span><span class="sxs-lookup"><span data-stu-id="b20fc-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="b20fc-469">toocreate een of meer listeners met behulp van een of meer IP-adressen, Zie [Create Availability Group-listener en load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b20fc-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="b20fc-470">Set-listener-poort</span><span class="sxs-lookup"><span data-stu-id="b20fc-470">Set listener port</span></span>

<span data-ttu-id="b20fc-471">In SQL Server Management Studio ingesteld Hallo-listener-poort.</span><span class="sxs-lookup"><span data-stu-id="b20fc-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="b20fc-472">Start SQL Server Management Studio en maak verbinding toohello primaire replica.</span><span class="sxs-lookup"><span data-stu-id="b20fc-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="b20fc-473">Navigeer te**AlwaysOn hoge beschikbaarheid** | **beschikbaarheidsgroepen** | **beschikbaarheid Beschikbaarheidsgroeplisteners**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="b20fc-474">U ziet nu Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="b20fc-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="b20fc-475">Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="b20fc-476">In Hallo **poort** Geef Hallo-poortnummer voor de beschikbaarheidsgroep-listener Hallo via Hallo $EndpointPort u eerder hebt gebruikt (1433 was Hallo standaard), klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b20fc-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="b20fc-477">U hebt nu een SQL Server-beschikbaarheidsgroep in Azure virtuele machines die worden uitgevoerd in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b20fc-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="b20fc-478">Test verbinding toolistener</span><span class="sxs-lookup"><span data-stu-id="b20fc-478">Test connection toolistener</span></span>

<span data-ttu-id="b20fc-479">tootest hello verbinding:</span><span class="sxs-lookup"><span data-stu-id="b20fc-479">tootest hello connection:</span></span>

1. <span data-ttu-id="b20fc-480">RDP-tooa SQL-Server die zich in Hallo hetzelfde virtuele netwerk, maar niet eigen Hallo replica.</span><span class="sxs-lookup"><span data-stu-id="b20fc-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="b20fc-481">U kunt andere SQL-Server in de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b20fc-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="b20fc-482">Gebruik **sqlcmd** hulpprogramma tootest Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="b20fc-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="b20fc-483">Bijvoorbeeld Hallo script volgen stelt een **sqlcmd** verbinding toohello primaire replica via het Hallo-listener met de Windows-verificatie:</span><span class="sxs-lookup"><span data-stu-id="b20fc-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="b20fc-484">Als het Hallo-listener poort wordt gebruikt door een andere waarde dan Hallo standaard poort (1433), Hallo-poort in de verbindingsreeks Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="b20fc-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="b20fc-485">Bijvoorbeeld: hello volgende sqlcmd-opdracht verbindt tooa listener op poort 1435:</span><span class="sxs-lookup"><span data-stu-id="b20fc-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="b20fc-486">Hallo SQLCMD-verbinding verbinding automatisch toowhichever exemplaar van SQL Server-hosts Hallo primaire replica.</span><span class="sxs-lookup"><span data-stu-id="b20fc-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="b20fc-487">Zorg ervoor dat Hallo poort die u opgeeft geopend op Hallo firewall beide SQL-servers is.</span><span class="sxs-lookup"><span data-stu-id="b20fc-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="b20fc-488">Beide servers vereisen een inkomende regel voor Hallo TCP-poort die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b20fc-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="b20fc-489">Zie voor meer informatie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="b20fc-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="b20fc-490">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b20fc-490">Next steps</span></span>

- <span data-ttu-id="b20fc-491">[Toevoegen van een IP-adres tooa load balancer voor een tweede beschikbaarheidsgroep](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="b20fc-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
