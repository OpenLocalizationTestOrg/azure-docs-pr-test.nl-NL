---
title: "Voorbeeld van de DMZ – bouwen een DMZ om netwerken met een Firewall, UDR en NSG te beveiligen | Microsoft Docs"
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
ms.openlocfilehash: fdb3c5cbd3acee90386352c6f180a71aa81f54fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="example-3--build-a-dmz-to-protect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="9e780-103">Voorbeeld 3: een DMZ netwerken met een Firewall, UDR en NSG beschermen bouwen</span><span class="sxs-lookup"><span data-stu-id="9e780-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="9e780-104">[Ga terug naar de grens van Best Practices beveiligingspagina][HOME]</span><span class="sxs-lookup"><span data-stu-id="9e780-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="9e780-105">In dit voorbeeld wordt een DMZ gemaakt met een firewall, vier windows-servers, gebruiker gedefinieerde routering, doorsturen via IP en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="9e780-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="9e780-106">Deze begeleidt ook bij elk van de relevante opdrachten voor het bieden van een beter begrip van elke stap.</span><span class="sxs-lookup"><span data-stu-id="9e780-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="9e780-107">Er is ook een sectie verkeer Scenario voor een gedetailleerd stapsgewijs hoe verkeer wordt uitgevoerd door de lagen verdediging in het Perimeternetwerk.</span><span class="sxs-lookup"><span data-stu-id="9e780-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="9e780-108">Ten slotte in de verwijzingen is sectie de volledige code en de instructies voor het bouwen van deze omgeving om te testen en Experimenteer met verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="9e780-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="9e780-109">![Bidirectionele DMZ met NVA, NSG en UDR][1]</span><span class="sxs-lookup"><span data-stu-id="9e780-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="9e780-110">Instellen van de omgeving</span><span class="sxs-lookup"><span data-stu-id="9e780-110">Environment Setup</span></span>
<span data-ttu-id="9e780-111">In dit voorbeeld is er een abonnement dat het volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="9e780-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="9e780-112">Drie cloudservices: 'SecSvc001', 'FrontEnd001' en 'BackEnd001'</span><span class="sxs-lookup"><span data-stu-id="9e780-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="9e780-113">Een virtueel netwerk 'CorpNetwork' met drie subnetten: 'SecNet', 'FrontEnd' en back-end'</span><span class="sxs-lookup"><span data-stu-id="9e780-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="9e780-114">Een virtueel netwerkapparaat, in dit voorbeeld van een firewall, die is verbonden met het subnet SecNet</span><span class="sxs-lookup"><span data-stu-id="9e780-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span></span>
* <span data-ttu-id="9e780-115">Een Windows-Server waarmee een toepassing webserver ('IIS01')</span><span class="sxs-lookup"><span data-stu-id="9e780-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="9e780-116">Twee windows-servers die toepassing terug vertegenwoordigen end servers ('AppVM01', 'AppVM02')</span><span class="sxs-lookup"><span data-stu-id="9e780-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="9e780-117">Een Windows-server met een DNS-server ('DNS01')</span><span class="sxs-lookup"><span data-stu-id="9e780-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="9e780-118">In de sectie Verwijzingen hieronder is er een PowerShell-script dat de meeste van de hierboven beschreven omgeving bouwt.</span><span class="sxs-lookup"><span data-stu-id="9e780-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="9e780-119">Opbouwen van de virtuele machines en virtuele netwerken, hoewel worden uitgevoerd door het voorbeeldscript worden niet beschreven in dit document uitvoeriger.</span><span class="sxs-lookup"><span data-stu-id="9e780-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="9e780-120">De omgeving maken:</span><span class="sxs-lookup"><span data-stu-id="9e780-120">To build the environment:</span></span>

1. <span data-ttu-id="9e780-121">Het netwerk config XML-bestand zijn opgenomen in de sectie Verwijzingen (bijgewerkt met de naam, locatie en IP-adressen zodat deze overeenkomt met het gegeven scenario)</span><span class="sxs-lookup"><span data-stu-id="9e780-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="9e780-122">Bijwerken van de gebruikersvariabelen in het script moet overeenkomen met de omgeving die het script wordt uitgevoerd tegen (abonnementen, servicenamen, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="9e780-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="9e780-123">Voer het script in PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e780-123">Execute the script in PowerShell</span></span>

<span data-ttu-id="9e780-124">**Opmerking**: de regio die wordt aangegeven in het PowerShell-script moet overeenkomen met de regio die wordt aangegeven in het netwerk van het XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="9e780-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="9e780-125">Nadat het script wordt uitgevoerd kan de volgende stappen voor na script kunnen worden genomen:</span><span class="sxs-lookup"><span data-stu-id="9e780-125">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="9e780-126">Stel de firewallregels, deze procedure wordt besproken in de sectie met de titel: Beschrijving van de Firewall-regel.</span><span class="sxs-lookup"><span data-stu-id="9e780-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="9e780-127">Optioneel zijn in de sectie Verwijzingen twee scripts voor het instellen van de webserver en de appserver met een eenvoudige webtoepassing waarmee testen met deze configuratie DMZ.</span><span class="sxs-lookup"><span data-stu-id="9e780-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="9e780-128">Nadat het script uitgevoerd in de firewall regels moeten worden voltooid, dit wordt beschreven in het gedeelte: Firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="9e780-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="9e780-129">Door de gebruiker gedefinieerde Routering</span><span class="sxs-lookup"><span data-stu-id="9e780-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="9e780-130">Standaard worden de volgende systeemroutes gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="9e780-130">By default, the following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="9e780-131">De VNETLocal is altijd de prefix(en) opgegeven adres van de VNet voor die specifieke netwerk (ie het wordt gewijzigd van VNet naar VNet, afhankelijk van hoe elke specifieke VNet is gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="9e780-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="9e780-132">De resterende systeemroutes zijn statisch en standaard als hierboven.</span><span class="sxs-lookup"><span data-stu-id="9e780-132">The remaining system routes are static and default as above.</span></span>

<span data-ttu-id="9e780-133">Als voor de prioriteit, routes worden verwerkt via de langste voorvoegsel overeen (LPM)-methode, dus het meest specifiek route in de tabel toepassing zou zijn op een gegeven doeladres.</span><span class="sxs-lookup"><span data-stu-id="9e780-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span></span>

<span data-ttu-id="9e780-134">Daarom zou verkeer (bijvoorbeeld naar de server DNS01 10.0.2.4) voor het lokale netwerk (10.0.0.0/16) worden gerouteerd tussen het VNet naar de bestemming als gevolg van de route 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="9e780-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span></span> <span data-ttu-id="9e780-135">Met andere woorden, voor 10.0.2.4, de 10.0.0.0/16 route is het meest specifiek route, hoewel de 10.0.0.0/8 en 0.0.0.0/0 ook kunnen toegepast, maar omdat ze minder specifieke ze niet op dit verkeer.</span><span class="sxs-lookup"><span data-stu-id="9e780-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="9e780-136">Het verkeer naar 10.0.2.4 zou dus een volgende hop van de lokale VNet en gewoon routeren naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="9e780-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span></span>

<span data-ttu-id="9e780-137">Als verkeer is bedoeld voor 10.1.1.1 bijvoorbeeld, de route 10.0.0.0/16 toepassen wouldn't, maar de 10.0.0.0/8 het meest specifiek zijn zou en het verkeer zou dit ('zwart gaan') verwijderd omdat de volgende hop Null is.</span><span class="sxs-lookup"><span data-stu-id="9e780-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span></span> 

<span data-ttu-id="9e780-138">Als de bestemming niet op een van de voorvoegsels Null of de voorvoegsels VNETLocal toepassen, wordt het minst specifiek volgt routeren, 0.0.0.0/0 en worden doorgestuurd naar het Internet als de volgende hop en dus buiten de Azure internet rand.</span><span class="sxs-lookup"><span data-stu-id="9e780-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="9e780-139">Als er twee identieke voorvoegsels in de routetabel aanwezig zijn, wordt het volgende is de volgorde van voorkeur op basis van de routes 'bron'-kenmerk:</span><span class="sxs-lookup"><span data-stu-id="9e780-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span></span>

1. <span data-ttu-id="9e780-140">'VirtualAppliance' = van een gebruiker gedefinieerde Route handmatig worden toegevoegd aan de tabel</span><span class="sxs-lookup"><span data-stu-id="9e780-140">"VirtualAppliance" = A User Defined Route manually added to the table</span></span>
2. <span data-ttu-id="9e780-141">'VPNGateway' een dynamische Route BGP (gebruikt in combinatie met hybride netwerken), = toegevoegd door een dynamische netwerkprotocol, deze routes kunnen op den duur veranderen als het protocol voor dynamische wordt automatisch in het netwerk als peer is ingesteld aangepast</span><span class="sxs-lookup"><span data-stu-id="9e780-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="9e780-142">'Standaard' = de Systeemroutes, het lokale VNet en de statische vermeldingen, zoals wordt weergegeven in de bovenstaande routetabel.</span><span class="sxs-lookup"><span data-stu-id="9e780-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="9e780-143">U kunt nu de gebruiker gedefinieerde routering (UDR) gebruiken met ExpressRoute en cross-premises VPN-Gateways om af te dwingen binnenkomend en uitgaand verkeer worden doorgestuurd naar een virtueel netwerkapparaat (NVA).</span><span class="sxs-lookup"><span data-stu-id="9e780-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premises traffic to be routed to a network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-the-local-routes"></a><span data-ttu-id="9e780-144">De lokale routes maken</span><span class="sxs-lookup"><span data-stu-id="9e780-144">Creating the local routes</span></span>
<span data-ttu-id="9e780-145">In dit voorbeeld worden twee routeringstabellen nodig, één voor de front-end- en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="9e780-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span></span> <span data-ttu-id="9e780-146">Elke tabel is geladen met statische routes die geschikt is voor het opgegeven subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-146">Each table is loaded with static routes appropriate for the given subnet.</span></span> <span data-ttu-id="9e780-147">In dit voorbeeld heeft elke tabel drie routes:</span><span class="sxs-lookup"><span data-stu-id="9e780-147">For the purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="9e780-148">Lokaal subnetverkeer met geen volgende Hop gedefinieerd, zodat lokaal subnetverkeer voor het overslaan van de firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span></span>
2. <span data-ttu-id="9e780-149">Virtueel netwerkverkeer met een volgende Hop gedefinieerd als een firewall, overschrijft dit de standaardregel waarmee lokale VNet-verkeer routeren rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="9e780-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span></span>
3. <span data-ttu-id="9e780-150">Alle resterende verkeer (0/0) met een volgende Hop gedefinieerd als de firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span></span>

<span data-ttu-id="9e780-151">Als de routeringstabellen zijn gemaakt zijn ze gekoppeld aan hun subnetten.</span><span class="sxs-lookup"><span data-stu-id="9e780-151">Once the routing tables are created they are bound to their subnets.</span></span> <span data-ttu-id="9e780-152">Voor het subnet Frontend er routeringstabel eenmaal gemaakt en gekoppeld aan het subnet als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="9e780-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="9e780-153">Bijvoorbeeld, de volgende opdrachten worden gebruikt voor het bouwen van de routetabel, een gebruiker gedefinieerde route toevoegen en vervolgens de routetabel binden aan een subnet (Opmerking; de items onder die begint met een dollarteken (bijvoorbeeld: $BESubnet) zijn van de gebruiker gedefinieerde variabelen uit het script in de verwijzing naar sectie van dit document):</span><span class="sxs-lookup"><span data-stu-id="9e780-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="9e780-154">De basistabel routering moet eerst worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e780-154">First the base routing table must be created.</span></span> <span data-ttu-id="9e780-155">In dit fragment toont het maken van de tabel voor de back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-155">This snippet shows the creation of the table for the Backend subnet.</span></span> <span data-ttu-id="9e780-156">In het script wordt ook een bijbehorende tabel gemaakt voor het subnet Frontend.</span><span class="sxs-lookup"><span data-stu-id="9e780-156">In the script, a corresponding table is also created for the Frontend subnet.</span></span>
   
     <span data-ttu-id="9e780-157">Nieuwe AzureRouteTable-naam $BERouteTableName '</span><span class="sxs-lookup"><span data-stu-id="9e780-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="9e780-158">Zodra de routetabel is gemaakt, kunnen specifieke gebruiker gedefinieerde routes worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9e780-158">Once the route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="9e780-159">In deze snipped wordt (0.0.0.0/0) van alle verkeer gerouteerd via het virtuele apparaat (een variabele, $VMIP [0] wordt gebruikt om door te geven in het IP-adres toegewezen wanneer het virtuele apparaat eerder in het script is gemaakt).</span><span class="sxs-lookup"><span data-stu-id="9e780-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span></span> <span data-ttu-id="9e780-160">In het script wordt ook een bijbehorende regel gemaakt in de Frontend-tabel.</span><span class="sxs-lookup"><span data-stu-id="9e780-160">In the script, a corresponding rule is also created in the Frontend table.</span></span>
   
     <span data-ttu-id="9e780-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="9e780-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="9e780-162">De bovenstaande routevermelding wordt overschreven door de '0.0.0.0/0' standaardroute, maar de standaardregel 10.0.0.0/16 nog steeds bestaande waarmee verkeer binnen het VNet rechtstreeks naar de bestemming en niet naar het virtuele apparaat netwerk routeren.</span><span class="sxs-lookup"><span data-stu-id="9e780-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span></span> <span data-ttu-id="9e780-163">Juiste dit gedrag van de volgende regel moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9e780-163">To correct this behavior the follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="9e780-164">Op dit moment is er een keuze kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e780-164">At this point there is a choice to be made.</span></span> <span data-ttu-id="9e780-165">Al het verkeer wordt met de bovenstaande twee routes route aan de firewall voor de beoordeling, zelfs verkeer binnen één subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="9e780-166">Dit kan nodig zijn, maar waarmee verkeer binnen een subnet voor het routeren lokaal zonder betrokkenheid van de firewall van een derde zeer specifieke regel kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9e780-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="9e780-167">Deze route statussen van een adres voor het lokale subnet kunt just destine routeren er rechtstreeks (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="9e780-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="9e780-168">Ten slotte wordt met de routeringstabel gemaakt en gevuld met een gebruiker gedefinieerde routes, moet de tabel nu worden gebonden aan een subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span></span> <span data-ttu-id="9e780-169">In het script is ook de front-end-routetabel gebonden aan de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-169">In the script, the front end route table is also bound to the Frontend subnet.</span></span> <span data-ttu-id="9e780-170">Hier wordt het script binding voor de back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-170">Here is the binding script for the back end subnet.</span></span>
   
     <span data-ttu-id="9e780-171">Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '</span><span class="sxs-lookup"><span data-stu-id="9e780-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="9e780-172">Doorsturen via IP</span><span class="sxs-lookup"><span data-stu-id="9e780-172">IP Forwarding</span></span>
<span data-ttu-id="9e780-173">Een onderdeel companion UDR, is het doorsturen via IP.</span><span class="sxs-lookup"><span data-stu-id="9e780-173">A companion feature to UDR, is IP Forwarding.</span></span> <span data-ttu-id="9e780-174">Dit is een instelling op een virtueel apparaat dat is toegestaan voor het ontvangen verkeer niet specifiek zijn gericht op het toestel en vervolgens doorsturen dat verkeer naar de uiteindelijke bestemming.</span><span class="sxs-lookup"><span data-stu-id="9e780-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span></span>

<span data-ttu-id="9e780-175">Bijvoorbeeld als verkeer van AppVM01 een aanvraag bij de server DNS01 doet wilt UDR routeren dit aan de firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span></span> <span data-ttu-id="9e780-176">Met het doorsturen via IP is ingeschakeld, wordt het verkeer voor de bestemming DNS01 (10.0.2.4) worden geaccepteerd door het toestel (10.0.0.4) en vervolgens doorgestuurd naar de uiteindelijke bestemming (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="9e780-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="9e780-177">Zonder doorsturen via IP ingeschakeld op de Firewall, wordt verkeer niet geaccepteerd door het toestel ondanks dat de routetabel de firewall als de volgende hop is.</span><span class="sxs-lookup"><span data-stu-id="9e780-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9e780-178">Het is essentieel om te onthouden doorsturen via IP inschakelen in combinatie met de gebruiker gedefinieerde routering.</span><span class="sxs-lookup"><span data-stu-id="9e780-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="9e780-179">Instellen van het doorsturen via IP is één opdracht en kan worden uitgevoerd tijdens de aanmaak van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9e780-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="9e780-180">Voor de stroom van dit voorbeeld is het codefragment is aan het einde van het script, en met de opdrachten UDR gegroepeerd:</span><span class="sxs-lookup"><span data-stu-id="9e780-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span></span>

1. <span data-ttu-id="9e780-181">Roept het VM-exemplaar dat uw virtuele apparaat, de firewall in dit geval is, en doorsturen via IP inschakelen (Opmerking; een item in rood die begint met een dollarteken (bijvoorbeeld: $VMName[0]) is een door de gebruiker gedefinieerde variabele van het script in de sectie Verwijzingen van dit document.</span><span class="sxs-lookup"><span data-stu-id="9e780-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="9e780-182">De op nul vierkante haken, [0] Hiermee geeft u de eerste virtuele machine in de matrix van virtuele machines voor het voorbeeldscript werken zonder dat aanpassingen nodig, de eerste virtuele machine (VM 0) moet de firewall):</span><span class="sxs-lookup"><span data-stu-id="9e780-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span></span>
   
     <span data-ttu-id="9e780-183">Get-AzureVM-naam $VMName [0] - ServiceName $ServiceName [0] | \`</span><span class="sxs-lookup"><span data-stu-id="9e780-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="9e780-184">Netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="9e780-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="9e780-185">In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met een enkele regel.</span><span class="sxs-lookup"><span data-stu-id="9e780-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="9e780-186">Deze groep wordt vervolgens uitsluitend gekoppeld aan de front-end- en back-end-subnetten (niet de SecNet).</span><span class="sxs-lookup"><span data-stu-id="9e780-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span></span> <span data-ttu-id="9e780-187">Declaratief wordt samengesteld met de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-187">Declaratively the following rule is being built:</span></span>

1. <span data-ttu-id="9e780-188">Verkeer (alle poorten) van het Internet naar het hele VNet (alle subnetten) is geweigerd</span><span class="sxs-lookup"><span data-stu-id="9e780-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="9e780-189">Hoewel het nsg's in dit voorbeeld worden gebruikt, worden de belangrijkste doel is als een laag secundaire beveiliging tegen handmatige onjuiste configuratie.</span><span class="sxs-lookup"><span data-stu-id="9e780-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="9e780-190">We willen alle binnenkomende verkeer blokkeren met vanaf het internet aan de front-end of back-end-subnetten, verkeer alleen door het SecNet-subnet aan de firewall moeten stromen (en vervolgens passende bij de Frontend- of back-end subnetten).</span><span class="sxs-lookup"><span data-stu-id="9e780-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span></span> <span data-ttu-id="9e780-191">Plus, aan de regels UDR aanwezig is, verkeer om het in de front-end of back-end-subnetten zou worden omgeleid uit aan de firewall (dankzij UDR).</span><span class="sxs-lookup"><span data-stu-id="9e780-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span></span> <span data-ttu-id="9e780-192">De firewall zou dit zien als een asymmetrische stroom en het uitgaande verkeer wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9e780-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span></span> <span data-ttu-id="9e780-193">Er zijn dus drie lagen van beveiliging voor het beveiligen van de front-end- en back-end-subnetten; 1) er zijn geen open eindpunten op de FrontEnd001 en BackEnd001 cloudservices, 2) nsg's voor het weigeren van verkeer van het Internet, 3) de firewall weggehaald asymmetrische verkeer.</span><span class="sxs-lookup"><span data-stu-id="9e780-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="9e780-194">Een interessant punt met betrekking tot de Netwerkbeveiligingsgroep in dit voorbeeld is dat deze slechts één regel, die bevat hieronder worden weergegeven die voor het weigeren van internet-verkeer op het volledige virtuele netwerk, waaronder het subnet van de beveiliging is.</span><span class="sxs-lookup"><span data-stu-id="9e780-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet `
        from the Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="9e780-195">Echter, aangezien het NSG wordt alleen gekoppeld aan de front-end- en back-end-subnetten, de regel is niet verwerkt op het verkeer inkomend verkeer naar het subnet van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9e780-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span></span> <span data-ttu-id="9e780-196">Als gevolg hiervan, zelfs als de NSG-regel geen internetverkeer aan een adres op het VNet, staat omdat het NSG nooit is gebonden aan het subnet van de beveiliging, worden verkeer overgebracht naar het subnet van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9e780-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="9e780-197">Firewallregels</span><span class="sxs-lookup"><span data-stu-id="9e780-197">Firewall Rules</span></span>
<span data-ttu-id="9e780-198">Op de firewall moet doorsturen regels worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e780-198">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="9e780-199">Omdat de firewall geblokkeerd of doorsturen van alle binnenkomende, uitgaande en intra-VNet-verkeer is worden veel firewallregels vereist.</span><span class="sxs-lookup"><span data-stu-id="9e780-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="9e780-200">Alle binnenkomend verkeer bereikt beveiligingsservice openbaar IP-adres (op verschillende poorten), ook moeten worden verwerkt door de firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span></span> <span data-ttu-id="9e780-201">Er is een best practice diagram van de logische stroom voor het instellen van de subnetten te en firewall-regels om te voorkomen dat later bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9e780-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span></span> <span data-ttu-id="9e780-202">De volgende afbeelding is een logische weergave van de firewallregels voor dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9e780-202">The following figure is a logical view of the firewall rules for this example:</span></span>

<span data-ttu-id="9e780-203">![Logische weergave van de Firewall-regels][2]</span><span class="sxs-lookup"><span data-stu-id="9e780-203">![Logical View of the Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="9e780-204">Op basis van het virtuele netwerk-apparaat gebruikt, variëren de beheerpoorten.</span><span class="sxs-lookup"><span data-stu-id="9e780-204">Based on the Network Virtual Appliance used, the management ports will vary.</span></span> <span data-ttu-id="9e780-205">In dit voorbeeld wordt verwezen naar een Barracuda NextGen Firewall gebruikt die poort 22, 801 en 807.</span><span class="sxs-lookup"><span data-stu-id="9e780-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="9e780-206">Raadpleeg de documentatie van de leverancier toestel om te zoeken welke poorten gebruikt voor het beheer van het apparaat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e780-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="9e780-207">Beschrijving van de logische regel</span><span class="sxs-lookup"><span data-stu-id="9e780-207">Logical Rule Description</span></span>
<span data-ttu-id="9e780-208">In het bovenstaande logisch diagram wordt het subnet van de beveiliging niet weergegeven omdat de firewall de enige resource in dat subnet is dit diagram wordt weergegeven, de firewall-regels en hoe ze logisch toestaan of verkeersstromen en niet de werkelijke gerouteerde pad weigeren.</span><span class="sxs-lookup"><span data-stu-id="9e780-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span></span> <span data-ttu-id="9e780-209">Ook de externe poorten voor de RDP-verkeer hoger zijn geselecteerd varieerde poorten (8014 – 8026) en enigszins uitgelijnd met de laatste twee octetten van het lokale IP-adres voor de leesbaarheid eenvoudiger zijn geselecteerd (bijvoorbeeld 10.0.1.4-adres van de lokale server is gekoppeld aan de externe poort 8014), maar een hogere poorten voor niet-conflicterende kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e780-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="9e780-210">Bijvoorbeeld, moeten we 7 typen regels, deze regeltypen worden als volgt beschreven:</span><span class="sxs-lookup"><span data-stu-id="9e780-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="9e780-211">Externe regels (voor inkomend verkeer):</span><span class="sxs-lookup"><span data-stu-id="9e780-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="9e780-212">Firewallregel voor beheer: Met deze regel omleidings-App kunt verkeer door te geven aan de management-poorten van het virtuele netwerk-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9e780-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span></span>
  2. <span data-ttu-id="9e780-213">RDP-regels (voor elke WindowsServer): deze vier regels (één voor elke server) wordt beheer van de afzonderlijke servers via RDP toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span></span> <span data-ttu-id="9e780-214">Dit kan ook worden gebundeld in één regel, afhankelijk van de mogelijkheden van het virtuele netwerk-apparaat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e780-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="9e780-215">Regels voor het verkeer van toepassing: Er zijn twee toepassing verkeersregels, de eerste voor het verkeer van de web-front-end en de tweede voor het back-end-verkeer (bijvoorbeeld webserver gegevenslaag).</span><span class="sxs-lookup"><span data-stu-id="9e780-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="9e780-216">De configuratie van deze regels, zal afhankelijk zijn van de netwerkarchitectuur (waar uw servers worden geplaatst) en er verkeer stromen (welke richting de verkeersstromen en welke poorten worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="9e780-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="9e780-217">De eerste regel wordt het verkeer van de werkelijke toepassing bereiken van de toepassingsserver toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-217">The first rule will allow the actual application traffic to reach the application server.</span></span> <span data-ttu-id="9e780-218">Terwijl de andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services voor toegang tot de toepassing(en) toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="9e780-219">In dit voorbeeld is er één webserver op poort 80, dus een firewallregel voor één toepassing binnenkomend verkeer worden omgeleid naar het externe IP-adres, het web servers interne IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9e780-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span> <span data-ttu-id="9e780-220">De sessie omgeleide verkeer zou worden NAT moest de interne server.</span><span class="sxs-lookup"><span data-stu-id="9e780-220">The redirected traffic session would be NAT’d to the internal server.</span></span>
     * <span data-ttu-id="9e780-221">De tweede regel van toepassing verkeer is het back-end-regel voor het toestaan dat de webserver Neem contact op met de server AppVM01 (maar niet AppVM02) via een willekeurige poort.</span><span class="sxs-lookup"><span data-stu-id="9e780-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="9e780-222">Interne regels (voor intra-VNet-verkeer)</span><span class="sxs-lookup"><span data-stu-id="9e780-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="9e780-223">Uitgaand naar Internet regel: met deze regel wordt verkeer van een netwerk te geven aan de geselecteerde netwerken toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span></span> <span data-ttu-id="9e780-224">Deze regel is meestal een standaardregel al op de firewall, maar een uitgeschakelde status.</span><span class="sxs-lookup"><span data-stu-id="9e780-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span></span> <span data-ttu-id="9e780-225">Deze regel moet worden ingeschakeld voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9e780-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="9e780-226">DNS-regel: Met deze regel kunnen alleen DNS (poort 53)-verkeer door te geven aan de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="9e780-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="9e780-227">Voor deze omgeving die meeste verkeer van de Frontend naar de back-end wordt geblokkeerd, kan deze regel specifiek DNS van een lokale subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="9e780-228">Subnet naar Subnet regel: met deze regel wordt als u een server op het subnet van de back-end verbinding maken met een willekeurige server in de front-end-subnet (maar niet andersom).</span><span class="sxs-lookup"><span data-stu-id="9e780-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span></span>
* <span data-ttu-id="9e780-229">Foutveilige regel (voor verkeer dat niet voldoet aan een van de bovenstaande):</span><span class="sxs-lookup"><span data-stu-id="9e780-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span></span>
  1. <span data-ttu-id="9e780-230">Alle Verkeersregel voor weigeren: Dit moet altijd de laatste regel (in termen van prioriteit), en als zodanig als een van de verkeersstromen niet overeen met een van de vorige regels die wordt door deze regel wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9e780-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="9e780-231">Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig.</span><span class="sxs-lookup"><span data-stu-id="9e780-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="9e780-232">Een willekeurige poort is toegestaan voor eenvoudige van dit voorbeeld is in een echte scenario de meest specifieke poort op de tweede verkeersregel van de toepassing en adresbereiken moeten worden gebruikt om de kwetsbaarheid van deze regel te beperken.</span><span class="sxs-lookup"><span data-stu-id="9e780-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="9e780-233">Zodra alle bovenstaande regels zijn gemaakt, is het belangrijk om te controleren van de prioriteit van elke regel om ervoor te zorgen verkeer wordt toegestaan of geweigerd desgewenst.</span><span class="sxs-lookup"><span data-stu-id="9e780-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="9e780-234">In dit voorbeeld zijn de regels in volgorde van prioriteit.</span><span class="sxs-lookup"><span data-stu-id="9e780-234">For this example, the rules are in priority order.</span></span> <span data-ttu-id="9e780-235">Het is gemakkelijk buiten de firewall vanwege niet-geordende regels worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="9e780-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span></span> <span data-ttu-id="9e780-236">Ten minste Zorg ervoor dat het beheer van de firewall zelf is altijd de absolute hoogste prioriteit regel.</span><span class="sxs-lookup"><span data-stu-id="9e780-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="9e780-237">Regel voor vereisten</span><span class="sxs-lookup"><span data-stu-id="9e780-237">Rule Prerequisites</span></span>
<span data-ttu-id="9e780-238">Een vereiste voor de virtuele Machine met de firewall zijn openbare eindpunten.</span><span class="sxs-lookup"><span data-stu-id="9e780-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span></span> <span data-ttu-id="9e780-239">De openbare eindpunten moeten zijn geopend voor de firewall verkeer verwerken.</span><span class="sxs-lookup"><span data-stu-id="9e780-239">For the firewall to process traffic the appropriate public endpoints must be open.</span></span> <span data-ttu-id="9e780-240">Er zijn drie typen verkeer in dit voorbeeld; De RDP-verkeer 1) beheer van verkeer voor beheer op de firewall en firewallregels, 2) om de windows-servers en 3) toepassing verkeer te regelen.</span><span class="sxs-lookup"><span data-stu-id="9e780-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="9e780-241">Dit zijn de drie kolommen van de verkeerstypen in het bovenste helft van de logische weergave van de firewallregels hierboven.</span><span class="sxs-lookup"><span data-stu-id="9e780-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e780-242">Een sleutel takeway hier is om te weten dat **alle** verkeer wordt geleverd door de firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="9e780-243">Dus met extern bureaublad met de server IIS01 wordt zelfs als het in de Front-End-Cloudservice en op de front-end-subnet voor toegang tot deze server RDP moet aan de firewall op poort 8014, en vervolgens de firewall voor het routeren van de RDP-aanvraag intern met de RDP-Por IIS01 toestaan t.</span><span class="sxs-lookup"><span data-stu-id="9e780-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="9e780-244">Knop voor de Azure portal 'Verbinden' werkt niet omdat er geen directe RDP-pad naar IIS01 (zo ver mogelijk de portal kunt zien).</span><span class="sxs-lookup"><span data-stu-id="9e780-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="9e780-245">Dit betekent dat alle verbindingen van internet naar de Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx (verwijzing in het bovenstaande diagram voor de toewijzing van de externe poort en intern IP-adres en poort).</span><span class="sxs-lookup"><span data-stu-id="9e780-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="9e780-246">Een eindpunt kan worden geopend op het moment van de virtuele machine maken of build boekt als in het voorbeeldscript en de hieronder weergegeven in dit codefragment (Opmerking; een item die begint met een dollarteken (bijvoorbeeld: $VMName[$i]) is een door de gebruiker gedefinieerde variabele van het script in de cties verwijzing n van dit document.</span><span class="sxs-lookup"><span data-stu-id="9e780-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="9e780-247">'$I' vierkante haken, [$i] Hiermee geeft u het nummer van de matrix van een specifieke virtuele machine in een matrix van virtuele machines):</span><span class="sxs-lookup"><span data-stu-id="9e780-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="9e780-248">Hoewel het niet duidelijk hier weergegeven vanwege het gebruik van variabelen, maar eindpunten zijn **alleen** geopend op de Cloud Security Service.</span><span class="sxs-lookup"><span data-stu-id="9e780-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span></span> <span data-ttu-id="9e780-249">Dit is om ervoor te zorgen dat alle binnenkomend verkeer wordt verwerkt (gerouteerd, NAT waren, verloren) door de firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span></span>

<span data-ttu-id="9e780-250">Een management-client moet worden geïnstalleerd op een computer voor het beheren van de firewall en maken van de configuraties die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="9e780-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="9e780-251">Zie de documentatie van uw firewall (of andere NVA)-leverancier voor het beheren van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="9e780-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="9e780-252">De rest van deze sectie en de volgende sectie, Firewall-regels maken, wordt de configuratie van de firewall zelf, via de leveranciers management-client (d.w.z. niet in de Azure-portal of PowerShell) beschreven.</span><span class="sxs-lookup"><span data-stu-id="9e780-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="9e780-253">Instructies voor het downloaden van de client en verbinding maken met de in dit voorbeeld gebruikt Barracuda vindt u hier: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="9e780-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="9e780-254">Zodra u aangemeld bent op de firewall, maar voordat u firewallregels maken, zijn er twee vereiste objectklassen die kunnen maken van de regels gemakkelijker; Netwerk- en Service-objecten.</span><span class="sxs-lookup"><span data-stu-id="9e780-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span></span>

<span data-ttu-id="9e780-255">In dit voorbeeld moet drie objecten van het benoemde netwerk gedefinieerde (één voor de front-end-subnet en het subnet ook een netwerkobject voor het IP-adres van de DNS-server van de back-end).</span><span class="sxs-lookup"><span data-stu-id="9e780-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span></span> <span data-ttu-id="9e780-256">Maken van een benoemde netwerk. starten vanuit het dashboard van de client Barracuda NG Admin, gaat u naar het tabblad configuratie, in de operationele configuratiesectie Ruleset, vervolgens klikt u op "Netwerken" in het menu Firewallobjecten, klik op Nieuw in het menu Bewerken netwerken.</span><span class="sxs-lookup"><span data-stu-id="9e780-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span></span> <span data-ttu-id="9e780-257">Het object network kan nu worden gemaakt, door de naam en het voorvoegsel toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="9e780-257">The network object can now be created, by adding the name and the prefix:</span></span>

<span data-ttu-id="9e780-258">![Een Object FrontEnd-netwerk maken][3]</span><span class="sxs-lookup"><span data-stu-id="9e780-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="9e780-259">Hiermee maakt u een netwerk met de naam voor de front-end-subnet, een vergelijkbaar object moet worden gemaakt voor de back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span></span> <span data-ttu-id="9e780-260">De subnetten kunnen nu gemakkelijker verwezen met de naam in de firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="9e780-260">Now the subnets can be more easily referenced by name in the firewall rules.</span></span>

<span data-ttu-id="9e780-261">Voor het Object van de DNS-Server:</span><span class="sxs-lookup"><span data-stu-id="9e780-261">For the DNS Server Object:</span></span>

<span data-ttu-id="9e780-262">![Een DNS-Server-Object maken][4]</span><span class="sxs-lookup"><span data-stu-id="9e780-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="9e780-263">Deze één verwijzing naar een IP-adres wordt gebruikt in een DNS-regel verderop in dit document.</span><span class="sxs-lookup"><span data-stu-id="9e780-263">This single IP address reference will be utilized in a DNS rule later in the document.</span></span>

<span data-ttu-id="9e780-264">De tweede vereiste objecten zijn Services objecten.</span><span class="sxs-lookup"><span data-stu-id="9e780-264">The second prerequisite objects are Services objects.</span></span> <span data-ttu-id="9e780-265">Deze vertegenwoordigt het RDP-verbindingspoorten voor elke server.</span><span class="sxs-lookup"><span data-stu-id="9e780-265">These will represent the RDP connection ports for each server.</span></span> <span data-ttu-id="9e780-266">Aangezien het bestaande object van de RDP-service is gekoppeld aan de standaardpoort voor RDP, kunnen 3389, nieuwe Services worden gemaakt om verkeer van de externe (8014 8026)-poorten toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span></span> <span data-ttu-id="9e780-267">De nieuwe poorten kunnen ook worden toegevoegd aan de bestaande RDP-service, maar voor een eenvoudige demonstratie een afzonderlijke regel voor elke server kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e780-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="9e780-268">Maken van een nieuwe RDP-regel voor een server. vanaf het dashboard van de client Barracuda NG Admin, gaat u naar het tabblad configuratie in de operationele configuratiesectie op Ruleset, en vervolgens klikt u op 'Services' in het menu Firewallobjecten, schuif omlaag in de lijst met services en selecteer de service 'RDP'.</span><span class="sxs-lookup"><span data-stu-id="9e780-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span></span> <span data-ttu-id="9e780-269">Met de rechtermuisknop op en selecteert u kopiëren, en vervolgens met de rechtermuisknop op en selecteer plakken.</span><span class="sxs-lookup"><span data-stu-id="9e780-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="9e780-270">Er is nu een RDP-Copy1-Object dat kan worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="9e780-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="9e780-271">Met de rechtermuisknop op de RDP-Copy1 en selecteer bewerken, het serviceobject bewerken venster maximaal zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9e780-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="9e780-272">![Kopie van de standaardregel voor RDP][5]</span><span class="sxs-lookup"><span data-stu-id="9e780-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="9e780-273">De waarden kunnen worden bewerkt ter vertegenwoordiging van de RDP-service voor een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="9e780-273">The values can then be edited to represent the RDP service for a specific server.</span></span> <span data-ttu-id="9e780-274">Voor AppVM01 de bovenstaande standaardregel voor RDP moet worden gewijzigd naar aanleiding van een nieuwe Service-naam, beschrijving en externe RDP-poort die wordt gebruikt in het diagram afbeelding 8 (Opmerking: de poorten van de RDP-standaardwaarde van 3389 worden gewijzigd in de externe poort die wordt gebruikt voor deze specifieke server in het geval van AppVM01 is de externe poort 8025) de gewijzigde service worden hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9e780-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span></span>

<span data-ttu-id="9e780-275">![AppVM01 regel][6]</span><span class="sxs-lookup"><span data-stu-id="9e780-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="9e780-276">Dit proces moet worden herhaald voor het maken van RDP-Services voor de overige servers; AppVM02, DNS01 en IIS01.</span><span class="sxs-lookup"><span data-stu-id="9e780-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="9e780-277">Het maken van deze Services maakt het maken van de regel eenvoudiger en duidelijker in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="9e780-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="9e780-278">Een RDP-service voor de Firewall is niet nodig om twee redenen; 1) de eerste de firewall VM een installatiekopie op basis van Linux is SSH op poort 22 zou worden gebruikt voor het beheer van de virtuele machine in plaats van RDP en 2)-poort 22, en twee andere poorten zijn toegestaan in de eerste management regel die hieronder worden beschreven om toe te staan voor de connectiviteit van het beheer.</span><span class="sxs-lookup"><span data-stu-id="9e780-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="9e780-279">Firewall-regels maken</span><span class="sxs-lookup"><span data-stu-id="9e780-279">Firewall Rules Creation</span></span>
<span data-ttu-id="9e780-280">Er zijn drie soorten firewallregels die in dit voorbeeld gebruikt, alle hebben verschillende pictogrammen:</span><span class="sxs-lookup"><span data-stu-id="9e780-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="9e780-281">De regel voor het omleiden van toepassing: ![toepassing omleidings-pictogram][7]</span><span class="sxs-lookup"><span data-stu-id="9e780-281">The Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="9e780-282">De doel-NAT-regel: ![bestemming NAT-pictogram][8]</span><span class="sxs-lookup"><span data-stu-id="9e780-282">The Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="9e780-283">De regel op te geven: ![pictogram doorgeven][9]</span><span class="sxs-lookup"><span data-stu-id="9e780-283">The Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="9e780-284">Meer informatie over deze regels kan worden gevonden op de website Barracuda.</span><span class="sxs-lookup"><span data-stu-id="9e780-284">More information on these rules can be found at the Barracuda web site.</span></span>

<span data-ttu-id="9e780-285">De volgende regels maken (of Controleer of de bestaande standaardregels) starten vanuit het dashboard van de client Barracuda NG Admin gaat u naar het tabblad configuratie, in de configuratie van de operationele sectie Ruleset op.</span><span class="sxs-lookup"><span data-stu-id="9e780-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="9e780-286">Een raster aangeroepen, 'Main regels' wordt de bestaande regels voor de actieve als gedeactiveerde op deze firewall weergeven.</span><span class="sxs-lookup"><span data-stu-id="9e780-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="9e780-287">In de rechterbovenhoek van dit raster is een klein, groene '+' knop, klik hierop om een nieuwe regel te maken (Opmerking: uw firewall mogelijk 'vergrendeld' om wijzigingen, als u ziet een knop 'Vergrendelen' gemarkeerd en u zich niet maken of bewerken van regels, klik op deze knop om de regelset 'ontgrendelen' en  bewerken toestaan).</span><span class="sxs-lookup"><span data-stu-id="9e780-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span></span> <span data-ttu-id="9e780-288">Als u bewerken van een bestaande regel wilt, selecteert u deze regel, met de rechtermuisknop op en selecteer regel bewerken.</span><span class="sxs-lookup"><span data-stu-id="9e780-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="9e780-289">Als uw regels zijn gemaakt en/of gewijzigd, moet aan de firewall gepusht en wordt geactiveerd, als u dit niet doet de regel wijzigingen pas van kracht.</span><span class="sxs-lookup"><span data-stu-id="9e780-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span></span> <span data-ttu-id="9e780-290">Het proces push en activering wordt hieronder de beschrijvingen van de regel details beschreven.</span><span class="sxs-lookup"><span data-stu-id="9e780-290">The push and activation process is described below the details rule descriptions.</span></span>

<span data-ttu-id="9e780-291">De details van elke regel vereist voor het voltooien van dit voorbeeld worden als volgt beschreven:</span><span class="sxs-lookup"><span data-stu-id="9e780-291">The specifics of each rule required to complete this example are described as follows:</span></span>

* <span data-ttu-id="9e780-292">**Firewall-regel Management**: deze App omleiden regel staat toe dat verkeer door te geven aan de beheerpoorten van de virtuele netwerkapparaat, in dit voorbeeld van een Barracuda NextGen Firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="9e780-293">De management-poorten zijn 801, 807 en eventueel 22.</span><span class="sxs-lookup"><span data-stu-id="9e780-293">The management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="9e780-294">De interne en externe poorten zijn hetzelfde (d.w.z. geen poortvertaling).</span><span class="sxs-lookup"><span data-stu-id="9e780-294">The external and internal ports are the same (i.e. no port translation).</span></span> <span data-ttu-id="9e780-295">Deze regel, SETUP-MGMT-toegang, is een standaardregel en (in Barracuda NextGen Firewall versie 6.1) standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9e780-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="9e780-296">![Firewallregel Management][10]</span><span class="sxs-lookup"><span data-stu-id="9e780-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="9e780-297">De bron-adresruimte in deze regel is aanwezig, als het beheer van IP-adresbereiken gekend zijn, waardoor dit bereik ook sneller de kwetsbaarheid voor aanvallen op de management-poorten.</span><span class="sxs-lookup"><span data-stu-id="9e780-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span></span>
> 
> 

* <span data-ttu-id="9e780-298">**Regels voor RDP**: deze bestemming NAT-regels kunnen beheer van de afzonderlijke servers via RDP.</span><span class="sxs-lookup"><span data-stu-id="9e780-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span></span>
  <span data-ttu-id="9e780-299">Er zijn vier kritieke velden die nodig zijn voor het maken van deze regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-299">There are four critical fields needed to create this rule:</span></span>
  
  1. <span data-ttu-id="9e780-300">Bron: zodat RDP 'Een' vanaf elke locatie en de verwijzing wordt gebruikt in het veld bron.</span><span class="sxs-lookup"><span data-stu-id="9e780-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span></span>
  2. <span data-ttu-id="9e780-301">Service – het juiste serviceobject eerder hebt gemaakt, in dit geval 'AppVM01 RDP' gebruiken, externe poorten doorsturen naar de lokale servers IP-adres en poort 3386 (de standaard RDP-poort).</span><span class="sxs-lookup"><span data-stu-id="9e780-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span></span> <span data-ttu-id="9e780-302">Deze specifieke regel is voor RDP-toegang tot AppVM01.</span><span class="sxs-lookup"><span data-stu-id="9e780-302">This specific rule is for RDP access to AppVM01.</span></span>
  3. <span data-ttu-id="9e780-303">Doel – moet het *lokale poort op de firewall*, 'DCHP 1 lokale IP-' of eth0 als statische IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="9e780-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="9e780-304">Het rangtelwoord (eth0, eth1, enzovoort) is mogelijk anders als uw netwerkapparaat meerdere lokale interfaces heeft.</span><span class="sxs-lookup"><span data-stu-id="9e780-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="9e780-305">Dit is de poort die de firewall van verstuurt (mogelijk dezelfde zijn als de ontvangende poort), de werkelijke gerouteerde bestemming is in het veld voor de lijst met doelservers.</span><span class="sxs-lookup"><span data-stu-id="9e780-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span></span>
  4. <span data-ttu-id="9e780-306">Omleiding – dit gedeelte wordt uitgelegd het virtuele apparaat waar u uiteindelijk dit verkeer worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="9e780-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span></span> <span data-ttu-id="9e780-307">De eenvoudigste omleiding is het IP- en de poort (optioneel) plaatsen in de lijst met doelservers-veld.</span><span class="sxs-lookup"><span data-stu-id="9e780-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span></span> <span data-ttu-id="9e780-308">Als er geen poort wordt gebruikt de doelpoort op de binnenkomende aanvraag worden (ie geen vertaling) gebruikt als een poort is de poort aangewezen worden ook NAT zou samen met het IP-adres adresseren.</span><span class="sxs-lookup"><span data-stu-id="9e780-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span></span>
     
     <span data-ttu-id="9e780-309">![RDP-firewallregel][11]</span><span class="sxs-lookup"><span data-stu-id="9e780-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="9e780-310">Een totaal van vier RDP regels moet worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="9e780-310">A total of four RDP rules will need to be created:</span></span> 
     
     | <span data-ttu-id="9e780-311">Regelnaam</span><span class="sxs-lookup"><span data-stu-id="9e780-311">Rule Name</span></span> | <span data-ttu-id="9e780-312">Server</span><span class="sxs-lookup"><span data-stu-id="9e780-312">Server</span></span> | <span data-ttu-id="9e780-313">Service</span><span class="sxs-lookup"><span data-stu-id="9e780-313">Service</span></span> | <span data-ttu-id="9e780-314">Lijst met doelservers</span><span class="sxs-lookup"><span data-stu-id="9e780-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="9e780-315">RDP-naar-IIS01</span><span class="sxs-lookup"><span data-stu-id="9e780-315">RDP-to-IIS01</span></span> |<span data-ttu-id="9e780-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="9e780-316">IIS01</span></span> |<span data-ttu-id="9e780-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="9e780-317">IIS01 RDP</span></span> |<span data-ttu-id="9e780-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="9e780-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="9e780-319">RDP-naar-DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-319">RDP-to-DNS01</span></span> |<span data-ttu-id="9e780-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-320">DNS01</span></span> |<span data-ttu-id="9e780-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="9e780-321">DNS01 RDP</span></span> |<span data-ttu-id="9e780-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="9e780-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="9e780-323">RDP-naar-AppVM01</span><span class="sxs-lookup"><span data-stu-id="9e780-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="9e780-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="9e780-324">AppVM01</span></span> |<span data-ttu-id="9e780-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="9e780-325">AppVM01 RDP</span></span> |<span data-ttu-id="9e780-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="9e780-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="9e780-327">RDP-naar-AppVM02</span><span class="sxs-lookup"><span data-stu-id="9e780-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="9e780-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="9e780-328">AppVM02</span></span> |<span data-ttu-id="9e780-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="9e780-329">AppVm02 RDP</span></span> |<span data-ttu-id="9e780-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="9e780-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="9e780-331">Beperking u het bereik van de bron- en velden beperkt u de kwetsbaarheid voor aanvallen.</span><span class="sxs-lookup"><span data-stu-id="9e780-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span></span> <span data-ttu-id="9e780-332">De meest beperkte mogelijkheden die zorgen de functionaliteit dat ervoor moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e780-332">The most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="9e780-333">**Toepassing verkeersregels**: Er zijn twee toepassing verkeersregels, de eerste voor het verkeer van de web-front-end en de tweede voor het back-end-verkeer (bijvoorbeeld webserver gegevenslaag).</span><span class="sxs-lookup"><span data-stu-id="9e780-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="9e780-334">Deze regels, zal afhankelijk zijn van de netwerkarchitectuur (waar uw servers worden geplaatst) en er verkeer stromen (welke richting de verkeersstromen en welke poorten worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="9e780-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="9e780-335">Eerst besproken, is de front-end-regel voor internetverkeer:</span><span class="sxs-lookup"><span data-stu-id="9e780-335">First discussed is the front end rule for web traffic:</span></span>
  
    <span data-ttu-id="9e780-336">![Web-firewallregel][12]</span><span class="sxs-lookup"><span data-stu-id="9e780-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="9e780-337">Deze bestemming NAT-regel kan het verkeer van de toepassing om de toepassingsserver te bereiken.</span><span class="sxs-lookup"><span data-stu-id="9e780-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span></span> <span data-ttu-id="9e780-338">Terwijl de andere regels toestaan voor de beveiliging, beheer, enz., zijn toepassing regels wat externe gebruikers of services voor toegang tot de toepassing(en) toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="9e780-339">In dit voorbeeld is er één webserver op poort 80, dus de firewallregel die één toepassing binnenkomend verkeer worden omgeleid naar het externe IP-adres, het web servers interne IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9e780-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span>
  
    <span data-ttu-id="9e780-340">**Opmerking**: dat er is geen poort toegewezen in het veld doellijst, dus de binnenkomende poort 80 (of 443 voor de geselecteerde Service) worden gebruikt voor het omleiden van de webserver.</span><span class="sxs-lookup"><span data-stu-id="9e780-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span></span> <span data-ttu-id="9e780-341">Als de webserver luistert op een andere poort, bijvoorbeeld poort 8080, wordt het veld doellijst kan worden bijgewerkt naar 10.0.1.4:8080 om toe te staan voor de poort-omleiding.</span><span class="sxs-lookup"><span data-stu-id="9e780-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span></span>
  
    <span data-ttu-id="9e780-342">De volgende regel van toepassing verkeer is het back-end-regel voor het toestaan dat de webserver Neem contact op met de server AppVM01 (maar niet AppVM02) via elke service:</span><span class="sxs-lookup"><span data-stu-id="9e780-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="9e780-343">![AppVM01 firewallregel][13]</span><span class="sxs-lookup"><span data-stu-id="9e780-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="9e780-344">Met deze regel op te geven kunnen elke IIS-server op het subnet Frontend bereiken van de AppVM01 (IP-adres 10.0.2.5) met behulp van elk Protocol voor toegang tot gegevens die nodig is voor de webtoepassing op een willekeurige poort.</span><span class="sxs-lookup"><span data-stu-id="9e780-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span></span>
  
    <span data-ttu-id="9e780-345">In deze schermafdruk een '\<expliciete-dest\>' in het doelveld wordt gebruikt om aan te duiden 10.0.2.5 als doel.</span><span class="sxs-lookup"><span data-stu-id="9e780-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span></span> <span data-ttu-id="9e780-346">Dit kan zijn expliciete zoals wordt weergegeven of een met de naam netwerkobject (net als bij de vereisten voor de DNS-server).</span><span class="sxs-lookup"><span data-stu-id="9e780-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span></span> <span data-ttu-id="9e780-347">Dit is aan de beheerder van de firewall wat betreft welke methode wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e780-347">This is up to the administrator of the firewall as to which method will be used.</span></span> <span data-ttu-id="9e780-348">Als u wilt toevoegen 10.0.2.5 als een Explict Desitnation, dubbelklik op de eerste lege rij onder \<expliciete-dest\> en voer het adres in het venster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9e780-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span></span>
  
    <span data-ttu-id="9e780-349">Met deze regel geeft is geen NAT nodig omdat dit interne verkeer, is zodat de verbindingsmethode kan worden ingesteld op 'Nee snat omzetten'.</span><span class="sxs-lookup"><span data-stu-id="9e780-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span></span>
  
    <span data-ttu-id="9e780-350">**Opmerking**: het Bronnetwerk in deze regel wordt een resource in het subnet FrontEnd als er slechts één of een bekende specifiek aantal webservers, een netwerkobject resource kan worden gemaakt als u wilt meer specifiek zijn voor de exacte IP-adressen in plaats van de gehele Frontend-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="9e780-351">Deze regel maakt gebruik van de service 'Any' om de voorbeeldtoepassing vereenvoudigen instellen en gebruiken, ook hierdoor ICMPv4 (ping) in een enkele regel.</span><span class="sxs-lookup"><span data-stu-id="9e780-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="9e780-352">Dit is echter niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="9e780-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="9e780-353">De poorten en protocollen ('Services') moeten worden teruggebracht tot het minimum mogelijk waarmee de toepassing opnieuw aan de kwetsbaarheid voor aanvallen via deze grens te reduceren.</span><span class="sxs-lookup"><span data-stu-id="9e780-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="9e780-354">Hoewel met deze regel een verwijzing naar een expliciete-dest wordt gebruikt bevat, moet een consistente manier worden gebruikt in de firewallconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="9e780-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span></span> <span data-ttu-id="9e780-355">Het verdient aanbeveling dat het benoemde netwerk-Object worden gebruikt in de gehele voor gemakkelijker leesbaarheid en ondersteuningsmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="9e780-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="9e780-356">De expliciete-dest wordt hier alleen gebruikt om een alternatieve verwijzing naar de methode show en wordt over het algemeen niet aanbevolen (met name voor complexe configuraties).</span><span class="sxs-lookup"><span data-stu-id="9e780-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="9e780-357">**Uitgaand naar Internet regel**: doorgeven voor deze regel wordt verkeer van een Bronnetwerk moeten worden doorgegeven aan de geselecteerde doelnetwerken toestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span></span> <span data-ttu-id="9e780-358">Deze regel is een standaardregel meestal al op de Barracuda NextGen firewall, maar is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9e780-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="9e780-359">Met de rechtermuisknop op deze regel hebben toegang tot de opdracht activeren regel.</span><span class="sxs-lookup"><span data-stu-id="9e780-359">Right-clicking on this rule can access the Activate Rule command.</span></span> <span data-ttu-id="9e780-360">De regel die hier worden weergegeven is als u wilt de twee lokale subnetten die zijn gemaakt als verwijzingen in de sectie vereisten van dit document toevoegen aan het bronkenmerk van deze regel gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9e780-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span></span>
  
    <span data-ttu-id="9e780-361">![Uitgaande firewallregel][14]</span><span class="sxs-lookup"><span data-stu-id="9e780-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="9e780-362">**Een DNS-regel**: deze doorgeven regel staat toe dat alleen DNS (poort 53)-verkeer door te geven aan de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="9e780-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="9e780-363">Deze regel kunnen specifiek DNS voor deze omgeving die de meeste verkeer van de FrontEnd naar de back-end is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="9e780-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="9e780-364">![DNS-firewallregel][15]</span><span class="sxs-lookup"><span data-stu-id="9e780-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="9e780-365">**Opmerking**: In dit scherm opname de verbindingsmethode is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="9e780-365">**Note**: In this screen shot the Connection Method is included.</span></span> <span data-ttu-id="9e780-366">Omdat deze regel is voor intern IP-adres voor verkeer van interne IP-adres, wordt geen NATing is vereist, wordt deze de verbindingsmethode is ingesteld op 'Nee snat omzetten' voor deze regel op te geven.</span><span class="sxs-lookup"><span data-stu-id="9e780-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="9e780-367">**Subnet naar Subnet regel**: doorgeven voor deze regel is een standaardregel die zijn geactiveerd en gewijzigd zodat alle servers in het subnet van de back-end verbinding maken met een willekeurige server in de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9e780-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span></span> <span data-ttu-id="9e780-368">Deze regel is alle interne verkeer, zodat de verbindingsmethode kan worden ingesteld op Nee snat omzetten.</span><span class="sxs-lookup"><span data-stu-id="9e780-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span></span>
  
    <span data-ttu-id="9e780-369">![Intra-VNet-firewallregel][16]</span><span class="sxs-lookup"><span data-stu-id="9e780-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="9e780-370">**Opmerking**: het selectievakje in twee richtingen niet is ingeschakeld (noch is ingeschakeld in de meeste regels), dit is van belang voor deze regel maakt deze regel 'eenrichtings', een verbinding kan worden gestart vanuit de back-end-subnet met het netwerk front-end, maar niet de omgekeerde.</span><span class="sxs-lookup"><span data-stu-id="9e780-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span></span> <span data-ttu-id="9e780-371">Als dit selectievakje is ingeschakeld, zou deze regel in twee richtingen verkeer, wat van onze logisch diagram niet inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9e780-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="9e780-372">**Alle Verkeersregel voor weigeren**: dit moet altijd de laatste regel (in termen van prioriteit), en als zodanig als een verkeersstromen niet overeen met een van de voorgaande regels wordt door deze regel wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9e780-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="9e780-373">Dit is een standaardregel en meestal geactiveerd, worden er zijn geen wijzigingen in het algemeen nodig.</span><span class="sxs-lookup"><span data-stu-id="9e780-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="9e780-374">![Regel voor weigeren van Firewall][17]</span><span class="sxs-lookup"><span data-stu-id="9e780-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e780-375">Zodra alle bovenstaande regels zijn gemaakt, is het belangrijk om te controleren van de prioriteit van elke regel om ervoor te zorgen verkeer wordt toegestaan of geweigerd desgewenst.</span><span class="sxs-lookup"><span data-stu-id="9e780-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="9e780-376">In dit voorbeeld zijn de regels in de volgorde die ze moeten worden weergegeven in het raster Main regels in de Barracuda Management-Client te sturen.</span><span class="sxs-lookup"><span data-stu-id="9e780-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="9e780-377">Activering van de regel</span><span class="sxs-lookup"><span data-stu-id="9e780-377">Rule Activation</span></span>
<span data-ttu-id="9e780-378">Met de ruleset aan de specificatie van het diagram logica is gewijzigd, moet de ruleset worden geüpload naar de firewall en wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9e780-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span></span>

<span data-ttu-id="9e780-379">![Activering van de firewall-regel][18]</span><span class="sxs-lookup"><span data-stu-id="9e780-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="9e780-380">In de rechterbovenhoek van de management-client zijn een cluster van knoppen.</span><span class="sxs-lookup"><span data-stu-id="9e780-380">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="9e780-381">Klik op de knop 'Wijzigingen verzenden' voor het verzenden van de gewijzigde regels op de firewall en klik vervolgens op de knop 'Activeren'.</span><span class="sxs-lookup"><span data-stu-id="9e780-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="9e780-382">Deze versie van de omgeving voorbeeld is voor de activering van de firewall ruleset voltooid.</span><span class="sxs-lookup"><span data-stu-id="9e780-382">With the activation of the firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="9e780-383">Verkeer scenario 's</span><span class="sxs-lookup"><span data-stu-id="9e780-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9e780-384">Een sleutel takeway is om te weten dat **alle** verkeer wordt geleverd door de firewall.</span><span class="sxs-lookup"><span data-stu-id="9e780-384">A key takeway is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="9e780-385">Dus met extern bureaublad met de server IIS01 wordt zelfs als het in de Front-End-Cloudservice en op de front-end-subnet voor toegang tot deze server RDP moet aan de firewall op poort 8014, en vervolgens de firewall voor het routeren van de RDP-aanvraag intern met de RDP-Por IIS01 toestaan t.</span><span class="sxs-lookup"><span data-stu-id="9e780-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="9e780-386">Knop voor de Azure portal 'Verbinden' werkt niet omdat er geen directe RDP-pad naar IIS01 (zo ver mogelijk de portal kunt zien).</span><span class="sxs-lookup"><span data-stu-id="9e780-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="9e780-387">Dit betekent dat alle verbindingen van internet naar de Security-Service en een poort, bijvoorbeeld secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="9e780-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="9e780-388">Voor deze scenario's, moeten de volgende firewallregels zijn voldaan:</span><span class="sxs-lookup"><span data-stu-id="9e780-388">For these scenarios, the following firewall rules should be in place:</span></span>

1. <span data-ttu-id="9e780-389">Beheer van Firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-389">Firewall Management</span></span>
2. <span data-ttu-id="9e780-390">RDP naar IIS01</span><span class="sxs-lookup"><span data-stu-id="9e780-390">RDP to IIS01</span></span>
3. <span data-ttu-id="9e780-391">RDP naar DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-391">RDP to DNS01</span></span>
4. <span data-ttu-id="9e780-392">RDP naar AppVM01</span><span class="sxs-lookup"><span data-stu-id="9e780-392">RDP to AppVM01</span></span>
5. <span data-ttu-id="9e780-393">RDP naar AppVM02</span><span class="sxs-lookup"><span data-stu-id="9e780-393">RDP to AppVM02</span></span>
6. <span data-ttu-id="9e780-394">App-verkeer naar het Web</span><span class="sxs-lookup"><span data-stu-id="9e780-394">App Traffic to the Web</span></span>
7. <span data-ttu-id="9e780-395">App-verkeer naar AppVM01</span><span class="sxs-lookup"><span data-stu-id="9e780-395">App Traffic to AppVM01</span></span>
8. <span data-ttu-id="9e780-396">Uitgaand naar het Internet</span><span class="sxs-lookup"><span data-stu-id="9e780-396">Outbound to the Internet</span></span>
9. <span data-ttu-id="9e780-397">Frontend naar DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-397">Frontend to DNS01</span></span>
10. <span data-ttu-id="9e780-398">Intra-subnetverkeer (back-end-front-end alleen)</span><span class="sxs-lookup"><span data-stu-id="9e780-398">Intra-Subnet Traffic (back end to front end only)</span></span>
11. <span data-ttu-id="9e780-399">Alles weigeren</span><span class="sxs-lookup"><span data-stu-id="9e780-399">Deny All</span></span>

<span data-ttu-id="9e780-400">De werkelijke firewall ruleset wordt waarschijnlijk veel andere regels naast deze informatie, de regels op een bepaalde firewall wordt ook beschikken over verschillende prioriteitsnummers dan degene die hier worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="9e780-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span></span> <span data-ttu-id="9e780-401">Deze lijst en de bijbehorende cijfers worden relevantie tussen alleen deze elf regels en de relatieve prioriteit onder ze bieden.</span><span class="sxs-lookup"><span data-stu-id="9e780-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span></span> <span data-ttu-id="9e780-402">Met andere woorden; op de werkelijke firewall kan de 'RDP naar IIS01' regel getal 5, maar als het zich onder de regel 'Firewallbeheer' en boven de regel 'RDP-DNS01' zou uitgelijnd met de bedoeling van deze lijst.</span><span class="sxs-lookup"><span data-stu-id="9e780-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span></span> <span data-ttu-id="9e780-403">De lijst helpt ook bij het onderstaande scenario's zodat beknopt alternatief bevat; bijvoorbeeld 'FW regel 9 (DNS)'.</span><span class="sxs-lookup"><span data-stu-id="9e780-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="9e780-404">Ook als beknopt alternatief bevat, de vier regels voor RDP wordt gezamenlijk aangeroepen, 'de RDP-regels' wanneer het verkeer scenario houdt geen verband met RDP.</span><span class="sxs-lookup"><span data-stu-id="9e780-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span></span>

<span data-ttu-id="9e780-405">Ook intrekken dat Netwerkbeveiligingsgroepen in-place zijn voor binnenkomend internetverkeer op de front-end- en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="9e780-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="9e780-406">(Toegestaan) Internet-webserver</span><span class="sxs-lookup"><span data-stu-id="9e780-406">(Allowed) Internet to Web Server</span></span>
1. <span data-ttu-id="9e780-407">Internet aanvragen HTTP-gebruikerspagina van SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="9e780-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="9e780-408">Cloud-service geeft verkeer via open eindpunten op poort 80 voor firewall-interface op 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="9e780-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="9e780-409">Er is geen NSG die is toegewezen aan beveiliging subnet, geval system NSG-regels verkeer firewall toestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="9e780-410">Verkeer komt binnen via interne IP-adres van de firewall (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="9e780-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="9e780-411">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="9e780-412">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-413">FW regels (regels RDP), 2-5 niet toepassen, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9e780-414">FW regel 6 (App: Web) is van toepassing, verkeer wordt toegestaan, firewall NAT's naar 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="9e780-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="9e780-415">Het subnet Frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-415">The Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9e780-416">NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door de firewall, het adres van de bronserver is dus nu de firewall die zich in het subnet van de beveiliging en zichtbaar zijn voor het subnet Frontend NSG moet 'lokaal' verkeer en is dus toegestaan), verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="9e780-417">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="9e780-418">IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van de aanvraag</span><span class="sxs-lookup"><span data-stu-id="9e780-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
8. <span data-ttu-id="9e780-419">IIS01 pogingen tot initieert een FTP-sessie naar AppVM01 op subnet Backend</span><span class="sxs-lookup"><span data-stu-id="9e780-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="9e780-420">De route UDR op subnet Frontend maakt de firewall van de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-420">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
10. <span data-ttu-id="9e780-421">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="9e780-422">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="9e780-423">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-424">FW regel 2-5 (RDP-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="9e780-425">FW regel 6 (App: Web) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span></span>
    4. <span data-ttu-id="9e780-426">FW regel 7 (App: back-end) is van toepassing, verkeer is toegestaan, firewall stuurt het verkeer naar 10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="9e780-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="9e780-427">Het back-end-subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-427">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9e780-428">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-429">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="9e780-430">AppVM01 ontvangt de aanvraag en start van de sessie en antwoordt</span><span class="sxs-lookup"><span data-stu-id="9e780-430">AppVM01 receives the request and initiates the session and responds</span></span>
14. <span data-ttu-id="9e780-431">De route UDR op subnet Backend maakt de firewall van de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-431">The UDR route on Backend subnet makes the firewall the next hop</span></span>
15. <span data-ttu-id="9e780-432">Aangezien er zijn geen uitgaande NSG-regels in het back-end-subnet dat het antwoord is toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
16. <span data-ttu-id="9e780-433">Omdat dit verkeer op een vastgestelde sessie retourneert stuurt de firewall het antwoord terug naar de webserver (IIS01)</span><span class="sxs-lookup"><span data-stu-id="9e780-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span></span>
17. <span data-ttu-id="9e780-434">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9e780-435">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-436">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="9e780-437">De IIS-server het antwoord ontvangt, de transactie met AppVM01 en daarna voltooit de HTTP-antwoord bouwen, wordt deze HTTP-antwoord verzonden naar de aanvrager</span><span class="sxs-lookup"><span data-stu-id="9e780-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span></span>
19. <span data-ttu-id="9e780-438">Aangezien er zijn geen uitgaande NSG-regels in het antwoord is toegestaan subnet Frontend</span><span class="sxs-lookup"><span data-stu-id="9e780-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
20. <span data-ttu-id="9e780-439">Het HTTP-antwoord treffers in de firewall en omdat dit het antwoord op een NAT-sessie tot stand gebrachte is wordt geaccepteerd door de firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span></span>
21. <span data-ttu-id="9e780-440">De firewall stuurt vervolgens door het antwoord terug naar de Internet-gebruiker</span><span class="sxs-lookup"><span data-stu-id="9e780-440">The firewall then redirects the response back to the Internet User</span></span>
22. <span data-ttu-id="9e780-441">Omdat er geen uitgaande ontvangt NSG-regels of UDR hops op het subnet Frontend het antwoord is toegestaan en de Internet-gebruiker de aangevraagde webpagina.</span><span class="sxs-lookup"><span data-stu-id="9e780-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-internet-rdp-to-backend"></a><span data-ttu-id="9e780-442">(Toegestaan) Internet RDP met back-end</span><span class="sxs-lookup"><span data-stu-id="9e780-442">(Allowed) Internet RDP to Backend</span></span>
1. <span data-ttu-id="9e780-443">RDP-sessie op AppVM01 via SecSvc001.CloudApp.Net:8025, waarbij 8025 het poortnummer van de gebruiker die is toegewezen voor de firewallregel 'RDP-AppVM01 is' serverbeheerder op internet-aanvragen</span><span class="sxs-lookup"><span data-stu-id="9e780-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span></span>
2. <span data-ttu-id="9e780-444">Geeft de cloudservice-verkeer via de open eindpunten op poort 8025 voor firewall-interface op 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="9e780-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="9e780-445">Er is geen NSG die is toegewezen aan beveiliging subnet, geval system NSG-regels verkeer firewall toestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="9e780-446">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="9e780-447">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-448">FW regel 2 (RDP IIS) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9e780-449">FW regel 3 (RDP DNS01) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9e780-450">FW regel 4 (RDP AppVM01) is van toepassing, het verkeer wordt toegestaan, firewall NAT's naar 10.0.2.5:3386 (RDP-poort op AppVM01)</span><span class="sxs-lookup"><span data-stu-id="9e780-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="9e780-451">Het back-end-subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-451">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9e780-452">NSG-regel 1 (Internet blokkeren) is niet van toepassing (dit verkeer is NAT zou door de firewall, het adres van de bronserver is dus nu de firewall die zich in het subnet van de beveiliging en zichtbaar zijn voor het subnet voor back-end NSG moet 'lokaal' verkeer en is dus toegestaan), verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="9e780-453">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="9e780-454">AppVM01 voor RDP-verkeer luistert en antwoordt</span><span class="sxs-lookup"><span data-stu-id="9e780-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="9e780-455">Standaardregels toepassen met geen uitgaande NSG-regels en terugkerend verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="9e780-456">UDR routes uitgaand verkeer naar de firewall als de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-456">UDR routes outbound traffic to the firewall as the next hop</span></span>
9. <span data-ttu-id="9e780-457">Omdat dit verkeer op een vastgestelde sessie retourneert het antwoord terug naar de internet-gebruiker wordt doorgegeven door de firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span></span>
10. <span data-ttu-id="9e780-458">RDP-sessie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9e780-458">RDP session is enabled</span></span>
11. <span data-ttu-id="9e780-459">AppVM01 gebruikersnaam wachtwoord gevraagd</span><span class="sxs-lookup"><span data-stu-id="9e780-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="9e780-460">(Toegestaan) Web Server DNS-lookup op DNS-server</span><span class="sxs-lookup"><span data-stu-id="9e780-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="9e780-461">Web Server, IIS01, moet een gegevensfeed op www.data.gov, maar moet u het adres omzetten.</span><span class="sxs-lookup"><span data-stu-id="9e780-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="9e780-462">De netwerkconfiguratie voor de VNet-lijsten DNS01 (10.0.2.4 op het subnet voor back-end) als de primaire DNS-server, IIS01 verzendt de DNS-aanvraag naar DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="9e780-463">UDR routes uitgaand verkeer naar de firewall als de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-463">UDR routes outbound traffic to the firewall as the next hop</span></span>
4. <span data-ttu-id="9e780-464">Er is geen uitgaand NSG-regels zijn gebonden aan het subnet Frontend, is verkeer toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="9e780-465">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="9e780-466">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-467">FW regel 2-5 (RDP-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9e780-468">FW regels 6 en 7 (App-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9e780-469">FW regel 8 (met Internet) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="9e780-470">FW regel 9 (DNS) is van toepassing, verkeer is toegestaan, firewall stuurt het verkeer naar 10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="9e780-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="9e780-471">Het back-end-subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-471">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9e780-472">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-473">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="9e780-474">DNS-server ontvangt de aanvraag</span><span class="sxs-lookup"><span data-stu-id="9e780-474">DNS server receives the request</span></span>
8. <span data-ttu-id="9e780-475">DNS-server beschikt niet over het adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op het internet</span><span class="sxs-lookup"><span data-stu-id="9e780-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
9. <span data-ttu-id="9e780-476">UDR routes uitgaand verkeer naar de firewall als de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-476">UDR routes outbound traffic to the firewall as the next hop</span></span>
10. <span data-ttu-id="9e780-477">Er is geen uitgaand NSG-regels op subnet Backend, verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="9e780-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="9e780-478">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="9e780-479">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-480">FW regel 2-5 (RDP-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="9e780-481">FW regels 6 en 7 (App-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
    4. <span data-ttu-id="9e780-482">Geldt FW regel 8 (met Internet), verkeer is toegestaan, sessie snat omzetten uit naar basis-DNS-server op het Internet is</span><span class="sxs-lookup"><span data-stu-id="9e780-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span></span>
12. <span data-ttu-id="9e780-483">Internet-DNS-server reageert, omdat deze sessie is geïnitieerd door de firewall, het antwoord wordt geaccepteerd door de firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span></span>
13. <span data-ttu-id="9e780-484">Omdat dit een vastgestelde sessie, stuurt de firewall het antwoord aan de gang worden gezet DNS01-server</span><span class="sxs-lookup"><span data-stu-id="9e780-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span></span>
14. <span data-ttu-id="9e780-485">Het back-end-subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-485">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9e780-486">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-487">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="9e780-488">De DNS-server ontvangt het antwoord plaatst en vervolgens reageert op de eerste aanvraag terug naar IIS01</span><span class="sxs-lookup"><span data-stu-id="9e780-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span></span>
16. <span data-ttu-id="9e780-489">De route UDR op subnet backend maakt de firewall van de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-489">The UDR route on backend subnet makes the firewall the next hop</span></span>
17. <span data-ttu-id="9e780-490">Er bestaat geen uitgaande NSG-regels op het subnet voor back-end, is verkeer toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="9e780-491">Dit is een vastgestelde sessie op de firewall, het antwoord wordt doorgestuurd door de firewall terug naar de IIS-server</span><span class="sxs-lookup"><span data-stu-id="9e780-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span></span>
19. <span data-ttu-id="9e780-492">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9e780-493">Er is geen NSG-regel voor inkomend verkeer van de back-end-subnet met het subnet Frontend, zodat geen van de NSG regels toepassen</span><span class="sxs-lookup"><span data-stu-id="9e780-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="9e780-494">De standaardregel systeem voor het verkeer tussen subnetten zou dit verkeer toestaan, zodat het verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
20. <span data-ttu-id="9e780-495">IIS01 ontvangt het antwoord van DNS01</span><span class="sxs-lookup"><span data-stu-id="9e780-495">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-backend-server-to-frontend-server"></a><span data-ttu-id="9e780-496">(Toegestaan) Back-endserver met Frontend-server</span><span class="sxs-lookup"><span data-stu-id="9e780-496">(Allowed) Backend server to Frontend server</span></span>
1. <span data-ttu-id="9e780-497">Een beheerder AppVM02 via RDP aangemeld op opvraagt een bestand rechtstreeks vanaf de server IIS01 via windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="9e780-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="9e780-498">De route UDR op subnet Backend maakt de firewall van de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-498">The UDR route on Backend subnet makes the firewall the next hop</span></span>
3. <span data-ttu-id="9e780-499">Aangezien er zijn geen uitgaande NSG-regels in het back-end-subnet dat het antwoord is toegestaan</span><span class="sxs-lookup"><span data-stu-id="9e780-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
4. <span data-ttu-id="9e780-500">Firewall begint regelverwerking:</span><span class="sxs-lookup"><span data-stu-id="9e780-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="9e780-501">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-502">FW regel 2-5 (RDP-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9e780-503">FW regels 6 en 7 (App-regels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9e780-504">FW regel 8 (met Internet) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="9e780-505">FW regel 9 (DNS) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="9e780-506">FW regel 10 (Intra-Subnet) is van toepassing, verkeer is toegestaan, firewall verkeer doorgegeven aan 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="9e780-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="9e780-507">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9e780-508">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-509">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="9e780-510">Als de juiste verificatie en autorisatie, IIS01 accepteert de aanvraag en reageert</span><span class="sxs-lookup"><span data-stu-id="9e780-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span></span>
7. <span data-ttu-id="9e780-511">De route UDR op subnet Frontend maakt de firewall van de volgende hop</span><span class="sxs-lookup"><span data-stu-id="9e780-511">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
8. <span data-ttu-id="9e780-512">Aangezien er zijn geen uitgaande NSG-regels in het antwoord is toegestaan subnet Frontend</span><span class="sxs-lookup"><span data-stu-id="9e780-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
9. <span data-ttu-id="9e780-513">Omdat dit een bestaande sessie op de firewall voor deze reactie is toegestaan en de firewall retourneert het antwoord op AppVM02</span><span class="sxs-lookup"><span data-stu-id="9e780-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span></span>
10. <span data-ttu-id="9e780-514">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="9e780-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9e780-515">NSG-regel 1 (Internet Block) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="9e780-516">Standaard NSG-regels toestaat subnet naar subnet verkeer, verkeer is toegestaan, stopt u de verwerking van NSG-regels</span><span class="sxs-lookup"><span data-stu-id="9e780-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="9e780-517">AppVM02 ontvangt het antwoord</span><span class="sxs-lookup"><span data-stu-id="9e780-517">AppVM02 receives the response</span></span>

#### <a name="denied-internet-direct-to-web-server"></a><span data-ttu-id="9e780-518">(Geweigerd) Rechtstreeks naar de webserver van Internet</span><span class="sxs-lookup"><span data-stu-id="9e780-518">(Denied) Internet direct to Web Server</span></span>
1. <span data-ttu-id="9e780-519">Internet-gebruiker probeert te krijgen van de webserver, IIS01, via de service FrontEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="9e780-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="9e780-520">Aangezien er geen eindpunten voor HTTP-verkeer is geopend zijn, dit zou niet doorgeven aan de Cloudservice en de server wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="9e780-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="9e780-521">Als de eindpunten geopend voor een bepaalde reden zijn, blokkeren het NSG (Internet blokkeren) op het subnet Frontend dit verkeer</span><span class="sxs-lookup"><span data-stu-id="9e780-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="9e780-522">Ten slotte de front-end-subnet UDR route zou uitgaand verkeer verzenden vanuit IIS01 aan de firewall als de volgende hop en de firewall zou dit zien als asymmetrische verkeer en het uitgaande antwoord Thus er ten minste drie onafhankelijke lagen verdediging tussen zijn neerzetten het internet en IIS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="9e780-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-backend-server"></a><span data-ttu-id="9e780-523">(Geweigerd) Internet naar back-endserver</span><span class="sxs-lookup"><span data-stu-id="9e780-523">(Denied) Internet to Backend Server</span></span>
1. <span data-ttu-id="9e780-524">Internet-gebruiker probeert te krijgen van een bestand op AppVM01 via de service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="9e780-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="9e780-525">Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit zou niet doorgeven voor de Cloudservice en wouldn't de server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="9e780-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="9e780-526">Als de eindpunten geopend voor een bepaalde reden zijn, blokkeren het NSG (Internet blokkeren) dit verkeer</span><span class="sxs-lookup"><span data-stu-id="9e780-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="9e780-527">Ten slotte de route UDR zou uitgaand verkeer verzenden vanuit AppVM01 aan de firewall als de volgende hop en de firewall zou dit zien als asymmetrische verkeer en het uitgaande antwoord, dus er zijn ten minste drie onafhankelijke lagen verdediging tussen internet verwijderen en AppVM01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="9e780-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-to-backend-server"></a><span data-ttu-id="9e780-528">(Geweigerd) Back-endserver frontend-server</span><span class="sxs-lookup"><span data-stu-id="9e780-528">(Denied) Frontend server to Backend Server</span></span>
1. <span data-ttu-id="9e780-529">Stel IIS01 is geknoeid en schadelijke code die bij de back-endservers subnet scan wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e780-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span></span>
2. <span data-ttu-id="9e780-530">De route Frontend subnet UDR zou Stuur alle uitgaande verkeer van IIS01 aan de firewall als de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="9e780-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span></span> <span data-ttu-id="9e780-531">Dit is geen iets dat kan worden gewijzigd door de VM waarmee is geknoeid.</span><span class="sxs-lookup"><span data-stu-id="9e780-531">This is not something that can be altered by the compromised VM.</span></span>
3. <span data-ttu-id="9e780-532">De firewall zou het verkeer verwerken als de aanvraag is AppVM01 of de DNS-server voor DNS-zoekacties die verkeer kan mogelijk worden toegestaan door de firewall (vanwege FW regels 7 en 9).</span><span class="sxs-lookup"><span data-stu-id="9e780-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span></span> <span data-ttu-id="9e780-533">Al het andere verkeer wordt geblokkeerd door FW regel 11 (alle weigeren).</span><span class="sxs-lookup"><span data-stu-id="9e780-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="9e780-534">Of geavanceerde detectie van dreigingen in de firewall is ingeschakeld (Zie de documentatie van de leverancier voor uw specifieke netwerkapparaat advanced threat mogelijkheden, die niet in dit document wordt besproken), zelfs als het verkeer dat door de basic doorstuurregels zou worden toegestaan beschreven in dit document kan worden voorkomen als het verkeer bevindt handtekeningen van bekende of patronen die een regel voor geavanceerde threat vlag.</span><span class="sxs-lookup"><span data-stu-id="9e780-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="9e780-535">(Geweigerd) Internet-DNS-lookup op DNS-server</span><span class="sxs-lookup"><span data-stu-id="9e780-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="9e780-536">Internet-gebruiker probeert voor het opzoeken van een interne DNS-record op DNS01 via BackEnd001.CloudApp.Net-service</span><span class="sxs-lookup"><span data-stu-id="9e780-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="9e780-537">Aangezien er geen eindpunten voor DNS-verkeer is geopend zijn, dit zou niet doorgeven aan de Cloudservice en de server wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="9e780-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="9e780-538">Als de eindpunten geopend voor een bepaalde reden zijn, wordt het NSG-regel (Internet blokkeren) op het subnet Frontend dit verkeer geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="9e780-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="9e780-539">Ten slotte de back-end subnet UDR route zou uitgaand verkeer verzenden vanuit DNS01 aan de firewall als de volgende hop en de firewall zou dit zien als asymmetrische verkeer en verwijderen van het uitgaande antwoord Thus er ten minste drie onafhankelijke lagen verdediging tussen zijn de Internet en DNS01 via de cloudservice zo wordt voorkomen dat onbevoegde/ongeoorloofde toegang.</span><span class="sxs-lookup"><span data-stu-id="9e780-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-sql-access-through-firewall"></a><span data-ttu-id="9e780-540">(Geweigerd) Internet op SQL-toegang via de Firewall</span><span class="sxs-lookup"><span data-stu-id="9e780-540">(Denied) Internet to SQL access through Firewall</span></span>
1. <span data-ttu-id="9e780-541">Internet-gebruiker opvraagt SQL-gegevens uit SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="9e780-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="9e780-542">Omdat er geen eindpunten geopend voor SQL zijn, dit zou niet doorgeven voor de Cloudservice en de firewall wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="9e780-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="9e780-543">Als SQL-eindpunten geopend voor een bepaalde reden zijn, zou de firewall regelverwerking begint:</span><span class="sxs-lookup"><span data-stu-id="9e780-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="9e780-544">FW regel 1 (FW Mgmt) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9e780-545">FW regels (regels RDP), 2-5 niet toepassen, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9e780-546">FW regel 6 en 7 (autorisatieregels) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9e780-547">FW regel 8 (met Internet) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="9e780-548">FW regel 9 (DNS) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="9e780-549">FW regel 10 (Intra-Subnet) niet van toepassing, verplaatsen naar de volgende regel</span><span class="sxs-lookup"><span data-stu-id="9e780-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span></span>
   7. <span data-ttu-id="9e780-550">FW regel 11 (alle weigeren) is van toepassing, het verkeer wordt geblokkeerd, stoppen, regelverwerking</span><span class="sxs-lookup"><span data-stu-id="9e780-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="9e780-551">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="9e780-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="9e780-552">Belangrijkste Script en netwerkconfiguratie</span><span class="sxs-lookup"><span data-stu-id="9e780-552">Main Script and Network Config</span></span>
<span data-ttu-id="9e780-553">Sla het volledige Script in een PowerShell-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="9e780-553">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="9e780-554">De netwerkconfiguratie opslaan in een bestand met de naam 'NetworkConf2.xml'.</span><span class="sxs-lookup"><span data-stu-id="9e780-554">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="9e780-555">De gebruiker gedefinieerde variabelen zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9e780-555">Modify the user defined variables as needed.</span></span> <span data-ttu-id="9e780-556">Voer het script uit en volg de bovenstaande van Firewall regel setup instructies.</span><span class="sxs-lookup"><span data-stu-id="9e780-556">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="9e780-557">Volledige Script</span><span class="sxs-lookup"><span data-stu-id="9e780-557">Full Script</span></span>
<span data-ttu-id="9e780-558">Dit script wordt, op basis van de gebruiker gedefinieerde variabelen:</span><span class="sxs-lookup"><span data-stu-id="9e780-558">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="9e780-559">Verbinding maken met een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="9e780-559">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="9e780-560">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="9e780-560">Create a new storage account</span></span>
3. <span data-ttu-id="9e780-561">Maak een nieuw VNet en drie subnetten zoals gedefinieerd in het netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="9e780-561">Create a new VNet and three subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="9e780-562">Vijf virtuele machines; opzetten firewall 1 en 4 WindowsServer VM 's</span><span class="sxs-lookup"><span data-stu-id="9e780-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="9e780-563">Configureer UDR inclusief:</span><span class="sxs-lookup"><span data-stu-id="9e780-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="9e780-564">Twee nieuwe routetabellen maken</span><span class="sxs-lookup"><span data-stu-id="9e780-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="9e780-565">Routes toevoegen aan de tabellen</span><span class="sxs-lookup"><span data-stu-id="9e780-565">Add routes to the tables</span></span>
   3. <span data-ttu-id="9e780-566">Tabellen aan de juiste subnetten binden</span><span class="sxs-lookup"><span data-stu-id="9e780-566">Bind tables to appropriate subnets</span></span>
6. <span data-ttu-id="9e780-567">Doorsturen via IP op de NVA inschakelen</span><span class="sxs-lookup"><span data-stu-id="9e780-567">Enable IP Forwarding on the NVA</span></span>
7. <span data-ttu-id="9e780-568">Configureer het NSG inclusief:</span><span class="sxs-lookup"><span data-stu-id="9e780-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="9e780-569">Maken van een NSG</span><span class="sxs-lookup"><span data-stu-id="9e780-569">Creating a NSG</span></span>
   2. <span data-ttu-id="9e780-570">Een regel toe te voegen</span><span class="sxs-lookup"><span data-stu-id="9e780-570">Adding a rule</span></span>
   3. <span data-ttu-id="9e780-571">Het NSG binden aan de juiste subnetten</span><span class="sxs-lookup"><span data-stu-id="9e780-571">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="9e780-572">Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.</span><span class="sxs-lookup"><span data-stu-id="9e780-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e780-573">Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e780-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="9e780-574">Alleen foutberichten in rood zijn aanleiding.</span><span class="sxs-lookup"><span data-stu-id="9e780-574">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet
       - Three Servers on the BackEnd Subnet
       - IP Forwading from the FireWall out to the internet
       - User Defined Routing FrontEnd and BackEnd Subnets to the NVA

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind the appropriate
      layer(s) of protection. This script serves as an example of some of the techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and the appropriate protections needed, and then effectively
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
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

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
        # Note: To ensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be the NVA.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "The SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
                # Set up all the EndPoints we'll need once we're up and running
                # Note: All traffic goes through the firewall, so we'll need to set up all ports here.
                #       Also, the firewall will be redirecting traffic to a new IP and Port in a forwarding
                #       rule, so all of these endpoint have the same public and local port and the firewall
                #       will do the mapping, NATing, and/or redirection as declared in the firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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

      # Create the Route Tables
        Write-Host "Creating the Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes to Route Tables
        Write-Host "Adding Routes to the Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate the Route Tables with the Subnets
        Write-Host "Binding Route Tables to the Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on the Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign the NSG to two Subnets
        # The NSG is *not* bound to the Security Subnet. The result
        # is that internet traffic flows only to the Security subnet
        # since the NSG bound to the Frontend and Backback subnets
        # will Deny internet traffic to those subnets.
        Write-Host "Binding the NSG to two subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="9e780-575">Netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="9e780-575">Network Config File</span></span>
<span data-ttu-id="9e780-576">Dit xml-bestand opslaan met bijgewerkte locatie en de koppeling toevoegen aan dit bestand naar de variabele $NetworkConfigFile in het bovenstaande script.</span><span class="sxs-lookup"><span data-stu-id="9e780-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="9e780-577">Voorbeeldscripts toepassing</span><span class="sxs-lookup"><span data-stu-id="9e780-577">Sample Application Scripts</span></span>
<span data-ttu-id="9e780-578">Als u een voorbeeldtoepassing voor deze en andere voorbeelden DMZ installeren wilt, een is opgegeven op de volgende koppeling: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="9e780-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="9e780-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bidirectionele DMZ met NVA, NSG en UDR"</span><span class="sxs-lookup"><span data-stu-id="9e780-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bi-directional DMZ with NVA, NSG, and UDR"</span></span>
<span data-ttu-id="9e780-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logische weergave van de Firewall-regels"</span><span class="sxs-lookup"><span data-stu-id="9e780-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logical View of the Firewall Rules"</span></span>
<span data-ttu-id="9e780-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Een Object FrontEnd-netwerk maken"</span><span class="sxs-lookup"><span data-stu-id="9e780-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Create a FrontEnd Network Object"</span></span>
<span data-ttu-id="9e780-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Een DNS-Server-Object maken"</span><span class="sxs-lookup"><span data-stu-id="9e780-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Create a DNS Server Object"</span></span>
<span data-ttu-id="9e780-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Kopie van de standaardregel voor RDP"</span><span class="sxs-lookup"><span data-stu-id="9e780-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copy of Default RDP Rule"</span></span>
<span data-ttu-id="9e780-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 regel"</span><span class="sxs-lookup"><span data-stu-id="9e780-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 Rule"</span></span>
<span data-ttu-id="9e780-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Pictogram voor toepassing omleiding"</span><span class="sxs-lookup"><span data-stu-id="9e780-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Application Redirect Icon"</span></span>
<span data-ttu-id="9e780-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Bestemming NAT-pictogram"</span><span class="sxs-lookup"><span data-stu-id="9e780-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Destination NAT Icon"</span></span>
<span data-ttu-id="9e780-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass-pictogram"</span><span class="sxs-lookup"><span data-stu-id="9e780-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass Icon"</span></span>
<span data-ttu-id="9e780-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewallregel Management"</span><span class="sxs-lookup"><span data-stu-id="9e780-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewall Management Rule"</span></span>
<span data-ttu-id="9e780-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "RDP-firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Firewall RDP Rule"</span></span>
<span data-ttu-id="9e780-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Web-firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Firewall Web Rule"</span></span>
<span data-ttu-id="9e780-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "AppVM01 firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Firewall AppVM01 Rule"</span></span>
<span data-ttu-id="9e780-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Uitgaande firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Firewall Outbound Rule"</span></span>
<span data-ttu-id="9e780-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "DNS-firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Firewall DNS Rule"</span></span>
<span data-ttu-id="9e780-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Intra-VNet-firewallregel"</span><span class="sxs-lookup"><span data-stu-id="9e780-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Firewall Intra-VNet Rule"</span></span>
<span data-ttu-id="9e780-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regel voor weigeren van Firewall"</span><span class="sxs-lookup"><span data-stu-id="9e780-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Firewall Deny Rule"</span></span>
<span data-ttu-id="9e780-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activering van de firewall-regel"</span><span class="sxs-lookup"><span data-stu-id="9e780-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
