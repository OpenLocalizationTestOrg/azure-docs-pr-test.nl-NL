---
title: Azure AD .NET-web-API aan de slag | Microsoft Docs
description: "Het bouwen van een .NET MVC-web-API die kan worden geïntegreerd met Azure AD voor verificatie en autorisatie."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="2f564-103">Een web-API beveiligen met behulp van bearer-tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f564-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="2f564-104">Als u een toepassing die toegang tot beveiligde bronnen biedt maakt, moet u weten hoe om te voorkomen dat onrechtmatige toegang tot deze bronnen.</span><span class="sxs-lookup"><span data-stu-id="2f564-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="2f564-105">Azure Active Directory (Azure AD) maakt het eenvoudig en snel een web-API beveiligen met behulp van OAuth 2.0-bearer-toegang met alleen een paar regels code tokens.</span><span class="sxs-lookup"><span data-stu-id="2f564-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="2f564-106">In ASP.NET-web-apps, kunt u deze beveiliging uitvoeren met behulp van de Microsoft-implementatie van de community aangestuurde OWIN-middleware opgenomen in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="2f564-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="2f564-107">We gebruiken hier OWIN te maken van een 'Takenlijst' web-API die:</span><span class="sxs-lookup"><span data-stu-id="2f564-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="2f564-108">Geeft aan dat de API's zijn beveiligd.</span><span class="sxs-lookup"><span data-stu-id="2f564-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="2f564-109">Hiermee valideert u dat de web-API-aanroepen een ongeldig toegangstoken bevat.</span><span class="sxs-lookup"><span data-stu-id="2f564-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="2f564-110">Als u wilt de te doen lijst API maken, moet u eerst:</span><span class="sxs-lookup"><span data-stu-id="2f564-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="2f564-111">U registreert een toepassing met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f564-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="2f564-112">De app instellen voor de pijplijn OWIN-verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f564-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="2f564-113">Configureer een clienttoepassing naar de web-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2f564-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="2f564-114">Aan de slag [de basis van de app downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) of [het voltooide voorbeeld downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="2f564-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="2f564-115">Elk is een Visual Studio 2013-oplossing.</span><span class="sxs-lookup"><span data-stu-id="2f564-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="2f564-116">U moet ook een Azure AD-tenant waarin u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="2f564-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="2f564-117">Als u niet hebt, [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2f564-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="2f564-118">Stap 1: Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f564-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="2f564-119">Als u wilt beveiligen uw toepassing, moet u eerst een toepassing maakt in uw tenant en Azure AD voorzien van enkele belangrijke informatie.</span><span class="sxs-lookup"><span data-stu-id="2f564-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="2f564-120">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f564-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2f564-121">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="2f564-121">On the top bar, click your account.</span></span> <span data-ttu-id="2f564-122">In de **Directory** kiest u de Azure AD-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="2f564-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="2f564-123">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f564-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="2f564-124">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2f564-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="2f564-125">Volg de aanwijzingen en maak een nieuwe **webtoepassing en/of Web-API**.</span><span class="sxs-lookup"><span data-stu-id="2f564-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="2f564-126">**Naam** beschrijving van uw toepassing voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2f564-126">**Name** describes your application to users.</span></span> <span data-ttu-id="2f564-127">Voer **takenlijst Service**.</span><span class="sxs-lookup"><span data-stu-id="2f564-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="2f564-128">**Omleidings-Uri** is een combinatie schema en de tekenreeks die Azure AD gebruikt om tokens retourneert die door uw app heeft aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="2f564-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="2f564-129">Voer `https://localhost:44321/` voor deze waarde.</span><span class="sxs-lookup"><span data-stu-id="2f564-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="2f564-130">Van de **instellingen** -> **eigenschappen** pagina voor uw toepassing, het bijwerken van de App ID URI.</span><span class="sxs-lookup"><span data-stu-id="2f564-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="2f564-131">Voer een tenantspecifieke-id.</span><span class="sxs-lookup"><span data-stu-id="2f564-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="2f564-132">Geef bijvoorbeeld `https://contoso.onmicrosoft.com/TodoListService` op.</span><span class="sxs-lookup"><span data-stu-id="2f564-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="2f564-133">De configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="2f564-133">Save the configuration.</span></span> <span data-ttu-id="2f564-134">Laat de portal geopend, omdat u ook moet de clienttoepassing binnenkort registreren.</span><span class="sxs-lookup"><span data-stu-id="2f564-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="2f564-135">Stap 2: De app instellen voor de pijplijn OWIN-verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="2f564-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="2f564-136">Voor het valideren van binnenkomende aanvragen en tokens, moet u voor het instellen van uw toepassing om te communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f564-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="2f564-137">Om te beginnen, opent u de oplossing en de OWIN middleware NuGet-pakketten toevoegen aan het project TodoListService met behulp van de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="2f564-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="2f564-138">Een OWIN-Opstartklasse toevoegen aan het project met de naam TodoListService `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="2f564-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="2f564-139">Met de rechtermuisknop op het project, selecteert u **toevoegen** > **Nieuw Item**, en zoek vervolgens naar **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="2f564-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="2f564-140">De OWIN-middleware roept de `Configuration(…)`-methode aan als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2f564-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="2f564-141">Wijzig de klassendeclaratie naar `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="2f564-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="2f564-142">We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="2f564-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="2f564-143">In de `Configuration(…)` een aanroep van methode `ConfgureAuth(…)` verificatie voor uw web-app instellen.</span><span class="sxs-lookup"><span data-stu-id="2f564-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="2f564-144">Open het bestand `App_Start\Startup.Auth.cs` en implementeren van de `ConfigureAuth(…)` methode.</span><span class="sxs-lookup"><span data-stu-id="2f564-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="2f564-145">De parameters die u opgeeft in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungeert als coördinaten voor uw app om te communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f564-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="2f564-146">Nu kunt u `[Authorize]` kenmerken om uw domeincontrollers en de acties met JSON Web Token (JWT) bearer-verificatie te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="2f564-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="2f564-147">Opmaken de `Controllers\TodoListController.cs` klasse met een tag autoriseren.</span><span class="sxs-lookup"><span data-stu-id="2f564-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="2f564-148">Hierdoor wordt de gebruiker zich aanmelden voor de toegang tot deze pagina geforceerd.</span><span class="sxs-lookup"><span data-stu-id="2f564-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="2f564-149">Wanneer een geautoriseerde beller is roept een van de `TodoListController` API's, de actie moet mogelijk toegang tot informatie over de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="2f564-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="2f564-150">OWIN biedt toegang tot de claims binnen het bearer-token via de `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="2f564-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="2f564-151">Een algemene vereiste voor web-API's is het valideren van de in het token aanwezige 'scopes'.</span><span class="sxs-lookup"><span data-stu-id="2f564-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="2f564-152">Dit zorgt ervoor dat de gebruiker heeft ingestemd met de vereiste machtigingen voor toegang tot de te doen lijst Service.</span><span class="sxs-lookup"><span data-stu-id="2f564-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="2f564-153">Open de `web.config` bestand in de hoofdmap van het project TodoListService en voer de configuratiewaarden van uw in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="2f564-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="2f564-154">`ida:Tenant`is de naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="2f564-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="2f564-155">`ida:Audience`is de URI van de App-ID van de toepassing die u hebt ingevoerd in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2f564-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="2f564-156">Stap 3: Een clienttoepassing configureren en uitvoeren van de service</span><span class="sxs-lookup"><span data-stu-id="2f564-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="2f564-157">Voordat u de te doen List-Service in actie zien kunt, moet u de client To Do List configureren zodat het kan tokens van Azure AD verkrijgen en naar de service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2f564-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="2f564-158">Ga terug naar de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f564-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2f564-159">Maak een nieuwe toepassing in uw Azure AD-tenant en selecteer **systeemeigen clienttoepassing** in de resulterende prompt.</span><span class="sxs-lookup"><span data-stu-id="2f564-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="2f564-160">**Naam** beschrijving van uw toepassing voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2f564-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="2f564-161">Voer `http://TodoListClient/` voor de **omleidings-Uri** waarde.</span><span class="sxs-lookup"><span data-stu-id="2f564-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="2f564-162">Nadat u de registratie, wijst Azure AD een unieke toepassings-ID toe aan uw app.</span><span class="sxs-lookup"><span data-stu-id="2f564-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="2f564-163">U moet deze waarde in de volgende stappen, dus kopiëren van de toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="2f564-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="2f564-164">Van de **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2f564-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="2f564-165">Zoek en selecteer de te doen lijst Service, toevoegen de **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="2f564-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="2f564-166">Open in Visual Studio `App.config` in de TodoListClient project en voer vervolgens de configuratiewaarden van uw in de `<appSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="2f564-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="2f564-167">`ida:Tenant`is de naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="2f564-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="2f564-168">`ida:ClientId`is de app-ID die u hebt gekopieerd uit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2f564-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="2f564-169">`todo:TodoListResourceId`is de URI van de App-ID van de toepassing om te doen List-Service die u hebt ingevoerd in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f564-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f564-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f564-170">Next steps</span></span>
<span data-ttu-id="2f564-171">Ten slotte wilt opschonen, bouwen en uitvoeren van elk project.</span><span class="sxs-lookup"><span data-stu-id="2f564-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="2f564-172">Als u nog niet gedaan hebt, is nu tijd om aan te maken van een nieuwe gebruiker in de tenant met een *. onmicrosoft.com-domein.</span><span class="sxs-lookup"><span data-stu-id="2f564-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="2f564-173">Aanmelden bij de client To Do List bij die gebruiker en een aantal taken toevoegen aan de takenlijst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2f564-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="2f564-174">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="2f564-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="2f564-175">U kunt nu verder met meer identity-scenario's.</span><span class="sxs-lookup"><span data-stu-id="2f564-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
