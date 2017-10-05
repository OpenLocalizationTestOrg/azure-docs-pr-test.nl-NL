---
title: Beschikbaarheid van SQL Server - virtuele Machines in Azure - noodherstel groepen | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u een SQL Server-beschikbaarheidsgroep configureren op Azure virtuele machines met een replica in een andere regio.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="4d261-103">Een AlwaysOn-beschikbaarheidsgroep configureren op virtuele Azure-machines in verschillende regio 's</span><span class="sxs-lookup"><span data-stu-id="4d261-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="4d261-104">In dit artikel wordt uitgelegd hoe u een SQL Server Always On beschikbaarheidsgroepreplica's op virtuele Azure-machines op een externe locatie voor Azure configureren.</span><span class="sxs-lookup"><span data-stu-id="4d261-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="4d261-105">Deze configuratie gebruiken ter ondersteuning van herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="4d261-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="4d261-106">In dit artikel is van toepassing op Azure Virtual Machines in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d261-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="4d261-107">De volgende afbeelding toont een algemene implementatie van een beschikbaarheidsgroep op Azure virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="4d261-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="4d261-109">In deze implementatie worden alle virtuele machines in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="4d261-110">De beschikbaarheidsgroepreplica's kunnen synchrone doorvoer met automatische failover op de SQL-1 en SQL-2 hebben.</span><span class="sxs-lookup"><span data-stu-id="4d261-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="4d261-111">Als u wilt maken van deze architectuur, Zie [beschikbaarheidsgroep sjabloon of zelfstudie](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="4d261-112">Deze architectuur is kwetsbaar voor downtime als de Azure-regio niet toegankelijk wordt.</span><span class="sxs-lookup"><span data-stu-id="4d261-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="4d261-113">Toevoegen voor het opheffen van deze kwetsbaarheid, een replica in een andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="4d261-114">Het volgende diagram toont de nieuwe architectuur zou als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="4d261-114">The following diagram shows how the new architecture would look:</span></span>

   ![Beschikbaarheid van groep DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="4d261-116">De voorgaande diagram ziet u een nieuwe virtuele machine SQL 3 aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4d261-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="4d261-117">SQL-3 is in een andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="4d261-118">SQL-3 wordt toegevoegd aan de Windows Server-failovercluster.</span><span class="sxs-lookup"><span data-stu-id="4d261-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="4d261-119">SQL-3 kan een beschikbaarheidsreplica van de groep host.</span><span class="sxs-lookup"><span data-stu-id="4d261-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="4d261-120">Ten slotte kunt u ziet dat de Azure-regio voor SQL-3 een nieuwe Azure load balancer heeft.</span><span class="sxs-lookup"><span data-stu-id="4d261-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="4d261-121">Een Azure beschikbaarheidsset is vereist wanneer meer dan één virtuele machine bevindt zich in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="4d261-122">De beschikbaarheidsset is niet vereist als er slechts één virtuele machine zich in de regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="4d261-123">U kunt alleen een virtuele machine in een beschikbaarheidsset tijdens de aanmaak plaatsen.</span><span class="sxs-lookup"><span data-stu-id="4d261-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="4d261-124">Als de virtuele machine is al in een beschikbaarheidsset bevindt, kunt u een virtuele machine voor een extra replica later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d261-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="4d261-125">In deze architectuur wordt de replica in de externe regio normaal gesproken geconfigureerd met asynchrone doorvoermodus voor beschikbaarheid en handmatige failover-modus.</span><span class="sxs-lookup"><span data-stu-id="4d261-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="4d261-126">Als replica's van beschikbaarheidsgroepen op Azure virtuele machines in verschillende Azure-regio's, moet elke regio:</span><span class="sxs-lookup"><span data-stu-id="4d261-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="4d261-127">Een virtuele netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="4d261-127">A virtual network gateway</span></span>
* <span data-ttu-id="4d261-128">Een verbinding met virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="4d261-128">A virtual network gateway connection</span></span>

<span data-ttu-id="4d261-129">Het volgende diagram toont hoe de netwerken communiceren tussen datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d261-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="4d261-131">Deze architectuur leidt ertoe dat kosten voor uitgaande gegevens voor gegevens gerepliceerd tussen Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="4d261-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="4d261-132">Zie [bandbreedte prijzen](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="4d261-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="4d261-133">Externe replica maken</span><span class="sxs-lookup"><span data-stu-id="4d261-133">Create remote replica</span></span>

<span data-ttu-id="4d261-134">Voor het maken van een replica in een externe Datacenter, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d261-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="4d261-135">[Een virtueel netwerk maken in de nieuwe regio](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="4d261-136">[Configureren van een VNet-naar-VNet-verbinding met de Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="4d261-137">In sommige gevallen moet u wellicht PowerShell gebruiken om de VNet-naar-VNet-verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="4d261-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="4d261-138">Als u verschillende Azure-accounts gebruiken niet kunt u de verbinding configureren in de portal.</span><span class="sxs-lookup"><span data-stu-id="4d261-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="4d261-139">In dit geval ziet, [configureren van een VNet-naar-VNet-verbinding met de Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="4d261-140">[Maken van een domeincontroller in het nieuwe gebied](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="4d261-141">Deze domeincontroller biedt verificatie als de domeincontroller in de primaire site niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="4d261-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="4d261-142">[Maken van een virtuele machine van SQL Server in de nieuwe regio](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4d261-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="4d261-143">[Maak een Azure load balancer in het netwerk op de nieuwe regio](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="4d261-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="4d261-144">Deze load balancer moet:</span><span class="sxs-lookup"><span data-stu-id="4d261-144">This load balancer must:</span></span>

   - <span data-ttu-id="4d261-145">Zich bevinden in hetzelfde netwerk en subnet als de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4d261-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="4d261-146">Een statisch IP-adres hebben voor de beschikbaarheidsgroeplistener.</span><span class="sxs-lookup"><span data-stu-id="4d261-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="4d261-147">Een back-endpool die bestaan uit alleen de virtuele machines in dezelfde regio bevinden als de load balancer bevatten.</span><span class="sxs-lookup"><span data-stu-id="4d261-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="4d261-148">Gebruik een TCP-poort test die specifiek zijn voor het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="4d261-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="4d261-149">Een taakverdelingsregel specifiek zijn voor de SQL-Server in dezelfde regio hebben.</span><span class="sxs-lookup"><span data-stu-id="4d261-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="4d261-150">[Functie Failover Clustering toevoegen aan de nieuwe SQL-Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="4d261-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="4d261-151">[De nieuwe SQL-Server toevoegen aan het domein](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="4d261-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="4d261-152">[Instellen van de nieuwe SQL Server-serviceaccount voor een domeinaccount gebruiken](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="4d261-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="4d261-153">[De nieuwe SQL-Server toevoegen aan Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="4d261-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="4d261-154">Maak een bron van de IP-adres op het cluster.</span><span class="sxs-lookup"><span data-stu-id="4d261-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="4d261-155">U kunt de IP-adres-resource maken in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="4d261-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="4d261-156">Met de rechtermuisknop op de rol van de groep beschikbaarheid, klikt u op **Resource toevoegen**, **meer bronnen**, en klik op **IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="4d261-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![IP-adres maken](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="4d261-158">Dit IP-adres als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="4d261-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="4d261-159">Het netwerk van het externe Datacenter gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d261-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="4d261-160">Wijs het IP-adres van de nieuwe Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="4d261-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="4d261-161">Op de nieuwe SQL-Server in SQL Server Configuration Manager [inschakelen altijd op beschikbaarheidsgroepen](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d261-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="4d261-162">[Open firewallpoorten op de nieuwe SQL-Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="4d261-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="4d261-163">De poortnummers die u wilt openen, is afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="4d261-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="4d261-164">Open poorten voor de spiegeling eindpunt en Azure load balancer health test.</span><span class="sxs-lookup"><span data-stu-id="4d261-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="4d261-165">[Een replica toevoegen aan de beschikbaarheidsgroep op de nieuwe SQL-Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d261-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="4d261-166">Voor een replica in een externe Azure-regio, moet u deze voor asynchrone replicatie met handmatige failover instellen.</span><span class="sxs-lookup"><span data-stu-id="4d261-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="4d261-167">De bron van het IP-adres toevoegen als een afhankelijkheid voor de listener client access point (netwerknaam) cluster.</span><span class="sxs-lookup"><span data-stu-id="4d261-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="4d261-168">De volgende schermafbeelding ziet een correct geconfigureerde clusterbron voor IP-adres:</span><span class="sxs-lookup"><span data-stu-id="4d261-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="4d261-170">De clusterbrongroep bevat beide IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="4d261-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="4d261-171">Afhankelijkheden voor de listener client access point-beide IP-adressen zijn.</span><span class="sxs-lookup"><span data-stu-id="4d261-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="4d261-172">Gebruik de **of** -operator in de configuratie van het cluster-afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="4d261-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="4d261-173">[Stel de clusterparameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="4d261-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="4d261-174">Voer de PowerShell-script met de clusternetwerknaam, IP-adres en testpoort die u hebt geconfigureerd op de load balancer in de nieuwe regio.</span><span class="sxs-lookup"><span data-stu-id="4d261-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="4d261-175">Set-verbinding voor meerdere subnetten</span><span class="sxs-lookup"><span data-stu-id="4d261-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="4d261-176">De replica in het externe Datacenter maakt deel uit van de beschikbaarheidsgroep, maar het is in een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="4d261-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="4d261-177">Als deze replica de primaire replica wordt, kunnen de time-outs van de toepassing optreden.</span><span class="sxs-lookup"><span data-stu-id="4d261-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="4d261-178">Dit gedrag is hetzelfde als een lokale beschikbaarheidsgroep in een implementatie met meerdere subnetten.</span><span class="sxs-lookup"><span data-stu-id="4d261-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="4d261-179">Als u wilt toestaan verbindingen vanaf client toepassingen, verbinding met de client bijwerken of opslaan in cache op de cluster-netwerknaam naamomzetting configureren.</span><span class="sxs-lookup"><span data-stu-id="4d261-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="4d261-180">Bij voorkeur, werk de verbindingsreeksen van de client in te stellen `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="4d261-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="4d261-181">Zie [verbinding te maken met MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="4d261-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="4d261-182">Als u de verbindingsreeksen niet wijzigen, kunt u de naam resolutie caching kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="4d261-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="4d261-183">Zie [time-outs voor verbindingen in meerdere subnetten beschikbaarheidsgroep](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="4d261-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="4d261-184">Failover naar externe regio</span><span class="sxs-lookup"><span data-stu-id="4d261-184">Fail over to remote region</span></span>

<span data-ttu-id="4d261-185">Als u wilt testen listener-verbindingsproblemen met de externe regio, kunt u de replica voor de externe regio failover.</span><span class="sxs-lookup"><span data-stu-id="4d261-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="4d261-186">Terwijl de replica asynchroon is, is failover kwetsbaar voor mogelijk gegevensverlies.</span><span class="sxs-lookup"><span data-stu-id="4d261-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="4d261-187">Wijzig de beschikbaarheidsmodus in synchrone failover zonder verlies van gegevens, en de failover-modus ingesteld op automatisch.</span><span class="sxs-lookup"><span data-stu-id="4d261-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="4d261-188">Voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d261-188">Use the following steps:</span></span>

1. <span data-ttu-id="4d261-189">In **Objectverkenner**, verbinding met het exemplaar van SQL Server die als host fungeert voor de primaire replica.</span><span class="sxs-lookup"><span data-stu-id="4d261-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="4d261-190">Onder **AlwaysOn Availability Groups**, **beschikbaarheidsgroepen**, met de rechtermuisknop op de beschikbaarheidsgroep en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="4d261-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="4d261-191">Op de **algemene** pagina onder **Beschikbaarheidsreplica**, instellen van de secundaire replica in de DR-site te gebruiken **synchroon doorvoeren** beschikbaarheidsmodus en **automatische** failover-modus.</span><span class="sxs-lookup"><span data-stu-id="4d261-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="4d261-192">Als u een secundaire replica in dezelfde site als de primaire replica voor hoge beschikbaarheid hebt, stelt u deze replica op **asynchrone doorvoeren** en **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="4d261-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="4d261-193">Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="4d261-193">Click OK.</span></span>
1. <span data-ttu-id="4d261-194">In **Objectverkenner**, met de rechtermuisknop op de beschikbaarheidsgroep en klikt u op **Dashboard weergeven**.</span><span class="sxs-lookup"><span data-stu-id="4d261-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="4d261-195">Controleren of de replica op de DR-site is gesynchroniseerd op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="4d261-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="4d261-196">In **Objectverkenner**, met de rechtermuisknop op de beschikbaarheidsgroep en klikt u op **Failover...** .</span><span class="sxs-lookup"><span data-stu-id="4d261-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="4d261-197">SQL Server Management Studios Hiermee opent u de wizard een failover van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d261-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="4d261-198">Klik op **volgende**, en selecteer het SQL Server-exemplaar in de DR-site.</span><span class="sxs-lookup"><span data-stu-id="4d261-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="4d261-199">Klik op **volgende** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4d261-199">Click **Next** again.</span></span>
1. <span data-ttu-id="4d261-200">Verbinding maken met de SQL Server-exemplaar in de DR-site en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4d261-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="4d261-201">Op de **samenvatting** pagina, Controleer de instellingen en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="4d261-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="4d261-202">Na de verbinding test, de primaire replica naar uw primaire Datacenter gaan en de beschikbaarheidsmodus weer instellen op hun normale operationele instellingen.</span><span class="sxs-lookup"><span data-stu-id="4d261-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="4d261-203">De volgende tabel ziet u de normale operationele instellingen voor de architectuur die in dit document beschreven:</span><span class="sxs-lookup"><span data-stu-id="4d261-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="4d261-204">Locatie</span><span class="sxs-lookup"><span data-stu-id="4d261-204">Location</span></span> | <span data-ttu-id="4d261-205">Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="4d261-205">Server Instance</span></span> | <span data-ttu-id="4d261-206">Rol</span><span class="sxs-lookup"><span data-stu-id="4d261-206">Role</span></span> | <span data-ttu-id="4d261-207">De Beschikbaarheidsmodus</span><span class="sxs-lookup"><span data-stu-id="4d261-207">Availability Mode</span></span> | <span data-ttu-id="4d261-208">Failover-modus</span><span class="sxs-lookup"><span data-stu-id="4d261-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="4d261-209">Primaire Datacenter</span><span class="sxs-lookup"><span data-stu-id="4d261-209">Primary data center</span></span> | <span data-ttu-id="4d261-210">SQL-1</span><span class="sxs-lookup"><span data-stu-id="4d261-210">SQL-1</span></span> | <span data-ttu-id="4d261-211">Primair</span><span class="sxs-lookup"><span data-stu-id="4d261-211">Primary</span></span> | <span data-ttu-id="4d261-212">Synchrone</span><span class="sxs-lookup"><span data-stu-id="4d261-212">Synchronous</span></span> | <span data-ttu-id="4d261-213">Automatisch</span><span class="sxs-lookup"><span data-stu-id="4d261-213">Automatic</span></span>
| <span data-ttu-id="4d261-214">Primaire Datacenter</span><span class="sxs-lookup"><span data-stu-id="4d261-214">Primary data center</span></span> | <span data-ttu-id="4d261-215">SQL-2</span><span class="sxs-lookup"><span data-stu-id="4d261-215">SQL-2</span></span> | <span data-ttu-id="4d261-216">Secundair</span><span class="sxs-lookup"><span data-stu-id="4d261-216">Secondary</span></span> | <span data-ttu-id="4d261-217">Synchrone</span><span class="sxs-lookup"><span data-stu-id="4d261-217">Synchronous</span></span> | <span data-ttu-id="4d261-218">Automatisch</span><span class="sxs-lookup"><span data-stu-id="4d261-218">Automatic</span></span>
| <span data-ttu-id="4d261-219">Secundaire of door de externe Datacenter</span><span class="sxs-lookup"><span data-stu-id="4d261-219">Secondary or remote data center</span></span> | <span data-ttu-id="4d261-220">SQL-3</span><span class="sxs-lookup"><span data-stu-id="4d261-220">SQL-3</span></span> | <span data-ttu-id="4d261-221">Secundair</span><span class="sxs-lookup"><span data-stu-id="4d261-221">Secondary</span></span> | <span data-ttu-id="4d261-222">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="4d261-222">Asynchronous</span></span> | <span data-ttu-id="4d261-223">Handmatig</span><span class="sxs-lookup"><span data-stu-id="4d261-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="4d261-224">Meer informatie over de geplande en geforceerde handmatige failover</span><span class="sxs-lookup"><span data-stu-id="4d261-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="4d261-225">Zie de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="4d261-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="4d261-226">Voer een geplande handmatige Failover van een beschikbaarheidsgroep (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="4d261-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="4d261-227">Voer een geforceerde handmatige Failover van een beschikbaarheidsgroep (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="4d261-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="4d261-228">Aanvullende koppelingen</span><span class="sxs-lookup"><span data-stu-id="4d261-228">Additional Links</span></span>

* [<span data-ttu-id="4d261-229">Altijd op beschikbaarheidsgroepen</span><span class="sxs-lookup"><span data-stu-id="4d261-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="4d261-230">Virtuele Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="4d261-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="4d261-231">Azure Load Balancers</span><span class="sxs-lookup"><span data-stu-id="4d261-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="4d261-232">Azure Beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="4d261-232">Azure Availability Sets</span></span>](../manage-availability.md)
