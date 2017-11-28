---
title: configureren van wachtwoord eenmalige aanmelding voor een toepassing niet galerie aaaProblem | Microsoft Docs
description: Hallo veelvoorkomende problemen mensen face begrijpen bij het configureren van wachtwoord eenmalige aanmelding voor aangepaste niet-galerie-toepassingen die niet worden weergegeven in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="76228-103">Probleem wachtwoord eenmalige aanmelding voor een toepassing niet galerie configureren</span><span class="sxs-lookup"><span data-stu-id="76228-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="76228-104">In dit artikel kunt u toounderstand Hallo veelvoorkomende problemen mensen face bij het configureren van **eenmalige aanmelding wachtwoord** met een niet-galerie-toepassing.</span><span class="sxs-lookup"><span data-stu-id="76228-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="76228-105">Hoe toocapture aanmelden velden voor een toepassing</span><span class="sxs-lookup"><span data-stu-id="76228-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="76228-106">Aanmelden veld vastleggen wordt alleen ondersteund voor HTML-functionaliteit aanmeldingspagina's en is **niet ondersteund voor niet-standaard aanmeldingspagina's**, zoals toepassingen die gebruikmaken van Flash of andere technologieën, zonder HTML-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="76228-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="76228-107">Er zijn twee manieren waarop u kunt aanmelden velden voor uw aangepaste toepassingen vastleggen:</span><span class="sxs-lookup"><span data-stu-id="76228-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="76228-108">Veld voor automatische aanmelding vastleggen</span><span class="sxs-lookup"><span data-stu-id="76228-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="76228-109">Handmatige aanmelden veld vastleggen</span><span class="sxs-lookup"><span data-stu-id="76228-109">Manual sign-in field capture</span></span>

<span data-ttu-id="76228-110">**Veld voor automatische aanmelding vastleggen** werkt goed samen met de meeste ingeschakeld HTML aanmeldingspagina's, als ze gebruiken **bekende DIV-id's voor het Hallo-gebruikersnaam en wachtwoord invoeren** veld.</span><span class="sxs-lookup"><span data-stu-id="76228-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="76228-111">Hallo manier die dit werkt, is door slijmen Hallo HTML op Hallo pagina toofind DIV-id's die aan bepaalde criteria voldoen en door vervolgens metagegevens voor deze toepassing op te slaan zodat we kunnen wachtwoorden tooit later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="76228-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="76228-112">**Handmatige aanmelden veld vastleggen** kan worden gebruikt in case Hallo toepassing hello **leverancier komt niet label** Hallo invoer velden die worden gebruikt voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="76228-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="76228-113">Handmatige aanmelden veld vastleggen kan ook worden gebruikt in geval van Hallo wanneer hello **leverancier renders meerdere velden** en kan niet worden automatisch gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="76228-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="76228-114">Azure AD kunt gegevens opslaan voor als veel velden als op Hallo aanmeldingspagina, zolang u laat ons weten waar deze velden zijn op de pagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="76228-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="76228-115">In het algemeen **als het veld voor automatische aanmelding vastleggen niet werkt, altijd het is raadzaam tijdens het Hallo handmatige optie.**</span><span class="sxs-lookup"><span data-stu-id="76228-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="76228-116">Hoe tooautomatically velden aanmelden voor een toepassing vastleggen</span><span class="sxs-lookup"><span data-stu-id="76228-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="76228-117">tooconfigure **op basis van wachtwoorden Single Sign-on** voor het gebruik van een toepassing **automatische aanmelding veld vastleggen**, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="76228-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="76228-118">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="76228-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="76228-119">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="76228-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="76228-120">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="76228-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="76228-121">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="76228-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="76228-122">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="76228-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="76228-123">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="76228-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="76228-124">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="76228-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="76228-125">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="76228-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="76228-126">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="76228-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="76228-127">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="76228-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="76228-128">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="76228-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="76228-129">**Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar op Hallo-URL die u opgeeft**.</span><span class="sxs-lookup"><span data-stu-id="76228-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="76228-130">Klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="76228-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="76228-131">Nadat u dit doen we je automatisch scrape die URL voor een gebruikersnaam en wachtwoord invoervak en kunt u verzenden toouse Azure AD toosecurely wachtwoorden toothat toepassing hello toegang Configuratiescherm Browseruitbreiding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76228-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="76228-132">Hoe toomanually velden aanmelden voor een toepassing vastleggen</span><span class="sxs-lookup"><span data-stu-id="76228-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="76228-133">toomanually vastleggen aanmelden velden, moet u eerst Hallo toegang Configuratiescherm Browseruitbreiding geïnstalleerd hebben en **niet wordt uitgevoerd in de modus InPrivate-navigatie, incognito of private.**</span><span class="sxs-lookup"><span data-stu-id="76228-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="76228-134">tooinstall hello Browseruitbreiding, volg de stappen Hallo in Hallo [hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo](#i-cannot-manually-detect-sign-in-fields-for-my-application) sectie.</span><span class="sxs-lookup"><span data-stu-id="76228-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="76228-135">tooconfigure **op basis van wachtwoorden Single Sign-on** voor het gebruik van een toepassing **handmatige aanmelden veld vastleggen**, volgt u onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="76228-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="76228-136">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="76228-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="76228-137">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="76228-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="76228-138">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="76228-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="76228-139">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="76228-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="76228-140">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="76228-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="76228-141">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="76228-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="76228-142">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="76228-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="76228-143">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="76228-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="76228-144">Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**</span><span class="sxs-lookup"><span data-stu-id="76228-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="76228-145">Voer Hallo **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="76228-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="76228-146">Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen.</span><span class="sxs-lookup"><span data-stu-id="76228-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="76228-147">**Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar op Hallo-URL die u opgeeft**.</span><span class="sxs-lookup"><span data-stu-id="76228-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="76228-148">Klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="76228-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="76228-149">Nadat u dit doen we je automatisch scrape die URL voor een gebruikersnaam en wachtwoord invoervak en kunt u verzenden toouse Azure AD toosecurely wachtwoorden toothat toepassing hello toegang Configuratiescherm Browseruitbreiding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76228-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="76228-150">In geval Hallo dat dit niet lukt, kunt u **Hallo-in-modus toouse handmatige aanmelden veld vastleggen wijzigen** toostep 12 voort te zetten.</span><span class="sxs-lookup"><span data-stu-id="76228-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="76228-151">Klik op **configureren &lt;appname&gt; instellingen voor wachtwoord eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="76228-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="76228-152">Selecteer Hallo **aanmelden velden handmatig detecteren** configuratieoptie.</span><span class="sxs-lookup"><span data-stu-id="76228-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="76228-153">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76228-153">Click **Ok**.</span></span>

15. <span data-ttu-id="76228-154">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="76228-154">Click **Save**.</span></span>

16. <span data-ttu-id="76228-155">Volg Hallo op het scherm instructies toouse Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="76228-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="76228-156">Er is een fout 'Niet vinden velden aanmelden op die URL'</span><span class="sxs-lookup"><span data-stu-id="76228-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="76228-157">U ziet deze fout wanneer automatische detectie van velden voor aanmelden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="76228-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="76228-158">Dit probleem, probeer handmatige aanmelden veld detectie door Hallo volgen de stappen in Hallo tooresolve [hoe de velden aanmelden voor een toepassing voor het vastleggen van toomanually](#how-to-manually-capture-sign-in-fields-for-an-application) sectie.</span><span class="sxs-lookup"><span data-stu-id="76228-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="76228-159">Er is een fout 'kan geen toosave Single Sign-on-configuratie'</span><span class="sxs-lookup"><span data-stu-id="76228-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="76228-160">In bepaalde zeldzame gevallen, kan één Hallo aanmelding configuratie bijwerken mislukken.</span><span class="sxs-lookup"><span data-stu-id="76228-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="76228-161">tooresolve deze Hallo eenmalige aanmelding configuratie opslaan opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="76228-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="76228-162">Als dit toofail consistent blijft, opent u een ondersteuningsaanvraag en Hallo informatie verzameld in Hallo [hoe toosee Hallo details van een portal melding](#i-cannot-manually-detect-sign-in-fields-for-my-application) en [hoe tooget helpen met het verzenden van meldingen details tooa ondersteuningstechnicus](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secties.</span><span class="sxs-lookup"><span data-stu-id="76228-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="76228-163">Ik kan geen aanmelding handmatig detecteren in velden voor de toepassing</span><span class="sxs-lookup"><span data-stu-id="76228-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="76228-164">Hallo-gedrag die u tegenkomen kunt wanneer handmatige detectie niet werkt onder andere:</span><span class="sxs-lookup"><span data-stu-id="76228-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="76228-165">Hallo handmatige vastleggen toowork komt, maar vastgelegd Hallo-velden zijn niet juist</span><span class="sxs-lookup"><span data-stu-id="76228-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="76228-166">Hallo rechts velden ophalen niet gemarkeerd bij het uitvoeren van Hallo vastleggen</span><span class="sxs-lookup"><span data-stu-id="76228-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="76228-167">Hallo vastleggen, ga ik de aanmeldingspagina van de toepassing toohello zoals verwacht, maar er gebeurt niets</span><span class="sxs-lookup"><span data-stu-id="76228-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="76228-168">Handmatige vastleggen toowork wordt weergegeven, maar SSO gebeurt niet wanneer mijn gebruikers toohello toepassing hello Toegangsvenster navigeren.</span><span class="sxs-lookup"><span data-stu-id="76228-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="76228-169">Controleer Hallo volgende als u een van deze problemen optreden:</span><span class="sxs-lookup"><span data-stu-id="76228-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="76228-170">Zorg ervoor dat u de meest recente versie Hallo van Hallo toegang Configuratiescherm Browseruitbreiding **geïnstalleerd** en **ingeschakeld** door Hallo stappen in Hallo [hoe tooinstall Hallo toegang Configuratiescherm Browser extensie](#how-to-install-the-access-panel-browser-extension) sectie.</span><span class="sxs-lookup"><span data-stu-id="76228-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="76228-171">Zorg ervoor dat u niet vastleggen Hallo probeert tijdens uw browser in **modus incognito, InPrivate- of persoonlijke**.</span><span class="sxs-lookup"><span data-stu-id="76228-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="76228-172">Hallo-uitbreiding voor toegang tot Configuratiescherm wordt niet ondersteund in deze modi.</span><span class="sxs-lookup"><span data-stu-id="76228-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="76228-173">Zorg ervoor dat uw gebruikers niet probeert toosign in toohello toepassing hello Toegangsvenster tijdens in **modus incognito, InPrivate- of persoonlijke**.</span><span class="sxs-lookup"><span data-stu-id="76228-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="76228-174">Hallo-uitbreiding voor toegang tot Configuratiescherm wordt niet ondersteund in deze modi.</span><span class="sxs-lookup"><span data-stu-id="76228-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="76228-175">Probeer het opnieuw Hallo handmatige vastleggen, gezorgd Hallo rode markeringen is via de juiste velden Hallo.</span><span class="sxs-lookup"><span data-stu-id="76228-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="76228-176">Als Hallo handmatige vastleggen lijken toohang of niet van toepassing zijn op de aanmeldingspagina Hallo Alles (geval 3 hierboven), Hallo handmatige vastleggen opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="76228-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="76228-177">Maar deze tijd na het voltooien van Hallo proces, drukt u op Hallo **F12** knop tooopen van uw browser developer-console.</span><span class="sxs-lookup"><span data-stu-id="76228-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="76228-178">Hallo eenmaal daar open **console** en het type **window.location= '&lt;Hallo aanmelding invoeren in een url die u hebt opgegeven bij het configureren van de app Hallo&gt;'** en druk vervolgens op  **Voer**.</span><span class="sxs-lookup"><span data-stu-id="76228-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="76228-179">Deze kracht een pagina omleiden die eindigen Hallo vastleggen en opslaan van Hallo velden die zijn vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="76228-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="76228-180">Als geen van deze benaderingen werkt, kunnen we helpen.</span><span class="sxs-lookup"><span data-stu-id="76228-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="76228-181">Een ondersteuningsaanvraag openen met details van wat u hebt geprobeerd, evenals Hallo informatie verzameld in Hallo Hallo [hoe toosee Hallo details van een portal melding](#i-cannot-manually-detect-sign-in-fields-for-my-application) en [hoe tooget helpen met het verzenden van gegevens meldingen tooa-ondersteuning engineering](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secties (indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="76228-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="76228-182">Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo</span><span class="sxs-lookup"><span data-stu-id="76228-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="76228-183">tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="76228-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="76228-184">Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76228-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="76228-185">Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="76228-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="76228-186">Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.</span><span class="sxs-lookup"><span data-stu-id="76228-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="76228-187">Op basis van uw browser zijn u gerichte toohello downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="76228-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="76228-188">**Voeg** Hallo extensie tooyour browser.</span><span class="sxs-lookup"><span data-stu-id="76228-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="76228-189">Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="76228-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="76228-190">Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.</span><span class="sxs-lookup"><span data-stu-id="76228-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="76228-191">Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="76228-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="76228-192">U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:</span><span class="sxs-lookup"><span data-stu-id="76228-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="76228-193">Uitbreiding van chrome toegang Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="76228-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="76228-194">Uitbreiding van het Configuratiescherm Firefox toegang</span><span class="sxs-lookup"><span data-stu-id="76228-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="76228-195">Hoe toosee Hallo details van een melding van de portal</span><span class="sxs-lookup"><span data-stu-id="76228-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="76228-196">Hallo-details van de bedrijfsportal meldingen kunt u zien door Hallo onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76228-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="76228-197">Klik op Hallo **meldingen** pictogram (Hallo bel) in de rechterbovenhoek Hallo Hallo Azure Portal</span><span class="sxs-lookup"><span data-stu-id="76228-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="76228-198">Selecteer een melding in een **fout** status (die met de volgende toothem van een rood (!)).</span><span class="sxs-lookup"><span data-stu-id="76228-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="76228-199">! Houd er rekening mee] u kunt niet op meldingen in een **geslaagd** of **In uitvoering** status.</span><span class="sxs-lookup"><span data-stu-id="76228-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="76228-200">Deze open Hallo **Meldingsdetails** blade.</span><span class="sxs-lookup"><span data-stu-id="76228-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="76228-201">Gebruik deze informatie zelf toounderstand meer details over Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="76228-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="76228-202">Als u nog hulp nodig hebt, kunt u deze informatie ook met een support engineer of Hallo groep tooget Help-informatie delen met uw probleem.</span><span class="sxs-lookup"><span data-stu-id="76228-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="76228-203">Klik op Hallo **kopiëren** **pictogram** toohello rechts van Hallo **Kopieerfout** textbox toocopy alle Hallo melding details tooshare met een medewerker van de groep ondersteuning of product.</span><span class="sxs-lookup"><span data-stu-id="76228-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="76228-204">Hoe tooget helpen met het verzenden van meldingen details tooa ondersteuningstechnicus</span><span class="sxs-lookup"><span data-stu-id="76228-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="76228-205">Het is heel belangrijk dat u delen **alle details hieronder vermelde Hallo** met de ondersteuningstechnicus als u hulp nodig hebt zodat u ze kunt u snel.</span><span class="sxs-lookup"><span data-stu-id="76228-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="76228-206">U kunt dit eenvoudig door doen **u een schermopname** of door te klikken op Hallo **foutpictogram kopiëren**, toohello rechts van Hallo gevonden **Kopieerfout** textbox.</span><span class="sxs-lookup"><span data-stu-id="76228-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="76228-207">Details van de melding uitgelegd</span><span class="sxs-lookup"><span data-stu-id="76228-207">Notification Details Explained</span></span>

<span data-ttu-id="76228-208">Hallo hieronder wordt uitgelegd meer wat elke Hallo melding items betekent en geven voorbeelden van elk van deze servers.</span><span class="sxs-lookup"><span data-stu-id="76228-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="76228-209">Melding van essentiële Items</span><span class="sxs-lookup"><span data-stu-id="76228-209">Essential Notification Items</span></span>

-   <span data-ttu-id="76228-210">**Titel** – Hallo beschrijvende titel Hallo-melding</span><span class="sxs-lookup"><span data-stu-id="76228-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="76228-211">Voorbeeld: **Application proxy-instellingen**</span><span class="sxs-lookup"><span data-stu-id="76228-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="76228-212">**Beschrijving** : Beschrijving van wat is het gevolg van Hallo bewerking Hallo</span><span class="sxs-lookup"><span data-stu-id="76228-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="76228-213">Voorbeeld: **interne url ingevoerd wordt al gebruikt door een andere toepassing**</span><span class="sxs-lookup"><span data-stu-id="76228-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="76228-214">**Id van de melding** – Hallo unieke id van Hallo-melding</span><span class="sxs-lookup"><span data-stu-id="76228-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="76228-215">Voorbeeld: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="76228-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="76228-216">**Aanvraag-Id van client** – Hallo specifieke aanvraag-id gemaakt door uw browser</span><span class="sxs-lookup"><span data-stu-id="76228-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="76228-217">Voorbeeld: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="76228-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="76228-218">**Stempel UTC-tijd** – Hallo tijdstempel waarover Hallo melding is opgetreden, in UTC</span><span class="sxs-lookup"><span data-stu-id="76228-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="76228-219">Voorbeeld: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="76228-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="76228-220">**Interne transactie-Id** – Hallo interne ID we in ons systeem toolook Hallo fout kunnen gebruiken</span><span class="sxs-lookup"><span data-stu-id="76228-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="76228-221">Voorbeeld: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="76228-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="76228-222">**UPN** – Hallo-gebruiker die Hallo is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="76228-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="76228-223">Voorbeeld:**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="76228-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="76228-224">**Tenant-Id** – Hallo unieke ID van Hallo tenant die gebruiker Hallo die Hallo bewerking uitgevoerd lid was van</span><span class="sxs-lookup"><span data-stu-id="76228-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="76228-225">Voorbeeld: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="76228-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="76228-226">**Gebruikersobject-Id** – Hallo unieke ID van het Hallo-gebruiker die Hallo is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="76228-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="76228-227">Voorbeeld: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="76228-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="76228-228">Gedetailleerde melding Items</span><span class="sxs-lookup"><span data-stu-id="76228-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="76228-229">**Weergavenaam** – **(kan niet leeg zijn)** een meer gedetailleerde weergavenaam voor Hallo-fout</span><span class="sxs-lookup"><span data-stu-id="76228-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="76228-230">Voorbeeld * – **Application proxy-instellingen**</span><span class="sxs-lookup"><span data-stu-id="76228-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="76228-231">**Status** – specifieke status van melding Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="76228-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="76228-232">Voorbeeld * – **is mislukt**</span><span class="sxs-lookup"><span data-stu-id="76228-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="76228-233">**Object-Id** – **(kan niet leeg zijn)** Hallo object-ID op basis van welke Hallo bewerking is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="76228-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="76228-234">Voorbeeld: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="76228-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="76228-235">**Details** – Hallo gedetailleerde beschrijving van wat is het gevolg van Hallo-bewerking</span><span class="sxs-lookup"><span data-stu-id="76228-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="76228-236">Voorbeeld: **interne url 'http://bing.com/' is ongeldig omdat het zich al in gebruik**</span><span class="sxs-lookup"><span data-stu-id="76228-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="76228-237">**Fout kopiëren** – klikt u op Hallo **pictogram kopiëren** toohello rechts van Hallo **Kopieerfout** textbox toocopy alle Hallo melding details tooshare met een medewerker van de groep ondersteuning of productupdates</span><span class="sxs-lookup"><span data-stu-id="76228-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="76228-238">Voorbeeld:```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="76228-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="76228-239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76228-239">Next steps</span></span>
[<span data-ttu-id="76228-240">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="76228-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

