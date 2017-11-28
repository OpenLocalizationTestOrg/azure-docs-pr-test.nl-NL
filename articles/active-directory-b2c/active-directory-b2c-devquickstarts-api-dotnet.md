---
title: aaaAzure AD B2C | Microsoft Docs
description: Hoe toobuild een .NET-Web-API met behulp van Azure Active Directory B2C, beveiligd met OAuth 2.0-toegangstokens voor verificatie.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="7b0c4-103">Azure Active Directory B2C: een .NET-web-API maken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="7b0c4-104">Met Azure Active Directory (Azure AD) B2C kunt u een web-API beveiligen met OAuth 2.0-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="7b0c4-105">Deze tokens kunnen uw client-apps tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="7b0c4-106">Dit artikel laat zien hoe een .NET MVC-API 'takenlijst' toocreate die kunnen gebruikers van uw toepassing tooCRUD taken.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="7b0c4-107">Hallo-web-API is beveiligd met Azure AD B2C en alleen hun takenlijst kan toomanage geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="7b0c4-108">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="7b0c4-109">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="7b0c4-110">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="7b0c4-111">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="7b0c4-112">Hallo-clienttoepassing en web-API moeten Hallo dezelfde Azure AD B2C-directory gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="7b0c4-113">Een web-API maken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-113">Create a web API</span></span>

<span data-ttu-id="7b0c4-114">Vervolgens moet u een web API-app toocreate in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="7b0c4-115">Hiermee geeft u Azure AD-informatie of deze behoeften toosecurely met uw app communiceren.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="7b0c4-116">toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="7b0c4-117">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-117">Be sure to:</span></span>

* <span data-ttu-id="7b0c4-118">Omvatten een **web-app** of **web-API** in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="7b0c4-119">Gebruik Hallo **omleidings-URI** `https://localhost:44332/` voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="7b0c4-120">Dit is de standaardlocatie Hallo van Hallo web app-client voor dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="7b0c4-121">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="7b0c4-122">U hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-122">You'll need it later.</span></span>
* <span data-ttu-id="7b0c4-123">Voer een app-id **URI voor de app-id** in.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="7b0c4-124">Machtigingen via Hallo toevoegen **gepubliceerd scopes** menu.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="7b0c4-125">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-125">Create your policies</span></span>

<span data-ttu-id="7b0c4-126">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7b0c4-127">U moet toocreate een toocommunicate beleid met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="7b0c4-128">Het is raadzaam met behulp van Hallo gecombineerd sign-up-to-date/aanmelden beleid, zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7b0c4-129">Wanneer u het beleid maakt, vergeet dan niet het volgende:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="7b0c4-130">Kies een **Weergavenaam** en andere registratiekenmerken in uw beleid.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="7b0c4-131">Kiest u **Weergavenaam**- en **Object-id**-claims als toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="7b0c4-132">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="7b0c4-133">Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="7b0c4-134">U hebt de beleidsnaam hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="7b0c4-135">Wanneer u Hallo beleid hebt gemaakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="7b0c4-136">Hallo code downloaden</span><span class="sxs-lookup"><span data-stu-id="7b0c4-136">Download hello code</span></span>

<span data-ttu-id="7b0c4-137">Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="7b0c4-138">U kunt Hallo voorbeeld klonen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="7b0c4-139">Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="7b0c4-140">Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="7b0c4-141">`TaskWebApp`is een MVC-webtoepassing die gebruiker Hallo communiceert met.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="7b0c4-142">`TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="7b0c4-143">In dit artikel wordt alleen besproken Hallo `TaskService` toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="7b0c4-144">toolearn hoe toobuild `TaskWebApp` met behulp van Azure AD B2C, Zie [onze zelfstudie .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="7b0c4-145">Hello Azure AD B2C-configuratie bijwerken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="7b0c4-146">Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="7b0c4-147">Als u toouse wilt uw eigen tenant, moet u toodo hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="7b0c4-148">Open `web.config` in Hallo `TaskService` project en vervang de waarden voor Hallo</span><span class="sxs-lookup"><span data-stu-id="7b0c4-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="7b0c4-149">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="7b0c4-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="7b0c4-150">`ida:ClientId` door de id van uw web-API-toepassing</span><span class="sxs-lookup"><span data-stu-id="7b0c4-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="7b0c4-151">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="7b0c4-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="7b0c4-152">Open `web.config` in Hallo `TaskWebApp` project en vervang de waarden voor Hallo</span><span class="sxs-lookup"><span data-stu-id="7b0c4-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="7b0c4-153">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="7b0c4-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="7b0c4-154">`ida:ClientId` door de id van uw web-app-toepassing</span><span class="sxs-lookup"><span data-stu-id="7b0c4-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="7b0c4-155">`ida:ClientSecret` door de geheime sleutel voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="7b0c4-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="7b0c4-156">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="7b0c4-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="7b0c4-157">`ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid</span><span class="sxs-lookup"><span data-stu-id="7b0c4-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="7b0c4-158">`ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid</span><span class="sxs-lookup"><span data-stu-id="7b0c4-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="7b0c4-159">Hallo-API beveiligen</span><span class="sxs-lookup"><span data-stu-id="7b0c4-159">Secure hello API</span></span>

<span data-ttu-id="7b0c4-160">Wanneer u een client hebt die de API aanroept, kunt u uw API (bijv. `TaskService`) beveiligen met Bearer-tokens van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="7b0c4-161">Dit zorgt ervoor dat elke aanvraag tooyour API worden pas geldig als het Hallo-aanvraag heeft een bearer-token.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="7b0c4-162">De API kan Bearer-tokens accepteren en valideren met behulp van de Microsoft Open Web Interface voor .NET-bibliotheek (OWIN).</span><span class="sxs-lookup"><span data-stu-id="7b0c4-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="7b0c4-163">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="7b0c4-163">Install OWIN</span></span>

<span data-ttu-id="7b0c4-164">Beginnen met het Hallo OWIN OAuth-verificatiepijplijn installeren met behulp van Hallo Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="7b0c4-165">Hiermee installeert u Hallo OWIN middleware waarmee accepteert en bearer-tokens te valideren.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="7b0c4-166">Een OWIN-opstartklasse toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b0c4-166">Add an OWIN startup class</span></span>

<span data-ttu-id="7b0c4-167">Voeg een OWIN starten van de klasse toohello API aangeroepen `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="7b0c4-168">Met de rechtermuisknop op het Hallo-project, selecteer **toevoegen** en **Nieuw Item**, en zoek naar OWIN.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="7b0c4-169">Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="7b0c4-170">In ons voorbeeld wijzigen we Hallo klassendeclaratie te`public partial class Startup` en geïmplementeerd met andere onderdelen van de klasse in Hallo Hallo `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="7b0c4-171">Hallo binnen `Configuration` methode, hebben we een gesprek te toegevoegd`ConfigureAuth`, die is gedefinieerd in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="7b0c4-172">Na het Hallo-wijzigingen `Startup.cs` Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="7b0c4-173">OAuth 2.0-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="7b0c4-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="7b0c4-174">Open Hallo bestand `App_Start\Startup.Auth.cs`, en implementeren van Hallo `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="7b0c4-175">Bijvoorbeeld, eruit het volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b0c4-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="7b0c4-176">Hallo taakcontroller beveiligen</span><span class="sxs-lookup"><span data-stu-id="7b0c4-176">Secure hello task controller</span></span>

<span data-ttu-id="7b0c4-177">Zodra Hallo app geconfigureerde toouse OAuth 2.0-verificatie, kunt u uw web-API beveiligen door het toevoegen van een `[Authorize]` tag toohello taakcontroller.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="7b0c4-178">Dit is Hallo controller waarop alle bewerkingen van de takenlijst uitgevoerd, worden dus moet u de hele controller Hallo op Hallo klasseniveau beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="7b0c4-179">U kunt ook toevoegen Hallo `[Authorize]` tag tooindividual acties voor nauwkeuriger beheer.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="7b0c4-180">Gebruikersgegevens uit Hallo-token ophalen</span><span class="sxs-lookup"><span data-stu-id="7b0c4-180">Get user information from hello token</span></span>

<span data-ttu-id="7b0c4-181">`TasksController`slaat taken in een database waarin elke taak een gekoppelde gebruiker die 'eigenaar' hello taak heeft.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="7b0c4-182">Hallo eigenaar wordt geïdentificeerd met van Hallo gebruiker **object-ID**.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="7b0c4-183">(Dit is de reden waarom u tooadd Hallo object-ID als een toepassing nodig toepassingsclaim in al uw beleidsregels.)</span><span class="sxs-lookup"><span data-stu-id="7b0c4-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="7b0c4-184">Hallo machtigingen in Hallo token valideren</span><span class="sxs-lookup"><span data-stu-id="7b0c4-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="7b0c4-185">Een algemene vereiste voor web-API's is toovalidate Hallo 'scopes' Hallo token aanwezig.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="7b0c4-186">Dit zorgt ervoor dat die gebruiker Hallo heeft ingestemd toohello machtigingen vereist tooaccess Hallo taak list-service.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="7b0c4-187">Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7b0c4-187">Run hello sample app</span></span>

<span data-ttu-id="7b0c4-188">Bouw ten slotte `TaskWebApp` en `TaskService` en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="7b0c4-189">Sommige taken in de takenlijst van de gebruiker Hallo maken en u ziet hoe ze worden doorgevoerd in Hallo API zelfs na het stoppen en het Hallo-client opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="7b0c4-190">Het beleid bewerken</span><span class="sxs-lookup"><span data-stu-id="7b0c4-190">Edit your policies</span></span>

<span data-ttu-id="7b0c4-191">Nadat u een API hebt beveiligd met behulp van Azure AD B2C, kunt u experimenteren met uw Sign-in/Sign-up-to-date beleid en het Hallo-effecten weergeven (of ontbreken daarvan) op Hallo API.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="7b0c4-192">U kunt toepassingsclaims voor Hallo Hallo beleidsregels bewerken en Hallo gebruikersgegevens die beschikbaar is in Hallo web-API wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="7b0c4-193">Claims die u toevoegt worden beschikbaar tooyour .NET MVC web-API in Hallo `ClaimsPrincipal` object, zoals eerder in dit artikel is beschreven.</span><span class="sxs-lookup"><span data-stu-id="7b0c4-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
