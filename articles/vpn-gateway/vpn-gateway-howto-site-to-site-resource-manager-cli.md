---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: CLI | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met CLI.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="4d1b8-104">Een virtueel netwerk maken met een site-naar-site-VPN-verbinding met CLI</span><span class="sxs-lookup"><span data-stu-id="4d1b8-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="4d1b8-105">Dit artikel laat zien hoe toouse hello Azure CLI toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw lokale netwerk toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="4d1b8-106">Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="4d1b8-107">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d1b8-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d1b8-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="4d1b8-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d1b8-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="4d1b8-110">CLI</span><span class="sxs-lookup"><span data-stu-id="4d1b8-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="4d1b8-111">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4d1b8-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="4d1b8-113">Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="4d1b8-114">Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="4d1b8-115">Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4d1b8-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4d1b8-116">Before you begin</span></span>

<span data-ttu-id="4d1b8-117">Controleer of dat u criteria na voorhand Hallo hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="4d1b8-118">Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="4d1b8-119">Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="4d1b8-120">Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="4d1b8-121">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="4d1b8-122">Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="4d1b8-123">Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="4d1b8-124">Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="4d1b8-125">Controleer of dat u de meest recente versie van Hallo CLI-opdrachten (2.0 of hoger) hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="4d1b8-126">Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli) en [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4d1b8-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="4d1b8-127"><a name="example"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="4d1b8-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="4d1b8-128">Gebruik Hallo waarden toocreate een testomgeving te volgen of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="4d1b8-129"><a name="Login"></a>1. Verbinding maken met tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="4d1b8-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="4d1b8-130"><a name="rg"></a>2. Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="4d1b8-131">Hallo wordt volgende voorbeeld een resourcegroep met de naam 'TestRG1' op Hallo 'eastus' locatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="4d1b8-132">Als u al een resourcegroep in Hallo regio die u toocreate uw VNet wilt hebt, kunt u dat een in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="4d1b8-133"><a name="VNet"></a>3. Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="4d1b8-134">Als u nog een virtueel netwerk hebt, maakt u een met Hallo [az network vnet maken](/cli/azure/network/vnet#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="4d1b8-135">Wanneer u een virtueel netwerk maakt, zorg dat Hallo-adresruimten die u opgeeft niet overlappen met adresruimten Hallo die u op uw on-premises netwerk hebt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="4d1b8-136">Hallo wordt volgende voorbeeld een virtueel netwerk met de naam 'TestVNet1' en een subnet, 'Subnet1'.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="4d1b8-137">4. <a name="gwsub"></a>Hallo gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="4d1b8-138">Voor deze configuratie hebt u ook een gatewaysubnet nodig.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="4d1b8-139">Hallo virtuele netwerkgateway maakt gebruik van een gatewaysubnet dat Hallo IP-adressen die worden gebruikt door Hallo VPN-gatewayservices bevat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="4d1b8-140">Wanneer u een gatewaysubnet maakt, moet dit de naam GatewaySubnet krijgen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="4d1b8-141">Als u een andere naam kiest, maakt u wel een subnet, maar wordt dit door Azure niet als een gatewaysubnet behandeld.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="4d1b8-142">Hallo grootte van gatewaysubnet Hallo die u opgeeft, afhankelijk Hallo VPN-gateway-configuratie die u toocreate wilt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="4d1b8-143">Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet die meer adressen maakt door het selecteren van/27 of /28 bevat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="4d1b8-144">Met behulp van een groter gatewaysubnet kunt voldoende IP-adressen tooaccommodate mogelijke toekomstige configuraties.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="4d1b8-145">Gebruik Hallo [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create) opdracht toocreate hello gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="4d1b8-146"><a name="localnet"></a>5. Hallo lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="4d1b8-147">Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="4d1b8-148">U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="4d1b8-149">U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="4d1b8-150">Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="4d1b8-151">Als uw on-premises netwerk verandert, kunt u Hallo voorvoegsels eenvoudig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="4d1b8-152">Hallo volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-152">Use hello following values:</span></span>

* <span data-ttu-id="4d1b8-153">Hallo *--gateway-ip-adres* Hallo IP-adres van uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="4d1b8-154">Het VPN-apparaat kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="4d1b8-155">Hallo *--lokale adresvoorvoegsels* uw on-premises adresruimten zijn.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="4d1b8-156">Gebruik Hallo [az local-netwerkgateway maken](/cli/azure/network/local-gateway#create) opdracht tooadd een lokale netwerkgateway met meerdere adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="4d1b8-157"><a name="PublicIP"></a>6. Een openbaar IP-adres aanvragen</span><span class="sxs-lookup"><span data-stu-id="4d1b8-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="4d1b8-158">Een VPN Gateway moet een openbaar IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="4d1b8-159">U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="4d1b8-160">Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="4d1b8-161">VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="4d1b8-162">U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="4d1b8-163">Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="4d1b8-164">de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="4d1b8-165">Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="4d1b8-166">Gebruik Hallo [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create) opdracht toorequest een dynamische openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="4d1b8-167"><a name="CreateGateway"></a>7. Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="4d1b8-168">VPN-gateway van Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="4d1b8-169">Maken van een VPN-gateway kan duren too45 minuten of meer toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="4d1b8-170">Hallo volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-170">Use hello following values:</span></span>

* <span data-ttu-id="4d1b8-171">Hallo *--type gateway* voor een Site-naar-Site configuratie is *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="4d1b8-172">Hallo-Gatewaytype is altijd specifiek toohello configuratie die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="4d1b8-173">Zie [Soorten gateways](vpn-gateway-about-vpn-gateway-settings.md#gwtype) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="4d1b8-174">Hallo *--vpn-type* kan *RouteBased* (bedoeld tooas een dynamische Gateway in sommige documentatie), of *PolicyBased* (tooas een statische Gateway in sommige genoemd documentatie).</span><span class="sxs-lookup"><span data-stu-id="4d1b8-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="4d1b8-175">Hallo-instelling is specifiek toorequirements van Hallo-apparaat dat u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="4d1b8-176">Zie [Informatie over VPN-gatewayconfiguratie-instellingen](vpn-gateway-about-vpn-gateway-settings.md#vpntype) voor meer informatie over soorten VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="4d1b8-177">Selecteer Hallo dat u wilt dat toouse Gateway-SKU.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="4d1b8-178">Voor bepaalde SKU's gelden configuratiebeperkingen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="4d1b8-179">Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="4d1b8-180">Hallo VPN-gateway met Hallo maken [az vnet-netwerkgateway maken](/cli/azure/network/vnet-gateway#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="4d1b8-181">Als u deze opdracht met Hallo '--geen - wait' parameter uitvoert, kunt u niet alle feedback of de uitvoer ziet.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="4d1b8-182">Deze parameter kan Hallo gateway toocreate op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="4d1b8-183">Het duurt ongeveer 45 minuten toocreate een gateway.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="4d1b8-184"><a name="VPNDevice"></a>8. Uw VPN-apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="4d1b8-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="4d1b8-185">Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="4d1b8-186">In deze stap configureert u het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="4d1b8-187">Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4d1b8-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="4d1b8-188">Een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-188">A shared key.</span></span> <span data-ttu-id="4d1b8-189">Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="4d1b8-190">In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="4d1b8-191">Het is raadzaam dat u een complexere sleutel toouse genereert.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="4d1b8-192">Hallo openbare IP-adres van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="4d1b8-193">U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="4d1b8-194">toofind hello openbare IP-adres van uw virtuele netwerkgateway, gebruik Hallo [az netwerk openbare ip-lijst](/cli/azure/network/public-ip#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="4d1b8-195">Hallo-uitvoer is gemakkelijk te lezen, opgemaakte toodisplay Hallo lijst met openbare IP-adressen in tabelindeling.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="4d1b8-196"><a name="CreateConnection"></a>9. Hallo VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="4d1b8-197">Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw on-premises VPN-apparaat maken.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="4d1b8-198">Betalen bijzondere aandacht toohello gedeeld sleutelwaarde, die moet overeenkomen met de Hallo geconfigureerd gedeeld sleutelwaarde voor uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="4d1b8-199">Hallo verbinding maken met de Hallo [az netwerk vpn-verbinding maken](/cli/azure/network/vpn-connection#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="4d1b8-200">Na een korte tijd hello wordt de verbinding worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="4d1b8-201"><a name="toverify"></a>10. Hallo VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="4d1b8-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="4d1b8-202">Als u een andere methode tooverify toouse wilt uw verbinding, Zie [een VPN-Gateway-verbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4d1b8-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="4d1b8-203"><a name="connectVM"></a>tooconnect tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4d1b8-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="4d1b8-204"><a name="tasks"></a>Algemene taken</span><span class="sxs-lookup"><span data-stu-id="4d1b8-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="4d1b8-205">Deze sectie bevat veelgebruikte opdrachten die nuttig zijn bij het werken met site-naar-siteconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="4d1b8-206">Zie voor Hallo volledige lijst met netwerken CLI-opdrachten, [Azure CLI - netwerken](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="4d1b8-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4d1b8-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d1b8-207">Next steps</span></span>

* <span data-ttu-id="4d1b8-208">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="4d1b8-209">Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="4d1b8-210">Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4d1b8-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="4d1b8-211">Zie [Informatie over geforceerde tunneling](vpn-gateway-forced-tunneling-rm.md) voor meer informatie over geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="4d1b8-212">Zie [Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor meer informatie over maximaal beschikbare actieve verbindingen.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="4d1b8-213">Zie [Azure CLI](https://docs.microsoft.com/cli/azure/network) voor een lijst met Azure CLI-opdrachten voor netwerken.</span><span class="sxs-lookup"><span data-stu-id="4d1b8-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>