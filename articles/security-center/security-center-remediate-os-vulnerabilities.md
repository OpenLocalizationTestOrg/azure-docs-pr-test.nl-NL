---
title: aaaRemediate OS beveiligingslekken in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** herstellen OS beveiligingslekken **.
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="ab915-103">OS-beveiligingslekken in Azure Security Center oplossen</span><span class="sxs-lookup"><span data-stu-id="ab915-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="ab915-104">Azure Security Center analyseert dagelijks uw virtuele machine (VM)-besturingssysteem (OS) voor configuraties die kunnen Hallo VM kwetsbaarder tooattack en raadt configuratiewijzigingen tooaddress beveiligingslekken.</span><span class="sxs-lookup"><span data-stu-id="ab915-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="ab915-105">Security Center adviseert u beveiligingsproblemen oplossen wanneer de configuratie van het besturingssysteem van de VM komt niet overeen met de Hallo configuratieregels aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="ab915-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="ab915-106">Zie voor meer informatie over Hallo specifieke configuraties die worden bewaakt Hallo [lijst met regels van de aanbevolen configuratie](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="ab915-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ab915-107">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="ab915-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="ab915-108">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ab915-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="ab915-109">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="ab915-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="ab915-110">In Hallo **aanbevelingen** blade Selecteer **herstellen OS beveiligingslekken**.</span><span class="sxs-lookup"><span data-stu-id="ab915-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="ab915-111">![Beveiligingsproblemen met het besturingssysteem herstellen][1]</span><span class="sxs-lookup"><span data-stu-id="ab915-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="ab915-112">Hallo **herstellen OS beveiligingslekken** blade wordt geopend en een lijst met uw virtuele machines met besturingssysteemconfiguraties die niet overeenkomen met de Hallo configuratieregels aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="ab915-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="ab915-113">Voor elke VM identificeert Hallo blade:</span><span class="sxs-lookup"><span data-stu-id="ab915-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="ab915-114">**REGELS voor MISLUKTE** --Hallo aantal regels dat Hallo configuratie van het besturingssysteem van de virtuele machine is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ab915-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="ab915-115">**TIJD van laatste SCAN** --Hallo datum en tijd dat Security Center voor het laatst gescand configuratie van het besturingssysteem Hallo van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ab915-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="ab915-116">**STATUS** --Hallo van de huidige status van Hallo beveiligingslek:</span><span class="sxs-lookup"><span data-stu-id="ab915-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="ab915-117">Open: Hallo beveiligingslek is nog niet opgelost</span><span class="sxs-lookup"><span data-stu-id="ab915-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="ab915-118">Bezig: Hallo beveiligingslek momenteel wordt toegepast, door u is geen actie vereist.</span><span class="sxs-lookup"><span data-stu-id="ab915-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="ab915-119">Opgelost: Hallo beveiligingslek is al opgenomen (wanneer het Hallo-probleem is opgelost, Hallo vermelding is lichter gekleurd weergegeven)</span><span class="sxs-lookup"><span data-stu-id="ab915-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="ab915-120">**ERNST** --alle zwakke plekken zijn ingesteld van tooa ernst van de laag, wat betekent dat een beveiligingsprobleem moet worden opgelost, maar geen onmiddellijke aandacht vereist.</span><span class="sxs-lookup"><span data-stu-id="ab915-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="ab915-121">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ab915-121">Select a VM.</span></span> <span data-ttu-id="ab915-122">Een blade voor die VM wordt geopend en geeft weer Hallo-regels die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="ab915-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="ab915-123">![Van configuratieregels die zijn mislukt][2]</span><span class="sxs-lookup"><span data-stu-id="ab915-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="ab915-124">Selecteer een regel.</span><span class="sxs-lookup"><span data-stu-id="ab915-124">Select a rule.</span></span> <span data-ttu-id="ab915-125">In dit voorbeeld kunt selecteren **wachtwoorden moeten voldoen aan de complexiteitsvereisten**.</span><span class="sxs-lookup"><span data-stu-id="ab915-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="ab915-126">Er wordt een blade geopend met een beschrijving regel en Hallo impact van Hallo is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ab915-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="ab915-127">Bekijk de details van Hallo en houd rekening met hoe besturingssysteemconfiguraties worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="ab915-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="ab915-128">![Beschrijving voor Hallo is mislukt voor regel][3]</span><span class="sxs-lookup"><span data-stu-id="ab915-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="ab915-129">Security Center gebruikt Common Configuration Enumeration (CCE) tooassign unieke id's voor van configuratieregels.</span><span class="sxs-lookup"><span data-stu-id="ab915-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="ab915-130">Hallo volgende informatie is beschikbaar op deze blade:</span><span class="sxs-lookup"><span data-stu-id="ab915-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="ab915-131">--Naam van regel</span><span class="sxs-lookup"><span data-stu-id="ab915-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="ab915-132">ERNST--Waarde voor CCE ernst van kritieke, belangrijk of waarschuwingsstatus</span><span class="sxs-lookup"><span data-stu-id="ab915-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="ab915-133">CCIED--CCE unieke id voor de regel Hallo</span><span class="sxs-lookup"><span data-stu-id="ab915-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="ab915-134">Beschrijving: Beschrijving van regel</span><span class="sxs-lookup"><span data-stu-id="ab915-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="ab915-135">BEVEILIGINGSLEK--Uitleg van beveiligingslek of het risico als de regel wordt niet toegepast</span><span class="sxs-lookup"><span data-stu-id="ab915-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="ab915-136">IMPACT--Zakelijke impact als regel wordt toegepast</span><span class="sxs-lookup"><span data-stu-id="ab915-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="ab915-137">VERWACHTE waarde--Waarde verwacht wanneer Security Center de configuratie van uw VM besturingssysteem tegen Hallo regel analyseert</span><span class="sxs-lookup"><span data-stu-id="ab915-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="ab915-138">--REGEL regel-bewerking door Security Center gebruikt tijdens de analyse van de configuratie van het besturingssysteem van virtuele machine tegen Hallo regel</span><span class="sxs-lookup"><span data-stu-id="ab915-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="ab915-139">WERKELIJKE waarde--Waarde geretourneerd na analyse van de configuratie van het besturingssysteem van virtuele machine tegen Hallo regel</span><span class="sxs-lookup"><span data-stu-id="ab915-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="ab915-140">RESULTAAT van evaluatie:-resultaat van de analyse: doorgeven, mislukken</span><span class="sxs-lookup"><span data-stu-id="ab915-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="ab915-141">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ab915-141">See also</span></span>
<span data-ttu-id="ab915-142">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'herstellen OS beveiligingslekken."</span><span class="sxs-lookup"><span data-stu-id="ab915-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="ab915-143">Kunt u bekijken Hallo set configuratieregels [hier](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="ab915-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="ab915-144">Unieke id's (Common Configuration opsomming) CCE tooassign Security Center gebruikt voor van configuratieregels.</span><span class="sxs-lookup"><span data-stu-id="ab915-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="ab915-145">Ga naar Hallo [CCE](https://nvd.nist.gov/cce/index.cfm) website voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ab915-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="ab915-146">toolearn meer informatie over Security Center, Zie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab915-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="ab915-147">[Ondersteunde platforms in Azure Security Center](security-center-os-coverage.md) -geeft een lijst van ondersteunde Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="ab915-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="ab915-148">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ab915-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ab915-149">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ab915-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ab915-150">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ab915-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ab915-151">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="ab915-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ab915-152">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) -informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab915-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ab915-153">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ab915-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ab915-154">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="ab915-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
