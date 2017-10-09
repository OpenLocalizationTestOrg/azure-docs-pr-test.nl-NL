---
title: 'Voorbeeld: aaaDMZ bouwen een DMZ tooProtect netwerken met een Firewall, UDR en NSG | Microsoft Docs'
description: Maken van een DMZ met een Firewall, de gebruiker gedefinieerde Routering en Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="f06a7-103">Voorbeeld 3: een DMZ tooProtect bouwen netwerken met een Firewall, UDR en NSG</span><span class="sxs-lookup"><span data-stu-id="f06a7-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="f06a7-104">[Best Practices beveiligingspagina-grens toohello retourneren][HOME]</span><span class="sxs-lookup"><span data-stu-id="f06a7-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="f06a7-105">In dit voorbeeld wordt een DMZ gemaakt met een firewall, vier windows-servers, gebruiker gedefinieerde routering, doorsturen via IP en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="f06a7-106">Deze ook begeleidt bij elk Hallo relevante opdrachten tooprovide een beter begrip van elke stap.</span><span class="sxs-lookup"><span data-stu-id="f06a7-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="f06a7-107">Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ.</span><span class="sxs-lookup"><span data-stu-id="f06a7-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="f06a7-108">Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="f06a7-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="f06a7-109">![Bidirectionele DMZ met NVA, NSG en UDR][1]</span><span class="sxs-lookup"><span data-stu-id="f06a7-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="f06a7-110">Instellen van de omgeving</span><span class="sxs-lookup"><span data-stu-id="f06a7-110">Environment Setup</span></span>
<span data-ttu-id="f06a7-111">In dit voorbeeld is er een abonnement dat Hallo volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="f06a7-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="f06a7-112">Drie cloudservices: 'SecSvc001', 'FrontEnd001' en 'BackEnd001'</span><span class="sxs-lookup"><span data-stu-id="f06a7-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="f06a7-113">Een virtueel netwerk 'CorpNetwork' met drie subnetten: 'SecNet', 'FrontEnd' en back-end'</span><span class="sxs-lookup"><span data-stu-id="f06a7-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="f06a7-114">Een virtueel netwerkapparaat, in dit voorbeeld van een firewall, verbonden toohello SecNet subnet</span><span class="sxs-lookup"><span data-stu-id="f06a7-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="f06a7-115">Een Windows-Server waarmee een toepassing webserver ('IIS01')</span><span class="sxs-lookup"><span data-stu-id="f06a7-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="f06a7-116">Twee windows-servers die toepassing terug vertegenwoordigen end servers ('AppVM01', 'AppVM02')</span><span class="sxs-lookup"><span data-stu-id="f06a7-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="f06a7-117">Een Windows-server met een DNS-server ('DNS01')</span><span class="sxs-lookup"><span data-stu-id="f06a7-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="f06a7-118">In onderstaande Hallo verwijzingen gedeelte is er een PowerShell-script dat de meeste Hallo-omgeving die hierboven worden beschreven bouwt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="f06a7-119">Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="f06a7-120">toobuild hello omgeving:</span><span class="sxs-lookup"><span data-stu-id="f06a7-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="f06a7-121">Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="f06a7-122">Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="f06a7-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="f06a7-123">Hallo-script uitvoeren in PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06a7-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="f06a7-124">**Opmerking**: Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="f06a7-125">Zodra het Hallo-script wordt uitgevoerd kan Hallo na script stappen kan worden genomen:</span><span class="sxs-lookup"><span data-stu-id="f06a7-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="f06a7-126">Hallo-firewallregels instellen, deze procedure wordt besproken in Hallo onderstaande sectie met de titel: Beschrijving van de Firewall-regel.</span><span class="sxs-lookup"><span data-stu-id="f06a7-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="f06a7-127">Optioneel zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.</span><span class="sxs-lookup"><span data-stu-id="f06a7-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="f06a7-128">Zodra het Hallo-script is uitgevoerd Hallo firewallregels moet toobe voltooid, moet deze procedure wordt besproken in het gedeelte Hallo: Firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="f06a7-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="f06a7-129">Door de gebruiker gedefinieerde Routering</span><span class="sxs-lookup"><span data-stu-id="f06a7-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="f06a7-130">Standaard worden Hallo na systeemroutes gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="f06a7-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="f06a7-131">Hallo VNETLocal is altijd Hallo gedefinieerd adres prefix(en) Hallo VNet voor die specifieke netwerk (ie wordt gewijzigd van VNet tooVNet, afhankelijk van hoe elke specifieke VNet is gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="f06a7-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="f06a7-132">Hallo resterende systeemroutes zijn statisch en standaard als hierboven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="f06a7-133">Als voor de prioriteit, routes worden verwerkt via Hallo langste voorvoegsel overeen (LPM)-methode, dus hello meest specifiek route in de tabel Hallo zou gelden tooa gegeven doeladres.</span><span class="sxs-lookup"><span data-stu-id="f06a7-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="f06a7-134">Verkeer (bijvoorbeeld toohello DNS01 server, 10.0.2.4) bedoeld voor LAN hello (10.0.0.0/16) zouden daarom worden gerouteerd via Hallo VNet tooits bestemming vanwege toohello 10.0.0.0/16 route.</span><span class="sxs-lookup"><span data-stu-id="f06a7-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="f06a7-135">Met andere woorden, voor 10.0.2.4 is Hallo 10.0.0.0/16 route het meest specifiek route hello, hoewel Hallo 10.0.0.0/8 en 0.0.0.0/0 ook kunnen toegepast, maar omdat deze minder specifiek zijn ze niet op dit verkeer.</span><span class="sxs-lookup"><span data-stu-id="f06a7-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="f06a7-136">Hallo verkeer too10.0.2.4 zou daarom de volgende hop Hallo lokale VNet en gewoon routeren toohello doel hebben.</span><span class="sxs-lookup"><span data-stu-id="f06a7-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="f06a7-137">Als verkeer is bedoeld voor 10.1.1.1 bijvoorbeeld, Hallo 10.0.0.0/16 route toepassen wouldn't, maar Hallo 10.0.0.0/8 Hallo meest specifiek zijn zou en dit verkeer Hallo zou worden verwijderd ('zwart gaan') omdat de volgende hop Hallo Null is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="f06a7-138">Als bestemming Hallo tooany van Hallo Null voorvoegsels of Hallo VNETLocal voorvoegsels niet toepassen en klik vervolgens het minst specifiek Hallo volgt routeren, 0.0.0.0/0 en toohello Internet, zoals de volgende hop Hallo en dus uit de rand van de Azure internet worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="f06a7-139">Als er twee identieke voorvoegsels in de routetabel hello, volgt Hallo Hallo-volgorde van voorkeur op basis van Hallo routes 'bron'-kenmerk:</span><span class="sxs-lookup"><span data-stu-id="f06a7-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="f06a7-140">'VirtualAppliance' een door de gebruiker gedefinieerde handmatig toegevoegde toohello routetabel =</span><span class="sxs-lookup"><span data-stu-id="f06a7-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="f06a7-141">'VPNGateway' een dynamische Route BGP (gebruikt in combinatie met hybride netwerken), = toegevoegd door een dynamische netwerkprotocol, deze routes kunnen op den duur veranderen als dynamische Hallo-protocol wordt automatisch in het netwerk als peer is ingesteld aangepast</span><span class="sxs-lookup"><span data-stu-id="f06a7-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="f06a7-142">'Standaard' hello Systeemroutes, = Hallo lokale VNet en Hallo statische vermeldingen, zoals wordt weergegeven in de routetabel Hallo hierboven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="f06a7-143">U kunt nu de gebruiker gedefinieerde routering (UDR) gebruiken met ExpressRoute- en VPN-Gateways tooforce uitgaande en binnenkomende cross-premises verkeer toobe gerouteerde tooa netwerk virtueel apparaat (NVA).</span><span class="sxs-lookup"><span data-stu-id="f06a7-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="f06a7-144">Hallo maken lokale routes</span><span class="sxs-lookup"><span data-stu-id="f06a7-144">Creating hello local routes</span></span>
<span data-ttu-id="f06a7-145">In dit voorbeeld worden twee routeringstabellen nodig, één voor Hallo front-end- en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="f06a7-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="f06a7-146">Elke tabel is geladen met statische routes die geschikt is voor Hallo opgegeven subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="f06a7-147">Voor Hallo doel van dit voorbeeld heeft elke tabel drie routes:</span><span class="sxs-lookup"><span data-stu-id="f06a7-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="f06a7-148">Lokaal subnetverkeer geen volgende Hop gedefinieerd tooallow lokale subnet verkeer toobypass Hallo firewall</span><span class="sxs-lookup"><span data-stu-id="f06a7-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="f06a7-149">Virtueel netwerkverkeer met een volgende Hop gedefinieerd als een firewall, overschrijft dit Hallo standaardregel waarmee lokale tooroute voor VNet-verkeer rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="f06a7-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="f06a7-150">Alle resterende verkeer (0/0) met de volgende Hop gedefinieerd als een firewall Hallo</span><span class="sxs-lookup"><span data-stu-id="f06a7-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="f06a7-151">Ze zijn gebonden tootheir subnetten als Hallo routeringstabellen zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="f06a7-152">Voor Hallo Frontend subnet routeringstabel nadat gemaakt en gekoppeld ziet toohello subnet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="f06a7-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="f06a7-153">Hallo volgende opdrachten in dit voorbeeld gebruikte toobuild Hallo routetabel zijn, een door de gebruiker gedefinieerde route toevoegen en vervolgens binden Hallo route tabel tooa subnet (Opmerking; de items onder die begint met een dollarteken (bijvoorbeeld: $BESubnet) zijn van de gebruiker gedefinieerde variabelen uit het Hallo-script in Hallo verwijzing sectie van dit document):</span><span class="sxs-lookup"><span data-stu-id="f06a7-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="f06a7-154">Eerste Hallo base routeringstabel moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-154">First hello base routing table must be created.</span></span> <span data-ttu-id="f06a7-155">Dit fragment toont Hallo maken van Hallo tabel voor Hallo back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="f06a7-156">Hallo-script wordt ook een bijbehorende tabel gemaakt voor Hallo Frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="f06a7-157">Nieuwe AzureRouteTable-naam $BERouteTableName '</span><span class="sxs-lookup"><span data-stu-id="f06a7-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="f06a7-158">Zodra de routetabel Hallo is gemaakt, kunnen specifieke gebruiker gedefinieerde routes worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="f06a7-159">In deze snipped worden al het verkeer (0.0.0.0/0) gerouteerd via Hallo virtueel apparaat (een variabele, $VMIP [0], is de gebruikte toopass Hallo IP-adres is toegewezen als virtueel apparaat Hallo eerder in Hallo-script is gemaakt).</span><span class="sxs-lookup"><span data-stu-id="f06a7-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="f06a7-160">In Hallo-script wordt een bijbehorende regel ook in Hallo Frontend tabel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="f06a7-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="f06a7-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="f06a7-162">Hallo boven route item overschrijft de standaardroute '0.0.0.0/0' hello, maar Hallo 10.0.0.0/16 standaardregel nog steeds bestaande zou waarmee verkeer binnen Hallo VNet tooroute rechtstreeks toohello doel en niet toohello virtueel netwerkapparaat.</span><span class="sxs-lookup"><span data-stu-id="f06a7-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="f06a7-163">toocorrect die dit gedrag Hallo Volg regel moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="f06a7-164">Er is op dit moment een toobe keuze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="f06a7-165">Hello hierboven twee routes wordt al het verkeer routeren toohello firewall voor de beoordeling, zelfs verkeer binnen één subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="f06a7-166">Dit kan nodig zijn, maar tooallow verkeer binnen een subnet tooroute lokaal zonder betrokkenheid van Hallo firewall een derde, zeer specifieke regel kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="f06a7-167">Deze route statussen van een adres voor het lokale subnet Hallo kunt just destine routeren er rechtstreeks (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="f06a7-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="f06a7-168">Ten slotte met Hallo routeringstabel gemaakt en gevuld met een gebruiker gedefinieerde routes, moet Hallo tabel nu zijn gebonden tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="f06a7-169">Hallo-front-end-routetabel is in Hallo-script wordt ook afhankelijke toohello subnet Frontend.</span><span class="sxs-lookup"><span data-stu-id="f06a7-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="f06a7-170">Hier volgt Hallo binding script voor Hallo back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="f06a7-171">Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '</span><span class="sxs-lookup"><span data-stu-id="f06a7-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="f06a7-172">Doorsturen via IP</span><span class="sxs-lookup"><span data-stu-id="f06a7-172">IP Forwarding</span></span>
<span data-ttu-id="f06a7-173">Een tooUDR companion-functie is doorsturen via IP.</span><span class="sxs-lookup"><span data-stu-id="f06a7-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="f06a7-174">Dit is een instelling in een virtueel apparaat waarmee het tooreceive verkeer niet specifiek gericht toohello toestel en vervolgens doorsturen die verkeer tooits uiteindelijke bestemming.</span><span class="sxs-lookup"><span data-stu-id="f06a7-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="f06a7-175">Bijvoorbeeld als een aanvraag toohello DNS01 server, kunt u verkeer van AppVM01 zou UDR routeren deze toohello-firewall.</span><span class="sxs-lookup"><span data-stu-id="f06a7-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="f06a7-176">Met doorsturen via IP is ingeschakeld, wordt het verkeer Hallo voor Hallo DNS01 doel (10.0.2.4) worden geaccepteerd door Hallo toestel (10.0.0.4) en vervolgens doorgestuurd tooits uiteindelijke bestemming (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="f06a7-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="f06a7-177">Zonder doorsturen via IP ingeschakeld op Hallo Firewall, zou verkeer niet geaccepteerd door Hallo toestel Hoewel routetabel Hallo Hallo firewall als Hallo volgende hop is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f06a7-178">Het is essentieel tooremember tooenable doorsturen via IP in combinatie met de gebruiker gedefinieerde routering.</span><span class="sxs-lookup"><span data-stu-id="f06a7-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="f06a7-179">Instellen van het doorsturen via IP is één opdracht en kan worden uitgevoerd tijdens de aanmaak van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f06a7-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="f06a7-180">Voor Hallo stroom van dit voorbeeld Hallo-codefragment aan Hallo einde van het Hallo-script en gegroepeerd met Hallo UDR opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f06a7-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="f06a7-181">Bellen Hallo VM-instantie die uw virtuele apparaat, firewall in dit geval Hallo en doorsturen via IP inschakelen (Opmerking; een item in rood die begint met een dollarteken (bijvoorbeeld: $VMName[0]) is een door de gebruiker gedefinieerde variabele uit het Hallo-script in Hallo verwijzing sectie van dit document.</span><span class="sxs-lookup"><span data-stu-id="f06a7-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="f06a7-182">Hallo nul vierkante haken, [0], vertegenwoordigt Hallo eerste VM in Hallo-matrix van virtuele machines, voor Hallo voorbeeld script toowork zonder aanpassingen, eerste VM (VM 0) moet Hallo Hallo firewall):</span><span class="sxs-lookup"><span data-stu-id="f06a7-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="f06a7-183">Get-AzureVM-naam $VMName [0] - ServiceName $ServiceName [0] | \`</span><span class="sxs-lookup"><span data-stu-id="f06a7-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="f06a7-184">Netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="f06a7-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="f06a7-185">In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met een enkele regel.</span><span class="sxs-lookup"><span data-stu-id="f06a7-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="f06a7-186">Deze groep wordt vervolgens gebonden alleen toohello Frontend en Backend subnetten (geen hello SecNet).</span><span class="sxs-lookup"><span data-stu-id="f06a7-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="f06a7-187">Declaratief wordt Hallo-regel samengesteld:</span><span class="sxs-lookup"><span data-stu-id="f06a7-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="f06a7-188">Verkeer (alle poorten) van Hallo Internet toohello hele VNet (alle subnetten) is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="f06a7-189">Hoewel het nsg's in dit voorbeeld worden gebruikt, worden de belangrijkste doel is als een laag secundaire beveiliging tegen handmatige onjuiste configuratie.</span><span class="sxs-lookup"><span data-stu-id="f06a7-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="f06a7-190">We willen tooblock alle binnenkomend verkeer van Hallo internet tooeither Hallo Frontend of back-end-subnetten, verkeer mag alleen door Hallo SecNet subnet toohello firewall stromen (en vervolgens van toepassing op toohello front-end of back-end subnetten).</span><span class="sxs-lookup"><span data-stu-id="f06a7-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="f06a7-191">Bovendien met Hallo UDR regels aanwezig is, zou verkeer om het in Hallo front-end of back-end subnetten worden omgeleid uit toohello firewall (Bedankt tooUDR).</span><span class="sxs-lookup"><span data-stu-id="f06a7-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="f06a7-192">Hallo firewall zou dit zien als een asymmetrische stroom en uitgaand verkeer hello wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="f06a7-193">Dus zijn er drie lagen beveiliging beschermen Hallo Frontend en Backend subnetten; 1) er is geen open eindpunten op Hallo FrontEnd001 en BackEnd001 cloudservices, 2) nsg's weigeren verkeer vanaf Internet, 3) Hallo firewall neer te zetten asymmetrische verkeer Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="f06a7-194">Een interessant punt met betrekking tot Hallo Netwerkbeveiligingsgroep in dit voorbeeld is dat deze slechts één regel, die bevat hieronder worden weergegeven die toodeny internet verkeer toohello gehele virtuele netwerk waaronder Hallo beveiliging subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="f06a7-195">Echter, aangezien Hallo NSG alleen wordt gekoppeld toohello Frontend en Backend subnetten, Hallo regel is niet verwerkt op het verkeer inkomend toohello beveiliging subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="f06a7-196">Als gevolg hiervan Hoewel Hallo NSG regel geen adres Internet verkeer tooany op Hallo VNet, staat omdat NSG nooit is Hallo toohello beveiliging subnet gebonden, stromen verkeer toohello beveiliging subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="f06a7-197">Firewallregels</span><span class="sxs-lookup"><span data-stu-id="f06a7-197">Firewall Rules</span></span>
<span data-ttu-id="f06a7-198">Regels voor doorsturen moet toobe gemaakt op Hallo-firewall.</span><span class="sxs-lookup"><span data-stu-id="f06a7-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="f06a7-199">Omdat Hallo-firewall geblokkeerd of doorsturen van alle binnenkomende, uitgaande en intra-VNet-verkeer is worden veel firewallregels vereist.</span><span class="sxs-lookup"><span data-stu-id="f06a7-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="f06a7-200">Alle binnenkomend verkeer bereikt ook Hallo beveiligingsservice openbaar IP-adres (op verschillende poorten) toobe verwerkt door Hallo firewall.</span><span class="sxs-lookup"><span data-stu-id="f06a7-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="f06a7-201">Een aanbevolen procedure is toodiagram Hallo logische stromen voordat u Hallo subnetten en firewall-regels tooavoid dubbel later instelt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="f06a7-202">Hallo is volgende afbeelding een logische weergave van de firewallregels Hallo voor dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f06a7-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="f06a7-203">![Logische weergave van Hallo Firewall-regels][2]</span><span class="sxs-lookup"><span data-stu-id="f06a7-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="f06a7-204">Op basis van Hallo die virtueel netwerkapparaat gebruikt, variëren Hallo beheerpoorten.</span><span class="sxs-lookup"><span data-stu-id="f06a7-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="f06a7-205">In dit voorbeeld wordt verwezen naar een Barracuda NextGen Firewall gebruikt die poort 22, 801 en 807.</span><span class="sxs-lookup"><span data-stu-id="f06a7-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="f06a7-206">Raadpleeg Hallo toestel leverancier documentatie toofind Hallo exacte poorten die worden gebruikt voor het beheer van Hallo-apparaat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="f06a7-207">Beschrijving van de logische regel</span><span class="sxs-lookup"><span data-stu-id="f06a7-207">Logical Rule Description</span></span>
<span data-ttu-id="f06a7-208">In Hallo logisch diagram bovenstaande Hallo beveiliging subnet niet weergegeven omdat Hallo firewall Hallo enige resource in dat subnet is, en dit diagram Hallo firewallregels en hoe ze logisch toestaan of verkeersstromen en niet Hallo werkelijke gerouteerde pad weigeren wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="f06a7-209">Ook Hallo externe poorten geselecteerd voor Hallo RDP-verkeer hoger varieerde poorten (8014 – 8026) zijn en zijn geselecteerde toosomewhat zijn afgestemd op Hallo van laatste twee octetten van het lokale IP-adres voor een eenvoudiger leesbaarheid Hallo (bijvoorbeeld 10.0.1.4-adres van de lokale server is gekoppeld externe poort 8014), maar een hogere poorten voor niet-conflicterende kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="f06a7-210">Bijvoorbeeld, moeten we 7 typen regels, deze regeltypen worden als volgt beschreven:</span><span class="sxs-lookup"><span data-stu-id="f06a7-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="f06a7-211">Externe regels (voor inkomend verkeer):</span><span class="sxs-lookup"><span data-stu-id="f06a7-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="f06a7-212">Firewallregel voor beheer: Met deze regel omleidings-App kunt verkeer toopass toohello beheerpoorten van virtueel netwerkapparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="f06a7-213">RDP-regels (voor elke WindowsServer): deze vier regels (één voor elke server) wordt toestaan van beheer van Hallo afzonderlijke servers via RDP.</span><span class="sxs-lookup"><span data-stu-id="f06a7-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="f06a7-214">Dit kan ook worden gebundeld in één regel, afhankelijk van de mogelijkheden Hallo Hallo virtueel netwerkapparaat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="f06a7-215">Verkeersregels voor toepassing: Er zijn twee regels voor het netwerkverkeer van toepassing hello eerst voor Hallo-front-end-webverkeer en Hallo tweede voor verkeer van de back-end hello (bijvoorbeeld web server toodata laag).</span><span class="sxs-lookup"><span data-stu-id="f06a7-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="f06a7-216">Hallo-configuratie van deze regels, is afhankelijk van Hallo netwerkarchitectuur (waar uw servers worden geplaatst) en verkeersstromen (welke richting Hallo-verkeersstromen en welke poorten worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="f06a7-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="f06a7-217">de eerste regel Hallo kunt Hallo werkelijke toepassing verkeer tooreach Hallo-toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="f06a7-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="f06a7-218">Hallo andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services tooaccess Hallo toepassing(en) toestaan.</span><span class="sxs-lookup"><span data-stu-id="f06a7-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="f06a7-219">In dit voorbeeld is er één webserver op poort 80, dus één firewallregel toepassing binnenkomend verkeer toohello extern IP-adres, toohello web servers interne IP-adres worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="f06a7-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="f06a7-220">Hallo omgeleid verkeer sessie zou worden NAT gehad toohello interne serverfout.</span><span class="sxs-lookup"><span data-stu-id="f06a7-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="f06a7-221">tweede regel voor het netwerkverkeer van toepassing is Hallo Hallo back-end regel tooallow Hallo webserver tootalk toohello AppVM01 server (maar niet AppVM02) via een willekeurige poort.</span><span class="sxs-lookup"><span data-stu-id="f06a7-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="f06a7-222">Interne regels (voor intra-VNet-verkeer)</span><span class="sxs-lookup"><span data-stu-id="f06a7-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="f06a7-223">Regel voor uitgaande tooInternet: met deze regel kan verkeer van een netwerk toopass toohello geselecteerd netwerken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="f06a7-224">Deze regel is meestal een standaardregel al op Hallo firewall, maar in een uitgeschakelde status.</span><span class="sxs-lookup"><span data-stu-id="f06a7-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="f06a7-225">Deze regel moet worden ingeschakeld voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="f06a7-226">DNS-regel: Met deze regel kunnen alleen DNS (poort 53)-verkeer toopass toohello DNS-server.</span><span class="sxs-lookup"><span data-stu-id="f06a7-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="f06a7-227">Voor deze omgeving die Hallo Frontend toohello back-end meeste verkeer wordt geblokkeerd, kan deze regel specifiek DNS van een lokale subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="f06a7-228">Subnet tooSubnet regel: deze regel is tooallow een willekeurige server op Hallo achterkant subnet tooconnect tooany server op Hallo front-end-subnet beëindigen (maar niet Hallo omgekeerde).</span><span class="sxs-lookup"><span data-stu-id="f06a7-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="f06a7-229">Foutveilige regel (voor verkeer dat niet voldoet aan alle bovenstaande Hallo):</span><span class="sxs-lookup"><span data-stu-id="f06a7-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="f06a7-230">Alle Verkeersregel voor weigeren: Dit moet altijd de laatste regel hello (in termen van prioriteit), en als zodanig als een van de verkeersstromen mislukt toomatch van Hallo voorafgaand aan de regels die het door deze regel wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="f06a7-231">Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig.</span><span class="sxs-lookup"><span data-stu-id="f06a7-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="f06a7-232">Een willekeurige poort is toegestaan voor dit voorbeeld eenvoudig op Hallo tweede toepassing verkeersregel, in een echte scenario Hallo meest specifiek poort en bereiken gebruikte tooreduce Hallo kwetsbaarheid voor aanvallen van deze regel moeten worden.</span><span class="sxs-lookup"><span data-stu-id="f06a7-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="f06a7-233">Zodra alle Hallo hierboven regels zijn gemaakt, is het belangrijk tooreview Hallo prioriteit van elke regel tooensure-verkeer wordt toegestaan of geweigerd desgewenst.</span><span class="sxs-lookup"><span data-stu-id="f06a7-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="f06a7-234">In dit voorbeeld zijn Hallo regels in volgorde van prioriteit.</span><span class="sxs-lookup"><span data-stu-id="f06a7-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="f06a7-235">Het is gemakkelijk toobe Hallo firewall vanwege toomis besteld regels vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="f06a7-236">Zorg ervoor Hallo beheer voor Hallo firewall zelf is altijd Hallo absolute hoogste prioriteit regel minimaal.</span><span class="sxs-lookup"><span data-stu-id="f06a7-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="f06a7-237">Regel voor vereisten</span><span class="sxs-lookup"><span data-stu-id="f06a7-237">Rule Prerequisites</span></span>
<span data-ttu-id="f06a7-238">Een vereiste voor Hallo virtuele Machine actief Hallo firewall openbare eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="f06a7-239">Voor Hallo firewall tooprocess verkeer moet de juiste openbare eindpunten Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="f06a7-240">Er zijn drie typen verkeer in dit voorbeeld; 1) management verkeer toocontrol Hallo firewall en firewall-regels, 2) de RDP-verkeer toocontrol Hallo windows-servers en toepassing 3)-verkeer.</span><span class="sxs-lookup"><span data-stu-id="f06a7-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="f06a7-241">Dit zijn drie kolommen van de verkeerstypen in het bovenste Hallo Hallo helft van de logische weergave van de firewallregels Hallo hierboven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06a7-242">Een sleutel takeway hier is tooremember die **alle** verkeer via de firewall hello wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="f06a7-243">In dat geval tooremote bureaublad toohello IIS01 server, zelfs als het in Hallo Front-End-Cloudservice en op Hallo front-end-subnet, tooaccess deze server moeten we tooRDP toohello firewall op poort 8014 en laat Hallo firewall tooroute Hallo RDP aanvraag intern toohello IIS01 RDP-poort.</span><span class="sxs-lookup"><span data-stu-id="f06a7-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="f06a7-244">Hello Azure portal 'Connect' knop werkt niet omdat er geen directe RDP pad tooIIS01 (zo ver mogelijk Hallo portal kunt zien).</span><span class="sxs-lookup"><span data-stu-id="f06a7-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="f06a7-245">Dit betekent dat alle verbindingen op Hallo internet moet worden toohello Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx (verwijzing hello hierboven diagram voor Hallo toewijzing van de externe poort en intern IP-adres en poort).</span><span class="sxs-lookup"><span data-stu-id="f06a7-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="f06a7-246">Een eindpunt kan worden geopend op Hallo-tijd van het maken van VM- of build boekt als is gedaan in Hallo voorbeeldscript en hieronder wordt weergegeven in dit codefragment (Opmerking; een item die begint met een dollarteken (bijvoorbeeld: $VMName[$i]) is een door de gebruiker gedefinieerde variabele uit het script in Hallo referen Hallo CE-sectie van dit document.</span><span class="sxs-lookup"><span data-stu-id="f06a7-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="f06a7-247">Hallo '$i' vierkante haken, [$i] Hallo matrix aantal vertegenwoordigt een specifieke virtuele machine in een matrix van virtuele machines):</span><span class="sxs-lookup"><span data-stu-id="f06a7-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="f06a7-248">Hoewel het niet duidelijk hier weergegeven vanwege toohello gebruik van variabelen, maar eindpunten zijn **alleen** geopend op Hallo Security Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="f06a7-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="f06a7-249">Dit is dat alle binnenkomend verkeer wordt verwerkt tooensure (gerouteerd, NAT waren, verloren) door Hallo firewall.</span><span class="sxs-lookup"><span data-stu-id="f06a7-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="f06a7-250">Een Beheerclient toobe geïnstalleerd op een PC toomanage Hallo firewall nodig hebt en Hallo configuraties nodig maken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="f06a7-251">Zie de leverancier van de documentatie van uw firewall (of andere NVA) Hallo over hoe toomanage apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="f06a7-252">Hallo rest van deze sectie en de volgende sectie hello, Firewall-regels maken, bevat een beschrijving van Hallo configuratie van Hallo firewall zelf, via Hallo leveranciers management-client (d.w.z. niet hello Azure-portal of PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f06a7-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="f06a7-253">Instructies voor het downloaden van de client en verbindende toohello Barracuda gebruikt in dit voorbeeld vindt u hier: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="f06a7-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="f06a7-254">Zodra u aangemeld bent op Hallo firewall, maar voordat u firewallregels maken, zijn er twee vereiste objectklassen waardoor maken Hallo regels gemakkelijker; Netwerk- en Service-objecten.</span><span class="sxs-lookup"><span data-stu-id="f06a7-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="f06a7-255">In dit voorbeeld moet drie benoemde netwerkobjecten gedefinieerd (een voor Hallo Frontend subnet en Hallo-subnet voor back-end, ook een netwerkobject voor Hallo IP-adres van Hallo DNS-server).</span><span class="sxs-lookup"><span data-stu-id="f06a7-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="f06a7-256">toocreate een benoemde netwerk. vanaf Hallo Barracuda NG Admin client dashboard, tabblad toohello-configuratie te navigeren, in Hallo operationele configuratiesectie Ruleset, vervolgens klikt u op "Netwerken" onder Hallo Firewallobjecten menu, klik op Nieuw in Hallo bewerken netwerken menu.</span><span class="sxs-lookup"><span data-stu-id="f06a7-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="f06a7-257">Hallo-netwerkobject kan nu worden gemaakt, door toe te voegen Hallo naam en het Hallo-voorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="f06a7-258">![Een Object FrontEnd-netwerk maken][3]</span><span class="sxs-lookup"><span data-stu-id="f06a7-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="f06a7-259">Hiermee maakt u een benoemde netwerk voor Hallo FrontEnd subnet, een vergelijkbaar object Hallo subnet BackEnd ook moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="f06a7-260">Hallo-subnetten kunnen nu gemakkelijker verwezen met de naam in de firewallregels Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="f06a7-261">Hallo voor DNS-Server-Object:</span><span class="sxs-lookup"><span data-stu-id="f06a7-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="f06a7-262">![Een DNS-Server-Object maken][4]</span><span class="sxs-lookup"><span data-stu-id="f06a7-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="f06a7-263">Deze één verwijzing naar een IP-adres wordt gebruikt in een DNS-regel verderop in document Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="f06a7-264">Hallo tweede vereiste objecten zijn Services objecten.</span><span class="sxs-lookup"><span data-stu-id="f06a7-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="f06a7-265">Deze vertegenwoordigt Hallo RDP verbindingspoorten voor elke server.</span><span class="sxs-lookup"><span data-stu-id="f06a7-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="f06a7-266">Omdat bestaande RDP-serviceobject Hallo gebonden toohello standaard RDP-poort, kunnen 3389, nieuwe Services worden gemaakt tooallow verkeer van externe Hallo-poorten (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="f06a7-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="f06a7-267">de nieuwe poorten Hallo kunnen ook worden toegevoegd toohello bestaande RDP-service, maar voor een eenvoudige demonstratie een afzonderlijke regel voor elke server kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="f06a7-268">toocreate een nieuwe RDP-regel voor een server. tabblad van de configuratie toohello hello Barracuda NG Admin client dashboard vanaf navigeren, Hallo operationele configuratie sectie Ruleset, klikt u op en klik op 'Services' onder Hallo Firewallobjecten menu, schuif omlaag Hallo lijst met services en selecteer Hallo 'RDP' service.</span><span class="sxs-lookup"><span data-stu-id="f06a7-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="f06a7-269">Met de rechtermuisknop op en selecteert u kopiëren, en vervolgens met de rechtermuisknop op en selecteer plakken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="f06a7-270">Er is nu een RDP-Copy1-Object dat kan worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="f06a7-271">Met de rechtermuisknop op de RDP-Copy1 en selecteer bewerken, Hallo bewerken serviceobject pop-up venster wordt als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f06a7-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="f06a7-272">![Kopie van de standaardregel voor RDP][5]</span><span class="sxs-lookup"><span data-stu-id="f06a7-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="f06a7-273">Hallo-waarden kunnen vervolgens worden bewerkte toorepresent Hallo RDP-service voor een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="f06a7-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="f06a7-274">RDP-regel moet voor AppVM01 Hallo hierboven standaard gewijzigde tooreflect een nieuwe Service-naam, beschrijving, en externe RDP-poort die worden gebruikt in Hallo afbeelding 8 diagram (Opmerking: Hallo poorten zijn gewijzigd van Hallo RDP 3389 toohello externe poort die wordt gebruikt voor deze standaardwaarde specifieke server, in geval van AppVM01 Hallo externe poort Hallo is 8025) hello gewijzigde service worden hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f06a7-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="f06a7-275">![AppVM01 regel][6]</span><span class="sxs-lookup"><span data-stu-id="f06a7-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="f06a7-276">Dit proces moet worden herhaald toocreate RDP-Services voor Hallo resterende servers. AppVM02, DNS01 en IIS01.</span><span class="sxs-lookup"><span data-stu-id="f06a7-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="f06a7-277">Hallo maken van deze Services maakt Hallo regel maken eenvoudiger en duidelijker in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="f06a7-278">Een RDP-service voor Hallo Firewall is niet nodig om twee redenen; 1) de eerste Hallo firewall VM is een installatiekopie op basis van Linux zodat SSH wordt gebruikt op poort 22 voor VM-management in plaats van RDP en 2)-poort 22 en twee andere poorten zijn toegestaan in Hallo eerste management regel hieronder tooallow voor connectiviteit van het beheer beschreven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="f06a7-279">Firewall-regels maken</span><span class="sxs-lookup"><span data-stu-id="f06a7-279">Firewall Rules Creation</span></span>
<span data-ttu-id="f06a7-280">Er zijn drie soorten firewallregels die in dit voorbeeld gebruikt, alle hebben verschillende pictogrammen:</span><span class="sxs-lookup"><span data-stu-id="f06a7-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="f06a7-281">Hallo toepassing omleiden regel: ![toepassing omleidings-pictogram][7]</span><span class="sxs-lookup"><span data-stu-id="f06a7-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="f06a7-282">Hallo bestemming NAT-regel: ![bestemming NAT-pictogram][8]</span><span class="sxs-lookup"><span data-stu-id="f06a7-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="f06a7-283">Hallo Pass regel: ![pictogram doorgeven][9]</span><span class="sxs-lookup"><span data-stu-id="f06a7-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="f06a7-284">U vindt meer informatie over deze regels op Hallo Barracuda-website.</span><span class="sxs-lookup"><span data-stu-id="f06a7-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="f06a7-285">toocreate Hallo regels (of Controleer of de bestaande standaardregels), vanaf Hallo Barracuda NG Admin client dashboard, navigeer toohello configuratie tabblad, in Hallo operationele configuratie sectie Ruleset klikt u op.</span><span class="sxs-lookup"><span data-stu-id="f06a7-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="f06a7-286">Een raster aangeroepen, wordt 'Main regels' hello bestaande actieve en gedeactiveerd regels op deze firewall weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="f06a7-287">Hallo rechterbovenhoek van dit raster is een klein, groene '+' knop, klikt u op deze toocreate een nieuwe regel (Opmerking: uw firewall mogelijk 'vergrendeld' om wijzigingen, als er een knop 'Vergrendelen' gemarkeerd en kan niet toocreate zijn of regels bewerken, klikt u op deze knop te regel se 'ontgrendelen' Hallo t en bewerken).</span><span class="sxs-lookup"><span data-stu-id="f06a7-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="f06a7-288">Als u een bestaande regel tooedit wilt, selecteert u deze regel, met de rechtermuisknop op en selecteer regel bewerken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="f06a7-289">Zodra uw regels zijn gemaakt en/of gewijzigd, moeten ze toohello firewall gepusht en vervolgens geactiveerd, als dit niet gebeurt Hallo regel wijzigingen pas van kracht.</span><span class="sxs-lookup"><span data-stu-id="f06a7-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="f06a7-290">Hallo push en activering proces wordt hieronder Hallo details regelbeschrijvingen beschreven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="f06a7-291">Hallo-details van elke regel vereist toocomplete in dit voorbeeld als volgt worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="f06a7-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="f06a7-292">**Firewall-regel Management**: deze App omleiden regel staat toe dat verkeer toopass toohello beheerpoorten van Hallo virtueel netwerkapparaat, in dit voorbeeld een Barracuda NextGen Firewall.</span><span class="sxs-lookup"><span data-stu-id="f06a7-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="f06a7-293">Hallo management poorten zijn 801, 807 en eventueel 22.</span><span class="sxs-lookup"><span data-stu-id="f06a7-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="f06a7-294">Hallo interne en externe poorten zijn Hallo dezelfde (d.w.z. geen poortvertaling).</span><span class="sxs-lookup"><span data-stu-id="f06a7-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="f06a7-295">Deze regel, SETUP-MGMT-toegang, is een standaardregel en (in Barracuda NextGen Firewall versie 6.1) standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="f06a7-296">![Firewallregel Management][10]</span><span class="sxs-lookup"><span data-stu-id="f06a7-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="f06a7-297">Hello bron-adresruimte in deze regel is, als hello management IP-adresbereiken bekend zijn, waardoor dit bereik Hallo aanval surface toohello beheerpoorten ook sneller.</span><span class="sxs-lookup"><span data-stu-id="f06a7-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="f06a7-298">**Regels voor RDP**: deze bestemming NAT-regels kunnen beheer van Hallo afzonderlijke servers via RDP.</span><span class="sxs-lookup"><span data-stu-id="f06a7-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="f06a7-299">Er zijn vier kritieke velden nodig toocreate met deze regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="f06a7-300">Bron: tooallow RDP vanaf elke locatie, Hallo verwijzing 'Any' in veld Hallo-bron gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="f06a7-301">Service – juiste serviceobject eerder hebt gemaakt, in dit geval 'AppVM01 RDP' hello gebruiken, externe poorten Hallo omleiden toohello servers lokale IP-adres en tooport 3386 (Hallo standaard RDP-poort).</span><span class="sxs-lookup"><span data-stu-id="f06a7-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="f06a7-302">Deze specifieke regel is voor RDP toegang tooAppVM01.</span><span class="sxs-lookup"><span data-stu-id="f06a7-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="f06a7-303">Doel – moet Hallo *lokale poort op Hallo firewall*, 'DCHP 1 lokale IP-' of eth0 als statische IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="f06a7-304">Hallo rangtelwoord (eth0, eth1, enzovoort) is mogelijk anders als uw netwerkapparaat meerdere lokale interfaces heeft.</span><span class="sxs-lookup"><span data-stu-id="f06a7-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="f06a7-305">Dit is de poort Hallo Hallo firewall verstuurt uit (mogelijk dezelfde als de poort ontvangen Hallo Hallo), werkelijke gerouteerde bestemming Hallo Hallo doellijst veld is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="f06a7-306">Omleiding – dit gedeelte wordt uitgelegd Hallo virtueel apparaat waar tooultimately dit verkeer worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="f06a7-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="f06a7-307">de eenvoudigste omleiding Hallo is tooplace Hallo IP- en poort (optioneel) in Hallo doellijst veld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="f06a7-308">Als er geen poort gebruikte Hallo doelpoort op Hallo binnenkomende aanvraag (ie geen vertaling) gebruikt als een poort is aangewezen Hallo poort worden ook NAT zou samen met de Hallo IP adres.</span><span class="sxs-lookup"><span data-stu-id="f06a7-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="f06a7-309">![RDP-firewallregel][11]</span><span class="sxs-lookup"><span data-stu-id="f06a7-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="f06a7-310">Een totaal van vier RDP-regels nodig toobe gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f06a7-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="f06a7-311">Regelnaam</span><span class="sxs-lookup"><span data-stu-id="f06a7-311">Rule Name</span></span> | <span data-ttu-id="f06a7-312">Server</span><span class="sxs-lookup"><span data-stu-id="f06a7-312">Server</span></span> | <span data-ttu-id="f06a7-313">Service</span><span class="sxs-lookup"><span data-stu-id="f06a7-313">Service</span></span> | <span data-ttu-id="f06a7-314">Lijst met doelservers</span><span class="sxs-lookup"><span data-stu-id="f06a7-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="f06a7-315">RDP-naar-IIS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-315">RDP-to-IIS01</span></span> |<span data-ttu-id="f06a7-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-316">IIS01</span></span> |<span data-ttu-id="f06a7-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="f06a7-317">IIS01 RDP</span></span> |<span data-ttu-id="f06a7-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="f06a7-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="f06a7-319">RDP-naar-DNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-319">RDP-to-DNS01</span></span> |<span data-ttu-id="f06a7-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-320">DNS01</span></span> |<span data-ttu-id="f06a7-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="f06a7-321">DNS01 RDP</span></span> |<span data-ttu-id="f06a7-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="f06a7-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="f06a7-323">RDP-naar-AppVM01</span><span class="sxs-lookup"><span data-stu-id="f06a7-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="f06a7-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="f06a7-324">AppVM01</span></span> |<span data-ttu-id="f06a7-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="f06a7-325">AppVM01 RDP</span></span> |<span data-ttu-id="f06a7-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="f06a7-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="f06a7-327">RDP-naar-AppVM02</span><span class="sxs-lookup"><span data-stu-id="f06a7-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="f06a7-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="f06a7-328">AppVM02</span></span> |<span data-ttu-id="f06a7-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="f06a7-329">AppVm02 RDP</span></span> |<span data-ttu-id="f06a7-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="f06a7-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="f06a7-331">Beperking Hallo bereik van Hallo bron en de velden van de Service beperkt Hallo kwetsbaarheid voor aanvallen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="f06a7-332">Hallo meest beperkt bereik die zorgen de functionaliteit dat ervoor moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="f06a7-333">**Toepassing verkeersregels**: Er zijn twee regels voor het netwerkverkeer van toepassing, Hallo eerst voor Hallo-front-end-webverkeer en Hallo tweede voor verkeer van de back-end hello (bijvoorbeeld web server toodata laag).</span><span class="sxs-lookup"><span data-stu-id="f06a7-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="f06a7-334">Deze regels, is afhankelijk van Hallo netwerkarchitectuur (waar uw servers worden geplaatst) en verkeersstromen (welke richting Hallo-verkeersstromen en welke poorten worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="f06a7-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="f06a7-335">Eerst besproken is Hallo-front-end-regel voor internetverkeer:</span><span class="sxs-lookup"><span data-stu-id="f06a7-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="f06a7-336">![Web-firewallregel][12]</span><span class="sxs-lookup"><span data-stu-id="f06a7-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="f06a7-337">Deze bestemming NAT-regel staat toe Hallo werkelijke verkeer tooreach Hallo toepassing toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="f06a7-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="f06a7-338">Hallo andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services tooaccess Hallo toepassing(en) toestaan.</span><span class="sxs-lookup"><span data-stu-id="f06a7-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="f06a7-339">In dit voorbeeld is er één webserver op poort 80, dus één firewallregel toepassing hello binnenkomend verkeer toohello extern IP-adres, toohello web servers interne IP-adres worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="f06a7-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="f06a7-340">**Opmerking**: dat er is geen poort toegewezen in Hallo doellijst veld, dus hello binnenkomende poort 80 (of 443 voor Hallo Service geselecteerd) wordt gebruikt in Hallo omleiding van Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="f06a7-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="f06a7-341">Als de webserver Hallo luistert op een andere poort, bijvoorbeeld poort 8080, Hallo doellijst veld bijgewerkte too10.0.1.4:8080 tooallow voor Hallo poort ook omleiding kan worden.</span><span class="sxs-lookup"><span data-stu-id="f06a7-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="f06a7-342">Hallo volgende Verkeersregel van toepassing is Hallo back-end regel tooallow Hallo webserver tootalk toohello AppVM01 server (maar niet AppVM02) via elke service:</span><span class="sxs-lookup"><span data-stu-id="f06a7-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="f06a7-343">![AppVM01 firewallregel][13]</span><span class="sxs-lookup"><span data-stu-id="f06a7-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="f06a7-344">Deze regel op te geven kunnen IIS-server op Hallo Frontend subnet tooreach hello AppVM01 (IP-adres 10.0.2.5) op een willekeurige poort Protocol tooaccess gegevens die nodig is voor de webtoepassing hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="f06a7-345">In deze schermafdruk een '\<expliciete-dest\>' hello bestemming in Hallo bestemming veld toosignify 10.0.2.5 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="f06a7-346">Dit kan zijn expliciete zoals wordt weergegeven of een met de naam netwerkobject (net als bij Hallo-vereisten voor Hallo DNS-server).</span><span class="sxs-lookup"><span data-stu-id="f06a7-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="f06a7-347">Dit is van de beheerder van de firewall Hallo toohello toowhich methode wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="f06a7-348">tooadd 10.0.2.5 als een Explict Desitnation, dubbelklik op Hallo eerste lege rij onder \<expliciete-dest\> en het Hallo-mailadres invoeren in het Hallo-venster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="f06a7-349">Met deze regel geeft geen NAT is nodig omdat dit is interne verkeer Hallo verbindingsmethode te kan worden ingesteld 'No snat omzetten'.</span><span class="sxs-lookup"><span data-stu-id="f06a7-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="f06a7-350">**Opmerking**: Hallo Bronnetwerk in deze regel wordt een resource in het subnet FrontEnd Hallo als er wordt niet meer dan een of meer specifieke toothose exacte IP-adressen in plaats van is gemaakt toobe een bekende specifiek aantal webservers, een resource kan worden netwerkobject Hallo gehele Frontend-subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="f06a7-351">Deze regel maakt gebruik van Hallo service '' toomake Hallo voorbeeld toepassing eenvoudiger toosetup en gebruiken, ook hierdoor ICMPv4 (ping) in een enkele regel.</span><span class="sxs-lookup"><span data-stu-id="f06a7-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="f06a7-352">Dit is echter niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="f06a7-353">Hallo-poorten en protocollen ('Services') moet versmalling toohello minimale mogelijk waarmee de toepassing opnieuw tooreduce Hallo kwetsbaarheid voor aanvallen via deze grens.</span><span class="sxs-lookup"><span data-stu-id="f06a7-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="f06a7-354">Hoewel met deze regel een verwijzing naar een expliciete-dest wordt gebruikt bevat, moet een consistente werkwijze in de firewallconfiguratie hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="f06a7-355">Het verdient aanbeveling dat met de naam netwerkobject hello worden gebruikt in de gehele voor gemakkelijker leesbaarheid en ondersteuningsmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f06a7-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="f06a7-356">Hallo expliciete-dest gebruikte hier alleen tooshow is een methode alternatieve verwijzing en wordt over het algemeen niet aanbevolen (met name voor complexe configuraties).</span><span class="sxs-lookup"><span data-stu-id="f06a7-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="f06a7-357">**Regel voor uitgaande tooInternet**: doorgeven voor deze regel wordt verkeer van elke bron netwerk toopass toohello geselecteerd doelnetwerken toestaan.</span><span class="sxs-lookup"><span data-stu-id="f06a7-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="f06a7-358">Deze regel is een standaardregel meestal al op Hallo Barracuda NextGen firewall, maar is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="f06a7-359">Met de rechtermuisknop op deze regel kunt Hallo activeren regel opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f06a7-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="f06a7-360">Hallo regel hier weergegeven is gewijzigde tooadd Hallo twee lokale subnetten die als verwijzingen in de sectie voor vereisten Hallo van dit document toohello bronkenmerk van deze regel zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f06a7-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="f06a7-361">![Uitgaande firewallregel][14]</span><span class="sxs-lookup"><span data-stu-id="f06a7-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="f06a7-362">**Een DNS-regel**: deze doorgeven regel staat toe dat alleen DNS (poort 53)-verkeer toopass toohello DNS-server.</span><span class="sxs-lookup"><span data-stu-id="f06a7-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="f06a7-363">Deze regel kunnen specifiek DNS voor deze omgeving die de meeste verkeer van Hallo FrontEnd toohello back-end is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="f06a7-364">![DNS-firewallregel][15]</span><span class="sxs-lookup"><span data-stu-id="f06a7-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="f06a7-365">**Opmerking**: In dit scherm schermopname Hallo verbindingsmethode is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="f06a7-366">Omdat deze regel is voor interne IP-toointernal IP-adres verkeer, geen NATing is vereist, wordt deze Hallo verbindingsmethode ingesteld te 'No snat omzetten' voor deze regel op te geven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="f06a7-367">**Subnet tooSubnet regel**: doorgeven voor deze regel is een standaardregel waarmee is geactiveerd en gewijzigde tooallow elke server op Hallo terug eindigt subnet tooconnect tooany server op Hallo front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="f06a7-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="f06a7-368">Deze regel is alle interne verkeer dus Hallo verbindingsmethode tooNo snat omzetten kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="f06a7-369">![Intra-VNet-firewallregel][16]</span><span class="sxs-lookup"><span data-stu-id="f06a7-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="f06a7-370">**Opmerking**: Hallo bidirectionele selectievakje niet is ingeschakeld (noch is ingeschakeld in de meeste regels), dit is van belang voor deze regel maakt deze regel 'eenrichtings', een verbinding kan worden gestart vanaf Hallo back-end subnet toohello front-end-netwerk maar Hallo niet omkeren.</span><span class="sxs-lookup"><span data-stu-id="f06a7-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="f06a7-371">Als dit selectievakje is ingeschakeld, zou deze regel in twee richtingen verkeer, wat van onze logisch diagram niet inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="f06a7-372">**Alle Verkeersregel voor weigeren**: dit moet altijd de laatste regel hello (in termen van prioriteit) en als zodanig als een verkeersstromen mislukt toomatch van Hallo regels voorafgaand aan deze verwijderd door deze regel.</span><span class="sxs-lookup"><span data-stu-id="f06a7-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="f06a7-373">Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig.</span><span class="sxs-lookup"><span data-stu-id="f06a7-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="f06a7-374">![Regel voor weigeren van Firewall][17]</span><span class="sxs-lookup"><span data-stu-id="f06a7-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06a7-375">Zodra alle Hallo hierboven regels zijn gemaakt, is het belangrijk tooreview Hallo prioriteit van elke regel tooensure-verkeer wordt toegestaan of geweigerd desgewenst.</span><span class="sxs-lookup"><span data-stu-id="f06a7-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="f06a7-376">In dit voorbeeld hebben Hallo regels Hallo volgorde die in Hallo Main raster van regels in Hallo Barracuda Beheerclient doorsturen dienen te worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="f06a7-377">Activering van de regel</span><span class="sxs-lookup"><span data-stu-id="f06a7-377">Rule Activation</span></span>
<span data-ttu-id="f06a7-378">Met de Hallo ruleset gewijzigd toohello specificatie van Hallo logica diagram Hallo ruleset moet toohello firewall geüpload en wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="f06a7-379">![Activering van de firewall-regel][18]</span><span class="sxs-lookup"><span data-stu-id="f06a7-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="f06a7-380">In Hallo rechtsboven van Hallo Beheerclient zijn een cluster van knoppen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="f06a7-381">Hallo 'verzenden wijzigingen' knop toosend Hallo gewijzigd regels toohello firewall, klik op de knop 'Activeren' Hallo.</span><span class="sxs-lookup"><span data-stu-id="f06a7-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="f06a7-382">Deze versie van de omgeving voorbeeld is bij activering via Hallo Hallo firewall ruleSet voltooid.</span><span class="sxs-lookup"><span data-stu-id="f06a7-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="f06a7-383">Verkeer scenario 's</span><span class="sxs-lookup"><span data-stu-id="f06a7-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f06a7-384">Een sleutel takeway is tooremember die **alle** verkeer via de firewall hello wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="f06a7-385">In dat geval tooremote bureaublad toohello IIS01 server, zelfs als het in Hallo Front-End-Cloudservice en op Hallo front-end-subnet, tooaccess deze server moeten we tooRDP toohello firewall op poort 8014 en laat Hallo firewall tooroute Hallo RDP aanvraag intern toohello IIS01 RDP-poort.</span><span class="sxs-lookup"><span data-stu-id="f06a7-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="f06a7-386">Hello Azure portal 'Connect' knop werkt niet omdat er geen directe RDP pad tooIIS01 (zo ver mogelijk Hallo portal kunt zien).</span><span class="sxs-lookup"><span data-stu-id="f06a7-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="f06a7-387">Dit betekent dat alle verbindingen op Hallo internet toohello Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx moet worden.</span><span class="sxs-lookup"><span data-stu-id="f06a7-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="f06a7-388">Voor deze scenario's moet Hallo firewallregels volgende zijn voldaan:</span><span class="sxs-lookup"><span data-stu-id="f06a7-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="f06a7-389">Beheer van Firewall</span><span class="sxs-lookup"><span data-stu-id="f06a7-389">Firewall Management</span></span>
2. <span data-ttu-id="f06a7-390">RDP-tooIIS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="f06a7-391">RDP-tooDNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="f06a7-392">RDP-tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="f06a7-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="f06a7-393">RDP-tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="f06a7-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="f06a7-394">App-verkeer toohello Web</span><span class="sxs-lookup"><span data-stu-id="f06a7-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="f06a7-395">App-verkeer tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="f06a7-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="f06a7-396">Uitgaande toohello Internet</span><span class="sxs-lookup"><span data-stu-id="f06a7-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="f06a7-397">Frontend tooDNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="f06a7-398">Intra-subnetverkeer (alleen voor back-end toofront end)</span><span class="sxs-lookup"><span data-stu-id="f06a7-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="f06a7-399">Alles weigeren</span><span class="sxs-lookup"><span data-stu-id="f06a7-399">Deny All</span></span>

<span data-ttu-id="f06a7-400">Hallo werkelijke firewall ruleset heeft waarschijnlijk veel andere regels in een toevoeging toothese, Hallo regels op een bepaalde firewall hebben ook andere prioriteitsnummers dan Hallo toepassingsgroepen hier vermeld.</span><span class="sxs-lookup"><span data-stu-id="f06a7-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="f06a7-401">Deze lijst en de bijbehorende cijfers zijn tooprovide relevantie tussen alleen deze elf regels en de relatieve prioriteit Hallo onder deze.</span><span class="sxs-lookup"><span data-stu-id="f06a7-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="f06a7-402">Met andere woorden; Hallo 'RDP tooIIS01' kan op Hallo werkelijke firewall, regel getal 5, maar als deze onder Hallo 'Firewallbeheer' regel en boven Hallo 'RDP tooDNS01' regel die zou deze afgestemd op Hallo bedoeling van deze lijst is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="f06a7-403">Hallo lijst helpt ook bij Hallo onderstaande scenario's zodat beknopt alternatief bevat; bijvoorbeeld 'FW regel 9 (DNS)'.</span><span class="sxs-lookup"><span data-stu-id="f06a7-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="f06a7-404">Ook als beknopt alternatief bevat, Hallo vier regels voor RDP gezamenlijk worden aangeroepen, "hello RDP regels" wanneer Hallo verkeer scenario niet-verwante tooRDP is.</span><span class="sxs-lookup"><span data-stu-id="f06a7-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="f06a7-405">Ook intrekken dat Netwerkbeveiligingsgroepen in-place voor binnenkomend internetverkeer op Hallo Frontend en Backend subnetten zijn.</span><span class="sxs-lookup"><span data-stu-id="f06a7-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="f06a7-406">(Toegestaan) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="f06a7-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="f06a7-407">Internet aanvragen HTTP-gebruikerspagina van SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="f06a7-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f06a7-408">Cloud-service geeft verkeer via open eindpunten op poort 80 toofirewall interface op 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="f06a7-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="f06a7-409">Er is geen NSG toegewezen tooSecurity subnet, zodat het NSG-Systeemregels toofirewall verkeer toestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="f06a7-410">Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="f06a7-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="f06a7-411">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f06a7-412">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-413">FW regels (regels RDP), 2-5 niet toepassen, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f06a7-414">FW regel 6 (App: Web) is van toepassing, verkeer wordt toegestaan, firewall NAT's het too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="f06a7-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="f06a7-415">Hallo Frontend subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f06a7-416">NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door Hallo firewall, Hallo bronadres is dus nu Hallo firewall die zich op Hallo beveiliging subnet en zichtbaar zijn voor subnet Frontend voor Hallo NSG toobe "local" verkeer en is dus toegestaan), toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-417">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="f06a7-418">IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f06a7-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="f06a7-419">IIS01 probeert een FTP-sessie tooAppVM01 tooinitiates op subnet Backend</span><span class="sxs-lookup"><span data-stu-id="f06a7-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="f06a7-420">Hallo UDR route voor subnet Frontend maakt Hallo firewall Hallo volgende hop</span><span class="sxs-lookup"><span data-stu-id="f06a7-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="f06a7-421">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f06a7-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f06a7-422">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="f06a7-423">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-424">FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="f06a7-425">FW regel 6 (App: Web) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="f06a7-426">FW regel 7 (App: back-end) is van toepassing, verkeer is toegestaan, firewall stuurt verkeer too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="f06a7-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="f06a7-427">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f06a7-428">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-429">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="f06a7-430">AppVM01 hello aanvraag ontvangt en Hallo-sessie start en reageert</span><span class="sxs-lookup"><span data-stu-id="f06a7-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="f06a7-431">Hallo UDR route voor subnet Backend maakt Hallo firewall Hallo volgende hop</span><span class="sxs-lookup"><span data-stu-id="f06a7-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="f06a7-432">Omdat er geen uitgaande NSG-regels op Hallo antwoord Hallo van back-end-subnet is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="f06a7-433">Omdat dit verkeer op retourneert een vastgestelde sessie Hallo firewall wordt doorgegeven Hallo antwoord back toohello webserver (IIS01)</span><span class="sxs-lookup"><span data-stu-id="f06a7-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="f06a7-434">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f06a7-435">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-436">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="f06a7-437">Hallo IIS-server Hallo antwoord wordt ontvangen, Hallo transactie met AppVM01 en daarna voltooit gebouw Hallo HTTP-antwoord, deze HTTP-antwoord verzonden toohello aanvrager</span><span class="sxs-lookup"><span data-stu-id="f06a7-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="f06a7-438">Omdat er geen uitgaande NSG-regels op Hallo Frontend subnet Hallo antwoord is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="f06a7-439">HTTP-antwoord treffers Hallo firewall Hallo en omdat dit Hallo antwoord tooan tot stand gebracht NAT-sessie wordt geaccepteerd door de firewall Hallo</span><span class="sxs-lookup"><span data-stu-id="f06a7-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="f06a7-440">Hallo firewall stuurt vervolgens door Hallo antwoord back toohello Internet-gebruiker</span><span class="sxs-lookup"><span data-stu-id="f06a7-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="f06a7-441">Aangezien er geen uitgaande NSG-regels of UDR hops zijn op Hallo Frontend subnet antwoord Hallo is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="f06a7-442">(Toegestaan) Internet RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="f06a7-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="f06a7-443">RDP-sessie tooAppVM01 via SecSvc001.CloudApp.Net:8025, waarbij 8025 Hallo gebruiker toegewezen poortnummer voor de firewallregel voor 'RDP tooAppVM01' hello is serverbeheerder op internet-aanvragen</span><span class="sxs-lookup"><span data-stu-id="f06a7-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="f06a7-444">Hallo-cloudservice wordt doorgegeven verkeer via Hallo open eindpunten op poort 8025 toofirewall interface op 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="f06a7-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="f06a7-445">Er is geen NSG toegewezen tooSecurity subnet, zodat het NSG-Systeemregels toofirewall verkeer toestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="f06a7-446">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f06a7-447">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-448">FW regel 2 (RDP IIS) is niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f06a7-449">FW regel 3 (RDP DNS01) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f06a7-450">FW regel 4 (RDP AppVM01) is van toepassing, het verkeer wordt toegestaan, firewall NAT's het too10.0.2.5:3386 (RDP-poort op AppVM01)</span><span class="sxs-lookup"><span data-stu-id="f06a7-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="f06a7-451">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f06a7-452">NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door Hallo firewall, Hallo bronadres is dus nu Hallo firewall die zich op Hallo beveiliging subnet en zichtbaar zijn voor het subnet van de back-end Hallo NSG toobe "local" verkeer en is dus toegestaan), toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-453">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="f06a7-454">AppVM01 voor RDP-verkeer luistert en antwoordt</span><span class="sxs-lookup"><span data-stu-id="f06a7-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="f06a7-455">Standaardregels toepassen met geen uitgaande NSG-regels en terugkerend verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="f06a7-456">UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo</span><span class="sxs-lookup"><span data-stu-id="f06a7-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="f06a7-457">Omdat dit verkeer op retourneert een vastgestelde sessie Hallo firewall wordt doorgegeven Hallo antwoord back toohello internet-gebruiker</span><span class="sxs-lookup"><span data-stu-id="f06a7-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="f06a7-458">RDP-sessie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="f06a7-458">RDP session is enabled</span></span>
11. <span data-ttu-id="f06a7-459">AppVM01 gebruikersnaam wachtwoord gevraagd</span><span class="sxs-lookup"><span data-stu-id="f06a7-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="f06a7-460">(Toegestaan) Web Server DNS-lookup op DNS-server</span><span class="sxs-lookup"><span data-stu-id="f06a7-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f06a7-461">Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="f06a7-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="f06a7-462">Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="f06a7-463">UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo</span><span class="sxs-lookup"><span data-stu-id="f06a7-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="f06a7-464">Er is geen uitgaand NSG-regels zijn gebonden toohello Frontend subnet, is verkeer toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="f06a7-465">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f06a7-466">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-467">FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f06a7-468">FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f06a7-469">FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="f06a7-470">FW regel 9 (DNS) is van toepassing, verkeer is toegestaan, firewall stuurt verkeer too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="f06a7-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="f06a7-471">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f06a7-472">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-473">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="f06a7-474">DNS-server ontvangt Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="f06a7-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="f06a7-475">DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet</span><span class="sxs-lookup"><span data-stu-id="f06a7-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="f06a7-476">UDR routes uitgaand verkeer toohello firewall als de volgende hop Hallo</span><span class="sxs-lookup"><span data-stu-id="f06a7-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="f06a7-477">Er is geen uitgaand NSG-regels op subnet Backend, verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f06a7-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f06a7-478">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="f06a7-479">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-480">FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="f06a7-481">FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="f06a7-482">FW regel 8 (tooInternet) is van toepassing, verkeer is toegestaan, sessie snat omzetten uit tooroot DNS-server op Hallo Internet is</span><span class="sxs-lookup"><span data-stu-id="f06a7-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="f06a7-483">Internet-DNS-server reageert, omdat deze sessie is gestart vanuit Hallo firewall, antwoord Hallo wordt geaccepteerd door Hallo-firewall</span><span class="sxs-lookup"><span data-stu-id="f06a7-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="f06a7-484">Omdat dit een vastgestelde sessie, stuurt Hallo firewall Hallo antwoord toohello initiëren DNS01-server</span><span class="sxs-lookup"><span data-stu-id="f06a7-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="f06a7-485">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f06a7-486">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-487">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="f06a7-488">Hallo DNS-server ontvangt in de cache opgeslagen antwoord Hallo en vervolgens reageert toohello eerste aanvraag back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="f06a7-489">Hallo UDR route voor subnet backend maakt Hallo firewall Hallo volgende hop</span><span class="sxs-lookup"><span data-stu-id="f06a7-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="f06a7-490">Er geen uitgaande NSG-regels bestaan op Hallo back-end-subnet, is verkeer toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="f06a7-491">Dit is een vastgestelde sessie op Hallo firewall, antwoord Hallo wordt doorgestuurd door Hallo firewall back toohello IIS-server</span><span class="sxs-lookup"><span data-stu-id="f06a7-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="f06a7-492">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f06a7-493">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="f06a7-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="f06a7-494">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="f06a7-495">IIS01 ontvangt antwoord Hallo van DNS01</span><span class="sxs-lookup"><span data-stu-id="f06a7-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="f06a7-496">(Toegestaan) Back-endserver server tooFrontend</span><span class="sxs-lookup"><span data-stu-id="f06a7-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="f06a7-497">Een beheerder is aangemeld tooAppVM02 via RDP opvraagt een bestand rechtstreeks vanaf Hallo IIS01 server via windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="f06a7-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="f06a7-498">Hallo UDR route voor subnet Backend maakt Hallo firewall Hallo volgende hop</span><span class="sxs-lookup"><span data-stu-id="f06a7-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="f06a7-499">Omdat er geen uitgaande NSG-regels op Hallo antwoord Hallo van back-end-subnet is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="f06a7-500">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="f06a7-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f06a7-501">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-502">FW regel 2-5 (RDP-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f06a7-503">FW regels 6 en 7 (App-regels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f06a7-504">FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="f06a7-505">FW regel 9 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="f06a7-506">FW regel 10 (Intra-Subnet) is van toepassing, verkeer is toegestaan, firewall verkeer too10.0.1.4 (IIS01) wordt doorgegeven</span><span class="sxs-lookup"><span data-stu-id="f06a7-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="f06a7-507">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f06a7-508">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-509">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="f06a7-510">Als de juiste verificatie en autorisatie, IIS01 Hallo verzoek accepteert en antwoordt</span><span class="sxs-lookup"><span data-stu-id="f06a7-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="f06a7-511">Hallo UDR route voor subnet Frontend maakt Hallo firewall Hallo volgende hop</span><span class="sxs-lookup"><span data-stu-id="f06a7-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="f06a7-512">Omdat er geen uitgaande NSG-regels op Hallo Frontend subnet Hallo antwoord is toegestaan</span><span class="sxs-lookup"><span data-stu-id="f06a7-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="f06a7-513">Omdat dit een bestaande sessie Hallo firewall voor deze reactie is toegestaan en Hallo firewall retourneert Hallo antwoord tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="f06a7-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="f06a7-514">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="f06a7-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f06a7-515">NSG-regel 1 (Internet Block) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="f06a7-516">Standaard NSG-regels toestaat subnet toosubnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="f06a7-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="f06a7-517">AppVM02 Hallo-antwoord wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="f06a7-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="f06a7-518">(Geweigerd) Internet direct tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="f06a7-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="f06a7-519">Internet-gebruiker probeert tooaccess Hallo webserver IIS01, via Hallo FrontEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="f06a7-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f06a7-520">Aangezien er geen eindpunten voor HTTP-verkeer is geopend zijn, dit zou niet doorgeven aan Hallo Cloudservice en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="f06a7-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f06a7-521">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, blokkeren Hallo NSG (Internet blokkeren) op Hallo Frontend subnet dit verkeer</span><span class="sxs-lookup"><span data-stu-id="f06a7-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="f06a7-522">Ten slotte Hallo Frontend subnet UDR route zou verzenden uitgaand verkeer van IIS01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen zijn verwijderen verdediging tussen Hallo internet en IIS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="f06a7-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="f06a7-523">(Geweigerd) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="f06a7-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="f06a7-524">Internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess</span><span class="sxs-lookup"><span data-stu-id="f06a7-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f06a7-525">Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="f06a7-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f06a7-526">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, blokkeren Hallo NSG (Internet blokkeren) dit verkeer</span><span class="sxs-lookup"><span data-stu-id="f06a7-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="f06a7-527">Ten slotte Hallo UDR route zou verzenden uitgaand verkeer van AppVM01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen verdediging tussen zijn neerzetten Hallo internet en AppVM01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="f06a7-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="f06a7-528">(Geweigerd) Frontend server tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="f06a7-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="f06a7-529">Stel IIS01 is geknoeid en schadelijke code probeert tooscan Hallo back-endservers voor subnet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f06a7-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="f06a7-530">Hallo Frontend subnet UDR route zou uitgaand verkeer van IIS01 toohello firewall als de volgende hop Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="f06a7-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="f06a7-531">Dit is geen iets dat kan worden gewijzigd door Hallo geknoeid VM.</span><span class="sxs-lookup"><span data-stu-id="f06a7-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="f06a7-532">Hallo firewall zou Hallo-verkeer verwerken als Hallo-aanvraag is tooAppVM01 of toohello DNS-server voor DNS-zoekacties die verkeer kan mogelijk worden toegestaan door de firewall hello (vervaldatum tooFW regels 7 en 9).</span><span class="sxs-lookup"><span data-stu-id="f06a7-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="f06a7-533">Al het andere verkeer wordt geblokkeerd door FW regel 11 (alle weigeren).</span><span class="sxs-lookup"><span data-stu-id="f06a7-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="f06a7-534">Of geavanceerde detectie van dreigingen op Hallo-firewall is ingeschakeld (Zie de documentatie Hallo leverancier voor uw specifieke netwerkapparaat advanced threat mogelijkheden, die niet in dit document wordt besproken), zelfs als het verkeer dat zou worden toegestaan door Hallo basic regels doorsturen beschreven in dit document kan worden voorkomen als Hallo-verkeer bevat handtekeningen van bekende of patronen die een regel voor geavanceerde threat vlag.</span><span class="sxs-lookup"><span data-stu-id="f06a7-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="f06a7-535">(Geweigerd) Internet-DNS-lookup op DNS-server</span><span class="sxs-lookup"><span data-stu-id="f06a7-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f06a7-536">Internet-gebruiker probeert een interne DNS-record op DNS01 via BackEnd001.CloudApp.Net service toolookup</span><span class="sxs-lookup"><span data-stu-id="f06a7-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="f06a7-537">Aangezien er geen eindpunten voor DNS-verkeer is geopend zijn, dit zou niet doorgeven aan Hallo Cloudservice en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="f06a7-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f06a7-538">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt Hallo NSG regel (Internet blokkeren) op Hallo Frontend subnet dit verkeer geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="f06a7-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="f06a7-539">Ten slotte Hallo back-end subnet UDR route zou verzenden uitgaand verkeer van DNS01 toohello firewall als de volgende hop Hallo en Hallo firewall zou dit zien als asymmetrische verkeer en uitgaande antwoord Hallo Thus er ten minste drie onafhankelijke lagen zijn verwijderen verdediging tussen Hallo internet en DNS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="f06a7-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="f06a7-540">(Geweigerd) TooSQL internettoegang via Firewall</span><span class="sxs-lookup"><span data-stu-id="f06a7-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="f06a7-541">Internet-gebruiker opvraagt SQL-gegevens uit SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="f06a7-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f06a7-542">Aangezien er geen eindpunten geopend voor SQL zijn, dit zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="f06a7-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="f06a7-543">Als de SQL-eindpunten zijn geopend voor een bepaalde reden, zouden Hallo firewall regelverwerking beginnen:</span><span class="sxs-lookup"><span data-stu-id="f06a7-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="f06a7-544">FW regel 1 (FW Mgmt) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f06a7-545">FW regels (regels RDP), 2-5 niet toepassen, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f06a7-546">FW regel 6 en 7 (autorisatieregels) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f06a7-547">FW regel 8 (tooInternet) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="f06a7-548">FW regel 9 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="f06a7-549">FW regel 10 (Intra-Subnet) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="f06a7-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="f06a7-550">FW regel 11 (alle weigeren) is van toepassing, het verkeer wordt geblokkeerd, stoppen, regelverwerking</span><span class="sxs-lookup"><span data-stu-id="f06a7-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="f06a7-551">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="f06a7-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="f06a7-552">Belangrijkste Script en netwerkconfiguratie</span><span class="sxs-lookup"><span data-stu-id="f06a7-552">Main Script and Network Config</span></span>
<span data-ttu-id="f06a7-553">Hallo volledige Script opslaat in een PowerShell-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="f06a7-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="f06a7-554">Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf2.xml'.</span><span class="sxs-lookup"><span data-stu-id="f06a7-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="f06a7-555">Hallo door de gebruiker gedefinieerde variabelen zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f06a7-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="f06a7-556">Hallo-script uitvoeren en volg Hallo Firewall regel setup instructies hierboven.</span><span class="sxs-lookup"><span data-stu-id="f06a7-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="f06a7-557">Volledige Script</span><span class="sxs-lookup"><span data-stu-id="f06a7-557">Full Script</span></span>
<span data-ttu-id="f06a7-558">Dit script wordt, op basis van Hallo door de gebruiker gedefinieerde variabelen:</span><span class="sxs-lookup"><span data-stu-id="f06a7-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="f06a7-559">Verbinding maken met tooan Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="f06a7-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="f06a7-560">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="f06a7-560">Create a new storage account</span></span>
3. <span data-ttu-id="f06a7-561">Maak een nieuw VNet en drie subnetten zoals gedefinieerd in het configuratiebestand voor Hallo netwerk</span><span class="sxs-lookup"><span data-stu-id="f06a7-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="f06a7-562">Vijf virtuele machines; opzetten firewall 1 en 4 WindowsServer VM 's</span><span class="sxs-lookup"><span data-stu-id="f06a7-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="f06a7-563">Configureer UDR inclusief:</span><span class="sxs-lookup"><span data-stu-id="f06a7-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="f06a7-564">Twee nieuwe routetabellen maken</span><span class="sxs-lookup"><span data-stu-id="f06a7-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="f06a7-565">Routes toohello tabellen toevoegen</span><span class="sxs-lookup"><span data-stu-id="f06a7-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="f06a7-566">Tabellen tooappropriate subnetten binden</span><span class="sxs-lookup"><span data-stu-id="f06a7-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="f06a7-567">Doorsturen via IP inschakelen op Hallo NVA</span><span class="sxs-lookup"><span data-stu-id="f06a7-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="f06a7-568">Configureer het NSG inclusief:</span><span class="sxs-lookup"><span data-stu-id="f06a7-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="f06a7-569">Maken van een NSG</span><span class="sxs-lookup"><span data-stu-id="f06a7-569">Creating a NSG</span></span>
   2. <span data-ttu-id="f06a7-570">Een regel toe te voegen</span><span class="sxs-lookup"><span data-stu-id="f06a7-570">Adding a rule</span></span>
   3. <span data-ttu-id="f06a7-571">Binding Hallo NSG toohello juiste subnetten</span><span class="sxs-lookup"><span data-stu-id="f06a7-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="f06a7-572">Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.</span><span class="sxs-lookup"><span data-stu-id="f06a7-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06a7-573">Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f06a7-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="f06a7-574">Alleen foutberichten in rood zijn aanleiding.</span><span class="sxs-lookup"><span data-stu-id="f06a7-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="f06a7-575">Netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="f06a7-575">Network Config File</span></span>
<span data-ttu-id="f06a7-576">Dit xml-bestand opslaan met bijgewerkte locatie en voeg Hallo koppeling toothis toohello $NetworkConfigFile variabele in bovenstaande Hallo-script bestand.</span><span class="sxs-lookup"><span data-stu-id="f06a7-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="f06a7-577">Voorbeeldscripts toepassing</span><span class="sxs-lookup"><span data-stu-id="f06a7-577">Sample Application Scripts</span></span>
<span data-ttu-id="f06a7-578">Als u een voorbeeldtoepassing tooinstall voor deze en andere voorbeelden van het Perimeternetwerk wilt, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="f06a7-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bidirectionele DMZ met NVA, NSG en UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logische weergave van Hallo Firewall-regels"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Een Object FrontEnd-netwerk maken"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Een DNS-Server-Object maken"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Kopie van de standaardregel voor RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 regel"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Pictogram voor toepassing omleiding"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Bestemming NAT-pictogram"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass-pictogram"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewallregel Management"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "RDP-firewallregel"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Web-firewallregel"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "AppVM01 firewallregel"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Uitgaande firewallregel"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "DNS-firewallregel"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Intra-VNet-firewallregel"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regel voor weigeren van Firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activering van de firewall-regel"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
