---
title: aaaConfigure een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen in Azure | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo en er een altijd op beschikbaarheidsgroep-listener gemaakt in Azure die gebruikmaakt van een interne load balancer.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="d1916-103">Een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure</span><span class="sxs-lookup"><span data-stu-id="d1916-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1916-104">Interne listener</span><span class="sxs-lookup"><span data-stu-id="d1916-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="d1916-105">Externe-listener</span><span class="sxs-lookup"><span data-stu-id="d1916-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="d1916-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d1916-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1916-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d1916-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d1916-108">In dit artikel bevat informatie over gebruik van het klassieke implementatiemodel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1916-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="d1916-109">U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d1916-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="d1916-110">tooconfigure een listener voor een beschikbaarheidsgroep altijd op in de Resource Manager-model hello, Zie [een load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="d1916-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="d1916-111">De beschikbaarheidsgroep kan de replica's die alleen op lokale of Azure alleen, of die zowel on-premises en Azure voor hybride configuraties omvatten bevatten.</span><span class="sxs-lookup"><span data-stu-id="d1916-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="d1916-112">Azure replica's kunnen zich bevinden in Hallo dezelfde regio of tussen meerdere regio's die gebruikmaken van meerdere virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="d1916-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="d1916-113">Hallo procedures in dit artikel wordt ervan uitgegaan dat u al hebt [geconfigureerd een beschikbaarheidsgroep](../classic/portal-sql-alwayson-availability-groups.md) maar nog niet zijn ingesteld op een listener.</span><span class="sxs-lookup"><span data-stu-id="d1916-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="d1916-114">Richtlijnen en beperkingen voor interne listeners</span><span class="sxs-lookup"><span data-stu-id="d1916-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="d1916-115">Hallo-gebruik van een interne load balancer (ILB) met een beschikbaarheidsgroep-listener in Azure wordt onderwerp toohello richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1916-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="d1916-116">Hallo beschikbaarheidsgroep-listener wordt ondersteund op Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d1916-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="d1916-117">Alleen een interne beschikbaarheidsgroep-listener wordt ondersteund voor elke cloudservice omdat Hallo-listener is toohello ILB is geconfigureerd en er is slechts één ILB voor elke cloudservice.</span><span class="sxs-lookup"><span data-stu-id="d1916-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="d1916-118">Het is echter mogelijk toocreate meerdere externe listeners.</span><span class="sxs-lookup"><span data-stu-id="d1916-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="d1916-119">Zie voor meer informatie [een externe-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="d1916-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="d1916-120">Hallo toegankelijkheid van Hallo listener bepalen</span><span class="sxs-lookup"><span data-stu-id="d1916-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="d1916-121">Dit artikel is gericht op het maken van een listener die gebruikmaakt van een ILB.</span><span class="sxs-lookup"><span data-stu-id="d1916-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="d1916-122">Als u een openbare of externe-listener moet, Zie Hallo-versie van dit artikel dat instelling van bespreekt een [externe listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1916-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="d1916-123">VM-eindpunten taakverdeling met direct server return maken</span><span class="sxs-lookup"><span data-stu-id="d1916-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="d1916-124">U eerst maken een ILB door het uitvoeren van script hello later in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="d1916-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="d1916-125">Maak een eindpunt taakverdeling voor elke virtuele machine die als host fungeert voor een Azure-replica.</span><span class="sxs-lookup"><span data-stu-id="d1916-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="d1916-126">Als u replica's in meerdere regio's hebt, elke replica voor deze regio moet in dezelfde cloudservice in Hallo Hallo hetzelfde virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="d1916-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="d1916-127">Maken van replica's die meerdere Azure-regio's omvatten voor beschikbaarheid, moet meerdere virtuele netwerken configureren.</span><span class="sxs-lookup"><span data-stu-id="d1916-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="d1916-128">Zie voor meer informatie over het configureren van cross-virtuele netwerkverbindingen [virtueel netwerk toovirtual netwerkconnectiviteit configureren](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="d1916-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="d1916-129">Ga in hello Azure-portal, tooeach virtuele machine die als host fungeert voor een replica tooview Hallo details.</span><span class="sxs-lookup"><span data-stu-id="d1916-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="d1916-130">Klik op Hallo **eindpunten** tabblad voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d1916-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="d1916-131">Controleer of deze Hallo **naam** en **openbare poort** van Hallo-listener-eindpunt dat u wilt dat toouse zijn niet al in gebruik.</span><span class="sxs-lookup"><span data-stu-id="d1916-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="d1916-132">In voorbeeld Hallo in deze sectie, is de naam van de Hallo *MyEndpoint*, en poort Hallo *1433*.</span><span class="sxs-lookup"><span data-stu-id="d1916-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="d1916-133">Op de lokale client downloaden en installeren Hallo meest recente [PowerShell-module](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d1916-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="d1916-134">Azure PowerShell te starten.</span><span class="sxs-lookup"><span data-stu-id="d1916-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="d1916-135">Een nieuwe PowerShell-sessie wordt geopend, hello Azure beheerdersrechten modules waren geladen.</span><span class="sxs-lookup"><span data-stu-id="d1916-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="d1916-136">Voer `Get-AzurePublishSettingsFile` uit.</span><span class="sxs-lookup"><span data-stu-id="d1916-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="d1916-137">Deze cmdlet stuurt tooa browser toodownload een publiceren instellingen bestand tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="d1916-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="d1916-138">U mogelijk gevraagd om uw referenties aanmelden om uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d1916-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="d1916-139">Voer de volgende Hallo `Import-AzurePublishSettingsFile` opdracht met Hallo pad Hallo bestand publicatie-instellingen die u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="d1916-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="d1916-140">Nadat Hallo publiceren instellingenbestand is geïmporteerd, kunt u uw Azure-abonnement in de PowerShell-sessie Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="d1916-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="d1916-141">Voor *ILB*, een statisch IP-adres toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d1916-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="d1916-142">Hallo huidige virtuele netwerkconfiguratie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d1916-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="d1916-143">Opmerking Hallo *Subnet* naam in voor het Hallo-subnet dat Hallo virtuele machines die als host Hallo replica's fungeren bevat.</span><span class="sxs-lookup"><span data-stu-id="d1916-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="d1916-144">Deze naam wordt gebruikt in de parameter Hallo $SubnetName in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d1916-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="d1916-145">Opmerking Hallo *VirtualNetworkSite* een naam geven en Hallo starten *AddressPrefix* voor Hallo-subnet dat Hallo virtuele machines die als host Hallo replica's fungeren bevat.</span><span class="sxs-lookup"><span data-stu-id="d1916-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="d1916-146">Zoek naar een beschikbaar IP-adres door het doorgeven van beide waarden toohello `Test-AzureStaticVNetIP` opdracht en door te onderzoeken Hallo *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="d1916-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="d1916-147">Bijvoorbeeld, als hello virtueel netwerk met de naam *MyVNet* en heeft een subnet-adresbereik dat begint bij *172.16.0.128*, Hallo volgende opdracht zou lijst beschikbare adressen:</span><span class="sxs-lookup"><span data-stu-id="d1916-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="d1916-148">Selecteer een van de beschikbare adressen Hallo en deze gebruiken in Hallo $ILBStaticIP-parameter van het script in de volgende stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1916-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="d1916-149">Kopiëren van de volgende PowerShell-script tooa teksteditor Hallo en stel Hallo waarden van variabelen toosuit uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="d1916-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="d1916-150">Standaardwaarden zijn opgegeven voor een aantal parameters.</span><span class="sxs-lookup"><span data-stu-id="d1916-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="d1916-151">Bestaande implementaties die gebruikmaken van affiniteitsgroepen kunnen een ILB niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d1916-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="d1916-152">Zie voor meer informatie over de vereisten voor de ILB [interne load balancer overzicht](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1916-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="d1916-153">Ook als de beschikbaarheidsgroep Azure-regio's omvat, moet u Hallo script uitvoeren één keer in elk datacenter voor het Hallo-cloudservice en de knooppunten die zich in dat datacenter bevinden.</span><span class="sxs-lookup"><span data-stu-id="d1916-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="d1916-154">Nadat u de variabelen Hallo hebt ingesteld, kopie Hallo script uit Hallo text editor tooyour PowerShell-sessie toorun deze.</span><span class="sxs-lookup"><span data-stu-id="d1916-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="d1916-155">Als de prompt Hallo nog steeds  **>>** , druk op Enter toomake ervoor Hallo script opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d1916-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="d1916-156">Controleer of KB2854082 wordt indien nodig geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="d1916-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="d1916-157">Hallo firewall-poorten openen in de beschikbaarheid van groepsknooppunten</span><span class="sxs-lookup"><span data-stu-id="d1916-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="d1916-158">Hallo beschikbaarheidsgroep-listener maken</span><span class="sxs-lookup"><span data-stu-id="d1916-158">Create hello availability group listener</span></span>

<span data-ttu-id="d1916-159">Maak Hallo beschikbaarheidsgroep-listener in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="d1916-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="d1916-160">Eerst Hallo client access point-clusterbron maken en configureren van afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d1916-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="d1916-161">Ten tweede Hallo clusterbronnen in PowerShell configureren.</span><span class="sxs-lookup"><span data-stu-id="d1916-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="d1916-162">Hallo clienttoegangspunt maken en configureren van Hallo cluster afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="d1916-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="d1916-163">Hallo-clusterbronnen configureren in PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1916-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="d1916-164">Voor de ILB, moet u Hallo IP-adres van Hallo ILB die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d1916-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="d1916-165">tooobtain dit IP-adres in PowerShell, gebruik Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="d1916-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="d1916-166">Op een van de virtuele machines Hallo Hallo PowerShell-script kopiëren voor uw besturingssysteem tooa-teksteditor en stel Hallo variabelen toohello waarden die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="d1916-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="d1916-167">Voor Windows Server 2012 of hoger, gebruikt u Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="d1916-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="d1916-168">Gebruik voor Windows Server 2008 R2 Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="d1916-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="d1916-169">Nadat u hebt ingesteld Hallo variabelen, open een Windows PowerShell-venster met verhoogde bevoegdheid, plakken Hallo script in de teksteditor Hallo in uw PowerShell-sessie toorun deze.</span><span class="sxs-lookup"><span data-stu-id="d1916-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="d1916-170">Als de prompt Hallo nog steeds  **>>** , druk op Enter opnieuw toomake ervoor dat Hallo script wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d1916-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="d1916-171">Herhaal de vorige stappen voor elke VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1916-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="d1916-172">Dit script Hallo IP-adres resource met Hallo IP-adres van de cloudservice Hallo configureert en stelt u andere parameters, zoals Hallo testpoort.</span><span class="sxs-lookup"><span data-stu-id="d1916-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="d1916-173">Wanneer de bron van het IP-adres Hallo online is gebracht, reageert het toohello polling op Hallo testpoort van Hallo taakverdeling eindpunt dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d1916-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="d1916-174">Hallo-listener online brengen</span><span class="sxs-lookup"><span data-stu-id="d1916-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="d1916-175">Items worden opgevolgd</span><span class="sxs-lookup"><span data-stu-id="d1916-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="d1916-176">Test Hallo beschikbaarheidsgroep-listener (Hallo binnen hetzelfde virtuele netwerk)</span><span class="sxs-lookup"><span data-stu-id="d1916-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="d1916-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1916-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
