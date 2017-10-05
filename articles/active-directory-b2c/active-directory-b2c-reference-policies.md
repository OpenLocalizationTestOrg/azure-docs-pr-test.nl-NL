---
title: 'Azure Active Directory B2C: Ingebouwde beleid | Microsoft Docs'
description: Een onderwerp in de uitbreidbaar beleidsframework van Azure Active Directory B2C en voor het maken van verschillende beleidstypen
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="2e5eb-103">Azure Active Directory B2C: Ingebouwde beleid</span><span class="sxs-lookup"><span data-stu-id="2e5eb-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="2e5eb-104">De uitbreidbaar beleidsframework van Azure Active Directory (Azure AD) B2C is de belangrijkste sterkte van de service.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="2e5eb-105">Volledig beschrijven consumer identiteitservaringen zoals beleidsregels registreren, aanmelden en profiel bewerken.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="2e5eb-106">Bijvoorbeeld, kunt een registratiebeleid u bepalen van gedrag door de volgende instellingen configureren:</span><span class="sxs-lookup"><span data-stu-id="2e5eb-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="2e5eb-107">Accounttypen (sociale accounts zoals Facebook) of lokale accounts zoals e-mailadressen die consumenten zich aanmelden voor de toepassing kunnen gebruiken</span><span class="sxs-lookup"><span data-stu-id="2e5eb-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="2e5eb-108">Kenmerken (bijvoorbeeld de voornaam, postcode en schoen grootte) worden opgehaald van de consument tijdens de registratie</span><span class="sxs-lookup"><span data-stu-id="2e5eb-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="2e5eb-109">Gebruik van Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2e5eb-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="2e5eb-110">Het uiterlijk van alle aanmeldingspagina 's</span><span class="sxs-lookup"><span data-stu-id="2e5eb-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="2e5eb-111">(Die zich voordoet als claims in een token) dat de toepassing wanneer het beleid ontvangt uitgevoerd is voltooid</span><span class="sxs-lookup"><span data-stu-id="2e5eb-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="2e5eb-112">U kunt meerdere beleidsregels met verschillende typen in uw tenant maken en gebruiken in uw toepassingen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="2e5eb-113">Beleid kunnen opnieuw worden gebruikt in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-113">Policies can be reused across applications.</span></span> <span data-ttu-id="2e5eb-114">Deze flexibiliteit kan ontwikkelaars definiëren en ervaringen van de consument identiteit met minimale of geen wijzigingen aangebracht in de code te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="2e5eb-115">Beleidsregels zijn beschikbaar voor gebruik via een eenvoudige developer-interface.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="2e5eb-116">Uw toepassing een beleid wordt geactiveerd met behulp van een standaard HTTP-authenticatie-aanvraag (het doorgeven van een parameter van het beleid in de aanvraag) en een aangepaste token als antwoord ontvangt.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="2e5eb-117">Het enige verschil tussen aanvragen die gebruikmaken van een registratiebeleid en aanvragen die gebruikmaken van een beleid voor aanmelden is bijvoorbeeld de naam van het beleid dat wordt gebruikt in de parameter 'p' query-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="2e5eb-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="2e5eb-118">Zie voor meer informatie over de beleidsframework [dit blogbericht over Azure AD B2C op de Enterprise Mobility and Security-Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e5eb-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="2e5eb-119">Maak een beleid registreren of aanmelden</span><span class="sxs-lookup"><span data-stu-id="2e5eb-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="2e5eb-120">Dit beleid verwerkt beide ervaringen consumenten registreren en aanmelden met een configuratie voor één.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="2e5eb-121">Consumenten worden omlaag het juiste pad (registreren of aanmelden) zijn afhankelijk van de context geleid.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="2e5eb-122">Hierin worden ook de inhoud van de tokens die de toepassing na geslaagde aanmelding-ups of aanmeldingen ontvangen.  Een voorbeeld van code voor het registreren of aanmelden beleid is [beschikbaar hier](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="2e5eb-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="2e5eb-123">Het wordt aanbevolen dat u dit beleid via een registratiebeleid en beleid voor aanmelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="2e5eb-124">Een registratiebeleid maken</span><span class="sxs-lookup"><span data-stu-id="2e5eb-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="2e5eb-125">Maak een beleid voor aanmelden</span><span class="sxs-lookup"><span data-stu-id="2e5eb-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="2e5eb-126">Maken van een profiel te bewerken van beleid</span><span class="sxs-lookup"><span data-stu-id="2e5eb-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="2e5eb-127">Maak een beleid voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="2e5eb-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="2e5eb-128">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="2e5eb-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="2e5eb-129">Hoe kan ik een beleid registreren of aanmelden met een beleid voor wachtwoordherstel koppelen?</span><span class="sxs-lookup"><span data-stu-id="2e5eb-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="2e5eb-130">Wanneer u een beleid registreren of aanmelden (met lokale accounts) maakt, ziet u een **wachtwoord vergeten?** koppeling op de eerste pagina van de gebruikerservaring.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="2e5eb-131">Op deze koppeling klikt herstellen niet automatisch trigger een wachtwoord beleid.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="2e5eb-132">In plaats daarvan de foutcode  **`AADB2C90118`**  wordt geretourneerd naar uw app.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="2e5eb-133">Uw app moet deze foutcode verwerkt door het aanroepen van een specifiek wachtwoord opnieuw instellen van beleid.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="2e5eb-134">Zie voor meer informatie een [voorbeeldbestand dat laat zien van de aanpak van het koppelen van beleidsregels](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="2e5eb-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="2e5eb-135">Moet ik een beleid registreren of aanmelden of een registratiebeleid en een beleid voor aanmelden gebruiken?</span><span class="sxs-lookup"><span data-stu-id="2e5eb-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="2e5eb-136">Het is raadzaam dat u een beleid registreren of aanmelden via een registratiebeleid en een beleid voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="2e5eb-137">Het registreren of aanmelden beleid heeft meer mogelijkheden dan het beleid voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="2e5eb-138">Ook kunt u gebruikmaken van pagina UI-aanpassing en biedt een betere ondersteuning voor lokalisatie.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="2e5eb-139">Het beleid voor aanmelden wordt aanbevolen als u niet nodig hebt voor uw beleid lokalisatie, alleen secundaire aanpassingsfuncties voor huisstijl nodig hebt en wilt wachtwoord opnieuw instellen die zijn ingebouwd.</span><span class="sxs-lookup"><span data-stu-id="2e5eb-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e5eb-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e5eb-140">Next steps</span></span>
* [<span data-ttu-id="2e5eb-141">Token, sessie en configuratie voor één aanmelding</span><span class="sxs-lookup"><span data-stu-id="2e5eb-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="2e5eb-142">E-mailverificatie tijdens registratie consumer uitschakelen</span><span class="sxs-lookup"><span data-stu-id="2e5eb-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

