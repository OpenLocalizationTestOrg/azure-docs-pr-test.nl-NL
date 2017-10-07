---
title: aaaProblems aanmelden tooa niet galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding | Microsoft Docs
description: Richtlijnen voor specifieke problemen Hallo u mogelijk mee te maken tijdens het aanmelden tooan toepassing is geconfigureerd voor op basis van SAML federatieve eenmalige aanmelding met Azure AD
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="bbbe2-103">Problemen met aanmelden tooa niet galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbbe2-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="bbbe2-104">tootroubleshoot uw probleem, moet u tooverify Hallo Toepassingsconfiguratie in Azure AD als volgt:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="bbbe2-105">U kunt alle Hallo configuratiestappen voor Azure AD-galerie toepassing hello hebt gevolgd.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="bbbe2-106">Hallo-id en de antwoord-URL is geconfigureerd in AAD overeenkomen ze verwachte waarden in de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="bbbe2-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="bbbe2-107">U hebt toegewezen gebruikers toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="bbbe2-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="bbbe2-108">Toepassing is niet gevonden in map</span><span class="sxs-lookup"><span data-stu-id="bbbe2-108">Application not found in directory</span></span>

<span data-ttu-id="bbbe2-109">*Fout AADSTS70001: Toepassing met id 'https://contoso.com' is niet gevonden in de directory Hallo*.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="bbbe2-110">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-110">**Possible cause**</span></span>

<span data-ttu-id="bbbe2-111">Hallo verlener kenmerk verzendt van Hallo toepassing tooAzure AD in Hallo SAML-aanvraag komt niet overeen met de id-waarde Hallo geconfigureerd in de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="bbbe2-112">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-112">**Resolution**</span></span>

<span data-ttu-id="bbbe2-113">Zorg ervoor dat kenmerk Hallo verlener in Hallo SAML-aanvraag dat deze komt overeen met de Hallo id waarde die is geconfigureerd in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="bbbe2-114">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bbbe2-115">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bbbe2-116">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bbbe2-117">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bbbe2-118">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="bbbe2-119">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bbbe2-120">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bbbe2-121">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bbbe2-122"><span id="_Hlk477190042" class="anchor"></span>Ga te**domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="bbbe2-123">Controleer of u die waarde Hallo in Hallo id textbox is die overeenkomt met Hallo-waarde voor Hallo id-waarde weergegeven in het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="bbbe2-124">Nadat u de id-waarde Hallo hebt bijgewerkt in Azure AD en de overeenkomende Hallo waarde door de toepassing hello in Hallo SAML-aanvraag verzendt, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="bbbe2-125">Hallo antwoordadres komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="bbbe2-126">*Fout AADSTS50011: antwoordadres Hallo 'https://contoso.com' komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello*</span><span class="sxs-lookup"><span data-stu-id="bbbe2-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="bbbe2-127">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-127">**Possible cause**</span></span> 

<span data-ttu-id="bbbe2-128">Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag komt niet overeen met de Hallo antwoord-URL-waarde of patroon dat is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="bbbe2-129">Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag is Hallo-URL die u in Hallo-fout ziet.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="bbbe2-130">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-130">**Resolution**</span></span> 

<span data-ttu-id="bbbe2-131">Zorg ervoor dat Hallo AssertionConsumerServiceURL de waarde in Hallo SAML-aanvraag de overeenkomende Hallo antwoord-URL-waarde die is geconfigureerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="bbbe2-132">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="bbbe2-133">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="bbbe2-134">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="bbbe2-135">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="bbbe2-136">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="bbbe2-137">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="bbbe2-138">Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren</span><span class="sxs-lookup"><span data-stu-id="bbbe2-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="bbbe2-139">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bbbe2-140">Ga te**domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="bbbe2-141">Controleren of bijwerken van Hallo-waarde in Hallo antwoord-URL textbox toomatch hello AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="bbbe2-142">Als u Hallo antwoord-URL textbox niet ziet, selecteert u Hallo **weergeven geavanceerde instellingen voor URL** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="bbbe2-143">Nadat u Hallo antwoord-URL-waarde hebben bijgewerkt in Azure AD en het Hallo-waarde die overeenkomt met verzendt door toepassing hello in Hallo SAML-aanvraag, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="bbbe2-144">Gebruiker met een niet toegewezen</span><span class="sxs-lookup"><span data-stu-id="bbbe2-144">User not assigned a role</span></span>

<span data-ttu-id="bbbe2-145">*Fout AADSTS50105: Hallo aangemelde gebruiker 'brian@contoso.com' tooa-rol voor de toepassing hello is niet toegewezen*</span><span class="sxs-lookup"><span data-stu-id="bbbe2-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="bbbe2-146">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-146">**Possible cause**</span></span>

<span data-ttu-id="bbbe2-147">Hallo-gebruiker is niet verleend access toohello-toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="bbbe2-148">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-148">**Resolution**</span></span>

<span data-ttu-id="bbbe2-149">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="bbbe2-150">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bbbe2-151">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bbbe2-152">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bbbe2-153">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bbbe2-154">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bbbe2-155">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bbbe2-156">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="bbbe2-157">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bbbe2-158">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="bbbe2-159">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="bbbe2-160">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="bbbe2-161">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="bbbe2-162">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="bbbe2-163">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="bbbe2-164">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="bbbe2-165">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="bbbe2-166">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="bbbe2-167">Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="bbbe2-168">Geen een geldige SAML aanvragen</span><span class="sxs-lookup"><span data-stu-id="bbbe2-168">Not a valid SAML Request</span></span>

<span data-ttu-id="bbbe2-169">*Fout AADSTS75005: Hallo-aanvraag is niet een geldig Saml2-protocolbericht.*</span><span class="sxs-lookup"><span data-stu-id="bbbe2-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="bbbe2-170">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-170">**Possible cause**</span></span>

<span data-ttu-id="bbbe2-171">Hallo SAML-aanvraag verzonden door de toepassing hello voor eenmalige aanmelding biedt geen ondersteuning voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="bbbe2-172">Enkele veelvoorkomende problemen zijn:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-172">Some common issues are:</span></span>

-   <span data-ttu-id="bbbe2-173">Ontbrekende vereiste velden in Hallo SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="bbbe2-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="bbbe2-174">SAML gecodeerd aanvraagmethode</span><span class="sxs-lookup"><span data-stu-id="bbbe2-174">SAML request encoded method</span></span>

<span data-ttu-id="bbbe2-175">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-175">**Resolution**</span></span>

1.  <span data-ttu-id="bbbe2-176">Vastleggen van SAML-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-176">Capture SAML request.</span></span> <span data-ttu-id="bbbe2-177">Volg Hallo-zelfstudie op [hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn hoe toocapture Hallo SAML aanvragen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="bbbe2-178">Neem contact op met de leverancier van de toepassing hello en -share:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="bbbe2-179">SAML-aanvraag</span><span class="sxs-lookup"><span data-stu-id="bbbe2-179">SAML request</span></span>

    -   [<span data-ttu-id="bbbe2-180">Vereisten voor Azure AD Single Sign-on SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="bbbe2-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="bbbe2-181">Ze moeten valideren hello Azure AD SAML-implementatie voor eenmalige aanmelding ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="bbbe2-182">Er is geen resource in de lijst requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="bbbe2-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="bbbe2-183">*Fout AADSTS65005: Hallo clienttoepassing heeft aangevraagd toegang tooresource ' 00000002-0000-0000-c000-000000000000'. Deze aanvraag is mislukt omdat het Hallo-client is niet opgegeven voor deze bron in de lijst met requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="bbbe2-184">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-184">**Possible cause**</span></span>

<span data-ttu-id="bbbe2-185">Hallo application-object is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-185">hello application object is corrupted.</span></span>

<span data-ttu-id="bbbe2-186">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-186">**Resolution**</span></span>

<span data-ttu-id="bbbe2-187">toosolve hello probleem verwijderen Hallo toepassing hello directory.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="bbbe2-188">Vervolgens toevoegen en configureren van de toepassing hello, volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bbbe2-189">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bbbe2-190">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bbbe2-191">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bbbe2-192">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bbbe2-193">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bbbe2-194">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bbbe2-195">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bbbe2-196">Klik op **verwijderen** op Hallo linksboven van de toepassing hello **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="bbbe2-197">Vernieuwen van Azure AD en voegt u de toepassing hello van Hallo-galerie van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="bbbe2-198">Configureer vervolgens Hallo toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="bbbe2-199">Na het opnieuw configureren van de toepassing hello, moet u kunnen toosign in toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="bbbe2-200">Certificaat of de sleutel niet geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="bbbe2-200">Certificate or key not configured</span></span>

<span data-ttu-id="bbbe2-201">Fout AADSTS50003: Er is geen ondertekeningssleutel geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="bbbe2-202">**Mogelijke oorzaak**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-202">**Possible cause**</span></span>

<span data-ttu-id="bbbe2-203">Hallo application-object is beschadigd en Azure AD geconfigureerd voor de toepassing hello Hallo-certificaat niet wordt herkend.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="bbbe2-204">**Naamomzetting**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-204">**Resolution**</span></span>

<span data-ttu-id="bbbe2-205">toodelete en maak een nieuw certificaat, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="bbbe2-206">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bbbe2-207">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bbbe2-208">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bbbe2-209">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bbbe2-210">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bbbe2-211">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bbbe2-212">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bbbe2-213">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bbbe2-214">Klik op **nieuw certificaat maken** onder Hallo **SAML handtekeningcertificaat** sectie.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="bbbe2-215">Selecteer de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-215">Select Expiration date.</span></span> <span data-ttu-id="bbbe2-216">Klik vervolgens op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="bbbe2-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="bbbe2-217">Controleer **nieuwe certificaat activeren** toooverride Hallo actieve certificaat.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="bbbe2-218">Klik vervolgens op **opslaan** Hallo boven aan het Hallo-blade tooactivate Hallo rollovercertificaat en accepteren.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="bbbe2-219">Onder Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **verwijderen** tooremove hello **ongebruikt** certificaat.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="bbbe2-220">Probleem bij het aanpassen van Hallo SAML claims verzonden tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="bbbe2-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="bbbe2-221">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbbe2-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bbbe2-222">Next steps</span></span>
[<span data-ttu-id="bbbe2-223">Vereisten voor Azure AD Single Sign-on SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="bbbe2-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
