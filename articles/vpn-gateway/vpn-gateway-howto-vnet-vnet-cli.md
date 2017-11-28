---
title: 'Verbinding maken met virtuele netwerk tooanother VNet: Azure CLI | Microsoft Docs'
description: Dit artikel helpt u bij het met elkaar verbinden van virtuele netwerken met behulp van Azure Resource Manager en Azure CLI.
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="179cb-103">Een VPN-gatewayverbinding tussen VNets configureren met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="179cb-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="179cb-104">Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="179cb-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="179cb-105">Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="179cb-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="179cb-106">Bij het maken van verbinding VNets uit verschillende abonnementen behoren, Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="179cb-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="179cb-107">Hallo stappen in dit artikel toepassen toohello Resource Manager-implementatiemodel en Azure CLI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="179cb-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="179cb-108">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="179cb-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="179cb-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="179cb-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="179cb-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="179cb-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="179cb-111">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="179cb-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="179cb-112">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="179cb-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="179cb-113">Verbinding maken tussen verschillende implementatiemodellen - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="179cb-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="179cb-114">Verbinding maken tussen verschillende implementatiemodellen - PowerShell</span><span class="sxs-lookup"><span data-stu-id="179cb-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="179cb-115">Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie.</span><span class="sxs-lookup"><span data-stu-id="179cb-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="179cb-116">Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="179cb-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="179cb-117">Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooconsider deze met behulp van VNet-Peering te verbinden.</span><span class="sxs-lookup"><span data-stu-id="179cb-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="179cb-118">Bij VNet-peering wordt geen VPN-gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="179cb-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="179cb-119">Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="179cb-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="179cb-120">VNet-naar-VNet-communicatie kan worden gecombineerd met configuraties voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="179cb-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="179cb-121">Hiermee kunt u netwerktopologieën maken waarin cross-premises-connectiviteit met connectiviteit tussen virtuele netwerken, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="179cb-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Over verbindingen](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="179cb-123"><a name="why"></a>Waarom virtuele netwerken koppelen?</span><span class="sxs-lookup"><span data-stu-id="179cb-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="179cb-124">U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="179cb-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="179cb-125">**Geografische redundantie en aanwezigheid tussen regio's**</span><span class="sxs-lookup"><span data-stu-id="179cb-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="179cb-126">U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.</span><span class="sxs-lookup"><span data-stu-id="179cb-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="179cb-127">Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="179cb-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="179cb-128">Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="179cb-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="179cb-129">**Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**</span><span class="sxs-lookup"><span data-stu-id="179cb-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="179cb-130">Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere virtuele netwerken met elkaar verbonden vervaldatum tooisolation of beheervereisten.</span><span class="sxs-lookup"><span data-stu-id="179cb-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="179cb-131">Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="179cb-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="179cb-132">Welke stappen moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="179cb-132">Which set of steps should I use?</span></span>

<span data-ttu-id="179cb-133">In dit artikel ziet u twee verschillende reeksen stappen.</span><span class="sxs-lookup"><span data-stu-id="179cb-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="179cb-134">Een reeks stappen voor het [VNets die tot hetzelfde abonnement Hallo](#samesub), en een andere voor [VNets die tot verschillende abonnementen](#difsub).</span><span class="sxs-lookup"><span data-stu-id="179cb-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="179cb-135"><a name="samesub"></a>VNets verbinden die in Hallo hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="179cb-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![v2v-diagram](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="179cb-137">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="179cb-137">Before you begin</span></span>

<span data-ttu-id="179cb-138">Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="179cb-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="179cb-139">Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="179cb-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="179cb-140"><a name="Plan"></a>De IP-adresbereiken plannen</span><span class="sxs-lookup"><span data-stu-id="179cb-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="179cb-141">In de Hallo stappen te volgen, maken we twee virtuele netwerken en hun bijbehorende gatewaysubnetten en configuraties.</span><span class="sxs-lookup"><span data-stu-id="179cb-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="179cb-142">We vervolgens een VPN-verbinding maken tussen Hallo twee VNets.</span><span class="sxs-lookup"><span data-stu-id="179cb-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="179cb-143">Het is belangrijk tooplan Hallo IP-adresbereiken voor uw netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="179cb-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="179cb-144">De VNet-bereiken of de bereiken van het lokale netwerk mogen elkaar niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="179cb-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="179cb-145">In deze voorbeelden behandelen we geen DNS-server.</span><span class="sxs-lookup"><span data-stu-id="179cb-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="179cb-146">Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.</span><span class="sxs-lookup"><span data-stu-id="179cb-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="179cb-147">We gebruiken de volgende waarden in de voorbeelden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="179cb-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="179cb-148">**Waarden voor TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="179cb-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="179cb-149">VNet-naam: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="179cb-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="179cb-150">Resourcegroep: TestRG1</span><span class="sxs-lookup"><span data-stu-id="179cb-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="179cb-151">Locatie: VS - oost</span><span class="sxs-lookup"><span data-stu-id="179cb-151">Location: East US</span></span>
* <span data-ttu-id="179cb-152">TestVNet1: 10.11.0.0/16 en 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="179cb-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="179cb-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="179cb-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="179cb-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="179cb-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="179cb-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="179cb-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="179cb-157">Openbare IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="179cb-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="179cb-158">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="179cb-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="179cb-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="179cb-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="179cb-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="179cb-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="179cb-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="179cb-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="179cb-162">**Waarden voor TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="179cb-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="179cb-163">VNet-naam: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="179cb-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="179cb-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="179cb-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="179cb-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="179cb-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="179cb-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="179cb-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="179cb-168">Resourcegroep: TestRG4</span><span class="sxs-lookup"><span data-stu-id="179cb-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="179cb-169">Locatie: VS - west</span><span class="sxs-lookup"><span data-stu-id="179cb-169">Location: West US</span></span>
* <span data-ttu-id="179cb-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="179cb-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="179cb-171">Openbare IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="179cb-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="179cb-172">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="179cb-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="179cb-173">Verbinding: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="179cb-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="179cb-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="179cb-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="179cb-175"><a name="Connect"></a>Stap 1: verbinding maken met tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="179cb-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="179cb-176"><a name="TestVNet1"></a>Stap 2: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="179cb-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="179cb-177">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="179cb-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="179cb-178">TestVNet1 en Hallo subnetten voor TestVNet1 maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="179cb-179">In dit voorbeeld worden een virtueel netwerk met de naam TestVNet1 en een subnet met de naam FrontEnd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="179cb-180">Maak een extra adresruimte voor Hallo back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="179cb-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="179cb-181">Merk op dat in deze stap we Geef beide Hallo-adresruimte die we eerder hebben gemaakt, en extra adresruimte willen we tooadd Hallo.</span><span class="sxs-lookup"><span data-stu-id="179cb-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="179cb-182">Dit komt doordat Hallo [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) opdracht Hallo vorige instellingen overschreven.</span><span class="sxs-lookup"><span data-stu-id="179cb-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="179cb-183">Controleer zeker toospecify alle Hallo adresvoorvoegsels bij gebruik van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="179cb-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="179cb-184">Hallo back-end subnet maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="179cb-185">Hallo gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-185">Create hello gateway subnet.</span></span> <span data-ttu-id="179cb-186">U ziet dat Hallo gateway-subnet met de naam 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="179cb-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="179cb-187">Deze naam is verplicht.</span><span class="sxs-lookup"><span data-stu-id="179cb-187">This name is required.</span></span> <span data-ttu-id="179cb-188">In dit voorbeeld maakt Hallo gatewaysubnet gebruik van een/27.</span><span class="sxs-lookup"><span data-stu-id="179cb-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="179cb-189">Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet met meer adressen maakt door ten minste/28 of /27 selecteren.</span><span class="sxs-lookup"><span data-stu-id="179cb-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="179cb-190">Hierdoor kunt voldoende adressen tooaccommodate mogelijk aanvullende configuraties die u kunt Hallo toekomstige.</span><span class="sxs-lookup"><span data-stu-id="179cb-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="179cb-191">Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="179cb-192">U ziet dat Hallo AllocationMethod is dynamische.</span><span class="sxs-lookup"><span data-stu-id="179cb-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="179cb-193">U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="179cb-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="179cb-194">Is dynamisch toegewezen tooyour gateway.</span><span class="sxs-lookup"><span data-stu-id="179cb-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="179cb-195">De virtuele netwerkgateway Hallo voor TestVNet1 maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="179cb-196">VNet-naar-VNet-configuraties vereisen een op route gebaseerd VpnType.</span><span class="sxs-lookup"><span data-stu-id="179cb-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="179cb-197">Als u deze opdracht met Hallo '--geen - wait' parameter uitvoert, kunt u niet alle feedback of de uitvoer ziet.</span><span class="sxs-lookup"><span data-stu-id="179cb-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="179cb-198">Hallo '--geen - wait' parameter kan Hallo gateway toocreate op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="179cb-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="179cb-199">Dit betekent niet dat Hallo VPN-gateway is onmiddellijk gemaakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="179cb-200">Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van Hallo gateway-SKU die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="179cb-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="179cb-201"><a name="TestVNet4"></a>Stap 3: TestVNet4 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="179cb-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="179cb-202">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="179cb-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="179cb-203">Maak TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="179cb-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="179cb-204">Extra subnetten voor TestVNet4 maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="179cb-205">Hallo gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="179cb-206">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="179cb-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="179cb-207">Hallo TestVNet4 virtuele netwerkgateway maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="179cb-208"><a name="createconnect"></a>Stap 4: Hallo verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="179cb-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="179cb-209">U hebt nu twee VNets met VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="179cb-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="179cb-210">de volgende stap Hallo is toocreate VPN-gatewayverbindingen tussen de virtuele netwerkgateways Hallo.</span><span class="sxs-lookup"><span data-stu-id="179cb-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="179cb-211">Als u de bovenstaande voorbeelden van Hallo gebruikt, wordt uw VNet-gateways zijn in verschillende resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="179cb-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="179cb-212">Gateways zijn in verschillende resourcegroepen, u moet tooidentify als Hallo resource-id's voor elke gateway opgeven wanneer u een verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="179cb-213">Als uw vnet's in Hallo zijn dezelfde resourcegroep bevinden, kunt u Hallo [tweede set instructies](#samerg) omdat u niet toospecify Hallo resource-id hoeft.</span><span class="sxs-lookup"><span data-stu-id="179cb-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="179cb-214"><a name="diffrg"></a>tooconnect VNets die tot verschillende resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="179cb-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="179cb-215">Hallo uitvoer van de volgende opdracht Hallo Hallo Resource-ID van VNet1GW verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="179cb-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="179cb-216">Hallo zoeken in de uitvoer van Hallo ' id: ' regel.</span><span class="sxs-lookup"><span data-stu-id="179cb-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="179cb-217">Hallo waarden binnen de aanhalingstekens Hallo zijn benodigde toocreate Hallo verbinding in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="179cb-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="179cb-218">Kopieer deze waarden tooa teksteditor zoals Kladblok, zodat u ze gemakkelijk plakken kunt wanneer u de verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="179cb-219">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="179cb-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="179cb-220">Kopieer de waarden Hallo na **'id':** Hallo aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="179cb-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="179cb-221">Hallo Resource-ID van VNet4GW en kopieer Hallo waarden tooa teksteditor ophalen.</span><span class="sxs-lookup"><span data-stu-id="179cb-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="179cb-222">Hallo TestVNet1 tooTestVNet4 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="179cb-223">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="179cb-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="179cb-224">Er is een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="179cb-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="179cb-225">U kunt uw eigen waarden voor Hallo gedeelde sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="179cb-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="179cb-226">Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="179cb-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="179cb-227">Maken van een verbinding nodig is een korte tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="179cb-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="179cb-228">Hallo TestVNet4 tooTestVNet1 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="179cb-229">Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="179cb-230">Zorg ervoor dat Hallo gedeelde sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="179cb-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="179cb-231">Het duurt enkele minuten tooestablish Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="179cb-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="179cb-232">Controleer uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="179cb-232">Verify your connections.</span></span> <span data-ttu-id="179cb-233">Zie [De verbinding controleren](#verify).</span><span class="sxs-lookup"><span data-stu-id="179cb-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="179cb-234"><a name="samerg"></a>tooconnect VNets die tot Hallo dezelfde resourcegroep</span><span class="sxs-lookup"><span data-stu-id="179cb-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="179cb-235">Hallo TestVNet1 tooTestVNet4 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="179cb-236">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="179cb-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="179cb-237">Kennisgeving Hallo resourcegroepen zijn hetzelfde in de voorbeelden Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="179cb-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="179cb-238">U ziet ook een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="179cb-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="179cb-239">U kunt uw eigen waarden voor de gedeelde sleutel hello, echter Hallo gedeelde sleutel voor beide verbindingen moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="179cb-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="179cb-240">Maken van een verbinding nodig is een korte tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="179cb-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="179cb-241">Hallo TestVNet4 tooTestVNet1 verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="179cb-242">Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt.</span><span class="sxs-lookup"><span data-stu-id="179cb-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="179cb-243">Zorg ervoor dat Hallo gedeelde sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="179cb-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="179cb-244">Het duurt enkele minuten tooestablish Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="179cb-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="179cb-245">Controleer uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="179cb-245">Verify your connections.</span></span> <span data-ttu-id="179cb-246">Zie [De verbinding controleren](#verify).</span><span class="sxs-lookup"><span data-stu-id="179cb-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="179cb-247"><a name="difsub"></a>VNets verbinden die tot verschillende abonnement behoren</span><span class="sxs-lookup"><span data-stu-id="179cb-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![v2v-diagram](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="179cb-249">In dit scenario worden TestVNet1 en TestVNet5 met elkaar verbonden.</span><span class="sxs-lookup"><span data-stu-id="179cb-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="179cb-250">Hallo VNets bevinden zich verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="179cb-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="179cb-251">Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="179cb-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="179cb-252">Hallo-stappen voor deze configuratie toevoegen een extra VNet-naar-VNet-verbinding in volgorde tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="179cb-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="179cb-253"><a name="TestVNet1diff"></a>Stap 5: TestVNet1 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="179cb-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="179cb-254">Deze instructies worden overgenomen van de stappen in de voorgaande secties Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="179cb-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="179cb-255">U moet voltooien [stap 1](#Connect) en [stap 2](#TestVNet1) toocreate en configureer TestVNet1 en hello VPN-Gateway voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="179cb-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="179cb-256">Voor deze configuratie moet zijn u niet vereist toocreate TestVNet4 uit de vorige sectie hello, hoewel als u deze maakt, wordt dit niet conflicteert met de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="179cb-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="179cb-257">Nadat u stap 1 en stap 2 hebt voltooid, gaat u verder met stap 6 hieronder.</span><span class="sxs-lookup"><span data-stu-id="179cb-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="179cb-258"><a name="verifyranges"></a>Stap 6: Hallo IP-adresbereiken controleren</span><span class="sxs-lookup"><span data-stu-id="179cb-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="179cb-259">Wanneer u extra verbindingen maakt, is het belangrijk tooverify dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk niet met een van uw andere VNet-bereiken of de gatewaybereiken lokale netwerk overlapt.</span><span class="sxs-lookup"><span data-stu-id="179cb-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="179cb-260">Voor deze oefening kunt u de volgende waarden voor TestVNet5 Hallo hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="179cb-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="179cb-261">**Waarden voor TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="179cb-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="179cb-262">VNet-naam: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="179cb-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="179cb-263">Resourcegroep: TestRG5</span><span class="sxs-lookup"><span data-stu-id="179cb-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="179cb-264">Locatie: Japan - oost</span><span class="sxs-lookup"><span data-stu-id="179cb-264">Location: Japan East</span></span>
* <span data-ttu-id="179cb-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="179cb-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="179cb-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="179cb-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="179cb-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="179cb-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="179cb-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="179cb-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="179cb-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="179cb-270">Openbare IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="179cb-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="179cb-271">VPNType: op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="179cb-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="179cb-272">Verbinding: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="179cb-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="179cb-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="179cb-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="179cb-274"><a name="TestVNet5"></a>Stap 7: TestVNet5 maken en configureren</span><span class="sxs-lookup"><span data-stu-id="179cb-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="179cb-275">Deze stap moet worden uitgevoerd in de context Hallo van Hallo nieuw abonnement abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="179cb-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="179cb-276">Dit onderdeel kan worden uitgevoerd door Hallo beheerder in een andere organisatie die eigenaar is van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="179cb-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="179cb-277">tooswitch tussen abonnementen gebruik ' lijst az--alle ' toolist Hallo abonnementen beschikbaar tooyour account en gebruik vervolgens ' az account set--abonnement <subscriptionID>' tooswitch toohello abonnement dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="179cb-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="179cb-278">Zorg ervoor dat u bent verbonden tooSubscription 5 en vervolgens een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="179cb-279">Maak TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="179cb-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="179cb-280">Voeg subnetten toe.</span><span class="sxs-lookup"><span data-stu-id="179cb-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="179cb-281">Hallo gatewaysubnet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="179cb-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="179cb-282">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="179cb-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="179cb-283">Hallo TestVNet5-gateway maken</span><span class="sxs-lookup"><span data-stu-id="179cb-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="179cb-284"><a name="connections5"></a>Stap 8: Maak Hallo-verbindingen</span><span class="sxs-lookup"><span data-stu-id="179cb-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="179cb-285">We deze stap in twee CLI sessies, aangeduid als splitsen **[abonnement 1]**, en **[abonnement 5]** omdat Hallo gateways Hallo verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="179cb-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="179cb-286">tooswitch tussen abonnementen gebruik ' lijst az--alle ' toolist Hallo abonnementen beschikbaar tooyour account en gebruik vervolgens ' az account set--abonnement <subscriptionID>' tooswitch toohello abonnement dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="179cb-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="179cb-287">**[Abonnement 1]**  Aanmelden en verbinding maken met tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="179cb-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="179cb-288">Voer Hallo volgende opdracht tooget Hallo naam en de ID van Hallo Gateway vanuit Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="179cb-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="179cb-289">Kopieer de uitvoer Hallo voor ' id: '.</span><span class="sxs-lookup"><span data-stu-id="179cb-289">Copy hello output for "id:".</span></span> <span data-ttu-id="179cb-290">Hallo-ID en naam van Hallo VNet gateway (VNet1GW) toohello beheerder van abonnement 5 via e-mail of een andere methode Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="179cb-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="179cb-291">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="179cb-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="179cb-292">**[Abonnement 5]**  Aanmelden en verbinding maken met tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="179cb-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="179cb-293">Voer Hallo volgende opdracht tooget Hallo naam en de ID van Hallo Gateway vanuit Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="179cb-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="179cb-294">Kopieer de uitvoer Hallo voor ' id: '.</span><span class="sxs-lookup"><span data-stu-id="179cb-294">Copy hello output for "id:".</span></span> <span data-ttu-id="179cb-295">Hallo-ID en naam van Hallo VNet gateway (VNet5GW) toohello beheerder van abonnement 1 via e-mail of een andere methode Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="179cb-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="179cb-296">**[Abonnement 1]**  In deze stap maakt u Hallo verbinding kunt maken van tooTestVNet5 TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="179cb-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="179cb-297">U kunt uw eigen waarden voor de gedeelde sleutel hello, echter Hallo gedeelde sleutel voor beide verbindingen moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="179cb-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="179cb-298">Maken van een verbinding kan duren voordat een korte tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="179cb-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="179cb-299">Zorg ervoor dat u verbinding maakt met tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="179cb-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="179cb-300">**[Abonnement 5]**  Deze stap is vergelijkbaar toohello hierboven, behalve dat u maakt Hallo verbinding nu vanuit TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="179cb-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="179cb-301">Zorg ervoor dat Hallo gedeelde sleutels overeenkomen en of u verbinding tooSubscription 5 maken.</span><span class="sxs-lookup"><span data-stu-id="179cb-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="179cb-302"><a name="verify"></a>Hallo-verbindingen controleren</span><span class="sxs-lookup"><span data-stu-id="179cb-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="179cb-303"><a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet</span><span class="sxs-lookup"><span data-stu-id="179cb-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="179cb-304">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="179cb-304">Next steps</span></span>

* <span data-ttu-id="179cb-305">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="179cb-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="179cb-306">Zie voor meer informatie, Hallo [documentatie Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="179cb-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="179cb-307">Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="179cb-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
