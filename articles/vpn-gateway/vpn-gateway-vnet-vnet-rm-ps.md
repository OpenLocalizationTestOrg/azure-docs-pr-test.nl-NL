---
title: 'Verbinding maken met een virtuele Azure-netwerk tooanother VNet: PowerShell | Microsoft Docs'
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
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="08b0c-103">Een VPN-gatewayverbinding tussen VNets configureren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="08b0c-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="08b0c-104">Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="08b0c-105">Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="08b0c-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="08b0c-106">Bij het maken van verbinding VNets uit verschillende abonnementen behoren, Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="08b0c-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="08b0c-107">Hallo stappen in dit artikel toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="08b0c-108">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="08b0c-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="08b0c-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="08b0c-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="08b0c-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08b0c-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="08b0c-111">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="08b0c-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="08b0c-112">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="08b0c-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="08b0c-113">Verbinding maken tussen verschillende implementatiemodellen - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="08b0c-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="08b0c-114">Verbinding maken tussen verschillende implementatiemodellen - PowerShell</span><span class="sxs-lookup"><span data-stu-id="08b0c-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="08b0c-115">Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="08b0c-116">Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="08b0c-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="08b0c-117">Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooconsider deze met behulp van VNet-Peering te verbinden.</span><span class="sxs-lookup"><span data-stu-id="08b0c-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="08b0c-118">Bij VNet-peering wordt geen VPN-gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="08b0c-119">Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="08b0c-120">VNet-naar-VNet-communicatie kan worden gecombineerd met configuraties voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="08b0c-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="08b0c-121">Hiermee kunt u netwerktopologieën maken waarin cross-premises-connectiviteit met connectiviteit tussen virtuele netwerken, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="08b0c-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Over verbindingen](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="08b0c-123">Waarom virtuele netwerken koppelen?</span><span class="sxs-lookup"><span data-stu-id="08b0c-123">Why connect virtual networks?</span></span>

<span data-ttu-id="08b0c-124">U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="08b0c-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="08b0c-125">**Geografische redundantie en aanwezigheid tussen regio's**</span><span class="sxs-lookup"><span data-stu-id="08b0c-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="08b0c-126">U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.</span><span class="sxs-lookup"><span data-stu-id="08b0c-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="08b0c-127">Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="08b0c-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="08b0c-128">Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="08b0c-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="08b0c-129">**Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**</span><span class="sxs-lookup"><span data-stu-id="08b0c-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="08b0c-130">Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere virtuele netwerken met elkaar verbonden vervaldatum tooisolation of beheervereisten.</span><span class="sxs-lookup"><span data-stu-id="08b0c-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="08b0c-131">Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="08b0c-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="08b0c-132">Welke stappen moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="08b0c-132">Which set of steps should I use?</span></span>

<span data-ttu-id="08b0c-133">In dit artikel ziet u twee verschillende reeksen stappen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="08b0c-134">Een reeks stappen voor het [VNets die tot hetzelfde abonnement Hallo](#samesub), en een andere voor [VNets die tot verschillende abonnementen](#difsub).</span><span class="sxs-lookup"><span data-stu-id="08b0c-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="08b0c-135">Hallo belangrijkste verschil tussen Hallo sets is of u kunt maken en configureren van alle virtuele netwerk en gateway bronnen binnen Hallo dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="08b0c-136">Hallo stappen in dit artikel variabelen gebruiken die zijn gedeclareerd op Hallo begin van elke sectie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="08b0c-137">Als u al met bestaande vnet's werkt, kunt u Hallo variabelen tooreflect Hallo instellingen in uw eigen omgeving aanpassen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="08b0c-138">Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="08b0c-139"><a name="samesub"></a>Hoe tooconnect VNets die zijn opgenomen in Hallo hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="08b0c-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="08b0c-141">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="08b0c-141">Before you begin</span></span>

<span data-ttu-id="08b0c-142">Voordat u begint moet u de meest recente versie van tooinstall Hallo van hello Azure Resource Manager PowerShell-cmdlets, ten minste 4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="08b0c-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="08b0c-143">Zie voor meer informatie over het installeren van de PowerShell-cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08b0c-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="08b0c-144"><a name="Step1"></a>Stap 1: De IP-adresbereiken plannen</span><span class="sxs-lookup"><span data-stu-id="08b0c-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="08b0c-145">In de Hallo stappen te volgen, maken we twee virtuele netwerken en hun bijbehorende gatewaysubnetten en configuraties.</span><span class="sxs-lookup"><span data-stu-id="08b0c-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="08b0c-146">We vervolgens een VPN-verbinding maken tussen Hallo twee VNets.</span><span class="sxs-lookup"><span data-stu-id="08b0c-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="08b0c-147">Het is belangrijk tooplan Hallo IP-adresbereiken voor uw netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="08b0c-148">De VNet-bereiken of de bereiken van het lokale netwerk mogen elkaar niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="08b0c-149">In deze voorbeelden behandelen we geen DNS-server.</span><span class="sxs-lookup"><span data-stu-id="08b0c-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="08b0c-150">Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="08b0c-151">We gebruiken de volgende waarden in de voorbeelden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="08b0c-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="08b0c-152">**Waarden voor TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="08b0c-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="08b0c-153">VNet-naam: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="08b0c-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="08b0c-154">Resourcegroep: TestRG1</span><span class="sxs-lookup"><span data-stu-id="08b0c-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="08b0c-155">Locatie: VS - oost</span><span class="sxs-lookup"><span data-stu-id="08b0c-155">Location: East US</span></span>
* <span data-ttu-id="08b0c-156">TestVNet1: 10.11.0.0/16 en 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="08b0c-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="08b0c-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="08b0c-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="08b0c-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="08b0c-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="08b0c-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="08b0c-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="08b0c-161">Openbare IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="08b0c-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="08b0c-162">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="08b0c-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="08b0c-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="08b0c-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="08b0c-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="08b0c-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="08b0c-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="08b0c-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="08b0c-166">**Waarden voor TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="08b0c-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="08b0c-167">VNet-naam: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="08b0c-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="08b0c-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="08b0c-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="08b0c-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="08b0c-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="08b0c-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="08b0c-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="08b0c-172">Resourcegroep: TestRG4</span><span class="sxs-lookup"><span data-stu-id="08b0c-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="08b0c-173">Locatie: VS - west</span><span class="sxs-lookup"><span data-stu-id="08b0c-173">Location: West US</span></span>
* <span data-ttu-id="08b0c-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="08b0c-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="08b0c-175">Openbare IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="08b0c-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="08b0c-176">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="08b0c-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="08b0c-177">Verbinding: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="08b0c-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="08b0c-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="08b0c-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="08b0c-179"><a name="Step2"></a>Stap 2: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="08b0c-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="08b0c-180">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-180">Declare your variables.</span></span> <span data-ttu-id="08b0c-181">In dit voorbeeld declareert Hallo variabelen met Hallo waarden voor deze oefening.</span><span class="sxs-lookup"><span data-stu-id="08b0c-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="08b0c-182">In de meeste gevallen moet u waarden Hallo vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="08b0c-183">U kunt deze variabelen echter gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="08b0c-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="08b0c-184">Wijzig variabelen Hallo indien nodig, en vervolgens Kopieer en plak ze in de PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="08b0c-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="08b0c-185">Tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-185">Connect tooyour account.</span></span> <span data-ttu-id="08b0c-186">Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="08b0c-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="08b0c-187">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="08b0c-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="08b0c-188">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="08b0c-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="08b0c-189">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="08b0c-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="08b0c-190">Hallo subnetconfiguraties maken voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="08b0c-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="08b0c-191">In dit voorbeeld wordt een virtueel netwerk gemaakt met de naam TestVNet1. Er worden ook drie subnetten gemaakt, GatewaySubnet, FrontEnd en BackEnd.</span><span class="sxs-lookup"><span data-stu-id="08b0c-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="08b0c-192">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="08b0c-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="08b0c-193">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="08b0c-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="08b0c-194">Hallo wordt volgende voorbeeld Hallo variabelen die u eerder hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="08b0c-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="08b0c-195">In dit voorbeeld maakt Hallo gatewaysubnet gebruik van een/27.</span><span class="sxs-lookup"><span data-stu-id="08b0c-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="08b0c-196">Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet met meer adressen maakt door ten minste/28 of /27 selecteren.</span><span class="sxs-lookup"><span data-stu-id="08b0c-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="08b0c-197">Hierdoor kunt voldoende adressen tooaccommodate mogelijk aanvullende configuraties die u kunt Hallo toekomstige.</span><span class="sxs-lookup"><span data-stu-id="08b0c-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="08b0c-198">Maak TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="08b0c-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="08b0c-199">Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="08b0c-200">U ziet dat Hallo AllocationMethod is dynamische.</span><span class="sxs-lookup"><span data-stu-id="08b0c-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="08b0c-201">U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="08b0c-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="08b0c-202">Is dynamisch toegewezen tooyour gateway.</span><span class="sxs-lookup"><span data-stu-id="08b0c-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="08b0c-203">Hallo gatewayconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-203">Create hello gateway configuration.</span></span> <span data-ttu-id="08b0c-204">Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse.</span><span class="sxs-lookup"><span data-stu-id="08b0c-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="08b0c-205">Hallo voorbeeld toocreate uw gatewayconfiguratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="08b0c-206">Hallo-gateway voor TestVNet1 maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="08b0c-207">In deze stap maakt u de virtuele netwerkgateway Hallo voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="08b0c-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="08b0c-208">VNet-naar-VNet-configuraties vereisen een op route gebaseerd VpnType.</span><span class="sxs-lookup"><span data-stu-id="08b0c-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="08b0c-209">Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="08b0c-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="08b0c-210">Stap 3: TestVNet4 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="08b0c-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="08b0c-211">Wanneer u TestVNet1 hebt geconfigureerd, maakt u TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="08b0c-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="08b0c-212">Hallo stappen hieronder en vervang Hallo waarden door uw eigen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="08b0c-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="08b0c-213">Deze stap kan worden uitgevoerd binnen Hallo dezelfde PowerShell-sessie omdat deze zich in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="08b0c-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="08b0c-214">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-214">Declare your variables.</span></span> <span data-ttu-id="08b0c-215">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="08b0c-216">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="08b0c-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="08b0c-217">Hallo subnetconfiguraties maken voor TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="08b0c-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="08b0c-218">Maak TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="08b0c-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="08b0c-219">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="08b0c-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="08b0c-220">Hallo gatewayconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="08b0c-221">Hallo TestVNet4-gateway maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="08b0c-222">Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="08b0c-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="08b0c-223">Stap 4: Hallo verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="08b0c-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="08b0c-224">Verkrijg beide gateways van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="08b0c-224">Get both virtual network gateways.</span></span> <span data-ttu-id="08b0c-225">Als beide Hallo gateways in Hallo hetzelfde abonnement behoren, zoals in het Hallo-voorbeeld, kunt u deze stap bij het Hallo voltooien dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="08b0c-226">Hallo TestVNet1 tooTestVNet4 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="08b0c-227">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="08b0c-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="08b0c-228">Hier ziet u een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="08b0c-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="08b0c-229">U kunt uw eigen waarden voor Hallo gedeelde sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="08b0c-230">Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="08b0c-231">Maken van een verbinding kan duren voordat een korte tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="08b0c-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="08b0c-232">Hallo TestVNet4 tooTestVNet1 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="08b0c-233">Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="08b0c-234">Zorg ervoor dat Hallo gedeelde sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="08b0c-235">Hallo verbinding zal worden gemaakt na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="08b0c-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="08b0c-236">Controleer de verbinding.</span><span class="sxs-lookup"><span data-stu-id="08b0c-236">Verify your connection.</span></span> <span data-ttu-id="08b0c-237">Zie de sectie Hallo [hoe tooverify uw verbinding](#verify).</span><span class="sxs-lookup"><span data-stu-id="08b0c-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="08b0c-238"><a name="difsub"></a>Hoe tooconnect VNets die zijn opgenomen in verschillende abonnementen</span><span class="sxs-lookup"><span data-stu-id="08b0c-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="08b0c-240">In dit scenario worden TestVNet1 en TestVNet5 met elkaar verbonden.</span><span class="sxs-lookup"><span data-stu-id="08b0c-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="08b0c-241">TestVNet1 en TestVNet5 bevinden zich in een verschillend abonnement.</span><span class="sxs-lookup"><span data-stu-id="08b0c-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="08b0c-242">Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="08b0c-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="08b0c-243">Hallo verschil tussen deze stappen en de vorige set Hallo is dat een aantal configuratiestappen Hallo toobe uitgevoerd in een aparte PowerShell-sessie in de context van de tweede abonnement Hallo Hallo moet.</span><span class="sxs-lookup"><span data-stu-id="08b0c-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="08b0c-244">Met name wanneer twee Hallo abonnementen behoren toodifferent organisaties.</span><span class="sxs-lookup"><span data-stu-id="08b0c-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="08b0c-245">Stap 5: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="08b0c-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="08b0c-246">U moet voltooien [stap 1](#Step1) en [stap 2](#Step2) van Hallo vorige sectie toocreate en TestVNet1 configureren en hello VPN-Gateway voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="08b0c-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="08b0c-247">Voor deze configuratie moet zijn u niet vereist toocreate TestVNet4 uit de vorige sectie hello, hoewel als u deze maakt, wordt dit niet conflicteert met de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="08b0c-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="08b0c-248">Nadat u stap 1 en stap 2 hebt voltooid, kunt u doorgaan met stap 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="08b0c-249">Stap 6: Hallo IP-adresbereiken controleren</span><span class="sxs-lookup"><span data-stu-id="08b0c-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="08b0c-250">Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet5, niet met een van uw VNet-bereiken of de gatewaybereiken van lokale netwerk overlapt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="08b0c-251">In dit voorbeeld kunnen de virtuele netwerken Hallo toodifferent organisaties behoren.</span><span class="sxs-lookup"><span data-stu-id="08b0c-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="08b0c-252">Voor deze oefening kunt u de volgende waarden voor TestVNet5 Hallo hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="08b0c-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="08b0c-253">**Waarden voor TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="08b0c-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="08b0c-254">VNet-naam: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="08b0c-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="08b0c-255">Resourcegroep: TestRG5</span><span class="sxs-lookup"><span data-stu-id="08b0c-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="08b0c-256">Locatie: Japan - oost</span><span class="sxs-lookup"><span data-stu-id="08b0c-256">Location: Japan East</span></span>
* <span data-ttu-id="08b0c-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="08b0c-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="08b0c-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="08b0c-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="08b0c-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="08b0c-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="08b0c-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="08b0c-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="08b0c-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="08b0c-262">Openbare IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="08b0c-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="08b0c-263">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="08b0c-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="08b0c-264">Verbinding: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="08b0c-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="08b0c-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="08b0c-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="08b0c-266">Stap 7: TestVNet5 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="08b0c-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="08b0c-267">Deze stap moet worden uitgevoerd in de context van het nieuwe abonnement Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="08b0c-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="08b0c-268">Dit onderdeel kan worden uitgevoerd door Hallo beheerder in een andere organisatie die eigenaar is van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="08b0c-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="08b0c-269">Declareer uw variabelen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-269">Declare your variables.</span></span> <span data-ttu-id="08b0c-270">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="08b0c-271">Verbinding maken met toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-271">Connect toosubscription 5.</span></span> <span data-ttu-id="08b0c-272">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="08b0c-273">Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="08b0c-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="08b0c-274">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="08b0c-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="08b0c-275">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="08b0c-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="08b0c-276">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="08b0c-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="08b0c-277">Hallo subnetconfiguraties maken voor TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="08b0c-278">Maak TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="08b0c-279">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="08b0c-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="08b0c-280">Hallo gatewayconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="08b0c-281">Hallo TestVNet5-gateway maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="08b0c-282">Stap 8: Maak Hallo-verbindingen</span><span class="sxs-lookup"><span data-stu-id="08b0c-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="08b0c-283">In dit voorbeeld omdat Hallo gateways Hallo verschillende abonnementen behoren, wordt deze stap opgesplitst in twee PowerShell-sessies die zijn gemarkeerd als [abonnement 1] en [abonnement 5].</span><span class="sxs-lookup"><span data-stu-id="08b0c-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="08b0c-284">**[Abonnement 1]**  Get Hallo virtuele netwerkgateway voor abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="08b0c-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="08b0c-285">Meld u bij en verbinding tooSubscription 1 voordat Hallo volgende voorbeeld wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="08b0c-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="08b0c-286">Hallo-uitvoer van de volgende elementen Hallo kopiëren en verzenden van deze toohello beheerder van abonnement 5 via e-mail of een andere methode.</span><span class="sxs-lookup"><span data-stu-id="08b0c-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="08b0c-287">Deze twee elementen hebben waarden vergelijkbare toohello voorbeelduitvoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="08b0c-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="08b0c-288">**[Abonnement 5]**  Get Hallo virtuele netwerkgateway voor abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="08b0c-289">Meld u bij en verbinding tooSubscription 5 voordat Hallo volgende voorbeeld wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="08b0c-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="08b0c-290">Hallo-uitvoer van de volgende elementen Hallo kopiëren en verzenden van deze toohello beheerder van abonnement 1 via e-mail of een andere methode.</span><span class="sxs-lookup"><span data-stu-id="08b0c-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="08b0c-291">Deze twee elementen hebben waarden vergelijkbare toohello voorbeelduitvoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="08b0c-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="08b0c-292">**[Abonnement 1]**  Hello TestVNet1 tooTestVNet5 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="08b0c-293">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="08b0c-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="08b0c-294">Hallo verschil is hier is $vnet5gw rechtstreeks kan worden verkregen omdat deze zich in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="08b0c-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="08b0c-295">U moet toocreate een nieuw PowerShell-object met Hallo waarden gecommuniceerd vanuit abonnement 1 in bovenstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="08b0c-296">Gebruik onderstaande Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="08b0c-296">Use hello example below.</span></span> <span data-ttu-id="08b0c-297">Hallo naam-Id en gedeelde sleutel vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="08b0c-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="08b0c-298">Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="08b0c-299">Maken van een verbinding kan duren voordat een korte tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="08b0c-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="08b0c-300">Verbind tooSubscription 1 voordat Hallo volgt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="08b0c-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="08b0c-301">**[Abonnement 5]**  Hello TestVNet5 tooTestVNet1 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="08b0c-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="08b0c-302">Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet5 tooTestVNet1 maakt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="08b0c-303">Hallo hetzelfde proces voor het maken van een PowerShell-object op basis van waarden van Hallo verkregen van abonnement 1 ook hier geldt.</span><span class="sxs-lookup"><span data-stu-id="08b0c-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="08b0c-304">In deze stap overeenkomen moet u ervoor zorgen dat Hallo gedeelde sleutels.</span><span class="sxs-lookup"><span data-stu-id="08b0c-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="08b0c-305">Verbind tooSubscription 5 voordat Hallo volgt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="08b0c-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="08b0c-306"><a name="verify"></a>Hoe tooverify een verbinding</span><span class="sxs-lookup"><span data-stu-id="08b0c-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="08b0c-307"><a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet</span><span class="sxs-lookup"><span data-stu-id="08b0c-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="08b0c-308">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08b0c-308">Next steps</span></span>

* <span data-ttu-id="08b0c-309">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="08b0c-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="08b0c-310">Zie Hallo [documentatie Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="08b0c-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="08b0c-311">Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="08b0c-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
