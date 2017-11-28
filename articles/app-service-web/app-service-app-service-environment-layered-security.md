---
title: aaaLayered beveiligingsarchitectuur met App Service-omgevingen
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
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="1db3a-103">Implementatie van een gelaagd beveiligingsarchitectuur met App Service-omgevingen</span><span class="sxs-lookup"><span data-stu-id="1db3a-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="1db3a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1db3a-104">Overview</span></span>
<span data-ttu-id="1db3a-105">Omdat App Service-omgevingen een geïsoleerde runtime-omgeving in een virtueel netwerk geïmplementeerd bieden, kunnen ontwikkelaars een gelaagd beveiligingsarchitectuur bieden verschillende niveaus van toegang tot het netwerk voor elke toepassingslaag fysieke maken.</span><span class="sxs-lookup"><span data-stu-id="1db3a-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="1db3a-106">Een algemene streven toohide API-back-ends van algemene toegang tot het Internet is en dat alleen API's toobe aangeroepen door de upstream-web-apps.</span><span class="sxs-lookup"><span data-stu-id="1db3a-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="1db3a-107">[Netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] op subnetten met App Service-omgevingen toorestrict openbare toegang tooAPI toepassingen kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1db3a-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="1db3a-108">Hallo diagram hieronder toont een voorbeeld-architectuur met een WebAPI op basis van app geïmplementeerd op een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1db3a-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="1db3a-109">Drie afzonderlijke web app-exemplaren, geïmplementeerd op drie aparte App Service-omgevingen, Controleer back-end-aanroepen toohello dezelfde WebAPI-app.</span><span class="sxs-lookup"><span data-stu-id="1db3a-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Conceptionele architectuur][ConceptualArchitecture] 

<span data-ttu-id="1db3a-111">Hallo groen plusteken aangeven dat Hallo netwerkbeveiligingsgroep op Hallo subnet met 'apiase' kunt binnenkomende oproepen van Hallo upstream web-apps, als ook aanroepen van zichzelf.</span><span class="sxs-lookup"><span data-stu-id="1db3a-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="1db3a-112">Maar Hallo dezelfde netwerkbeveiligingsgroep expliciet geweigerd toegang toogeneral binnenkomend verkeer van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="1db3a-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="1db3a-113">netwerkbeveiligingsgroep van Hallo stappen nodig tooconfigure Hallo Hallo rest van dit onderwerp wordt uitgelegd op Hallo subnet met 'apiase'.</span><span class="sxs-lookup"><span data-stu-id="1db3a-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="1db3a-114">Hallo netwerkverkeer bepalen</span><span class="sxs-lookup"><span data-stu-id="1db3a-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="1db3a-115">In de volgorde tooknow moet welke netwerkbeveiliging regels nodig zijn, u toodetermine welke netwerkclients krijgt tooreach Hallo App Service-omgeving met Hallo API-app en welke clients worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="1db3a-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="1db3a-116">Aangezien [netwerkbeveiligingsgroepen (nsg's)] [ NetworkSecurityGroups] zijn toegepaste toosubnets en App Service-omgevingen zijn geïmplementeerd in subnetten, toepassing hello regels in een NSG te**alle** Apps die worden uitgevoerd op een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1db3a-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="1db3a-117">Hallo voorbeeldarchitectuur voor dit artikel met zodra een netwerkbeveiligingsgroep toegepaste toohello subnet 'apiase' alle apps die worden uitgevoerd op Hallo 'apiase is' App Service-omgeving worden beveiligd door Hallo met set dezelfde beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="1db3a-118">**Hallo uitgaande IP-adres van de upstream-aanroepfuncties bepalen:** wat is er of Hallo IP-adressen van Hallo upstream aanroepfuncties?</span><span class="sxs-lookup"><span data-stu-id="1db3a-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="1db3a-119">Deze adressen moet expliciet toegang is toegestaan in Hallo NSG toobe.</span><span class="sxs-lookup"><span data-stu-id="1db3a-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="1db3a-120">Omdat aanroepen tussen App Service-omgevingen worden beschouwd als 'Internet' aanroepen, betekent dit Hallo uitgaande IP-adres toegewezen tooeach van Hallo drie upstream-App Service-omgevingen behoeften toobe toegang is toegestaan in Hallo NSG voor subnet van Hallo 'apiase'.</span><span class="sxs-lookup"><span data-stu-id="1db3a-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="1db3a-121">Voor meer informatie over het Hallo uitgaande IP-adres bepalen voor apps die worden uitgevoerd in een App-serviceomgeving Zie Hallo [netwerkarchitectuur] [ NetworkArchitecture] overzichtsartikel.</span><span class="sxs-lookup"><span data-stu-id="1db3a-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="1db3a-122">**Moet Hallo back-end-API-app toocall zelf?**</span><span class="sxs-lookup"><span data-stu-id="1db3a-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="1db3a-123">Een punt soms onderbelicht en subtiele is Hallo-scenario waarin het back-endtoepassing Hallo toocall zelf moet.</span><span class="sxs-lookup"><span data-stu-id="1db3a-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="1db3a-124">Als een back-end-API-toepassing op een App-serviceomgeving toocall zelf moet, is dit ook behandeld als een aanroep van 'Internet'.</span><span class="sxs-lookup"><span data-stu-id="1db3a-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="1db3a-125">Hiervoor moet de toegang te verlenen vanaf Hallo uitgaande IP-adres van Hallo 'apiase' App Service-omgeving ook uit te voeren in Hallo voorbeeldarchitectuur.</span><span class="sxs-lookup"><span data-stu-id="1db3a-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="1db3a-126">Hallo Netwerkbeveiligingsgroep instellen</span><span class="sxs-lookup"><span data-stu-id="1db3a-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="1db3a-127">Zodra Hallo ingesteld van uitgaande IP-adressen bekend zijn, de volgende stap Hallo is tooconstruct een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1db3a-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="1db3a-128">Netwerkbeveiligingsgroepen kunnen worden gemaakt voor beide Resource Manager virtuele netwerken, evenals klassieke virtuele netwerken gebaseerde.</span><span class="sxs-lookup"><span data-stu-id="1db3a-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="1db3a-129">Hallo voorbeelden hieronder ziet u maken en configureren van een NSG op een klassiek virtueel netwerk met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="1db3a-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="1db3a-130">Hallo-omgevingen bevinden zich in Zuid-centraal VS, voor voorbeeldarchitectuur hello, zodat een lege NSG wordt gemaakt in deze regio:</span><span class="sxs-lookup"><span data-stu-id="1db3a-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="1db3a-131">Eerst een expliciete toestaan regel wordt toegevoegd voor hello Azure management infrastructuur zoals beschreven in artikel Hallo op [binnenkomend verkeer] [ InboundTraffic] voor App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="1db3a-132">Vervolgens twee regels worden toegevoegd tooallow HTTP en HTTPS-aanroepen vanuit Hallo eerste upstream-App Service-omgeving ('fe1ase').</span><span class="sxs-lookup"><span data-stu-id="1db3a-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1db3a-133">Spoelen en Herhaal dit voor Hallo tweede en derde upstream-App Service-omgevingen ('fe2ase' en 'fe3ase').</span><span class="sxs-lookup"><span data-stu-id="1db3a-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1db3a-134">Ten slotte verlenen toegang toohello uitgaande IP-adres van Hallo back-end-API-App Service-omgeving zodat terug naar zichzelf kan worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1db3a-135">Er zijn geen andere netwerkbeveiligingsregels moeten toobe omdat elke NSG bevat een set met standaardregels die inkomende toegang tot Internet Hallo geblokkeerd standaard geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1db3a-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="1db3a-136">Hallo volledige lijst met regels in Hallo netwerkbeveiligingsgroep worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1db3a-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="1db3a-137">Houd er rekening mee hoe de laatste regel hello, die is gemarkeerd, blokkeert binnenkomende toegang vanaf alle aanroepfuncties dan degene die expliciet toegang hebben gekregen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG-configuratie][NSGConfiguration] 

<span data-ttu-id="1db3a-139">de laatste stap Hallo is tooapply hello NSG toohello subnet met Hallo 'apiase' App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1db3a-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="1db3a-140">Met Hallo NSG toegepast toohello subnet zijn alleen hello drie upstream-App Service-omgevingen en Hallo App Service-omgeving met Hallo API-back-end, toegestaan toocall naar Hallo 'apiase'-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1db3a-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="1db3a-141">Aanvullende koppelingen en informatie</span><span class="sxs-lookup"><span data-stu-id="1db3a-141">Additional Links and Information</span></span>
<span data-ttu-id="1db3a-142">Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="1db3a-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="1db3a-143">Informatie over [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1db3a-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="1db3a-144">Informatie over [uitgaande IP-adressen] [ NetworkArchitecture] en App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="1db3a-145">[Netwerkpoorten] [ InboundTraffic] die wordt gebruikt door App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1db3a-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
