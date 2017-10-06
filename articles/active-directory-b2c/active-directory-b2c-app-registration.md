---
title: 'Azure Active Directory B2C: toepassingsregistratie | Microsoft Docs'
description: Hoe tooregister uw toepassing met Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="70fab-103">Azure Active Directory B2C: uw toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="70fab-104">Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70fab-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="70fab-105">Wanneer u klaar bent, wordt uw toepassing geregistreerd voor gebruik in hello Azure B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="70fab-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70fab-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="70fab-106">Prerequisites</span></span>

<span data-ttu-id="70fab-107">toobuild een toepassing waarin zich kunnen registreren en aanmelden consumenten, moet u eerst tooregister Hallo toepassing met een Azure Active Directory B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="70fab-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="70fab-108">Haal uw eigen tenant met behulp van Hallo stappen die worden beschreven in [een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="70fab-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="70fab-109">Toepassingen die zijn gemaakt op basis van hello Azure AD B2C-blade in hello Azure-portal moeten worden beheerd vanaf Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="70fab-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="70fab-110">Als u Hallo B2C-toepassingen met PowerShell of een andere portal hebt bewerkt, moet deze worden niet ondersteund en werken niet met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="70fab-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="70fab-111">Zie de details in Hallo [mislukt apps](#faulted-apps) sectie.</span><span class="sxs-lookup"><span data-stu-id="70fab-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="70fab-112">Navigeer tooB2C instellingen</span><span class="sxs-lookup"><span data-stu-id="70fab-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="70fab-113">Meld u bij toohello [Azure-portal](https://portal.azure.com/) zoals Hallo globale beheerder van Hallo B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="70fab-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="70fab-114">De volgende stappen op basis van het toepassingstype Hallo die u registreert kiezen:</span><span class="sxs-lookup"><span data-stu-id="70fab-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="70fab-115">Een web-app registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="70fab-116">Een web-API registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="70fab-117">Een mobiele of native toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="70fab-118">Een web-app registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="70fab-119">Als de web-app een web-API aanroept die is beveiligd door Azure AD B2C, voert u deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="70fab-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="70fab-120">Maken van een toepassingsgeheim door te gaan toohello **sleutels** blade en te klikken op Hallo **sleutel genereren** knop.</span><span class="sxs-lookup"><span data-stu-id="70fab-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="70fab-121">Noteer Hallo **App-sleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="70fab-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="70fab-122">Hallo-waarde worden gebruikt als Hallo toepassingsgeheim in de code van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="70fab-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="70fab-123">Klik op **API-toegang**, klik op **Toevoegen** en selecteer uw web-API en bereiken (machtigingen).</span><span class="sxs-lookup"><span data-stu-id="70fab-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="70fab-124">Een **toepassingsgeheim** is een belangrijke beveiligingsreferentie en moet op de juiste wijze worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="70fab-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="70fab-125">Te gaan**volgende stappen**</span><span class="sxs-lookup"><span data-stu-id="70fab-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="70fab-126">Een web-API registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="70fab-127">Klik op **gepubliceerd scopes** tooadd meer scopes zo nodig.</span><span class="sxs-lookup"><span data-stu-id="70fab-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="70fab-128">Standaard is Hallo 'user_impersonation' bereik gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="70fab-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="70fab-129">Hallo user_impersonation bereik biedt andere toepassingen Hallo mogelijkheid tooaccess deze api namens Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="70fab-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="70fab-130">Als u wenst, kunt Hallo user_impersonation bereik worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="70fab-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="70fab-131">Te gaan**volgende stappen**</span><span class="sxs-lookup"><span data-stu-id="70fab-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="70fab-132">Een mobiele of native toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="70fab-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="70fab-133">Te gaan**volgende stappen**</span><span class="sxs-lookup"><span data-stu-id="70fab-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="70fab-134">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="70fab-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="70fab-135">De antwoord-URL van een web-app of -API kiezen</span><span class="sxs-lookup"><span data-stu-id="70fab-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="70fab-136">Apps die zijn geregistreerd bij Azure AD B2C zijn momenteel beperkt tooa beperkte set waarden voor antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="70fab-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="70fab-137">antwoord-URL voor web-apps en services met het schema Hallo beginnen moet Hallo `https`, en alle beantwoorden URL waarden moeten delen één DNS-domein.</span><span class="sxs-lookup"><span data-stu-id="70fab-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="70fab-138">U kunt bijvoorbeeld geen webtoepassing met een van deze antwoord-URL's registreren:</span><span class="sxs-lookup"><span data-stu-id="70fab-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="70fab-139">Hallo registratie system Vergelijkt Hallo volledige DNS-naam van Hallo bestaande antwoord-URL toohello DNS-naam van Hallo antwoord-URL die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="70fab-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="70fab-140">Hallo aanvraag tooadd Hallo DNS-naam mislukt als een van de Hallo volgende voorwaarden is voldaan:</span><span class="sxs-lookup"><span data-stu-id="70fab-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="70fab-141">Hallo hele DNS-naam van de nieuwe antwoord-URL Hallo komt niet overeen met de Hallo DNS-naam van Hallo bestaande antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="70fab-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="70fab-142">Hallo volledige DNS-naam van Hallo nieuwe antwoord-URL is niet een subdomein van Hallo bestaande antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="70fab-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="70fab-143">Als hello heeft app deze antwoord-URL:</span><span class="sxs-lookup"><span data-stu-id="70fab-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="70fab-144">U kunt tooit als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="70fab-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="70fab-145">In dit geval overeenkomt Hallo DNS-naam exact.</span><span class="sxs-lookup"><span data-stu-id="70fab-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="70fab-146">Of u kunt dit doen:</span><span class="sxs-lookup"><span data-stu-id="70fab-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="70fab-147">In dit geval verwijst u tooa DNS-subdomein van login.contoso.com. Als u een app waarvoor aanmelding east.contoso.com en aanmelding-west.contoso.com als URL's beantwoorden toohave wilt, moet u deze antwoord-URL's in deze volgorde toevoegen:</span><span class="sxs-lookup"><span data-stu-id="70fab-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="70fab-148">U kunt twee laatstgenoemde Hallo toevoegen omdat ze subdomeinen van Hallo eerste antwoord-URL, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="70fab-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="70fab-149">Een omleidings-URI voor een native app kiezen</span><span class="sxs-lookup"><span data-stu-id="70fab-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="70fab-150">Er zijn twee belangrijke overwegingen bij het kiezen van een omleidings-URI voor mobiele/native toepassingen:</span><span class="sxs-lookup"><span data-stu-id="70fab-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="70fab-151">**Unieke**: Hallo-schema van Hallo omleidings-URI moet uniek zijn voor elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="70fab-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="70fab-152">In ons voorbeeld (com.onmicrosoft.contoso.appname://redirect/path) gebruiken we com.onmicrosoft.contoso.appname als Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="70fab-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="70fab-153">We raden aan dit patroon te volgen.</span><span class="sxs-lookup"><span data-stu-id="70fab-153">We recommend following this pattern.</span></span> <span data-ttu-id="70fab-154">Als twee toepassingen Hallo delen dezelfde schema, hello gebruiker ziet een dialoogvenster 'Kies app'.</span><span class="sxs-lookup"><span data-stu-id="70fab-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="70fab-155">Als de gebruiker Hallo een onjuiste keuze, Hallo aanmelden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="70fab-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="70fab-156">**Volledig**: de omleidings-URI moet een schema en een pad hebben.</span><span class="sxs-lookup"><span data-stu-id="70fab-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="70fab-157">Hallo-pad moet ten minste één een slash bevatten na het Hallo-domein (bijvoorbeeld //contoso/ werkt en //contoso mislukt).</span><span class="sxs-lookup"><span data-stu-id="70fab-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="70fab-158">Zorg ervoor dat er geen speciale tekens zoals onderstrepingstekens in Hallo omleidings-uri.</span><span class="sxs-lookup"><span data-stu-id="70fab-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="70fab-159">Mislukte toepassingen</span><span class="sxs-lookup"><span data-stu-id="70fab-159">Faulted apps</span></span>

<span data-ttu-id="70fab-160">B2C-toepassingen moeten niet worden bewerkt:</span><span class="sxs-lookup"><span data-stu-id="70fab-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="70fab-161">Op andere appbeheerportals zoals de [klassieke Azure-portal](https://manage.windowsazure.com/) en de [portal voor appregistratie](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="70fab-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="70fab-162">Met Graph API of PowerShell</span><span class="sxs-lookup"><span data-stu-id="70fab-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="70fab-163">Als u Hallo B2C-toepassing bewerken, zoals hierboven wordt beschreven en tooedit probeert opnieuw in hello Azure AD B2C-functiesblade op Hallo van Azure-portal, wordt een fout-app en uw toepassing is niet langer bruikbaar met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="70fab-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="70fab-164">U hebt toodelete Hallo toepassing en maak deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="70fab-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="70fab-165">Ga toohello-app Hallo toodelete [toepassing Registratieportal](https://apps.dev.microsoft.com/) en er Hallo toepassing verwijderen.</span><span class="sxs-lookup"><span data-stu-id="70fab-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="70fab-166">Opdat Hallo toepassing toobe zichtbaar is moet u toobe Hallo eigenaar van de toepassing hello (en niet alleen een beheerder van Hallo tenant).</span><span class="sxs-lookup"><span data-stu-id="70fab-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70fab-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70fab-167">Next steps</span></span>

<span data-ttu-id="70fab-168">Nu dat u een toepassing die is geregistreerd bij Azure AD B2C hebt, kunt u een van voltooien [onze zelfstudies snel starten](active-directory-b2c-overview.md#get-started) tooget zetten.</span><span class="sxs-lookup"><span data-stu-id="70fab-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70fab-169">Een ASP.NET-web-app maken met registreren, aanmelden en wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="70fab-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)