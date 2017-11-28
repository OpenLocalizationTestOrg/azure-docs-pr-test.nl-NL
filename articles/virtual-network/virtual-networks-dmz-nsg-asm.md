---
title: "aaaAzure DMZ voorbeeld – een eenvoudige DMZ met nsg's bouwen | Microsoft Docs"
description: Maken van een DMZ met Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="999a2-103">Voorbeeld 1: een eenvoudige DMZ met nsg's met klassieke PowerShell bouwen</span><span class="sxs-lookup"><span data-stu-id="999a2-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="999a2-104">[Best Practices beveiligingspagina-grens toohello retourneren][HOME]</span><span class="sxs-lookup"><span data-stu-id="999a2-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="999a2-105">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="999a2-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="999a2-106">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="999a2-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="999a2-107">In dit voorbeeld maakt een primitieve DMZ met vier Windows-servers en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="999a2-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="999a2-108">In dit voorbeeld worden alle Hallo relevante PowerShell-opdrachten tooprovide een beter begrip van elke stap beschreven.</span><span class="sxs-lookup"><span data-stu-id="999a2-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="999a2-109">Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ.</span><span class="sxs-lookup"><span data-stu-id="999a2-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="999a2-110">Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="999a2-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="999a2-111">![Inkomende DMZ met NSG][1]</span><span class="sxs-lookup"><span data-stu-id="999a2-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="999a2-112">Beschrijving van de omgeving</span><span class="sxs-lookup"><span data-stu-id="999a2-112">Environment description</span></span>
<span data-ttu-id="999a2-113">In dit voorbeeld bevat een abonnement Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="999a2-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="999a2-114">Twee cloudservices: 'FrontEnd001' en 'BackEnd001'</span><span class="sxs-lookup"><span data-stu-id="999a2-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="999a2-115">Een virtueel netwerk, 'CorpNetwork' met twee subnetten; 'FrontEnd' en back-end'</span><span class="sxs-lookup"><span data-stu-id="999a2-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="999a2-116">Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten</span><span class="sxs-lookup"><span data-stu-id="999a2-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="999a2-117">Een Windows-Server waarmee een toepassing webserver ('IIS01')</span><span class="sxs-lookup"><span data-stu-id="999a2-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="999a2-118">Twee windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')</span><span class="sxs-lookup"><span data-stu-id="999a2-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="999a2-119">Een Windows-server met een DNS-server ('DNS01')</span><span class="sxs-lookup"><span data-stu-id="999a2-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="999a2-120">In de sectie Verwijzingen hello is er een PowerShell-script dat de meeste Hallo-omgeving beschreven in dit voorbeeld is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="999a2-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="999a2-121">Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="999a2-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="999a2-122">toobuild Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="999a2-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="999a2-123">Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan</span><span class="sxs-lookup"><span data-stu-id="999a2-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="999a2-124">Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enz.)</span><span class="sxs-lookup"><span data-stu-id="999a2-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="999a2-125">Hallo-script uitvoeren in PowerShell</span><span class="sxs-lookup"><span data-stu-id="999a2-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="999a2-126">Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.</span><span class="sxs-lookup"><span data-stu-id="999a2-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="999a2-127">Zodra het Hallo-script wordt uitgevoerd is aanvullende optionele stappen kunnen worden genomen, zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.</span><span class="sxs-lookup"><span data-stu-id="999a2-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="999a2-128">Hallo bevatten volgende secties een gedetailleerde beschrijving van Netwerkbeveiligingsgroepen en hoe ze werken in dit voorbeeld door de regels van de PowerShell-script Hallo doorlopen.</span><span class="sxs-lookup"><span data-stu-id="999a2-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="999a2-129">Netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="999a2-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="999a2-130">In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels.</span><span class="sxs-lookup"><span data-stu-id="999a2-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="999a2-131">In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels.</span><span class="sxs-lookup"><span data-stu-id="999a2-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="999a2-132">Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="999a2-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="999a2-133">Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="999a2-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="999a2-134">NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).</span><span class="sxs-lookup"><span data-stu-id="999a2-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="999a2-135">Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:</span><span class="sxs-lookup"><span data-stu-id="999a2-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="999a2-136">Interne DNS-verkeer (poort 53) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="999a2-137">RDP-verkeer (poort 3389) van Hallo Internet tooany VM is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="999a2-138">HTTP-verkeer (poort 80) van Hallo tooweb internetserver (IIS01) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="999a2-139">Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="999a2-140">Verkeer (alle poorten) van Hallo Internet toohello hele VNet (beide subnetten) is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="999a2-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="999a2-141">Verkeer (alle poorten) van Hallo Frontend subnet toohello back-end-subnet is geweigerd</span><span class="sxs-lookup"><span data-stu-id="999a2-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="999a2-142">Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn, maar omdat de regel 3 heeft een hogere prioriteit alleen zou worden toegepast en regel 5 niet in de play zou komen.</span><span class="sxs-lookup"><span data-stu-id="999a2-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="999a2-143">Hallo HTTP-aanvraag zou dus toohello webserver toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="999a2-144">Als dat dezelfde verkeer tooreach hello DNS01 server probeerde, zou regel 5 (weigeren) zijn de eerste tooapply en Hallo verkeer Hallo zou niet toegestaan toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="999a2-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="999a2-145">Regel 6 (weigeren) blokkeert Hallo Frontend subnet uit praten toohello back-end-subnet (met uitzondering van toegestane regels 1 en 4-verkeer), deze regelset beschermt Hallo back-end-netwerk als een aanvaller inbreuk Hallo webtoepassing op Hallo Frontend, Hallo aanvaller zou beperkte toegang toohello back-end '-beveiliging gebruiken' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).</span><span class="sxs-lookup"><span data-stu-id="999a2-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="999a2-146">Er is een uitgaande standaardregel waarmee verkeer van toohello internet.</span><span class="sxs-lookup"><span data-stu-id="999a2-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="999a2-147">Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="999a2-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="999a2-148">toolock omlaag verkeer in beide richtingen, de gebruiker gedefinieerde routering is vereist en in 'Voorbeeld 3' is verkend op Hallo [Best Practices beveiligingspagina-grens][HOME].</span><span class="sxs-lookup"><span data-stu-id="999a2-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="999a2-149">Elke regel als volgt in detail beschreven (**Opmerking**: een item in de volgende lijst, te beginnen met een dollarteken Hallo (bijvoorbeeld: $NSGName) is een gebruiker gedefinieerde variabele uit het Hallo-script in Hallo verwijzing sectie van dit document):</span><span class="sxs-lookup"><span data-stu-id="999a2-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="999a2-150">Een Netwerkbeveiligingsgroep moet eerst toohold Hallo regels gebaseerd:</span><span class="sxs-lookup"><span data-stu-id="999a2-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="999a2-151">de eerste regel Hallo in dit voorbeeld kunt DNS-verkeer tussen alle interne netwerken toohello DNS-server op Hallo back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="999a2-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="999a2-152">Hallo regel heeft enkele belangrijke parameters:</span><span class="sxs-lookup"><span data-stu-id="999a2-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="999a2-153">'Typ' geeft aan in welke richting van verkeer met deze regel wordt van kracht.</span><span class="sxs-lookup"><span data-stu-id="999a2-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="999a2-154">Hallo richting is vanuit Hallo perspectief van Hallo subnet of een virtuele Machine (afhankelijk van waar deze NSG is gekoppeld).</span><span class="sxs-lookup"><span data-stu-id="999a2-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="999a2-155">Dus als Type is 'Inkomend' en verkeer is Hallo subnet invoeren, Hallo regel van toepassing en Hallo subnet uitgaand verkeer niet wordt beïnvloed door deze regel.</span><span class="sxs-lookup"><span data-stu-id="999a2-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="999a2-156">'Prioriteit' stelt Hallo volgorde waarin netwerkverkeer wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="999a2-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="999a2-157">Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="999a2-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="999a2-158">Wanneer een regel van toepassing tooa specifieke netwerkverkeer is, kan er geen verdere regels worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="999a2-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="999a2-159">Dus als een regel met prioriteit 1 gegevensverkeer, en een regel met prioriteit 2 verkeer weigert, en beide regels zijn van toepassing tootraffic vervolgens Hallo verkeer tooflow mogen (omdat de regel 1 een hogere prioriteit heeft geduurd effect en geen verdere regels zijn toegepast).</span><span class="sxs-lookup"><span data-stu-id="999a2-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="999a2-160">"Action" betekent dat verkeer dat is beïnvloed door deze regel is geblokkeerd of toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="999a2-161">Deze regel kunnen de RDP-verkeer tooflow vanaf internet toohello RDP-poort op elke server op Hallo Hallo gebonden subnet.</span><span class="sxs-lookup"><span data-stu-id="999a2-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="999a2-162">Deze regel maakt gebruik van twee speciale soorten adresvoorvoegsels; 'VIRTUAL_NETWORK' en 'INTERNET'.</span><span class="sxs-lookup"><span data-stu-id="999a2-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="999a2-163">Deze tags zijn een eenvoudige manier tooaddress een grotere categorie van adresvoorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="999a2-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="999a2-164">Deze regel kunnen binnenkomende internet verkeer toohit Hallo webserver.</span><span class="sxs-lookup"><span data-stu-id="999a2-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="999a2-165">Deze regel wordt het routeringsgedrag Hallo niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="999a2-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="999a2-166">Hallo regel kunnen alleen verkeer dat is bestemd voor IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="999a2-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="999a2-167">Dus als verkeer van Internet Hallo Hallo webserver als de bestemming voor deze regel zou toe te staan en stoppen met het verwerken van verdere regels had.</span><span class="sxs-lookup"><span data-stu-id="999a2-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="999a2-168">(In de regel Hallo met prioriteit 140 alle andere Binnenkomend internetverkeer wordt geblokkeerd).</span><span class="sxs-lookup"><span data-stu-id="999a2-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="999a2-169">Als u alleen HTTP-verkeer wordt verwerkt, met deze regel kan worden verder beperkt tooonly toestaan bestemming poort 80.</span><span class="sxs-lookup"><span data-stu-id="999a2-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="999a2-170">Deze regel kan verkeer toopass van Hallo IIS01 server toohello AppVM01 server, een hoger regel blokkeert al het andere Frontend tooBackend verkeer.</span><span class="sxs-lookup"><span data-stu-id="999a2-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="999a2-171">tooimprove deze regel als Hallo poort bekend is dat moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="999a2-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="999a2-172">Bijvoorbeeld, als Hallo IIS-server alleen SQL Server op AppVM01 roept is, Hallo Doelpoortbereik moet worden gewijzigd van ' * ' (Any) too1433 (hello SQL-poort) waardoor een kleinere inkomende kwetsbaarheid voor aanvallen op AppVM01 of webtoepassing Hallo ooit verdacht.</span><span class="sxs-lookup"><span data-stu-id="999a2-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="999a2-173">Deze regel weigert verkeer van Hallo internet tooany servers op Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="999a2-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="999a2-174">Met regels met prioriteit 110 en 120 Hallo Hallo effect is tooallow alleen inkomend verkeer toohello firewall voor internet- en RDP-poorten op servers en blokkeert al het andere.</span><span class="sxs-lookup"><span data-stu-id="999a2-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="999a2-175">Deze regel is een 'veiligheidsmaatregel' regel tooblock alle onverwachte stromen.</span><span class="sxs-lookup"><span data-stu-id="999a2-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="999a2-176">de laatste regel Hallo weigert verkeer van Hallo Frontend subnet toohello back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="999a2-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="999a2-177">Aangezien deze regel een inkomende regel alleen is, is (van Hallo back-end toohello Frontend) omgekeerde verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="999a2-178">Verkeer scenario 's</span><span class="sxs-lookup"><span data-stu-id="999a2-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="999a2-179">(*Toegestane*) tooweb internetserver</span><span class="sxs-lookup"><span data-stu-id="999a2-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="999a2-180">Een internet-gebruiker aanvragen een pagina http-van FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="999a2-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="999a2-181">Cloud service geeft verkeer via open eindpunten op poort 80 voor IIS01 (Hallo webserver)</span><span class="sxs-lookup"><span data-stu-id="999a2-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="999a2-182">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-183">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="999a2-184">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="999a2-185">NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="999a2-186">Verkeer komt binnen via interne IP-adres van de webserver Hallo IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="999a2-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="999a2-187">IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag</span><span class="sxs-lookup"><span data-stu-id="999a2-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="999a2-188">IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="999a2-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="999a2-189">Aangezien er geen uitgaande regels op subnet Frontend zijn, is verkeer toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="999a2-190">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-191">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="999a2-192">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="999a2-193">NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="999a2-194">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="999a2-195">AppVM01 ontvangen Hallo SQL-Query en beantwoord</span><span class="sxs-lookup"><span data-stu-id="999a2-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="999a2-196">Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="999a2-197">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="999a2-198">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="999a2-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="999a2-199">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="999a2-200">Hallo SQL antwoord wordt ontvangen en Hallo HTTP-antwoord is voltooid en toohello aanvrager verzendt Hallo IIS-server</span><span class="sxs-lookup"><span data-stu-id="999a2-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="999a2-201">Aangezien er geen uitgaande regels op Hallo Frontend subnet zijn hello antwoord is toegestaan en hello internet ontvangt Hallo webpagina aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="999a2-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="999a2-202">(*Toegestane*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="999a2-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="999a2-203">RDP-sessie tooAppVM01 op BackEnd001.CloudApp.Net:xxxxx waarbij xxxxx Hallo willekeurig toegewezen poort voor RDP tooAppVM01 is serverbeheerder op internet-aanvragen (Hallo toegewezen poort kan worden gevonden op Hallo Azure-portal of via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="999a2-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="999a2-204">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-205">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="999a2-206">NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="999a2-207">Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="999a2-208">RDP-sessie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="999a2-208">RDP session is enabled</span></span>
5. <span data-ttu-id="999a2-209">AppVM01 wordt u gevraagd om het Hallo-gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="999a2-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="999a2-210">(*Toegestane*) Web server opzoeken in DNS op DNS-server</span><span class="sxs-lookup"><span data-stu-id="999a2-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="999a2-211">Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="999a2-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="999a2-212">Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01</span><span class="sxs-lookup"><span data-stu-id="999a2-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="999a2-213">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="999a2-214">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="999a2-215">NSG regel 1 (DNS) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="999a2-216">DNS-server ontvangt Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="999a2-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="999a2-217">DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet</span><span class="sxs-lookup"><span data-stu-id="999a2-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="999a2-218">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="999a2-219">Internet-DNS-server reageert, omdat deze sessie is gestart, intern, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="999a2-220">DNS-server in de cache opgeslagen antwoord Hallo en toohello eerste aanvraag back tooIIS01 reageert</span><span class="sxs-lookup"><span data-stu-id="999a2-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="999a2-221">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="999a2-222">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="999a2-223">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="999a2-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="999a2-224">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="999a2-225">IIS01 ontvangt antwoord Hallo van DNS01</span><span class="sxs-lookup"><span data-stu-id="999a2-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="999a2-226">(*Toegestane*) Web server toegang tot bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="999a2-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="999a2-227">IIS01 vraagt om een bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="999a2-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="999a2-228">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="999a2-229">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-230">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="999a2-231">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="999a2-232">NSG regel 3 (Internet tooIIS01) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="999a2-233">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="999a2-234">AppVM01 hello aanvraag ontvangt en reageert met bestand (ervan uitgaande dat toegang wordt geverifieerd)</span><span class="sxs-lookup"><span data-stu-id="999a2-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="999a2-235">Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="999a2-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="999a2-236">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-237">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="999a2-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="999a2-238">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="999a2-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="999a2-239">Hallo IIS server ontvangt Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="999a2-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="999a2-240">(*Geweigerd*) toobackend webserver</span><span class="sxs-lookup"><span data-stu-id="999a2-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="999a2-241">Een internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess</span><span class="sxs-lookup"><span data-stu-id="999a2-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="999a2-242">Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="999a2-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="999a2-243">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="999a2-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="999a2-244">(*Geweigerd*) opzoeken in Web DNS op DNS-server</span><span class="sxs-lookup"><span data-stu-id="999a2-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="999a2-245">Een internet-gebruiker probeert toolook van een interne DNS-record op DNS01 via Hallo BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="999a2-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="999a2-246">Aangezien er geen eindpunten voor DNS is geopend zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="999a2-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="999a2-247">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: deze regel 1 (DNS) is niet van toepassing om twee redenen, eerste Hallo-bronadres is internet Hallo, deze regel is alleen van toepassing toohello lokale VNet als Hallo bron ook Deze regel wordt een regel voor toestaan, zodat deze zou nooit verkeer weigeren)</span><span class="sxs-lookup"><span data-stu-id="999a2-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="999a2-248">(*Geweigerd*) tooSQL webtoegang via firewall</span><span class="sxs-lookup"><span data-stu-id="999a2-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="999a2-249">Een internetgebruiker opvraagt SQL-gegevens uit FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="999a2-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="999a2-250">Aangezien er geen eindpunten geopend voor SQL zijn, dit verkeer zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="999a2-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="999a2-251">Als eindpunten geopend voor een bepaalde reden zijn, begint Hallo Frontend subnet verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="999a2-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="999a2-252">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="999a2-253">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="999a2-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="999a2-254">NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="999a2-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="999a2-255">Verkeer komt binnen via interne IP-adres van Hallo IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="999a2-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="999a2-256">IIS01 wordt niet geluisterd op poort 1433, zodat er geen reactie toohello aanvraag</span><span class="sxs-lookup"><span data-stu-id="999a2-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="999a2-257">Conclusie</span><span class="sxs-lookup"><span data-stu-id="999a2-257">Conclusion</span></span>
<span data-ttu-id="999a2-258">In dit voorbeeld is een relatief eenvoudige en meteen verder manier Hallo back-end subnet uit binnenkomend verkeer isoleren.</span><span class="sxs-lookup"><span data-stu-id="999a2-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="999a2-259">Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].</span><span class="sxs-lookup"><span data-stu-id="999a2-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="999a2-260">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="999a2-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="999a2-261">Belangrijkste script en netwerk-configuratie</span><span class="sxs-lookup"><span data-stu-id="999a2-261">Main script and network config</span></span>
<span data-ttu-id="999a2-262">Hallo volledige Script opslaat in een PowerShell-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="999a2-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="999a2-263">Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf1.xml'.</span><span class="sxs-lookup"><span data-stu-id="999a2-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="999a2-264">De gebruiker gedefinieerde variabelen Hallo als nodig en Voer Hallo script wijzigen.</span><span class="sxs-lookup"><span data-stu-id="999a2-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="999a2-265">Volledige script</span><span class="sxs-lookup"><span data-stu-id="999a2-265">Full script</span></span>
<span data-ttu-id="999a2-266">Dit script wordt, op basis van Hallo door gebruiker gedefinieerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="999a2-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="999a2-267">Verbinding maken met tooan Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="999a2-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="999a2-268">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="999a2-268">Create a storage account</span></span>
3. <span data-ttu-id="999a2-269">Een VNet en twee subnetten zoals gedefinieerd in het configuratiebestand voor Hallo netwerk maken</span><span class="sxs-lookup"><span data-stu-id="999a2-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="999a2-270">Vier windows server-VM's maken</span><span class="sxs-lookup"><span data-stu-id="999a2-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="999a2-271">Configureer het NSG inclusief:</span><span class="sxs-lookup"><span data-stu-id="999a2-271">Configure NSG including:</span></span>
   * <span data-ttu-id="999a2-272">Maken van een NSG</span><span class="sxs-lookup"><span data-stu-id="999a2-272">Creating an NSG</span></span>
   * <span data-ttu-id="999a2-273">Met regels in te vullen</span><span class="sxs-lookup"><span data-stu-id="999a2-273">Populating it with rules</span></span>
   * <span data-ttu-id="999a2-274">Binding Hallo NSG toohello juiste subnetten</span><span class="sxs-lookup"><span data-stu-id="999a2-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="999a2-275">Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.</span><span class="sxs-lookup"><span data-stu-id="999a2-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="999a2-276">Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="999a2-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="999a2-277">Alleen foutberichten in rood zijn aanleiding.</span><span class="sxs-lookup"><span data-stu-id="999a2-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="999a2-278">Netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="999a2-278">Network config file</span></span>
<span data-ttu-id="999a2-279">Dit xml-bestand opslaan met bijgewerkte locatie en Hallo koppeling toothis bestand toohello $NetworkConfigFile variabele toevoegen in Hallo vóór het script.</span><span class="sxs-lookup"><span data-stu-id="999a2-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="999a2-280">Voorbeeldscripts toepassing</span><span class="sxs-lookup"><span data-stu-id="999a2-280">Sample application scripts</span></span>
<span data-ttu-id="999a2-281">Als u een voorbeeldtoepassing tooinstall voor deze en andere voorbeelden van het Perimeternetwerk wilt, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="999a2-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="999a2-282">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="999a2-282">Next steps</span></span>
* <span data-ttu-id="999a2-283">Bijwerken en XML-bestand opslaan</span><span class="sxs-lookup"><span data-stu-id="999a2-283">Update and save XML file</span></span>
* <span data-ttu-id="999a2-284">Hallo PowerShell script toobuild Hallo-omgeving uitvoeren</span><span class="sxs-lookup"><span data-stu-id="999a2-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="999a2-285">Hallo-voorbeeldtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="999a2-285">Install hello sample application</span></span>
* <span data-ttu-id="999a2-286">Ander verkeer stroomt via deze DMZ testen</span><span class="sxs-lookup"><span data-stu-id="999a2-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inkomende DMZ met NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

