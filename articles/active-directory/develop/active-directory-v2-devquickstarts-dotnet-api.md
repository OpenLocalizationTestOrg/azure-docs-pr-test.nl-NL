---
title: Aanmelden voor een .NET MVC-web-API met behulp van het Azure AD v2.0-eindpunt toevoegen | Microsoft Docs
description: Het bouwen van een .NET MVC Web-Api die tokens van beide persoonlijke Microsoft-Account accepteert en werk- of schoolaccount accounts.
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
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="d56b9-103">Een MVC-web-API beveiligen</span><span class="sxs-lookup"><span data-stu-id="d56b9-103">Secure an MVC web API</span></span>
<span data-ttu-id="d56b9-104">U kunt met Azure Active Directory het v2.0-eindpunt, beveiligen een Web-API met [OAuth 2.0](active-directory-v2-protocols.md) tokens, waardoor gebruikers met beide persoonlijke Microsoft-account openen en werk- of schoolaccount gebruikersaccounts aan veilige toegang tot uw Web-API.</span><span class="sxs-lookup"><span data-stu-id="d56b9-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="d56b9-105">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d56b9-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d56b9-106">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d56b9-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="d56b9-107">In ASP.NET web-API's, kunt u dit doen met behulp van Microsoft OWIN middleware is opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d56b9-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="d56b9-108">We gebruiken hier OWIN voor het bouwen van een 'Takenlijst' MVC Web-API waarmee clients kunnen maken en taken te lezen uit de takenlijst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d56b9-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="d56b9-109">De web-API valideert dat inkomende aanvragen een ongeldig toegangstoken bevatten en alle aanvragen die niet zijn gevalideerd op een beveiligde route afwijzen.</span><span class="sxs-lookup"><span data-stu-id="d56b9-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="d56b9-110">Dit voorbeeld is gebouwd met behulp van Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d56b9-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="d56b9-111">Downloaden</span><span class="sxs-lookup"><span data-stu-id="d56b9-111">Download</span></span>
<span data-ttu-id="d56b9-112">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="d56b9-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="d56b9-113">Als u wilt volgen, kunt u [basis van de app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="d56b9-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="d56b9-114">De geraamte app omvat alle standaardcode voor een eenvoudige API, maar alle benodigde onderdelen identiteitsgerelateerde ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="d56b9-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="d56b9-115">Als u niet volgen wilt, kunt u in plaats daarvan klonen of [het voltooide voorbeeld downloaden](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d56b9-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="d56b9-116">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="d56b9-116">Register an app</span></span>
<span data-ttu-id="d56b9-117">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d56b9-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d56b9-118">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="d56b9-118">Make sure to:</span></span>

* <span data-ttu-id="d56b9-119">Noteer de **toepassings-Id** toegewezen aan uw app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="d56b9-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="d56b9-120">Deze visual studio-oplossing bevat ook een 'TodoListClient', dit een eenvoudige WPF-app is.</span><span class="sxs-lookup"><span data-stu-id="d56b9-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="d56b9-121">De TodoListClient wordt gebruikt om u te laten zien hoe een gebruiker zich aanmeldt en hoe een client aanvragen kunt geven tot uw Web-API.</span><span class="sxs-lookup"><span data-stu-id="d56b9-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="d56b9-122">In dit geval worden zowel de TodoListClient en de TodoListService vertegenwoordigd door dezelfde app.</span><span class="sxs-lookup"><span data-stu-id="d56b9-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="d56b9-123">Als u wilt de TodoListClient configureren, moet u ook:</span><span class="sxs-lookup"><span data-stu-id="d56b9-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="d56b9-124">Voeg de **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="d56b9-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="d56b9-125">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="d56b9-125">Install OWIN</span></span>
<span data-ttu-id="d56b9-126">Nu u een app hebt geregistreerd, moet u uw app instellen om te communiceren met het v2.0-eindpunt om te valideren van binnenkomende aanvragen en -tokens.</span><span class="sxs-lookup"><span data-stu-id="d56b9-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="d56b9-127">Om te beginnen, opent u de oplossing en de OWIN middleware NuGet-pakketten toevoegen aan het TodoListService-project met de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="d56b9-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="d56b9-128">OAuth-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="d56b9-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="d56b9-129">Een OWIN-Opstartklasse toevoegen aan het project met de naam TodoListService `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d56b9-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d56b9-130">Rechtermuisknop te klikken op het project op--> **toevoegen** --> **Nieuw Item** --> Zoek naar 'OWIN'.</span><span class="sxs-lookup"><span data-stu-id="d56b9-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="d56b9-131">De OWIN-middleware roept de `Configuration(…)`-methode aan als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d56b9-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="d56b9-132">Wijzig de klassendeclaratie naar `public partial class Startup` -we hebben u al deel uit van deze klasse geïmplementeerd in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="d56b9-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="d56b9-133">In de `Configuration(…)` methode, een aanroep van ConfgureAuth(...) verificatie voor uw web-app instellen.</span><span class="sxs-lookup"><span data-stu-id="d56b9-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="d56b9-134">Open het bestand `App_Start\Startup.Auth.cs` en implementeren van de `ConfigureAuth(…)` methode, waarmee de Web-API wordt ingesteld om te accepteren van tokens van het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d56b9-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="d56b9-135">Nu kunt u `[Authorize]` kenmerken ter bescherming van uw domeincontrollers en de acties met OAuth 2.0-bearer-verificatie.</span><span class="sxs-lookup"><span data-stu-id="d56b9-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="d56b9-136">Opmaken de `Controllers\TodoListController.cs` klasse met een tag autoriseren.</span><span class="sxs-lookup"><span data-stu-id="d56b9-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="d56b9-137">Hierdoor wordt de gebruiker zich aanmelden voor de toegang tot deze pagina geforceerd.</span><span class="sxs-lookup"><span data-stu-id="d56b9-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="d56b9-138">Wanneer een geautoriseerde beller is roept een van de `TodoListController` API's, de actie moet mogelijk toegang tot informatie over de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="d56b9-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="d56b9-139">OWIN biedt toegang tot de claims binnen het bearer-token via de `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="d56b9-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="d56b9-140">Tot slot opent u de `web.config` bestand in de hoofdmap van het project TodoListService en voer de configuratiewaarden van uw in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="d56b9-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d56b9-141">Uw `ida:Audience` is de **toepassings-Id** van de app die u hebt ingevoerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="d56b9-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="d56b9-142">De client-app configureren</span><span class="sxs-lookup"><span data-stu-id="d56b9-142">Configure the client app</span></span>
<span data-ttu-id="d56b9-143">Voordat u de Todo List-Service in actie zien kunt, moet u de Client Todo-lijst configureren zodat het kan tokens uit het v2.0-eindpunt ophalen en naar de service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d56b9-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="d56b9-144">Open in het project TodoListClient `App.config` en voer de configuratiewaarden van uw in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="d56b9-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d56b9-145">Uw `ida:ClientId` toepassings-Id die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="d56b9-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="d56b9-146">Ten slotte wilt opschonen, bouwen en uitvoeren van elk project!</span><span class="sxs-lookup"><span data-stu-id="d56b9-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="d56b9-147">U hebt nu een .NET MVC Web-API die tokens van beide persoonlijke Microsoft-accounts en werk-of schoolaccounts accepteert.</span><span class="sxs-lookup"><span data-stu-id="d56b9-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="d56b9-148">Meld u aan bij de TodoListClient en roept u uw web-api taken toevoegen aan de takenlijst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d56b9-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="d56b9-149">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="d56b9-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="d56b9-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d56b9-150">Next steps</span></span>
<span data-ttu-id="d56b9-151">U kunt nu verplaatsen naar andere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="d56b9-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="d56b9-152">U wilt proberen:</span><span class="sxs-lookup"><span data-stu-id="d56b9-152">You may want to try:</span></span>

[<span data-ttu-id="d56b9-153">Een Web-API aanroept vanuit een Web-App >></span><span class="sxs-lookup"><span data-stu-id="d56b9-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="d56b9-154">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="d56b9-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="d56b9-155">De ontwikkelaarshandleiding v2.0 >></span><span class="sxs-lookup"><span data-stu-id="d56b9-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d56b9-156">StackOverflow 'azure active directory'-tag >></span><span class="sxs-lookup"><span data-stu-id="d56b9-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d56b9-157">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="d56b9-157">Get security updates for our products</span></span>
<span data-ttu-id="d56b9-158">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="d56b9-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
