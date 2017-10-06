---
title: aaaChanges aangebracht tooa WebApi project wanneer u verbinding maakt met tooAzure AD | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt tooyour WebApi project wanneer u tooAzure AD verbinding maken met behulp van Visual Studio
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Wat is er gebeurd toomy WebApi-project (Visual Studio Azure Active Directory verbonden service)
> [!div class="op_single_selector"]
> * [Aan de slag](vs-active-directory-webapi-getting-started.md)
> * [Wat is er gebeurd](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Verwijzingen zijn toegevoegd
### <a name="nuget-package-references"></a>NuGet-pakket met verwijzingen
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>.NET-verwijzingen
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Codewijzigingen
### <a name="code-files-were-added-tooyour-project"></a>Codebestanden zijn tooyour project toegevoegd
Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** tooyour project met starten van de logica voor Azure AD-verificatie is toegevoegd.

### <a name="startup-code-was-added-tooyour-project"></a>Starten van de code is tooyour project toegevoegd
Als u al een Opstartklasse in uw project, Hallo **configuratie** methode is een aanroep van bijgewerkte tooinclude te`ConfigureAuth(app)`. Een Opstartklasse is anders tooyour project toegevoegd.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Uw app.config of web.config-bestand heeft de nieuwe configuratiewaarden.
Hallo na configuratie-items zijn toegevoegd.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Een Azure AD-App is gemaakt
Een Azure AD-toepassing is gemaakt in het Hallo-map die u hebt geselecteerd in de wizard Hallo.

[Meer informatie over Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht toomy project?
NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up. Afhankelijk van de status van de Hallo van uw project, mogelijk hebt u toomanually aanvullende verwijzingen of bestanden verwijderen of wijzigen van de code naar gelang van toepassing.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet-pakket verwijzingen verwijderd (voor die aanwezig)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)
Elk van de volgende bestanden is een back-up en verwijderd uit het Hallo-project. Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Codebestanden back-up gemaakt (die aanwezig)
Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen. Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht toomy project?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Als u meer wijzigingen zijn aangebracht tooyour app.config of web.config
Hallo zijn volgende aanvullende configuratie-items toegevoegd.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Uw App in Azure Active Directory is bijgewerkt
Uw App in Azure Active Directory is een bijgewerkte tooinclude hello *mapgegevens lezen* machtigingen en de sleutel is gemaakt dat vervolgens is gebruikt als Hallo *ida: wachtwoord* in Hallo `web.config` bestand.

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

