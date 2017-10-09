---
title: aaaProtect persoonlijke gegevens met Azure Security Center | Microsoft Docs
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="9aad7-103">Persoonlijke gegevens beschermen tegen aanvallen en inbreuken op: Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9aad7-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="9aad7-104">In dit artikel helpt u begrijpen hoe toouse Azure Security Center tooprotect persoonlijke gegevens van kiezen oplossingen en aanvallen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="9aad7-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="9aad7-105">Scenario</span></span> 

<span data-ttu-id="9aad7-106">Een bedrijf grote cruise, gevestigd in de Verenigde Staten Hallo breidt de bewerkingen toooffer routes in Hallo Middellandse, en Baltische veiligheid, evenals Hallo Florida.</span><span class="sxs-lookup"><span data-stu-id="9aad7-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="9aad7-107">toohelp bij deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en Hallo VK verkregen</span><span class="sxs-lookup"><span data-stu-id="9aad7-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="9aad7-108">Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="9aad7-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="9aad7-109">Dit omvat persoonlijk identificeerbare informatie zoals namen, adressen, telefoonnummers en creditcardgegevens.</span><span class="sxs-lookup"><span data-stu-id="9aad7-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="9aad7-110">Het bevat ook informatie Human Resources, zoals:</span><span class="sxs-lookup"><span data-stu-id="9aad7-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="9aad7-111">Adressen</span><span class="sxs-lookup"><span data-stu-id="9aad7-111">Addresses</span></span>
- <span data-ttu-id="9aad7-112">telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="9aad7-112">Phone numbers</span></span>
- <span data-ttu-id="9aad7-113">BTW-id 's</span><span class="sxs-lookup"><span data-stu-id="9aad7-113">Tax identification numbers</span></span>
- <span data-ttu-id="9aad7-114">medische informatie</span><span class="sxs-lookup"><span data-stu-id="9aad7-114">Medical information</span></span>

<span data-ttu-id="9aad7-115">Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden.</span><span class="sxs-lookup"><span data-stu-id="9aad7-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="9aad7-116">Zakelijke werknemers toegang tot het Hallo netwerk van de externe kantoren en reizen agents van het bedrijf Hallo wereld Hallo zich toegang tot toosome bedrijfsbronnen hebben.</span><span class="sxs-lookup"><span data-stu-id="9aad7-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="9aad7-117">Persoonlijke gegevens die tussen deze locaties en Hallo Microsoft Datacenter via Hallo-netwerk is verzonden.</span><span class="sxs-lookup"><span data-stu-id="9aad7-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="9aad7-118">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="9aad7-118">Problem statement</span></span>

<span data-ttu-id="9aad7-119">Hallo bedrijf maakt zich zorgen over Hallo dreiging van aanvallen op Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9aad7-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="9aad7-120">Ze willen tooprevent blootstelling van werknemers en klanten persoonsgegevens toounauthorized personen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="9aad7-121">Ze willen richtlijnen op zowel voorkomen en antwoord/herstel, evenals een effectieve manier toomonitor Hallo actieve beveiliging van hun cloudbronnen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="9aad7-122">Ze moeten een sterke line-of beveiliging tegen kwaadwillende personen de hedendaagse geavanceerde en geordend.</span><span class="sxs-lookup"><span data-stu-id="9aad7-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="9aad7-123">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="9aad7-123">Company goal</span></span>

<span data-ttu-id="9aad7-124">Een van de doelstellingen van het bedrijf Hallo is tooensure Hallo privacy van klanten en werknemers persoonlijke gegevens te beveiligen tegen bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="9aad7-125">Een van hun doelstellingen is toorespond onmiddellijk toosigns van inbreuk op de toomitigate Hallo impact.</span><span class="sxs-lookup"><span data-stu-id="9aad7-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="9aad7-126">Een manier tooassess Hallo huidige status van de beveiliging is vereist, kwetsbaar configuraties te identificeren en ze herstellen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="9aad7-127">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="9aad7-127">Solutions</span></span>

<span data-ttu-id="9aad7-128">Microsoft Azure Security Center (ASC) biedt een geïntegreerde beveiliging en beleidsbeheer beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="9aad7-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="9aad7-129">Het biedt eenvoudig te gebruiken en effectieve bedreiging mogelijkheden voor preventie, detectie en reactie.</span><span class="sxs-lookup"><span data-stu-id="9aad7-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="9aad7-130">Preventie</span><span class="sxs-lookup"><span data-stu-id="9aad7-130">Prevention</span></span>

<span data-ttu-id="9aad7-131">ASC helpt u bij schendingen doordat u beveiligingsbeleid tooset just-in-time-toegang bieden, voorkomen van en aanbevelingen voor beveiliging te implementeren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="9aad7-132">Een beveiligingsbeleid bepaalt Hallo set besturingselementen die worden aanbevolen voor resources binnen Hallo opgegeven abonnement.</span><span class="sxs-lookup"><span data-stu-id="9aad7-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="9aad7-133">In de tijd kan toegang worden gebruikte toolock omlaag binnenkomend verkeer tooyour Azure Virtual machines blootstelling tooattacks verminderen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="9aad7-134">Aanbevelingen voor beveiliging worden gemaakt door ASC na het analyseren van Hallo beveiligingsstatus van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9aad7-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="9aad7-135">Hoe Stel beleidsregels voor veiligheid in ASC?</span><span class="sxs-lookup"><span data-stu-id="9aad7-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="9aad7-136">U kunt voor elk abonnement beveiligingsbeleid configureren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="9aad7-137">toomodify een beveiligingsbeleid, moet u een eigenaar of bijdrager van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="9aad7-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="9aad7-138">In hello Azure-portal, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9aad7-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="9aad7-139">Selecteer **beleid** in Hallo ASC-dashboard.</span><span class="sxs-lookup"><span data-stu-id="9aad7-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="9aad7-140">Selecteer Hallo abonnement waarop tooenable Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="9aad7-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="9aad7-141">Kies **preventiebeleid** tooconfigure beleid per abonnement.</span><span class="sxs-lookup"><span data-stu-id="9aad7-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="9aad7-142">**Verzamel gegevens van virtuele machines** te moet worden ingesteld**op.**</span><span class="sxs-lookup"><span data-stu-id="9aad7-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="9aad7-143">In Hallo **preventiebeleid** opties, dient u **op** tooenable Hallo aanbevelingen voor beveiliging die relevant voor het Hallo-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="9aad7-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="9aad7-144">Zie voor meer gedetailleerde instructies en een uitleg van Hallo beleid aanbevelingen die kunnen worden ingeschakeld, [beveiligingsbeleid instellen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="9aad7-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="9aad7-145">Hoe configureer ik Just in Time toegang (Just in time)?</span><span class="sxs-lookup"><span data-stu-id="9aad7-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="9aad7-146">Wanneer JIT is ingeschakeld, wordt in Security Center binnenkomend verkeer tooyour Azure Virtual machines vergrendelt door het maken van een NSG-regel.</span><span class="sxs-lookup"><span data-stu-id="9aad7-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="9aad7-147">U selecteert Hallo poorten op Hallo VM toowhich binnenkomend verkeer wordt worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="9aad7-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="9aad7-148">toouse JIT krijgen, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9aad7-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="9aad7-149">Selecteer Hallo **Just in time VM toegang tegel** op Hallo ASC blade.</span><span class="sxs-lookup"><span data-stu-id="9aad7-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="9aad7-150">Selecteer Hallo **aanbevolen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9aad7-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="9aad7-151">Onder **VMs**, Hallo virtuele machines die u tooenable wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="9aad7-152">Hiermee wordt een vinkje volgende tooa VM geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9aad7-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="9aad7-153">Selecteer **inschakelen JIT** op virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9aad7-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="9aad7-154">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9aad7-154">Select **Save**.</span></span>

<span data-ttu-id="9aad7-155">Hallo-standaardpoorten die ASC aanbeveelt wordt ingeschakeld voor JIT, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="9aad7-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="9aad7-156">U kunt ook toevoegen en configureren van een nieuwe poort waarop tooenable Hallo NET in tijdoplossing.</span><span class="sxs-lookup"><span data-stu-id="9aad7-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="9aad7-157">Hallo **Just in time VM toegang** tegel in Hallo Security Center bevat Hallo-nummer van virtuele machines die zijn geconfigureerd voor JIT-toegang.</span><span class="sxs-lookup"><span data-stu-id="9aad7-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="9aad7-158">U ziet ook Hallo aantal goedgekeurde toegangsaanvragen in Hallo afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="9aad7-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="9aad7-159">Voor instructies over het toodo, en aanvullende informatie over Just in Time-toegang, Zie [beheren via in de tijd toegang tot een virtuele machine.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="9aad7-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="9aad7-160">Hoe ik ASC beveiligingsaanbevelingen implementeren?</span><span class="sxs-lookup"><span data-stu-id="9aad7-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="9aad7-161">Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="9aad7-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="9aad7-162">Hallo aanbevelingen helpt u bij Hallo Hallo nodig-besturingselementen configureren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="9aad7-163">Selecteer Hallo **aanbevelingen** tegel op Hallo ASC dashboard.</span><span class="sxs-lookup"><span data-stu-id="9aad7-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="9aad7-164">Hallo-aanbevelingen die worden weergegeven in een tabel waarin elke regel een aanbeveling vertegenwoordigt weergeven.</span><span class="sxs-lookup"><span data-stu-id="9aad7-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="9aad7-165">toofilter aanbevelingen, selecteer **Filter** en selecteer Hallo ernst en status waarden voor toosee.</span><span class="sxs-lookup"><span data-stu-id="9aad7-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="9aad7-166">toodismiss een aanbeveling die niet van toepassing, die u kunt met de rechtermuisknop op en selecteer **sluiten.**</span><span class="sxs-lookup"><span data-stu-id="9aad7-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="9aad7-167">Denk na over welke aanbeveling eerst moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="9aad7-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="9aad7-168">Hallo aanbevelingen in volgorde van prioriteit toepassen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="9aad7-169">Voor een lijst met mogelijke aanbevelingen en de zelfstudies over het tooapply, Zie [aanbevelingen voor beveiliging in Azure Security Center beheren.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="9aad7-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="9aad7-170">Detectie van en reactie</span><span class="sxs-lookup"><span data-stu-id="9aad7-170">Detection and Response</span></span>

<span data-ttu-id="9aad7-171">Detectie- en Ga samen als u zo snel mogelijk toorespond wilt nadat een bedreiging is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="9aad7-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="9aad7-172">Detectie van dreigingen ASC werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="9aad7-173">ASC kunt snel de detectiealgoritmen bijwerken als aanvallers release nieuwe en steeds meer geavanceerde aanvallen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="9aad7-174">Zie voor meer informatie gedetailleerde over de werking van de detectie van dreigingen van ASC [Azure Security Center detectiemogelijkheden](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="9aad7-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="9aad7-175">Hoe ik beheren en toosecurity waarschuwingen reageren?</span><span class="sxs-lookup"><span data-stu-id="9aad7-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="9aad7-176">Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly Hallo probleem onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="9aad7-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="9aad7-177">Security Center bevat ook aanbevelingen voor het tooremediate een aanval.</span><span class="sxs-lookup"><span data-stu-id="9aad7-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="9aad7-178">toomanage uw beveiligingswaarschuwingen, Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="9aad7-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="9aad7-179">Selecteer Hallo **beveiligingswaarschuwingen** -tegel in Hallo ASC dashboard.</span><span class="sxs-lookup"><span data-stu-id="9aad7-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="9aad7-180">Hiermee worden de details voor elke waarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9aad7-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="9aad7-181">toofilter waarschuwingen op basis van datum, status en ernst, selecteer **Filter** en selecteer vervolgens de gewenste toosee Hallo-waarden.</span><span class="sxs-lookup"><span data-stu-id="9aad7-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="9aad7-182">toorespond tooan waarschuwing, selecteert u deze en Hallo informatie bekijken, en selecteer vervolgens Hallo resource die is aangevallen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="9aad7-183">In Hallo **beschrijving** veld, ziet u informatie, zoals aanbevolen herstel.</span><span class="sxs-lookup"><span data-stu-id="9aad7-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="9aad7-184">Zie voor meer instructies voor het reageert toosecurity waarschuwingen, [beheren en reageert toosecurity waarschuwingen in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="9aad7-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="9aad7-185">Voor verdere hulp bij het onderzoeken van beveiligingswaarschuwingen Hallo bedrijf ASC waarschuwingen kunt integreren met een eigen SIEM-oplossing met behulp van [Azure Log integratie](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="9aad7-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="9aad7-186">Hoe beheer ik beveiligingsincidenten?</span><span class="sxs-lookup"><span data-stu-id="9aad7-186">How do I manage security incidents?</span></span>

<span data-ttu-id="9aad7-187">In ASC is een beveiligingsincident voordoet een aggregatie van alle waarschuwingen voor een resource uitgelijnd met de kill-keten patronen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="9aad7-188">Een Incident onthullen Hallo lijst met verwante waarschuwingen, waarmee u tooobtain meer informatie over elk exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9aad7-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="9aad7-189">Incidenten verschijnen in de tegel beveiligingswaarschuwingen Hallo en blade.</span><span class="sxs-lookup"><span data-stu-id="9aad7-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="9aad7-190">tooreview en beveiligingsincidenten, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9aad7-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="9aad7-191">Selecteer Hallo **beveiligingswaarschuwingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="9aad7-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="9aad7-192">Als een beveiligingsincident voordoet wordt gedetecteerd, wordt weergegeven onder Hallo beveiliging waarschuwingen grafiek.</span><span class="sxs-lookup"><span data-stu-id="9aad7-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="9aad7-193">Er is een pictogram dat verschilt van andere waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="9aad7-194">Selecteer Hallo incident toosee meer informatie over deze beveiligingsincident voordoet.</span><span class="sxs-lookup"><span data-stu-id="9aad7-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="9aad7-195">Aanvullende gegevens bevatten een volledige beschrijving, de ernst, de huidige status, Hallo aangevallen resources, Hallo herstelstappen voor Hallo incident en Hallo waarschuwingen die zijn opgenomen in dit incident.</span><span class="sxs-lookup"><span data-stu-id="9aad7-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="9aad7-196">U kunt filteren toosee **alleen incidenten**, **alleen waarschuwingen**, of **beide**.</span><span class="sxs-lookup"><span data-stu-id="9aad7-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="9aad7-197">Hoe krijg ik toegang tot Hallo Threat Intelligence-rapport?</span><span class="sxs-lookup"><span data-stu-id="9aad7-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="9aad7-198">ASC analyseert gegevens uit meerdere bronnen tooidentify bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="9aad7-199">tooassist respons op incidenten teams onderzoeken en bedreigingen te herstellen, Security Center bevat een bedreiging intelligence-rapport dat informatie bevat over Hallo threat die is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="9aad7-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="9aad7-200">Security Center heeft drie soorten threat rapporten die per aanval kunnen variëren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="9aad7-201">Hallo rapporten zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="9aad7-201">hello reports available are:</span></span>

- <span data-ttu-id="9aad7-202">Activiteitengroep rapport: biedt verdiepen in aanvallers, hun doelstellingen en -tactieken.</span><span class="sxs-lookup"><span data-stu-id="9aad7-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="9aad7-203">Campagne rapport: Er is gericht op gegevens van specifieke aanval campagnes.</span><span class="sxs-lookup"><span data-stu-id="9aad7-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="9aad7-204">Het overzichtsrapport voor Threat: bevat informatie over alle items in de vorige twee rapporten Hallo.</span><span class="sxs-lookup"><span data-stu-id="9aad7-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="9aad7-205">Dit type gegevens is zeer nuttig tijdens Hallo respons op incidenten, wanneer er een bron lopende onderzoek toounderstand Hallo Hallo aanval, Hallo aanvaller beweegredenen, en welke toomitigate toodo dit probleem zwevend doorsturen.</span><span class="sxs-lookup"><span data-stu-id="9aad7-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="9aad7-206">tooaccess Hallo dreigingen rapporteren, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9aad7-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="9aad7-207">Selecteer Hallo **beveiligingswaarschuwingen** tegel op Hallo ASC dashboard.</span><span class="sxs-lookup"><span data-stu-id="9aad7-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="9aad7-208">Selecteer Hallo beveiligingswaarschuwing waarvoor u tooobtain wilt meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9aad7-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="9aad7-209">In Hallo **rapporten** veld, klikt u op Hallo koppeling toohello threat intelligence-rapport.</span><span class="sxs-lookup"><span data-stu-id="9aad7-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="9aad7-210">Hiermee opent u Hallo PDF-bestand, die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="9aad7-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="9aad7-211">Zie voor meer informatie over Hallo ASC threat intelligence-rapport [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="9aad7-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="9aad7-212">Evaluatie</span><span class="sxs-lookup"><span data-stu-id="9aad7-212">Assessment</span></span>

<span data-ttu-id="9aad7-213">toohelp met testen, beoordelen en evalueren van uw beveiligingspostuur ASC biedt voor het evalueren van de geïntegreerde beveiligingsproblemen met Qualys cloud agents, als onderdeel van het onderdeel van de aanbevelingen voor virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9aad7-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="9aad7-214">Hallo Qualys agent rapporteert beveiligingslek toohello Qualys platform voor gegevensbeheer, die vervolgens verzendt beveiligingslek en health bewakingsgegevens weer tooASC.</span><span class="sxs-lookup"><span data-stu-id="9aad7-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="9aad7-215">aanbeveling tooadd oplossing voor een beveiligingsprobleem wordt weergegeven in Hallo Hallo **aanbevelingen** blade op Hallo ASC dashboard.</span><span class="sxs-lookup"><span data-stu-id="9aad7-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="9aad7-216">Nadat Hallo vulnerability assessment oplossing op Hallo doel VM is geïnstalleerd, wordt in Security Center scans VM toodetect Hallo en systeem- en kwetsbaarheden identificeren.</span><span class="sxs-lookup"><span data-stu-id="9aad7-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="9aad7-217">Gevonden problemen worden vermeld in de Hallo **aanbevelingen voor virtuele Machines** optie.</span><span class="sxs-lookup"><span data-stu-id="9aad7-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="9aad7-218">Hoe ik een vulnerability assessment oplossing implementeren?</span><span class="sxs-lookup"><span data-stu-id="9aad7-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="9aad7-219">Als een virtuele Machine geen een geïntegreerde vulnerability assessment oplossing is al geïmplementeerd Security Center raadt aan om te worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9aad7-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="9aad7-220">In Hallo ASC dashboard Hallo **aanbevelingen** blade Selecteer **een vulnerability assessment oplossing toevoegen.**</span><span class="sxs-lookup"><span data-stu-id="9aad7-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="9aad7-221">Selecteer Hallo VMs waar u tooinstall Hallo vulnerability assessment oplossing.</span><span class="sxs-lookup"><span data-stu-id="9aad7-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="9aad7-222">Klik op **installeren op virtuele machines [aantal].**</span><span class="sxs-lookup"><span data-stu-id="9aad7-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="9aad7-223">Selecteer een partneroplossing in hello Azure Marketplace of onder **bestaande oplossing gebruiken** Selecteer **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="9aad7-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="9aad7-224">Kunt u Hallo automatische update-instellingen in- of uitschakelen in Hallo **partneroplossingen** blade.</span><span class="sxs-lookup"><span data-stu-id="9aad7-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="9aad7-225">Voor verdere instructies voor het tooimplement een oplossing voor vulnerability assessment, Zie [controle op beveiligingslekken in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="9aad7-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aad7-226">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9aad7-226">Next steps</span></span>

- [<span data-ttu-id="9aad7-227">Snelstartgids voor Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9aad7-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="9aad7-228">Inleiding tooAzure Security Center</span><span class="sxs-lookup"><span data-stu-id="9aad7-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="9aad7-229">Waarschuwingen van Azure Security Center integreren met Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="9aad7-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="9aad7-230">Versterking Azure Security Center met geïntegreerde Vulnerability Assessment</span><span class="sxs-lookup"><span data-stu-id="9aad7-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
