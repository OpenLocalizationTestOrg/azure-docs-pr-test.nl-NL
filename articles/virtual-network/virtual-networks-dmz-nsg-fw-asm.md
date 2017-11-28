---
title: "toepassingen met een Firewall en nsg's van een DMZ tooprotect bouwen aaaDMZ voorbeeld – | Microsoft Docs"
description: Maken van een DMZ met een Firewall en Netwerkbeveiligingsgroepen (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="bbc6f-103">Voorbeeld 2: een DMZ tooprotect bouwen toepassingen met een Firewall en nsg 's</span><span class="sxs-lookup"><span data-stu-id="bbc6f-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="bbc6f-104">[Best Practices beveiligingspagina-grens toohello retourneren][HOME]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="bbc6f-105">In dit voorbeeld wordt een DMZ maken met een firewall, vier windows-servers en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="bbc6f-106">Deze ook begeleidt bij elk Hallo relevante opdrachten tooprovide een beter begrip van elke stap.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="bbc6f-107">Er is ook een verkeer Scenario sectie tooprovide een gedetailleerd stapsgewijs hoe verkeer wordt voortgezet via Hallo lagen verdediging in Hallo DMZ.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="bbc6f-108">Ten slotte is in de sectie Verwijzingen Hallo de volledige code Hallo en instructie toobuild deze omgeving tootest en het experiment met verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="bbc6f-109">![Inkomende DMZ met NVA en NSG][1]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="bbc6f-110">Beschrijving van de omgeving</span><span class="sxs-lookup"><span data-stu-id="bbc6f-110">Environment Description</span></span>
<span data-ttu-id="bbc6f-111">In dit voorbeeld is er een abonnement dat Hallo volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="bbc6f-112">Twee cloudservices: 'FrontEnd001' en 'BackEnd001'</span><span class="sxs-lookup"><span data-stu-id="bbc6f-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="bbc6f-113">Een virtueel netwerk 'CorpNetwork' met twee subnetten: 'FrontEnd' en back-end'</span><span class="sxs-lookup"><span data-stu-id="bbc6f-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="bbc6f-114">Een enkele Netwerkbeveiligingsgroep die toegepaste tooboth subnetten</span><span class="sxs-lookup"><span data-stu-id="bbc6f-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="bbc6f-115">Een virtueel netwerkapparaat, in dit voorbeeld een Barracuda NextGen Firewall, verbonden toohello Frontend subnet</span><span class="sxs-lookup"><span data-stu-id="bbc6f-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="bbc6f-116">Een Windows-Server waarmee een toepassing webserver ('IIS01')</span><span class="sxs-lookup"><span data-stu-id="bbc6f-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="bbc6f-117">Twee windows-servers die toepassing terug vertegenwoordigen end servers ('AppVM01', 'AppVM02')</span><span class="sxs-lookup"><span data-stu-id="bbc6f-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="bbc6f-118">Een Windows-server met een DNS-server ('DNS01')</span><span class="sxs-lookup"><span data-stu-id="bbc6f-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="bbc6f-119">Hoewel dit voorbeeld een Barracuda NextGen Firewall veel Hallo die verschillende virtuele netwerkapparaten kan worden gebruikt voor dit voorbeeld wordt.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="bbc6f-120">In onderstaande Hallo verwijzingen gedeelte is er een PowerShell-script dat de meeste Hallo-omgeving die hierboven worden beschreven bouwt.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="bbc6f-121">Gebouw Hallo VM's en virtuele netwerken worden Hoewel worden uitgevoerd door Hallo voorbeeldscript wordt niet in dit document uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="bbc6f-122">toobuild hello omgeving:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="bbc6f-123">Hallo netwerk config XML-bestand is opgenomen in de sectie Verwijzingen hello (bijgewerkt met de naam, locatie en IP-adressen toomatch Hallo gegeven scenario) opslaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="bbc6f-124">Update Hallo Gebruikersvariabelen in Hallo script toomatch Hallo omgeving Hallo script is toobe uitgevoerd (abonnementen, servicenamen, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="bbc6f-125">Hallo-script uitvoeren in PowerShell</span><span class="sxs-lookup"><span data-stu-id="bbc6f-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="bbc6f-126">**Opmerking**: Hallo regio aangegeven in Hallo PowerShell-script moet overeenkomen met de Hallo regio in xml-configuratiebestand met Hallo netwerk aangegeven.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="bbc6f-127">Zodra het Hallo-script wordt uitgevoerd kan Hallo na script stappen kan worden genomen:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="bbc6f-128">Hallo-firewallregels instellen, deze procedure wordt besproken in Hallo onderstaande sectie met de titel: Firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="bbc6f-129">Optioneel zijn in de sectie Verwijzingen Hallo twee scripts tooset up Hallo-webserver en appserver met een eenvoudige web application tooallow testen met deze configuratie DMZ.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="bbc6f-130">Hallo volgende sectie wordt uitgelegd meeste Hallo scripts instructies relatieve tooNetwork beveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="bbc6f-131">Netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="bbc6f-132">In dit voorbeeld is een groep NSG gebouwd en vervolgens geladen met zes regels.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="bbc6f-133">In het algemeen moet u eerst uw specifieke regels voor 'Toestaan' maken en vervolgens laatste Hallo algemene "Deny" regels.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="bbc6f-134">Hallo toegewezen prioriteit bepaalt welke regels eerst worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="bbc6f-135">Als verkeer tooapply tooa specifieke regel gevonden wordt, wordt er geen verdere regels worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="bbc6f-136">NSG-regels kunnen toepassen in op Hallo binnenkomende of uitgaande richting (vanuit het perspectief van de Hallo van Hallo subnet).</span><span class="sxs-lookup"><span data-stu-id="bbc6f-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="bbc6f-137">Declaratief, worden Hallo volgens de regels voor binnenkomend verkeer gebouwd:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="bbc6f-138">Interne DNS-verkeer (poort 53) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="bbc6f-139">RDP-verkeer (poort 3389) van Hallo Internet tooany VM is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="bbc6f-140">HTTP-verkeer (poort 80) van Hallo Internet toohello NVA (firewall) is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="bbc6f-141">Verkeer (alle poorten) van IIS01 tooAppVM1 is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="bbc6f-142">Verkeer (alle poorten) van Hallo Internet toohello hele VNet (beide subnetten) is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="bbc6f-143">Verkeer (alle poorten) van Hallo Frontend subnet toohello back-end-subnet is geweigerd</span><span class="sxs-lookup"><span data-stu-id="bbc6f-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="bbc6f-144">Met deze regels gebonden tooeach-subnet als een HTTP-aanvraag was binnenkomend van Hallo Internet toohello webserver beide regels 3 (toestaan) en 5 (weigeren) toepassing zou zijn, maar omdat de regel 3 heeft een hogere prioriteit alleen zou worden toegepast en regel 5 niet in de play zou komen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="bbc6f-145">Hallo HTTP-aanvraag zou dus toohello firewall toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="bbc6f-146">Als dat dezelfde verkeer tooreach hello DNS01 server probeerde, zou regel 5 (weigeren) zijn de eerste tooapply en Hallo verkeer Hallo zou niet toegestaan toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="bbc6f-147">Regel 6 (weigeren) blokken Hallo subnet Frontend in gesprekken toohello back-end-subnet (met uitzondering van toegestane regels 1 en 4-verkeer), dit beschermt Hallo back-end-netwerk als een aanvaller inbreuk Hallo webtoepassing op Hallo Frontend, Hallo aanvaller moet beperkte toegang toohello back-end '-beveiliging gebruiken' netwerk (alleen tooresources blootgesteld op Hallo AppVM01 server).</span><span class="sxs-lookup"><span data-stu-id="bbc6f-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="bbc6f-148">Er is een uitgaande standaardregel waarmee verkeer van toohello internet.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="bbc6f-149">Voor dit voorbeeld bent we uitgaand verkeer toestaat en alle regels voor uitgaande verbindingen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="bbc6f-150">toolock omlaag verkeer in beide richtingen gebruiker gedefinieerde routering is vereist, dit in een ander voorbeeld die u in Hallo vinden kunt is verkend [belangrijkste beveiliging grens document][HOME].</span><span class="sxs-lookup"><span data-stu-id="bbc6f-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="bbc6f-151">Hallo hierboven besproken NSG-regels zijn vergelijkbaar toohello NSG-regels in [voorbeeld 1: een eenvoudige DMZ met nsg's bouwen][Example1].</span><span class="sxs-lookup"><span data-stu-id="bbc6f-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="bbc6f-152">Controleer Hallo NSG beschrijving in dat document voor een gedetailleerde blik op elke regel van het NSG en de kenmerken.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="bbc6f-153">Firewallregels</span><span class="sxs-lookup"><span data-stu-id="bbc6f-153">Firewall Rules</span></span>
<span data-ttu-id="bbc6f-154">Een Beheerclient toobe geïnstalleerd op een PC toomanage Hallo firewall nodig hebt en Hallo configuraties nodig maken.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="bbc6f-155">Zie de leverancier van de documentatie van uw firewall (of andere NVA) Hallo over hoe toomanage apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="bbc6f-156">Hallo rest van deze sectie wordt beschreven Hallo configuratie van Hallo firewall zelf, via Hallo leveranciers management-client (d.w.z. niet hello Azure-portal of PowerShell).</span><span class="sxs-lookup"><span data-stu-id="bbc6f-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="bbc6f-157">Instructies voor het downloaden van de client en verbindende toohello Barracuda gebruikt in dit voorbeeld vindt u hier: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="bbc6f-158">Regels voor doorsturen moet toobe gemaakt op Hallo-firewall.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="bbc6f-159">Omdat in dit voorbeeld wordt alleen routes in gebonden toohello firewall voor internet-verkeer en vervolgens toohello webserver, wordt slechts één doorsturen NAT-regel vereist.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="bbc6f-160">Regel zou op Hallo Barracuda NextGen Firewall gebruikt in dit voorbeeld Hallo zijn een doel-NAT-regel ('zomertijd NAT') toopass dit verkeer.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="bbc6f-161">toocreate hello volgende regel (of Controleer of de bestaande standaardregels), vanaf Hallo Barracuda NG Admin client dashboard, navigeer toohello configuratie tabblad, in Hallo operationele configuratie sectie Ruleset klikt u op.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="bbc6f-162">Een raster aangeroepen, wordt 'Main regels' hello bestaande actieve en gedeactiveerd regels op Hallo firewall weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="bbc6f-163">Hallo rechterbovenhoek van dit raster is een klein, groene '+' knop, klikt u op deze toocreate een nieuwe regel (Opmerking: uw firewall mogelijk 'vergrendeld' om wijzigingen, als er een knop gemarkeerd als 'Vergrendelen' en kan niet toocreate zijn of regels bewerken, klikt u op deze knop te 'ontgrendelen' Hallo ruleSet en bewerken).</span><span class="sxs-lookup"><span data-stu-id="bbc6f-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="bbc6f-164">Als u een bestaande regel tooedit wilt, selecteert u deze regel, met de rechtermuisknop op en selecteer regel bewerken.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="bbc6f-165">Maak een nieuwe regel en geef een naam op, zoals 'WebTraffic'.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="bbc6f-166">Hallo bestemming NAT-regel pictogram uitziet: ![bestemming NAT-pictogram][2]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="bbc6f-167">Hallo-regel zelf zou als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="bbc6f-168">![Firewallregel][3]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="bbc6f-169">Hier een inkomende adres dat treffers Hallo Firewall probeert tooreach HTTP (poort 80 of 443 voor HTTPS) wordt verzonden van Firewall 'DHCP1 lokale-IP-interface en omgeleide toohello Web Server met IP-adres van 10.0.1.5 Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="bbc6f-170">Omdat Hallo-verkeer op poort 80 en gaat toohello webserver op poort 80 in afkomstig is geen poortwijziging is vereist.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="bbc6f-171">Echter Hallo Hallo doellijst kan zijn 10.0.1.5:8080 als uw webserver worden geluisterd op poort 8080 dus vertalen van de binnenkomende poort 80 op Hallo firewall tooinbound poort 8080 op Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="bbc6f-172">Een verbindingsmethode moet ook worden aangegeven, voor Hallo bestemming regel vanaf Internet, Hallo 'Dynamische snat omzetten' is het meest geschikt.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="bbc6f-173">Hoewel u slechts één regel is gemaakt is het belangrijk dat de prioriteit correct is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="bbc6f-174">Als in raster Hallo van alle regels op Hallo firewall voor dat deze nieuwe regel wordt aan de onderkant hello (onder Hallo 'BLOCKALL' regel) dit wordt nooit een rol spelen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="bbc6f-175">Zorg ervoor dat Hallo nieuwe regel voor internetverkeer hierboven Hallo BLOCKALL regel.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="bbc6f-176">Zodra het Hallo-regel is gemaakt, moet deze zijn gedistribueerd toohello firewall en wordt geactiveerd, als dit niet gebeurt Hallo regel wijziging wordt pas van kracht.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="bbc6f-177">Hallo push en activering proces wordt beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="bbc6f-178">Activering van de regel</span><span class="sxs-lookup"><span data-stu-id="bbc6f-178">Rule Activation</span></span>
<span data-ttu-id="bbc6f-179">Hello ruleset gewijzigd tooadd met deze regel, Hallo ruleset moet worden geüpload toohello firewall en geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="bbc6f-180">![Activering van de firewall-regel][4]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="bbc6f-181">In Hallo rechtsboven van Hallo Beheerclient zijn een cluster van knoppen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="bbc6f-182">Hallo 'verzenden wijzigingen' knop toosend Hallo gewijzigd regels toohello firewall, klik op de knop 'Activeren' Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="bbc6f-183">Deze versie van de omgeving voorbeeld is bij activering via Hallo Hallo firewall ruleSet voltooid.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="bbc6f-184">Eventueel Hallo post build scripts in Hallo verwijzingen sectie kan worden uitgevoerd tooadd een toepassing toothis omgeving tootest Hallo onderstaande verkeer scenario's.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbc6f-185">Kritieke toorealize dat niet u Hallo webserver rechtstreeks bereikt is.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="bbc6f-186">Wanneer een browser een HTTP-pagina van FrontEnd001.CloudApp.Net aanvraagt, webserver Hallo HTTP-eindpunt (poort 80) geeft dit verkeer toohello firewall niet Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="bbc6f-187">Hallo firewall vervolgens hierboven NAT's die toohello webserver aanvragen volgens regel toohello gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="bbc6f-188">Verkeer scenario 's</span><span class="sxs-lookup"><span data-stu-id="bbc6f-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="bbc6f-189">(Toegestaan) TooWeb Web Server via de Firewall</span><span class="sxs-lookup"><span data-stu-id="bbc6f-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="bbc6f-190">Internet aanvragen HTTP-gebruikerspagina van FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="bbc6f-191">Cloud-service geeft verkeer via open eindpunten op poort 80 toofirewall lokale interface op 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="bbc6f-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="bbc6f-192">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-193">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="bbc6f-194">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="bbc6f-195">NSG regel 3 (Internet tooFirewall) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bbc6f-196">Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="bbc6f-197">Regel voor doorsturen van de firewall Zie dit netwerkverkeer via de poort 80 is, stuurt het webserver toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="bbc6f-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="bbc6f-198">IIS01 luistert voor internetverkeer, ontvangt deze aanvraag en begint met de verwerking van Hallo-aanvraag</span><span class="sxs-lookup"><span data-stu-id="bbc6f-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="bbc6f-199">IIS01 vraagt Hallo SQL Server op AppVM01 voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="bbc6f-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="bbc6f-200">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="bbc6f-201">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-202">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="bbc6f-203">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="bbc6f-204">NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="bbc6f-205">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="bbc6f-206">AppVM01 ontvangen Hallo SQL-Query en beantwoord</span><span class="sxs-lookup"><span data-stu-id="bbc6f-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="bbc6f-207">Omdat er geen uitgaande regels op Hallo antwoord Hallo van back-end-subnet is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="bbc6f-208">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="bbc6f-209">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="bbc6f-210">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="bbc6f-211">Hallo SQL antwoord wordt ontvangen en Hallo HTTP-antwoord is voltooid en toohello aanvrager verzendt Hallo IIS-server</span><span class="sxs-lookup"><span data-stu-id="bbc6f-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="bbc6f-212">Aangezien dit een NAT-sessie van de firewall hello, is Hallo antwoord bestemming (in eerste instantie) voor Hallo Firewall</span><span class="sxs-lookup"><span data-stu-id="bbc6f-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="bbc6f-213">Hallo firewall antwoord Hallo ontvangt van Hallo webserver en stuurt back toohello Internet-gebruiker</span><span class="sxs-lookup"><span data-stu-id="bbc6f-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="bbc6f-214">Omdat er geen uitgaande regels op Hallo Frontend subnet Hallo antwoord is toegestaan en Hallo Internet-gebruiker ontvangt Hallo webpagina aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="bbc6f-215">(Toegestaan) RDP-tooBackend</span><span class="sxs-lookup"><span data-stu-id="bbc6f-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="bbc6f-216">RDP-sessie tooAppVM01 op BackEnd001.CloudApp.Net:xxxxx waarbij xxxxx Hallo willekeurig toegewezen poort voor RDP tooAppVM01 is serverbeheerder op internet-aanvragen (Hallo toegewezen poort kan worden gevonden op Hallo Azure Portal of via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="bbc6f-217">Sinds Hallo die Hallo FrontEnd001.CloudApp.Net adres alleen Firewall luistert, is niet verbonden met dit netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="bbc6f-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="bbc6f-218">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-219">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="bbc6f-220">NSG regel 2 (RDP) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bbc6f-221">Er is geen uitgaande regels standaardregels toepassen en terugkerend verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="bbc6f-222">RDP-sessie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="bbc6f-222">RDP session is enabled</span></span>
6. <span data-ttu-id="bbc6f-223">AppVM01 gebruikersnaam wachtwoord gevraagd</span><span class="sxs-lookup"><span data-stu-id="bbc6f-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="bbc6f-224">(Toegestaan) Web Server DNS-lookup op DNS-server</span><span class="sxs-lookup"><span data-stu-id="bbc6f-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="bbc6f-225">Web-Server, IIS01, moeten een gegevensfeed op www.data.gov, maar moet tooresolve Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="bbc6f-226">Hallo netwerkconfiguratie voor Hallo VNet lijsten DNS01 (10.0.2.4 op Hallo back-end subnet) als het primaire DNS-server hello, IIS01 verzendt Hallo DNS-aanvraag tooDNS01</span><span class="sxs-lookup"><span data-stu-id="bbc6f-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="bbc6f-227">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="bbc6f-228">Subnet backend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-229">NSG regel 1 (DNS) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="bbc6f-230">DNS-server ontvangt Hallo aanvraag</span><span class="sxs-lookup"><span data-stu-id="bbc6f-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="bbc6f-231">DNS-server heeft geen Hallo-adres in de cache opgeslagen en wordt u gevraagd een basis-DNS-server op Hallo internet</span><span class="sxs-lookup"><span data-stu-id="bbc6f-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="bbc6f-232">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="bbc6f-233">Internet-DNS-server reageert, omdat deze sessie is gestart, intern, is antwoord Hallo toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="bbc6f-234">DNS-server in de cache opgeslagen antwoord Hallo en toohello eerste aanvraag back tooIIS01 reageert</span><span class="sxs-lookup"><span data-stu-id="bbc6f-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="bbc6f-235">Er is geen uitgaande regels op subnet Backend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="bbc6f-236">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="bbc6f-237">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="bbc6f-238">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan dus Hallo verkeer is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="bbc6f-239">IIS01 ontvangt antwoord Hallo van DNS01</span><span class="sxs-lookup"><span data-stu-id="bbc6f-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="bbc6f-240">(Toegestaan) Web Server toegang tot bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="bbc6f-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="bbc6f-241">IIS01 vraagt om een bestand op AppVM01</span><span class="sxs-lookup"><span data-stu-id="bbc6f-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="bbc6f-242">Er is geen uitgaande regels op subnet Frontend verkeer wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="bbc6f-243">Hallo back-end subnet begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-244">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="bbc6f-245">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="bbc6f-246">NSG regel 3 (Internet tooFirewall) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="bbc6f-247">NSG regel 4 (IIS01 tooAppVM01) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bbc6f-248">AppVM01 hello aanvraag ontvangt en reageert met bestand (ervan uitgaande dat toegang wordt geverifieerd)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="bbc6f-249">Omdat er geen uitgaande regels op Hallo antwoord Hallo van back-end-subnet is toegestaan</span><span class="sxs-lookup"><span data-stu-id="bbc6f-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="bbc6f-250">Subnet frontend begint verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-251">Er is geen NSG-regel die van toepassing tooInbound verkeer van Hallo back-end subnet toohello Frontend subnet, is zodat geen van Hallo NSG-regels toepassen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="bbc6f-252">Hallo system standaardregel verkeer tussen subnetten zou dit verkeer toestaan zodat Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="bbc6f-253">Hallo IIS server ontvangt Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="bbc6f-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="bbc6f-254">(Geweigerd) Web direct tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="bbc6f-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="bbc6f-255">Sinds Hallo webserver, IIS01 en Hallo Firewall zijn in Hallo dezelfde Cloudservice ze delen Hallo dezelfde openbare internetgerichte IP-adres.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="bbc6f-256">Dus HTTP-verkeer zou worden omgeleid toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="bbc6f-257">Tijdens het Hallo-aanvraag zou met succes worden geleverd, deze kan niet gaat u rechtstreeks toohello webserver, die wordt doorgegeven, die is ontworpen, via Hallo Firewall eerst.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="bbc6f-258">Zie Hallo eerste Scenario in dit gedeelte voor het Hallo-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="bbc6f-259">(Geweigerd) TooBackend Web Server</span><span class="sxs-lookup"><span data-stu-id="bbc6f-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="bbc6f-260">Internet-gebruiker probeert een bestand op AppVM01 via Hallo BackEnd001.CloudApp.Net service tooaccess</span><span class="sxs-lookup"><span data-stu-id="bbc6f-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="bbc6f-261">Aangezien er geen eindpunten voor de bestandsshare is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="bbc6f-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="bbc6f-262">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, wordt NSG regel 5 (Internet tooVNet) dit verkeer geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="bbc6f-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="bbc6f-263">(Geweigerd) Web DNS-zoekopdracht op DNS-server</span><span class="sxs-lookup"><span data-stu-id="bbc6f-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="bbc6f-264">Internet-gebruiker probeert een interne DNS-record op DNS01 via Hallo BackEnd001.CloudApp.Net service toolookup</span><span class="sxs-lookup"><span data-stu-id="bbc6f-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="bbc6f-265">Aangezien er geen eindpunten voor DNS is geopend zijn, dit zou niet Hallo Cloudservice doorgeven en wouldn't Hallo-server niet bereiken</span><span class="sxs-lookup"><span data-stu-id="bbc6f-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="bbc6f-266">Als het Hallo-eindpunten zijn geopend voor een bepaalde reden, NSG regel 5 (Internet tooVNet) dit verkeer wordt geblokkeerd (Opmerking: deze regel 1 (DNS) is niet van toepassing om twee redenen, eerste Hallo-bronadres is internet Hallo, deze regel is alleen van toepassing toohello lokale VNet als Hallo bron ook Dit is een regel voor toestaan, zodat deze zou nooit verkeer weigeren)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="bbc6f-267">(Geweigerd) TooSQL webtoegang via Firewall</span><span class="sxs-lookup"><span data-stu-id="bbc6f-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="bbc6f-268">Internet-gebruiker opvraagt SQL-gegevens uit FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="bbc6f-269">Aangezien er geen eindpunten geopend voor SQL zijn, dit zou Hallo Cloudservice niet doorgeven en Hallo firewall wouldn't bereiken</span><span class="sxs-lookup"><span data-stu-id="bbc6f-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="bbc6f-270">Als eindpunten geopend voor een bepaalde reden zijn, begint Hallo Frontend subnet verwerking van inkomende regel:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bbc6f-271">NSG regel 1 (DNS) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="bbc6f-272">NSG regel 2 (RDP) niet van toepassing, toonext regel verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="bbc6f-273">NSG-regel 2 (Internet tooFirewall) is van toepassing, -verkeer is toegestaan, zelfs niet meer regelverwerking</span><span class="sxs-lookup"><span data-stu-id="bbc6f-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bbc6f-274">Verkeer komt binnen via interne IP-adres van Hallo firewall (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="bbc6f-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="bbc6f-275">Firewall heeft geen regels doorsturen voor SQL en verwijdert Hallo verkeer</span><span class="sxs-lookup"><span data-stu-id="bbc6f-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="bbc6f-276">Conclusie</span><span class="sxs-lookup"><span data-stu-id="bbc6f-276">Conclusion</span></span>
<span data-ttu-id="bbc6f-277">Dit is een relatief eenvoudig en duidelijk van het beveiligen van uw toepassing met een firewall en Hallo back-end subnet uit binnenkomend verkeer isoleren.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="bbc6f-278">Meer voorbeelden en een overzicht van het netwerk beveiligingsgrenzen vindt [hier][HOME].</span><span class="sxs-lookup"><span data-stu-id="bbc6f-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="bbc6f-279">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="bbc6f-280">Belangrijkste Script en netwerkconfiguratie</span><span class="sxs-lookup"><span data-stu-id="bbc6f-280">Main Script and Network Config</span></span>
<span data-ttu-id="bbc6f-281">Hallo volledige Script opslaat in een PowerShell-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="bbc6f-282">Sla Hallo netwerkconfiguratie naar een bestand met de naam 'NetworkConf2.xml'.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="bbc6f-283">Hallo door de gebruiker gedefinieerde variabelen zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="bbc6f-284">Hallo-script uitvoeren en volg Hallo Firewall regel setup instructies hierboven.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="bbc6f-285">Volledige Script</span><span class="sxs-lookup"><span data-stu-id="bbc6f-285">Full Script</span></span>
<span data-ttu-id="bbc6f-286">Dit script wordt, op basis van Hallo door de gebruiker gedefinieerde variabelen:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="bbc6f-287">Verbinding maken met tooan Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="bbc6f-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="bbc6f-288">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="bbc6f-288">Create a new storage account</span></span>
3. <span data-ttu-id="bbc6f-289">Maak een nieuw VNet en twee subnets zoals gedefinieerd in het configuratiebestand voor Hallo netwerk</span><span class="sxs-lookup"><span data-stu-id="bbc6f-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="bbc6f-290">4 windows server-VM's maken</span><span class="sxs-lookup"><span data-stu-id="bbc6f-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="bbc6f-291">Configureer het NSG inclusief:</span><span class="sxs-lookup"><span data-stu-id="bbc6f-291">Configure NSG including:</span></span>
   * <span data-ttu-id="bbc6f-292">Maken van een NSG</span><span class="sxs-lookup"><span data-stu-id="bbc6f-292">Creating a NSG</span></span>
   * <span data-ttu-id="bbc6f-293">Met regels in te vullen</span><span class="sxs-lookup"><span data-stu-id="bbc6f-293">Populating it with rules</span></span>
   * <span data-ttu-id="bbc6f-294">Binding Hallo NSG toohello juiste subnetten</span><span class="sxs-lookup"><span data-stu-id="bbc6f-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="bbc6f-295">Deze PowerShell-script moet lokaal op worden uitgevoerd dat een internet verbonden PC of de server.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbc6f-296">Wanneer dit script wordt uitgevoerd, kunnen er waarschuwingen of andere informatieve berichten die pop in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="bbc6f-297">Alleen foutberichten in rood zijn aanleiding.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="bbc6f-298">Netwerk-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="bbc6f-298">Network Config File</span></span>
<span data-ttu-id="bbc6f-299">Dit xml-bestand opslaan met bijgewerkte locatie en voeg Hallo koppeling toothis toohello $NetworkConfigFile variabele in bovenstaande Hallo-script bestand.</span><span class="sxs-lookup"><span data-stu-id="bbc6f-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="bbc6f-300">Voorbeeldscripts toepassing</span><span class="sxs-lookup"><span data-stu-id="bbc6f-300">Sample Application Scripts</span></span>
<span data-ttu-id="bbc6f-301">Als u een voorbeeldtoepassing tooinstall voor deze en andere voorbeelden van het Perimeternetwerk wilt, een is opgegeven op de koppeling Hallo: [voorbeeldscript toepassing][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="bbc6f-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inkomende DMZ met NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Bestemming NAT-pictogram"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewallregel"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activering van de firewall-regel"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
