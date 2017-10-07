---
title: aaaAzure Active Directory-rapportage latenties | Microsoft Docs
description: Meer informatie over Hallo hoeveelheid tijd die nodig is voor het melden van gebeurtenissen tooshow up in uw Azure-portal
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="de161-103">Azure Active Directory-rapportage latenties</span><span class="sxs-lookup"><span data-stu-id="de161-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="de161-104">Met [reporting](active-directory-preview-explainer.md) hello Azure Active Directory, u alle benodigde toodetermine hoe uw omgeving doet Hallo gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="de161-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="de161-105">Hallo hoeveelheid tijd die nodig is voor het melden van gegevens tooshow omhoog in hello Azure-portal wordt ook wel latentie.</span><span class="sxs-lookup"><span data-stu-id="de161-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="de161-106">Dit onderwerp staan Hallo latentiegegevens Hallo alle reporting categorieën in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="de161-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="de161-107">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="de161-107">Activity reports</span></span>

<span data-ttu-id="de161-108">Er zijn twee gebieden van de activiteit reporting:</span><span class="sxs-lookup"><span data-stu-id="de161-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="de161-109">**Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden</span><span class="sxs-lookup"><span data-stu-id="de161-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="de161-110">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten</span><span class="sxs-lookup"><span data-stu-id="de161-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="de161-111">Hallo volgende tabel vindt u Hallo latentiegegevens voor activiteitsrapporten.</span><span class="sxs-lookup"><span data-stu-id="de161-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="de161-112">Rapport</span><span class="sxs-lookup"><span data-stu-id="de161-112">Report</span></span> | <span data-ttu-id="de161-113">Minimum</span><span class="sxs-lookup"><span data-stu-id="de161-113">Minimum</span></span> | <span data-ttu-id="de161-114">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="de161-114">Average</span></span> | <span data-ttu-id="de161-115">Maximum</span><span class="sxs-lookup"><span data-stu-id="de161-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="de161-116">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="de161-116">Audit logs</span></span>             | <span data-ttu-id="de161-117">30 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-117">30 minutes</span></span>  | <span data-ttu-id="de161-118">45 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-118">45 Minutes</span></span> | <span data-ttu-id="de161-119">1 uur</span><span class="sxs-lookup"><span data-stu-id="de161-119">1 hour</span></span>     |
| <span data-ttu-id="de161-120">Aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="de161-120">Sign-ins</span></span>               | <span data-ttu-id="de161-121">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-121">15 minutes</span></span>  | <span data-ttu-id="de161-122">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-122">15 minutes</span></span> | <span data-ttu-id="de161-123">2 uur *</span><span class="sxs-lookup"><span data-stu-id="de161-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="de161-124">Voor sommige activiteitsgegevens voor aanmeldingen afkomstig is van de oudere office-toepassingen, kan het Hallo gegevens tooshow rapporteert too8 uur duren voordat.</span><span class="sxs-lookup"><span data-stu-id="de161-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="de161-125">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="de161-125">Security reports</span></span>

<span data-ttu-id="de161-126">Er zijn twee soorten beveiliging reporting:</span><span class="sxs-lookup"><span data-stu-id="de161-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="de161-127">**Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="de161-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="de161-128">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="de161-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="de161-129">Hallo volgende tabel geeft een lijst Hallo latentiegegevens beveiligingsrapporten.</span><span class="sxs-lookup"><span data-stu-id="de161-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="de161-130">Rapport</span><span class="sxs-lookup"><span data-stu-id="de161-130">Report</span></span> | <span data-ttu-id="de161-131">Minimum</span><span class="sxs-lookup"><span data-stu-id="de161-131">Minimum</span></span> | <span data-ttu-id="de161-132">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="de161-132">Average</span></span> | <span data-ttu-id="de161-133">Maximum</span><span class="sxs-lookup"><span data-stu-id="de161-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="de161-134">Gebruikers die risico lopen</span><span class="sxs-lookup"><span data-stu-id="de161-134">Users at risk</span></span>          | <span data-ttu-id="de161-135">5 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-135">5 minutes</span></span>   | <span data-ttu-id="de161-136">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-136">15 minutes</span></span>  | <span data-ttu-id="de161-137">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-137">2 hours</span></span>  |
| <span data-ttu-id="de161-138">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="de161-138">Risky sign-ins</span></span>         | <span data-ttu-id="de161-139">5 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-139">5 minutes</span></span>   | <span data-ttu-id="de161-140">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-140">15 minutes</span></span>  | <span data-ttu-id="de161-141">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="de161-142">Risico 's</span><span class="sxs-lookup"><span data-stu-id="de161-142">Risk events</span></span>

<span data-ttu-id="de161-143">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect verdachte acties die gerelateerd tooyour gebruikersaccounts zijn.</span><span class="sxs-lookup"><span data-stu-id="de161-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="de161-144">Elke verdachte actie wordt opgeslagen in een gebeurtenis vastleggen genoemd risico gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="de161-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="de161-145">Hallo volgende tabel geeft een lijst Hallo latentiegegevens risico's.</span><span class="sxs-lookup"><span data-stu-id="de161-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="de161-146">Rapport</span><span class="sxs-lookup"><span data-stu-id="de161-146">Report</span></span> | <span data-ttu-id="de161-147">Minimum</span><span class="sxs-lookup"><span data-stu-id="de161-147">Minimum</span></span> | <span data-ttu-id="de161-148">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="de161-148">Average</span></span> | <span data-ttu-id="de161-149">Maximum</span><span class="sxs-lookup"><span data-stu-id="de161-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="de161-150">Aanmeldingen vanaf anonieme IP-adressen</span><span class="sxs-lookup"><span data-stu-id="de161-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="de161-151">5 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-151">5 minutes</span></span> |<span data-ttu-id="de161-152">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-152">15 Minutes</span></span> |<span data-ttu-id="de161-153">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-153">2 hours</span></span> |
| <span data-ttu-id="de161-154">Aanmeldingen vanaf onbekende locaties</span><span class="sxs-lookup"><span data-stu-id="de161-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="de161-155">5 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-155">5 minutes</span></span> |<span data-ttu-id="de161-156">15 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-156">15 Minutes</span></span> |<span data-ttu-id="de161-157">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-157">2 hours</span></span> |
| <span data-ttu-id="de161-158">Gebruikers van wie de referenties zijn gelekt</span><span class="sxs-lookup"><span data-stu-id="de161-158">Users with leaked credentials</span></span> |<span data-ttu-id="de161-159">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-159">2 hours</span></span> |<span data-ttu-id="de161-160">4 uur</span><span class="sxs-lookup"><span data-stu-id="de161-160">4 hours</span></span> |<span data-ttu-id="de161-161">8 uur</span><span class="sxs-lookup"><span data-stu-id="de161-161">8 hours</span></span> |
| <span data-ttu-id="de161-162">Onmogelijke reis tooatypical locaties</span><span class="sxs-lookup"><span data-stu-id="de161-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="de161-163">5 minuten</span><span class="sxs-lookup"><span data-stu-id="de161-163">5 minutes</span></span> |<span data-ttu-id="de161-164">1 uur</span><span class="sxs-lookup"><span data-stu-id="de161-164">1 hour</span></span> |<span data-ttu-id="de161-165">8 uur</span><span class="sxs-lookup"><span data-stu-id="de161-165">8 hours</span></span>  |
| <span data-ttu-id="de161-166">Aanmeldingen vanaf geïnfecteerde apparaten</span><span class="sxs-lookup"><span data-stu-id="de161-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="de161-167">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-167">2 hours</span></span> |<span data-ttu-id="de161-168">4 uur</span><span class="sxs-lookup"><span data-stu-id="de161-168">4 hours</span></span> |<span data-ttu-id="de161-169">8 uur</span><span class="sxs-lookup"><span data-stu-id="de161-169">8 hours</span></span>  |
| <span data-ttu-id="de161-170">Aanmeldingen van IP-adressen met verdachte activiteit</span><span class="sxs-lookup"><span data-stu-id="de161-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="de161-171">2 uur</span><span class="sxs-lookup"><span data-stu-id="de161-171">2 hours</span></span> |<span data-ttu-id="de161-172">4 uur</span><span class="sxs-lookup"><span data-stu-id="de161-172">4 hours</span></span> |<span data-ttu-id="de161-173">8 uur</span><span class="sxs-lookup"><span data-stu-id="de161-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="de161-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de161-174">Next steps</span></span>

<span data-ttu-id="de161-175">Als u meer over Hallo activiteitsrapporten in Azure-portal Hallo tooknow wilt, Zie:</span><span class="sxs-lookup"><span data-stu-id="de161-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="de161-176">Rapporten in Azure Active Directory-beheerportal Hallo aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="de161-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="de161-177">Activiteitsrapporten in Azure Active Directory-beheerportal Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="de161-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="de161-178">Als u meer informatie over de beveiligingsrapporten Hallo in hello Azure-portal tooknow wilt, Zie:</span><span class="sxs-lookup"><span data-stu-id="de161-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="de161-179">Gebruikers op risico beveiligingsrapport in hello Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="de161-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="de161-180">Rapport van riskante aanmeldingen in hello Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="de161-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="de161-181">Als u meer informatie over de risico's tooknow wilt, Zie [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="de161-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
