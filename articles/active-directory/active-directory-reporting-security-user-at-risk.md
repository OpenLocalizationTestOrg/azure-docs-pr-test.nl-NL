---
title: aaaUsers gemarkeerd voor beveiligingsrapport risico's in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Meer informatie over het Hallo-gebruikers die zijn gemarkeerd voor risico beveiligingsrapport in hello Azure Active Directory-portal
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
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="5764f-103">Gebruikers die zijn gemarkeerd voor risico beveiligingsrapport in hello Azure Active Directory-portal</span><span class="sxs-lookup"><span data-stu-id="5764f-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="5764f-104">Met de Hallo beveiligingsrapporten in hello Azure Active Directory (Azure AD) krijgt u inzicht in de kans op Hallo van verdachte gebruikersaccounts in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5764f-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="5764f-105">Azure Active Directory detecteert verdachte acties die gerelateerd tooyour gebruikersaccounts zijn.</span><span class="sxs-lookup"><span data-stu-id="5764f-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="5764f-106">Voor elke gedetecteerde activiteit wordt een record met de naam *risicogebeurtenis* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5764f-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="5764f-107">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5764f-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="5764f-108">Hallo gedetecteerd risicogebeurtenissen gebruikte toocalculate zijn:</span><span class="sxs-lookup"><span data-stu-id="5764f-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="5764f-109">**Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5764f-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="5764f-110">Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5764f-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="5764f-111">**Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="5764f-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="5764f-112">Zie [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-identityprotection.md#users-flagged-for-risk) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5764f-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="5764f-113">In hello Azure-portal, kunt u vinden Hallo beveiliging rapporten over Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="5764f-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="5764f-115">Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?</span><span class="sxs-lookup"><span data-stu-id="5764f-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="5764f-116">Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen.</span><span class="sxs-lookup"><span data-stu-id="5764f-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="5764f-117">Hallo-niveau van rapportgranulatie is echter van Hallo edities:</span><span class="sxs-lookup"><span data-stu-id="5764f-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="5764f-118">In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst met gebruikers die zijn gemarkeerd voor risico's.</span><span class="sxs-lookup"><span data-stu-id="5764f-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="5764f-119">Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport.</span><span class="sxs-lookup"><span data-stu-id="5764f-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="5764f-120">Hallo **Azure Active Directory Premium 2** -versie Hallo meest gedetailleerde informatie over alle onderliggende risicogebeurtenissen en kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured risico reageren niveaus.</span><span class="sxs-lookup"><span data-stu-id="5764f-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="5764f-121">Gratis en Basic edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5764f-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="5764f-122">Hallo-gebruikers die zijn gemarkeerd voor risico rapport in de gratis en basic-edities van Azure Active Directory Hallo biedt u een lijst met gebruikersaccounts die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="5764f-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="5764f-124">Als u een gebruiker selecteert, wordt Hallo gerelateerde gebruiker gegevens blade geopend.</span><span class="sxs-lookup"><span data-stu-id="5764f-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="5764f-125">U kunt voor gebruikers die risico lopen van Hallo gebruiker aanmelden geschiedenis bekijken en Hallo wachtwoord opnieuw instellen als nodig.</span><span class="sxs-lookup"><span data-stu-id="5764f-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="5764f-127">Dit rapport biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="5764f-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="5764f-128">Hallo rapport downloaden</span><span class="sxs-lookup"><span data-stu-id="5764f-128">Download hello report</span></span>

- <span data-ttu-id="5764f-129">Gebruikers zoeken</span><span class="sxs-lookup"><span data-stu-id="5764f-129">Search users</span></span>

![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="5764f-131">Premium edities van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5764f-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="5764f-132">Hallo-gebruikers die zijn gemarkeerd voor risico rapport in Azure Active Directory premium-edities Hallo beschikt u over:</span><span class="sxs-lookup"><span data-stu-id="5764f-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="5764f-133">Een [lijst met gebruikersaccounts](active-directory-identityprotection.md#users-flagged-for-risk) die mogelijk zijn aangetast</span><span class="sxs-lookup"><span data-stu-id="5764f-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="5764f-134">Informatie over Hallo geaggregeerd [risico gebeurtenistypen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="5764f-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="5764f-135">Een optie toodownload Hallo-rapport</span><span class="sxs-lookup"><span data-stu-id="5764f-135">An option toodownload hello report</span></span>

- <span data-ttu-id="5764f-136">Een optie tooconfigure een [gebruikersbeleid risico herstel](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="5764f-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="5764f-138">Wanneer u een gebruiker selecteert, krijgt u een gedetailleerde rapportweergave voor deze gebruiker waarmee u het volgende kunt:</span><span class="sxs-lookup"><span data-stu-id="5764f-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="5764f-139">Open Hallo alle aanmeldingen weergeven</span><span class="sxs-lookup"><span data-stu-id="5764f-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="5764f-140">Hallo gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="5764f-140">Reset hello user's password</span></span>

- <span data-ttu-id="5764f-141">Alle gebeurtenissen sluiten</span><span class="sxs-lookup"><span data-stu-id="5764f-141">Dismiss all events</span></span>

- <span data-ttu-id="5764f-142">Onderzoek gemelde risicogebeurtenissen voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5764f-142">Investigate reported risk events for hello user.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="5764f-144">tooinvestigate een risicogebeurtenis, selecteer een optie uit Hallo lijst tooopen hello **Details** blade voor deze risicogebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5764f-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="5764f-145">Op Hallo **Details** blade hebt Hallo optie tooeither [handmatig sluit een risicogebeurtenis](active-directory-identityprotection.md#closing-risk-events-manually) of opnieuw activeren van een risicogebeurtenis handmatig gesloten.</span><span class="sxs-lookup"><span data-stu-id="5764f-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskante aanmeldingen](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="5764f-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5764f-147">Next steps</span></span>

- <span data-ttu-id="5764f-148">Zie [Azure Active Directory Identity Protection](active-directory-identityprotection.md) voor meer informatie over Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="5764f-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

