---
title: aaaProblems aanmelden tooa galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding | Microsoft Docs
description: Richtlijnen voor het Hallo specifieke fouten bij het ondertekenen van een toepassing die u hebt geconfigureerd voor op basis van SAML federatieve eenmalige aanmelding met Azure AD
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="7a491-103">Problemen met aanmelden tooa galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7a491-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="7a491-104">tootroubleshoot uw probleem, moet u tooverify Hallo Toepassingsconfiguratie in Azure AD als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a491-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="7a491-105">U kunt alle Hallo configuratiestappen voor Azure AD-galerie toepassing hello hebt gevolgd.</span><span class="sxs-lookup"><span data-stu-id="7a491-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="7a491-106">Hallo-id en de antwoord-URL is geconfigureerd in AAD overeenkomen ze verwachte waarden in de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="7a491-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="7a491-107">U hebt toegewezen gebruikers toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="7a491-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="7a491-108">Toepassing is niet gevonden in map</span><span class="sxs-lookup"><span data-stu-id="7a491-108">Application not found in directory</span></span>

<span data-ttu-id="7a491-109">*Fout AADSTS70001: Toepassing met id 'https://contoso.com' is niet gevonden in de directory Hallo*.</span><span class="sxs-lookup"><span data-stu-id="7a491-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="7a491-110">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-110">**Possible cause**</span></span>

<span data-ttu-id="7a491-111">Hallo verlener kenmerk verzendt van Hallo toepassing tooAzure AD in Hallo SAML-aanvraag komt niet overeen met de id-waarde Hallo geconfigureerd in de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="7a491-112">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-112">**Resolution**</span></span>

<span data-ttu-id="7a491-113">Zorg ervoor dat kenmerk Hallo verlener in Hallo SAML-aanvraag dat deze komt overeen met de Hallo id waarde die is geconfigureerd in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="7a491-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="7a491-114">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7a491-115">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-116">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-117">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-118">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7a491-119">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-120">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="7a491-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="7a491-121">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="7a491-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7a491-122">Ga te**domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="7a491-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="7a491-123">Controleer of u die waarde Hallo in Hallo id textbox is die overeenkomt met Hallo-waarde voor Hallo id-waarde weergegeven in het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="7a491-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="7a491-124">Nadat u de id-waarde Hallo hebt bijgewerkt in Azure AD en de overeenkomende Hallo waarde door de toepassing hello in Hallo SAML-aanvraag verzendt, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="7a491-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="7a491-125">Hallo antwoordadres komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="7a491-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="7a491-126">*Fout AADSTS50011: antwoordadres Hallo 'https://contoso.com' komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello*</span><span class="sxs-lookup"><span data-stu-id="7a491-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="7a491-127">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-127">**Possible cause**</span></span>

<span data-ttu-id="7a491-128">Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag komt niet overeen met de Hallo antwoord-URL-waarde of patroon dat is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="7a491-129">Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag is Hallo-URL die u in Hallo-fout ziet.</span><span class="sxs-lookup"><span data-stu-id="7a491-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="7a491-130">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-130">**Resolution**</span></span>

<span data-ttu-id="7a491-131">Zorg ervoor dat Hallo AssertionConsumerServiceURL de waarde in Hallo SAML-aanvraag de overeenkomende Hallo antwoord-URL-waarde die is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="7a491-132">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7a491-133">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-134">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-135">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-136">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7a491-137">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-138">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="7a491-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="7a491-139">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="7a491-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7a491-140">Ga te**domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="7a491-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="7a491-141">Controleren of bijwerken van Hallo-waarde in Hallo antwoord-URL textbox toomatch hello AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="7a491-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="7a491-142">Als u Hallo antwoord-URL textbox niet ziet, selecteert u Hallo **weergeven geavanceerde instellingen voor URL** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="7a491-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="7a491-143">Nadat u Hallo antwoord-URL-waarde hebben bijgewerkt in Azure AD en het Hallo-waarde die overeenkomt met verzendt door toepassing hello in Hallo SAML-aanvraag, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="7a491-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="7a491-144">Gebruiker met een niet toegewezen</span><span class="sxs-lookup"><span data-stu-id="7a491-144">User not assigned a role</span></span>

<span data-ttu-id="7a491-145">*Fout AADSTS50105: Hallo aangemelde gebruiker 'brian@contoso.com' is niet toegewezen rol voor de toepassing hello tooa*.</span><span class="sxs-lookup"><span data-stu-id="7a491-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="7a491-146">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-146">**Possible cause**</span></span>

<span data-ttu-id="7a491-147">Hallo-gebruiker is niet verleend access toohello-toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="7a491-148">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-148">**Resolution**</span></span>

<span data-ttu-id="7a491-149">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="7a491-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="7a491-150">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7a491-151">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-152">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-153">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-154">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7a491-155">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-156">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="7a491-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="7a491-157">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="7a491-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7a491-158">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="7a491-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7a491-159">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="7a491-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7a491-160">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="7a491-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7a491-161">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="7a491-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="7a491-162">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="7a491-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="7a491-163">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="7a491-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="7a491-164">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="7a491-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="7a491-165">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7a491-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="7a491-166">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7a491-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="7a491-167">Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="7a491-168">Geen een geldige SAML aanvragen</span><span class="sxs-lookup"><span data-stu-id="7a491-168">Not a valid SAML Request</span></span>

<span data-ttu-id="7a491-169">*Fout AADSTS75005: Hallo-aanvraag is niet een geldig Saml2-protocolbericht.*</span><span class="sxs-lookup"><span data-stu-id="7a491-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="7a491-170">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-170">**Possible cause**</span></span>

<span data-ttu-id="7a491-171">Hallo SAML-aanvraag verzonden door de toepassing hello voor eenmalige aanmelding biedt geen ondersteuning voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="7a491-172">Enkele veelvoorkomende problemen zijn:</span><span class="sxs-lookup"><span data-stu-id="7a491-172">Some common issues are:</span></span>

-   <span data-ttu-id="7a491-173">Ontbrekende vereiste velden in Hallo SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="7a491-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="7a491-174">SAML gecodeerd aanvraagmethode</span><span class="sxs-lookup"><span data-stu-id="7a491-174">SAML request encoded method</span></span>

<span data-ttu-id="7a491-175">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-175">**Resolution**</span></span>

1.  <span data-ttu-id="7a491-176">Vastleggen van SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="7a491-176">Capture SAML request.</span></span> <span data-ttu-id="7a491-177">Volg de zelfstudie Hallo [hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn hoe toocapture Hallo SAML aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7a491-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="7a491-178">Neem contact op met de leverancier van de toepassing hello en -share:</span><span class="sxs-lookup"><span data-stu-id="7a491-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="7a491-179">SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="7a491-179">SAML request</span></span>

   -   [<span data-ttu-id="7a491-180">Vereisten voor Azure AD Single Sign-on SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="7a491-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="7a491-181">Ze moeten valideren hello Azure AD SAML-implementatie voor eenmalige aanmelding ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7a491-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="7a491-182">Er is geen resource in de lijst requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="7a491-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="7a491-183">*Fout AADSTS65005:hello clienttoepassing toegang tooresource heeft aangevraagd ' 00000002-0000-0000-c000-000000000000'. Deze aanvraag is mislukt omdat het Hallo-client is niet opgegeven voor deze bron in de lijst met requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="7a491-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="7a491-184">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-184">**Possible cause**</span></span>

<span data-ttu-id="7a491-185">Hallo application-object is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="7a491-185">hello application object is corrupted.</span></span>

<span data-ttu-id="7a491-186">**Oplossing: optie 1**</span><span class="sxs-lookup"><span data-stu-id="7a491-186">**Resolution: option 1**</span></span>

<span data-ttu-id="7a491-187">toosolve hello probleem Hallo unieke id-waarde in hello Azure AD-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a491-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="7a491-188">een id-waarde tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="7a491-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="7a491-189">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7a491-190">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-191">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-192">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-193">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7a491-194">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-195">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7a491-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7a491-196">Nadat de toepassing hello wordt geladen, klikt u op op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu</span><span class="sxs-lookup"><span data-stu-id="7a491-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="7a491-197">Onder Hallo **domein en de URL** sectie, moet u controleren op Hallo **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="7a491-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="7a491-198">in Hallo **id** textbox Typ een unieke id voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="7a491-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="7a491-199">**Sla** Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7a491-199">**Save** hello configuration.</span></span>


<span data-ttu-id="7a491-200">**Optie 2 voor naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-200">**Resolution option 2**</span></span>

<span data-ttu-id="7a491-201">Als optie 1 hierboven niet werkt, probeert u het Hallo-toepassing worden verwijderd uit Hallo directory.</span><span class="sxs-lookup"><span data-stu-id="7a491-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="7a491-202">Vervolgens toevoegen en configureren van de toepassing hello, volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="7a491-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7a491-203">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7a491-204">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-205">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-206">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-207">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7a491-208">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-209">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="7a491-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="7a491-210">Klik op **verwijderen** op Hallo linksboven van de toepassing hello **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="7a491-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="7a491-211">Vernieuwen van Azure AD en voegt u de toepassing hello van Hallo-galerie van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a491-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="7a491-212">Configureer vervolgens de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="7a491-212">Then, Configure hello application</span></span>

<span data-ttu-id="7a491-213"><span id="_Hlk477190176" class="anchor"></span>Na het opnieuw configureren van de toepassing hello, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="7a491-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="7a491-214">Certificaat of de sleutel niet geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="7a491-214">Certificate or key not configured</span></span>

<span data-ttu-id="7a491-215">*Fout AADSTS50003: Er is geen ondertekeningssleutel geconfigureerd.*</span><span class="sxs-lookup"><span data-stu-id="7a491-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="7a491-216">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="7a491-216">**Possible cause**</span></span>

<span data-ttu-id="7a491-217">Hallo application-object is beschadigd en Azure AD geconfigureerd voor de toepassing hello Hallo-certificaat niet wordt herkend.</span><span class="sxs-lookup"><span data-stu-id="7a491-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="7a491-218">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="7a491-218">**Resolution**</span></span>

<span data-ttu-id="7a491-219">toodelete en maak een nieuw certificaat, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="7a491-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="7a491-220">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="7a491-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7a491-221">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a491-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7a491-222">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7a491-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7a491-223">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a491-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7a491-224">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a491-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="7a491-225">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="7a491-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7a491-226">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="7a491-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="7a491-227">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="7a491-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7a491-228">Klik op **nieuw certificaat maken** onder Hallo **SAML handtekeningcertificaat** sectie.</span><span class="sxs-lookup"><span data-stu-id="7a491-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="7a491-229">Selecteer de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="7a491-229">Select Expiration date.</span></span> <span data-ttu-id="7a491-230">Klik vervolgens op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="7a491-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="7a491-231">Controleer **nieuwe certificaat activeren** toooverride Hallo actieve certificaat.</span><span class="sxs-lookup"><span data-stu-id="7a491-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="7a491-232">Klik vervolgens op **opslaan** Hallo boven aan het Hallo-blade tooactivate Hallo rollovercertificaat en accepteren.</span><span class="sxs-lookup"><span data-stu-id="7a491-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="7a491-233">Onder Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **verwijderen** tooremove hello **ongebruikt** certificaat.</span><span class="sxs-lookup"><span data-stu-id="7a491-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="7a491-234">Probleem bij het aanpassen van Hallo SAML claims verzonden tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="7a491-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="7a491-235">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7a491-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a491-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a491-236">Next steps</span></span>
[<span data-ttu-id="7a491-237">Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a491-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
