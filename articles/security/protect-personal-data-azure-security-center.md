---
title: Persoonlijke gegevens beschermen met Azure Security Center | Microsoft Docs
description: beveiligen van persoonlijke gegevens met Azure security center
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
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="a5074-103">Persoonlijke gegevens beschermen tegen aanvallen en inbreuken op: Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a5074-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="a5074-104">In dit artikel helpt u begrijpen hoe Azure Security Center persoonlijke gegevens beveiligen tegen aanvallen en inbreuken op.</span><span class="sxs-lookup"><span data-stu-id="a5074-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="a5074-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="a5074-105">Scenario</span></span> 

<span data-ttu-id="a5074-106">Een bedrijf grote cruise, gevestigd in de Verenigde Staten, aanvullende bewerkingen voor het bieden van routes in de Middellandse en Baltische veiligheid, evenals Florida.</span><span class="sxs-lookup"><span data-stu-id="a5074-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="a5074-107">Om te helpen bij deze inspanningen, heeft die is verkregen meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en het Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="a5074-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="a5074-108">Het bedrijf gebruikmaakt van Microsoft Azure voor het opslaan van bedrijfsgegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="a5074-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="a5074-109">Dit omvat persoonlijk identificeerbare informatie zoals namen, adressen, telefoonnummers en creditcardgegevens.</span><span class="sxs-lookup"><span data-stu-id="a5074-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="a5074-110">Het bevat ook informatie Human Resources, zoals:</span><span class="sxs-lookup"><span data-stu-id="a5074-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="a5074-111">Adressen</span><span class="sxs-lookup"><span data-stu-id="a5074-111">Addresses</span></span>
- <span data-ttu-id="a5074-112">telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="a5074-112">Phone numbers</span></span>
- <span data-ttu-id="a5074-113">BTW-id 's</span><span class="sxs-lookup"><span data-stu-id="a5074-113">Tax identification numbers</span></span>
- <span data-ttu-id="a5074-114">medische informatie</span><span class="sxs-lookup"><span data-stu-id="a5074-114">Medical information</span></span>

<span data-ttu-id="a5074-115">De regel cruise onderhoudt ook een grote database van derden en loyaliteit voor leden.</span><span class="sxs-lookup"><span data-stu-id="a5074-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="a5074-116">Zakelijke werknemers toegang tot het netwerk van het bedrijf externe kantoren en reizen agents over de hele wereld hebben toegang tot een aantal bedrijfsresources.</span><span class="sxs-lookup"><span data-stu-id="a5074-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="a5074-117">Persoonlijke gegevens verzonden via het netwerk tussen deze locaties en het Microsoft-datacentrum.</span><span class="sxs-lookup"><span data-stu-id="a5074-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a5074-118">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="a5074-118">Problem statement</span></span>

<span data-ttu-id="a5074-119">Het bedrijf maakt zich zorgen over de bedreiging van aanvallen op Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a5074-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="a5074-120">Ze willen blootstelling van werknemers en klanten persoonlijke gegevens te voorkomen dat onbevoegden.</span><span class="sxs-lookup"><span data-stu-id="a5074-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="a5074-121">Ze willen richtlijnen op zowel voorkomen en antwoord/herstel, evenals een effectieve manier voor het bewaken van de actieve beveiliging van hun cloudbronnen.</span><span class="sxs-lookup"><span data-stu-id="a5074-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="a5074-122">Ze moeten een sterke line-of beveiliging tegen kwaadwillende personen de hedendaagse geavanceerde en geordend.</span><span class="sxs-lookup"><span data-stu-id="a5074-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a5074-123">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="a5074-123">Company goal</span></span>

<span data-ttu-id="a5074-124">Een van de doelstellingen van het bedrijf is om te garanderen dat de privacy van klanten en werknemers persoonlijke gegevens te beveiligen tegen bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="a5074-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="a5074-125">Een van hun doelstellingen is onmiddellijk reageren op tekenen van inbreuk op de impact helpen.</span><span class="sxs-lookup"><span data-stu-id="a5074-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="a5074-126">Is er een manier om te beoordelen van de huidige status van de beveiliging, kwetsbaar configuraties te identificeren en ze herstellen.</span><span class="sxs-lookup"><span data-stu-id="a5074-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="a5074-127">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="a5074-127">Solutions</span></span>

<span data-ttu-id="a5074-128">Microsoft Azure Security Center (ASC) biedt een geïntegreerde beveiliging en beleidsbeheer beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="a5074-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="a5074-129">Het biedt eenvoudig te gebruiken en effectieve bedreiging mogelijkheden voor preventie, detectie en reactie.</span><span class="sxs-lookup"><span data-stu-id="a5074-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="a5074-130">Preventie</span><span class="sxs-lookup"><span data-stu-id="a5074-130">Prevention</span></span>

<span data-ttu-id="a5074-131">ASC kunt u voorkomen dat schendingen doordat u beveiligingsbeleid instellen en implementeren van aanbevelingen voor beveiliging just-in-time-toegang bieden.</span><span class="sxs-lookup"><span data-stu-id="a5074-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="a5074-132">Een beveiligingsbeleid bepaalt welke set besturingselementen die worden aanbevolen voor resources binnen het opgegeven abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5074-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="a5074-133">Alleen bij het time-toegang kan worden gebruikt vergrendelen binnenkomend verkeer naar uw Azure VM's, blootstelling aan aanvallen te verminderen.</span><span class="sxs-lookup"><span data-stu-id="a5074-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="a5074-134">Aanbevelingen voor beveiliging worden gemaakt door ASC na het analyseren van de beveiligingsstatus van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a5074-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="a5074-135">Hoe Stel beleidsregels voor veiligheid in ASC?</span><span class="sxs-lookup"><span data-stu-id="a5074-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="a5074-136">U kunt voor elk abonnement beveiligingsbeleid configureren.</span><span class="sxs-lookup"><span data-stu-id="a5074-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="a5074-137">Het beveiligingsbeleid kan alleen worden gewijzigd door een eigenaar of bijdrager van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5074-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="a5074-138">In de Azure portal, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5074-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="a5074-139">Selecteer **beleid** in het dashboard ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="a5074-140">Selecteer het abonnement die u wilt inschakelen, het beleid.</span><span class="sxs-lookup"><span data-stu-id="a5074-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="a5074-141">Kies **preventiebeleid** configureren van beleid per abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5074-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="a5074-142">**Verzamel gegevens van virtuele machines** moet worden ingesteld op **op.**</span><span class="sxs-lookup"><span data-stu-id="a5074-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="a5074-143">In de **preventiebeleid** opties, dient u **op** om in te schakelen van de aanbevelingen voor beveiliging die relevant voor het abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="a5074-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="a5074-144">Zie voor meer gedetailleerde instructies en een uitleg van elk van de beleid-aanbevelingen die kunnen worden ingeschakeld, [beveiligingsbeleid instellen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="a5074-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="a5074-145">Hoe configureer ik Just in Time toegang (Just in time)?</span><span class="sxs-lookup"><span data-stu-id="a5074-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="a5074-146">Wanneer JIT is ingeschakeld, wordt in Security Center binnenkomend verkeer naar uw Azure VM's vergrendelt door het maken van een NSG-regel.</span><span class="sxs-lookup"><span data-stu-id="a5074-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="a5074-147">Selecteert u de poorten op de virtuele machine waarmee binnenkomend verkeer wordt worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="a5074-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="a5074-148">Voor het gebruik van JIT-toegang tot het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5074-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="a5074-149">Selecteer de **Just in time VM toegang tegel** op de blade ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="a5074-150">Selecteer de **aanbevolen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a5074-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="a5074-151">Onder **VMs**, selecteert u de virtuele machines die u wilt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a5074-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="a5074-152">Hiermee wordt het selectievakje naast een virtuele machine geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a5074-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="a5074-153">Selecteer **inschakelen JIT** op virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a5074-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="a5074-154">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a5074-154">Select **Save**.</span></span>

<span data-ttu-id="a5074-155">Vervolgens ziet u de standaardpoorten die ASC aanbeveelt wordt ingeschakeld voor JIT.</span><span class="sxs-lookup"><span data-stu-id="a5074-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="a5074-156">U kunt ook toevoegen en configureren van een nieuwe poort waarop u wilt de zojuist inschakelen in tijdoplossing.</span><span class="sxs-lookup"><span data-stu-id="a5074-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="a5074-157">De **Just in time VM toegang** tegel in het Beveiligingscentrum toont het aantal virtuele machines die zijn geconfigureerd voor JIT-toegang.</span><span class="sxs-lookup"><span data-stu-id="a5074-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="a5074-158">Ook ziet u het aantal goedgekeurde toegangsaanvragen in de afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="a5074-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="a5074-159">Voor instructies over hoe u dit doet, en aanvullende informatie over Just in Time-toegang, Zie [beheren via in de tijd toegang tot een virtuele machine.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="a5074-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="a5074-160">Hoe ik ASC beveiligingsaanbevelingen implementeren?</span><span class="sxs-lookup"><span data-stu-id="a5074-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="a5074-161">Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="a5074-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="a5074-162">Deze aanbevelingen begeleiden u bij het configureren van de benodigde besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="a5074-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="a5074-163">Selecteer de **aanbevelingen** tegel op het dashboard ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="a5074-164">Bekijk de aanbevelingen die worden weergegeven in een tabel waarin elke regel een aanbeveling vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="a5074-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="a5074-165">Filter aanbevelingen, selecteer **Filter** en selecteer de ernst en status waarden die u wilt zien.</span><span class="sxs-lookup"><span data-stu-id="a5074-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="a5074-166">Als u wilt verwijderen van een aanbeveling die niet van toepassing, kunt u met de rechtermuisknop op en selecteer **sluiten.**</span><span class="sxs-lookup"><span data-stu-id="a5074-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="a5074-167">Denk na over welke aanbeveling eerst moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="a5074-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="a5074-168">De aanbevelingen in volgorde van prioriteit toepassen.</span><span class="sxs-lookup"><span data-stu-id="a5074-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="a5074-169">Zie voor een lijst van mogelijke aanbevelingen en de zelfstudies over het toepassen van elk [aanbevelingen voor beveiliging in Azure Security Center beheren.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a5074-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="a5074-170">Detectie van en reactie</span><span class="sxs-lookup"><span data-stu-id="a5074-170">Detection and Response</span></span>

<span data-ttu-id="a5074-171">Detectie- en Ga samen als moet worden gereageerd zo snel mogelijk na een bedreiging wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="a5074-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="a5074-172">Detectie van dreigingen ASC werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het netwerk en verbonden partneroplossingen.</span><span class="sxs-lookup"><span data-stu-id="a5074-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="a5074-173">ASC kunt snel de detectiealgoritmen bijwerken als aanvallers release nieuwe en steeds meer geavanceerde aanvallen.</span><span class="sxs-lookup"><span data-stu-id="a5074-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="a5074-174">Zie voor meer informatie gedetailleerde over de werking van de detectie van dreigingen van ASC [Azure Security Center detectiemogelijkheden](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="a5074-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="a5074-175">Hoe ik beheren en reageren op beveiligingswaarschuwingen?</span><span class="sxs-lookup"><span data-stu-id="a5074-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="a5074-176">Een lijst met beveiligingswaarschuwingen wordt weergegeven in Security Center samen met de informatie die u nodig hebt om snel onderzoek te het probleem.</span><span class="sxs-lookup"><span data-stu-id="a5074-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="a5074-177">Security Center bevat ook aanbevelingen voor het herstellen van een aanval.</span><span class="sxs-lookup"><span data-stu-id="a5074-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="a5074-178">Voor het beheren van uw beveiligingswaarschuwingen, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5074-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="a5074-179">Selecteer de **beveiligingswaarschuwingen** -tegel in het dashboard ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="a5074-180">Hiermee worden de details voor elke waarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a5074-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="a5074-181">U kunt waarschuwingen op basis van datum, status en ernst filteren selecteren **Filter** en selecteer vervolgens de waarden die u wilt zien.</span><span class="sxs-lookup"><span data-stu-id="a5074-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="a5074-182">Om te reageren op een waarschuwing, selecteert u deze en lees de informatie in en selecteer de resource die is aangevallen.</span><span class="sxs-lookup"><span data-stu-id="a5074-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="a5074-183">In de **beschrijving** veld, ziet u informatie, zoals aanbevolen herstel.</span><span class="sxs-lookup"><span data-stu-id="a5074-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="a5074-184">Zie voor meer informatie over het reageren op beveiligingswaarschuwingen, [beheren en erop reageren beveiligingswaarschuwingen in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="a5074-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="a5074-185">Voor verdere hulp bij het onderzoeken van beveiligingswaarschuwingen het bedrijf ASC waarschuwingen kunt integreren met een eigen SIEM-oplossing met behulp van [Azure Log integratie](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="a5074-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="a5074-186">Hoe beheer ik beveiligingsincidenten?</span><span class="sxs-lookup"><span data-stu-id="a5074-186">How do I manage security incidents?</span></span>

<span data-ttu-id="a5074-187">In ASC is een beveiligingsincident voordoet een aggregatie van alle waarschuwingen voor een resource uitgelijnd met de kill-keten patronen.</span><span class="sxs-lookup"><span data-stu-id="a5074-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="a5074-188">Een incident zal de lijst van gerelateerde waarschuwingen tonen, zodat u meer info krijgt over elke gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="a5074-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="a5074-189">Incidenten worden weergegeven in de tegel beveiligingswaarschuwingen en de blade.</span><span class="sxs-lookup"><span data-stu-id="a5074-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="a5074-190">Om te bekijken en beheren van beveiligingsincidenten, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5074-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="a5074-191">Selecteer de **beveiligingswaarschuwingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="a5074-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="a5074-192">Als een beveiligingsincident voordoet wordt gedetecteerd, wordt weergegeven onder de grafiek security-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="a5074-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="a5074-193">Er is een pictogram dat verschilt van andere waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="a5074-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="a5074-194">Selecteer het incident voor meer informatie over deze beveiligingsincident voordoet.</span><span class="sxs-lookup"><span data-stu-id="a5074-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="a5074-195">Aanvullende informatie bevatten een volledige beschrijving, de ernst, de huidige status, de aangevallen resource, de herstelstappen uit voor het incident en de waarschuwingen die zijn opgenomen in dit incident.</span><span class="sxs-lookup"><span data-stu-id="a5074-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="a5074-196">U kunt filteren om te zien **alleen incidenten**, **alleen waarschuwingen**, of **beide**.</span><span class="sxs-lookup"><span data-stu-id="a5074-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="a5074-197">Hoe krijg ik toegang tot het Threat Intelligence-rapport?</span><span class="sxs-lookup"><span data-stu-id="a5074-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="a5074-198">ASC analyseert gegevens uit meerdere bronnen bedreigingen identificeren.</span><span class="sxs-lookup"><span data-stu-id="a5074-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="a5074-199">Security Center bevat om te helpen respons op incidenten teams onderzoeken en bedreigingen te herstellen, een bedreiging intelligence-rapport dat informatie bevat over de bedreiging die is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="a5074-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="a5074-200">Security Center heeft drie soorten threat rapporten die per aanval kunnen variëren.</span><span class="sxs-lookup"><span data-stu-id="a5074-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="a5074-201">De beschikbare rapporten zijn:</span><span class="sxs-lookup"><span data-stu-id="a5074-201">The reports available are:</span></span>

- <span data-ttu-id="a5074-202">Activiteitengroep rapport: biedt verdiepen in aanvallers, hun doelstellingen en -tactieken.</span><span class="sxs-lookup"><span data-stu-id="a5074-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="a5074-203">Campagne rapport: Er is gericht op gegevens van specifieke aanval campagnes.</span><span class="sxs-lookup"><span data-stu-id="a5074-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="a5074-204">Het overzichtsrapport voor Threat: bevat informatie over alle items in de vorige twee rapporten.</span><span class="sxs-lookup"><span data-stu-id="a5074-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="a5074-205">Dit type gegevens zeer nuttig is tijdens de respons op incidenten, waarbij er lopende onderzoek om te begrijpen van de bron van de aanval, de aanvaller beweegredenen en wat te doen om dit probleem vooruitgang beperken.</span><span class="sxs-lookup"><span data-stu-id="a5074-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="a5074-206">Voor toegang tot de threat intelligence-rapport moet het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a5074-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="a5074-207">Selecteer de **beveiligingswaarschuwingen** tegel op het dashboard ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="a5074-208">Selecteer de beveiligingswaarschuwing waarvoor u wilt meer informatie vinden.</span><span class="sxs-lookup"><span data-stu-id="a5074-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="a5074-209">In de **rapporten** veld, klikt u op de koppeling naar het threat intelligence-rapport.</span><span class="sxs-lookup"><span data-stu-id="a5074-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="a5074-210">Hiermee opent u het PDF-bestand, die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="a5074-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="a5074-211">Zie voor meer informatie over het rapport ASC threat intelligence [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="a5074-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="a5074-212">Evaluatie</span><span class="sxs-lookup"><span data-stu-id="a5074-212">Assessment</span></span>

<span data-ttu-id="a5074-213">Om te helpen met testen, beoordelen en evalueren van uw beveiligingspostuur, biedt ASC voor het evalueren van de geïntegreerde beveiligingsproblemen met Qualys cloud agents, als onderdeel van het onderdeel van de aanbevelingen voor virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a5074-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="a5074-214">De agent Qualys rapporten beveiligingslek gegevens voor het beheerplatform Qualys die verzendt vervolgens beveiligingslek en health monitoring die gegevens terug naar ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="a5074-215">De aanbeveling om een vulnerability assessment oplossing toevoegen wordt weergegeven in de **aanbevelingen** blade op het dashboard ASC.</span><span class="sxs-lookup"><span data-stu-id="a5074-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="a5074-216">Nadat de oplossing voor de evaluatie van beveiligingsproblemen op de doel-VM is geïnstalleerd, wordt de VM met Security Center gescand op beveiligingsproblemen in het systeem en in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a5074-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="a5074-217">Gedetecteerde problemen worden weergegeven bij de optie **Aanbevelingen voor virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="a5074-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="a5074-218">Hoe ik een vulnerability assessment oplossing implementeren?</span><span class="sxs-lookup"><span data-stu-id="a5074-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="a5074-219">Als een virtuele Machine geen een geïntegreerde vulnerability assessment oplossing is al geïmplementeerd Security Center raadt aan om te worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a5074-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="a5074-220">In het dashboard ASC op de **aanbevelingen** blade Selecteer **een vulnerability assessment oplossing toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="a5074-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="a5074-221">Selecteer de virtuele machines waarop u wilt installeren van de vulnerability assessment-oplossing.</span><span class="sxs-lookup"><span data-stu-id="a5074-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="a5074-222">Klik op **installeren op virtuele machines [aantal].**</span><span class="sxs-lookup"><span data-stu-id="a5074-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="a5074-223">Selecteer een partneroplossing in Azure Marketplace of onder **bestaande oplossing gebruiken** Selecteer **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="a5074-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="a5074-224">U kunt de instellingen voor automatisch bijwerken inschakelen of uitschakelen de **partneroplossingen** blade.</span><span class="sxs-lookup"><span data-stu-id="a5074-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="a5074-225">Zie voor meer informatie wilt over het implementeren van een oplossing voor vulnerability assessment [controle op beveiligingslekken in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a5074-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5074-226">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5074-226">Next steps</span></span>

- [<span data-ttu-id="a5074-227">Snelstartgids voor Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a5074-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="a5074-228">Inleiding tot Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a5074-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="a5074-229">Waarschuwingen van Azure Security Center integreren met Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="a5074-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="a5074-230">Versterking Azure Security Center met geïntegreerde Vulnerability Assessment</span><span class="sxs-lookup"><span data-stu-id="a5074-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
