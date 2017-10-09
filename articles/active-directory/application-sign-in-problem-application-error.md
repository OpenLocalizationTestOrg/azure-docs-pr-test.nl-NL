---
title: aaaError op de pagina van de toepassing na het aanmelden | Microsoft Docs
description: Hoe tooresolve problemen met Azure AD aanmelden bij het Hallo-toepassing zelf genereert een fout opgetreden
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="c817b-103">Fout op de pagina voor een toepassing na het aanmelden</span><span class="sxs-lookup"><span data-stu-id="c817b-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="c817b-104">In dit scenario Azure AD Hallo-gebruiker in heeft ondertekend, maar Hallo toepassing is een fout opgetreden bij het Hallo gebruiker toosuccessfully voltooien Hallo teken is niet toegestaan in stroom om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c817b-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="c817b-105">In dit scenario accepteert Hallo toepassing geen Hallo antwoord probleem door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c817b-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="c817b-106">Er zijn enkele mogelijke redenen waarom Hallo toepassing hello Azure AD-antwoord niet geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="c817b-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="c817b-107">Als het Hallo-fout in de toepassing hello is niet genoeg wissen tooknow ontbreekt wat Hallo antwoord wordt vervolgens:</span><span class="sxs-lookup"><span data-stu-id="c817b-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="c817b-108">Controleer of u alle stappen van Hallo in Hallo artikel hebt uitgevoerd als Hallo toepassing hello Azure AD-galerie, [hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="c817b-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="c817b-109">Gebruik een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) toocapture SAML SAML-reactie en SAML-token aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c817b-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="c817b-110">Hallo SAML-reactie delen met Hallo toepassing leverancier tooknow wat ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="c817b-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="c817b-111">Ontbrekende kenmerken in Hallo SAML-reactie</span><span class="sxs-lookup"><span data-stu-id="c817b-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="c817b-112">een kenmerk in hello Azure AD configuratie toobe verzonden in antwoord hello Azure AD, tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c817b-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="c817b-113">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c817b-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c817b-114">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c817b-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c817b-115">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c817b-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c817b-116">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c817b-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c817b-117">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c817b-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c817b-118">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c817b-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c817b-119">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c817b-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c817b-120">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c817b-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c817b-121">Klik op **weergeven en alle andere gebruiker onder kenmerken bewerken** hello **gebruikerskenmerken** sectie tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c817b-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="c817b-122">een kenmerk tooadd:</span><span class="sxs-lookup"><span data-stu-id="c817b-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="c817b-123">Klik op **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="c817b-123">click **Add attribute**.</span></span> <span data-ttu-id="c817b-124">Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c817b-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="c817b-125">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="c817b-125">Click **Save.**</span></span> <span data-ttu-id="c817b-126">U zien nieuw kenmerk Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="c817b-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="c817b-127">Hallo-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c817b-127">Save hello configuration.</span></span>

<span data-ttu-id="c817b-128">Volgende keer Hallo gebruiker zich aanmeldt toohello toepassing, Azure AD verzenden Hallo nieuw kenmerk in Hallo SAML-reactie.</span><span class="sxs-lookup"><span data-stu-id="c817b-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="c817b-129">Hallo-toepassing verwacht een andere gebruikers-id-waarde of de indeling</span><span class="sxs-lookup"><span data-stu-id="c817b-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="c817b-130">Hallo is aanmelden toohello toepassing mislukt omdat Hallo SAML-reactie kenmerken, zoals rollen ontbreekt of omdat het Hallo-toepassing een andere indeling voor het Hallo-id van de entiteit-kenmerk worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="c817b-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="c817b-131">Een kenmerk in de configuratie van hello Azure AD-toepassing toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c817b-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="c817b-132">toochange hello gebruikers-id-waarde Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c817b-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="c817b-133">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c817b-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c817b-134">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c817b-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c817b-135">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c817b-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c817b-136">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c817b-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c817b-137">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c817b-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c817b-138">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c817b-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c817b-139">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c817b-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c817b-140">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c817b-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c817b-141">Onder Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c817b-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="c817b-142">Wijzigen van de id van de entiteit (gebruikers-id)</span><span class="sxs-lookup"><span data-stu-id="c817b-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="c817b-143">Als de toepassing hello een andere indeling voor het Hallo-id van de entiteit-kenmerk verwacht.</span><span class="sxs-lookup"><span data-stu-id="c817b-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="c817b-144">Vervolgens niet kunnen tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c817b-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="c817b-145">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="c817b-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="c817b-146">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="c817b-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="c817b-147">Hallo-toepassing verwacht een andere handtekening-methode voor het SAML-reactie Hallo</span><span class="sxs-lookup"><span data-stu-id="c817b-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="c817b-148">toochange welke onderdelen van het SAML-token Hallo digitaal zijn ondertekend door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c817b-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="c817b-149">Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="c817b-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="c817b-150">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c817b-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c817b-151">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c817b-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c817b-152">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c817b-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c817b-153">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c817b-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c817b-154">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c817b-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c817b-155">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c817b-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c817b-156">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c817b-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c817b-157">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c817b-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c817b-158">Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder Hallo **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="c817b-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="c817b-159">Selecteer Hallo juiste **ondertekening optie** werd verwacht door de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="c817b-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="c817b-160">Meld u SAML-reactie</span><span class="sxs-lookup"><span data-stu-id="c817b-160">Sign SAML response</span></span>

  * <span data-ttu-id="c817b-161">Meld u aan de SAML-reactie en verklaring</span><span class="sxs-lookup"><span data-stu-id="c817b-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="c817b-162">Aanmelding van SAML-verklaring</span><span class="sxs-lookup"><span data-stu-id="c817b-162">Sign SAML assertion</span></span>

<span data-ttu-id="c817b-163">Volgende keer Hallo gebruiker zich aanmeldt toohello toepassing, Hallo Azure AD-aanmelding deel uit van SAML-reactie Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c817b-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="c817b-164">Hallo-toepassing verwacht hello toobe algoritme SHA-1-ondertekening</span><span class="sxs-lookup"><span data-stu-id="c817b-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="c817b-165">Standaard ondertekent Azure AD Hallo SAML-token met Hallo meeste beveiliging wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c817b-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="c817b-166">Niet Hallo-algoritme tooSHA-1 is raadzaam wijzigen tenzij Hallo toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="c817b-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="c817b-167">toochange Hallo ondertekeningsalgoritme, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="c817b-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="c817b-168">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c817b-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c817b-169">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c817b-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c817b-170">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c817b-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c817b-171">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="c817b-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c817b-172">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c817b-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c817b-173">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="c817b-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c817b-174">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c817b-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c817b-175">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="c817b-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c817b-176">Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder Hallo **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="c817b-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="c817b-177">Selecteer SHA-1 in Hallo **ondertekening algoritme**.</span><span class="sxs-lookup"><span data-stu-id="c817b-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="c817b-178">Volgende keer dat de gebruiker zich aanmeldt toohello toepassing hello, Azure AD-aanmelding Hallo SAML-token met behulp van algoritme SHA-1.</span><span class="sxs-lookup"><span data-stu-id="c817b-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c817b-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c817b-179">Next steps</span></span>
[<span data-ttu-id="c817b-180">Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c817b-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
