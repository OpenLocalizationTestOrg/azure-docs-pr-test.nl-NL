---
title: 'Verbinding maken met de klassieke virtuele netwerken tooAzure Resource Manager VNets: PowerShell | Microsoft Docs'
description: Meer informatie over hoe toocreate een VPN-verbinding tussen het klassieke vnet's en Resource Manager-VNets met VPN-Gateway en PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="5f939-103">Virtuele netwerken van verschillende implementatiemodellen verbinden met PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f939-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="5f939-104">Dit artikel laat zien hoe tooconnect klassieke vnet's tooResource Manager VNets tooallow Hallo bronnen in Hallo afzonderlijke implementatie modellen toocommunicate met elkaar.</span><span class="sxs-lookup"><span data-stu-id="5f939-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="5f939-105">Hallo stappen in dit artikel PowerShell gebruiken, maar u kunt ook maken met deze configuratie met behulp van hello Azure-portal door Hallo artikel in deze lijst te selecteren.</span><span class="sxs-lookup"><span data-stu-id="5f939-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f939-106">Portal</span><span class="sxs-lookup"><span data-stu-id="5f939-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="5f939-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f939-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="5f939-108">Verbinding maken met een klassiek VNet tooa Resource Manager VNet is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie.</span><span class="sxs-lookup"><span data-stu-id="5f939-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="5f939-109">Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="5f939-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="5f939-110">U kunt een verbinding tussen VNets die tot verschillende abonnementen behoren en in verschillende regio's maken.</span><span class="sxs-lookup"><span data-stu-id="5f939-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="5f939-111">U kunt ook VNets die u al verbindingen tooon-premises netwerken hebt, verbinden, zolang het Hallo-gateway die is geconfigureerd met dynamische of op basis van route is.</span><span class="sxs-lookup"><span data-stu-id="5f939-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="5f939-112">Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5f939-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="5f939-113">Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooinstead overwegen deze met behulp van VNet-Peering te verbinden.</span><span class="sxs-lookup"><span data-stu-id="5f939-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="5f939-114">Bij VNet-peering wordt geen VPN-gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5f939-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="5f939-115">Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f939-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="5f939-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5f939-116">Before beginning</span></span>

<span data-ttu-id="5f939-117">Hallo volgt helpt u bij het Hallo-instellingen nodig tooconfigure een dynamisch of op route gebaseerde gateway voor elk VNet en een VPN-verbinding maken tussen Hallo gateways.</span><span class="sxs-lookup"><span data-stu-id="5f939-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="5f939-118">Deze configuratie biedt geen ondersteuning voor statische of op beleid gebaseerde gateways.</span><span class="sxs-lookup"><span data-stu-id="5f939-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5f939-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5f939-119">Prerequisites</span></span>

* <span data-ttu-id="5f939-120">Beide VNets zijn al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="5f939-121">Hallo-adresbereiken voor Hallo VNets met elkaar overlappen, of niet overlappen met een van de bereiken Hallo voor Hallo gateways mogen worden verbonden met andere verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5f939-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="5f939-122">U kunt de meest recente PowerShell-cmdlets Hallo hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5f939-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="5f939-123">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f939-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="5f939-124">Zorg ervoor dat u Hallo Service Management (SM) en Hallo Resource Manager (RM)-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="5f939-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="5f939-125"><a name="exampleref"></a>Voorbeeldinstellingen</span><span class="sxs-lookup"><span data-stu-id="5f939-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="5f939-126">U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5f939-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="5f939-127">**Klassieke VNet-instellingen**</span><span class="sxs-lookup"><span data-stu-id="5f939-127">**Classic VNet settings**</span></span>

<span data-ttu-id="5f939-128">VNet-naam = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="5f939-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="5f939-129">Locatie VS-West =</span><span class="sxs-lookup"><span data-stu-id="5f939-129">Location = West US</span></span> <br>
<span data-ttu-id="5f939-130">Adresruimten voor virtueel netwerk 10.0.0.0/24 =</span><span class="sxs-lookup"><span data-stu-id="5f939-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="5f939-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="5f939-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="5f939-132">GatewaySubnet 10.0.0.32/29 =</span><span class="sxs-lookup"><span data-stu-id="5f939-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="5f939-133">De naam van het lokale netwerk RMVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="5f939-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="5f939-134">GatewayType DynamicRouting =</span><span class="sxs-lookup"><span data-stu-id="5f939-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="5f939-135">**Resource Manager VNet-instellingen**</span><span class="sxs-lookup"><span data-stu-id="5f939-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="5f939-136">VNet-naam = RMVNet</span><span class="sxs-lookup"><span data-stu-id="5f939-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="5f939-137">Resourcegroep RG1 =</span><span class="sxs-lookup"><span data-stu-id="5f939-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="5f939-138">Virtueel netwerk-IP-adresruimten 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="5f939-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="5f939-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="5f939-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="5f939-140">GatewaySubnet 192.168.0.0/26 =</span><span class="sxs-lookup"><span data-stu-id="5f939-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="5f939-141">Locatie VS-Oost =</span><span class="sxs-lookup"><span data-stu-id="5f939-141">Location = East US</span></span> <br>
<span data-ttu-id="5f939-142">Het openbare IP-gatewaynaam gwpip =</span><span class="sxs-lookup"><span data-stu-id="5f939-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="5f939-143">Lokale netwerkgateway ClassicVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="5f939-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="5f939-144">Naam van de virtuele netwerkgateway RMGateway =</span><span class="sxs-lookup"><span data-stu-id="5f939-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="5f939-145">Gateway-IP-adresconfiguratie gwipconfig =</span><span class="sxs-lookup"><span data-stu-id="5f939-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="5f939-146"><a name="createsmgw"></a>Sectie 1: Configureer Hallo klassieke VNet</span><span class="sxs-lookup"><span data-stu-id="5f939-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="5f939-147">Deel 1: Download het configuratiebestand van uw netwerk</span><span class="sxs-lookup"><span data-stu-id="5f939-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="5f939-148">Meld u bij tooyour Azure-account in Hallo PowerShell-console met verhoogde rechten.</span><span class="sxs-lookup"><span data-stu-id="5f939-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="5f939-149">Hallo vraagt volgende cmdlet u om Hallo aanmeldingsreferenties voor uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="5f939-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="5f939-150">Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell zijn.</span><span class="sxs-lookup"><span data-stu-id="5f939-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="5f939-151">U Hallo SM PowerShell-cmdlets toocomplete dit deel van het Hallo-configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f939-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="5f939-152">Exporteer het bestand met de Azure-netwerk door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f939-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="5f939-153">U kunt Hallo-locatie van Hallo tooexport tooa verschillende bestandslocatie indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f939-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="5f939-154">Open Hallo .xml-bestand dat u hebt gedownload tooedit deze.</span><span class="sxs-lookup"><span data-stu-id="5f939-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="5f939-155">Zie voor een voorbeeld van netwerk-configuratiebestand Hallo Hallo [Network-configuratieschema](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f939-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="5f939-156">Deel 2 - Hallo gatewaysubnet controleren</span><span class="sxs-lookup"><span data-stu-id="5f939-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="5f939-157">In Hallo **VirtualNetworkSites** element, een gateway subnet tooyour VNet toevoegen als een nog niet is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="5f939-158">Als u werkt met Hallo netwerk configuratiebestand, Hallo gatewaysubnet moet de naam 'GatewaySubnet' of Azure kan niet herkennen en gebruiken als een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="5f939-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="5f939-159">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="5f939-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="5f939-160">Deel 3: de lokale netwerksite Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="5f939-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="5f939-161">lokale netwerksite Hallo die u toevoegen vertegenwoordigt Hallo RM VNet toowhich gewenste tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5f939-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="5f939-162">Voeg een **LocalNetworkSites** element toohello bestand als een nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="5f939-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="5f939-163">Op dit moment in configuratie Hallo mag Hallo VPNGatewayAddress geldig openbaar IP-adres omdat we nog Hallo gateway voor Hallo Resource Manager VNet dat nog niet hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="5f939-164">Wanneer we Hallo gateway maakt, wordt vervangen door dit tijdelijke aanduiding voor IP-adres Hallo juiste openbare IP-adres dat is toegewezen toohello RM-gateway.</span><span class="sxs-lookup"><span data-stu-id="5f939-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="5f939-165">Deel 4 – hello VNet koppelen aan de lokale netwerksite Hallo</span><span class="sxs-lookup"><span data-stu-id="5f939-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="5f939-166">In deze sectie opgegeven lokale netwerksite Hallo dat u wilt dat tooconnect VNet-naar-Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f939-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="5f939-167">In dit geval is het Hallo Resource Manager VNet dat u eerder naar verwezen.</span><span class="sxs-lookup"><span data-stu-id="5f939-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="5f939-168">Zorg ervoor dat Hallo-namen die overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="5f939-168">Make sure hello names match.</span></span> <span data-ttu-id="5f939-169">Deze stap maakt een gateway niet.</span><span class="sxs-lookup"><span data-stu-id="5f939-169">This step does not create a gateway.</span></span> <span data-ttu-id="5f939-170">Hiermee geeft u Hallo lokale netwerk die Hallo gateway maakt verbinding met.</span><span class="sxs-lookup"><span data-stu-id="5f939-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="5f939-171">Deel 5 - Hallo bestand opslaan en uploaden</span><span class="sxs-lookup"><span data-stu-id="5f939-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="5f939-172">Hallo-bestand opslaan en vervolgens tooAzure door het uitvoeren van de volgende opdracht Hallo importeren.</span><span class="sxs-lookup"><span data-stu-id="5f939-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="5f939-173">Zorg ervoor dat u het bestandspad Hallo die nodig zijn voor uw omgeving wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f939-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="5f939-174">Hier ziet u een vergelijkbaar resultaat Hallo importeren is voltooid wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5f939-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="5f939-175">Deel 6 – Hallo-gateway maken</span><span class="sxs-lookup"><span data-stu-id="5f939-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="5f939-176">Raadpleeg voordat u dit voorbeeld, toohello netwerk-configuratiebestand dat u hebt gedownload voor Hallo exacte die Azure namen toosee verwacht.</span><span class="sxs-lookup"><span data-stu-id="5f939-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="5f939-177">Hallo netwerk configuratiebestand bevat Hallo waarden voor uw klassieke virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="5f939-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="5f939-178">Soms Hallo Hallo namen voor klassieke die vnet 's zijn gewijzigd in Hallo netwerk configuratiebestand bij het maken van klassieke VNet-instellingen in Azure-portal vanwege toohello verschillen in Hallo implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="5f939-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="5f939-179">Bijvoorbeeld, als u Azure portal toocreate een klassiek VNet met de naam 'Klassieke VNet' en deze is gemaakt in een resourcegroep met de naam 'ClassicRG' hello gebruikt, Hallo-naam die is opgenomen in het configuratiebestand Hallo-netwerk is geconverteerde too'Group ClassicRG klassieke VNet'.</span><span class="sxs-lookup"><span data-stu-id="5f939-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="5f939-180">Wanneer u opgeeft Hallo-naam van een VNet dat spaties bevat, Gebruik aanhalingstekens rond het Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="5f939-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="5f939-181">Hallo voorbeeld toocreate een gateway voor dynamische routering volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f939-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="5f939-182">U kunt de status Hallo van Hallo gateway controleren met behulp van Hallo **Get-AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5f939-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="5f939-183"><a name="creatermgw"></a>Deel 2: Hallo RM-VNet-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="5f939-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="5f939-184">een VPN-gateway voor Hallo RM-VNet toocreate Volg Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="5f939-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="5f939-185">Hallo stappen totdat niet worden gestart nadat u Hallo openbaar IP-adres voor de gateway Hallo klassieke VNet hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5f939-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="5f939-186">Tooyour aanmelden met Azure-account in Hallo PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="5f939-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="5f939-187">Hallo vraagt volgende cmdlet u om Hallo aanmeldingsreferenties voor uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="5f939-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="5f939-188">Na het aanmelden, worden de instellingen van uw account zodat ze beschikbaar tooAzure PowerShell zijn gedownload.</span><span class="sxs-lookup"><span data-stu-id="5f939-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="5f939-189">Een lijst met uw Azure-abonnementen ophalen als u meer dan één abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="5f939-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="5f939-190">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f939-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="5f939-191">Maak een lokale netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="5f939-191">Create a local network gateway.</span></span> <span data-ttu-id="5f939-192">Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="5f939-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="5f939-193">In dit geval verwijst de lokale netwerkgateway Hallo tooyour klassieke VNet.</span><span class="sxs-lookup"><span data-stu-id="5f939-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="5f939-194">Geef het een naam waarmee Azure kunt tooit verwijzen, en ook het adresruimtevoorvoegsel Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f939-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="5f939-195">Hallo IP-adresvoorvoegsel u opgeven welk verkeer toosend tooyour lokale locatie tooidentify maakt gebruik van Azure.</span><span class="sxs-lookup"><span data-stu-id="5f939-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="5f939-196">Als u tooadjust Hallo informatie hier later voordat u de gateway maakt kunt u Hallo waarden en Voer Hallo voorbeeld opnieuw wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f939-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="5f939-197">**-Naam** gewenste tooassign toorefer toohello lokale netwerkgateway Hallo-naam is.</span><span class="sxs-lookup"><span data-stu-id="5f939-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="5f939-198">
   **-AddressPrefix** Hallo adresruimte voor het klassieke VNet is.</span><span class="sxs-lookup"><span data-stu-id="5f939-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="5f939-199">
**-GatewayIpAddress** Hallo openbare IP-adres van gateway Hallo klassieke VNet.</span><span class="sxs-lookup"><span data-stu-id="5f939-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="5f939-200">Zorg ervoor dat toochange Hallo volgende steekproef tooreflect Hallo juiste IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5f939-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="5f939-201">Een openbaar IP-adres toobe toegewezen toohello virtuele netwerkgateway voor Resource Manager VNet Hallo aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5f939-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="5f939-202">U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f939-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="5f939-203">Hallo IP-adres wordt dynamisch toegewezen toohello virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="5f939-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="5f939-204">Dit betekent echter niet Hallo IP-adreswijzigingen dat.</span><span class="sxs-lookup"><span data-stu-id="5f939-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="5f939-205">de enige keer Hallo Hallo virtuele IP-adreswijzigingen netwerkgateway is wanneer Hallo gateway is verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="5f939-206">Wordt niet gewijzigd via vergroten of verkleinen, opnieuw wordt ingesteld, of een andere interne onderhoud of upgrades worden uitgevoerd Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="5f939-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="5f939-207">In deze stap wordt ook een variabele die wordt gebruikt in een latere stap instellen.</span><span class="sxs-lookup"><span data-stu-id="5f939-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="5f939-208">Controleer of het virtuele netwerk een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="5f939-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="5f939-209">Als er geen gatewaysubnet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="5f939-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="5f939-210">Zorg ervoor dat het gatewaysubnet Hallo heet *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="5f939-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="5f939-211">Hallo subnet dat wordt gebruikt voor de gateway Hallo door het uitvoeren van de volgende opdracht Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="5f939-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="5f939-212">In deze stap wordt ook een variabele toobe gebruikt in de volgende stap Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="5f939-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="5f939-213">**-Naam** Hallo-naam van uw VNet Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f939-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="5f939-214">
   **-ResourceGroupName** is Hallo resourcegroep die Hallo VNet is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5f939-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="5f939-215">Hallo gatewaysubnet moet al bestaan voor dit VNet en moet de naam *GatewaySubnet* toowork goed.</span><span class="sxs-lookup"><span data-stu-id="5f939-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="5f939-216">Hallo-gateway voor IP-adressen van de configuratie maken.</span><span class="sxs-lookup"><span data-stu-id="5f939-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="5f939-217">Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse.</span><span class="sxs-lookup"><span data-stu-id="5f939-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="5f939-218">Hallo voorbeeld toocreate na de configuratie van uw gateway gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f939-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="5f939-219">In deze stap Hallo **- SubnetId** en **- PublicIpAddressId** parameters moeten worden doorgegeven Hallo id-eigenschap van het Hallo-subnet en IP-adres objecten, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="5f939-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="5f939-220">U kunt een eenvoudige tekenreeks niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f939-220">You can't use a simple string.</span></span> <span data-ttu-id="5f939-221">Deze variabelen worden ingesteld in Hallo stap toorequest een openbaar IP-adres en Hallo stap tooretrieve Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="5f939-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="5f939-222">Hallo Resource Manager virtuele netwerkgateway maken door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f939-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="5f939-223">Hallo `-VpnType` moet *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="5f939-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="5f939-224">Het kan duren voordat 45 minuten of langer Hallo gateway toocreate.</span><span class="sxs-lookup"><span data-stu-id="5f939-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="5f939-225">Kopieer Hallo openbaar IP-adres als Hallo VPN-gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="5f939-226">U gebruiken wanneer u Hallo LAN-instellingen voor het klassieke VNet configureert.</span><span class="sxs-lookup"><span data-stu-id="5f939-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="5f939-227">U kunt Hallo volgende cmdlet tooretrieve Hallo openbare IP-adres gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f939-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="5f939-228">Hallo openbaar IP-adres staat in Hallo retourneren als *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="5f939-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="5f939-229">Deel 3: Hallo klassieke VNet lokale site-instellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="5f939-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="5f939-230">In deze sectie kunt u samenwerken met Hallo klassieke VNet.</span><span class="sxs-lookup"><span data-stu-id="5f939-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="5f939-231">U vervangen Hallo tijdelijke aanduiding voor IP-adres dat u hebt gebruikt bij het opgeven van Hallo lokale site-instellingen die gebruikt tooconnect toohello Resource Manager VNet gateway worden.</span><span class="sxs-lookup"><span data-stu-id="5f939-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="5f939-232">Hallo netwerk configuratiebestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="5f939-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="5f939-233">Met een teksteditor Hallo waarde wijzigen voor VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="5f939-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="5f939-234">Hallo tijdelijke aanduiding voor IP-adres met openbare IP-adres van de Resource Manager-gateway Hallo Hallo vervangen en Hallo wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="5f939-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="5f939-235">Importeren Hallo netwerk configuratie bestand tooAzure gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5f939-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="5f939-236"><a name="connect"></a>Sectie 4: Maak een verbinding tussen Hallo gateways</span><span class="sxs-lookup"><span data-stu-id="5f939-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="5f939-237">Maken van een verbinding tussen de gateways Hallo is PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="5f939-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="5f939-238">U moet mogelijk tooadd uw Azure-Account toouse Hallo klassieke versie van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5f939-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="5f939-239">toodo dus gebruiken **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="5f939-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="5f939-240">Stel uw gedeelde sleutel in Hallo PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="5f939-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="5f939-241">Raadpleeg voordat u cmdlets hello, toohello netwerk-configuratiebestand dat u hebt gedownload voor Hallo exacte die Azure namen toosee verwacht.</span><span class="sxs-lookup"><span data-stu-id="5f939-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="5f939-242">Wanneer u opgeeft Hallo-naam van een VNet dat spaties bevat, gebruik Hallo-waarde op tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="5f939-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="5f939-243">In het volgende voorbeeld **- VNetName** heet Hallo Hallo klassiek VNet en **- LocalNetworkSiteName** is opgegeven voor de lokale netwerksite Hallo Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="5f939-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="5f939-244">Hallo **- SharedKey** is een waarde die u genereren en opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f939-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="5f939-245">In voorbeeld Hallo we 'abc123' gebruikt, maar u kunt genereren en gebruikmaken van iets meer complexe.</span><span class="sxs-lookup"><span data-stu-id="5f939-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="5f939-246">Hallo belangrijke dingen die u hier opgeeft, Hallo-waarde is moet Hallo die dezelfde waarde die u in de volgende stap Hallo opgeeft wanneer u uw verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="5f939-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="5f939-247">Hallo return moet worden weergegeven **Status: geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="5f939-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="5f939-248">Hallo VPN-verbinding door het uitvoeren van de volgende opdrachten Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="5f939-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="5f939-249">Hallo-variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5f939-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="5f939-250">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="5f939-250">Create hello connection.</span></span> <span data-ttu-id="5f939-251">U ziet dat Hallo **- ConnectionType** IPsec, niet Vnet2Vnet is.</span><span class="sxs-lookup"><span data-stu-id="5f939-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="5f939-252">Sectie 5: Controleer of uw verbindingen</span><span class="sxs-lookup"><span data-stu-id="5f939-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="5f939-253">tooverify hello verbinding van uw klassieke VNet tooyour Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="5f939-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f939-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f939-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="5f939-255">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f939-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="5f939-256">tooverify hello verbinding van de Resource Manager VNet tooyour klassieke VNet</span><span class="sxs-lookup"><span data-stu-id="5f939-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f939-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f939-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="5f939-258">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f939-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="5f939-259"><a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet</span><span class="sxs-lookup"><span data-stu-id="5f939-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

