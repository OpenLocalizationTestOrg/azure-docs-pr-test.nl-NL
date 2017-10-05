---
title: SQL Server-beschikbaarheidsgroepen - virtuele Machines in Azure - zelfstudie | Microsoft Docs
description: Deze zelfstudie laat zien hoe een SQL Server altijd op beschikbaarheidsgroep maken op Azure Virtual Machines.
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
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="cedea-103">Configureren AlwaysOn-beschikbaarheidsgroep in Azure VM handmatig</span><span class="sxs-lookup"><span data-stu-id="cedea-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="cedea-104">Deze zelfstudie laat zien hoe een SQL Server altijd op beschikbaarheidsgroep maken op Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="cedea-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="cedea-105">De volledige zelfstudie maakt een beschikbaarheidsgroep met een databasereplica op twee SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="cedea-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="cedea-106">**Tijd schatting**: duurt ongeveer 30 minuten voltooid als aan de vereisten is voldaan.</span><span class="sxs-lookup"><span data-stu-id="cedea-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="cedea-107">Het diagram ziet u wat u in de zelfstudie bouwen.</span><span class="sxs-lookup"><span data-stu-id="cedea-107">The diagram illustrates what you build in the tutorial.</span></span>

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="cedea-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cedea-109">Prerequisites</span></span>

<span data-ttu-id="cedea-110">De zelfstudie wordt ervan uitgegaan dat u basiskennis van SQL Server altijd op beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="cedea-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="cedea-111">Als u meer informatie, Zie [overzicht van AlwaysOn-beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="cedea-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="cedea-112">De volgende tabel bevat de vereisten die u nodig hebt voltooid voordat u deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="cedea-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="cedea-113">Vereiste</span><span class="sxs-lookup"><span data-stu-id="cedea-113">Requirement</span></span> |<span data-ttu-id="cedea-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cedea-114">Description</span></span> |
|----- |----- |----- |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="cedea-116">Twee SQL-Servers</span><span class="sxs-lookup"><span data-stu-id="cedea-116">Two SQL Servers</span></span> | <span data-ttu-id="cedea-117">-In een Azure beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="cedea-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="cedea-118">-In één domein</span><span class="sxs-lookup"><span data-stu-id="cedea-118">- In a single domain</span></span> <br/> <span data-ttu-id="cedea-119">-Met de functie Failover Clustering is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="cedea-119">- With Failover Clustering feature installed</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="cedea-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="cedea-121">Windows Server</span></span> | <span data-ttu-id="cedea-122">Bestandsshare voor cluster-witness</span><span class="sxs-lookup"><span data-stu-id="cedea-122">File share for cluster witness</span></span> |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="cedea-124">SQL Server-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="cedea-124">SQL Server service account</span></span> | <span data-ttu-id="cedea-125">Domeinaccount</span><span class="sxs-lookup"><span data-stu-id="cedea-125">Domain account</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="cedea-127">SQL Server Agent-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="cedea-127">SQL Server Agent service account</span></span> | <span data-ttu-id="cedea-128">Domeinaccount</span><span class="sxs-lookup"><span data-stu-id="cedea-128">Domain account</span></span> |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="cedea-130">Firewall-poorten</span><span class="sxs-lookup"><span data-stu-id="cedea-130">Firewall ports open</span></span> | <span data-ttu-id="cedea-131">-SQL Server: **1433** voor het standaardexemplaar</span><span class="sxs-lookup"><span data-stu-id="cedea-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="cedea-132">-Eindpunt voor databasespiegeling: **5022** of een beschikbare poort</span><span class="sxs-lookup"><span data-stu-id="cedea-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="cedea-133">-Azure load balancer-test: **59999** of een beschikbare poort</span><span class="sxs-lookup"><span data-stu-id="cedea-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="cedea-135">Toevoegen van de functie Failoverclustering</span><span class="sxs-lookup"><span data-stu-id="cedea-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="cedea-136">Deze functie nodig hebben voor zowel SQL-Servers</span><span class="sxs-lookup"><span data-stu-id="cedea-136">Both SQL Servers require this feature</span></span> |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="cedea-138">Installatieaccount van het domein</span><span class="sxs-lookup"><span data-stu-id="cedea-138">Installation domain account</span></span> | <span data-ttu-id="cedea-139">-Lokale beheerder zijn op elke SQL Server</span><span class="sxs-lookup"><span data-stu-id="cedea-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="cedea-140">-Lid is van SQL Server vaste serverrol sysadmin voor elk exemplaar van SQL Server</span><span class="sxs-lookup"><span data-stu-id="cedea-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="cedea-141">Voordat u de zelfstudie begint, moet u [voldoen aan vereisten voor het maken van AlwaysOn-beschikbaarheidsgroepen in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="cedea-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="cedea-142">Als deze vereiste onderdelen zijn al voltooid, kunt u springen naar [Cluster maken](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="cedea-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="cedea-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Het cluster maken</span><span class="sxs-lookup"><span data-stu-id="cedea-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="cedea-144">Nadat de vereiste onderdelen zijn voltooid, wordt de eerste stap is om een Windows Server-failovercluster met twee SQL-servers en een witness-server te maken.</span><span class="sxs-lookup"><span data-stu-id="cedea-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="cedea-145">RDP naar de eerste SQL-Server met behulp van een domeinaccount met een Administrator op SQL-Servers en de witness-server.</span><span class="sxs-lookup"><span data-stu-id="cedea-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="cedea-146">Als u hebt gevolgd de [vereisten document](virtual-machines-windows-portal-sql-availability-group-prereq.md), u hebt gemaakt met een account met de naam **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="cedea-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="cedea-147">Dit account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cedea-147">Use this account.</span></span>

2. <span data-ttu-id="cedea-148">In de **Serverbeheer** dashboard, selecteer **extra**, en klik vervolgens op **Failoverclusterbeheer**.</span><span class="sxs-lookup"><span data-stu-id="cedea-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="cedea-149">In het linkerdeelvenster met de rechtermuisknop op **Failoverclusterbeheer**, en klik vervolgens op **maken van een Cluster**.</span><span class="sxs-lookup"><span data-stu-id="cedea-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="cedea-150">![Cluster maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="cedea-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="cedea-151">Maak een cluster met één knooppunt door door de pagina's met de instellingen in de volgende tabel in de Wizard Cluster maken:</span><span class="sxs-lookup"><span data-stu-id="cedea-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="cedea-152">Pagina</span><span class="sxs-lookup"><span data-stu-id="cedea-152">Page</span></span> | <span data-ttu-id="cedea-153">Instellingen</span><span class="sxs-lookup"><span data-stu-id="cedea-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="cedea-154">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="cedea-154">Before You Begin</span></span> |<span data-ttu-id="cedea-155">Standaardinstellingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="cedea-155">Use defaults</span></span> |
   | <span data-ttu-id="cedea-156">Servers selecteren</span><span class="sxs-lookup"><span data-stu-id="cedea-156">Select Servers</span></span> |<span data-ttu-id="cedea-157">Typ de naam van de eerste SQL Server in **Enter servernaam** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="cedea-158">Van validatiewaarschuwing</span><span class="sxs-lookup"><span data-stu-id="cedea-158">Validation Warning</span></span> |<span data-ttu-id="cedea-159">Selecteer **nr. ik geen ondersteuning van Microsoft nodig hebt voor dit cluster, en daarom niet wilt de validatietests uit te voeren. Als ik op Volgende klikt, doorgaan met het maken van het cluster**.</span><span class="sxs-lookup"><span data-stu-id="cedea-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="cedea-160">Toegangspunt voor beheer van het Cluster</span><span class="sxs-lookup"><span data-stu-id="cedea-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="cedea-161">Typ de naam van een cluster, zoals **SQLAGCluster1** in **clusternaam**.</span><span class="sxs-lookup"><span data-stu-id="cedea-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="cedea-162">Bevestiging</span><span class="sxs-lookup"><span data-stu-id="cedea-162">Confirmation</span></span> |<span data-ttu-id="cedea-163">Gebruik de standaardwaarden tenzij u van opslagruimten gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="cedea-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="cedea-164">Zie de opmerking onder deze tabel.</span><span class="sxs-lookup"><span data-stu-id="cedea-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="cedea-165">De cluster-IP-adres instellen</span><span class="sxs-lookup"><span data-stu-id="cedea-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="cedea-166">In **Failoverclusterbeheer**, schuif omlaag naar **Clusterkernresources** en vouwt u de clusterdetails van de.</span><span class="sxs-lookup"><span data-stu-id="cedea-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="cedea-167">Ziet u zowel de **naam** en de **IP-adres** bronnen in de **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="cedea-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="cedea-168">De bron van het IP-adres kan niet online worden gebracht omdat het cluster is toegewezen aan hetzelfde IP-adres als de machine zelf, daarom is een dubbel adres.</span><span class="sxs-lookup"><span data-stu-id="cedea-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="cedea-169">Met de rechtermuisknop op de mislukte **IP-adres** bron en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Eigenschappen van cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="cedea-171">Selecteer **statisch IP-adres** en geef een beschikbaar adres van waar de SQL-Server zich in het tekstvak voor het bevindt subnet.</span><span class="sxs-lookup"><span data-stu-id="cedea-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="cedea-172">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedea-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="cedea-173">In de **Clusterkernresources** sectie, met de rechtermuisknop op de clusternaam van het en klik op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="cedea-174">Vervolgens wacht u totdat beide bronnen online zijn.</span><span class="sxs-lookup"><span data-stu-id="cedea-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="cedea-175">Wanneer de clusterbron met de naam van online wordt gezet, de DC-server wordt bijgewerkt met een nieuw AD-account.</span><span class="sxs-lookup"><span data-stu-id="cedea-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="cedea-176">Gebruik deze AD-account later uit te voeren de beschikbaarheidsgroep geclusterde service.</span><span class="sxs-lookup"><span data-stu-id="cedea-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="cedea-177"><a name="addNode"></a>De SQL-Server toevoegen aan cluster</span><span class="sxs-lookup"><span data-stu-id="cedea-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="cedea-178">De SQL-Server toevoegen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="cedea-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="cedea-179">In de boomstructuur van de browser, met de rechtermuisknop op het cluster en klikt u op **knooppunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Knooppunt toevoegen aan het Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="cedea-181">In de **Wizard knooppunt toevoegen**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="cedea-182">In de **Servers selecteren** pagina, de tweede SQL-Server toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cedea-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="cedea-183">Typ de servernaam in **Enter servernaam** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="cedea-184">Wanneer u klaar bent, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="cedea-185">In de **Validation Warning** pagina, klikt u op **Nee** (in een productiescenario u moet de validatietests uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="cedea-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="cedea-186">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="cedea-187">In de **bevestiging** pagina als u gebruikmaakt van opslagruimten, schakelt u het selectievakje **alle in aanmerking komende opslag toevoegen aan het cluster.**</span><span class="sxs-lookup"><span data-stu-id="cedea-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Knooppunt bevestiging toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="cedea-189">Als u met behulp van opslagruimten en niet doen schakelt **alle in aanmerking komende opslag toevoegen aan het cluster**, Windows wordt losgekoppeld van de virtuele schijven tijdens het clusterproces.</span><span class="sxs-lookup"><span data-stu-id="cedea-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="cedea-190">Als gevolg hiervan worden niet weergegeven in Schijfbeheer of Explorer totdat de opslagruimten zijn verwijderd uit het cluster en opnieuw gekoppeld met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cedea-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="cedea-191">Opslagruimten gegroepeerd op meerdere schijven in aan opslaggroepen.</span><span class="sxs-lookup"><span data-stu-id="cedea-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="cedea-192">Zie voor meer informatie [opslagruimten](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="cedea-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="cedea-193">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-193">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-194">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cedea-194">Click **Finish**.</span></span>

   <span data-ttu-id="cedea-195">Failover Cluster Manager blijkt dat het cluster een nieuw knooppunt is en wordt weergegeven in de **knooppunten** container.</span><span class="sxs-lookup"><span data-stu-id="cedea-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="cedea-196">Meld u af bij van de extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="cedea-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="cedea-197">Toevoegen van een clusterquorum-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="cedea-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="cedea-198">In dit voorbeeld gebruikt de Windows-cluster een bestandsshare te maken van een clusterquorum.</span><span class="sxs-lookup"><span data-stu-id="cedea-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="cedea-199">Deze zelfstudie maakt gebruik van een knooppunt en bestandssharemeerderheid quorum.</span><span class="sxs-lookup"><span data-stu-id="cedea-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="cedea-200">Zie voor meer informatie [Quorumconfiguraties in een failovercluster](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="cedea-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="cedea-201">Verbinding maken met de share witness lid bestandsserver met een extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="cedea-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="cedea-202">Op **Serverbeheer**, klikt u op **extra**.</span><span class="sxs-lookup"><span data-stu-id="cedea-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="cedea-203">Open **Computerbeheer**.</span><span class="sxs-lookup"><span data-stu-id="cedea-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="cedea-204">Klik op **gedeelde mappen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="cedea-205">Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="cedea-207">Gebruik **Wizard gedeelde map maken** voor het maken van een share.</span><span class="sxs-lookup"><span data-stu-id="cedea-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="cedea-208">Op **mappad**, klikt u op **Bladeren** en niet vinden of een pad voor de gedeelde map maken.</span><span class="sxs-lookup"><span data-stu-id="cedea-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="cedea-209">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-209">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-210">In **naam, beschrijving en instellingen** Controleer of de sharenaam en het pad.</span><span class="sxs-lookup"><span data-stu-id="cedea-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="cedea-211">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-211">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-212">Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="cedea-213">Klik op **aangepaste...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="cedea-214">Op **machtigingen aanpassen**, klikt u op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="cedea-215">Zorg ervoor dat het account dat wordt gebruikt voor het maken van het cluster volledig beheer heeft.</span><span class="sxs-lookup"><span data-stu-id="cedea-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="cedea-217">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedea-217">Click **OK**.</span></span>

1. <span data-ttu-id="cedea-218">In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cedea-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="cedea-219">Klik op **voltooien** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="cedea-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="cedea-220">Meld u af bij de server</span><span class="sxs-lookup"><span data-stu-id="cedea-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="cedea-221">Clusterquorum configureren</span><span class="sxs-lookup"><span data-stu-id="cedea-221">Configure cluster quorum</span></span>

<span data-ttu-id="cedea-222">Vervolgens stelt u het clusterquorum.</span><span class="sxs-lookup"><span data-stu-id="cedea-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="cedea-223">Verbinding maken met het eerste clusterknooppunt met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="cedea-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="cedea-224">In **Failoverclusterbeheer**, met de rechtermuisknop op het cluster, wijs **meer acties**, en klik op **Clusterquoruminstellingen configureren...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="cedea-226">In **Wizard clusterquorum configureren**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="cedea-227">In **optie voor quorumconfiguratie**, kies **selecteert u de quorumwitness**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="cedea-228">Op **Quorumwitness selecteren**, klikt u op **een bestandssharewitness configureren**.</span><span class="sxs-lookup"><span data-stu-id="cedea-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="cedea-229">Windows Server 2016 biedt ondersteuning voor een cloud-witness.</span><span class="sxs-lookup"><span data-stu-id="cedea-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="cedea-230">Als u dit soort witness kiest, hoeft u niet een bestand witness delen.</span><span class="sxs-lookup"><span data-stu-id="cedea-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="cedea-231">Zie voor meer informatie [een witness cloud voor een failover-Cluster implementeren](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="cedea-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="cedea-232">Deze zelfstudie maakt gebruik van een bestandssharewitness wordt ondersteund door eerdere besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="cedea-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="cedea-233">Op **bestandssharewitness configureren**, typt u het pad voor de share die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cedea-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="cedea-234">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-234">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-235">Controleer de instellingen op **bevestiging**.</span><span class="sxs-lookup"><span data-stu-id="cedea-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="cedea-236">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-236">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-237">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cedea-237">Click **Finish**.</span></span>

<span data-ttu-id="cedea-238">De clusterkernresources zijn geconfigureerd met een bestandssharewitness.</span><span class="sxs-lookup"><span data-stu-id="cedea-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="cedea-239">Beschikbaarheidsgroepen inschakelen</span><span class="sxs-lookup"><span data-stu-id="cedea-239">Enable Availability Groups</span></span>

<span data-ttu-id="cedea-240">Schakel vervolgens de **AlwaysOn Availability Groups** functie.</span><span class="sxs-lookup"><span data-stu-id="cedea-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="cedea-241">Voer deze stappen uit op beide SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="cedea-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="cedea-242">Van de **Start** scherm, starten **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="cedea-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="cedea-243">Klik in de structuur van de browser op **SQL Server-Services**, klik met de rechtermuisknop op de **SQL Server (MSSQLSERVER)** service en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="cedea-244">Klik op de **AlwaysOn hoge beschikbaarheid** tabblad en selecteer vervolgens **Schakel AlwaysOn Availability Groups**als volgt:</span><span class="sxs-lookup"><span data-stu-id="cedea-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn-beschikbaarheidsgroepen inschakelen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="cedea-246">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-246">Click **Apply**.</span></span> <span data-ttu-id="cedea-247">Klik op **OK** in het pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="cedea-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="cedea-248">De SQL Server-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="cedea-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="cedea-249">Herhaal deze stappen op de SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="cedea-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="cedea-250">Een database maken op de eerste SQL-Server</span><span class="sxs-lookup"><span data-stu-id="cedea-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="cedea-251">Start het RDP-bestand naar de eerste SQL-Server met een domeinaccount dat lid is van de vaste serverrol sysadmin.</span><span class="sxs-lookup"><span data-stu-id="cedea-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="cedea-252">Open SQL Server Management Studio en maak verbinding met de eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="cedea-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="cedea-253">In **Objectverkenner**, met de rechtermuisknop op **Databases** en klik op **nieuwe Database**.</span><span class="sxs-lookup"><span data-stu-id="cedea-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="cedea-254">In **databasenaam**, type **MyDB1**, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedea-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="cedea-255"><a name="backupshare"></a>Maak een back-share</span><span class="sxs-lookup"><span data-stu-id="cedea-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="cedea-256">Op de eerste SQL-Server in **Serverbeheer**, klikt u op **extra**.</span><span class="sxs-lookup"><span data-stu-id="cedea-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="cedea-257">Open **Computerbeheer**.</span><span class="sxs-lookup"><span data-stu-id="cedea-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="cedea-258">Klik op **gedeelde mappen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="cedea-259">Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="cedea-261">Gebruik **Wizard gedeelde map maken** voor het maken van een share.</span><span class="sxs-lookup"><span data-stu-id="cedea-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="cedea-262">Op **mappad**, klikt u op **Bladeren** en niet vinden of een pad voor de database een back-gedeelde map maken.</span><span class="sxs-lookup"><span data-stu-id="cedea-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="cedea-263">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-263">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-264">In **naam, beschrijving en instellingen** Controleer of de sharenaam en het pad.</span><span class="sxs-lookup"><span data-stu-id="cedea-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="cedea-265">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-265">Click **Next**.</span></span>

1. <span data-ttu-id="cedea-266">Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="cedea-267">Klik op **aangepaste...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="cedea-268">Op **machtigingen aanpassen**, klikt u op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="cedea-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="cedea-269">Zorg ervoor dat de SQL Server en SQL Server Agent-service-accounts voor beide servers volledig beheer hebben.</span><span class="sxs-lookup"><span data-stu-id="cedea-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="cedea-271">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedea-271">Click **OK**.</span></span>

1. <span data-ttu-id="cedea-272">In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="cedea-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="cedea-273">Klik op **voltooien** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="cedea-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="cedea-274">Een volledige back-up van de database uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cedea-274">Take a full backup of the database</span></span>

<span data-ttu-id="cedea-275">U moet back-up van de nieuwe database in de logboekketen initialiseren.</span><span class="sxs-lookup"><span data-stu-id="cedea-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="cedea-276">Als u een back-up van de nieuwe database pas van kracht worden, kan deze kan niet worden opgenomen in een beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="cedea-277">In **Objectverkenner**, met de rechtermuisknop op de database, wijs **taken...** , klikt u op **Back-Up**.</span><span class="sxs-lookup"><span data-stu-id="cedea-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="cedea-278">Klik op **OK** te laten een volledige back-up op de standaardlocatie van de back-up.</span><span class="sxs-lookup"><span data-stu-id="cedea-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="cedea-279">Maken van de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-279">Create the Availability Group</span></span>
<span data-ttu-id="cedea-280">U bent nu klaar om te configureren van een beschikbaarheidsgroep met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cedea-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="cedea-281">Een database maken op de eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="cedea-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="cedea-282">Neem een volledige back-up en de een transactielogboek van de database</span><span class="sxs-lookup"><span data-stu-id="cedea-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="cedea-283">Herstellen van de volledige en logboekback-ups naar het tweede SQL Server met de **NORECOVERY** optie</span><span class="sxs-lookup"><span data-stu-id="cedea-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="cedea-284">Maken van de beschikbaarheidsgroep (**AG1**) met synchrone doorvoer en automatische failover leesbare secundaire replica's</span><span class="sxs-lookup"><span data-stu-id="cedea-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="cedea-285">De beschikbaarheidsgroep maken:</span><span class="sxs-lookup"><span data-stu-id="cedea-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="cedea-286">Op de extern-bureaubladsessie naar de eerste SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="cedea-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="cedea-287">In **Objectverkenner** SSMS, met de rechtermuisknop op **AlwaysOn hoge beschikbaarheid** en klik op **nieuwe Wizard beschikbaarheidsgroep**.</span><span class="sxs-lookup"><span data-stu-id="cedea-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![De Wizard Nieuwe beschikbaarheidsgroep starten](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="cedea-289">In de **inleiding** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="cedea-290">In de **naam van de beschikbaarheidsgroep opgeven** pagina, typ een naam voor de beschikbaarheidsgroep, bijvoorbeeld **AG1**in **naam van de beschikbaarheidsgroep**.</span><span class="sxs-lookup"><span data-stu-id="cedea-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="cedea-291">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-291">Click **Next**.</span></span>

    ![Wizard Nieuwe AG AG-naam opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="cedea-293">In de **Databases selecteren** pagina, selecteer uw database en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="cedea-294">De database voldoet aan de vereisten voor een beschikbaarheidsgroep, omdat u ten minste één volledige back-up hebt uitgevoerd op de beoogde primaire replica.</span><span class="sxs-lookup"><span data-stu-id="cedea-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![Wizard Nieuwe AG Databases selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="cedea-296">In de **replica's opgeven** pagina, klikt u op **Replica toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Wizard Nieuwe AG replica's opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="cedea-298">De **verbinding maken met Server** dialoogvenster verschijnt.</span><span class="sxs-lookup"><span data-stu-id="cedea-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="cedea-299">Typ de naam van de tweede server in **servernaam**.</span><span class="sxs-lookup"><span data-stu-id="cedea-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="cedea-300">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="cedea-300">Click **Connect**.</span></span>

   <span data-ttu-id="cedea-301">Terug in de **replica's opgeven** pagina u ziet nu de tweede server die worden vermeld in **Beschikbaarheidsreplica**.</span><span class="sxs-lookup"><span data-stu-id="cedea-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="cedea-302">De replica's als volgt configureren.</span><span class="sxs-lookup"><span data-stu-id="cedea-302">Configure the replicas as follows.</span></span>

   ![Wizard Nieuwe AG replica's (voltooid) opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="cedea-304">Klik op **eindpunten** om te zien van het eindpunt voor databasespiegeling voor deze beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="cedea-305">Gebruik dezelfde poort die u hebt gebruikt bij het instellen van de [firewallregel voor databasespiegeling eindpunten](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="cedea-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="cedea-307">In de **eerste gegevenssynchronisatie selecteren** pagina **volledige** en geef een gedeelde netwerklocatie.</span><span class="sxs-lookup"><span data-stu-id="cedea-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="cedea-308">Gebruik voor de locatie, de [back-upshare die u hebt gemaakt](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="cedea-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="cedea-309">In het voorbeeld was, **\\\\\<eerste SQL-Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="cedea-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="cedea-310">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="cedea-311">Volledige synchronisatie duurt een volledige back-up van de database op het eerste exemplaar van SQL Server en te herstellen op de tweede instantie.</span><span class="sxs-lookup"><span data-stu-id="cedea-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="cedea-312">Voor grote databases worden volledige synchronisatie wordt niet aanbevolen omdat het kan lang duren.</span><span class="sxs-lookup"><span data-stu-id="cedea-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="cedea-313">U kunt deze tijd verkorten door handmatig een back-up van de database maken en terugzetten met `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="cedea-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="cedea-314">Als de database al is teruggezet met `NO RECOVERY` op de tweede SQL Server voordat u de beschikbaarheidsgroep configureert, kiest u **alleen deelnemen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="cedea-315">Als u wilt de back-up uitvoeren na het configureren van de beschikbaarheidsgroep, kiest u **eerste gegevenssynchronisatie overslaan**.</span><span class="sxs-lookup"><span data-stu-id="cedea-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="cedea-317">In de **validatie** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="cedea-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="cedea-318">Deze pagina moet er ongeveer als de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="cedea-318">This page should look similar to the following image:</span></span>

    ![Wizard Nieuwe AG, validatie](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="cedea-320">Er is een waarschuwing voor de listenerconfiguratie van de omdat u een beschikbaarheidsgroep-listener niet hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cedea-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="cedea-321">U kunt deze waarschuwing negeren omdat op virtuele machines in Azure maakt u de listener na het maken van de Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="cedea-322">In de **samenvatting** pagina, klikt u op **voltooien**, wacht u totdat de wizard configureert u de nieuwe beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="cedea-323">In de **voortgang** pagina, klikt u op **meer details** om de voortgang van de gedetailleerde weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cedea-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="cedea-324">Zodra de wizard voltooid is, controleert de **resultaten** pagina om te controleren of de beschikbaarheidsgroep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cedea-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![Wizard Nieuwe AG resulteert](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="cedea-326">Klik op **sluiten** de wizard wilt afsluiten.</span><span class="sxs-lookup"><span data-stu-id="cedea-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="cedea-327">Controleer de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-327">Check the Availability Group</span></span>

1. <span data-ttu-id="cedea-328">In **Objectverkenner**, vouw **AlwaysOn hoge beschikbaarheid**, vouw vervolgens **beschikbaarheidsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="cedea-329">U ziet nu de nieuwe beschikbaarheidsgroep in deze container.</span><span class="sxs-lookup"><span data-stu-id="cedea-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="cedea-330">Met de rechtermuisknop op de beschikbaarheidsgroep en klik op **Dashboard weergeven**.</span><span class="sxs-lookup"><span data-stu-id="cedea-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![AG-Dashboard weergeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="cedea-332">Uw **AlwaysOn Dashboard** ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="cedea-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![AG-Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="cedea-334">U ziet de replica's, de failover-modus van elke replica en de synchronisatiestatus.</span><span class="sxs-lookup"><span data-stu-id="cedea-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="cedea-335">In **Failoverclusterbeheer**, klikt u op het cluster.</span><span class="sxs-lookup"><span data-stu-id="cedea-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="cedea-336">Selecteer **rollen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-336">Select **Roles**.</span></span> <span data-ttu-id="cedea-337">De naam van de beschikbaarheidsgroep die u gebruikt, is een rol op het cluster.</span><span class="sxs-lookup"><span data-stu-id="cedea-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="cedea-338">Deze beschikbaarheidsgroep heeft geen een IP-adres voor clientverbindingen, omdat u niet een listener hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cedea-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="cedea-339">U configureert de listener nadat u een Azure load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="cedea-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="cedea-341">Probeer geen failover van de beschikbaarheidsgroep vanuit Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="cedea-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="cedea-342">Alle failover-bewerkingen moeten worden uitgevoerd vanuit **AlwaysOn Dashboard** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="cedea-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="cedea-343">Zie voor meer informatie [beperkingen op met behulp van de Failover-clusterbeheer met beschikbaarheidsgroepen](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="cedea-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="cedea-344">U hebt op dit moment een beschikbaarheidsgroep met replica's op twee exemplaren van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cedea-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="cedea-345">U kunt de beschikbaarheidsgroep verplaatsen tussen exemplaren.</span><span class="sxs-lookup"><span data-stu-id="cedea-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="cedea-346">U kan geen verbinding met de beschikbaarheidsgroep nog omdat u niet over een listener.</span><span class="sxs-lookup"><span data-stu-id="cedea-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="cedea-347">In Azure virtuele machines moet de listener voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="cedea-348">De volgende stap is het maken van de load balancer in Azure.</span><span class="sxs-lookup"><span data-stu-id="cedea-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="cedea-349">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="cedea-349">Create an Azure load balancer</span></span>

<span data-ttu-id="cedea-350">Op virtuele machines in Azure vereist een SQL Server-beschikbaarheidsgroep een load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="cedea-351">De load balancer bevat het IP-adres voor de beschikbaarheidsgroep-listener.</span><span class="sxs-lookup"><span data-stu-id="cedea-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="cedea-352">Deze sectie bevat een overzicht van de load balancer maken in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cedea-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="cedea-353">In de Azure portal, gaat u naar de resourcegroep waar uw SQL-Servers zijn en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="cedea-354">Zoeken naar **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="cedea-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="cedea-355">Kies de load balancer gepubliceerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cedea-355">Choose the load balancer published by Microsoft.</span></span>

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="cedea-357">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cedea-357">Click **Create**.</span></span>
3. <span data-ttu-id="cedea-358">Configureer de volgende parameters voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="cedea-359">Instelling</span><span class="sxs-lookup"><span data-stu-id="cedea-359">Setting</span></span> | <span data-ttu-id="cedea-360">Veld</span><span class="sxs-lookup"><span data-stu-id="cedea-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="cedea-361">**Naam**</span><span class="sxs-lookup"><span data-stu-id="cedea-361">**Name**</span></span> |<span data-ttu-id="cedea-362">Gebruik een naam in voor de load balancer, zoals **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="cedea-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="cedea-363">**Type**</span><span class="sxs-lookup"><span data-stu-id="cedea-363">**Type**</span></span> |<span data-ttu-id="cedea-364">interne</span><span class="sxs-lookup"><span data-stu-id="cedea-364">Internal</span></span> |
   | <span data-ttu-id="cedea-365">**Virtueel netwerk**</span><span class="sxs-lookup"><span data-stu-id="cedea-365">**Virtual network**</span></span> |<span data-ttu-id="cedea-366">Gebruik de naam van de virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cedea-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="cedea-367">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="cedea-367">**Subnet**</span></span> |<span data-ttu-id="cedea-368">De naam van het subnet dat de virtuele machine is in gebruik.</span><span class="sxs-lookup"><span data-stu-id="cedea-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="cedea-369">**IP-adrestoewijzing**</span><span class="sxs-lookup"><span data-stu-id="cedea-369">**IP address assignment**</span></span> |<span data-ttu-id="cedea-370">Statisch</span><span class="sxs-lookup"><span data-stu-id="cedea-370">Static</span></span> |
   | <span data-ttu-id="cedea-371">**IP-adres**</span><span class="sxs-lookup"><span data-stu-id="cedea-371">**IP address**</span></span> |<span data-ttu-id="cedea-372">Gebruik een beschikbaar adres van subnet.</span><span class="sxs-lookup"><span data-stu-id="cedea-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="cedea-373">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="cedea-373">**Subscription**</span></span> |<span data-ttu-id="cedea-374">Gebruik hetzelfde abonnement als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cedea-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="cedea-375">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="cedea-375">**Location**</span></span> |<span data-ttu-id="cedea-376">Gebruik dezelfde locatie als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cedea-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="cedea-377">De Azure portal blade ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="cedea-377">The Azure portal blade should look like this:</span></span>

   ![Load Balancer maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="cedea-379">Klik op **maken**wilt maken van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="cedea-380">Voor het configureren van de load balancer, moet u een back-endpool een test maken en de load-balancingregels.</span><span class="sxs-lookup"><span data-stu-id="cedea-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="cedea-381">Voer deze in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cedea-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="cedea-382">Back-endpool toevoegen</span><span class="sxs-lookup"><span data-stu-id="cedea-382">Add backend pool</span></span>

1. <span data-ttu-id="cedea-383">Ga in de Azure-portal aan de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="cedea-384">Mogelijk moet u de weergave voor de zojuist gemaakte load balancer vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="cedea-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Load Balancer niet vinden in de resourcegroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="cedea-386">Klik op de load balancer, **back-endpools**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="cedea-387">De back-endpool als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="cedea-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="cedea-388">Instelling</span><span class="sxs-lookup"><span data-stu-id="cedea-388">Setting</span></span> | <span data-ttu-id="cedea-389">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cedea-389">Description</span></span> | <span data-ttu-id="cedea-390">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cedea-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="cedea-391">**Naam**</span><span class="sxs-lookup"><span data-stu-id="cedea-391">**Name**</span></span> | <span data-ttu-id="cedea-392">Typ een naam</span><span class="sxs-lookup"><span data-stu-id="cedea-392">Type a text name</span></span> | <span data-ttu-id="cedea-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="cedea-393">SQLLBBE</span></span>
   | <span data-ttu-id="cedea-394">**Gekoppeld aan**</span><span class="sxs-lookup"><span data-stu-id="cedea-394">**Associated to**</span></span> | <span data-ttu-id="cedea-395">Kies uit de lijst</span><span class="sxs-lookup"><span data-stu-id="cedea-395">Pick from list</span></span> | <span data-ttu-id="cedea-396">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="cedea-396">Availability set</span></span>
   | <span data-ttu-id="cedea-397">**Beschikbaarheidsset**</span><span class="sxs-lookup"><span data-stu-id="cedea-397">**Availability set**</span></span> | <span data-ttu-id="cedea-398">Gebruik een naam van de beschikbaarheidsset die uw SQL Server-VM's in</span><span class="sxs-lookup"><span data-stu-id="cedea-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="cedea-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="cedea-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="cedea-400">**Virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="cedea-400">**Virtual machines**</span></span> |<span data-ttu-id="cedea-401">De twee namen van de virtuele machine in Azure SQL-Server</span><span class="sxs-lookup"><span data-stu-id="cedea-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="cedea-402">SQL Server-0, SQL Server-1</span><span class="sxs-lookup"><span data-stu-id="cedea-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="cedea-403">Typ de naam voor de back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="cedea-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="cedea-404">Klik op **+ toevoegen van een virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="cedea-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="cedea-405">Kies dat de beschikbaarheidsset dat de SQL-Servers zijn voor de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="cedea-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="cedea-406">Voor virtuele machines zijn beide van de SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="cedea-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="cedea-407">De bestandsserver van de bestandsshare-witness niet opnemen.</span><span class="sxs-lookup"><span data-stu-id="cedea-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="cedea-408">Klik op **OK** om de back endpool te maken.</span><span class="sxs-lookup"><span data-stu-id="cedea-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="cedea-409">Instellen van de test</span><span class="sxs-lookup"><span data-stu-id="cedea-409">Set the probe</span></span>

1. <span data-ttu-id="cedea-410">Klik op de load balancer, **statuscontroles**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="cedea-411">De health test als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="cedea-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="cedea-412">Instelling</span><span class="sxs-lookup"><span data-stu-id="cedea-412">Setting</span></span> | <span data-ttu-id="cedea-413">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cedea-413">Description</span></span> | <span data-ttu-id="cedea-414">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cedea-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="cedea-415">**Naam**</span><span class="sxs-lookup"><span data-stu-id="cedea-415">**Name**</span></span> | <span data-ttu-id="cedea-416">Tekst</span><span class="sxs-lookup"><span data-stu-id="cedea-416">Text</span></span> | <span data-ttu-id="cedea-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="cedea-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="cedea-418">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="cedea-418">**Protocol**</span></span> | <span data-ttu-id="cedea-419">Kies TCP</span><span class="sxs-lookup"><span data-stu-id="cedea-419">Choose TCP</span></span> | <span data-ttu-id="cedea-420">TCP</span><span class="sxs-lookup"><span data-stu-id="cedea-420">TCP</span></span> |
   | <span data-ttu-id="cedea-421">**Poort**</span><span class="sxs-lookup"><span data-stu-id="cedea-421">**Port**</span></span> | <span data-ttu-id="cedea-422">Een niet-gebruikte poort</span><span class="sxs-lookup"><span data-stu-id="cedea-422">Any unused port</span></span> | <span data-ttu-id="cedea-423">59999</span><span class="sxs-lookup"><span data-stu-id="cedea-423">59999</span></span> |
   | <span data-ttu-id="cedea-424">**Interval**</span><span class="sxs-lookup"><span data-stu-id="cedea-424">**Interval**</span></span>  | <span data-ttu-id="cedea-425">De tijdsduur tussen testpogingen in seconden</span><span class="sxs-lookup"><span data-stu-id="cedea-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="cedea-426">5</span><span class="sxs-lookup"><span data-stu-id="cedea-426">5</span></span> |
   | <span data-ttu-id="cedea-427">**Drempelwaarde voor onjuiste status**</span><span class="sxs-lookup"><span data-stu-id="cedea-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="cedea-428">Het aantal opeenvolgende testfouten dat moet optreden voor een virtuele machine moet worden beschouwd als niet in orde</span><span class="sxs-lookup"><span data-stu-id="cedea-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="cedea-429">2</span><span class="sxs-lookup"><span data-stu-id="cedea-429">2</span></span> |

1. <span data-ttu-id="cedea-430">Klik op **OK** om in te stellen van de health-test.</span><span class="sxs-lookup"><span data-stu-id="cedea-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="cedea-431">De load-balancingregels instellen</span><span class="sxs-lookup"><span data-stu-id="cedea-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="cedea-432">Klik op de load balancer, **Taakverdelingsregels**, en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="cedea-433">De load-balancingregels als volgt instellen.</span><span class="sxs-lookup"><span data-stu-id="cedea-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="cedea-434">Instelling</span><span class="sxs-lookup"><span data-stu-id="cedea-434">Setting</span></span> | <span data-ttu-id="cedea-435">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cedea-435">Description</span></span> | <span data-ttu-id="cedea-436">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cedea-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="cedea-437">**Naam**</span><span class="sxs-lookup"><span data-stu-id="cedea-437">**Name**</span></span> | <span data-ttu-id="cedea-438">Tekst</span><span class="sxs-lookup"><span data-stu-id="cedea-438">Text</span></span> | <span data-ttu-id="cedea-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="cedea-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="cedea-440">**Frontend IP-adres**</span><span class="sxs-lookup"><span data-stu-id="cedea-440">**Frontend IP address**</span></span> | <span data-ttu-id="cedea-441">Kies een adres</span><span class="sxs-lookup"><span data-stu-id="cedea-441">Choose an address</span></span> |<span data-ttu-id="cedea-442">Gebruik het adres dat u hebt gemaakt tijdens het maken van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="cedea-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="cedea-443">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="cedea-443">**Protocol**</span></span> | <span data-ttu-id="cedea-444">Kies TCP</span><span class="sxs-lookup"><span data-stu-id="cedea-444">Choose TCP</span></span> |<span data-ttu-id="cedea-445">TCP</span><span class="sxs-lookup"><span data-stu-id="cedea-445">TCP</span></span> |
   | <span data-ttu-id="cedea-446">**Poort**</span><span class="sxs-lookup"><span data-stu-id="cedea-446">**Port**</span></span> | <span data-ttu-id="cedea-447">Gebruik de poort voor SQL Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="cedea-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="cedea-448">1433</span><span class="sxs-lookup"><span data-stu-id="cedea-448">1433</span></span> |
   | <span data-ttu-id="cedea-449">**Back-Endpoort**</span><span class="sxs-lookup"><span data-stu-id="cedea-449">**Backend Port**</span></span> | <span data-ttu-id="cedea-450">Dit veld wordt niet gebruikt wanneer zwevend IP is ingesteld voor direct server return</span><span class="sxs-lookup"><span data-stu-id="cedea-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="cedea-451">1433</span><span class="sxs-lookup"><span data-stu-id="cedea-451">1433</span></span> |
   | <span data-ttu-id="cedea-452">**Test**</span><span class="sxs-lookup"><span data-stu-id="cedea-452">**Probe**</span></span> |<span data-ttu-id="cedea-453">De naam die u hebt opgegeven voor de test</span><span class="sxs-lookup"><span data-stu-id="cedea-453">The name you specified for the probe</span></span> | <span data-ttu-id="cedea-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="cedea-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="cedea-455">**Sessiepersistentie**</span><span class="sxs-lookup"><span data-stu-id="cedea-455">**Session Persistence**</span></span> | <span data-ttu-id="cedea-456">Vervolgkeuzelijst</span><span class="sxs-lookup"><span data-stu-id="cedea-456">Drop down list</span></span> | <span data-ttu-id="cedea-457">**Geen**</span><span class="sxs-lookup"><span data-stu-id="cedea-457">**None**</span></span> |
   | <span data-ttu-id="cedea-458">**Time-out voor inactiviteit**</span><span class="sxs-lookup"><span data-stu-id="cedea-458">**Idle Timeout**</span></span> | <span data-ttu-id="cedea-459">Minuten geopend te houden die een TCP-verbinding</span><span class="sxs-lookup"><span data-stu-id="cedea-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="cedea-460">4</span><span class="sxs-lookup"><span data-stu-id="cedea-460">4</span></span> |
   | <span data-ttu-id="cedea-461">**Zwevend IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="cedea-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="cedea-462">Ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="cedea-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="cedea-463">Direct server return is ingesteld tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="cedea-463">Direct server return is set during creation.</span></span> <span data-ttu-id="cedea-464">Deze kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="cedea-464">It cannot be changed.</span></span>

1. <span data-ttu-id="cedea-465">Klik op **OK** om in te stellen van de load-balancingregels.</span><span class="sxs-lookup"><span data-stu-id="cedea-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="cedea-466"><a name="configure-listener"></a>De listener configureren</span><span class="sxs-lookup"><span data-stu-id="cedea-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="cedea-467">De volgende wat te doen is voor het configureren van een beschikbaarheidsgroep-listener op het failovercluster.</span><span class="sxs-lookup"><span data-stu-id="cedea-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cedea-468">Deze zelfstudie laat zien hoe u een één listener - maakt met een ILB IP-adres.</span><span class="sxs-lookup"><span data-stu-id="cedea-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="cedea-469">Zie het maken van een of meer listeners met behulp van een of meer IP-adressen [Create Availability Group-listener en load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cedea-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="cedea-470">Set-listener-poort</span><span class="sxs-lookup"><span data-stu-id="cedea-470">Set listener port</span></span>

<span data-ttu-id="cedea-471">Stel de listener-poort in SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="cedea-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="cedea-472">Start SQL Server Management Studio en maak verbinding met de primaire replica.</span><span class="sxs-lookup"><span data-stu-id="cedea-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="cedea-473">Navigeer naar **AlwaysOn hoge beschikbaarheid** | **beschikbaarheidsgroepen** | **beschikbaarheidsgroep-Listeners**.</span><span class="sxs-lookup"><span data-stu-id="cedea-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="cedea-474">U ziet nu de naam van de listener die u hebt gemaakt in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="cedea-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="cedea-475">Met de rechtermuisknop op de naam van de listener en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="cedea-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="cedea-476">In de **poort** vak het poortnummer opgeven voor de beschikbaarheidsgroep-listener met behulp van de $EndpointPort u eerder hebt gebruikt (1433 is de standaardinstelling), klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedea-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="cedea-477">U hebt nu een SQL Server-beschikbaarheidsgroep in Azure virtuele machines die worden uitgevoerd in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cedea-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="cedea-478">De testverbinding met listener</span><span class="sxs-lookup"><span data-stu-id="cedea-478">Test connection to listener</span></span>

<span data-ttu-id="cedea-479">De verbinding testen:</span><span class="sxs-lookup"><span data-stu-id="cedea-479">To test the connection:</span></span>

1. <span data-ttu-id="cedea-480">RDP naar een SQL-Server die zich in hetzelfde virtuele netwerk, maar is geen eigenaar van de replica.</span><span class="sxs-lookup"><span data-stu-id="cedea-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="cedea-481">U kunt de SQL-Server in het cluster.</span><span class="sxs-lookup"><span data-stu-id="cedea-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="cedea-482">Gebruik **sqlcmd** hulpprogramma om de verbinding te testen.</span><span class="sxs-lookup"><span data-stu-id="cedea-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="cedea-483">Bijvoorbeeld, het volgende script stelt een **sqlcmd** verbinding met de primaire replica via de listener met de Windows-verificatie:</span><span class="sxs-lookup"><span data-stu-id="cedea-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="cedea-484">Als de listener met behulp van een andere poort dan de standaard poort (1433), de poort in de verbindingsreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="cedea-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="cedea-485">Bijvoorbeeld de volgende sqlcmd-opdracht is verbonden met een listener op poort 1435:</span><span class="sxs-lookup"><span data-stu-id="cedea-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="cedea-486">De SQLCMD-verbinding wordt automatisch verbinding met elk ander exemplaar van SQL Server als host fungeert voor de primaire replica.</span><span class="sxs-lookup"><span data-stu-id="cedea-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="cedea-487">Zorg ervoor dat de poort die u opgeeft geopend op de firewall van beide SQL-Servers is.</span><span class="sxs-lookup"><span data-stu-id="cedea-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="cedea-488">Beide servers vereisen een inkomende regel voor de TCP-poort die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cedea-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="cedea-489">Zie voor meer informatie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="cedea-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="cedea-490">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cedea-490">Next steps</span></span>

- <span data-ttu-id="cedea-491">[Een IP-adres toevoegen aan een load balancer voor een tweede beschikbaarheidsgroep](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="cedea-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
