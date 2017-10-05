---
title: Herstellen van de OS-beveiligingslekken in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** herstellen OS beveiligingslekken **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="0a418-103">OS-beveiligingslekken in Azure Security Center oplossen</span><span class="sxs-lookup"><span data-stu-id="0a418-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="0a418-104">Azure Security Center analyseert dagelijks uw virtuele machine (VM)-besturingssysteem (OS) voor configuraties die de virtuele machine kwetsbaar voor aanvallen kunnen maken en raadt aan om de configuratiewijzigingen voor deze beveiligingsproblemen te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="0a418-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="0a418-105">Security Center raadt aan dat u beveiligingsproblemen oplossen wanneer de configuratie van het besturingssysteem van de VM komt niet overeen met de aanbevolen configuratieregels.</span><span class="sxs-lookup"><span data-stu-id="0a418-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="0a418-106">Zie voor meer informatie over de specifieke configuraties die worden bewaakt de [lijst met regels van de aanbevolen configuratie](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="0a418-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="0a418-107">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="0a418-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="0a418-108">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="0a418-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="0a418-109">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="0a418-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="0a418-110">In de **aanbevelingen** blade Selecteer **herstellen OS beveiligingslekken**.</span><span class="sxs-lookup"><span data-stu-id="0a418-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="0a418-111">![Beveiligingsproblemen met het besturingssysteem herstellen][1]</span><span class="sxs-lookup"><span data-stu-id="0a418-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="0a418-112">De **herstellen OS beveiligingslekken** blade wordt geopend en een lijst met uw virtuele machines met besturingssysteemconfiguraties die niet overeenkomen met de aanbevolen configuratie-regels.</span><span class="sxs-lookup"><span data-stu-id="0a418-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="0a418-113">Voor elke VM identificeert de blade:</span><span class="sxs-lookup"><span data-stu-id="0a418-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="0a418-114">**REGELS voor MISLUKTE** --het aantal regels dat configuratie van het besturingssysteem van de VM is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0a418-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="0a418-115">**TIJD van laatste SCAN** --de datum en tijd dat Security Center voor het laatst gescand configuratie van het besturingssysteem van de VM.</span><span class="sxs-lookup"><span data-stu-id="0a418-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="0a418-116">**STATUS** --de huidige status van het probleem:</span><span class="sxs-lookup"><span data-stu-id="0a418-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="0a418-117">Open: De kwetsbaarheid ertoe is nog niet opgelost</span><span class="sxs-lookup"><span data-stu-id="0a418-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="0a418-118">Bezig: De kwetsbaarheid ertoe dat momenteel wordt toegepast, door u is geen actie vereist.</span><span class="sxs-lookup"><span data-stu-id="0a418-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="0a418-119">Opgelost: De kwetsbaarheid ertoe is al opgenomen in (als het probleem verholpen is, de vermelding is lichter gekleurd weergegeven)</span><span class="sxs-lookup"><span data-stu-id="0a418-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="0a418-120">**ERNST** --alle zwakke plekken zijn ingesteld op een ernst van de laag, wat betekent dat een beveiligingsprobleem moet worden opgelost, maar geen onmiddellijke aandacht vereist.</span><span class="sxs-lookup"><span data-stu-id="0a418-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="0a418-121">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0a418-121">Select a VM.</span></span> <span data-ttu-id="0a418-122">Een blade voor die VM wordt geopend en de regels die niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a418-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="0a418-123">![Van configuratieregels die zijn mislukt][2]</span><span class="sxs-lookup"><span data-stu-id="0a418-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="0a418-124">Selecteer een regel.</span><span class="sxs-lookup"><span data-stu-id="0a418-124">Select a rule.</span></span> <span data-ttu-id="0a418-125">In dit voorbeeld kunt selecteren **wachtwoorden moeten voldoen aan de complexiteitsvereisten**.</span><span class="sxs-lookup"><span data-stu-id="0a418-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="0a418-126">Er wordt een blade geopend met een beschrijving van de regel is mislukt en de impact.</span><span class="sxs-lookup"><span data-stu-id="0a418-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="0a418-127">Bekijk de details en houd rekening met hoe besturingssysteemconfiguraties worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="0a418-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="0a418-128">![Beschrijving voor de regel is mislukt][3]</span><span class="sxs-lookup"><span data-stu-id="0a418-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="0a418-129">Security Center gebruikt Common Configuration Enumeration (CCE) om de unieke id's voor configuratieregels toewijzen.</span><span class="sxs-lookup"><span data-stu-id="0a418-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="0a418-130">De volgende informatie wordt in deze blade verstrekt:</span><span class="sxs-lookup"><span data-stu-id="0a418-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="0a418-131">--Naam van regel</span><span class="sxs-lookup"><span data-stu-id="0a418-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="0a418-132">ERNST--Waarde voor CCE ernst van kritieke, belangrijk of waarschuwingsstatus</span><span class="sxs-lookup"><span data-stu-id="0a418-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="0a418-133">CCIED--CCE unieke id voor de regel</span><span class="sxs-lookup"><span data-stu-id="0a418-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="0a418-134">Beschrijving: Beschrijving van regel</span><span class="sxs-lookup"><span data-stu-id="0a418-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="0a418-135">BEVEILIGINGSLEK--Uitleg van beveiligingslek of het risico als de regel wordt niet toegepast</span><span class="sxs-lookup"><span data-stu-id="0a418-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="0a418-136">IMPACT--Zakelijke impact als regel wordt toegepast</span><span class="sxs-lookup"><span data-stu-id="0a418-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="0a418-137">VERWACHTE waarde--Waarde verwacht wanneer Security Center uw configuratie van het besturingssysteem van de virtuele machine op basis van de regel analyseert</span><span class="sxs-lookup"><span data-stu-id="0a418-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="0a418-138">--REGEL regel-bewerking door Security Center gebruikt tijdens de analyse van de configuratie van het besturingssysteem van virtuele machine op basis van de regel</span><span class="sxs-lookup"><span data-stu-id="0a418-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="0a418-139">WERKELIJKE waarde--Waarde geretourneerd na analyse van uw besturingssysteem voor VM-configuratie op basis van de regel</span><span class="sxs-lookup"><span data-stu-id="0a418-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="0a418-140">RESULTAAT van evaluatie:-resultaat van de analyse: doorgeven, mislukken</span><span class="sxs-lookup"><span data-stu-id="0a418-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="0a418-141">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0a418-141">See also</span></span>
<span data-ttu-id="0a418-142">In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center "Herstellen OS beveiligingslekken."</span><span class="sxs-lookup"><span data-stu-id="0a418-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="0a418-143">U kunt de reeks configuratieregels bekijken [hier](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="0a418-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="0a418-144">Security Center gebruikt CCE (algemene configuratie opsomming) om de unieke id's voor configuratieregels toewijzen.</span><span class="sxs-lookup"><span data-stu-id="0a418-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="0a418-145">Ga naar de [CCE](https://nvd.nist.gov/cce/index.cfm) website voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0a418-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="0a418-146">Zie de volgende bronnen voor meer informatie over Security Center:</span><span class="sxs-lookup"><span data-stu-id="0a418-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="0a418-147">[Ondersteunde platforms in Azure Security Center](security-center-os-coverage.md) -geeft een lijst van ondersteunde Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="0a418-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="0a418-148">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over het beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="0a418-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0a418-149">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="0a418-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="0a418-150">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="0a418-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="0a418-151">[Het beheren van en reageren op beveiligingswaarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over het beheren van en reageren op beveiligingswaarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="0a418-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="0a418-152">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) -informatie over het bewaken van de status van uw partneroplossingen.</span><span class="sxs-lookup"><span data-stu-id="0a418-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="0a418-153">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="0a418-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="0a418-154">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="0a418-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
