---
title: Azure Active Directory-rapportage latenties | Microsoft Docs
description: Meer informatie over de hoeveelheid tijd die nodig is voor rapportage gebeurtenissen worden weergegeven in uw Azure-portal
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="c4b26-103">Azure Active Directory-rapportage latenties</span><span class="sxs-lookup"><span data-stu-id="c4b26-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="c4b26-104">Met [reporting](active-directory-preview-explainer.md) in Azure Active Directory, dat u alle informatie die u nodig hebt om te bepalen hoe uw omgeving doet.</span><span class="sxs-lookup"><span data-stu-id="c4b26-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="c4b26-105">De hoeveelheid tijd die nodig is voor het melden van gegevens worden weergegeven in de Azure-portal wordt ook wel latentie.</span><span class="sxs-lookup"><span data-stu-id="c4b26-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="c4b26-106">Dit onderwerp worden de latentie-informatie voor de categorieën alle rapportage in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c4b26-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="c4b26-107">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="c4b26-107">Activity reports</span></span>

<span data-ttu-id="c4b26-108">Er zijn twee gebieden van de activiteit reporting:</span><span class="sxs-lookup"><span data-stu-id="c4b26-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="c4b26-109">**Aanmeldactiviteiten**: informatie over het gebruik van beheerde toepassingen en aanmeldactiviteiten van gebruikers</span><span class="sxs-lookup"><span data-stu-id="c4b26-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="c4b26-110">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten</span><span class="sxs-lookup"><span data-stu-id="c4b26-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="c4b26-111">De volgende tabel bevat de latentie-informatie voor activiteitsrapporten.</span><span class="sxs-lookup"><span data-stu-id="c4b26-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="c4b26-112">Rapport</span><span class="sxs-lookup"><span data-stu-id="c4b26-112">Report</span></span> | <span data-ttu-id="c4b26-113">Minimum</span><span class="sxs-lookup"><span data-stu-id="c4b26-113">Minimum</span></span> | <span data-ttu-id="c4b26-114">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="c4b26-114">Average</span></span> | <span data-ttu-id="c4b26-115">Maximum</span><span class="sxs-lookup"><span data-stu-id="c4b26-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="c4b26-116">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="c4b26-116">Audit logs</span></span>             | <span data-ttu-id="c4b26-117">30 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-117">30 minutes</span></span>  | <span data-ttu-id="c4b26-118">45 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-118">45 Minutes</span></span> | <span data-ttu-id="c4b26-119">1 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-119">1 hour</span></span>     |
| <span data-ttu-id="c4b26-120">Aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="c4b26-120">Sign-ins</span></span>               | <span data-ttu-id="c4b26-121">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-121">15 minutes</span></span>  | <span data-ttu-id="c4b26-122">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-122">15 minutes</span></span> | <span data-ttu-id="c4b26-123">2 uur *</span><span class="sxs-lookup"><span data-stu-id="c4b26-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="c4b26-124">Als de aanmeldactiviteitgegevens afkomstig zijn van verouderde Office-toepassingen, kan het tot acht uur duren voor de rapportagegegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4b26-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="c4b26-125">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="c4b26-125">Security reports</span></span>

<span data-ttu-id="c4b26-126">Er zijn twee soorten beveiliging reporting:</span><span class="sxs-lookup"><span data-stu-id="c4b26-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="c4b26-127">**Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="c4b26-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="c4b26-128">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="c4b26-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="c4b26-129">De volgende tabel bevat de latentie-informatie voor beveiligingsrapporten.</span><span class="sxs-lookup"><span data-stu-id="c4b26-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="c4b26-130">Rapport</span><span class="sxs-lookup"><span data-stu-id="c4b26-130">Report</span></span> | <span data-ttu-id="c4b26-131">Minimum</span><span class="sxs-lookup"><span data-stu-id="c4b26-131">Minimum</span></span> | <span data-ttu-id="c4b26-132">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="c4b26-132">Average</span></span> | <span data-ttu-id="c4b26-133">Maximum</span><span class="sxs-lookup"><span data-stu-id="c4b26-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="c4b26-134">Gebruikers die risico lopen</span><span class="sxs-lookup"><span data-stu-id="c4b26-134">Users at risk</span></span>          | <span data-ttu-id="c4b26-135">5 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-135">5 minutes</span></span>   | <span data-ttu-id="c4b26-136">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-136">15 minutes</span></span>  | <span data-ttu-id="c4b26-137">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-137">2 hours</span></span>  |
| <span data-ttu-id="c4b26-138">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="c4b26-138">Risky sign-ins</span></span>         | <span data-ttu-id="c4b26-139">5 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-139">5 minutes</span></span>   | <span data-ttu-id="c4b26-140">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-140">15 minutes</span></span>  | <span data-ttu-id="c4b26-141">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="c4b26-142">Risico 's</span><span class="sxs-lookup"><span data-stu-id="c4b26-142">Risk events</span></span>

<span data-ttu-id="c4b26-143">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek voor het detecteren van verdachte acties die zijn gekoppeld aan uw gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c4b26-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="c4b26-144">Elke verdachte actie wordt opgeslagen in een gebeurtenis vastleggen genoemd risico gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c4b26-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="c4b26-145">De volgende tabel bevat de latentie-informatie voor risico's.</span><span class="sxs-lookup"><span data-stu-id="c4b26-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="c4b26-146">Rapport</span><span class="sxs-lookup"><span data-stu-id="c4b26-146">Report</span></span> | <span data-ttu-id="c4b26-147">Minimum</span><span class="sxs-lookup"><span data-stu-id="c4b26-147">Minimum</span></span> | <span data-ttu-id="c4b26-148">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="c4b26-148">Average</span></span> | <span data-ttu-id="c4b26-149">Maximum</span><span class="sxs-lookup"><span data-stu-id="c4b26-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="c4b26-150">Aanmeldingen vanaf anonieme IP-adressen</span><span class="sxs-lookup"><span data-stu-id="c4b26-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="c4b26-151">5 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-151">5 minutes</span></span> |<span data-ttu-id="c4b26-152">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-152">15 Minutes</span></span> |<span data-ttu-id="c4b26-153">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-153">2 hours</span></span> |
| <span data-ttu-id="c4b26-154">Aanmeldingen vanaf onbekende locaties</span><span class="sxs-lookup"><span data-stu-id="c4b26-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="c4b26-155">5 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-155">5 minutes</span></span> |<span data-ttu-id="c4b26-156">15 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-156">15 Minutes</span></span> |<span data-ttu-id="c4b26-157">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-157">2 hours</span></span> |
| <span data-ttu-id="c4b26-158">Gebruikers van wie de referenties zijn gelekt</span><span class="sxs-lookup"><span data-stu-id="c4b26-158">Users with leaked credentials</span></span> |<span data-ttu-id="c4b26-159">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-159">2 hours</span></span> |<span data-ttu-id="c4b26-160">4 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-160">4 hours</span></span> |<span data-ttu-id="c4b26-161">8 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-161">8 hours</span></span> |
| <span data-ttu-id="c4b26-162">Onmogelijke reis naar ongewone locaties</span><span class="sxs-lookup"><span data-stu-id="c4b26-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="c4b26-163">5 minuten</span><span class="sxs-lookup"><span data-stu-id="c4b26-163">5 minutes</span></span> |<span data-ttu-id="c4b26-164">1 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-164">1 hour</span></span> |<span data-ttu-id="c4b26-165">8 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-165">8 hours</span></span>  |
| <span data-ttu-id="c4b26-166">Aanmeldingen vanaf geïnfecteerde apparaten</span><span class="sxs-lookup"><span data-stu-id="c4b26-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="c4b26-167">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-167">2 hours</span></span> |<span data-ttu-id="c4b26-168">4 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-168">4 hours</span></span> |<span data-ttu-id="c4b26-169">8 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-169">8 hours</span></span>  |
| <span data-ttu-id="c4b26-170">Aanmeldingen vanaf IP-adressen met verdachte activiteiten</span><span class="sxs-lookup"><span data-stu-id="c4b26-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="c4b26-171">2 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-171">2 hours</span></span> |<span data-ttu-id="c4b26-172">4 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-172">4 hours</span></span> |<span data-ttu-id="c4b26-173">8 uur</span><span class="sxs-lookup"><span data-stu-id="c4b26-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="c4b26-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4b26-174">Next steps</span></span>

<span data-ttu-id="c4b26-175">Als u meer weten over de activiteitsrapporten in de Azure portal wilt, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="c4b26-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="c4b26-176">Aanmeldingsactiviteiten rapporten in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="c4b26-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="c4b26-177">Controlerapporten van activiteit in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="c4b26-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="c4b26-178">Als u meer weten over de beveiligingsrapporten in de Azure portal wilt, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="c4b26-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="c4b26-179">Gebruikers op beveiligingsrapport risico's in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="c4b26-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="c4b26-180">Riskant aanmeldingen rapport in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="c4b26-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="c4b26-181">Als u meer weten over de risico's wilt, Zie [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="c4b26-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
