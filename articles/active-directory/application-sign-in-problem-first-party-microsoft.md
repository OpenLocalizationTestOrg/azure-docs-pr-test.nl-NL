---
title: aaaProblems aanmelden tooa Microsoft-toepassing | Microsoft Docs
description: Algemene problemen geconfronteerd tijdens het aanmelden toofirst derden Microsoft Applications using Azure AD (zoals Office 365)
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="5eb77-103">Problemen met aanmelden tooa Microsoft-toepassing</span><span class="sxs-lookup"><span data-stu-id="5eb77-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="5eb77-104">Microsoft Applications (zoals Office 365 Exchange, SharePoint, Yammer, enzovoort) worden toegewezen en beheerd iets anders dan 3e SaaS-toepassingen van derden of andere toepassingen die u integreert met Azure AD voor eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="5eb77-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="5eb77-105">Er zijn drie manieren die een gebruiker toegang tot tooa Microsoft gepubliceerde toepassing krijgt.</span><span class="sxs-lookup"><span data-stu-id="5eb77-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="5eb77-106">Voor toepassingen in Hallo Office 365 of andere betaald suites gebruikers krijgen toegang via **licentie toewijzing** ofwel rechtstreeks tootheir-gebruikersaccount, of door een groep met onze toewijzing op basis van een groep licentie mogelijkheid.</span><span class="sxs-lookup"><span data-stu-id="5eb77-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="5eb77-107">Voor toepassingen die Microsoft of een derde partij vrijelijk voor iedereen toouse publiceert gebruikers mogelijk toegang worden verleend via **toestemming van de gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="5eb77-108">This0 betekent dat ze zich in de toepassing toohello met hun Azure AD werk of School-account en toohave toegang toosome beperkte set van gegevens op hun account toestaan.</span><span class="sxs-lookup"><span data-stu-id="5eb77-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="5eb77-109">Voor toepassingen die Microsoft of een 3rd Party vrijelijk voor iedereen toouse publiceert gebruikers kunnen ook toegang worden verleend via **beheerder toestemming**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="5eb77-110">Dit betekent dat een beheerder heeft vastgesteld Hallo toepassing kan worden gebruikt door iedereen in de organisatie hello, zodat ze zich in de toepassing toohello met een globale beheerdersaccount en tooeveryone in Hallo organisatie toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="5eb77-111">tootroubleshoot uw probleem, beginnen met Hallo [algemene probleemgebieden met toegang tot toepassingen tooconsider](#general-problem-areas-with-application-access-to-consider) en leest u Hallo [Walkthrough: stappen tootroubleshoot Microsoft Application toegang](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget in Hallo details.</span><span class="sxs-lookup"><span data-stu-id="5eb77-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="5eb77-112">Algemene probleemgebieden met toegang tot toepassingen tooconsider</span><span class="sxs-lookup"><span data-stu-id="5eb77-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="5eb77-113">Hieronder volgt een lijst van Hallo algemene probleemgebieden die u inzoomen kunt in als u al weet waar toostart, maar we raden u Hallo scenario tooget gaan snel lezen: [Walkthrough: stappen tootroubleshoot Microsoft Application toegang](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="5eb77-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="5eb77-114">Problemen met Hallo gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="5eb77-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="5eb77-115">Problemen met groepen</span><span class="sxs-lookup"><span data-stu-id="5eb77-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="5eb77-116">Problemen met het beleid voor voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="5eb77-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="5eb77-117">Problemen met toestemming van de toepassing</span><span class="sxs-lookup"><span data-stu-id="5eb77-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="5eb77-118">Stappen tootroubleshoot Microsoft Application toegang</span><span class="sxs-lookup"><span data-stu-id="5eb77-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="5eb77-119">Hieronder worden enkele veelvoorkomende problemen met mensen uitgevoerd in wanneer gebruikers zich niet tooa Microsoft-toepassing aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5eb77-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="5eb77-120">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="5eb77-120">General issues toocheck first</span></span>

  * <span data-ttu-id="5eb77-121">Zorg ervoor dat het Hallo-gebruiker zich aanmeldt toohello **Corrigeer URL** en niet de URL van een lokale toepassing.</span><span class="sxs-lookup"><span data-stu-id="5eb77-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="5eb77-122">Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="5eb77-123">Zorg ervoor dat Hallo **gebruikersaccount bestaat** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5eb77-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="5eb77-124">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="5eb77-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="5eb77-125">Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen. [Controleer de status van de account van een gebruiker](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="5eb77-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="5eb77-126">Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="5eb77-127">[Opnieuw instellen van het wachtwoord van een gebruiker](#reset-a-users-password) of [selfservice voor wachtwoordherstel inschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="5eb77-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="5eb77-128">Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5eb77-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="5eb77-129">[Controleer de status van een gebruiker multi-factor authentication-server](#check-a-users-multi-factor-authentication-status) of [contactgegevens van de verificatie van de gebruiker controleren](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="5eb77-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="5eb77-130">Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5eb77-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="5eb77-131">[Controleren van een specifieke voorwaardelijk toegangsbeleid](#problems-with-conditional-access-policies) of [beleid voor voorwaardelijke toegang van een specifieke toepassing controleren](#check-a-specific-applications-conditional-access-policy) of [beleid voor specifieke voorwaardelijke toegang uitschakelen](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="5eb77-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="5eb77-132">Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="5eb77-133">[Controleer de status van een gebruiker multi-factor authentication-server](#check-a-users-multi-factor-authentication-status) of [contactgegevens van de verificatie van de gebruiker controleren](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="5eb77-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="5eb77-134">Voor **Microsoft** **toepassingen waarvoor een licentie** (zoals Office365) worden hier zijn enkele specifieke problemen toocheck zodra u algemene problemen Hallo hierboven hebt uitgesloten:</span><span class="sxs-lookup"><span data-stu-id="5eb77-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="5eb77-135">Zorg ervoor dat de gebruiker Hallo of heeft een **licentie is toegewezen.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="5eb77-136">[Controleer de toegewezen licenties van een gebruiker](#check-a-users-assigned-licenses) of [controleren van de groep toegewezen licenties](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="5eb77-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="5eb77-137">Als het Hallo-licentie is **toegewezen tooa** **statische groep**, zorg ervoor dat Hallo **gebruiker lid is** van die groep.</span><span class="sxs-lookup"><span data-stu-id="5eb77-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="5eb77-138">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="5eb77-139">Als het Hallo-licentie is **toegewezen tooa** **dynamische groep**, zorg ervoor dat Hallo **dynamische groepsregel correct is ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="5eb77-140">Controleer de criteria voor lidmaatschap van een dynamische groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="5eb77-141">Als het Hallo-licentie is **toegewezen tooa** **dynamische groep**, ervoor zorgen dat dynamische groep Hallo heeft **verwerkt** lidmaatschap en die Hallo **gebruiker is een lid** (dit kan enige tijd duren).</span><span class="sxs-lookup"><span data-stu-id="5eb77-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="5eb77-142">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="5eb77-143">Nadat u ervoor te zorgen Hallo-licentie is toegewezen, zorg ervoor dat Hallo-licentie is **niet verlopen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="5eb77-144">Zorg ervoor dat het Hallo-licentie is **voor de toepassing hello** ze toegang hebben tot.</span><span class="sxs-lookup"><span data-stu-id="5eb77-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="5eb77-145">Voor **Microsoft** **toepassingen waarvoor een licentie niet**, hier zijn enkele andere dingen toocheck:</span><span class="sxs-lookup"><span data-stu-id="5eb77-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="5eb77-146">Als de toepassing hello aanvraagt **op gebruikersniveau machtigingen** (bijvoorbeeld ' toegang tot deze gebruiker Postvak'), zorg ervoor dat deze gebruiker Hallo toohello toepassing heeft aangemeld en heeft uitgevoerd een **op gebruikersniveau toestemming bewerking**  toolet Hallo toepassing toegang tot haar gegevens.</span><span class="sxs-lookup"><span data-stu-id="5eb77-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="5eb77-147">Als de toepassing hello aanvraagt **administratormachtigingen** (bijvoorbeeld ' toegang tot postvakken van alle gebruikers'), zorg ervoor dat een globale beheerder is uitgevoerd. een **bewerking op beheerdersniveau toestemming andere gebruikers van alle gebruikers** in Hallo-organisatie.</span><span class="sxs-lookup"><span data-stu-id="5eb77-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="5eb77-148">Problemen met Hallo gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="5eb77-148">Problems with hello user’s account</span></span>

<span data-ttu-id="5eb77-149">Toegang tot de toepassing kan vanwege een probleem met een gebruiker die is toegewezen toohello toepassing tooa worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="5eb77-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="5eb77-150">Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met gebruikers en hun Accountinstellingen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="5eb77-151">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="5eb77-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="5eb77-152">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="5eb77-153">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="5eb77-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="5eb77-154">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="5eb77-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="5eb77-155">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="5eb77-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="5eb77-156">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="5eb77-157">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="5eb77-158">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="5eb77-159">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="5eb77-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="5eb77-160">Controleer of er een gebruikersaccount in Azure Active Directory bestaat</span><span class="sxs-lookup"><span data-stu-id="5eb77-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="5eb77-161">toocheck als aanwezig is, is van een gebruikersaccount Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-162">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-163">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-164">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-165">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-166">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-166">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-167">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-168">Controleer de eigenschappen Hallo van Hallo gebruiker object toobe zeker van te zijn dat ze zo uitzien als u verwacht en er worden geen gegevens ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="5eb77-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="5eb77-169">Controleer de status van de account van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-169">Check a user’s account status</span></span>

<span data-ttu-id="5eb77-170">toocheck een gebruiker van account status, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-171">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-172">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-173">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-174">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-175">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-175">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-176">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-177">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-177">click **Profile**.</span></span>

8.  <span data-ttu-id="5eb77-178">Onder **instellingen** ervoor te zorgen dat **blok aanmelden** te is ingesteld,**Nee**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="5eb77-179">Een gebruiker-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="5eb77-179">Reset a user’s password</span></span>

<span data-ttu-id="5eb77-180">tooreset het gebruikerswachtwoord Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-181">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-182">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-183">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-184">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-185">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-185">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-186">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-187">Klik op Hallo **wachtwoord opnieuw instellen** knop bovenaan Hallo Hallo gebruiker blade.</span><span class="sxs-lookup"><span data-stu-id="5eb77-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="5eb77-188">Klik op Hallo **wachtwoord opnieuw instellen** knop op Hallo **wachtwoord opnieuw instellen** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5eb77-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="5eb77-189">Kopiëren Hallo **tijdelijk wachtwoord** of **een nieuw wachtwoord invoeren** voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5eb77-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="5eb77-190">Deze nieuwe gebruiker met wachtwoord toohello communiceren, kunnen ze vereist toochange dit wachtwoord tijdens de volgende aanmelden tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5eb77-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="5eb77-191">Selfservice voor wachtwoordherstel inschakelen</span><span class="sxs-lookup"><span data-stu-id="5eb77-191">Enable self-service password reset</span></span>

<span data-ttu-id="5eb77-192">tooenable zelf uw wachtwoord opnieuw instellen, Hallo implementatie volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="5eb77-193">Tooreset gebruikers hun wachtwoorden met Azure Active Directory inschakelen</span><span class="sxs-lookup"><span data-stu-id="5eb77-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="5eb77-194">Inschakelen van gebruikers tooreset of hun on-premises Active Directory wachtwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="5eb77-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="5eb77-195">Controleer de status van een gebruiker multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="5eb77-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="5eb77-196">toocheck een gebruiker de multi-factor authentication status, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-197">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-198">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-199">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-200">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-201">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-201">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-202">Klik op Hallo **multi-Factor Authentication** knop Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="5eb77-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="5eb77-203">Eenmaal Hallo **multi-factor Authentication-beheerportal** laadt, zorg ervoor dat u op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5eb77-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="5eb77-204">Hallo-gebruiker in de lijst met gebruikers Hallo vinden door te zoeken, filteren of sorteren.</span><span class="sxs-lookup"><span data-stu-id="5eb77-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="5eb77-205">Selecteer Hallo gebruiker uit Hallo lijst met gebruikers en **inschakelen**, **uitschakelen**, of **afdwingen** multi-factor authentication-server naar wens.</span><span class="sxs-lookup"><span data-stu-id="5eb77-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="5eb77-206">**Opmerking**: als een gebruiker zich in een **afgedwongen** staat, kunt u ze te instellen**uitgeschakelde** tijdelijk toolet deze terug te zetten bij hun account.</span><span class="sxs-lookup"><span data-stu-id="5eb77-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="5eb77-207">Wanneer ze terug in bent, kunt u wijzigen hun status te**ingeschakeld** opnieuw toorequire ze hun contactgegevens tijdens de volgende Meld u aan de toore registratie.</span><span class="sxs-lookup"><span data-stu-id="5eb77-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="5eb77-208">U kunt ook u kunt stappen Hallo in Hallo [controleren van de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info) tooverify of instellen van deze gegevens voor deze.</span><span class="sxs-lookup"><span data-stu-id="5eb77-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="5eb77-209">Controleer de contactgegevens van de verificatie van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="5eb77-210">verificatie van een gebruiker contactgegevens gebruikt voor multi-factor authentication, voorwaardelijke toegang, Identity Protection en het wachtwoord opnieuw instellen, toocheck Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-211">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-212">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-213">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-214">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-215">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-215">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-216">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-217">Klik op **profiel**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-217">click **Profile**.</span></span>

8.  <span data-ttu-id="5eb77-218">Schuif naar beneden te**verificatie contactgegevens**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="5eb77-219">**Bekijk** Hallo gegevens geregistreerd voor Hallo gebruiker en de update zo nodig.</span><span class="sxs-lookup"><span data-stu-id="5eb77-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="5eb77-220">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-220">Check a user’s group memberships</span></span>

<span data-ttu-id="5eb77-221">toocheck een gebruiker van groepslidmaatschappen, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-222">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-223">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-224">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-225">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-226">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-226">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-227">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-228">Klik op **groepen** toosee die Hallo gebruiker groepen lid van is.</span><span class="sxs-lookup"><span data-stu-id="5eb77-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="5eb77-229">Controleer de toegewezen licenties van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5eb77-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="5eb77-230">toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-231">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-232">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-233">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-234">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-235">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-235">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-236">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-237">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="5eb77-238">Een gebruiker een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="5eb77-238">Assign a user a license</span></span> 

<span data-ttu-id="5eb77-239">een gebruiker van de tooa licentie tooassign Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-240">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-241">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-242">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-243">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-244">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-244">click **All users**.</span></span>

6.  <span data-ttu-id="5eb77-245">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-246">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="5eb77-247">Klik op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="5eb77-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="5eb77-248">Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="5eb77-249">**Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="5eb77-250">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5eb77-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="5eb77-251">Klik op Hallo **toewijzen** knop tooassign deze licenties toothis-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5eb77-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="5eb77-252">Problemen met groepen</span><span class="sxs-lookup"><span data-stu-id="5eb77-252">Problems with groups</span></span>

<span data-ttu-id="5eb77-253">Toegang tot toepassingen kan worden geblokkeerd vanwege tooa probleem met een groep die is toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="5eb77-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="5eb77-254">Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met groepen en groepslidmaatschappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="5eb77-255">Controleer het lidmaatschap van een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="5eb77-256">Controleer de criteria voor lidmaatschap van een dynamische groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="5eb77-257">Controleer de toegewezen licenties van een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="5eb77-258">Opnieuw verwerken van een groep licenties</span><span class="sxs-lookup"><span data-stu-id="5eb77-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="5eb77-259">Een licentie toewijzen aan een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="5eb77-260">Controleer het lidmaatschap van een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-260">Check a group’s membership</span></span>

<span data-ttu-id="5eb77-261">toocheck een groepslidmaatschap, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-262">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-263">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-264">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-265">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-266">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-266">click **All groups**.</span></span>

6.  <span data-ttu-id="5eb77-267">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-268">Klik op **leden** tooreview Hallo lijst met gebruikers toothis groep toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="5eb77-269">Controleer de criteria voor lidmaatschap van een dynamische groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="5eb77-270">toocheck criteria voor het lidmaatschap van een dynamische groep Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-271">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-272">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-273">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-274">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-275">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-275">click **All groups**.</span></span>

6.  <span data-ttu-id="5eb77-276">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-277">Klik op **dynamisch lidmaatschapsregels.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="5eb77-278">Bekijk Hallo **eenvoudige** of **geavanceerde** regel gedefinieerd voor de groep en zorg ervoor dat die u wilt dat een lid van deze groep toobe Hallo-gebruiker aan deze criteria voldoet.</span><span class="sxs-lookup"><span data-stu-id="5eb77-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="5eb77-279">Controleer de toegewezen licenties van een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="5eb77-280">toocheck een groep van toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-281">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-282">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-283">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-284">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-285">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-285">click **All groups**.</span></span>

6.  <span data-ttu-id="5eb77-286">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-287">Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="5eb77-288">Opnieuw verwerken van een groep licenties</span><span class="sxs-lookup"><span data-stu-id="5eb77-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="5eb77-289">tooreprocess een groep van toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="5eb77-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-290">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-291">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-292">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-293">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-294">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-294">click **All groups**.</span></span>

6.  <span data-ttu-id="5eb77-295">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-296">Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="5eb77-297">Klik op Hallo **opnieuw verwerken** knop tooensure die leden van de licenties die zijn toegewezen toothis beveiligingsgroep Hallo actueel zijn.</span><span class="sxs-lookup"><span data-stu-id="5eb77-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="5eb77-298">Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="5eb77-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5eb77-299">toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="5eb77-300">[Een gebruiker een licentie toewijzen](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="5eb77-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="5eb77-301">Een licentie toewijzen aan een groep</span><span class="sxs-lookup"><span data-stu-id="5eb77-301">Assign a group a license</span></span>

<span data-ttu-id="5eb77-302">een licentiegroep tooa tooassign Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5eb77-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="5eb77-303">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-304">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-305">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-306">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-307">Klik op **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-307">click **All groups**.</span></span>

6.  <span data-ttu-id="5eb77-308">**Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="5eb77-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="5eb77-309">Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="5eb77-310">Klik op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="5eb77-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="5eb77-311">Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="5eb77-312">**Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="5eb77-313">Klik op **Ok** wanneer dit is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5eb77-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="5eb77-314">Klik op Hallo **toewijzen** knop tooassign deze groep toothis-licenties.</span><span class="sxs-lookup"><span data-stu-id="5eb77-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="5eb77-315">Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="5eb77-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5eb77-316">toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="5eb77-317">[Een gebruiker een licentie toewijzen](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="5eb77-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="5eb77-318">Problemen met het beleid voor voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="5eb77-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="5eb77-319">Beleid voor voorwaardelijke toegang specifieke controleren</span><span class="sxs-lookup"><span data-stu-id="5eb77-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="5eb77-320">toocheck of om een voorwaardelijk toegangsbeleid te valideren:</span><span class="sxs-lookup"><span data-stu-id="5eb77-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="5eb77-321">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-322">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-323">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-324">Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-325">Klik op Hallo **voorwaardelijke toegang** navigatie-item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="5eb77-326">Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.</span><span class="sxs-lookup"><span data-stu-id="5eb77-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="5eb77-327">Controleer of er zijn geen specifieke voorwaarden, toewijzingen of andere instellingen die gebruikerstoegang mogelijk blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5eb77-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5eb77-328">U kunt desgewenst tootemporarily uitschakelen op dit beleid tooensure deze geen invloed op aanmelding mediaprofielen toodo deze, Hallo set **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop .</span><span class="sxs-lookup"><span data-stu-id="5eb77-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="5eb77-329">Beleid voor voorwaardelijke toegang van een specifieke toepassing controleren</span><span class="sxs-lookup"><span data-stu-id="5eb77-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="5eb77-330">toocheck of valideren van één toepassing momenteel geconfigureerde voorwaardelijk toegangsbeleid:</span><span class="sxs-lookup"><span data-stu-id="5eb77-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="5eb77-331">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-332">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-333">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-334">Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-335">Klik op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-335">click **All applications**.</span></span>

6.  <span data-ttu-id="5eb77-336">Zoeken voor het Hallo-toepassing u geïnteresseerd bent in of Hallo gebruiker probeert toosign in tooby toepassing weergegeven naam of een toepassing-id.</span><span class="sxs-lookup"><span data-stu-id="5eb77-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="5eb77-337">Als het Hallo-toepassing die u zoekt niet wordt weergegeven, klikt u op Hallo **Filter** knop en het Hallo-bereik van Hallo lijst te vergroten**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5eb77-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="5eb77-338">Als u wilt dat toosee meer kolommen, klikt u op Hallo **kolommen** knop tooadd aanvullende informatie voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5eb77-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="5eb77-339">Klik op Hallo **voorwaardelijke toegang** navigatie-item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="5eb77-340">Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.</span><span class="sxs-lookup"><span data-stu-id="5eb77-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="5eb77-341">Controleer of er zijn geen specifieke voorwaarden, toewijzingen of andere instellingen die gebruikerstoegang mogelijk blokkeert.</span><span class="sxs-lookup"><span data-stu-id="5eb77-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="5eb77-342">U kunt desgewenst tootemporarily uitschakelen op dit beleid tooensure deze geen invloed op aanmelding mediaprofielen toodo deze, Hallo set **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop .</span><span class="sxs-lookup"><span data-stu-id="5eb77-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="5eb77-343">Beleid voor specifieke voorwaardelijke toegang uitschakelen</span><span class="sxs-lookup"><span data-stu-id="5eb77-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="5eb77-344">toocheck of om een voorwaardelijk toegangsbeleid te valideren:</span><span class="sxs-lookup"><span data-stu-id="5eb77-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="5eb77-345">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="5eb77-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5eb77-346">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5eb77-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5eb77-347">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5eb77-348">Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eb77-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="5eb77-349">Klik op Hallo **voorwaardelijke toegang** navigatie-item.</span><span class="sxs-lookup"><span data-stu-id="5eb77-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="5eb77-350">Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.</span><span class="sxs-lookup"><span data-stu-id="5eb77-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="5eb77-351">Hallo-beleid uitschakelen door Hallo instelling **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5eb77-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="5eb77-352">Problemen met toestemming van de toepassing</span><span class="sxs-lookup"><span data-stu-id="5eb77-352">Problems with application consent</span></span>

<span data-ttu-id="5eb77-353">Toegang tot toepassingen kan worden geblokkeerd omdat Hallo juiste machtigingen toestemming bewerking nog niet heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="5eb77-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="5eb77-354">Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met de toepassing toestemming:</span><span class="sxs-lookup"><span data-stu-id="5eb77-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="5eb77-355">Een bewerking op gebruikersniveau toestemming uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="5eb77-356">De bewerking beheerdersniveau toestemming voor elke toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="5eb77-357">Beheerdersniveau toestemming uitvoeren voor een toepassing voor één tenant</span><span class="sxs-lookup"><span data-stu-id="5eb77-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="5eb77-358">Beheerdersniveau toestemming voor een multitenant-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="5eb77-359">Een bewerking op gebruikersniveau toestemming uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="5eb77-360">Voor een Open ID Connect-toepassing die machtigingen aanvragen, voert navigeren van de toepassing toohello scherm aanmelden een toepassing van de gebruiker toestemming niveau toohello voor Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5eb77-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="5eb77-361">Als u toodo dit programmatisch wenst, Zie [afzonderlijke gebruikers toestemming wordt gevraagd](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="5eb77-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="5eb77-362">De bewerking beheerdersniveau toestemming voor elke toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="5eb77-363">Voor **alleen toepassingen die zijn ontwikkeld met Hallo V1 toepassingsmodel**, kunt u deze beheerder niveau toestemming toooccur forceren door toe te voegen '**? prompt = admin\_toestemming**' toohello einde van een aanmelding van de toepassing in een URL.</span><span class="sxs-lookup"><span data-stu-id="5eb77-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="5eb77-364">Voor **alle toepassingen die zijn ontwikkeld met Hallo V2 toepassingsmodel**, kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **Hallo machtigingen aanvragen bij een map beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5eb77-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="5eb77-365">Beheerdersniveau toestemming uitvoeren voor een toepassing voor één tenant</span><span class="sxs-lookup"><span data-stu-id="5eb77-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="5eb77-366">Voor **toepassingen voor één tenant** die aanvragen machtigingen (zoals die u ontwikkelt of in uw organisatie eigenaar), kunt u uitvoeren een **beheerniveau toestemming** bewerking namens alle gebruikers met aanmelden als globale beheerder en te klikken op Hallo **machtigingen verlenen** knop bovenaan Hallo Hallo **toepassingsregister -&gt; alle toepassingen -&gt; Selecteer een App - &gt; Required Permissions** blade.</span><span class="sxs-lookup"><span data-stu-id="5eb77-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="5eb77-367">Voor **alle toepassingen die zijn ontwikkeld met Hallo V1 of V2-toepassingsmodel**, kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **hello om machtigingen vragen bij een Directory-beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5eb77-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="5eb77-368">Beheerdersniveau toestemming voor een multitenant-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5eb77-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="5eb77-369">Voor **multitenant-toepassingen** dat machtigingen voor aanvragen (zoals een toepassing van een derde partij, of Microsoft, ontwikkelt), kunt u uitvoeren een **beheerniveau toestemming** bewerking.</span><span class="sxs-lookup"><span data-stu-id="5eb77-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="5eb77-370">Meld u aan als een globale beheerder en te klikken op Hallo **machtigingen verlenen** knop onder Hallo **bedrijfstoepassingen -&gt; alle toepassingen -&gt; Selecteer een App -&gt; Machtigingen** blade (beschikbaar snel).</span><span class="sxs-lookup"><span data-stu-id="5eb77-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="5eb77-371">Ook kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **Hallo machtigingen aanvragen bij een directory-beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5eb77-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eb77-372">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5eb77-372">Next steps</span></span>
[<span data-ttu-id="5eb77-373">Gebruik van het Hallo-beheerder toestemming eindpunt</span><span class="sxs-lookup"><span data-stu-id="5eb77-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

