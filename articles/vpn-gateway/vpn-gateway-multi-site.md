---
title: 'Verbinding maken met een virtueel netwerk toomultiple sites met behulp van VPN-Gateway en PowerShell: klassieke | Microsoft Docs'
description: In dit artikel begeleidt u stapsgewijs door meerdere lokale on-premises sites tooa virtueel netwerk met behulp van een VPN-Gateway voor het klassieke implementatiemodel Hallo verbinding te maken.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="4219f-103">Toevoegen van een Site-naar-Site-verbinding tooa VNet met een bestaande VPN-gatewayverbinding (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4219f-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4219f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4219f-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="4219f-105">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4219f-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="4219f-106">Dit artikel begeleidt u bij het gebruik van PowerShell tooadd Site-naar-Site (S2S)-verbindingen tooa VPN-gateway met een bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="4219f-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="4219f-107">Dit type verbinding is vaak waarnaar wordt verwezen tooas een 'multi-site'-configuratie.</span><span class="sxs-lookup"><span data-stu-id="4219f-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="4219f-108">Hallo stappen in dit artikel van toepassing toovirtual netwerken die zijn gemaakt met Hallo klassieke implementatiemodel (ook wel bekend als Service Management).</span><span class="sxs-lookup"><span data-stu-id="4219f-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="4219f-109">Deze stappen zijn niet van toepassing tooExpressRoute/Site-naar-Site naast elkaar bestaande verbinding configuraties.</span><span class="sxs-lookup"><span data-stu-id="4219f-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="4219f-110">Implementatiemodellen en -methoden</span><span class="sxs-lookup"><span data-stu-id="4219f-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="4219f-111">Deze tabel wordt bijgewerkt als er nieuwe artikelen en aanvullende hulpprogramma's beschikbaar zijn voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="4219f-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="4219f-112">Wanneer een artikel beschikbaar is, koppelen we rechtstreeks tooit uit deze tabel.</span><span class="sxs-lookup"><span data-stu-id="4219f-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="4219f-113">Over het aansluiten van</span><span class="sxs-lookup"><span data-stu-id="4219f-113">About connecting</span></span>

<span data-ttu-id="4219f-114">U kunt meerdere on-premises sites tooa één virtueel netwerk verbinden.</span><span class="sxs-lookup"><span data-stu-id="4219f-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="4219f-115">Dit is vooral aantrekkelijke voor het bouwen van oplossingen voor hybride cloud.</span><span class="sxs-lookup"><span data-stu-id="4219f-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="4219f-116">Maken van een gateway met multi-site-verbinding tooyour virtuele Azure-netwerk is vergelijkbaar toocreating andere Site-naar-Site-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="4219f-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="4219f-117">In feite kunt u een bestaande Azure VPN-gateway, zolang het Hallo-gateway is dynamische (op route gebaseerd).</span><span class="sxs-lookup"><span data-stu-id="4219f-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="4219f-118">Als u al een statische gateway verbonden tooyour virtueel netwerk hebt, kunt u Hallo gateway type toodynamic wijzigen zonder toorebuild Hallo virtueel netwerk in volgorde tooaccommodate meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="4219f-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="4219f-119">Voordat u Hallo routeringstype wijzigt, zorg dat uw on-premises VPN-gateway ondersteuning biedt voor op route gebaseerde VPN-configuraties.</span><span class="sxs-lookup"><span data-stu-id="4219f-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="4219f-120">![Multi-site-diagram](./media/vpn-gateway-multi-site/multisite.png "meerdere locaties")</span><span class="sxs-lookup"><span data-stu-id="4219f-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="4219f-121">Punten tooconsider</span><span class="sxs-lookup"><span data-stu-id="4219f-121">Points tooconsider</span></span>

<span data-ttu-id="4219f-122">**U kunt toouse Hallo portal toomake wijzigingen toothis virtueel netwerk niet.**</span><span class="sxs-lookup"><span data-stu-id="4219f-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="4219f-123">U moet toomake wijzigingen toohello netwerk-configuratiebestand in plaats van met Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="4219f-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="4219f-124">Als u wijzigingen in Hallo-portal aanbrengt, worden ze uw documentatie over de meerdere site-instellingen voor dit virtuele netwerk hebt overschreven.</span><span class="sxs-lookup"><span data-stu-id="4219f-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="4219f-125">U moet vertrouwd Hallo netwerk-configuratiebestand gebruiken door Hallo tijd inschrijvingen Hallo multi-site procedure.</span><span class="sxs-lookup"><span data-stu-id="4219f-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="4219f-126">Echter, als er meerdere personen op uw netwerkconfiguratie werkt, moet u ervoor dat iedereen op de hoogte van deze beperking toomake.</span><span class="sxs-lookup"><span data-stu-id="4219f-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="4219f-127">Dit betekent niet dat u de portal Hallo helemaal niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4219f-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="4219f-128">U kunt deze gebruiken voor alle andere behalve configuratie wijzigingen toothis bepaald virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="4219f-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4219f-129">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4219f-129">Before you begin</span></span>

<span data-ttu-id="4219f-130">Voordat u begint met de configuratie, Controleer of u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4219f-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="4219f-131">Compatibele VPN-hardware voor elke lokale locatie.</span><span class="sxs-lookup"><span data-stu-id="4219f-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="4219f-132">Controleer [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md) tooverify als Hallo-apparaat dat u wilt dat toouse iets waarvan bekend toobe compatibel is.</span><span class="sxs-lookup"><span data-stu-id="4219f-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="4219f-133">Een extern gericht openbaar IPv4-IP-adres voor elke VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4219f-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="4219f-134">Hallo IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="4219f-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="4219f-135">Dit is vereiste.</span><span class="sxs-lookup"><span data-stu-id="4219f-135">This is requirement.</span></span>
* <span data-ttu-id="4219f-136">U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4219f-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4219f-137">Zorg ervoor dat u Hallo Service Management (SM) versie in toevoeging toohello Resource Manager-versie installeert.</span><span class="sxs-lookup"><span data-stu-id="4219f-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="4219f-138">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4219f-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="4219f-139">Iemand die wordt getoond hoe u goed configureren van uw VPN-hardware.</span><span class="sxs-lookup"><span data-stu-id="4219f-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="4219f-140">Hebt u toohave een sterke begrijpt hoe tooconfigure uw VPN-apparaat of werk met iemand die biedt.</span><span class="sxs-lookup"><span data-stu-id="4219f-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="4219f-141">Hallo IP-adresbereiken dat u toouse voor het virtuele netwerk wilt (als u dit nog niet hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="4219f-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="4219f-142">Hallo IP-adresbereiken voor elk Hallo lokale netwerksites die u een verbinding met maken hebt.</span><span class="sxs-lookup"><span data-stu-id="4219f-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="4219f-143">U moet toomake ervoor dat Hallo IP-voor elk van de lokale netwerksites Hallo adresbereiken dat u wilt dat tooconnect toodo niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="4219f-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="4219f-144">Anders weigert Hallo portal of REST-API Hallo Hallo-configuratie die u wilt uploaden.</span><span class="sxs-lookup"><span data-stu-id="4219f-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="4219f-145">Bijvoorbeeld, als er twee lokale netwerksites dat beide Hallo IP-adresbereik 10.2.3.0/24 bevatten en u een pakket met een doeladres 10.2.3.3 hebt, wouldn't Azure weten welke site die u wilt dat toosend Hallo pakket toobecause Hallo-adresbereiken zijn overlappende.</span><span class="sxs-lookup"><span data-stu-id="4219f-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="4219f-146">problemen met tooprevent routing, Azure is niet toegestaan tooupload een configuratiebestand met overlappende bereiken.</span><span class="sxs-lookup"><span data-stu-id="4219f-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="4219f-147">1. Een Site-naar-Site VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="4219f-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="4219f-148">Als u al een Site-naar-Site VPN met een gateway voor dynamische routering geweldig!</span><span class="sxs-lookup"><span data-stu-id="4219f-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="4219f-149">U kunt verdergaan te[Hallo virtueel netwerk configuratie-instellingen exporteren](#export).</span><span class="sxs-lookup"><span data-stu-id="4219f-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="4219f-150">Als dat niet Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="4219f-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="4219f-151">Als u al een virtueel netwerk van de Site-naar-Site hebt, maar een statische routering (op beleid gebaseerd)-gateway heeft:</span><span class="sxs-lookup"><span data-stu-id="4219f-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="4219f-152">Wijzig uw gateway type toodynamic routering.</span><span class="sxs-lookup"><span data-stu-id="4219f-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="4219f-153">Een VPN voor meerdere locaties is een (ook wel bekend als op route gebaseerd) gateway voor dynamische routering vereist.</span><span class="sxs-lookup"><span data-stu-id="4219f-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="4219f-154">toochange uw gateway typt, maar u zult toofirst verwijderen Hallo bestaande gateway nodig en vervolgens een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="4219f-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="4219f-155">Zie voor instructies [hoe toochange routering VPN-type voor uw gateway Hallo](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="4219f-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="4219f-156">De nieuwe gateway configureren en uw VPN-tunnel maken.</span><span class="sxs-lookup"><span data-stu-id="4219f-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="4219f-157">Zie voor instructies [een VPN-Gateway configureren in de klassieke Azure-Portal Hallo](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="4219f-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="4219f-158">Wijzig eerst uw gateway type toodynamic routering.</span><span class="sxs-lookup"><span data-stu-id="4219f-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="4219f-159">Als u geen Site-naar-Site virtueel netwerk hebt:</span><span class="sxs-lookup"><span data-stu-id="4219f-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="4219f-160">Uw Site-naar-Site virtueel netwerk maken met deze instructies: [een virtueel netwerk maken met een Site-naar-Site VPN-verbinding in de klassieke Azure-Portal Hallo](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="4219f-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="4219f-161">Configureren van een gateway voor dynamische routering met behulp van deze instructies: [configureren van een VPN-Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="4219f-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="4219f-162">Ervoor tooselect worden **dynamische routering** voor uw Gatewaytype.</span><span class="sxs-lookup"><span data-stu-id="4219f-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="4219f-163"><a name="export"></a>2. Hallo netwerk configuratiebestand exporteren</span><span class="sxs-lookup"><span data-stu-id="4219f-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="4219f-164">Exporteer het bestand met de Azure-netwerk door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="4219f-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="4219f-165">U kunt Hallo-locatie van Hallo tooexport tooa verschillende bestandslocatie indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4219f-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="4219f-166">3. Open Hallo netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="4219f-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="4219f-167">Configuratiebestand van het Hallo-netwerk dat u hebt gedownload in de laatste stap Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="4219f-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="4219f-168">Een xml-editor die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4219f-168">Use any xml editor that you like.</span></span> <span data-ttu-id="4219f-169">Hallo-bestand ziet er vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="4219f-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="4219f-170">4. Verwijzingen naar meerdere toevoegen</span><span class="sxs-lookup"><span data-stu-id="4219f-170">4. Add multiple site references</span></span>
<span data-ttu-id="4219f-171">Wanneer u toevoegen of verwijderen van de referentie-informatie voor site, zult u configuratiewijzigingen aanbrengt toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="4219f-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="4219f-172">Een nieuwe lokale siteverwijzing toevoegen activeert Azure toocreate een nieuwe tunnel.</span><span class="sxs-lookup"><span data-stu-id="4219f-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="4219f-173">In onderstaande Hallo voorbeeld is Hallo netwerkconfiguratie voor een enkele site-verbinding.</span><span class="sxs-lookup"><span data-stu-id="4219f-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="4219f-174">Hallo-bestand opslaan nadat u uw wijzigingen hebt aangebracht.</span><span class="sxs-lookup"><span data-stu-id="4219f-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="4219f-175">tooadd aanvullende verwijzingen naar websites (een configuratie met meerdere sites maken), toevoegen gewoon 'LocalNetworkSiteRef' extra regels, zoals weergegeven in Hallo voorbeeld hieronder:</span><span class="sxs-lookup"><span data-stu-id="4219f-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="4219f-176">5. Importbestand Hallo netwerk configuratie</span><span class="sxs-lookup"><span data-stu-id="4219f-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="4219f-177">Hallo netwerk-configuratiebestand importeren.</span><span class="sxs-lookup"><span data-stu-id="4219f-177">Import hello network configuration file.</span></span> <span data-ttu-id="4219f-178">Als u dit bestand met de Hallo wijzigingen importeert, worden nieuwe tunnels Hallo wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4219f-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="4219f-179">Hallo-tunnels gebruikt Hallo dynamische gateway die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4219f-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="4219f-180">U kunt ofwel Hallo klassieke portal of PowerShell tooimport Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="4219f-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="4219f-181">6. Downloaden van sleutels</span><span class="sxs-lookup"><span data-stu-id="4219f-181">6. Download keys</span></span>
<span data-ttu-id="4219f-182">Als uw nieuwe tunnels zijn toegevoegd, moet u Hallo PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Hallo IPsec/IKE vooraf gedeelde sleutels gebruiken voor elke tunnel.</span><span class="sxs-lookup"><span data-stu-id="4219f-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="4219f-183">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4219f-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="4219f-184">Als u liever, kunt u ook hello gebruiken *ophalen Virtual Network Gateway gedeelde sleutel* REST-API tooget Hallo vooraf gedeelde sleutels.</span><span class="sxs-lookup"><span data-stu-id="4219f-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="4219f-185">7. Controleer uw verbindingen</span><span class="sxs-lookup"><span data-stu-id="4219f-185">7. Verify your connections</span></span>
<span data-ttu-id="4219f-186">Controleer de status van Hallo tunnel voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="4219f-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="4219f-187">Na het downloaden van Hallo sleutels voor elke tunnel, moet u tooverify verbindingen.</span><span class="sxs-lookup"><span data-stu-id="4219f-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="4219f-188">Gebruik 'Get-AzureVnetConnection' tooget een lijst van het virtuele netwerk tunnels, zoals getoond in Hallo in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4219f-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="4219f-189">VNet1 is de naam Hallo Hallo VNet.</span><span class="sxs-lookup"><span data-stu-id="4219f-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="4219f-190">Voorbeeld geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="4219f-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="4219f-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4219f-191">Next steps</span></span>

<span data-ttu-id="4219f-192">toolearn meer informatie over VPN-Gateways, Zie [over VPN-Gateways](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="4219f-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
