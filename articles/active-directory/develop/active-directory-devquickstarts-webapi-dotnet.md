---
title: aaaAzure AD .NET web-API aan de slag | Microsoft Docs
description: "Hoe toobuild een .NET MVC-web-API die kan worden geïntegreerd met Azure AD voor verificatie en autorisatie."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="f1c0e-103">Een web-API beveiligen met behulp van bearer-tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c0e-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f1c0e-104">Als u een toepassing die toegang tooprotected resources biedt maakt, moet u tooknow hoe tooprevent ongerechtvaardigd toegang krijgen tot bronnen toothose.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="f1c0e-105">Azure Active Directory (Azure AD) kunt u eenvoudig en eenvoudige toohelp een web-API beveiligen met behulp van OAuth 2.0-bearer-toegangstokens met alleen een paar regels code.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="f1c0e-106">In ASP.NET-web-apps, kunt u deze beveiliging uitvoeren met behulp van Microsoft-implementatie Hallo van Hallo community aangestuurde OWIN middleware opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="f1c0e-107">We gebruiken hier OWIN toobuild een 'tooDo lijst' web-API die:</span><span class="sxs-lookup"><span data-stu-id="f1c0e-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="f1c0e-108">Geeft aan dat de API's zijn beveiligd.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="f1c0e-109">Valideert dat Hallo web-API aanroepen een geldige toegangstoken bevatten.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="f1c0e-110">toobuild hello tooDo lijst API, moet u eerst:</span><span class="sxs-lookup"><span data-stu-id="f1c0e-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="f1c0e-111">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="f1c0e-112">Hallo app toouse hello OWIN-verificatiepijplijn instellen.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="f1c0e-113">Configureer een client toepassing toocall Hallo-web-API.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="f1c0e-114">tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f1c0e-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f1c0e-115">Elk is een Visual Studio 2013-oplossing.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="f1c0e-116">U moet ook een Azure AD-tenant in welke tooregister uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="f1c0e-117">Als u niet hebt, [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f1c0e-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="f1c0e-118">Stap 1: Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c0e-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="f1c0e-119">toohelp beveiligen uw toepassing, wordt u eerst een toepassing toocreate moet in uw tenant en Azure AD voorzien van enkele belangrijke informatie.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="f1c0e-120">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1c0e-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f1c0e-121">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-121">On hello top bar, click your account.</span></span> <span data-ttu-id="f1c0e-122">In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="f1c0e-123">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="f1c0e-124">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="f1c0e-125">Volg de aanwijzingen Hallo en maak een nieuwe **webtoepassing en/of Web-API**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="f1c0e-126">**Naam** beschrijft de toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="f1c0e-127">Voer **tooDo lijst Service**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="f1c0e-128">**Omleidings-Uri** is een combinatie schema en de tekenreeks die gebruikmaakt van Azure AD tooreturn een tokens dat uw app heeft aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="f1c0e-129">Voer `https://localhost:44321/` voor deze waarde.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="f1c0e-130">Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="f1c0e-131">Voer een tenantspecifieke-id.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="f1c0e-132">Geef bijvoorbeeld `https://contoso.onmicrosoft.com/TodoListService` op.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="f1c0e-133">Hallo-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-133">Save hello configuration.</span></span> <span data-ttu-id="f1c0e-134">Laat Hallo portal geopend, omdat u ook tooregister uw clienttoepassing binnenkort moet.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="f1c0e-135">Stap 2: Hallo app toouse hello OWIN-verificatiepijplijn instellen</span><span class="sxs-lookup"><span data-stu-id="f1c0e-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="f1c0e-136">toovalidate inkomende aanvragen en -tokens, moet u tooset van uw toepassing toocommunicate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="f1c0e-137">toobegin, open Hallo oplossing en voeg Hallo OWIN middleware NuGet-pakketten toohello TodoListService project met behulp van Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="f1c0e-138">Voeg een OWIN klasse toohello TodoListService opstartproject aangeroepen `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="f1c0e-139">Klik met de rechtermuisknop Hallo project, selecteer **toevoegen** > **Nieuw Item**, en zoek vervolgens naar **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="f1c0e-140">Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="f1c0e-141">Hallo klassendeclaratie ook wijzigen`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="f1c0e-142">We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="f1c0e-143">In Hallo `Configuration(…)` methode te maken van een aanroep van`ConfgureAuth(…)` tooset van verificatie voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="f1c0e-144">Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(…)` methode.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="f1c0e-145">parameters die u opgeeft in Hallo `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="f1c0e-146">Nu kunt u `[Authorize]` kenmerken toohelp bescherming van uw domeincontrollers en de acties met JSON Web Token (JWT) bearer-verificatie.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="f1c0e-147">Hallo opmaken `Controllers\TodoListController.cs` klasse met een tag autoriseren.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="f1c0e-148">Hierdoor moeten Hallo gebruiker toosign in voor de toegang tot deze pagina.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="f1c0e-149">Wanneer een geautoriseerde beller is roept een Hallo `TodoListController` API's, Hallo actie mogelijk moet toegang tot tooinformation over Hallo aanroeper.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="f1c0e-150">OWIN toegang toohello claims binnen Hallo bearer-token via Hallo levert `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="f1c0e-151">Een algemene vereiste voor web-API's is toovalidate Hallo 'scopes' Hallo token aanwezig.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="f1c0e-152">Dit zorgt ervoor dat die gebruiker Hallo heeft ingestemd toohello machtigingen vereist tooaccess hello tooDo List-Service.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="f1c0e-153">Open Hallo `web.config` bestand in de hoofdmap Hallo van Hallo TodoListService project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="f1c0e-154">`ida:Tenant`Hallo-naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="f1c0e-155">`ida:Audience`is Hallo App ID URI van Hallo-toepassing die u hebt ingevoerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="f1c0e-156">Stap 3: Een clienttoepassing configureren en uitvoeren van Hallo-service</span><span class="sxs-lookup"><span data-stu-id="f1c0e-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="f1c0e-157">Voordat u Hallo tooDo List-Service in actie zien kunt, moet u tooconfigure hello tooDo lijst client, zodat het kan tokens van Azure AD verkrijgen en aanroepen toohello service maken.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="f1c0e-158">Ga terug toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1c0e-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f1c0e-159">Maak een nieuwe toepassing in uw Azure AD-tenant en selecteer **systeemeigen clienttoepassing** Hallo resulterende gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="f1c0e-160">**Naam** beschrijft de toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="f1c0e-161">Voer `http://TodoListClient/` voor Hallo **omleidings-Uri** waarde.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="f1c0e-162">Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="f1c0e-163">U moet deze waarde in de volgende stappen hello, dus kopiëren van de pagina van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="f1c0e-164">Van Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="f1c0e-165">Zoek en selecteer Hallo tooDo List-Service, Hallo toevoegen **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="f1c0e-166">Open in Visual Studio `App.config` in Hallo TodoListClient project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="f1c0e-167">`ida:Tenant`Hallo-naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="f1c0e-168">`ida:ClientId`is Hallo app-ID die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="f1c0e-169">`todo:TodoListResourceId`Hallo App ID URI van Hallo tooDo List-Service-toepassing die u hebt ingevoerd in hello Azure-portal is.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1c0e-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1c0e-170">Next steps</span></span>
<span data-ttu-id="f1c0e-171">Ten slotte wilt opschonen, bouwen en uitvoeren van elk project.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="f1c0e-172">Als u nog niet gedaan hebt, is nu Hallo tijd toocreate een nieuwe gebruiker in uw tenant met een *. onmicrosoft.com-domein.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="f1c0e-173">Meld u bij toohello tooDo lijst client met die gebruiker en de takenlijst van sommige taken toohello gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="f1c0e-174">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f1c0e-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f1c0e-175">U kunt nu verplaatsen op toomore identity-scenario's.</span><span class="sxs-lookup"><span data-stu-id="f1c0e-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
