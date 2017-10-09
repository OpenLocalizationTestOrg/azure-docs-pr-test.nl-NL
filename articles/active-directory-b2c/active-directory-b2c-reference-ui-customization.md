---
title: Aanpassingen van de gebruikersinterface (UI) - Azure AD B2C | Microsoft Docs
description: Een onderwerp op Hallo gebruiker gebruikersinterface (UI) aanpassingsfuncties in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="b8ef8-103">Azure Active Directory B2C: Hello Azure AD B2C-gebruikersinterface (UI) aanpassen</span><span class="sxs-lookup"><span data-stu-id="b8ef8-103">Azure Active Directory B2C: Customize hello Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="b8ef8-104">Gebruikerservaring is uitermate belangrijk in een klantgerichte toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="b8ef8-105">Uw klant base vergroten door gebruikerservaringen met Hallo uiterlijk van uw merk.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-105">Grow your customer base by crafting user experiences with hello look and feel of your brand.</span></span> <span data-ttu-id="b8ef8-106">Azure Active Directory B2C (Azure AD B2C) kunt u aanpassen registreren, aanmelden, profiel bewerken en wachtwoord opnieuw instellen van pagina's met pixel perfect besturingselement.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ef8-107">Hallo pagina UI aanpassing functie die wordt beschreven in dit artikel is niet van toepassing toohello aanmelden alleen beleid, de bijbehorende pagina voor het opnieuw instellen van wachtwoorden en verificatie van e-mailberichten.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-107">hello page UI customization feature described in this article does not apply toohello sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="b8ef8-108">Deze functies gebruiken Hallo [functie huisstijl](../active-directory/active-directory-add-company-branding.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-108">These features use hello [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="b8ef8-109">Dit artikel behandelt Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="b8ef8-109">This article covers hello following topics:</span></span>

* <span data-ttu-id="b8ef8-110">Hallo pagina UI aanpassing-functie.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-110">hello page UI customization feature.</span></span>
* <span data-ttu-id="b8ef8-111">Een hulpprogramma voor het uploaden van HTML-inhoud tooAzure Blob-opslag voor gebruik met Hallo pagina UI-functie voor aanpassing.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-111">A tool for uploading HTML content tooAzure Blob Storage for use with hello page UI customization feature.</span></span>
* <span data-ttu-id="b8ef8-112">Hallo UI-elementen die worden gebruikt door Azure AD B2C die u kunt aanpassen met behulp van Cascading stylesheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-112">hello UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="b8ef8-113">Aanbevolen procedures bij het uitoefenen van deze functie.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-113">Best practices when exercising this feature.</span></span>

## <a name="hello-page-ui-customization-feature"></a><span data-ttu-id="b8ef8-114">Hallo pagina UI-functie voor aanpassing</span><span class="sxs-lookup"><span data-stu-id="b8ef8-114">hello page UI customization feature</span></span>

<span data-ttu-id="b8ef8-115">U kunt aanpassen Hallo uiterlijk aan van de klant registreren, aanmelden, wachtwoord opnieuw instellen en profiel bewerken's (door het configureren van [beleid](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-115">You can customize hello look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="b8ef8-116">Uw klanten krijgen een naadloze ervaring bij het navigeren tussen de toepassing en pagina's die worden bediend door Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="b8ef8-117">In tegenstelling tot andere services waar de opties van de gebruikersinterface, maakt gebruik van Azure AD B2C een eenvoudige en moderne tooUI aanpassing benaderen.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach tooUI customization.</span></span>

<span data-ttu-id="b8ef8-118">Dit is hoe het werkt: Azure AD B2C wordt code wordt uitgevoerd in de browser van uw klant en maakt gebruik van een benadering van moderne aangeroepen [Cross-Origin-Resource delen (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="b8ef8-119">Inhoud wordt geladen tijdens runtime, via een URL die u in een beleid opgeeft.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="b8ef8-120">U kunt verschillende URL's voor verschillende pagina's opgeven.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="b8ef8-121">Nadat geladen vanuit de URL van uw inhoud wordt samengevoegd met een HTML-fragment van Azure AD B2C wordt ingevoegd, is Hallo pagina weergegeven tooyour klant.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, hello page is displayed tooyour customer.</span></span> <span data-ttu-id="b8ef8-122">U hoeft alleen toodo is:</span><span class="sxs-lookup"><span data-stu-id="b8ef8-122">All you need toodo is:</span></span>

1. <span data-ttu-id="b8ef8-123">HTML5 juist opgemaakte inhoud met een lege maken `<div id="api"></div>` element zich ergens in Hallo `<body>`.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in hello `<body>`.</span></span> <span data-ttu-id="b8ef8-124">Dit element aanhalingstekens waar hello Azure AD B2C-inhoud wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-124">This element marks where hello Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="b8ef8-125">Host uw inhoud op een HTTPS-eindpunt (met CORS toegestaan).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="b8ef8-126">Houd er rekening mee beide ophalen en opties aanvraagmethoden moeten zijn ingeschakeld wanneer u CORS configureert.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="b8ef8-127">Gebruik CSS toostyle Hallo UI-elementen die worden ingevoegd door Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-127">Use CSS toostyle hello UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="b8ef8-128">Een eenvoudige voorbeeld van aangepaste HTML</span><span class="sxs-lookup"><span data-stu-id="b8ef8-128">A basic example of customized HTML</span></span>

<span data-ttu-id="b8ef8-129">Hallo volgt is Hallo meest eenvoudige HTML-inhoud die u tootest deze mogelijkheid gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-129">hello following example is hello most basic HTML content that you can use tootest this capability.</span></span> <span data-ttu-id="b8ef8-130">Gebruik Hallo [hulpprogramma helper](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload en het configureren van deze inhoud op uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-130">Use hello [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="b8ef8-131">Vervolgens kunt u controleren dat Hallo basic, niet-vorm van een gestileerde knoppen & formuliervelden op elke pagina weergegeven en werken worden.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-131">You can then verify that hello basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a><span data-ttu-id="b8ef8-132">Testen van Hallo UI-functie voor aanpassing</span><span class="sxs-lookup"><span data-stu-id="b8ef8-132">Test out hello UI customization feature</span></span>

<span data-ttu-id="b8ef8-133">Tootry uit Hallo-functie voor het aanpassen van gebruikersinterface wilt met behulp van onze voorbeeldinhoud HTML en CSS?</span><span class="sxs-lookup"><span data-stu-id="b8ef8-133">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="b8ef8-134">We bieden u [een helper-hulpprogramma](active-directory-b2c-reference-ui-customization-helper-tool.md) die uploadt en configureert u voorbeelden van uw Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ef8-135">U kunt de inhoud van uw gebruikersinterface overal hosten: op webservers CDN, AWS S3, delen bestandssystemen, enzovoort. Zolang het Hallo-inhoud wordt gehost op een openbaar HTTPS-eindpunt met CORS ingeschakeld, zijn goede toogo.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as hello content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good toogo.</span></span> <span data-ttu-id="b8ef8-136">We ter illustratie alleen Azure Blob-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="b8ef8-137">Hallo UI fragmenten ingesloten door Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b8ef8-137">hello UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="b8ef8-138">Hallo volgende secties geven lijsten Hallo HTML5-fragmenten die Azure AD B2C wordt samengevoegd in Hallo `<div id="api"></div>` element zich in uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-138">hello following sections list hello HTML5 fragments that Azure AD B2C merges into hello `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="b8ef8-139">**Voeg deze fragmenten geen uw HTML 5-inhoud.**</span><span class="sxs-lookup"><span data-stu-id="b8ef8-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="b8ef8-140">Hello Azure AD B2C-service wordt deze in ingevoegd tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-140">hello Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="b8ef8-141">Deze fragmenten gebruiken als referentiemateriaal bij het ontwerpen van uw eigen Cascading stylesheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a><span data-ttu-id="b8ef8-142">Fragment 'Pagina identiteit provider selecteren' hello ingevoegd</span><span class="sxs-lookup"><span data-stu-id="b8ef8-142">Fragment inserted into hello "Identity provider selection page"</span></span>

<span data-ttu-id="b8ef8-143">Deze pagina bevat een lijst met de id-providers die gebruiker Hallo uit tijdens het registreren of aanmelden kiezen kunnen.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-143">This page contains a list of identity providers that hello user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="b8ef8-144">Deze knoppen bevatten sociale id-providers zoals Facebook en Google + of lokale accounts (op basis van e-mailadres of de gebruiker naam).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a><span data-ttu-id="b8ef8-145">Fragment 'lokale account-aanmeldingspagina' hello ingevoegd</span><span class="sxs-lookup"><span data-stu-id="b8ef8-145">Fragment inserted into hello "Local account sign-up page"</span></span>

<span data-ttu-id="b8ef8-146">Deze pagina bevat een formulier voor het lokale account aanmelding op basis van een e-mailadres of een gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="b8ef8-147">Hallo formulier kan andere invoer besturingselementen zoals tekstinvoervak, vermelding wachtwoordvak keuzerondje, één vervolgkeuzelijsten en meervoudige selectie selectievakjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-147">hello form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a><span data-ttu-id="b8ef8-148">Fragment ingevoegd in Hallo '' sociale account aanmeldpagina'</span><span class="sxs-lookup"><span data-stu-id="b8ef8-148">Fragment inserted into hello ""Social account sign-up page"</span></span>

<span data-ttu-id="b8ef8-149">Deze pagina kan worden weergegeven wanneer u zich aanmeldt met een bestaand account van een identiteitsprovider van sociale zoals Facebook of Google +.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="b8ef8-150">Deze wordt gebruikt wanneer u meer informatie moet worden verzameld van de eindgebruiker Hallo met behulp van een aanmeldingsformulier hebt ingevuld.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-150">It is used when additional information must be collected from hello end user using a sign-up form.</span></span> <span data-ttu-id="b8ef8-151">Deze pagina is vergelijkbaar toohello lokale account registratiepagina (weergegeven in de vorige sectie Hallo) met uitzondering van Hallo wachtwoord invoervelden Hallo.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-151">This page is similar toohello local account sign-up page (shown in hello previous section) with hello exception of hello password entry fields.</span></span>

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="b8ef8-152">Fragment ingevoegd in Hallo "Unified registreren of aanmelden pagina'</span><span class="sxs-lookup"><span data-stu-id="b8ef8-152">Fragment inserted into hello "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="b8ef8-153">Deze pagina verwerkt zowel registreren en aanmelden aan klanten, die sociale id-providers zoals Facebook of Google + of lokale accounts kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a><span data-ttu-id="b8ef8-154">Fragment ingevoegd in Hallo "multi-factor authentication-page"</span><span class="sxs-lookup"><span data-stu-id="b8ef8-154">Fragment inserted into hello "Multi-factor authentication page"</span></span>

<span data-ttu-id="b8ef8-155">Gebruikers kunnen hun telefoonnummers (met behulp van de tekst of stem) verifiëren tijdens het registreren of aanmelden op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a><span data-ttu-id="b8ef8-156">Fragment '' foutpagina' hello ingevoegd</span><span class="sxs-lookup"><span data-stu-id="b8ef8-156">Fragment inserted into hello ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="b8ef8-157">Lokalisatie van uw HTML-inhoud</span><span class="sxs-lookup"><span data-stu-id="b8ef8-157">Localizing your HTML content</span></span>

<span data-ttu-id="b8ef8-158">U kunt uw HTML-inhoud door het inschakelen van lokaliseren ['Aanpassing taal'](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="b8ef8-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="b8ef8-159">Azure AD B2C tooforward Hallo Open ID Connect parameter inschakelen van deze functie kunt `ui-locales`, tooyour-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-159">Enabling this feature allows Azure AD B2C tooforward hello Open ID Connect parameter, `ui-locales`, tooyour endpoint.</span></span>  <span data-ttu-id="b8ef8-160">De inhoudsserver kunt deze parameter tooprovide aangepast HTML-pagina's die een specifieke taal zijn gebonden.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-160">Your content server can use this parameter tooprovide customized HTML pages that are language-specific.</span></span>

## <a name="things-tooremember-when-building-your-own-content"></a><span data-ttu-id="b8ef8-161">Dingen tooremember tijdens het bouwen van uw eigen inhoud</span><span class="sxs-lookup"><span data-stu-id="b8ef8-161">Things tooremember when building your own content</span></span>

<span data-ttu-id="b8ef8-162">Wanneer u van plan bent toouse Hallo pagina UI aanpassing-functie, controleert u Hallo aanbevolen procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="b8ef8-162">If you are planning toouse hello page UI customization feature, review hello following best practices:</span></span>

* <span data-ttu-id="b8ef8-163">Geen hello Azure AD B2C van standaardinhoud kopiëren en toomodify probeert deze.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-163">Don't copy hello Azure AD B2C's default content and attempt toomodify it.</span></span> <span data-ttu-id="b8ef8-164">Het is aanbevolen toobuild uw HTML5-inhoud van het begin- en toouse standaardinhoud als verwijzing.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-164">It is best toobuild your HTML5 content from scratch and toouse default content as reference.</span></span>
* <span data-ttu-id="b8ef8-165">Uit veiligheidsoverwegingen we kunt u geen tooinclude alle JavaScript in uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-165">For security reasons, we don't allow you tooinclude any JavaScript in your content.</span></span> <span data-ttu-id="b8ef8-166">Wat u moet de meeste zijn out of box Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-166">Most of what you need should be available out of hello box.</span></span> <span data-ttu-id="b8ef8-167">Als dit niet het geval is, gebruik [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nieuwe functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="b8ef8-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest new functionality.</span></span>
* <span data-ttu-id="b8ef8-168">Ondersteunde browserversies:</span><span class="sxs-lookup"><span data-stu-id="b8ef8-168">Supported browser versions:</span></span>
  * <span data-ttu-id="b8ef8-169">Internet Explorer 11, 10, rand</span><span class="sxs-lookup"><span data-stu-id="b8ef8-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="b8ef8-170">Beperkte ondersteuning voor Internet Explorer 9 kunt 8</span><span class="sxs-lookup"><span data-stu-id="b8ef8-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="b8ef8-171">Google Chrome 42.0 en hoger</span><span class="sxs-lookup"><span data-stu-id="b8ef8-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="b8ef8-172">Mozilla Firefox 38.0 en hoger</span><span class="sxs-lookup"><span data-stu-id="b8ef8-172">Mozilla Firefox 38.0 and above</span></span>
