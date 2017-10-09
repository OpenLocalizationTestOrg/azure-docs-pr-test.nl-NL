---
title: aaaHandling beveiligingswaarschuwingen in Azure Security Center | Microsoft Docs
description: Dit document helpt u toohandle beveiligingsincidenten voor toouse Azure Security Center mogelijkheden.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="9b17b-103">Beveiligingsincidenten afhandelen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9b17b-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="9b17b-104">Gesorteerd en beveiligingswaarschuwingen onderzoeken kunnen enige tijd duren voor de meest ervaren beveiligingsanalisten zelfs Hallo en voor veel is harde tooeven weet waar toobegin.</span><span class="sxs-lookup"><span data-stu-id="9b17b-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="9b17b-105">Met behulp van [analytics](security-center-detection-capabilities.md) tooconnect Hallo informatie tussen verschillende [beveiligingswaarschuwingen](security-center-managing-and-responding-alerts.md), Security Center kunt u kennismaken met één enkele weergave van een campagne aanval en alle Hallo gerelateerde waarschuwingen – u kunt snel inzicht in welke acties Hallo aanvaller vond en welke bronnen zijn veranderd.</span><span class="sxs-lookup"><span data-stu-id="9b17b-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="9b17b-106">Dit document wordt beschreven hoe toouse beveiliging mogelijkheden in Security Center tooassist waarschuwt u afhandelen van beveiligingsincidenten.</span><span class="sxs-lookup"><span data-stu-id="9b17b-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="9b17b-107">Wat is een beveiligingsincident?</span><span class="sxs-lookup"><span data-stu-id="9b17b-107">What is a security incident?</span></span>
<span data-ttu-id="9b17b-108">In het Beveiligingscentrum is een beveiligingsincident een samenloop van alle waarschuwingen voor een resource die overeenstemt met [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)-patronen.</span><span class="sxs-lookup"><span data-stu-id="9b17b-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="9b17b-109">Incidenten verschijnen in Hallo [beveiligingswaarschuwingen](security-center-managing-and-responding-alerts.md) tegel en blade.</span><span class="sxs-lookup"><span data-stu-id="9b17b-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="9b17b-110">Een Incident onthullen Hallo lijst met verwante waarschuwingen, waarmee u tooobtain meer informatie over elk exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9b17b-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="9b17b-111">Beveiligingsincidenten beheren</span><span class="sxs-lookup"><span data-stu-id="9b17b-111">Managing security incidents</span></span>
<span data-ttu-id="9b17b-112">U kunt uw huidige beveiligingsincidenten controleren door te kijken Hallo waarschuwingen beveiligingstegel.</span><span class="sxs-lookup"><span data-stu-id="9b17b-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="9b17b-113">Toegang tot hello Azure-Portal en stappen Hallo hieronder toosee meer informatie over elk beveiligingsincident:</span><span class="sxs-lookup"><span data-stu-id="9b17b-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="9b17b-114">Op Hallo Security Center-dashboard, ziet u Hallo **beveiligingswaarschuwingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="9b17b-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![De tegel Beveiligingswaarschuwingen in Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="9b17b-116">Klik op deze tegel tooexpand en als een beveiligingsincident voordoet wordt gedetecteerd, wordt deze weergegeven bij Hallo beveiliging waarschuwingen grafiek zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9b17b-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="9b17b-118">U ziet dat Hallo security incident beschrijving een ander pictogram heeft vergeleken tooother waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9b17b-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="9b17b-119">Klik op het tooview om meer details over dit incident.</span><span class="sxs-lookup"><span data-stu-id="9b17b-119">Click on it tooview more details about this incident.</span></span>

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="9b17b-121">Op Hallo **incident** blade u meer ziet details over deze veiligheidsincident, waaronder de volledige beschrijving, de ernst (die in dit geval is hoog), de huidige status (in dit geval is nog steeds *active*, een actie tooit die impliceert Hallo gebruiker nog niet uitgevoerde - kunt u dit doen met de rechtermuisknop te klikken op Hallo incident in Hallo **beveiligingswaarschuwingen** blade), Hallo aangevallen resource (in dit geval *VM1*), Hallo herstelstappen voor Hallo incident en in Hallo onderste deelvenster hebt u Hallo-waarschuwingen die zijn opgenomen in dit incident.</span><span class="sxs-lookup"><span data-stu-id="9b17b-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="9b17b-122">Als u meer informatie over elke waarschuwing tooobtain wilt, wordt Klik op het bestand en een andere blade geopend, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9b17b-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="9b17b-124">Hallo-informatie over deze blade varieert volgens toohello waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="9b17b-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="9b17b-125">Lees [beheren en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) voor meer informatie over het toomanage deze waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9b17b-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="9b17b-126">Enkele belangrijke overwegingen met betrekking tot deze mogelijkheid:</span><span class="sxs-lookup"><span data-stu-id="9b17b-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="9b17b-127">Een nieuw filter kunt u uw weergave tooIncident alleen waarschuwingen alleen toocustomize of beide.</span><span class="sxs-lookup"><span data-stu-id="9b17b-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="9b17b-128">Hallo dezelfde waarschuwing als onderdeel van een Incident (indien van toepassing), evenals de toobe zichtbaar als een zelfstandige waarschuwing kan bestaan.</span><span class="sxs-lookup"><span data-stu-id="9b17b-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="9b17b-129">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9b17b-129">See also</span></span>
<span data-ttu-id="9b17b-130">In dit document hebt u geleerd hoe toouse Hallo security incident mogelijkheden in Security Center.</span><span class="sxs-lookup"><span data-stu-id="9b17b-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="9b17b-131">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="9b17b-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="9b17b-132">Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9b17b-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="9b17b-133">Detectiemogelijkheden van Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9b17b-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="9b17b-134">Plannings- en bedieningsgids voor Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9b17b-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="9b17b-135">Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9b17b-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="9b17b-136">[Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="9b17b-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="9b17b-137">[Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.</span><span class="sxs-lookup"><span data-stu-id="9b17b-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
