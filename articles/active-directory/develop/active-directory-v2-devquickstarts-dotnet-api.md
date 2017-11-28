---
title: aaaAdd aanmelden tooa .NET MVC-web-API met behulp van Azure AD v2.0-eindpunt Hallo | Microsoft Docs
description: Hoe toobuild een .NET MVC Web-Api die tokens van beide persoonlijke Microsoft-Account en werk-of schoolaccounts accepteert.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="32fdd-103">Een MVC-web-API beveiligen</span><span class="sxs-lookup"><span data-stu-id="32fdd-103">Secure an MVC web API</span></span>
<span data-ttu-id="32fdd-104">U kunt met Azure Active Directory Hallo v2.0-eindpunt beveiligen een Web-API met [OAuth 2.0](active-directory-v2-protocols.md) toegangstokens, waardoor gebruikers met beide persoonlijke Microsoft-account en werk- of schoolaccount accounts toosecurely toegang tot uw Web-API.</span><span class="sxs-lookup"><span data-stu-id="32fdd-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="32fdd-105">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="32fdd-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="32fdd-106">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="32fdd-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="32fdd-107">In ASP.NET web-API's, kunt u dit doen met behulp van Microsoft OWIN middleware is opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="32fdd-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="32fdd-108">We gebruiken hier OWIN toobuild een 'tooDo lijst' MVC Web-API waarmee clients toocreate weergeven en lezen taken van de takenlijst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="32fdd-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="32fdd-109">Hallo-web-API valideert dat inkomende aanvragen een ongeldig toegangstoken bevatten en alle aanvragen die niet zijn gevalideerd op een beveiligde route afwijzen.</span><span class="sxs-lookup"><span data-stu-id="32fdd-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="32fdd-110">Dit voorbeeld is gebouwd met behulp van Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="32fdd-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="32fdd-111">Downloaden</span><span class="sxs-lookup"><span data-stu-id="32fdd-111">Download</span></span>
<span data-ttu-id="32fdd-112">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="32fdd-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="32fdd-113">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="32fdd-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="32fdd-114">Hallo geraamte app omvat alle Hallo standaardcode voor een eenvoudige API, maar alle Hallo identity-gerelateerde onderdelen ontbreken.</span><span class="sxs-lookup"><span data-stu-id="32fdd-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="32fdd-115">Als u toofollow langs niet wilt, kunt u in plaats daarvan klonen of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="32fdd-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="32fdd-116">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="32fdd-116">Register an app</span></span>
<span data-ttu-id="32fdd-117">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="32fdd-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="32fdd-118">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="32fdd-118">Make sure to:</span></span>

* <span data-ttu-id="32fdd-119">Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="32fdd-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="32fdd-120">Deze visual studio-oplossing bevat ook een 'TodoListClient', dit een eenvoudige WPF-app is.</span><span class="sxs-lookup"><span data-stu-id="32fdd-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="32fdd-121">Hallo TodoListClient gebruikte toodemonstrate hoe een gebruiker zich aanmeldt is en hoe u een client kan verlenen tooyour Web API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="32fdd-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="32fdd-122">In dit geval Hallo TodoListClient zowel Hallo TodoListService worden vertegenwoordigd door Hallo dezelfde app.</span><span class="sxs-lookup"><span data-stu-id="32fdd-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="32fdd-123">tooconfigure Hallo TodoListClient, moet u ook:</span><span class="sxs-lookup"><span data-stu-id="32fdd-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="32fdd-124">Hallo toevoegen **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="32fdd-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="32fdd-125">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="32fdd-125">Install OWIN</span></span>
<span data-ttu-id="32fdd-126">Nu u een app hebt geregistreerd, moet u tooset van uw app toocommunicate met Hallo v2.0-eindpunt in de volgorde toovalidate inkomende aanvragen & tokens.</span><span class="sxs-lookup"><span data-stu-id="32fdd-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="32fdd-127">toobegin, open Hallo oplossing en Hallo OWIN middleware NuGet-pakketten toohello TodoListService-project toevoegen met behulp van Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="32fdd-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="32fdd-128">OAuth-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="32fdd-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="32fdd-129">Voeg een OWIN klasse toohello TodoListService opstartproject aangeroepen `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="32fdd-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="32fdd-130">Rechtermuisknop te klikken op op Hallo project--> **toevoegen** --> **Nieuw Item** --> Zoek naar 'OWIN'.</span><span class="sxs-lookup"><span data-stu-id="32fdd-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="32fdd-131">Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="32fdd-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="32fdd-132">Hallo klassendeclaratie ook wijzigen`public partial class Startup` -we hebben u al deel uit van deze klasse geïmplementeerd in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="32fdd-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="32fdd-133">In Hallo `Configuration(…)` methode, een aanroep van tooConfgureAuth(...) tooset van verificatie voor uw web-app maken.</span><span class="sxs-lookup"><span data-stu-id="32fdd-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="32fdd-134">Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(…)` methode die Hallo Web API tooaccept tokens van Hallo v2.0-eindpunt wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="32fdd-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="32fdd-135">Nu kunt u `[Authorize]` tooprotect kenmerken uw domeincontrollers en de acties met OAuth 2.0-bearer-verificatie.</span><span class="sxs-lookup"><span data-stu-id="32fdd-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="32fdd-136">Hallo opmaken `Controllers\TodoListController.cs` klasse met een tag autoriseren.</span><span class="sxs-lookup"><span data-stu-id="32fdd-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="32fdd-137">Hierdoor moeten Hallo gebruiker toosign in voor de toegang tot deze pagina.</span><span class="sxs-lookup"><span data-stu-id="32fdd-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="32fdd-138">Wanneer een geautoriseerde beller is roept een Hallo `TodoListController` API's, Hallo actie mogelijk moet toegang tot tooinformation over Hallo aanroeper.</span><span class="sxs-lookup"><span data-stu-id="32fdd-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="32fdd-139">OWIN toegang toohello claims binnen Hallo bearer-token via Hallo levert `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="32fdd-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="32fdd-140">Tot slot opent Hallo `web.config` bestand in de hoofdmap Hallo van Hallo TodoListService project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="32fdd-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="32fdd-141">Uw `ida:Audience` Hallo is **toepassings-Id** van Hallo-app die u hebt ingevoerd in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="32fdd-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="32fdd-142">Hallo client-app configureren</span><span class="sxs-lookup"><span data-stu-id="32fdd-142">Configure hello client app</span></span>
<span data-ttu-id="32fdd-143">Voordat u Hallo Todo List-Service in actie zien kunt, moet u tooconfigure Hallo Todo lijst Client, zodat het kan tokens van Hallo v2.0-eindpunt verkrijgen en aanroepen toohello service maken.</span><span class="sxs-lookup"><span data-stu-id="32fdd-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="32fdd-144">Open in Hallo TodoListClient project `App.config` en voer de configuratiewaarden van uw in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="32fdd-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="32fdd-145">Uw `ida:ClientId` toepassings-Id die u hebt gekopieerd uit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="32fdd-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="32fdd-146">Ten slotte wilt opschonen, bouwen en uitvoeren van elk project!</span><span class="sxs-lookup"><span data-stu-id="32fdd-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="32fdd-147">U hebt nu een .NET MVC Web-API die tokens van beide persoonlijke Microsoft-accounts en werk-of schoolaccounts accepteert.</span><span class="sxs-lookup"><span data-stu-id="32fdd-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="32fdd-148">Meld u aan bij Hallo TodoListClient en roept u de takenlijst web api tooadd taken toohello van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="32fdd-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="32fdd-149">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="32fdd-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="32fdd-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32fdd-150">Next steps</span></span>
<span data-ttu-id="32fdd-151">U kunt nu verplaatsen naar andere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="32fdd-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="32fdd-152">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="32fdd-152">You may want tootry:</span></span>

[<span data-ttu-id="32fdd-153">Een Web-API aanroept vanuit een Web-App >></span><span class="sxs-lookup"><span data-stu-id="32fdd-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="32fdd-154">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="32fdd-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="32fdd-155">Hallo v2.0 ontwikkelaarshandleiding >></span><span class="sxs-lookup"><span data-stu-id="32fdd-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="32fdd-156">StackOverflow 'azure active directory'-tag >></span><span class="sxs-lookup"><span data-stu-id="32fdd-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="32fdd-157">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="32fdd-157">Get security updates for our products</span></span>
<span data-ttu-id="32fdd-158">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="32fdd-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
