---
title: Wanneer u verbinding maakt met tooAzure AD aaaChanges aangebracht tooa MVC-project | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt tooyour MVC-project wanneer u tooAzure AD verbinding maken met behulp van Visual Studio verbonden services
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Wat is er gebeurd toomy MVC-project (Visual Studio Azure Active Directory verbonden service)?
> [!div class="op_single_selector"]
> * [Aan de slag](vs-active-directory-dotnet-getting-started.md)
> * [Wat is er gebeurd](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Verwijzingen zijn toegevoegd
### <a name="nuget-package-references"></a>NuGet-pakket met verwijzingen
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>.NET-verwijzingen
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Code is toegevoegd
### <a name="code-files-were-added-tooyour-project"></a>Codebestanden zijn tooyour project toegevoegd
Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** tooyour project met starten van de logica voor Azure AD-verificatie is toegevoegd. Ook een controllerklasse, Controllers/AccountController.cs is toegevoegd die bevat **SignIn()** en **SignOut()** methoden. Ten slotte een gedeeltelijke weergave **Views/Shared/_LoginPartial.cshtml** is toegevoegd met de actiekoppeling van een voor aanmelding/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Starten van de code is tooyour project toegevoegd
Als u al een Opstartklasse in uw project, Hallo **configuratie** methode is een aanroep van bijgewerkte tooinclude te**ConfigureAuth(app)**. Een Opstartklasse is anders tooyour project toegevoegd.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Uw app.config of web.config heeft nieuwe configuratiewaarden
Hallo na configuratie-items zijn toegevoegd.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Een Azure Active Directory (AD)-App is gemaakt
Een Azure AD-toepassing is gemaakt in het Hallo-map die u hebt geselecteerd in de wizard Hallo.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht toomy project?
NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up. Afhankelijk van de status van de Hallo van uw project, mogelijk hebt u toomanually aanvullende verwijzingen of bestanden verwijderen of wijzigen van de code naar gelang van toepassing.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet-pakket verwijzingen verwijderd (voor die aanwezig)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)
Elk van de volgende bestanden is een back-up en verwijderd uit het Hallo-project. Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Codebestanden back-up gemaakt (die aanwezig)
Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen. Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.

* **Startup.cs**
* **App_Start\Startup.auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht toomy project?
Aanvullende verwijzingen zijn toegevoegd.

### <a name="additional-nuget-package-references"></a>Aanvullende naslaginformatie voor NuGet-pakket
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Aanvullende naslaginformatie voor .NET
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Aanvullende bestanden van de Code zijn tooyour project toegevoegd
Er zijn twee bestanden toegevoegd toosupport token opslaan in cache: **Models\ADALTokenCache.cs** en **Models\ApplicationDbContext.cs**.  Een extra domeincontroller en de weergave zijn tooillustrate toegang tot gebruikersprofielgegevens met Azure graph API's toegevoegd.  Deze bestanden zijn **Controllers\UserProfileController.cs** en **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Aanvullende opstartcode is tooyour project toegevoegd
In Hallo **startup.auth.cs** bestand, een nieuwe **OpenIdConnectAuthenticationNotifications** object werd toegevoegd toohello **meldingen** lid is van Hallo  **OpenIdConnectAuthenticationOptions**.  Dit is tooenable Hallo OAuth code ontvangen en het uitwisselen van een toegangstoken.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Als u meer wijzigingen zijn aangebracht tooyour app.config of web.config
Hallo zijn volgende aanvullende configuratie-items toegevoegd.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Hallo zijn volgende configuratiesecties en de verbindingsreeks toegevoegd.

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Uw App in Azure Active Directory is bijgewerkt
Uw App in Azure Active Directory is een bijgewerkte tooinclude hello *mapgegevens lezen* machtigingen en de sleutel is gemaakt dat vervolgens is gebruikt als Hallo *ida: ClientSecret* in Hallo  **Web.config** bestand.

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

