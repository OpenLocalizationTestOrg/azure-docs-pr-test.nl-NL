---
title: Beveiligingsrapport over gebruikers voor wie wordt aangegeven dat ze risico lopen in de Azure Active Directory-portal | Microsoft Docs
description: Meer informatie over het beveiligingsrapport over gebruikers voor wie wordt aangegeven dat ze risico lopen in de Azure Active Directory-portal
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="2d731-103">Beveiligingsrapport over gebruikers voor wie wordt aangegeven dat ze risico lopen in de Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="2d731-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="2d731-104">Met de beveiligingsrapporten in Azure Active Directory (Azure AD) krijgt u inzicht in de kans op verdachte gebruikersaccounts in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="2d731-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="2d731-105">Azure Active Directory detecteert verdachte activiteit die is gekoppeld aan uw gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2d731-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="2d731-106">Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2d731-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="2d731-107">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2d731-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="2d731-108">De gedetecteerde risico's worden gebruikt om het volgende te berekenen:</span><span class="sxs-lookup"><span data-stu-id="2d731-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="2d731-109">**Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="2d731-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="2d731-110">Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2d731-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="2d731-111">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="2d731-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="2d731-112">Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2d731-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="2d731-113">In Azure Portal kunt u de beveiligingsrapporten vinden op de blade **Azure Active Directory** in het gedeelte **Beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="2d731-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="2d731-115">Welke Azure AD-licentie heb ik nodig voor toegang tot een beveiligingsrapport?</span><span class="sxs-lookup"><span data-stu-id="2d731-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="2d731-116">Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen.</span><span class="sxs-lookup"><span data-stu-id="2d731-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="2d731-117">Het detailniveau van rapporten verschilt wel per editie:</span><span class="sxs-lookup"><span data-stu-id="2d731-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="2d731-118">In de edities **Azure Active Directory Free en Basic** hebt u toegang tot een lijst die gebruikers bevat voor wie wordt aangegeven dat ze risico lopen.</span><span class="sxs-lookup"><span data-stu-id="2d731-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="2d731-119">De editie **Azure Active Directory Premium 1** bevat een uitgebreider model waarmee u ook bepaalde onderliggende risicogebeurtenissen kunt onderzoeken die voor elk rapport zijn gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="2d731-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="2d731-120">De editie **Azure Active Directory Premium 2** biedt u de meest gedetailleerde informatie over alle onderliggende risicogebeurtenissen. Deze editie stelt u ook in staat beveiligingsbeleidsregels te configureren die automatisch op de geconfigureerde risiconiveaus reageren.</span><span class="sxs-lookup"><span data-stu-id="2d731-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="2d731-121">Gratis en Basic edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d731-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="2d731-122">Het rapport over gebruikers voor wie wordt aangegeven dat ze risico lopen in de gratis en Basic-editie van Azure Active Directory biedt een lijst gebruikersaccounts die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="2d731-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="2d731-124">Wanneer u op een gebruiker klikt, wordt de betreffende blade met gebruikersgegevens geopend.</span><span class="sxs-lookup"><span data-stu-id="2d731-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="2d731-125">Controleer de aanmeldgeschiedenis van gebruikers die risico lopen en stel het wachtwoord indien nodig opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="2d731-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="2d731-127">Dit rapport biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="2d731-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="2d731-128">Het rapport downloaden</span><span class="sxs-lookup"><span data-stu-id="2d731-128">Download the report</span></span>

- <span data-ttu-id="2d731-129">Gebruikers zoeken</span><span class="sxs-lookup"><span data-stu-id="2d731-129">Search users</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="2d731-131">Premium edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d731-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="2d731-132">Het rapport over gebruikers voor wie wordt aangegeven dat ze risico lopen in de Azure Active Directory Premium-edities biedt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="2d731-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="2d731-133">Een [lijst met gebruikersaccounts](active-directory-identityprotection.md#users-flagged-for-risk) die mogelijk zijn aangetast</span><span class="sxs-lookup"><span data-stu-id="2d731-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="2d731-134">Verzamelde informatie over de gedetecteerde [risicogebeurtenistypen](active-directory-identity-protection-risk-events.md)</span><span class="sxs-lookup"><span data-stu-id="2d731-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="2d731-135">Een optie voor het downloaden van het rapport</span><span class="sxs-lookup"><span data-stu-id="2d731-135">An option to download the report</span></span>

- <span data-ttu-id="2d731-136">Een optie voor het configureren van een [beleid voor herstel van gebruikersrisico's](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="2d731-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="2d731-138">Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="2d731-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="2d731-139">De weergave Alle aanmeldingen openen</span><span class="sxs-lookup"><span data-stu-id="2d731-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="2d731-140">Het gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="2d731-140">Reset the user's password</span></span>

- <span data-ttu-id="2d731-141">Alle gebeurtenissen sluiten</span><span class="sxs-lookup"><span data-stu-id="2d731-141">Dismiss all events</span></span>

- <span data-ttu-id="2d731-142">De gemelde risico's voor de gebruiker onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="2d731-142">Investigate reported risk events for the user.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="2d731-144">Als u een risicogebeurtenis wilt onderzoeken, selecteert u de gebeurtenis in de lijst om de bijbehorende blade **Details** te openen.</span><span class="sxs-lookup"><span data-stu-id="2d731-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="2d731-145">Op de blade **Details** kunt u een [risicogebeurtenis handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually) of een handmatig gesloten risicogebeurtenis opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="2d731-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="2d731-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d731-147">Next steps</span></span>

- <span data-ttu-id="2d731-148">Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="2d731-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

