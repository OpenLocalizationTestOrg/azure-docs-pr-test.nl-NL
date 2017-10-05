---
title: Persoonlijke gegevens beschermen met Azure-netwerkbeveiligingsfuncties | Microsoft Docs
description: Persoonlijke gegevens beschermen met beveiligingsfuncties van Azure-netwerk
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: b7a6343f37f890b65d9536eac34e1069d24ad97e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="d45df-103">Persoonlijke gegevens beschermen met netwerkbeveiligingsfuncties: Azure Application Gateway en Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="d45df-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="d45df-104">Dit artikel bevat informatie en procedures waarmee u Azure Application Gateway en Netwerkbeveiligingsgroepen gebruiken om persoonlijke gegevens te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="d45df-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups to protect personal data.</span></span>

<span data-ttu-id="d45df-105">Een belangrijk aspect vormt in een meerlaagse beveiligingsstrategie om de privacy van persoonlijke gegevens te beschermen, is een beveiliging tegen misbruik van algemene beveiligingsproblemen zoals SQL-injectie of cross-site scripting.</span><span class="sxs-lookup"><span data-stu-id="d45df-105">An important element in a multi-layered security strategy to protect the privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="d45df-106">Ongewenste netwerkverkeer buiten uw Azure virtual network beschermt tegen mogelijke inbreuk op gevoelige gegevens, en houden Microsoft Azure biedt u hulpprogramma's om u te helpen uw gegevens beschermen tegen kwaadwillende personen.</span><span class="sxs-lookup"><span data-stu-id="d45df-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools to help protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="d45df-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="d45df-107">Scenario</span></span>

<span data-ttu-id="d45df-108">Een bedrijf grote cruise, gevestigd in de Verenigde Staten, aanvullende bewerkingen voor het bieden van routes in de Middellandse, Adriatische, Baltische veiligheid ook Florida.</span><span class="sxs-lookup"><span data-stu-id="d45df-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="d45df-109">Ter bevordering van deze inspanningen is die is verkregen meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en het Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="d45df-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="d45df-110">Het bedrijf gebruikmaakt van Microsoft Azure worden bedrijfsgegevens opgeslagen in de cloud en toepassingen worden uitgevoerd op virtuele machines die worden verwerkt en toegang tot deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="d45df-110">The company uses Microsoft Azure to store corporate data in the cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="d45df-111">Deze gegevens omvatten persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase.</span><span class="sxs-lookup"><span data-stu-id="d45df-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="d45df-112">Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="d45df-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="d45df-113">De regel cruise onderhoudt ook een grote database van derden en loyaliteit programma leden met persoonlijke gegevens voor de relaties met de huidige en eerdere klanten bijhouden.</span><span class="sxs-lookup"><span data-stu-id="d45df-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="d45df-114">Zakelijke werknemers toegang tot het netwerk van het bedrijf externe kantoren en reizen agents over de hele wereld toegang hebben tot een aantal bedrijfsresources en webtoepassingen die worden gehost in Azure VM's gebruiken om te communiceren met het.</span><span class="sxs-lookup"><span data-stu-id="d45df-114">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources and use web-based applications hosted in Azure VMs to interact with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d45df-115">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="d45df-115">Problem statement</span></span>

<span data-ttu-id="d45df-116">Het bedrijf dient de privacy van klanten te beschermen en persoonlijke gegevens van de werknemers van aanvallers die gebruikmaken van beveiligingsproblemen om uit te voeren schadelijke code die persoonlijke gegevens worden namelijk blootgesteld software opgeslagen of gebruikt door het bedrijf cloud-gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d45df-116">The company must protect the privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities to run malicious code that could expose personal data stored or used by the company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="d45df-117">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="d45df-117">Company goal</span></span>

<span data-ttu-id="d45df-118">Het doel van het bedrijf om ervoor te zorgen dat onbevoegden geen toegang tot zakelijke Azure Virtual Networks en de toepassingen en gegevens die door misbruik van veelvoorkomende beveiligingslekken in staan.</span><span class="sxs-lookup"><span data-stu-id="d45df-118">The company’s goal to ensure that unauthorized persons cannot access corporate Azure Virtual Networks and the applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="d45df-119">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="d45df-119">Solutions</span></span>

<span data-ttu-id="d45df-120">Microsoft Azure biedt beveiligingsmethoden om te voorkomen dat ongewenste verkeer Azure Virtual Networks invoeren.</span><span class="sxs-lookup"><span data-stu-id="d45df-120">Microsoft Azure provides security mechanisms to help prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="d45df-121">Beheer van binnenkomende en uitgaande verkeer wordt normaal uitgevoerd door firewalls.</span><span class="sxs-lookup"><span data-stu-id="d45df-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="d45df-122">In Azure, kunt u de toepassingsgateway met de Web Application Firewall en de Netwerkbeveiligingsgroep groepen (NSG), die als een eenvoudige gedistribueerde firewall fungeren.</span><span class="sxs-lookup"><span data-stu-id="d45df-122">In Azure, you can use the Application Gateway with the Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="d45df-123">Deze hulpprogramma's kunnen u detecteren en blokkeren van ongewenste netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="d45df-123">These tools enable you to detect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="d45df-124">Application Gateway of Web Application Firewall</span><span class="sxs-lookup"><span data-stu-id="d45df-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="d45df-125">De [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF)-onderdeel van de [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) webtoepassingen zijn steeds meer doelen van aanvallen die gebruikmaken van algemene bekende beveiligt beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="d45df-125">The [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of the [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="d45df-126">Een gecentraliseerde WAF wordt beschermd tegen aanvallen via Internet door en beveiligingsbeheer zonder eventuele wijzigingen in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d45df-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="d45df-127">Azure WAF adressen verschillende aanval categorieën inclusief SQL-injectie, cross-site scripting schendingen van HTTP-protocol en afwijkingen, bots, crawlers, scanners, veelvoorkomende onvolkomenheden in de toepassing, HTTP-Denial of Service en andere algemene aanvallen, zoals het invoegen van de opdracht HTTP-aanvraag ' smokkelen ', HTTP-antwoord splitsen en extern bestand insluiting aanvallen.</span><span class="sxs-lookup"><span data-stu-id="d45df-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="d45df-128">U kunt een toepassingsgateway maken met WAF of WAF toevoegen aan een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d45df-128">You can create an application gateway with WAF, or add WAF to an existing application gateway.</span></span> <span data-ttu-id="d45df-129">Azure Application Gateway vereist in beide gevallen moet een eigen subnet.</span><span class="sxs-lookup"><span data-stu-id="d45df-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="d45df-130">Hoe maak ik een toepassingsgateway met WAF?</span><span class="sxs-lookup"><span data-stu-id="d45df-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="d45df-131">Als een nieuwe toepassingsgateway maken met WAF ingeschakeld, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="d45df-131">To create a new application gateway with WAF enabled, do the following:</span></span>

1. <span data-ttu-id="d45df-132">Aanmelden bij de Azure portal en in de **Favorieten** deelvenster van de portal klikt u op **nieuw**</span><span class="sxs-lookup"><span data-stu-id="d45df-132">Log in to the Azure portal and in the **Favorites** pane of the portal, click **New**</span></span>

2. <span data-ttu-id="d45df-133">Klik op de blade **Nieuw** op **Netwerken**.</span><span class="sxs-lookup"><span data-stu-id="d45df-133">In the **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="d45df-134">Klik op **toepassingsgateway**.</span><span class="sxs-lookup"><span data-stu-id="d45df-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="d45df-135">Navigeer naar de Azure-portal **klikt u op nieuw \> Networking \> Application Gateway.**</span><span class="sxs-lookup"><span data-stu-id="d45df-135">Navigate to the Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![Toepassingsgateways maken](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="d45df-137">In de **basisbeginselen** blade die wordt weergegeven, geef de waarden voor de volgende velden: naam, laag SKU (Standard of WAF)-grootte (klein, middelgroot of groot), aantal (2 voor hoge beschikbaarheid)-instantie abonnement, resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="d45df-137">In the **Basics** blade that appears, enter the values for the following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="d45df-138">In de **instellingen** blade die wordt weergegeven onder **virtueel netwerk**, klikt u op **Kies een virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="d45df-138">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="d45df-139">Deze stap wordt geopend, voer de blade van het virtueel netwerk kiezen.</span><span class="sxs-lookup"><span data-stu-id="d45df-139">This step opens enter the Choose virtual network blade.</span></span>

7. <span data-ttu-id="d45df-140">Klik op **nieuw** openen de **virtueel netwerk maken** blade.</span><span class="sxs-lookup"><span data-stu-id="d45df-140">Click **Create new** to open the **Create virtual network** blade.</span></span>

8. <span data-ttu-id="d45df-141">Voer de volgende waarden: naam, de adresruimte, subnetnaam, adres-subnetbereik.</span><span class="sxs-lookup"><span data-stu-id="d45df-141">Enter the following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="d45df-142">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d45df-142">Click **OK**.</span></span>

9. <span data-ttu-id="d45df-143">Op de **instellingen** blade onder **Frontend IP-configuratie**, kies het type IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d45df-143">On the **Settings** blade under **Frontend IP configuration**, choose the IP address type.</span></span>

10. <span data-ttu-id="d45df-144">Klik op **Kies een openbaar IP-adres** vervolgens **nieuwe maken.**</span><span class="sxs-lookup"><span data-stu-id="d45df-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="d45df-145">De standaardwaarde accepteren en klik op **OK.**</span><span class="sxs-lookup"><span data-stu-id="d45df-145">Accept the default value, and click **OK.**</span></span>

12. <span data-ttu-id="d45df-146">Op de **instellingen** blade onder **listenerconfiguratie**, selecteer het gebruik van HTTP of HTTPS onder **Protocol**.</span><span class="sxs-lookup"><span data-stu-id="d45df-146">On the **Settings** blade under **Listener configuration**, select to use HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="d45df-147">Er is een certificaat vereist voor het gebruik van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d45df-147">To use HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="d45df-148">Configureer de specifieke instellingen WAF: **Firewall-status** (**ingeschakeld**) en **firewallmodus** (**preventie**).</span><span class="sxs-lookup"><span data-stu-id="d45df-148">Configure the WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="d45df-149">Als u ervoor kiest **detectie** als de modus, wordt alleen verkeer vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="d45df-149">If you choose **Detection** as the mode, traffic is only logged.</span></span>

14. <span data-ttu-id="d45df-150">Controleer de **samenvatting** pagina en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d45df-150">Review the **Summary** page and click **OK**.</span></span> <span data-ttu-id="d45df-151">De toepassingsgateway is nu in de wachtrij geplaatst en gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d45df-151">Now the application gateway is queued up and created.</span></span>

<span data-ttu-id="d45df-152">Nadat de toepassingsgateway is gemaakt, kunt u navigeren naar het in de portal en gaan met de configuratie van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="d45df-152">After the application gateway has been created, you can navigate to it in the portal and continue configuration of the application gateway.</span></span>

![gemaakte toepassingsgateway](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-to-an-existing-application"></a><span data-ttu-id="d45df-154">Hoe kan ik WAF naar een bestaande toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="d45df-154">How do I add WAF to an existing application?</span></span>

<span data-ttu-id="d45df-155">Voor het bijwerken van een bestaande toepassingsgateway ter ondersteuning van WAF in de modus voor preventie van het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="d45df-155">To update an existing application gateway to support WAF in prevention mode, do the following:</span></span>

1. <span data-ttu-id="d45df-156">Klik in het deelvenster **Favorieten** van Azure Portal op **Alle resources**.</span><span class="sxs-lookup"><span data-stu-id="d45df-156">In the Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="d45df-157">Klik op de bestaande toepassingsgateway in de **alle resources** blade.</span><span class="sxs-lookup"><span data-stu-id="d45df-157">Click the existing Application Gateway in the **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="d45df-158">Opmerking: Als het abonnement dat u hebt geselecteerd al verschillende bronnen heeft, kunt u de naam in het Filter met de naam...</span><span class="sxs-lookup"><span data-stu-id="d45df-158">Note: If the subscription you selected already has several resources in it, you can enter the name in the Filter by name…</span></span> <span data-ttu-id="d45df-159">voor eenvoudige toegang tot de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="d45df-159">box to easily access the DNS zone.</span></span>
3. <span data-ttu-id="d45df-160">Klik op **Web application firewall** en de instellingen voor de toepassingsgateway bijwerken: **upgraden naar de laag WAF** (ingeschakeld) **Firewall-status** (ingeschakeld)  **Firewallmodus** (preventie).</span><span class="sxs-lookup"><span data-stu-id="d45df-160">Click **Web application firewall** and update the application gateway settings: **Upgrade to WAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="d45df-161">U moet ook de regelinstellingen configureren en uitgeschakelde regels configureren.</span><span class="sxs-lookup"><span data-stu-id="d45df-161">You also need to configure the rule set, and configure disabled rules.</span></span>

<span data-ttu-id="d45df-162">Zie voor meer gedetailleerde informatie over het maken van een nieuwe toepassingsgateway met WAF en WAF toevoegen aan een bestaande toepassingsgateway [een toepassingsgateway maken met web application firewall via de portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span><span class="sxs-lookup"><span data-stu-id="d45df-162">For more detailed information on how to create a new application gateway with WAF and how to add WAF to an existing application gateway, see [Create an application gateway with web application firewall by using the portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="d45df-163">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="d45df-163">Network Security Groups</span></span>

<span data-ttu-id="d45df-164">Een [netwerkbeveiligingsgroep](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) bevat een lijst met regels voor toestaan of weigeren van netwerkverkeer naar bronnen die zijn verbonden met [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span><span class="sxs-lookup"><span data-stu-id="d45df-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic to resources connected to [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="d45df-165">Nsg's kunnen worden gekoppeld aan subnetten of afzonderlijke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d45df-165">NSGs can be associated to subnets or individual VMs.</span></span> <span data-ttu-id="d45df-166">Wanneer een NSG is gekoppeld aan een subnet, zijn de regels van toepassing op alle resources die zijn verbonden met het subnet.</span><span class="sxs-lookup"><span data-stu-id="d45df-166">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> <span data-ttu-id="d45df-167">Verkeer kan verder worden beperkt door ook een NSG te koppelen aan een VM of NIC.</span><span class="sxs-lookup"><span data-stu-id="d45df-167">Traffic can further be restricted by also associating an NSG to a VM or NIC.</span></span>

<span data-ttu-id="d45df-168">Nsg's bevatten vier eigenschappen: naam, regio, resourcegroep en regels.</span><span class="sxs-lookup"><span data-stu-id="d45df-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="d45df-169">Hoewel een NSG bestaat in een resourcegroep, kan deze worden gekoppeld aan resources in elke willekeurige resourcegroep, mits de resource tot dezelfde Azure-regio als de NSG behoort.</span><span class="sxs-lookup"><span data-stu-id="d45df-169">Although an NSG exists in a resource group, it can be associated to resources in any resource group, as long as the resource is part of the same Azure region as the NSG.</span></span>

<span data-ttu-id="d45df-170">NSG-regels negen eigenschappen bevatten: naam, het Protocol (TCP, UDP of \*, waaronder ICMP als UDP en TCP), bron poortbereik, doelpoortbereik, bronadres voorvoegsel, doel-adresvoorvoegsel, richting (inkomend of uitgaand), () prioriteit tussen 100 en 4096) en toegang tot type (toestaan of weigeren).</span><span class="sxs-lookup"><span data-stu-id="d45df-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="d45df-171">Alle nsg's bevatten een set met standaardregels die kan worden verwijderd of overschreven door de regels die u maakt.</span><span class="sxs-lookup"><span data-stu-id="d45df-171">All NSGs contain a set of default rules that can be deleted, or overridden by the rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="d45df-172">Hoe ik nsg's implementeren?</span><span class="sxs-lookup"><span data-stu-id="d45df-172">How do I implement NSGs?</span></span>

<span data-ttu-id="d45df-173">Nsg's implementeert vereist plannen en er zijn verschillende ontwerpoverwegingen, u moet rekening te houden.</span><span class="sxs-lookup"><span data-stu-id="d45df-173">Implementing NSGs requires planning, and there are several design considerations you need to take into account.</span></span> <span data-ttu-id="d45df-174">Deze omvatten beperkingen met betrekking tot het aantal nsg's per abonnement en -regels per NSG; 'S VNet en subnetten ontwerpen, speciale regels, ICMP-verkeer, isolatie van lagen met subnetten, load balancers en meer.</span><span class="sxs-lookup"><span data-stu-id="d45df-174">These include limits on the number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="d45df-175">Zie voor meer richtlijnen bij het plannen en implementeren van nsg's en een voorbeeld implementatiescenario [filteren van netwerkverkeer met netwerkbeveiligingsgroepen.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span><span class="sxs-lookup"><span data-stu-id="d45df-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="d45df-176">Hoe maak ik regels in een NSG</span><span class="sxs-lookup"><span data-stu-id="d45df-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="d45df-177">U maakt regels voor binnenkomende verbindingen in een bestaande NSG door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="d45df-177">To create inbound rules in an existing NSG, do the following:</span></span>

1. <span data-ttu-id="d45df-178">Klik op **Bladeren**, en vervolgens **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="d45df-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="d45df-179">Klik in de lijst van nsg's op **NSG-FrontEnd**, en vervolgens **inkomende beveiligingsregels voor verbindingen.**</span><span class="sxs-lookup"><span data-stu-id="d45df-179">In the list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="d45df-180">Klik in de lijst met regels voor binnenkomend verkeer op **toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="d45df-180">In the list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="d45df-181">Geef de waarden in de volgende velden: naam, prioriteit, bron, Protocol, bron-bereik, bestemming bestemming poortbereik en in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="d45df-181">Enter the values in the following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="d45df-182">De nieuwe regel wordt weergegeven in de NSG na enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="d45df-182">The new rule will appear in the NSG after a few seconds.</span></span>

![netwerkbeveiligingsregels](media/protect-netsec/inbound-security.png)

<span data-ttu-id="d45df-184">Zie voor meer instructies voor het nsg's maken in subnetten, regels maken en een NSG koppelen aan een subnet front-end en back-end [netwerkbeveiligingsgroepen met de Azure portal maken.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span><span class="sxs-lookup"><span data-stu-id="d45df-184">For more instructions on how to create NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using the Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d45df-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d45df-185">Next steps</span></span>

[<span data-ttu-id="d45df-186">Azure-netwerkbeveiliging</span><span class="sxs-lookup"><span data-stu-id="d45df-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="d45df-187">Aanbevolen beveiligingsprocedures voor Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="d45df-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="d45df-188">Informatie over een netwerkbeveiligingsgroep ophalen</span><span class="sxs-lookup"><span data-stu-id="d45df-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="d45df-189">Web application firewall (WAF)</span><span class="sxs-lookup"><span data-stu-id="d45df-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
