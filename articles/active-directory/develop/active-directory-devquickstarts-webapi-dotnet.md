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
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Een web-API beveiligen met behulp van bearer-tokens van Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Als u een toepassing die toegang tooprotected resources biedt maakt, moet u tooknow hoe tooprevent ongerechtvaardigd toegang krijgen tot bronnen toothose.
Azure Active Directory (Azure AD) kunt u eenvoudig en eenvoudige toohelp een web-API beveiligen met behulp van OAuth 2.0-bearer-toegangstokens met alleen een paar regels code.

In ASP.NET-web-apps, kunt u deze beveiliging uitvoeren met behulp van Microsoft-implementatie Hallo van Hallo community aangestuurde OWIN middleware opgenomen in .NET Framework 4.5. We gebruiken hier OWIN toobuild een 'tooDo lijst' web-API die:

* Geeft aan dat de API's zijn beveiligd.
* Valideert dat Hallo web-API aanroepen een geldige toegangstoken bevatten.

toobuild hello tooDo lijst API, moet u eerst:

1. U registreert een toepassing met Azure AD.
2. Hallo app toouse hello OWIN-verificatiepijplijn instellen.
3. Configureer een client toepassing toocall Hallo-web-API.

tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Elk is een Visual Studio 2013-oplossing. U moet ook een Azure AD-tenant in welke tooregister uw toepassing. Als u niet hebt, [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Stap 1: Een toepassing registreren met Azure AD
toohelp beveiligen uw toepassing, wordt u eerst een toepassing toocreate moet in uw tenant en Azure AD voorzien van enkele belangrijke informatie.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Klik op de bovenste balk hello, uw account. In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.

3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.

4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.

5. Volg de aanwijzingen Hallo en maak een nieuwe **webtoepassing en/of Web-API**.
  * **Naam** beschrijft de toousers van uw toepassing. Voer **tooDo lijst Service**.
  * **Omleidings-Uri** is een combinatie schema en de tekenreeks die gebruikmaakt van Azure AD tooreturn een tokens dat uw app heeft aangevraagd. Voer `https://localhost:44321/` voor deze waarde.

6. Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken. Voer een tenantspecifieke-id. Geef bijvoorbeeld `https://contoso.onmicrosoft.com/TodoListService` op.

7. Hallo-configuratie op te slaan. Laat Hallo portal geopend, omdat u ook tooregister uw clienttoepassing binnenkort moet.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Stap 2: Hallo app toouse hello OWIN-verificatiepijplijn instellen
toovalidate inkomende aanvragen en -tokens, moet u tooset van uw toepassing toocommunicate met Azure AD.

1. toobegin, open Hallo oplossing en voeg Hallo OWIN middleware NuGet-pakketten toohello TodoListService project met behulp van Hallo Package Manager-Console.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Voeg een OWIN klasse toohello TodoListService opstartproject aangeroepen `Startup.cs`.  Klik met de rechtermuisknop Hallo project, selecteer **toevoegen** > **Nieuw Item**, en zoek vervolgens naar **OWIN**. Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.

3. Hallo klassendeclaratie ook wijzigen`public partial class Startup`. We hebben al deel uit van deze klasse geïmplementeerd voor u in een ander bestand. In Hallo `Configuration(…)` methode te maken van een aanroep van`ConfgureAuth(…)` tooset van verificatie voor uw web-app.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(…)` methode. parameters die u opgeeft in Hallo `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungeert als coördinaten voor de toocommunicate van uw app met Azure AD.

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

5. Nu kunt u `[Authorize]` kenmerken toohelp bescherming van uw domeincontrollers en de acties met JSON Web Token (JWT) bearer-verificatie. Hallo opmaken `Controllers\TodoListController.cs` klasse met een tag autoriseren. Hierdoor moeten Hallo gebruiker toosign in voor de toegang tot deze pagina.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Wanneer een geautoriseerde beller is roept een Hallo `TodoListController` API's, Hallo actie mogelijk moet toegang tot tooinformation over Hallo aanroeper. OWIN toegang toohello claims binnen Hallo bearer-token via Hallo levert `ClaimsPrincpal` object.  

6. Een algemene vereiste voor web-API's is toovalidate Hallo 'scopes' Hallo token aanwezig. Dit zorgt ervoor dat die gebruiker Hallo heeft ingestemd toohello machtigingen vereist tooaccess hello tooDo List-Service.

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

7. Open Hallo `web.config` bestand in de hoofdmap Hallo van Hallo TodoListService project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.
  * `ida:Tenant`Hallo-naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.
  * `ida:Audience`is Hallo App ID URI van Hallo-toepassing die u hebt ingevoerd in hello Azure-portal.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Stap 3: Een clienttoepassing configureren en uitvoeren van Hallo-service
Voordat u Hallo tooDo List-Service in actie zien kunt, moet u tooconfigure hello tooDo lijst client, zodat het kan tokens van Azure AD verkrijgen en aanroepen toohello service maken.

1. Ga terug toohello [Azure-portal](https://portal.azure.com).

2. Maak een nieuwe toepassing in uw Azure AD-tenant en selecteer **systeemeigen clienttoepassing** Hallo resulterende gevraagd.
  * **Naam** beschrijft de toousers van uw toepassing.
  * Voer `http://TodoListClient/` voor Hallo **omleidings-Uri** waarde.

3. Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe. U moet deze waarde in de volgende stappen hello, dus kopiëren van de pagina van de toepassing hello.

4. Van Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**. Zoek en selecteer Hallo tooDo List-Service, Hallo toevoegen **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik vervolgens op **gedaan**.

5. Open in Visual Studio `App.config` in Hallo TodoListClient project en voer uw configuratiewaarden in Hallo `<appSettings>` sectie.

  * `ida:Tenant`Hallo-naam van uw Azure AD-tenant bijvoorbeeld: contoso.onmicrosoft.com is.
  * `ida:ClientId`is Hallo app-ID die u hebt gekopieerd uit hello Azure-portal.
  * `todo:TodoListResourceId`Hallo App ID URI van Hallo tooDo List-Service-toepassing die u hebt ingevoerd in hello Azure-portal is.

## <a name="next-steps"></a>Volgende stappen
Ten slotte wilt opschonen, bouwen en uitvoeren van elk project. Als u nog niet gedaan hebt, is nu Hallo tijd toocreate een nieuwe gebruiker in uw tenant met een *. onmicrosoft.com-domein. Meld u bij toohello tooDo lijst client met die gebruiker en de takenlijst van sommige taken toohello gebruiker toevoegen.

Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). U kunt nu verplaatsen op toomore identity-scenario's.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
