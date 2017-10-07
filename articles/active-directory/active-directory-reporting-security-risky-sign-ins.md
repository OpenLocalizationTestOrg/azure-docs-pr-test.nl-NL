---
title: aaaRisky aanmeldingen rapport in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Meer informatie over Hallo riskant aanmeldingen rapport in hello Azure Active Directory-portal
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
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="d9b5b-103">Rapport van riskante aanmeldingen in hello Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="d9b5b-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="d9b5b-104">Met de Hallo beveiligingsrapporten in Azure Active Directory (Azure AD) krijgt u inzicht in de kans op Hallo van verdachte gebruikersaccounts in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="d9b5b-105">Azure AD detecteert verdachte acties die gerelateerd tooyour gebruikersaccounts zijn.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="d9b5b-106">Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="d9b5b-107">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="d9b5b-108">Hallo gedetecteerd risicogebeurtenissen gebruikte toocalculate zijn:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="d9b5b-109">**Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="d9b5b-110">Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="d9b5b-111">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="d9b5b-112">Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="d9b5b-113">In [hello Azure-portal](https://portal.azure.com), vindt u Hallo beveiliging rapporten over Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="d9b5b-115">Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?</span><span class="sxs-lookup"><span data-stu-id="d9b5b-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="d9b5b-116">Alle edities van Azure Active Directory bieden rapporten over riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="d9b5b-117">Hallo-niveau van rapportgranulatie is echter van Hallo edities:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="d9b5b-118">In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst van riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="d9b5b-119">Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="d9b5b-120">Hallo **Azure Active Directory Premium 2** editie biedt u Hello meest gedetailleerde informatie weer over alle onderliggende risicogebeurtenissen en ook kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured reageren risiconiveaus.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="d9b5b-121">Gratis en Basic edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9b5b-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="d9b5b-122">Hello Azure Active Directory gratis edities en basic bieden u een lijst van riskante aanmeldingen die zijn gedetecteerd voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="d9b5b-123">Dit rapport bevat:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-123">This report lists:</span></span>

- <span data-ttu-id="d9b5b-124">**Gebruiker** - hello naam van het Hallo-gebruiker die is gebruikt tijdens het Hallo-in bewerking</span><span class="sxs-lookup"><span data-stu-id="d9b5b-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="d9b5b-125">**IP** -Hallo IP-adres van het Hallo-apparaat dat gebruikt tooconnect tooAzure Active Directory is</span><span class="sxs-lookup"><span data-stu-id="d9b5b-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="d9b5b-126">**Locatie** -Hallo-locatie gebruikt tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9b5b-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="d9b5b-127">**Tijd van aanmelden** -Hallo tijd wanneer dat aanmeldingspagina Hallo is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="d9b5b-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="d9b5b-128">**Status** -status van de aanmeldingspagina Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="d9b5b-128">**Status** - hello status of hello sign-in</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="d9b5b-130">Op basis van uw onderzoek van riskante aanmelden hello, kunt u feedback tooAzure Active Directory in de vorm van de volgende activiteiten Hallo bieden:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="d9b5b-131">Oplossen</span><span class="sxs-lookup"><span data-stu-id="d9b5b-131">Resolve</span></span>
- <span data-ttu-id="d9b5b-132">Markeren als fout-positief</span><span class="sxs-lookup"><span data-stu-id="d9b5b-132">Mark as false positive</span></span>
- <span data-ttu-id="d9b5b-133">Negeren</span><span class="sxs-lookup"><span data-stu-id="d9b5b-133">Ignore</span></span>
- <span data-ttu-id="d9b5b-134">Opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="d9b5b-134">Reactivate</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="d9b5b-136">Zie voor meer informatie [Risico's handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="d9b5b-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="d9b5b-137">Dit rapport biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="d9b5b-138">Resources zoeken</span><span class="sxs-lookup"><span data-stu-id="d9b5b-138">Searh resources</span></span>
- <span data-ttu-id="d9b5b-139">Hallo rapportgegevens downloaden</span><span class="sxs-lookup"><span data-stu-id="d9b5b-139">Download hello report data</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="d9b5b-141">Premium edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9b5b-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="d9b5b-142">Hallo riskant aanmeldingen rapport in Azure Active Directory premium-edities Hallo beschikt u over:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="d9b5b-143">Informatie over Hallo geaggregeerd [risico gebeurtenistypen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="d9b5b-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="d9b5b-144">Een optie toodownload Hallo-rapport</span><span class="sxs-lookup"><span data-stu-id="d9b5b-144">An option toodownload hello report</span></span>


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="d9b5b-146">Wanneer u een risicogebeurtenis selecteert, krijgt u een gedetailleerde rapportweergave voor deze risicogebeurtenis waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="d9b5b-147">Een optie tooconfigure een [gebruikersbeleid risico herstel](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="d9b5b-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="d9b5b-148">Hallo detectie tijdlijn voor Hallo risicogebeurtenis bekijken</span><span class="sxs-lookup"><span data-stu-id="d9b5b-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="d9b5b-149">Een lijst met gebruikers bekijken waarvoor deze risicogebeurtenis is gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="d9b5b-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="d9b5b-150">[Risicogebeurtenissen handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually) of een handmatig gesloten risicogebeurtenis opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="d9b5b-152">Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="d9b5b-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="d9b5b-153">Open Hallo alle aanmeldingen weergeven</span><span class="sxs-lookup"><span data-stu-id="d9b5b-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="d9b5b-154">Hallo gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="d9b5b-154">Reset hello user's password</span></span>

- <span data-ttu-id="d9b5b-155">Alle gebeurtenissen sluiten</span><span class="sxs-lookup"><span data-stu-id="d9b5b-155">Dismiss all events</span></span>

- <span data-ttu-id="d9b5b-156">Onderzoek gemelde risicogebeurtenissen voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-156">Investigate reported risk events for hello user.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="d9b5b-158">een risicogebeurtenis tooinvestigate geselecteerd in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="d9b5b-159">Hiermee opent u Hallo **Details** blade voor deze risicogebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="d9b5b-160">Op Hallo **Details** blade hebt Hallo optie tooeither [handmatig sluit een risicogebeurtenis](active-directory-identityprotection.md#closing-risk-events-manually) of opnieuw activeren van een risicogebeurtenis handmatig gesloten.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="d9b5b-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9b5b-162">Next steps</span></span>

- <span data-ttu-id="d9b5b-163">Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="d9b5b-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

