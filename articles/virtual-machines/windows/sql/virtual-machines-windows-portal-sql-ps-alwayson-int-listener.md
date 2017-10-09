---
title: "aaaConfigure altijd op beschikbaarheid Beschikbaarheidsgroeplisteners – Microsoft Azure | Microsoft Docs"
description: Beschikbaarheid van groep Listeners hello Azure Resource Manager-model, met behulp van een interne load balancer met een of meer IP-adressen configureren.
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="7a619-103">Een of meer altijd op beschikbaarheid beschikbaarheidsgroeplisteners - Resource Manager configureren</span><span class="sxs-lookup"><span data-stu-id="7a619-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="7a619-104">Dit onderwerp wordt beschreven hoe:</span><span class="sxs-lookup"><span data-stu-id="7a619-104">This topic shows how to:</span></span>

* <span data-ttu-id="7a619-105">Maak een interne load balancer voor SQL Server-beschikbaarheidsgroepen met PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7a619-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="7a619-106">Extra IP-adressen tooa load balancer voor meer dan één beschikbaarheidsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a619-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="7a619-107">Een beschikbaarheidsgroep-listener is de naam van een virtueel netwerk dat clients verbinding toofor toegang tot de database maken.</span><span class="sxs-lookup"><span data-stu-id="7a619-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="7a619-108">Op virtuele machines in Azure bevat een load balancer Hallo IP-adres voor het Hallo-listener.</span><span class="sxs-lookup"><span data-stu-id="7a619-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="7a619-109">Hallo load balancer routes verkeer toohello exemplaar van SQL Server die op Hallo testpoort luistert.</span><span class="sxs-lookup"><span data-stu-id="7a619-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="7a619-110">Een beschikbaarheidsgroep maakt meestal gebruik van een interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="7a619-111">Een Azure interne load balancer kan één of meerdere IP-adressen te hosten.</span><span class="sxs-lookup"><span data-stu-id="7a619-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="7a619-112">Elk IP-adres gebruikt een specifieke testpoort.</span><span class="sxs-lookup"><span data-stu-id="7a619-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="7a619-113">Dit document beschrijft hoe toouse PowerShell toocreate een load balancer, of Voeg de IP-adressen tooan bestaande load balancer voor SQL Server-beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="7a619-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="7a619-114">Hallo mogelijkheid tooassign meerdere IP-adressen tooan interne load balancer is nieuwe tooAzure en is alleen beschikbaar in het Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="7a619-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="7a619-115">toocomplete deze taak moet u een SQL Server-beschikbaarheidsgroep is geïmplementeerd op Azure virtuele machines in de Resource Manager-model toohave.</span><span class="sxs-lookup"><span data-stu-id="7a619-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="7a619-116">Beide virtuele machines van SQL Server moet behoren toohello dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="7a619-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="7a619-117">U kunt Hallo [Microsoft sjabloon](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Hallo-beschikbaarheidsgroep maken in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a619-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="7a619-118">Deze sjabloon wordt automatisch de beschikbaarheidsgroep hello, inclusief Hallo interne load balancer voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a619-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="7a619-119">Als u liever, kunt u [handmatig configureren van een AlwaysOn-beschikbaarheidsgroep](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="7a619-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="7a619-120">In dit onderwerp is vereist dat uw beschikbaarheidsgroepen al zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7a619-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="7a619-121">Verwante onderwerpen zijn:</span><span class="sxs-lookup"><span data-stu-id="7a619-121">Related topics include:</span></span>

* [<span data-ttu-id="7a619-122">AlwaysOn-beschikbaarheidsgroepen configureren in Azure virtuele machine (GUI)</span><span class="sxs-lookup"><span data-stu-id="7a619-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="7a619-123">Een VNet-naar-VNet-verbinding configureren met behulp van Azure Resource Manager en PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a619-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="7a619-124">Hallo Windows Firewall configureren</span><span class="sxs-lookup"><span data-stu-id="7a619-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="7a619-125">Hallo Windows Firewall tooallow SQL Server-toegang configureren.</span><span class="sxs-lookup"><span data-stu-id="7a619-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="7a619-126">Hallo-firewallregels toestaan TCP-verbindingen toohello poorten gebruiken door Hallo SQL Server-exemplaar en Hallo-listener-test.</span><span class="sxs-lookup"><span data-stu-id="7a619-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="7a619-127">Zie voor gedetailleerde instructies [Windows Firewall configureren voor toegang tot de Database-Engine](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="7a619-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="7a619-128">Een inkomende regel voor Hallo SQL Server-poort en de testpoort Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7a619-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="7a619-129">Voorbeeldscript: Een interne load balancer maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a619-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="7a619-130">Als u de beschikbaarheidsgroep hebt gemaakt met de Hallo [Microsoft sjabloon](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), Hallo interne load balancer al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a619-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="7a619-131">Hallo volgende PowerShell-script maakt een interne load balancer, configureert u regels voor taakverdeling hello, en stelt een IP-adres voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="7a619-132">toorun hello script, opent u Windows PowerShell ISE en Hallo script in het scriptvenster hello te plakken.</span><span class="sxs-lookup"><span data-stu-id="7a619-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="7a619-133">Gebruik `Login-AzureRMAccount` toolog in tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a619-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="7a619-134">Als u meerdere Azure-abonnementen hebt, gebruikt u `Select-AzureRmSubscription ` tooset Hallo abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a619-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="7a619-135"><a name="Add-IP"></a>Voorbeeldscript: een IP-adres tooan bestaande load balancer toevoegen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a619-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="7a619-136">Voeg een extra IP-adres toohello load balancer toouse meer dan één beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="7a619-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="7a619-137">Elk IP-adres vereist een eigen taakverdeling regel, testpoort en front-poort.</span><span class="sxs-lookup"><span data-stu-id="7a619-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="7a619-138">Hallo front-endpoort is Hallo-poort dat toepassingen tooconnect toohello SQL Server-exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a619-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="7a619-139">IP-adressen voor verschillende beschikbaarheid groepen kunnen gebruiken dezelfde front-endpoort Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a619-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="7a619-140">Elk IP-adres vereist voor beschikbaarheidsgroepen van SQL Server, een specifieke testpoort.</span><span class="sxs-lookup"><span data-stu-id="7a619-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="7a619-141">Als u één IP-adres voor een load balancer testpoort 59999 gebruikt, kunnen geen andere IP-adressen op die load balancer testpoort 59999 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a619-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="7a619-142">Zie voor meer informatie over de load balancer limieten **persoonlijke front-end-IP per load balancer** onder [Networking limieten - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="7a619-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="7a619-143">Zie voor meer informatie over de beschikbaarheid van groep limieten [beperkingen (beschikbaarheidsgroepen)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="7a619-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="7a619-144">Hallo voegt volgende script een nieuwe IP-adres tooan bestaande load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="7a619-145">Hallo ILB gebruikt Hallo-listener-poort voor Hallo-front-endpoort voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="7a619-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="7a619-146">Deze poort kan worden Hallo-poort die SQL Server luistert.</span><span class="sxs-lookup"><span data-stu-id="7a619-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="7a619-147">Hallo-poort is voor standaardexemplaren van SQL Server is 1433.</span><span class="sxs-lookup"><span data-stu-id="7a619-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="7a619-148">taakverdelingsregel voor een beschikbaarheidsgroep Hallo vereist een zwevend IP (direct server return) zodat Hallo back-endpoort Hallo dezelfde als de front-endpoort Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a619-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="7a619-149">Hallo variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7a619-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="7a619-150">Hallo-listener configureren</span><span class="sxs-lookup"><span data-stu-id="7a619-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="7a619-151">Hallo-listener-poort ingesteld in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="7a619-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="7a619-152">Start SQL Server Management Studio en maak verbinding toohello primaire replica.</span><span class="sxs-lookup"><span data-stu-id="7a619-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="7a619-153">Navigeer te**AlwaysOn hoge beschikbaarheid** | **beschikbaarheidsgroepen** | **beschikbaarheid Beschikbaarheidsgroeplisteners**.</span><span class="sxs-lookup"><span data-stu-id="7a619-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="7a619-154">U ziet nu Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="7a619-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="7a619-155">Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7a619-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="7a619-156">In Hallo **poort** Geef Hallo-poortnummer voor Hallo beschikbaarheidsgroep-listener met behulp van Hallo $EndpointPort u eerder hebt gebruikt (1433 was Hallo standaard), klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a619-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="7a619-157">Test Hallo verbinding toohello listener</span><span class="sxs-lookup"><span data-stu-id="7a619-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="7a619-158">tootest hello verbinding:</span><span class="sxs-lookup"><span data-stu-id="7a619-158">tootest hello connection:</span></span>

1. <span data-ttu-id="7a619-159">RDP-tooa SQL-Server die zich in Hallo hetzelfde virtuele netwerk, maar niet eigen Hallo replica.</span><span class="sxs-lookup"><span data-stu-id="7a619-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="7a619-160">Dit kan Hallo andere SQL-Server in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a619-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="7a619-161">Gebruik **sqlcmd** hulpprogramma tootest Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="7a619-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="7a619-162">Bijvoorbeeld Hallo script volgen stelt een **sqlcmd** verbinding toohello primaire replica via het Hallo-listener met de Windows-verificatie:</span><span class="sxs-lookup"><span data-stu-id="7a619-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="7a619-163">Als het Hallo-listener poort wordt gebruikt door een andere waarde dan Hallo standaard poort (1433), Hallo-poort in de verbindingsreeks Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="7a619-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="7a619-164">Bijvoorbeeld: hello volgende sqlcmd-opdracht verbindt tooa listener op poort 1435:</span><span class="sxs-lookup"><span data-stu-id="7a619-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="7a619-165">Hallo SQLCMD-verbinding verbinding automatisch toowhichever exemplaar van SQL Server-hosts Hallo primaire replica.</span><span class="sxs-lookup"><span data-stu-id="7a619-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="7a619-166">Zorg ervoor dat Hallo poort die u opgeeft geopend op Hallo firewall beide SQL-servers is.</span><span class="sxs-lookup"><span data-stu-id="7a619-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="7a619-167">Beide servers vereisen een inkomende regel voor Hallo TCP-poort die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a619-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="7a619-168">Zie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7a619-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="7a619-169">Richtlijnen en beperkingen</span><span class="sxs-lookup"><span data-stu-id="7a619-169">Guidelines and limitations</span></span>
<span data-ttu-id="7a619-170">Houd er rekening mee Hallo richtlijnen op beschikbaarheidsgroep-listener in Azure met behulp van de interne load balancer:</span><span class="sxs-lookup"><span data-stu-id="7a619-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="7a619-171">Met een interne load balancer u alleen toegang tot Hallo-listener van Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="7a619-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="7a619-172">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="7a619-172">For more information</span></span>
<span data-ttu-id="7a619-173">Zie voor meer informatie [configureren altijd op de beschikbaarheidsgroep in Azure VM handmatig](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="7a619-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="7a619-174">PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="7a619-174">PowerShell cmdlets</span></span>
<span data-ttu-id="7a619-175">Hallo volgende PowerShell-cmdlets toocreate een interne load balancer voor virtuele machines in Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a619-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="7a619-176">[Nieuwe AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) maakt u een load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="7a619-177">[Nieuwe AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) maakt een front-end-IP-configuratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="7a619-178">[Nieuwe AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) maakt u de regelconfiguratie van een voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="7a619-179">[Nieuwe AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) maakt een back-end-pool-adresconfiguratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="7a619-180">[Nieuwe AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) maakt u een test-configuratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a619-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="7a619-181">[Verwijder AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) Hiermee verwijdert u een load balancer van een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7a619-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
