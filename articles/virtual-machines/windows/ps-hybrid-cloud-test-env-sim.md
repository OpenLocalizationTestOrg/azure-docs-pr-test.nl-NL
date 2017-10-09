---
title: aaaSimulated hybride cloud-testomgeving | Microsoft Docs
description: Maakt een gesimuleerde hybride cloud-omgeving voor IT pro of ontwikkeling testen met behulp van twee virtuele Azure-netwerken en een VNet-naar-VNet-verbinding.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="a944f-103">Een gesimuleerde hybride cloudomgeving instellen voor testen</span><span class="sxs-lookup"><span data-stu-id="a944f-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="a944f-104">In dit artikel begeleidt u bij het maken van een omgeving met gesimuleerde hybride cloud met Microsoft Azure met behulp van twee virtuele Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="a944f-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="a944f-105">Hier wordt de resulterende configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a944f-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="a944f-106">Dit simuleert een hybride cloud-productieomgeving en bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="a944f-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="a944f-107">Een gesimuleerde en vereenvoudigd on-premises netwerk wordt gehost in een Azure-netwerk (Hallo TestLab virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="a944f-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="a944f-108">Een gesimuleerde cross-premises virtueel netwerk gehost in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="a944f-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="a944f-109">Een VNet-naar-VNet-verbinding tussen Hallo twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="a944f-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="a944f-110">Een secundaire domeincontroller in het Hallo TestVNET virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="a944f-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="a944f-111">Dit biedt dat een basis- en algemene starten van het rapportageservicepunt vanuit die u kunt:</span><span class="sxs-lookup"><span data-stu-id="a944f-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="a944f-112">Toepassingen ontwikkelen en testen in een gesimuleerde hybride cloud-omgeving.</span><span class="sxs-lookup"><span data-stu-id="a944f-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="a944f-113">Test-configuraties van computers, sommige vanuit Hallo TestLab virtueel netwerk en sommige binnen Hallo TestVNET virtueel netwerk, toosimulate hybride cloud-gebaseerde IT werkbelastingen maken.</span><span class="sxs-lookup"><span data-stu-id="a944f-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="a944f-114">Er zijn vier belangrijke fasen toosetting u deze testomgeving van hybride cloud:</span><span class="sxs-lookup"><span data-stu-id="a944f-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="a944f-115">Hallo TestLab virtueel netwerk configureren.</span><span class="sxs-lookup"><span data-stu-id="a944f-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="a944f-116">Hallo cross-premises virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="a944f-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="a944f-117">Hallo VNet-naar-VNet-VPN-verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="a944f-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="a944f-118">DC2 configureren.</span><span class="sxs-lookup"><span data-stu-id="a944f-118">Configure DC2.</span></span> 

<span data-ttu-id="a944f-119">Deze configuratie is vereist voor een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a944f-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="a944f-120">Als u een MSDN- of Visual Studio-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="a944f-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="a944f-121">Virtuele machines en virtuele netwerkgateways in Azure kosten in rekening gebracht een lopende financieel wanneer ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a944f-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="a944f-122">Deze kosten in rekening gebracht op basis van uw MSDN of betaald abonnement.</span><span class="sxs-lookup"><span data-stu-id="a944f-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="a944f-123">Een Azure VPN-gateway wordt geïmplementeerd als een set van twee virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a944f-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="a944f-124">toominimize hello kosten, Hallo testomgeving maken en het benodigde testen en demonstratie zo snel mogelijk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a944f-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="a944f-125">Fase 1: Hallo TestLab virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="a944f-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="a944f-126">Hallo-instructies gebruiken in Hallo [basisconfiguratie testomgeving](https://technet.microsoft.com/library/mt771177.aspx) onderwerp tooconfigure Hallo DC1, APP1 en CLIENT1-computers in hello Azure-netwerk de naam van TestLab.</span><span class="sxs-lookup"><span data-stu-id="a944f-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="a944f-127">Vervolgens start u een Azure PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="a944f-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="a944f-128">Hallo volgende opdracht stelt u Azure PowerShell 1.0 en hoger gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a944f-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="a944f-129">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="a944f-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="a944f-130">De abonnementsnaam van uw met behulp van de volgende opdracht Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="a944f-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="a944f-131">Stel uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a944f-131">Set your Azure subscription.</span></span> <span data-ttu-id="a944f-132">Gebruik Hallo hetzelfde abonnement dat u toobuild de basisconfiguratie in fase 1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a944f-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="a944f-133">Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste naam Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="a944f-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="a944f-134">Vervolgens voegt u een gateway subnet toohello TestLab virtueel netwerk van uw basisconfiguratie, de gebruikte toohost hello Azure-gateway worden.</span><span class="sxs-lookup"><span data-stu-id="a944f-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="a944f-135">Vervolgens vraagt u een openbaar IP-adres tooassign toohello gateway voor Hallo TestLab virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="a944f-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="a944f-136">Maak vervolgens uw gateway.</span><span class="sxs-lookup"><span data-stu-id="a944f-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="a944f-137">Houd er rekening mee dat nieuwe gateways 20 minuten of meer toocreate kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="a944f-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="a944f-138">Verbinding van hello Azure-portal op uw lokale computer, tooDC1 met Hallo corp\gebruiker1-referenties.</span><span class="sxs-lookup"><span data-stu-id="a944f-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="a944f-139">tooconfigure hello CORP-domein dat computers en gebruikers hun lokale domeincontroller voor verificatie, gebruiken deze opdrachten uitvoeren vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op DC1.</span><span class="sxs-lookup"><span data-stu-id="a944f-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="a944f-140">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="a944f-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="a944f-141">Fase 2: Hallo TestVNET virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a944f-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="a944f-142">Eerst Hallo TestVNET virtueel netwerk maken en beveiligen met een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="a944f-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="a944f-143">Vervolgens aanvraag een openbare IP-adres toobe toohello gateway toegewezen voor Hallo TestVNET virtuele netwerk en maak uw gateway.</span><span class="sxs-lookup"><span data-stu-id="a944f-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="a944f-144">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="a944f-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="a944f-145">Fase 3: Maak Hallo VNet-naar-VNet-verbinding</span><span class="sxs-lookup"><span data-stu-id="a944f-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="a944f-146">Eerst moet u een willekeurige, cryptografisch sterke, 32-teken vooraf gedeelde sleutel van uw netwerk- of -beheerder.</span><span class="sxs-lookup"><span data-stu-id="a944f-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="a944f-147">U kunt ook gebruik Hallo informatie op [maken van een willekeurige tekenreeks op voor een vooraf gedeelde sleutel IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain een vooraf gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="a944f-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="a944f-148">Gebruik vervolgens deze opdrachten toocreate hello VNet-naar-VNet-VPN-verbinding, waarvan sommige toocomplete tijd kan duren.</span><span class="sxs-lookup"><span data-stu-id="a944f-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="a944f-149">Na een paar minuten moet Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="a944f-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="a944f-150">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="a944f-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="a944f-151">Fase 4: DC2 configureren</span><span class="sxs-lookup"><span data-stu-id="a944f-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="a944f-152">Maak eerst een virtuele machine voor DC2.</span><span class="sxs-lookup"><span data-stu-id="a944f-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="a944f-153">Deze opdrachten uitvoeren bij hello Azure PowerShell-opdrachtprompt op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="a944f-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="a944f-154">Vervolgens maakt u verbinding toohello nieuwe DC2 virtuele machine uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a944f-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="a944f-155">Configureer vervolgens een Windows Firewall tooallow verkeer van de regel voor het testen van verbinding.</span><span class="sxs-lookup"><span data-stu-id="a944f-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="a944f-156">Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op DC2.</span><span class="sxs-lookup"><span data-stu-id="a944f-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="a944f-157">Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="a944f-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="a944f-158">Dit is een test van het verkeer tussen Hallo VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="a944f-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="a944f-159">Vervolgens voegt u Hallo extra gegevensschijf op DC2 als een nieuw volume met de stationsletter Hallo F:.</span><span class="sxs-lookup"><span data-stu-id="a944f-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="a944f-160">In Hallo linkerdeelvenster van Serverbeheer, klikt u op **File and Storage Services**, en klik vervolgens op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="a944f-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="a944f-161">In het Hallo inhoudsdeelvenster Hallo **schijven** groep, klikt u op **schijf 2** (Hello **partitie** instellen te**onbekende**).</span><span class="sxs-lookup"><span data-stu-id="a944f-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="a944f-162">Klik op **taken**, en klik vervolgens op **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="a944f-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="a944f-163">Hallo voordat u een pagina van Wizard Nieuw Volume hello, klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a944f-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="a944f-164">Klik op Hallo Selecteer Hallo-server en schijfpagina op **schijf 2**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a944f-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="a944f-165">Wanneer u wordt gevraagd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a944f-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="a944f-166">Klik op Hallo Hallo grootte opgeven van Hallo volume pagina, **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a944f-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="a944f-167">Klik op Hallo toewijzen tooa station stationsletter of map pagina op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a944f-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="a944f-168">Klik op Hallo bestand selecteren pagina systeeminstellingen, **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a944f-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="a944f-169">Klik op de pagina van het Hallo bevestigen selecties **maken**.</span><span class="sxs-lookup"><span data-stu-id="a944f-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="a944f-170">Wanneer voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="a944f-170">When complete, click **Close**.</span></span>

<span data-ttu-id="a944f-171">Configureer vervolgens de DC2 als een replicadomeincontroller voor Hallo corp.contoso.com domein.</span><span class="sxs-lookup"><span data-stu-id="a944f-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="a944f-172">Deze opdrachten uitvoeren met Windows PowerShell-opdrachtprompt Hallo op DC2.</span><span class="sxs-lookup"><span data-stu-id="a944f-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="a944f-173">Er rekening mee dat u na vragen aan gebruiker toosupply beide Hallo corp\gebruiker1 wachtwoord en een wachtwoord van Directory Services Restore Mode (DSRM) en toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="a944f-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="a944f-174">Nu dat hello TestVNET virtueel netwerk heeft zijn eigen DNS-server (DC2), moet u Hallo TestVNET virtueel netwerk toouse deze DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="a944f-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="a944f-175">Klik op Hallo virtuele netwerken pictogram in het linkerdeelvenster Hallo Hallo Azure-portal en klik vervolgens op **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="a944f-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="a944f-176">Op Hallo **instellingen** tabblad **DNS-servers**.</span><span class="sxs-lookup"><span data-stu-id="a944f-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="a944f-177">In **primaire DNS-server**, type **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="a944f-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="a944f-178">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a944f-178">Click **Save**.</span></span>

<span data-ttu-id="a944f-179">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="a944f-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="a944f-180">Uw gesimuleerde hybride cloudomgeving is nu gereed voor het testen.</span><span class="sxs-lookup"><span data-stu-id="a944f-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="a944f-181">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="a944f-181">Next step</span></span>
* <span data-ttu-id="a944f-182">Instellen van een [webgebaseerde line-of-business-toepassing](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in deze omgeving.</span><span class="sxs-lookup"><span data-stu-id="a944f-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

