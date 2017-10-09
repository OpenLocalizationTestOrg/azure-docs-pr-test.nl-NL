---
title: 'Verbinding maken met een computer tooan punt-naar-Site met virtuele Azure-netwerk en certificaat gebaseerde verificatie: PowerShell | Microsoft Docs'
description: Veilig verbinding maken met een computer tooyour virtueel netwerk door het maken van een punt-naar-Site VPN-gatewayverbinding certificaatauthenticatie wordt gebruikt. In dit artikel is van toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruikt.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="5a94a-104">Een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a94a-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="5a94a-105">Dit artikel laat zien hoe toocreate een VNet met een punt-naar-Site-verbinding in Hallo Resource Manager deployment model met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a94a-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="5a94a-106">Deze configuratie maakt gebruik van certificaten tooauthenticate Hallo client verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="5a94a-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="5a94a-107">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="5a94a-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a94a-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5a94a-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="5a94a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a94a-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="5a94a-110">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5a94a-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="5a94a-111">Een punt-naar-Site (P2S) VPN-gateway kunt u een beveiligde verbinding tooyour virtueel netwerk maken van een afzonderlijke clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="5a94a-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="5a94a-112">Punt-naar-Site VPN-verbindingen zijn handig als u wilt dat tooconnect tooyour VNet vanaf een externe locatie, zoals wanneer u vanaf thuis of een conferentie zijn teleforenzen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="5a94a-113">Een P2S-VPN is ook een uitstekende oplossing toouse in plaats van een Site-naar-Site VPN-wanneer u slechts enkele clients hebt die tooconnect tooa VNet nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="5a94a-114">Maakt gebruik van P2S Hallo SSTP Secure Socket Tunneling Protocol (), die een VPN op basis van een SSL-protocol.</span><span class="sxs-lookup"><span data-stu-id="5a94a-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="5a94a-115">Een P2S-VPN-verbinding tot stand is gebracht vanaf Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="5a94a-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Verbinding maken met een computer tooan Azure VNet - verbindingsdiagram voor punt-naar-Site](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="5a94a-117">Punt-naar-Site certificaat verificatie verbindingen vereisen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5a94a-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="5a94a-118">Een RouteBased VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="5a94a-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="5a94a-119">Hallo openbare sleutel (.cer-bestand) voor een basiscertificaat dat geüpload tooAzure is.</span><span class="sxs-lookup"><span data-stu-id="5a94a-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="5a94a-120">Zodra het Hallo-certificaat is geüpload, wordt beschouwd als een vertrouwd certificaat en wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="5a94a-121">Een clientcertificaat dat is gegenereerd op basis van het basiscertificaat Hallo en geïnstalleerd op elke clientcomputer waarmee verbinding wordt gemaakt van toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="5a94a-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="5a94a-122">Dit certificaat wordt gebruikt voor clientverificatie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="5a94a-123">Een configuratiepakket voor de VPN-client.</span><span class="sxs-lookup"><span data-stu-id="5a94a-123">A VPN client configuration package.</span></span> <span data-ttu-id="5a94a-124">Hallo VPN-clientpakket configuratie bevat Hallo benodigde gegevens voor het Hallo client tooconnect toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="5a94a-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="5a94a-125">Hallo pakket configureert u het bestaande VPN-client hello, dat systeemeigen toohello Windows-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="5a94a-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="5a94a-126">Elke client die verbinding maakt, moet worden geconfigureerd met behulp van het configuratiepakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="5a94a-127">Punt-naar-site-verbindingen hebben geen VPN-apparaat of on-premises openbaar IP-adres nodig.</span><span class="sxs-lookup"><span data-stu-id="5a94a-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="5a94a-128">Hallo VPN-verbinding wordt gemaakt via SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="5a94a-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="5a94a-129">Aan de serverzijde hello ondersteunen wij SSTP versies 1.0, 1.1 en 1.2.</span><span class="sxs-lookup"><span data-stu-id="5a94a-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="5a94a-130">Hallo-client bepaalt welke versie toouse.</span><span class="sxs-lookup"><span data-stu-id="5a94a-130">hello client decides which version toouse.</span></span> <span data-ttu-id="5a94a-131">Voor Windows 8.1 en hoger, gebruikt SSTP standaard 1.2.</span><span class="sxs-lookup"><span data-stu-id="5a94a-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="5a94a-132">Zie voor meer informatie over punt-naar-Site-verbindingen Hallo [punt-naar-Site Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5a94a-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="5a94a-133">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5a94a-133">Before beginning</span></span>

* <span data-ttu-id="5a94a-134">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5a94a-135">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="5a94a-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="5a94a-136">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a94a-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5a94a-137">Zie voor meer informatie over het installeren van de PowerShell-cmdlets [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a94a-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="5a94a-138"><a name="example"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="5a94a-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="5a94a-139">Hallo voorbeeld waarden toocreate een testomgeving gebruiken of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5a94a-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="5a94a-140">We Hallo variabelen ingesteld in de sectie [1](#declare) van Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="5a94a-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="5a94a-141">U kunt stappen hello gebruiken als een procedure en gebruik Hallo waarden niet wijzigen, of ze tooreflect wijzigen uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5a94a-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="5a94a-142">**Naam: VNet1**</span><span class="sxs-lookup"><span data-stu-id="5a94a-142">**Name: VNet1**</span></span>
* <span data-ttu-id="5a94a-143">**Adresruimte: 192.168.0.0/16** en **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="5a94a-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="5a94a-144">In dit voorbeeld gebruiken we meer dan één adresruimte tooillustrate die deze configuratie met meerdere adresruimten werkt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="5a94a-145">Meerdere adresruimten zijn echter niet vereist voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="5a94a-146">**Subnetnaam: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="5a94a-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="5a94a-147">**Subnetadresbereik: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="5a94a-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="5a94a-148">**Subnetnaam: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="5a94a-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="5a94a-149">**Subnetadresbereik: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="5a94a-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="5a94a-150">**Subnetnaam: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="5a94a-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="5a94a-151">de subnetnaam Hello *GatewaySubnet* is verplicht voor Hallo VPN-gateway toowork.</span><span class="sxs-lookup"><span data-stu-id="5a94a-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="5a94a-152">**Adresbereik GatewaySubnet: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="5a94a-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="5a94a-153">**VPN-clientadresgroep: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="5a94a-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="5a94a-154">VPN-clients die verbinding maken via deze punt-naar-Site-verbinding VNet toohello ontvangen een IP-adres van VPN-clientadresgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="5a94a-155">**Abonnement:** als u meer dan één abonnement hebt, Controleer of u de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="5a94a-156">**Resourcegroep: TestRG**</span><span class="sxs-lookup"><span data-stu-id="5a94a-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="5a94a-157">**Locatie: VS - oost**</span><span class="sxs-lookup"><span data-stu-id="5a94a-157">**Location: East US**</span></span>
* <span data-ttu-id="5a94a-158">**DNS-Server: IP-adres** van Hallo DNS-server wilt u toouse voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="5a94a-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="5a94a-159">**Gatewaynaam: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="5a94a-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="5a94a-160">**Openbare IP-naam: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="5a94a-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="5a94a-161">**VPNType: op route gebaseerd**</span><span class="sxs-lookup"><span data-stu-id="5a94a-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="5a94a-162"><a name="declare"></a>1. Aanmelden en variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="5a94a-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="5a94a-163">In deze sectie aanmelden en declareren Hallo waarden voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="5a94a-164">Hallo gedeclareerd waarden in voorbeeldscripts hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="5a94a-165">Hallo waarden tooreflect uw eigen omgeving wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="5a94a-166">Of u kunt gebruiken Hallo waarden gedeclareerd en Hallo stappen doorlopen wijze van oefening maakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="5a94a-167">Open de PowerShell-console met verhoogde bevoegdheden en meld u bij tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5a94a-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="5a94a-168">Deze cmdlet wordt u gevraagd om inloggegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="5a94a-169">Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell zijn.</span><span class="sxs-lookup"><span data-stu-id="5a94a-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="5a94a-170">Haal een lijst met uw Azure-abonnementen op.</span><span class="sxs-lookup"><span data-stu-id="5a94a-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="5a94a-171">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="5a94a-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="5a94a-172">Hallo-variabelen die u wilt dat toouse declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="5a94a-173">Gebruik hello voorbeeld te volgen, vervangen door Hallo waarden voor uw eigen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5a94a-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="5a94a-174"><a name="ConfigureVNet"></a>2. Een VNet configureren</span><span class="sxs-lookup"><span data-stu-id="5a94a-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="5a94a-175">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5a94a-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="5a94a-176">Hallo subnetconfiguraties maken voor Hallo virtueel netwerk, en ze naming *FrontEnd*, *back-end*, en *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="5a94a-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="5a94a-177">Deze voorvoegsels moeten deel uitmaken van Hallo VNet-adresruimte die u gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="5a94a-178">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="5a94a-178">Create hello virtual network.</span></span>

  <span data-ttu-id="5a94a-179">In dit voorbeeld zijn Hallo DNS-server is optioneel.</span><span class="sxs-lookup"><span data-stu-id="5a94a-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="5a94a-180">Het opgeven van een waarde betekent niet dat er een nieuwe DNS-server wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="5a94a-181">Hallo moet DNS-server IP-adres dat u opgeeft een DNS-server die u kunt Hallo namen omzetten voor Hallo resources die u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="5a94a-182">In dit voorbeeld wordt een particulier IP-adres gebruikt, maar is het waarschijnlijk dat dit geen Hallo IP-adres van uw DNS-server is.</span><span class="sxs-lookup"><span data-stu-id="5a94a-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="5a94a-183">Worden toouse ervoor dat uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="5a94a-184">Geef variabelen op Hallo voor Hallo virtuele netwerk die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="5a94a-185">Een VPN Gateway moet een openbaar IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="5a94a-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="5a94a-186">U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="5a94a-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="5a94a-187">Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="5a94a-188">VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="5a94a-189">U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="5a94a-190">Echter, het betekent niet dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="5a94a-191">de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="5a94a-192">Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="5a94a-193">Vraag een dynamisch toegewezen openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="5a94a-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="5a94a-194"><a name="creategateway"></a>3. Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="5a94a-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="5a94a-195">Configureren en de virtuele netwerkgateway Hallo voor uw VNet maken.</span><span class="sxs-lookup"><span data-stu-id="5a94a-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="5a94a-196">Hallo *- GatewayType* moet **Vpn** en Hallo *- VpnType* moet **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="5a94a-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="5a94a-197">Een VPN-gateway kan duren voordat too45 minuten toocomplete, afhankelijk van Hallo [gateway-sku](vpn-gateway-about-vpn-gateway-settings.md) u selecteert.</span><span class="sxs-lookup"><span data-stu-id="5a94a-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="5a94a-198"><a name="addresspool"></a>4. Hallo VPN-clientadresgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="5a94a-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="5a94a-199">Nadat het Hallo-VPN-gateway is gemaakt, kunt u Hallo VPN-clientadresgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="5a94a-200">Hallo VPN-clientadresgroep is Hallo-bereik waarvan Hallo VPN-clients een IP-adres ontvangen wanneer verbinding wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="5a94a-201">Gebruik een persoonlijk IP-adresbereik dat niet overlapt Hallo on-premises locatie waarmee u verbinding maken of met Hallo VNet dat u wilt dat tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="5a94a-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="5a94a-202">In dit voorbeeld Hallo VPN-clientadresgroep is gedeclareerd als een [variabele](#declare) in stap 1.</span><span class="sxs-lookup"><span data-stu-id="5a94a-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="5a94a-203"><a name="Certificates"></a>5. Certificaten genereren</span><span class="sxs-lookup"><span data-stu-id="5a94a-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="5a94a-204">Certificaten worden gebruikt door Azure tooauthenticate VPN-clients voor punt-naar-Site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="5a94a-205">U uploaden Hallo informatie over openbare sleutels van Hallo root certificate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5a94a-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="5a94a-206">Hallo openbare sleutel vervolgens beschouwd als 'vertrouwd'.</span><span class="sxs-lookup"><span data-stu-id="5a94a-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="5a94a-207">Clientcertificaten moeten worden gegenereerd op basis van het vertrouwde basiscertificaat Hallo en geïnstalleerd op elke clientcomputer in Hallo certificaten-huidige gebruiker/persoonlijk certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="5a94a-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="5a94a-208">Hallo-certificaat is gebruikte tooauthenticate Hallo client wanneer een verbinding toohello VNet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="5a94a-209">Als u zelfondertekende certificaten gebruikt, moeten ze worden gemaakt met behulp van specifieke parameters.</span><span class="sxs-lookup"><span data-stu-id="5a94a-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="5a94a-210">U kunt een zelfondertekend certificaat met behulp van instructies voor het Hallo maken [PowerShell en Windows 10](vpn-gateway-certificates-point-to-site.md), of als u geen Windows 10 hebt, kunt u [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="5a94a-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="5a94a-211">Het is belangrijk dat u Hallo in Hallo instructies stappen wanneer zelfondertekende basiscertificaten en clientcertificaten te genereren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="5a94a-212">Anders Hallo certificaten u genereert niet langer compatibel zijn met P2S-verbindingen en ontvangt u een verbindingsfout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="5a94a-213"><a name="cer"></a>1. Hallo cer-bestand voor het basiscertificaat Hallo verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5a94a-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="5a94a-214"><a name="generate"></a>2. Een clientcertificaat genereren</span><span class="sxs-lookup"><span data-stu-id="5a94a-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="5a94a-215"><a name="upload"></a>6. Hallo root certificate openbare sleutelinformatie uploaden</span><span class="sxs-lookup"><span data-stu-id="5a94a-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="5a94a-216">Controleer of het maken van de VPN-gateway is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5a94a-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="5a94a-217">Nadat deze is voltooid, kunt u Hallo cer-bestand (met daarin de openbare sleutelinformatie Hallo) voor een vertrouwd basiscertificaat certificaat tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="5a94a-218">Zodra a.cer bestand is geüpload, Azure kan worden gebruikt tooauthenticate-clients die een clientcertificaat dat is gegenereerd op basis van het vertrouwde basiscertificaat Hallo hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="5a94a-219">U kunt extra vertrouwde basis-certificaatbestanden - up tooa totaal van 20 - later uploaden, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5a94a-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="5a94a-220">Hallo-variabele voor de certificaatnaam van het, Hallo waarde vervangen door uw eigen declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="5a94a-221">Hallo-bestandspad vervangen door uw eigen en voer vervolgens Hallo-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a94a-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="5a94a-222">Hallo openbare sleutelinformatie tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="5a94a-223">Zodra het Hallo-certificaatinformatie is geüpload, beschouwt Azure deze toobe een vertrouwd basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5a94a-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="5a94a-224"><a name="clientconfig"></a>7. Hallo VPN-clientpakket configuratie downloaden</span><span class="sxs-lookup"><span data-stu-id="5a94a-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="5a94a-225">tooconnect tooa VNet met een punt-naar-Site VPN, moet elke client installeren met het een client-configuratiepakket dat Hallo systeemeigen VPN-client met Hallo-instellingen configureert en bestanden die nodig zijn tooconnect toohello virtueel netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="5a94a-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="5a94a-226">Hallo VPN-clientpakket configuratie Hallo systeemeigen Windows VPN-client configureert, wordt een nieuwe of andere VPN-client niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="5a94a-227">Kunt u dezelfde configuratie van VPN-client van het pakket op elke clientcomputer hello, zolang het Hallo-versie komt overeen met de Hallo-architectuur voor Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="5a94a-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="5a94a-228">Voor de lijst van de Hallo van client-besturingssystemen die worden ondersteund, Zie Hallo [punt-naar-Site-verbindingen Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5a94a-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="5a94a-229">Nadat het Hallo-gateway is gemaakt, kunt u genereren en Hallo configuratie clientpakket downloaden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="5a94a-230">In dit voorbeeld downloads Hallo-pakket voor 64-bits clients.</span><span class="sxs-lookup"><span data-stu-id="5a94a-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="5a94a-231">Als u toodownload Hallo 32-bits client wilt, vervangen door 'Amd64' 'x86'.</span><span class="sxs-lookup"><span data-stu-id="5a94a-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="5a94a-232">U kunt Hallo VPN-client ook downloaden via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5a94a-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="5a94a-233">Kopieer en plak Hallo-koppeling die tooa web browser toodownload Hallo pakket, wordt gelet op de tooremove Hallo aanhalingstekens rond Hallo koppeling wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="5a94a-234">Download en installeer Hallo-pakket op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="5a94a-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="5a94a-235">Als u een SmartScreen-melding ziet, klikt u op **Meer info** en vervolgens op **Toch uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="5a94a-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="5a94a-236">U kunt ook Hallo pakket tooinstall opslaan op andere clientcomputers.</span><span class="sxs-lookup"><span data-stu-id="5a94a-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="5a94a-237">Op de clientcomputer hello, te navigeren**netwerkinstellingen** en klik op **VPN**.</span><span class="sxs-lookup"><span data-stu-id="5a94a-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="5a94a-238">Hallo VPN-verbinding bevat Hallo Hallo virtueel netwerk dat deze verbinding met maakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="5a94a-239"><a name="clientcertificate"></a>8. Een geëxporteerd clientcertificaat installeren</span><span class="sxs-lookup"><span data-stu-id="5a94a-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="5a94a-240">Als u wilt een P2S toocreate verbinding vanaf een clientcomputer dan Hallo u toogenerate Hallo clientcertificaten gebruikt, moet u een clientcertificaat tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5a94a-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="5a94a-241">Als u een clientcertificaat installeert, moet u Hallo wachtwoord dat is gemaakt tijdens het Hallo-clientcertificaat is geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="5a94a-242">Het is doorgaans simpelweg het gevolg van te dubbelklikken op Hallo-certificaat en te installeren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="5a94a-243">Zorg ervoor dat het Hallo-clientcertificaat is geëxporteerd als een .pfx-bestand samen met de Hallo volledige certificaatketen (dit is standaard Hallo).</span><span class="sxs-lookup"><span data-stu-id="5a94a-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="5a94a-244">Anders Hallo root-certificaatgegevens niet aanwezig is op de clientcomputer Hallo en Hallo-client niet kan tooauthenticate goed.</span><span class="sxs-lookup"><span data-stu-id="5a94a-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="5a94a-245">Zie [Een geëxporteerd clientcertificaat installeren](vpn-gateway-certificates-point-to-site.md#install) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="5a94a-246"><a name="connect"></a>9. Verbinding maken met tooAzure</span><span class="sxs-lookup"><span data-stu-id="5a94a-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="5a94a-247">tooconnect tooyour VNet, op de clientcomputer hello, gaat u tooVPN verbindingen en zoek Hallo VPN-verbinding die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="5a94a-248">Dit sjabloon heet Hallo dezelfde naam als het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a94a-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="5a94a-249">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="5a94a-249">Click **Connect**.</span></span> <span data-ttu-id="5a94a-250">Een pop-upbericht lijkt dat toousing Hallo certificaat verwijst.</span><span class="sxs-lookup"><span data-stu-id="5a94a-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="5a94a-251">Klik op **doorgaan** toouse verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="5a94a-252">Op Hallo **verbinding** statuspagina, klikt u op **Connect** toostart Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="5a94a-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="5a94a-253">Als u ziet een **certificaat selecteren** scherm, controleert u of dat het clientcertificaat Hallo Hallo een gewenste toouse tooconnect is.</span><span class="sxs-lookup"><span data-stu-id="5a94a-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="5a94a-254">Als dit niet het geval is, Hallo pijl-omlaag tooselect Hallo juiste certificaat te gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a94a-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN-client verbinding maakt tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="5a94a-256">De verbinding is tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="5a94a-256">Your connection is established.</span></span>

  ![Verbinding tot stand gebracht](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="5a94a-258">Problemen met P2S-verbindingen oplossen</span><span class="sxs-lookup"><span data-stu-id="5a94a-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="5a94a-259"><a name="verify"></a>10. De verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="5a94a-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="5a94a-260">tooverify uw VPN-verbinding is actief en open een opdrachtprompt met verhoogde bevoegdheid en voer *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="5a94a-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="5a94a-261">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="5a94a-261">View hello results.</span></span> <span data-ttu-id="5a94a-262">U ziet dat Hallo IP-adres die u hebt ontvangen een Hallo adressen binnen Hallo punt-naar-Site VPN-Client-adresgroep die u hebt opgegeven in uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="5a94a-263">Hallo resultaten zijn vergelijkbaar toothis voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5a94a-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="5a94a-264"><a name="connectVM"></a>Verbinding maken met tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5a94a-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="5a94a-265"><a name="addremovecert"></a>Een basiscertificaat toevoegen of verwijderen</span><span class="sxs-lookup"><span data-stu-id="5a94a-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="5a94a-266">U kunt vertrouwde basiscertificaat toevoegen in en verwijderen uit Azure.</span><span class="sxs-lookup"><span data-stu-id="5a94a-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="5a94a-267">Wanneer u een basiscertificaat verwijdert, clients die een certificaat dat is gegenereerd op basis van het basiscertificaat Hallo kunnen niet worden geverifieerd en niet kunnen tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5a94a-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="5a94a-268">Als u wilt dat een client tooauthenticate en verbinding maakt, moet u een nieuw clientcertificaat gegenereerd op basis van een basiscertificaat dat wordt vertrouwd (geüploade) tooAzure tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5a94a-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="5a94a-269"><a name="addtrustedroot"></a>tooadd een vertrouwd basiscertificaat</span><span class="sxs-lookup"><span data-stu-id="5a94a-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="5a94a-270">U kunt toevoegen, too20 root certificate .cer bestanden tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5a94a-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="5a94a-271">Hallo volgende stappen help u een basiscertificaat toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5a94a-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="5a94a-272"><a name="certmethod1"></a>Methode 1</span><span class="sxs-lookup"><span data-stu-id="5a94a-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="5a94a-273">Dit is Hallo efficiëntste methode tooupload een basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5a94a-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="5a94a-274">Hallo .cer-bestand tooupload voorbereiden:</span><span class="sxs-lookup"><span data-stu-id="5a94a-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="5a94a-275">Hallo-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-275">Upload hello file.</span></span> <span data-ttu-id="5a94a-276">U kunt slechts één bestand tegelijk uploaden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="5a94a-277">tooverify dat bestand Hallo-certificaat geüpload:</span><span class="sxs-lookup"><span data-stu-id="5a94a-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="5a94a-278"><a name="certmethod2"></a>Methode 2</span><span class="sxs-lookup"><span data-stu-id="5a94a-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="5a94a-279">Deze methode is een aantal extra stappen dan methode 1, maar heeft hetzelfde resultaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="5a94a-280">Het is opgenomen als u tooview Hallo certificaatgegevens nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5a94a-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="5a94a-281">Maak en Hallo nieuwe root certificate tooadd tooAzure voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="5a94a-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="5a94a-282">Hallo openbare sleutel niet exporteren als een Base-64 X.509 gecodeerde (. CER) en open het met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="5a94a-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="5a94a-283">Kopieer Hallo waarden, zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a94a-283">Copy hello values, as shown in hello following example:</span></span>

  ![certificaat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="5a94a-285">Bij het kopiëren van gegevens van het certificaat hello, zorg er dan voor dat u de tekst hello kopiëren als één continue regel zonder regelterugloop of regelinvoer.</span><span class="sxs-lookup"><span data-stu-id="5a94a-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="5a94a-286">U moet mogelijk toomodify uw weergave in Hallo text editor too'Show symbool/weergeven alle tekens toosee Hallo regeleinde retourneert en regelinvoertekens.</span><span class="sxs-lookup"><span data-stu-id="5a94a-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="5a94a-287">Hallo certificaatnaam en belangrijke informatie opgeven als een variabele.</span><span class="sxs-lookup"><span data-stu-id="5a94a-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="5a94a-288">Hallo gegevens vervangen door uw eigen, zoals weergegeven in Hallo volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5a94a-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="5a94a-289">Hallo nieuwe basiscertificaat toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-289">Add hello new root certificate.</span></span> <span data-ttu-id="5a94a-290">U kunt slechts één certificaat tegelijk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="5a94a-291">U kunt controleren dat Hallo nieuwe certificaat correct is toegevoegd met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a94a-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="5a94a-292"><a name="removerootcert"></a>tooremove een basiscertificaat</span><span class="sxs-lookup"><span data-stu-id="5a94a-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="5a94a-293">Hallo variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="5a94a-294">Hallo-certificaat verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="5a94a-295">Gebruik Hallo na voorbeeld tooverify die Hallo certificaat is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="5a94a-296"><a name="revoke"></a>Een clientcertificaat intrekken</span><span class="sxs-lookup"><span data-stu-id="5a94a-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="5a94a-297">U kunt clientcertificaten intrekken.</span><span class="sxs-lookup"><span data-stu-id="5a94a-297">You can revoke client certificates.</span></span> <span data-ttu-id="5a94a-298">Hallo certificaat intrekkingslijst kunt u tooselectively weigeren op basis van afzonderlijke clientcertificaten punt-naar-Site-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="5a94a-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="5a94a-299">Dit is anders van het verwijderen van een vertrouwd basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5a94a-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="5a94a-300">Als u een certificaat vertrouwd basiscertificaat .cer van Azure verwijdert, trekt het Hallo-toegang voor alle clientcertificaten gegenereerd/ondertekend door Hallo ingetrokken basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="5a94a-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="5a94a-301">Intrekken van een clientcertificaat, staat in plaats van het basiscertificaat hello, Hallo andere certificaten die zijn gegenereerd uit Hallo root certificate toocontinue toobe gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="5a94a-302">Hallo gebruikelijk is toouse Hallo certificaat toomanage toegang tot de hoofdmap op team of organisatie niveaus, tijdens het gebruik van de ingetrokken clientcertificaten voor verfijnd toegangsbeheer op afzonderlijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5a94a-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="5a94a-303"><a name="revokeclientcert"></a>een clientcertificaat toorevoke</span><span class="sxs-lookup"><span data-stu-id="5a94a-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="5a94a-304">Hallo-client de vingerafdruk van certificaat ophalen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="5a94a-305">Zie voor meer informatie [hoe tooretrieve vingerafdruk van een certificaat Hallo](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a94a-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="5a94a-306">Hallo informatie tooa teksteditor kopiëren en verwijdert alle spaties zodat deze een doorlopend tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5a94a-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="5a94a-307">Deze tekenreeks is gedeclareerd als een variabele in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="5a94a-308">Hallo variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-308">Declare hello variables.</span></span> <span data-ttu-id="5a94a-309">Zorg ervoor dat toodeclare Hallo vingerafdruk dat u hebt opgehaald in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a94a-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="5a94a-310">Hallo vingerafdruk toohello lijst met ingetrokken certificaten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="5a94a-311">'Geslaagd' ziet u wanneer Hallo vingerafdruk is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="5a94a-312">Controleer of dat vingerafdruk Hallo toohello certificaatintrekkingslijst is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5a94a-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="5a94a-313">Nadat het Hallo-vingerafdruk is toegevoegd, kan Hallo certificaat niet langer gebruikt tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5a94a-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="5a94a-314">Clients die proberen tooconnect met dit certificaat ontvangen een bericht weergegeven dat Hallo-certificaat is niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="5a94a-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="5a94a-315"><a name="reinstateclientcert"></a>een clientcertificaat tooreinstate</span><span class="sxs-lookup"><span data-stu-id="5a94a-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="5a94a-316">U kunt een clientcertificaat herstellen door het verwijderen van Hallo vingerafdruk uit Hallo lijst met ingetrokken clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="5a94a-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="5a94a-317">Hallo variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-317">Declare hello variables.</span></span> <span data-ttu-id="5a94a-318">Zorg ervoor dat u de juiste vingerafdruk Hallo voor Hallo-certificaat dat u wilt dat tooreinstate declareren.</span><span class="sxs-lookup"><span data-stu-id="5a94a-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="5a94a-319">Hallo certificaatvingerafdruk uit Hallo certificaatintrekkingslijst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="5a94a-320">Controleer of het Hallo-vingerafdruk is verwijderd uit Hallo ingetrokken lijst.</span><span class="sxs-lookup"><span data-stu-id="5a94a-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="5a94a-321"><a name="faq"></a>Veelgestelde vragen over punt-naar-site</span><span class="sxs-lookup"><span data-stu-id="5a94a-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5a94a-322">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a94a-322">Next steps</span></span>
<span data-ttu-id="5a94a-323">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a94a-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5a94a-324">Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5a94a-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="5a94a-325">toounderstand meer informatie over netwerken en virtuele machines, Zie [overzicht van Azure en Linux-VM-netwerk](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a94a-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
