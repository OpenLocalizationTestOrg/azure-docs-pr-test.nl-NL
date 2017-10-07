---
title: "aaaAzure DMZ voorbeeld – een eenvoudige DMZ met nsg's bouwen | Microsoft Docs"
description: Maken van een DMZ met Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="3159f-103">Voorbeeld 1: een eenvoudige DMZ met nsg's met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="3159f-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="3159f-104">[Best Practices beveiligingspagina-grens toohello retourneren][HOME]</span><span class="sxs-lookup"><span data-stu-id="3159f-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3159f-105">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="3159f-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="3159f-106">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3159f-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="3159f-107">In dit voorbeeld maakt een primitieve DMZ met vier Windows-servers en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="3159f-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="3159f-108">In dit voorbeeld worden alle Hallo gewenste sjabloon secties tooprovide een beter begrip van elke stap beschreven.</span><span class="sxs-lookup"><span data-stu-id="3159f-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="3159f-109">Er is ook een sectie verkeer Scenario tooprovide een diepgaande stapsgewijze blik op hoe verkeer Hallo lagen verdediging in Hallo DMZ doorlopen.</span><span class="sxs-lookup"><span data-stu-id="3159f-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="3159f-110">Ten slotte is in de sectie Verwijzingen Hallo het Hallo volledige sjabloon code en instructies toobuild deze omgeving tootest en experiment met verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="3159f-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="3159f-111">![Inkomende DMZ met NSG][1]</span><span class="sxs-lookup"><span data-stu-id="3159f-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="3159f-112">Beschrijving van de omgeving</span><span class="sxs-lookup"><span data-stu-id="3159f-112">Environment description</span></span>
<span data-ttu-id="3159f-113">In dit voorbeeld bevat een abonnement Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="3159f-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="3159f-114">Één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="3159f-114">A single resource group</span></span>
* <span data-ttu-id="3159f-115">Een virtueel netwerk met twee subnetten; 'FrontEnd' en back-end'</span><span class="sxs-lookup"><span data-stu-id="3159f-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="3159f-116">Een Netwerkbeveiligingsgroep die toegepaste tooboth subnetten</span><span class="sxs-lookup"><span data-stu-id="3159f-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="3159f-117">Een Windows-Server waarmee een toepassing webserver ('IIS01')</span><span class="sxs-lookup"><span data-stu-id="3159f-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="3159f-118">Twee windows-servers die vertegenwoordigen toepassingsservers van back-end ('AppVM01', 'AppVM02')</span><span class="sxs-lookup"><span data-stu-id="3159f-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="3159f-119">Een Windows-server met een DNS-server ('DNS01')</span><span class="sxs-lookup"><span data-stu-id="3159f-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="3159f-120">Een openbaar IP-adres die zijn gekoppeld aan de webserver Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="3159f-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="3159f-121">In de sectie Verwijzingen hello is er een koppeling tooan Azure Resource Manager-sjabloon die Hallo-omgeving beschreven in dit voorbeeld voortbouwt.</span><span class="sxs-lookup"><span data-stu-id="3159f-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="3159f-122">Gebouw Hallo VM's en virtuele netwerken worden Hoewel uitgevoerd door Hallo voorbeeldsjabloon, niet in dit document uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="3159f-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="3159f-123">**toobuild deze omgeving** (gedetailleerde instructies vindt u in Hallo verwijzingen sectie van dit document);</span><span class="sxs-lookup"><span data-stu-id="3159f-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="3159f-124">Implementatie van Azure Resource Manager-sjabloon op Hallo: [Azure Quick Start-sjablonen][Template]</span><span class="sxs-lookup"><span data-stu-id="3159f-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="3159f-125">Installeren van de voorbeeldtoepassing Hallo op: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="3159f-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="3159f-126">tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'.</span><span class="sxs-lookup"><span data-stu-id="3159f-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="3159f-127">Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.</span><span class="sxs-lookup"><span data-stu-id="3159f-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="3159f-128">Een openbaar IP-adres kan ook worden gekoppeld aan elke server NIC voor RDP eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="3159f-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="3159f-129">Hallo bevatten volgende secties een gedetailleerde beschrijving van Hallo Netwerkbeveiligingsgroep en hoe werkt dit voorbeeld door de stap voor stap regels Hallo Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3159f-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="3159f-130">Netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="3159f-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="3159f-131">In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels.</span><span class="sxs-lookup"><span data-stu-id="3159f-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="3159f-132">In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels.</span><span class="sxs-lookup"><span data-stu-id="3159f-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="3159f-133">Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="3159f-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="3159f-134">Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="3159f-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="3159f-135">NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).</span><span class="sxs-lookup"><span data-stu-id="3159f-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="3159f-136">Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:</span><span class="sxs-lookup"><span data-stu-id="3159f-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="3159f-137">Interne DNS-verkeer (poort 53) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="3159f-138">RDP-verkeer (poort 3389) van Hallo Internet tooany VM is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="3159f-139">HTTP-verkeer (poort 80) van Hallo tooweb internetserver (IIS01) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="3159f-140">Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="3159f-141">Verkeer (alle poorten) van Hallo Internet toohello hele VNet (beide subnetten) is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="3159f-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="3159f-142">Verkeer (alle poorten) van Hallo Frontend subnet toohello back-end-subnet is geweigerd</span><span class="sxs-lookup"><span data-stu-id="3159f-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="3159f-143">Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn, maar omdat de regel 3 heeft een hogere prioriteit alleen zou worden toegepast en regel 5 niet in de play zou komen.</span><span class="sxs-lookup"><span data-stu-id="3159f-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="3159f-144">Hallo HTTP-aanvraag zou dus toohello webserver toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="3159f-145">Als dat dezelfde verkeer tooreach hello DNS01 server probeerde, zou regel 5 (weigeren) zijn de eerste tooapply en Hallo verkeer Hallo zou niet toegestaan toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="3159f-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="3159f-146">Regel 6 (weigeren) blokkeert Hallo Frontend subnet uit praten toohello back-end-subnet (met uitzondering van toegestane regels 1 en 4-verkeer), deze regelset beschermt Hallo back-end-netwerk als een aanvaller inbreuk Hallo webtoepassing op Hallo Frontend, Hallo aanvaller zou beperkte toegang toohello back-end '-beveiliging gebruiken' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).</span><span class="sxs-lookup"><span data-stu-id="3159f-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="3159f-147">Er is een uitgaande standaardregel waarmee verkeer van toohello internet.</span><span class="sxs-lookup"><span data-stu-id="3159f-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="3159f-148">Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3159f-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="3159f-149">tooapply beveiliging beleid tootraffic in beide richtingen, de gebruiker gedefinieerde routering is vereist en in 'Voorbeeld 3' is verkend op Hallo [Best Practices beveiligingspagina-grens][HOME].</span><span class="sxs-lookup"><span data-stu-id="3159f-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="3159f-150">Elke regel is als volgt in meer detail besproken:</span><span class="sxs-lookup"><span data-stu-id="3159f-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="3159f-151">De bron van een Netwerkbeveiligingsgroep moet geïnstantieerd toohold Hallo regels:</span><span class="sxs-lookup"><span data-stu-id="3159f-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="3159f-152">de eerste regel Hallo in dit voorbeeld kunt DNS-verkeer tussen alle interne netwerken toohello DNS-server op Hallo back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="3159f-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="3159f-153">Hallo regel heeft enkele belangrijke parameters:</span><span class="sxs-lookup"><span data-stu-id="3159f-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="3159f-154">'destinationAddressPrefix' - regels kunnen gebruiken een speciaal type adresvoorvoegsel een "standaard code' genoemd, deze tags zijn systeem-id's die een grotere categorie van adresvoorvoegsels voor een eenvoudige manier tooaddress toestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="3159f-155">Deze regel gebruikt standaard Tag 'Internet' Hallo toosignify een adres buiten Hallo VNet.</span><span class="sxs-lookup"><span data-stu-id="3159f-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="3159f-156">Andere labels voorvoegsel zijn VirtualNetwork en AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="3159f-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="3159f-157">'Richting' geeft aan in welke richting van verkeer met deze regel wordt van kracht.</span><span class="sxs-lookup"><span data-stu-id="3159f-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="3159f-158">Hallo richting is vanuit Hallo perspectief van Hallo subnet of een virtuele Machine (afhankelijk van waar deze NSG is gekoppeld).</span><span class="sxs-lookup"><span data-stu-id="3159f-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="3159f-159">Dus als richting is 'Inkomend' en verkeer is Hallo subnet invoeren, Hallo regel van toepassing en Hallo subnet uitgaand verkeer niet wordt beïnvloed door deze regel.</span><span class="sxs-lookup"><span data-stu-id="3159f-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="3159f-160">'Prioriteit' stelt Hallo volgorde waarin netwerkverkeer wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="3159f-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="3159f-161">Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="3159f-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="3159f-162">Wanneer een regel van toepassing tooa specifieke netwerkverkeer is, kan er geen verdere regels worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3159f-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="3159f-163">Dus als een regel met prioriteit 1 gegevensverkeer, en een regel met prioriteit 2 verkeer weigert, en beide regels zijn van toepassing tootraffic vervolgens Hallo verkeer tooflow mogen (omdat de regel 1 een hogere prioriteit heeft geduurd effect en geen verdere regels zijn toegepast).</span><span class="sxs-lookup"><span data-stu-id="3159f-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="3159f-164">'Toegang' geeft aan of verkeer dat is beïnvloed door deze regel is geblokkeerd ("Deny") of toegestane ('toestaan').</span><span class="sxs-lookup"><span data-stu-id="3159f-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="3159f-165">Deze regel kunnen de RDP-verkeer tooflow vanaf internet toohello RDP-poort op elke server op Hallo Hallo gebonden subnet.</span><span class="sxs-lookup"><span data-stu-id="3159f-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="3159f-166">Deze regel kunnen binnenkomende internet verkeer toohit Hallo webserver.</span><span class="sxs-lookup"><span data-stu-id="3159f-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="3159f-167">Deze regel wordt het routeringsgedrag Hallo niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3159f-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="3159f-168">Hallo regel kunnen alleen verkeer dat is bestemd voor IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="3159f-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="3159f-169">Dus als verkeer van Internet Hallo Hallo webserver als de bestemming voor deze regel zou toe te staan en stoppen met het verwerken van verdere regels had.</span><span class="sxs-lookup"><span data-stu-id="3159f-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="3159f-170">(In de regel Hallo met prioriteit 140 alle andere Binnenkomend internetverkeer wordt geblokkeerd).</span><span class="sxs-lookup"><span data-stu-id="3159f-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="3159f-171">Als u alleen HTTP-verkeer wordt verwerkt, met deze regel kan worden verder beperkt tooonly toestaan bestemming poort 80.</span><span class="sxs-lookup"><span data-stu-id="3159f-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="3159f-172">Deze regel kan verkeer toopass van Hallo IIS01 server toohello AppVM01 server, een hoger regel blokkeert al het andere Frontend tooBackend verkeer.</span><span class="sxs-lookup"><span data-stu-id="3159f-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="3159f-173">tooimprove deze regel als Hallo poort bekend is dat moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3159f-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="3159f-174">Bijvoorbeeld, als Hallo IIS-server alleen SQL Server op AppVM01 roept is, Hallo Doelpoortbereik moet worden gewijzigd van ' * ' (Any) too1433 (hello SQL-poort) waardoor een kleinere inkomende kwetsbaarheid voor aanvallen op AppVM01 of webtoepassing Hallo ooit verdacht.</span><span class="sxs-lookup"><span data-stu-id="3159f-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="3159f-175">Deze regel weigert verkeer van Hallo internet tooany servers op Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="3159f-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="3159f-176">Met regels met prioriteit 110 en 120 Hallo Hallo effect is tooallow alleen inkomend verkeer toohello firewall voor internet- en RDP-poorten op servers en blokkeert al het andere.</span><span class="sxs-lookup"><span data-stu-id="3159f-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="3159f-177">Deze regel is een 'veiligheidsmaatregel' regel tooblock alle onverwachte stromen.</span><span class="sxs-lookup"><span data-stu-id="3159f-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="3159f-178">de laatste regel Hallo weigert verkeer van Hallo Frontend subnet toohello back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="3159f-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="3159f-179">Aangezien deze regel een inkomende regel alleen is, is (van Hallo back-end toohello Frontend) omgekeerde verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="3159f-180">Verkeer scenario 's</span><span class="sxs-lookup"><span data-stu-id="3159f-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="3159f-181">(*Toegestane*) tooweb internetserver</span><span class="sxs-lookup"><span data-stu-id="3159f-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="3159f-182">Een internet-gebruiker aanvragen een pagina http-van het openbare IP-adres Hallo Hallo NIC die is gekoppeld aan Hallo IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="3159f-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="3159f-183">Hallo openbare IP-adres wordt doorgegeven verkeer toohello VNet naar IIS01 (Hallo webserver)</span><span class="sxs-lookup"><span data-stu-id="3159f-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="3159f-184">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-185">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="3159f-186">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="3159f-187">NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3159f-188">Verkeer komt binnen via interne IP-adres van de webserver Hallo IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="3159f-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="3159f-189">IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag</span><span class="sxs-lookup"><span data-stu-id="3159f-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="3159f-190">IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="3159f-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="3159f-191">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="3159f-192">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-193">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="3159f-194">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="3159f-195">NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="3159f-196">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="3159f-197">AppVM01 ontvangen Hallo SQL-Query en beantwoord</span><span class="sxs-lookup"><span data-stu-id="3159f-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="3159f-198">Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="3159f-199">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-200">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="3159f-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="3159f-201">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="3159f-202">Hallo SQL antwoord wordt ontvangen en Hallo HTTP-antwoord is voltooid en toohello aanvrager verzendt Hallo IIS-server</span><span class="sxs-lookup"><span data-stu-id="3159f-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="3159f-203">Aangezien er geen uitgaande regels op Hallo Frontend subnet zijn, antwoord Hallo is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="3159f-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="3159f-204">(*Toegestane*) RDP tooIIS server</span><span class="sxs-lookup"><span data-stu-id="3159f-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="3159f-205">Een serverbeheerder op internet vraagt een tooIIS01 RDP-sessie op het openbare IP-adres Hallo Hallo NIC die is gekoppeld aan Hallo IIS01 NIC (dit openbare IP-adres kan worden gevonden via Hallo Portal of PowerShell)</span><span class="sxs-lookup"><span data-stu-id="3159f-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="3159f-206">Hallo openbare IP-adres wordt doorgegeven verkeer toohello VNet naar IIS01 (Hallo webserver)</span><span class="sxs-lookup"><span data-stu-id="3159f-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="3159f-207">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-208">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="3159f-209">NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3159f-210">Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="3159f-211">RDP-sessie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3159f-211">RDP session is enabled</span></span>
6. <span data-ttu-id="3159f-212">IIS01 wordt u gevraagd om het Hallo-gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3159f-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="3159f-213">tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'.</span><span class="sxs-lookup"><span data-stu-id="3159f-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="3159f-214">Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.</span><span class="sxs-lookup"><span data-stu-id="3159f-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="3159f-215">(*Toegestane*) Web server opzoeken in DNS op DNS-server</span><span class="sxs-lookup"><span data-stu-id="3159f-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="3159f-216">Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="3159f-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="3159f-217">Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01</span><span class="sxs-lookup"><span data-stu-id="3159f-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="3159f-218">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="3159f-219">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="3159f-220">NSG regel 1 (DNS) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="3159f-221">DNS-server ontvangt Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="3159f-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="3159f-222">DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet</span><span class="sxs-lookup"><span data-stu-id="3159f-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="3159f-223">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="3159f-224">Internet-DNS-server reageert, omdat deze sessie is gestart, intern, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="3159f-225">DNS-server in de cache opgeslagen antwoord Hallo en toohello eerste aanvraag back tooIIS01 reageert</span><span class="sxs-lookup"><span data-stu-id="3159f-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="3159f-226">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="3159f-227">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-228">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="3159f-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="3159f-229">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="3159f-230">IIS01 ontvangt antwoord Hallo van DNS01</span><span class="sxs-lookup"><span data-stu-id="3159f-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="3159f-231">(*Toegestane*) Web server toegang tot bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="3159f-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="3159f-232">IIS01 vraagt om een bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="3159f-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="3159f-233">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="3159f-234">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-235">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="3159f-236">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="3159f-237">NSG regel 3 (Internet tooIIS01) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="3159f-238">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3159f-239">AppVM01 hello aanvraag ontvangt en reageert met bestand (ervan uitgaande dat toegang wordt geverifieerd)</span><span class="sxs-lookup"><span data-stu-id="3159f-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="3159f-240">Aangezien er geen uitgaande regels op Hallo back-end-subnet zijn, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="3159f-241">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-242">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="3159f-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="3159f-243">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="3159f-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="3159f-244">Hallo IIS server ontvangt Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="3159f-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="3159f-245">(*Geweigerd*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="3159f-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="3159f-246">Een internet-gebruiker probeert tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="3159f-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="3159f-247">Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="3159f-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3159f-248">Maar als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, NSG-regel 2 (RDP) zou dit verkeer toestaan</span><span class="sxs-lookup"><span data-stu-id="3159f-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="3159f-249">tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'.</span><span class="sxs-lookup"><span data-stu-id="3159f-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="3159f-250">Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.</span><span class="sxs-lookup"><span data-stu-id="3159f-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="3159f-251">(*Geweigerd*) toobackend webserver</span><span class="sxs-lookup"><span data-stu-id="3159f-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="3159f-252">Een internet-gebruiker probeert een bestand op AppVM01 tooaccess</span><span class="sxs-lookup"><span data-stu-id="3159f-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="3159f-253">Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="3159f-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3159f-254">Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="3159f-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="3159f-255">(*Geweigerd*) opzoeken in Web DNS op DNS-server</span><span class="sxs-lookup"><span data-stu-id="3159f-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="3159f-256">Een internet-gebruiker probeert toolook van een interne DNS-record op DNS01</span><span class="sxs-lookup"><span data-stu-id="3159f-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="3159f-257">Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="3159f-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3159f-258">Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: of regel 1 (DNS) niet van toepassing hello verzoeken bronadres is internet Hallo en regel 1 zijn alleen van toepassing toohello lokale VNet als Hallo bron)</span><span class="sxs-lookup"><span data-stu-id="3159f-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="3159f-259">(*Geweigerd*) toegang tot SQL op Hallo-webserver</span><span class="sxs-lookup"><span data-stu-id="3159f-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="3159f-260">Een internetgebruiker opvraagt SQL-gegevens uit IIS01</span><span class="sxs-lookup"><span data-stu-id="3159f-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="3159f-261">Aangezien er geen openbare IP-adressen die zijn gekoppeld aan deze servers NIC zijn, dit verkeer voert nooit Hallo VNet en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="3159f-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3159f-262">Als een openbaar IP-adres is ingeschakeld voor een bepaalde reden, begint Hallo Frontend subnet verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="3159f-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="3159f-263">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="3159f-264">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="3159f-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="3159f-265">NSG regel 3 (Internet tooIIS01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="3159f-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3159f-266">Verkeer komt binnen via interne IP-adres van Hallo IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="3159f-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="3159f-267">IIS01 wordt niet geluisterd op poort 1433, zodat er geen reactie toohello aanvraag</span><span class="sxs-lookup"><span data-stu-id="3159f-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="3159f-268">Conclusie</span><span class="sxs-lookup"><span data-stu-id="3159f-268">Conclusion</span></span>
<span data-ttu-id="3159f-269">In dit voorbeeld is een relatief eenvoudige en meteen verder manier Hallo back-end subnet uit binnenkomend verkeer isoleren.</span><span class="sxs-lookup"><span data-stu-id="3159f-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="3159f-270">Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].</span><span class="sxs-lookup"><span data-stu-id="3159f-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="3159f-271">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="3159f-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="3159f-272">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="3159f-272">Azure Resource Manager template</span></span>
<span data-ttu-id="3159f-273">In dit voorbeeld wordt een vooraf gedefinieerde Azure Resource Manager-sjabloon gebruikt in een door Microsoft beheerde GitHub-opslagplaats en open toohello community.</span><span class="sxs-lookup"><span data-stu-id="3159f-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="3159f-274">Deze sjabloon kan worden geïmplementeerd rechtstreeks uit de GitHub of gedownload en gewijzigd toofit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="3159f-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="3159f-275">Hallo belangrijkste sjabloon is in het Hallo-bestand met de naam 'azuredeploy.json'.</span><span class="sxs-lookup"><span data-stu-id="3159f-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="3159f-276">Deze sjabloon kan worden verzonden via PowerShell of CLI (met Hallo gekoppeld 'azuredeploy.parameters.json'-bestand) toodeploy deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3159f-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="3159f-277">Ik vinden Hallo eenvoudigste manier is toouse Hallo 'TooAzure implementeren' knop op Hallo README.md pagina op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3159f-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="3159f-278">toodeploy hello sjabloon die in dit voorbeeld voortbouwt GitHub en hello Azure-portal, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="3159f-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="3159f-279">Navigeer via een browser toohello [sjabloon][Template]</span><span class="sxs-lookup"><span data-stu-id="3159f-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="3159f-280">Klik op Hallo 'TooAzure implementeren' knop (of Hallo 'Visualiseren' knop toosee een grafische weergave van deze sjabloon)</span><span class="sxs-lookup"><span data-stu-id="3159f-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="3159f-281">Hallo Storage-Account, gebruikersnaam en wachtwoord invoeren in de blade Parameters Hallo en klik vervolgens op **OK**</span><span class="sxs-lookup"><span data-stu-id="3159f-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="3159f-282">Maak een resourcegroep voor deze implementatie (u kunt een bestaande, maar ik het beste een nieuw wachtwoord voor de beste resultaten)</span><span class="sxs-lookup"><span data-stu-id="3159f-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="3159f-283">Wijzig indien nodig, Hallo abonnement en de locatie-instellingen voor uw VNet.</span><span class="sxs-lookup"><span data-stu-id="3159f-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="3159f-284">Klik op **juridische voorwaarden bekijken**, Hallo voorwaarden lezen en klikt u op **aankoop** tooagree.</span><span class="sxs-lookup"><span data-stu-id="3159f-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="3159f-285">Klik op **maken** toobegin Hallo implementatie van deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3159f-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="3159f-286">Nadat de Hallo-implementatie wordt voltooid, gaat u toohello die resourcegroep voor deze implementatie toosee Hallo bronnen gemaakt binnen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3159f-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="3159f-287">Deze sjabloon kunt RDP toohello IIS01 alleen server (zoeken hello openbare IP-adres voor IIS01 op Hallo Portal).</span><span class="sxs-lookup"><span data-stu-id="3159f-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="3159f-288">tooRDP tooany back-end-servers in dit geval wordt Hallo IIS-server wordt gebruikt als een 'jump vak'.</span><span class="sxs-lookup"><span data-stu-id="3159f-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="3159f-289">Eerste RDP toohello IIS-server en vervolgens naar Hallo IIS Server RDP toohello back-end-server.</span><span class="sxs-lookup"><span data-stu-id="3159f-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="3159f-290">tooremove voor deze implementatie, delete Hallo resourcegroep en alle onderliggende resources worden eveneens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3159f-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="3159f-291">Voorbeeldscripts toepassing</span><span class="sxs-lookup"><span data-stu-id="3159f-291">Sample application scripts</span></span>
<span data-ttu-id="3159f-292">Als Hallo sjabloon uitgevoerd is, kunt u met een eenvoudige web application tooallow testen met deze configuratie DMZ up Hallo-webserver en appserver instellen.</span><span class="sxs-lookup"><span data-stu-id="3159f-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="3159f-293">een voorbeeldtoepassing voor deze en andere voorbeelden DMZ tooinstall, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="3159f-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3159f-294">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3159f-294">Next steps</span></span>

* <span data-ttu-id="3159f-295">In dit voorbeeld implementeren</span><span class="sxs-lookup"><span data-stu-id="3159f-295">Deploy this example</span></span>
* <span data-ttu-id="3159f-296">Hallo-voorbeeldtoepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="3159f-296">Build hello sample application</span></span>
* <span data-ttu-id="3159f-297">Ander verkeer stroomt via deze DMZ testen</span><span class="sxs-lookup"><span data-stu-id="3159f-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inkomende DMZ met NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md