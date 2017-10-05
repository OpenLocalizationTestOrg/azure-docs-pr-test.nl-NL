---
title: Gelaagde beveiligingsarchitectuur met App Service-omgevingen
description: Het implementeren van een gelaagd beveiligingsarchitectuur met App Service-omgevingen.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="5bf5f-103">Implementatie van een gelaagd beveiligingsarchitectuur met App Service-omgevingen</span><span class="sxs-lookup"><span data-stu-id="5bf5f-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="5bf5f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5bf5f-104">Overview</span></span>
<span data-ttu-id="5bf5f-105">Omdat App Service-omgevingen een geïsoleerde runtime-omgeving in een virtueel netwerk geïmplementeerd bieden, kunnen ontwikkelaars een gelaagd beveiligingsarchitectuur bieden verschillende niveaus van toegang tot het netwerk voor elke toepassingslaag fysieke maken.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="5bf5f-106">Een algemene streven is verbergen API back-ends van algemene toegang tot Internet en dat alleen API's om te worden aangeroepen door de upstream-web-apps.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="5bf5f-107">[Netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] op subnetten met App Service-omgevingen kunnen worden gebruikt voor het openbare toegang tot API toepassingen beperken.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="5bf5f-108">Het volgende diagram toont een voorbeeld-architectuur met een WebAPI op basis van app geïmplementeerd op een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="5bf5f-109">Drie afzonderlijke web app-exemplaren, geïmplementeerd op drie aparte App Service-omgevingen, moeten back-end-aanroepen naar dezelfde WebAPI-app.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Conceptionele architectuur][ConceptualArchitecture] 

<span data-ttu-id="5bf5f-111">Het groen plusteken aangeven dat de netwerkbeveiligingsgroep op het subnet met 'apiase' inkomende aanroepen van de upstream-web-apps, kunt u als goed aanroepen van zichzelf.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="5bf5f-112">Evenwel de dezelfde netwerkbeveiligingsgroep expliciet geweigerd voor toegang tot algemene binnenkomend verkeer vanaf Internet.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="5bf5f-113">De rest van dit onderwerp worden de stappen die nodig zijn voor het configureren van de netwerkbeveiligingsgroep op het subnet met 'apiase'.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="5bf5f-114">Bepalen het gedrag van het netwerk</span><span class="sxs-lookup"><span data-stu-id="5bf5f-114">Determining the Network Behavior</span></span>
<span data-ttu-id="5bf5f-115">Als u wilt weten welke netwerkbeveiligingsregels nodig zijn, moet u bepalen welke netwerkclients kunnen worden bereikt van het App Service-omgeving waarin de API-app en welke clients worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="5bf5f-116">Aangezien [netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] worden toegepast op subnetten, en App Service-omgevingen in subnetten worden geïmplementeerd, de regels in een NSG van toepassing op **alle** apps uitgevoerd op een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="5bf5f-117">Gebruik de voorbeeldarchitectuur voor dit artikel nadat een netwerkbeveiligingsgroep is toegepast op het subnet met 'apiase' en worden alle apps die worden uitgevoerd op de App Service-omgeving 'apiase' beveiligd door dezelfde set beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="5bf5f-118">**Bepalen van de uitgaande IP-adres van de upstream aanroepers:** wat is de IP-adres of de adressen van de upstream aanroepfuncties?</span><span class="sxs-lookup"><span data-stu-id="5bf5f-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="5bf5f-119">Deze adressen moet expliciet toegang te krijgen in de NSG.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="5bf5f-120">Omdat aanroepen tussen App Service-omgevingen worden beschouwd als 'Internet' aanroepen, moet dit betekent dat het uitgaande IP-adres toegewezen aan elk van de drie upstream-App Service-omgevingen moet u toegang te krijgen in de NSG voor het subnet 'apiase'.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="5bf5f-121">Voor meer informatie over het bepalen van het uitgaande IP-adres voor apps die worden uitgevoerd in een App Service-omgeving raadpleegt u de [netwerkarchitectuur] [ NetworkArchitecture] overzichtsartikel.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="5bf5f-122">**De back-end-API-app moet aan te roepen zelf?**</span><span class="sxs-lookup"><span data-stu-id="5bf5f-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="5bf5f-123">Een punt soms onderbelicht en subtiele is het scenario waarin de back-endtoepassing moet zichzelf.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="5bf5f-124">Als een back-end-API-toepassing op een App-serviceomgeving zichzelf moet, wordt dit ook behandeld als een aanroep van 'Internet'.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="5bf5f-125">Hiervoor moet de toegang te verlenen vanaf de uitgaande IP-adres van de 'apiase' App Service-omgeving ook uit te voeren in de voorbeeldarchitectuur.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="5bf5f-126">Instellen van de Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="5bf5f-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="5bf5f-127">Zodra de set met uitgaande IP-adressen gekend zijn, worden de volgende stap is om een netwerkbeveiligingsgroep samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="5bf5f-128">Netwerkbeveiligingsgroepen kunnen worden gemaakt voor beide Resource Manager virtuele netwerken, evenals klassieke virtuele netwerken gebaseerde.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="5bf5f-129">De volgende voorbeelden tonen maken en configureren van een NSG op een klassiek virtueel netwerk met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="5bf5f-130">Voor de voorbeeldarchitectuur staan de omgevingen in Zuid-centraal VS, zodat een lege NSG wordt gemaakt in deze regio:</span><span class="sxs-lookup"><span data-stu-id="5bf5f-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="5bf5f-131">Eerst een expliciete toestaan regel wordt toegevoegd voor de Azure management-infrastructuur zoals aangegeven in het artikel op [binnenkomend verkeer] [ InboundTraffic] voor App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="5bf5f-132">Vervolgens twee regels worden toegevoegd aan het toestaan van HTTP en HTTPS-aanroepen vanuit de eerste upstream-App Service-omgeving ('fe1ase').</span><span class="sxs-lookup"><span data-stu-id="5bf5f-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5bf5f-133">Spoel en Herhaal voor de tweede en derde upstream-App Service-omgevingen ('fe2ase' en 'fe3ase').</span><span class="sxs-lookup"><span data-stu-id="5bf5f-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5bf5f-134">Ten slotte toegang verlenen tot de uitgaande IP-adres van de back-end-API-App Service-omgeving zodat terug naar zichzelf kan worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5bf5f-135">Er zijn geen andere netwerkbeveiligingsregels moeten worden geconfigureerd omdat elke NSG heeft een set met standaardregels die inkomende toegang via het Internet blokkeren standaard.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="5bf5f-136">De volledige lijst met regels in de netwerkbeveiligingsgroep worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="5bf5f-137">Houd er rekening mee hoe de laatste regel die is gemarkeerd, blokkeert binnenkomende toegang vanaf alle aanroepfuncties dan degene die expliciet toegang hebben gekregen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG-configuratie][NSGConfiguration] 

<span data-ttu-id="5bf5f-139">De laatste stap wordt de NSG toegepast op het subnet waarin de 'apiase' App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="5bf5f-140">Met het NSG wordt toegepast op het subnet, worden alleen de drie upstream-App Service-omgevingen en de App Service-omgeving met de API-back-end, om aan te roepen in de omgeving 'apiase' toegestaan.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="5bf5f-141">Aanvullende koppelingen en informatie</span><span class="sxs-lookup"><span data-stu-id="5bf5f-141">Additional Links and Information</span></span>
<span data-ttu-id="5bf5f-142">Alle artikelen en hoe-aan de voor App Service-omgevingen zijn beschikbaar in de [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="5bf5f-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5bf5f-143">Informatie over [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="5bf5f-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="5bf5f-144">Informatie over [uitgaande IP-adressen] [ NetworkArchitecture] en App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="5bf5f-145">[Netwerkpoorten] [ InboundTraffic] die wordt gebruikt door App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="5bf5f-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
