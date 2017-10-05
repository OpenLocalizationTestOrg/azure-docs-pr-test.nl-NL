---
title: Beveiligingswaarschuwingen beheren in Azure Security Center | Microsoft Docs
description: Dit document bevat informatie over het gebruik van de mogelijkheden van Azure Security Center om beveiligingswaarschuwingen te beheren en hierop te reageren.
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
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="ec644-103">Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ec644-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="ec644-104">Dit document bevat informatie over het gebruik van Azure Security Center om beveiligingswaarschuwingen te beheren en hierop te reageren.</span><span class="sxs-lookup"><span data-stu-id="ec644-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="ec644-105">Als u geavanceerde detectie wilt inschakelen, voert u een upgrade uit naar Azure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="ec644-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="ec644-106">Er is een gratis proefversie voor 60 dagen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ec644-106">A free 60-day trial is available.</span></span> <span data-ttu-id="ec644-107">Als u een upgrade wilt uitvoeren, selecteert u de prijscategorie in het [beveiligingsbeleid](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ec644-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="ec644-108">Zie [Prijsinformatie over Azure Security Center](security-center-pricing.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec644-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="ec644-109">Wat zijn beveiligingswaarschuwingen?</span><span class="sxs-lookup"><span data-stu-id="ec644-109">What are security alerts?</span></span>
<span data-ttu-id="ec644-110">Security Center verzamelt, analyseert en integreert automatisch logboekgegevens van uw Azure-resources, het netwerk en verbonden partneroplossingen, zoals firewall- en eindpuntbeveiligingsoplossingen om werkelijke dreigingen te detecteren en fout-positieven te reduceren.</span><span class="sxs-lookup"><span data-stu-id="ec644-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="ec644-111">In Security Center wordt een lijst met beveiligingswaarschuwingen met prioriteiten weergegeven samen met de informatie die u nodig hebt om snel onderzoek te doen naar het probleem en aanbevelingen voor het herstellen van een aanval.</span><span class="sxs-lookup"><span data-stu-id="ec644-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="ec644-112">Lees [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md) voor meer informatie over de werking van de detectiemogelijkheden van Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="ec644-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="ec644-113">Beveiligingswaarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="ec644-113">Managing security alerts</span></span>
<span data-ttu-id="ec644-114">U kunt uw huidige waarschuwingen controleren met de tegel **Beveiligingswaarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="ec644-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="ec644-115">Open Azure Portal en voer de volgende stappen uit om meer informatie over elke waarschuwing weer te geven:</span><span class="sxs-lookup"><span data-stu-id="ec644-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="ec644-116">Op het Security Center-dashboard ziet u de tegel **Beveiligingswaarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="ec644-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![De tegel Beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="ec644-118">Klik op de tegel om de blade **Beveiligingswaarschuwingen** met meer informatie over de waarschuwingen te openen (zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="ec644-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![De blade Beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="ec644-120">In het onderste gedeelte van deze blade vindt u de details voor elke waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ec644-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="ec644-121">Als u wilt sorteren, klikt u op de kolom waarop u wilt sorteren.</span><span class="sxs-lookup"><span data-stu-id="ec644-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="ec644-122">Hieronder volgt de definitie voor elke kolom:</span><span class="sxs-lookup"><span data-stu-id="ec644-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="ec644-123">**Beschrijving**: een korte beschrijving van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ec644-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="ec644-124">**Aantal**: een lijst met alle waarschuwingen van dit specifieke type die zijn gedetecteerd op een specifieke dag.</span><span class="sxs-lookup"><span data-stu-id="ec644-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="ec644-125">**Gedetecteerd door**: de service die verantwoordelijk is voor activering van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ec644-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="ec644-126">**Datum**: de datum waarop de gebeurtenis heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="ec644-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="ec644-127">**Status**: de huidige status voor deze waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ec644-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="ec644-128">Er zijn twee soorten statussen:</span><span class="sxs-lookup"><span data-stu-id="ec644-128">There are two types of states:</span></span>
  * <span data-ttu-id="ec644-129">**Actief**: de beveiligingswaarschuwing is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="ec644-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="ec644-130">**Ernst**: de ernst kan hoog, gemiddeld of laag zijn.</span><span class="sxs-lookup"><span data-stu-id="ec644-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="ec644-131">Waarschuwingen filteren</span><span class="sxs-lookup"><span data-stu-id="ec644-131">Filtering alerts</span></span>
<span data-ttu-id="ec644-132">U kunt waarschuwingen filteren op basis van datum, status en ernst.</span><span class="sxs-lookup"><span data-stu-id="ec644-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="ec644-133">Het filteren van waarschuwingen kan nuttig zijn wanneer u minder beveiligingswaarschuwingen wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="ec644-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="ec644-134">U kunt u bijvoorbeeld concentreren op de beveiligingswaarschuwingen van de afgelopen 24 uur, omdat u een mogelijke inbreuk in het systeem onderzoekt.</span><span class="sxs-lookup"><span data-stu-id="ec644-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="ec644-135">Klik op **Filter** op de blade **Beveiligingswaarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="ec644-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="ec644-136">De blade **Filter** wordt geopend en u selecteert de gewenste waarden voor datum, status en ernst.</span><span class="sxs-lookup"><span data-stu-id="ec644-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Waarschuwingen filteren in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="ec644-138">Reageren op beveiligingswaarschuwingen</span><span class="sxs-lookup"><span data-stu-id="ec644-138">Respond to security alerts</span></span>
<span data-ttu-id="ec644-139">Selecteer een beveiligingswaarschuwing voor meer informatie over de gebeurtenis(sen) waarmee de waarschuwing is geactiveerd en welke stappen u zo nodig moet uitvoeren om een aanval te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="ec644-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="ec644-140">Beveiligingswaarschuwingen zijn gegroepeerd op type en datum.</span><span class="sxs-lookup"><span data-stu-id="ec644-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="ec644-141">Als u op een beveiligingswaarschuwing klikt, wordt een blade met een lijst gegroepeerde waarschuwingen geopend.</span><span class="sxs-lookup"><span data-stu-id="ec644-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Op beveiligingswaarschuwingen reageren in Azure Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="ec644-143">In dit geval verwijzen de geactiveerde waarschuwingen naar verdachte RDP-activiteiten (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="ec644-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="ec644-144">In de eerste kolom ziet u welke resources zijn aangevallen, de tweede kolom toont hoe vaak de resource is aangevallen, de derde kolom bevat de tijd waarop de aanval heeft gevonden; de vierde kolom bevat de status van de waarschuwing en in de vijfde kolom wordt de ernst van de aanval weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ec644-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="ec644-145">Bekijk deze informatie en klik op de resource die is aangevallen. Er wordt dan een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="ec644-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Suggesties voor wat u kunt doen bij beveiligingswaarschuwingen in Azure Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="ec644-147">U vindt in het veld **Omschrijving** van deze blade meer informatie over deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="ec644-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="ec644-148">Deze aanvullende informatie biedt inzicht in wat de beveiligingswaarschuwing heeft geactiveerd, de doelresource, eventueel het bron-IP-adres en aanbevelingen voor het herstellen.</span><span class="sxs-lookup"><span data-stu-id="ec644-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="ec644-149">In sommige gevallen zal het bron-IP-adres leeg zijn (niet beschikbaar), omdat niet alle Windows-logboeken voor beveiligingsgebeurtenissen het IP-adres bevatten.</span><span class="sxs-lookup"><span data-stu-id="ec644-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="ec644-150">Het herstel dat door Security Center wordt voorgesteld, is afhankelijk van de beveiligingswaarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ec644-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="ec644-151">In sommige gevallen moet u wellicht andere Azure-mogelijkheden gebruiken om het aanbevolen herstel te implementeren.</span><span class="sxs-lookup"><span data-stu-id="ec644-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="ec644-152">Als herstel voor deze aanval moet bijvoorbeeld het IP-adres op een zwarte lijst worden gezet dat door de aanval is gegenereerd. Hiervoor is de regel van een [netwerk-ACL](../virtual-network/virtual-networks-acl.md) of een [netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) nodig.</span><span class="sxs-lookup"><span data-stu-id="ec644-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="ec644-153">Lees voor meer informatie over de verschillende typen waarschuwingen [Beveiligingswaarschuwingen per type in Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="ec644-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="ec644-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ec644-154">See also</span></span>
<span data-ttu-id="ec644-155">In dit document hebt u kunnen lezen hoe u het beveiligingsbeleid in Security Center configureert.</span><span class="sxs-lookup"><span data-stu-id="ec644-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="ec644-156">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="ec644-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="ec644-157">Beveiligingsincidenten afhandelen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ec644-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="ec644-158">Detectiemogelijkheden van Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ec644-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="ec644-159">Plannings- en bedieningsgids voor Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ec644-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="ec644-160">[Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="ec644-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ec644-161">[Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.</span><span class="sxs-lookup"><span data-stu-id="ec644-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
