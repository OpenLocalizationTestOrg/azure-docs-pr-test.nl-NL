---
title: 'Een virtueel Azure-netwerk verbinden met een ander VNet: Powershell | Microsoft Docs'
description: Dit artikel helpt u bij het met elkaar verbinden van virtuele netwerken met behulp van Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="ef07f-103">Een VPN-gatewayverbinding tussen VNets configureren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef07f-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="ef07f-104">In dit artikel wordt beschreven hoe u een VPN-gatewayverbinding tussen virtuele netwerken maakt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="ef07f-105">De virtuele netwerken kunnen zich in dezelfde of verschillende regio's bevinden en tot dezelfde of verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="ef07f-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="ef07f-106">Wanneer u VNets uit verschillende abonnementen koppelt, hoeven de abonnementen niet aan dezelfde Active Directory-tenant gekoppeld te zijn.</span><span class="sxs-lookup"><span data-stu-id="ef07f-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="ef07f-107">De stappen in dit artikel zijn van toepassing op het Resource Manager-implementatiemodel. Er wordt gebruikgemaakt van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef07f-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="ef07f-108">U kunt deze configuratie ook maken met een ander implementatiehulpprogramma of een ander implementatiemodel door in de volgende lijst een andere optie te selecteren:</span><span class="sxs-lookup"><span data-stu-id="ef07f-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef07f-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef07f-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="ef07f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef07f-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="ef07f-111">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="ef07f-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="ef07f-112">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ef07f-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="ef07f-113">Verbinding maken tussen verschillende implementatiemodellen - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef07f-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="ef07f-114">Verbinding maken tussen verschillende implementatiemodellen - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef07f-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="ef07f-115">Het verbinden van een virtueel netwerk met een ander virtueel netwerk (VNet-naar-VNet) lijkt op het verbinden van een VNet met een on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="ef07f-116">Voor beide connectiviteitstypen wordt een VPN-gateway gebruikt om een beveiligde tunnel met IPsec/IKE te bieden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="ef07f-117">Als uw VNET's zich in dezelfde regio bevinden, kunt u daarmee verbinding maken met behulp van VNet-peering.</span><span class="sxs-lookup"><span data-stu-id="ef07f-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="ef07f-118">Bij VNet-peering wordt geen VPN-gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="ef07f-119">Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="ef07f-120">VNet-naar-VNet-communicatie kan worden gecombineerd met configuraties voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="ef07f-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="ef07f-121">Zoals u in het volgende diagram kunt zien, kunt u netwerktopologieën maken waarin cross-premises connectiviteit wordt gecombineerd met connectiviteit tussen virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="ef07f-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Over verbindingen](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="ef07f-123">Waarom virtuele netwerken koppelen?</span><span class="sxs-lookup"><span data-stu-id="ef07f-123">Why connect virtual networks?</span></span>

<span data-ttu-id="ef07f-124">U wilt virtuele netwerken wellicht koppelen om de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="ef07f-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="ef07f-125">**Geografische redundantie en aanwezigheid tussen regio's**</span><span class="sxs-lookup"><span data-stu-id="ef07f-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="ef07f-126">U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ef07f-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="ef07f-127">Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="ef07f-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="ef07f-128">Een belangrijk voorbeeld hiervan is het instellen van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="ef07f-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="ef07f-129">**Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**</span><span class="sxs-lookup"><span data-stu-id="ef07f-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="ef07f-130">Binnen dezelfde regio kunt u vanwege isolatie- of beheervereisten toepassingen met meerdere lagen instellen met meerdere virtuele netwerken die met elkaar zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="ef07f-131">Zie voor meer informatie over verbindingen tussen VNets de [Veelgestelde vragen over VNet-naar-VNet](#faq) aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ef07f-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="ef07f-132">Welke stappen moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="ef07f-132">Which set of steps should I use?</span></span>

<span data-ttu-id="ef07f-133">In dit artikel ziet u twee verschillende reeksen stappen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="ef07f-134">Een reeks stappen voor [VNets die zich in hetzelfde abonnement bevinden](#samesub) en een andere voor [VNets die zich in verschillende abonnementen bevinden](#difsub).</span><span class="sxs-lookup"><span data-stu-id="ef07f-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="ef07f-135">Het belangrijkste verschil tussen de reeksen is of u alle resources van het virtuele netwerk en de gateway kunt maken en configureren binnen dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="ef07f-136">In de stappen in dit artikel worden variabelen gebruikt die aan het begin van elke sectie zijn gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="ef07f-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="ef07f-137">Als u al met bestaande VNets werkt, wijzigt u de variabelen zo dat ze overeenkomen met de instellingen in uw eigen omgeving.</span><span class="sxs-lookup"><span data-stu-id="ef07f-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="ef07f-138">Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="ef07f-139"><a name="samesub"></a>VNets verbinden die tot hetzelfde abonnement behoren</span><span class="sxs-lookup"><span data-stu-id="ef07f-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="ef07f-141">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ef07f-141">Before you begin</span></span>

<span data-ttu-id="ef07f-142">Installeer eerst de meest recente versie van de Azure Resource Manager PowerShell-cmdlets (versie 4.0 of hoger).</span><span class="sxs-lookup"><span data-stu-id="ef07f-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="ef07f-143">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ef07f-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="ef07f-144"><a name="Step1"></a>Stap 1: De IP-adresbereiken plannen</span><span class="sxs-lookup"><span data-stu-id="ef07f-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="ef07f-145">In de volgende stappen maakt u twee virtuele netwerken en hun bijbehorende gatewaysubnetten en configuraties.</span><span class="sxs-lookup"><span data-stu-id="ef07f-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="ef07f-146">Vervolgens maakt u een VPN-verbinding tussen de twee VNets.</span><span class="sxs-lookup"><span data-stu-id="ef07f-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="ef07f-147">Het is belangrijk dat u de IP-adresbereiken voor uw netwerkconfiguratie plant.</span><span class="sxs-lookup"><span data-stu-id="ef07f-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="ef07f-148">De VNet-bereiken of de bereiken van het lokale netwerk mogen elkaar niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="ef07f-149">In deze voorbeelden behandelen we geen DNS-server.</span><span class="sxs-lookup"><span data-stu-id="ef07f-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="ef07f-150">Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="ef07f-151">In de voorbeelden worden de volgende waarden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="ef07f-151">We use the following values in the examples:</span></span>

<span data-ttu-id="ef07f-152">**Waarden voor TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="ef07f-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="ef07f-153">VNet-naam: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="ef07f-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="ef07f-154">Resourcegroep: TestRG1</span><span class="sxs-lookup"><span data-stu-id="ef07f-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="ef07f-155">Locatie: VS - oost</span><span class="sxs-lookup"><span data-stu-id="ef07f-155">Location: East US</span></span>
* <span data-ttu-id="ef07f-156">TestVNet1: 10.11.0.0/16 en 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ef07f-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="ef07f-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="ef07f-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="ef07f-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="ef07f-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="ef07f-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="ef07f-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="ef07f-161">Openbare IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="ef07f-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="ef07f-162">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="ef07f-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="ef07f-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="ef07f-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="ef07f-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="ef07f-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="ef07f-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="ef07f-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="ef07f-166">**Waarden voor TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="ef07f-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="ef07f-167">VNet-naam: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="ef07f-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="ef07f-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ef07f-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="ef07f-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="ef07f-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="ef07f-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="ef07f-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="ef07f-172">Resourcegroep: TestRG4</span><span class="sxs-lookup"><span data-stu-id="ef07f-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="ef07f-173">Locatie: VS - west</span><span class="sxs-lookup"><span data-stu-id="ef07f-173">Location: West US</span></span>
* <span data-ttu-id="ef07f-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="ef07f-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="ef07f-175">Openbare IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="ef07f-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="ef07f-176">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="ef07f-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="ef07f-177">Verbinding: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="ef07f-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="ef07f-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="ef07f-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="ef07f-179"><a name="Step2"></a>Stap 2: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="ef07f-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="ef07f-180">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-180">Declare your variables.</span></span> <span data-ttu-id="ef07f-181">In dit voorbeeld worden de variabelen gedeclareerd met de waarden voor deze oefening.</span><span class="sxs-lookup"><span data-stu-id="ef07f-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="ef07f-182">In de meeste gevallen moet u de waarden vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="ef07f-183">U kunt deze variabelen echter gebruiken als u de stappen alleen wilt doorlopen om vertrouwd te raken met dit type configuratie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="ef07f-184">Wijzig de variabelen als dat nodig is en kopieer en plak ze vervolgens in uw PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="ef07f-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="ef07f-185">Maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="ef07f-185">Connect to your account.</span></span> <span data-ttu-id="ef07f-186">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="ef07f-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="ef07f-187">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="ef07f-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="ef07f-188">Geef het abonnement op dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="ef07f-189">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef07f-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="ef07f-190">Maak de subnetconfiguraties voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="ef07f-191">In dit voorbeeld wordt een virtueel netwerk gemaakt met de naam TestVNet1. Er worden ook drie subnetten gemaakt, GatewaySubnet, FrontEnd en BackEnd.</span><span class="sxs-lookup"><span data-stu-id="ef07f-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="ef07f-192">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="ef07f-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="ef07f-193">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="ef07f-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="ef07f-194">In het volgende voorbeeld worden de variabelen gebruikt die u eerder hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ef07f-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="ef07f-195">In dit voorbeeld maakt het gatewaysubnet gebruik van een /27.</span><span class="sxs-lookup"><span data-stu-id="ef07f-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="ef07f-196">Het is mogelijk om een klein gatewaysubnet van /29 te maken, maar we raden u aan een groter subnet met meer adressen te maken door ten minste /28 of /27 te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ef07f-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="ef07f-197">Hierdoor hebt u genoeg adressen voor mogelijke aanvullende toekomstige configuraties.</span><span class="sxs-lookup"><span data-stu-id="ef07f-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="ef07f-198">Maak TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="ef07f-199">Vraag om een openbaar IP-adres toe te wijzen aan de gateway die u voor uw VNet gaat maken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="ef07f-200">De toewijzingsmethode is Dynamisch.</span><span class="sxs-lookup"><span data-stu-id="ef07f-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="ef07f-201">U kunt het IP-adres dat u wilt gebruiken niet zelf opgeven.</span><span class="sxs-lookup"><span data-stu-id="ef07f-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="ef07f-202">Het wordt dynamisch toegewezen aan uw gateway.</span><span class="sxs-lookup"><span data-stu-id="ef07f-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="ef07f-203">Maak de gatewayconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-203">Create the gateway configuration.</span></span> <span data-ttu-id="ef07f-204">De gatewayconfiguratie bepaalt welk subnet en openbaar IP-adres moeten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="ef07f-205">Gebruik het voorbeeld om de gatewayconfiguratie te maken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="ef07f-206">Maak de gateway voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="ef07f-207">In deze stap maakt u de virtuele netwerkgateway TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="ef07f-208">VNet-naar-VNet-configuraties vereisen een op route gebaseerd VpnType.</span><span class="sxs-lookup"><span data-stu-id="ef07f-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="ef07f-209">Het maken van een gateway duurt vaak 45 minuten of langer, afhankelijk van de geselecteerde gateway-SKU.</span><span class="sxs-lookup"><span data-stu-id="ef07f-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="ef07f-210">Stap 3: TestVNet4 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="ef07f-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="ef07f-211">Wanneer u TestVNet1 hebt geconfigureerd, maakt u TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="ef07f-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="ef07f-212">Volg de stappen hieronder en vervang de waarden door uw eigen waarden wanneer dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="ef07f-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="ef07f-213">Deze stap kan worden uitgevoerd binnen dezelfde PowerShell-sessie omdat deze tot hetzelfde abonnement behoort.</span><span class="sxs-lookup"><span data-stu-id="ef07f-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="ef07f-214">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-214">Declare your variables.</span></span> <span data-ttu-id="ef07f-215">Zorg ervoor dat u de waarden vervangt door de waarden die u voor uw configuratie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="ef07f-216">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef07f-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="ef07f-217">Maak de subnetconfiguraties voor TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="ef07f-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="ef07f-218">Maak TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="ef07f-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="ef07f-219">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="ef07f-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="ef07f-220">Maak de gatewayconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="ef07f-221">Maak de TestVNet4-gateway.</span><span class="sxs-lookup"><span data-stu-id="ef07f-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="ef07f-222">Het maken van een gateway duurt vaak 45 minuten of langer, afhankelijk van de geselecteerde gateway-SKU.</span><span class="sxs-lookup"><span data-stu-id="ef07f-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="ef07f-223">Stap 4: de verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="ef07f-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="ef07f-224">Verkrijg beide gateways van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef07f-224">Get both virtual network gateways.</span></span> <span data-ttu-id="ef07f-225">Als beide gateways tot hetzelfde abonnement behoren, zoals in het voorbeeld, kunt u deze stap in dezelfde PowerShell-sessie voltooien.</span><span class="sxs-lookup"><span data-stu-id="ef07f-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="ef07f-226">Maak de verbinding tussen TestVNet1 en TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="ef07f-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="ef07f-227">In deze stap maakt u de verbinding van TestVNet1 naar TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="ef07f-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="ef07f-228">Hier ziet u een gedeelde sleutel waarnaar wordt verwezen in de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="ef07f-229">U kunt uw eigen waarden voor de gedeelde sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="ef07f-230">Het belangrijkste is dat de gedeelde sleutel voor beide verbindingen moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="ef07f-231">Het kan even duren voordat de verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="ef07f-232">Maak de verbinding tussen TestVNet4 en TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="ef07f-233">Deze stap is vergelijkbaar met die hierboven, alleen maakt u de verbinding nu vanuit TestVNet4 naar TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="ef07f-234">Zorg dat de gedeelde sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-234">Make sure the shared keys match.</span></span> <span data-ttu-id="ef07f-235">De verbinding wordt na enkele minuten tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ef07f-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="ef07f-236">Controleer de verbinding.</span><span class="sxs-lookup"><span data-stu-id="ef07f-236">Verify your connection.</span></span> <span data-ttu-id="ef07f-237">Raadpleeg de sectie [De verbinding controleren](#verify).</span><span class="sxs-lookup"><span data-stu-id="ef07f-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="ef07f-238"><a name="difsub"></a>VNets verbinden die tot verschillende abonnement behoren</span><span class="sxs-lookup"><span data-stu-id="ef07f-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="ef07f-240">In dit scenario worden TestVNet1 en TestVNet5 met elkaar verbonden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="ef07f-241">TestVNet1 en TestVNet5 bevinden zich in een verschillend abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef07f-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="ef07f-242">De abonnementen hoeven niet aan dezelfde Active Directory-tenant gekoppeld te zijn.</span><span class="sxs-lookup"><span data-stu-id="ef07f-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="ef07f-243">Het verschil tussen deze stappen en de eerste set is dat een deel van de configuratiestappen moet worden uitgevoerd in een aparte PowerShell-sessie in de context van het tweede abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef07f-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="ef07f-244">Dit geldt met name wanneer de twee abonnementen tot verschillende organisaties behoren.</span><span class="sxs-lookup"><span data-stu-id="ef07f-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="ef07f-245">Stap 5: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="ef07f-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="ef07f-246">U moet [Stap 1](#Step1) en [Stap 2](#Step2) van de vorige sessie uitvoeren om TestVNet1 en de VPN-gateway voor TestVNet1 te maken en te configureren.</span><span class="sxs-lookup"><span data-stu-id="ef07f-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="ef07f-247">Voor deze configuratie is het niet vereist TestVNet4 uit de vorige sectie te maken. Als u deze wel maakt, levert dit geen problemen op met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="ef07f-248">Nadat u stap 1 en stap 2 hebt voltooid, gaat u verder met stap 6 om TestVNet5 te maken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="ef07f-249">Stap 6: de IP-adresbereiken controleren</span><span class="sxs-lookup"><span data-stu-id="ef07f-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="ef07f-250">Het is belangrijk dat u controleert of de IP-adresruimte van het nieuwe virtuele netwerk, TestVNet5, niet overlapt met een van de VNet-bereiken of de gatewaybereiken van het lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef07f-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="ef07f-251">In dit voorbeeld kunnen de virtuele netwerken tot verschillende organisaties behoren.</span><span class="sxs-lookup"><span data-stu-id="ef07f-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="ef07f-252">Voor deze oefening kunt u de volgende waarden voor TestVNet5 gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ef07f-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="ef07f-253">**Waarden voor TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="ef07f-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="ef07f-254">VNet-naam: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="ef07f-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="ef07f-255">Resourcegroep: TestRG5</span><span class="sxs-lookup"><span data-stu-id="ef07f-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="ef07f-256">Locatie: Japan - oost</span><span class="sxs-lookup"><span data-stu-id="ef07f-256">Location: Japan East</span></span>
* <span data-ttu-id="ef07f-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ef07f-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="ef07f-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="ef07f-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ef07f-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="ef07f-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="ef07f-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="ef07f-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="ef07f-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="ef07f-262">Openbare IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="ef07f-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="ef07f-263">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="ef07f-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="ef07f-264">Verbinding: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="ef07f-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="ef07f-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="ef07f-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="ef07f-266">Stap 7: TestVNet5 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="ef07f-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="ef07f-267">Deze stap moet worden uitgevoerd in de context van het nieuwe abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef07f-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="ef07f-268">Dit deel kan worden uitgevoerd door de beheerder in een andere organisatie die eigenaar is van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef07f-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="ef07f-269">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-269">Declare your variables.</span></span> <span data-ttu-id="ef07f-270">Zorg ervoor dat u de waarden vervangt door de waarden die u voor uw configuratie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="ef07f-271">Maak verbinding met abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-271">Connect to subscription 5.</span></span> <span data-ttu-id="ef07f-272">Open de PowerShell-console en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="ef07f-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="ef07f-273">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="ef07f-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="ef07f-274">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="ef07f-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="ef07f-275">Geef het abonnement op dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef07f-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="ef07f-276">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef07f-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="ef07f-277">Maak de subnetconfiguraties voor TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="ef07f-278">Maak TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="ef07f-279">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="ef07f-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="ef07f-280">Maak de gatewayconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="ef07f-281">Maak de TestVNet5-gateway.</span><span class="sxs-lookup"><span data-stu-id="ef07f-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="ef07f-282">Stap 8: de verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="ef07f-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="ef07f-283">Omdat de gateways in dit voorbeeld tot verschillende abonnementen behoren, is deze stap opgesplitst in twee PowerShell-sessies, aangeduid als [Abonnement 1] en [Abonnement 5].</span><span class="sxs-lookup"><span data-stu-id="ef07f-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="ef07f-284">**[Abonnement 1]** Verkrijg de gateway van het virtuele netwerk voor abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="ef07f-285">Meld u aan bij en maak verbinding met abonnement 1 voordat u het volgende voorbeeld uitvoert:</span><span class="sxs-lookup"><span data-stu-id="ef07f-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="ef07f-286">Kopieer de uitvoer van de volgende elementen en stuur deze via e-mail of een andere manier naar de beheerder van abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="ef07f-287">De waarden van deze twee elementen lijken op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ef07f-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="ef07f-288">**[Abonnement 5]** Verkrijg de gateway van het virtuele netwerk voor abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="ef07f-289">Meld u aan bij en maak verbinding met abonnement 5 voordat u het volgende voorbeeld uitvoert:</span><span class="sxs-lookup"><span data-stu-id="ef07f-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="ef07f-290">Kopieer de uitvoer van de volgende elementen en stuur deze via e-mail of een andere manier naar de beheerder van Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="ef07f-291">De waarden van deze twee elementen lijken op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ef07f-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="ef07f-292">**[Abonnement 1]** Maak de verbinding tussen TestVNet1 en TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="ef07f-293">In deze stap maakt u de verbinding van TestVNet1 naar TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="ef07f-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="ef07f-294">Het verschil is hier dat $vnet5gw niet rechtstreeks kan worden verkregen omdat het zich in een ander abonnement bevindt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="ef07f-295">U moet een nieuw PowerShell-object maken met de waarden die in de bovenstaande stappen zijn gecommuniceerd vanuit Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="ef07f-296">Gebruik onderstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ef07f-296">Use the example below.</span></span> <span data-ttu-id="ef07f-297">Vervang de naam, de id en de gedeelde sleutel door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ef07f-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="ef07f-298">Het belangrijkste is dat de gedeelde sleutel voor beide verbindingen moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="ef07f-299">Het kan even duren voordat de verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef07f-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="ef07f-300">Maak verbinding met abonnement 1 voordat u het volgende voorbeeld uitvoert:</span><span class="sxs-lookup"><span data-stu-id="ef07f-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="ef07f-301">**[Abonnement 5]** Maak de verbinding tussen TestVNet5 en TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="ef07f-302">Deze stap is vergelijkbaar met die hierboven, alleen maakt u de verbinding nu vanuit TestVNet5 naar TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="ef07f-303">Hier moet op dezelfde manier een PowerShell-object worden gemaakt op basis van de waarden die zijn verkregen van Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="ef07f-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="ef07f-304">Zorg in deze stap dat de gedeelde sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="ef07f-305">Maak verbinding met abonnement 5 voordat u het volgende voorbeeld uitvoert:</span><span class="sxs-lookup"><span data-stu-id="ef07f-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="ef07f-306"><a name="verify"></a>Een verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="ef07f-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="ef07f-307"><a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet</span><span class="sxs-lookup"><span data-stu-id="ef07f-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ef07f-308">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef07f-308">Next steps</span></span>

* <span data-ttu-id="ef07f-309">Wanneer de verbinding is voltooid, kunt u virtuele machines aan uw virtuele netwerken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef07f-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="ef07f-310">Raadpleeg de [documentatie over Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef07f-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="ef07f-311">Voor meer informatie over BGP raadpleegt u [BGP Overview](vpn-gateway-bgp-overview.md) (BGP-overzicht) en [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md) (BGP configureren).</span><span class="sxs-lookup"><span data-stu-id="ef07f-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>