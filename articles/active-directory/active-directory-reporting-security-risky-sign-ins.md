---
title: Rapport Riskante aanmeldingen in de Azure Active Directory-portal | Microsoft Docs
description: Meer informatie over het rapport Riskante aanmeldingen in de Azure Active Directory-portal
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 45a6f63bd920c9a70c25b8dfae084ea030256cf4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="14822-103">Het rapport Riskante aanmeldingen in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="14822-103">Risky sign-ins report in the Azure Active Directory portal</span></span>

<span data-ttu-id="14822-104">Met de beveiligingsrapporten in Azure Active Directory (Azure AD) krijgt u inzicht in de kans op verdachte gebruikersaccounts in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="14822-104">With the security reports in Azure Active Directory (Azure AD) you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="14822-105">Azure AD detecteert verdachte activiteit die is gekoppeld aan uw gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="14822-105">Azure AD detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="14822-106">Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14822-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="14822-107">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14822-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="14822-108">De gedetecteerde risico's worden gebruikt om het volgende te berekenen:</span><span class="sxs-lookup"><span data-stu-id="14822-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="14822-109">**Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="14822-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="14822-110">Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14822-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="14822-111">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="14822-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="14822-112">Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14822-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="14822-113">In [Azure Portal](https://portal.azure.com) kunt u de beveiligingsrapporten vinden op de blade **Azure Active Directory** in het gedeelte **Beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="14822-113">In [the Azure portal](https://portal.azure.com), you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span> 

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="14822-115">Welke Azure AD-licentie heb ik nodig voor toegang tot een beveiligingsrapport?</span><span class="sxs-lookup"><span data-stu-id="14822-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="14822-116">Alle edities van Azure Active Directory bieden rapporten over riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="14822-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="14822-117">Het detailniveau van rapporten verschilt wel per editie:</span><span class="sxs-lookup"><span data-stu-id="14822-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="14822-118">Bij de edities **Azure Active Directory Free en Basic** krijgt u al een lijst met riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="14822-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="14822-119">De editie **Azure Active Directory Premium 1** bevat een uitgebreider model waarmee u ook bepaalde onderliggende risicogebeurtenissen kunt onderzoeken die voor elk rapport zijn gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="14822-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="14822-120">De editie **Azure Active Directory Premium 2** biedt u de meest gedetailleerde informatie over alle onderliggende risicogebeurtenissen. Deze editie stelt u ook in staat beveiligingsbeleidsregels te configureren die automatisch op de geconfigureerde risiconiveaus reageren.</span><span class="sxs-lookup"><span data-stu-id="14822-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="14822-121">Gratis en Basic edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14822-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="14822-122">De edities Gratis en Basic van Azure Active Directory bieden u een lijst met riskante aanmeldingen die zijn gedetecteerd voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="14822-122">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="14822-123">Dit rapport bevat:</span><span class="sxs-lookup"><span data-stu-id="14822-123">This report lists:</span></span>

- <span data-ttu-id="14822-124">**Gebruiker**: de naam van de gebruiker die is gebruikt tijdens het aanmelden</span><span class="sxs-lookup"><span data-stu-id="14822-124">**User** - The name of the user that was used during the sign-in operation</span></span>
- <span data-ttu-id="14822-125">**IP**: het IP-adres van het apparaat dat is gebruikt om verbinding te maken met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14822-125">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="14822-126">**Locatie**: de locatie die is gebruikt om verbinding te maken met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14822-126">**Location** - The location used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="14822-127">**Tijd van aanmelden**: de tijd waarop de aanmelding heeft plaatsgevonden</span><span class="sxs-lookup"><span data-stu-id="14822-127">**Sign-in time** - The time when the sign-in was performed</span></span>
- <span data-ttu-id="14822-128">**Status**: de status van de aanmelding</span><span class="sxs-lookup"><span data-stu-id="14822-128">**Status** - The status of the sign-in</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="14822-130">Op basis van uw onderzoek van de riskante aanmelding kunt u uw feedback naar Azure Active Directory sturen door een van de volgende acties te ondernemen:</span><span class="sxs-lookup"><span data-stu-id="14822-130">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span></span>

- <span data-ttu-id="14822-131">Oplossen</span><span class="sxs-lookup"><span data-stu-id="14822-131">Resolve</span></span>
- <span data-ttu-id="14822-132">Markeren als fout-positief</span><span class="sxs-lookup"><span data-stu-id="14822-132">Mark as false positive</span></span>
- <span data-ttu-id="14822-133">Negeren</span><span class="sxs-lookup"><span data-stu-id="14822-133">Ignore</span></span>
- <span data-ttu-id="14822-134">Opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="14822-134">Reactivate</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="14822-136">Zie voor meer informatie [Risico's handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="14822-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="14822-137">Dit rapport biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="14822-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="14822-138">Resources zoeken</span><span class="sxs-lookup"><span data-stu-id="14822-138">Searh resources</span></span>
- <span data-ttu-id="14822-139">De rapportgegevens downloaden</span><span class="sxs-lookup"><span data-stu-id="14822-139">Download the report data</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="14822-141">Premium edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14822-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="14822-142">Het rapport Riskante aanmeldingen in de Azure Active Directory-portal biedt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="14822-142">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="14822-143">Verzamelde informatie over de gedetecteerde [risicogebeurtenistypen](active-directory-identity-protection-risk-events.md)</span><span class="sxs-lookup"><span data-stu-id="14822-143">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="14822-144">Een optie voor het downloaden van het rapport</span><span class="sxs-lookup"><span data-stu-id="14822-144">An option to download the report</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="14822-146">Wanneer u een risicogebeurtenis selecteert, krijgt u een gedetailleerde rapportweergave voor deze risicogebeurtenis waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="14822-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="14822-147">Een optie voor het configureren van een [beleid voor herstel van gebruikersrisico's](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="14822-147">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="14822-148">De detectietijdlijn voor de risicogebeurtenis bekijken</span><span class="sxs-lookup"><span data-stu-id="14822-148">Review the detection timeline for the risk event</span></span>  

- <span data-ttu-id="14822-149">Een lijst met gebruikers bekijken waarvoor deze risicogebeurtenis is gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="14822-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="14822-150">[Risicogebeurtenissen handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually) of een handmatig gesloten risicogebeurtenis opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="14822-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="14822-152">Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="14822-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="14822-153">De weergave Alle aanmeldingen openen</span><span class="sxs-lookup"><span data-stu-id="14822-153">Open the All sign-ins view</span></span>

- <span data-ttu-id="14822-154">Het gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="14822-154">Reset the user's password</span></span>

- <span data-ttu-id="14822-155">Alle gebeurtenissen sluiten</span><span class="sxs-lookup"><span data-stu-id="14822-155">Dismiss all events</span></span>

- <span data-ttu-id="14822-156">De gemelde risico's voor de gebruiker onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="14822-156">Investigate reported risk events for the user.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="14822-158">Selecteer in de lijst de risicogebeurtenis die u wilt onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="14822-158">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="14822-159">Hiermee opent u de blade **Details** voor deze risicogebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="14822-159">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="14822-160">Op de blade **Details** kunt u een [risicogebeurtenis handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually) of een handmatig gesloten risicogebeurtenis opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="14822-160">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="14822-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14822-162">Next steps</span></span>

- <span data-ttu-id="14822-163">Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="14822-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

