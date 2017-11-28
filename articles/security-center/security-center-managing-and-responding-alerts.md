---
title: aaaManage beveiligingswaarschuwingen in Azure Security Center | Microsoft Docs
description: Dit document helpt u toouse Azure Security Center mogelijkheden toomanage en toosecurity waarschuwingen reageren.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="f1359-103">Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f1359-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="f1359-104">Dit document helpt u bij gebruik van Azure Security Center toomanage en toosecurity waarschuwingen reageren.</span><span class="sxs-lookup"><span data-stu-id="f1359-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="f1359-105">Geavanceerde tooenable detecties, upgrade tooAzure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="f1359-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="f1359-106">Er is een gratis proefversie voor 60 dagen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f1359-106">A free 60-day trial is available.</span></span> <span data-ttu-id="f1359-107">tooupgrade, selecteer prijscategorie in Hallo [beveiligingsbeleid](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f1359-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="f1359-108">Zie [prijzen van Azure Security Center](security-center-pricing.md) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="f1359-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="f1359-109">Wat zijn beveiligingswaarschuwingen?</span><span class="sxs-lookup"><span data-stu-id="f1359-109">What are security alerts?</span></span>
<span data-ttu-id="f1359-110">Security Center automatisch verzamelt, analyseert, en integreert logboekgegevens van uw Azure-resources, Hallo netwerk, en verbonden partneroplossingen, zoals een firewall en endpoint protection-oplossingen, toodetect Werkelijke dreigingen en fout-positieven te reduceren.</span><span class="sxs-lookup"><span data-stu-id="f1359-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="f1359-111">Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly onderzoeken Hallo probleem en aanbevelingen voor hoe tooremediate een aanval.</span><span class="sxs-lookup"><span data-stu-id="f1359-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="f1359-112">Lees [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md) voor meer informatie over de werking van de detectiemogelijkheden van Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="f1359-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="f1359-113">Beveiligingswaarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="f1359-113">Managing security alerts</span></span>
<span data-ttu-id="f1359-114">U kunt uw huidige waarschuwingen controleren door te kijken Hallo **beveiligingswaarschuwingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="f1359-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="f1359-115">Azure Portal openen en volg Hallo stappen hieronder toosee meer informatie over elke waarschuwing:</span><span class="sxs-lookup"><span data-stu-id="f1359-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="f1359-116">Op Hallo Security Center-dashboard, ziet u Hallo **beveiligingswaarschuwingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="f1359-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![De tegel Beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="f1359-118">Klik op Hallo tegel tooopen hello **beveiligingswaarschuwingen** blade met meer informatie over Hallo waarschuwingen zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f1359-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Hallo blade beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="f1359-120">Hallo onder in deze blade zijn Hallo details voor elke waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f1359-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="f1359-121">toosort, klikt u op Hallo-kolom die u wilt toosort door.</span><span class="sxs-lookup"><span data-stu-id="f1359-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="f1359-122">Hallo-definitie voor elke kolom hieronder:</span><span class="sxs-lookup"><span data-stu-id="f1359-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="f1359-123">**Beschrijving**: een korte uitleg van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f1359-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="f1359-124">**Aantal**: een lijst met alle waarschuwingen van dit specifieke type die zijn gedetecteerd op een specifieke dag.</span><span class="sxs-lookup"><span data-stu-id="f1359-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="f1359-125">**Gedetecteerd door**: Hallo-service die verantwoordelijk is voor activering Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f1359-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="f1359-126">**Datum**: Hallo datum die Hallo-gebeurtenis is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f1359-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="f1359-127">**Status**: Hallo van de huidige status voor deze waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f1359-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="f1359-128">Er zijn twee soorten statussen:</span><span class="sxs-lookup"><span data-stu-id="f1359-128">There are two types of states:</span></span>
  * <span data-ttu-id="f1359-129">**Actieve**: Hallo beveiligingswaarschuwing is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f1359-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="f1359-130">**Ernst**: Hallo ernst kan hoog, Gemiddeld of laag zijn.</span><span class="sxs-lookup"><span data-stu-id="f1359-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="f1359-131">Waarschuwingen filteren</span><span class="sxs-lookup"><span data-stu-id="f1359-131">Filtering alerts</span></span>
<span data-ttu-id="f1359-132">U kunt waarschuwingen filteren op basis van datum, status en ernst.</span><span class="sxs-lookup"><span data-stu-id="f1359-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="f1359-133">Filteren van waarschuwingen kan nuttig zijn voor scenario's waarbij u toonarrow Hallo bereik van beveiliging waarschuwingen weergeven moet zijn.</span><span class="sxs-lookup"><span data-stu-id="f1359-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="f1359-134">Bijvoorbeeld, u kunt u wilt dat tooaddress beveiligingswaarschuwingen in Hallo afgelopen 24 uur omdat u een mogelijke inbreuk in Hallo systeem onderzoekt.</span><span class="sxs-lookup"><span data-stu-id="f1359-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="f1359-135">Klik op **Filter** op Hallo **beveiligingswaarschuwingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f1359-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="f1359-136">Hallo **Filter** blade wordt geopend en u Hallo datum, status en ernst waarden u toosee wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f1359-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Waarschuwingen filteren in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="f1359-138">Reageren toosecurity waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f1359-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="f1359-139">Selecteer een waarschuwing toolearn beveiliging meer informatie over Hallo gebeurtenis(sen) waarmee geactiveerd Hallo waarschuwing en wat, indien aanwezig, stappen u moet tootake tooremediate een aanval.</span><span class="sxs-lookup"><span data-stu-id="f1359-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="f1359-140">Beveiligingswaarschuwingen zijn gegroepeerd op type en datum.</span><span class="sxs-lookup"><span data-stu-id="f1359-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="f1359-141">Te klikken op een beveiligingswaarschuwing wordt een blade met een lijst met Hallo gegroepeerde waarschuwingen geopend.</span><span class="sxs-lookup"><span data-stu-id="f1359-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Reageren toosecurity waarschuwingen in Azure Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="f1359-143">In dit geval verwijzen geactiveerde Hallo waarschuwingen toosuspicious Remote Desktop Protocol (RDP)-activiteit.</span><span class="sxs-lookup"><span data-stu-id="f1359-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="f1359-144">Hallo eerste kolom ziet u welke resources zijn aangevallen; Hallo tweede wordt aangegeven hoe vaak Hallo resource is aangevallen; Hallo derde laat zien Hallo Hallo aanval; Hallo toont vierde status van waarschuwing Hallo; en Hallo vijfde Hallo ernst van de Hallo aanval worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f1359-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="f1359-145">Bekijk deze informatie en klikt u op Hallo resource die is aangevallen en wordt een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="f1359-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Suggesties voor welke toodo over beveiliging in Azure Security Center waarschuwingen](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="f1359-147">In Hallo **beschrijving** veld van deze blade vindt u meer informatie over deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f1359-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="f1359-148">Deze aanvullende informatie biedt inzicht in welke triggered Hallo beveiliging waarschuwing, Hallo doelresource, wanneer van toepassing hello bron-IP-adres en aanbevelingen over het tooremediate.</span><span class="sxs-lookup"><span data-stu-id="f1359-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="f1359-149">In sommige gevallen kan leeg de IP-bronadres Hallo zijn (niet beschikbaar) omdat niet alle Windows-Logboeken voor beveiligingsgebeurtenissen Hallo IP-adres bevatten.</span><span class="sxs-lookup"><span data-stu-id="f1359-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="f1359-150">Hallo herstel voorgesteld door Security Center varieert volgens toohello beveiligingswaarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f1359-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="f1359-151">In sommige gevallen moet u wellicht toouse andere mogelijkheden van Azure tooimplement Hallo aanbevolen herstel.</span><span class="sxs-lookup"><span data-stu-id="f1359-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="f1359-152">Bijvoorbeeld, Hallo herstel voor deze aanval tooblacklist Hallo IP-adres dat aanval is gegenereerd is met behulp van een [netwerk-ACL](../virtual-network/virtual-networks-acl.md) of een [netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) regel.</span><span class="sxs-lookup"><span data-stu-id="f1359-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="f1359-153">Lees voor meer informatie over verschillende soorten waarschuwingen Hallo [beveiligingswaarschuwingen op typen in Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="f1359-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="f1359-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f1359-154">See also</span></span>
<span data-ttu-id="f1359-155">In dit document, u leert hoe tooconfigure beveiligingsbeleid in Security Center.</span><span class="sxs-lookup"><span data-stu-id="f1359-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="f1359-156">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="f1359-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="f1359-157">Beveiligingsincidenten afhandelen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f1359-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="f1359-158">Detectiemogelijkheden van Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f1359-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="f1359-159">Plannings- en bedieningsgids voor Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f1359-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="f1359-160">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="f1359-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f1359-161">[Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.</span><span class="sxs-lookup"><span data-stu-id="f1359-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
