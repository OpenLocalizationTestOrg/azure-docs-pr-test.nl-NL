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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="bd807-103">Wat is er gebeurd toomy WebApi-project (Visual Studio Azure Active Directory verbonden service)</span><span class="sxs-lookup"><span data-stu-id="bd807-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd807-104">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="bd807-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="bd807-105">Wat is er gebeurd</span><span class="sxs-lookup"><span data-stu-id="bd807-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="bd807-106">Verwijzingen zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="bd807-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="bd807-107">NuGet-pakket met verwijzingen</span><span class="sxs-lookup"><span data-stu-id="bd807-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="bd807-108">.NET-verwijzingen</span><span class="sxs-lookup"><span data-stu-id="bd807-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="bd807-109">Codewijzigingen</span><span class="sxs-lookup"><span data-stu-id="bd807-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="bd807-110">Codebestanden zijn tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="bd807-110">Code files were added tooyour project</span></span>
<span data-ttu-id="bd807-111">Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** tooyour project met starten van de logica voor Azure AD-verificatie is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd807-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="bd807-112">Starten van de code is tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="bd807-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="bd807-113">Als u al een Opstartklasse in uw project, Hallo **configuratie** methode is een aanroep van bijgewerkte tooinclude te`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="bd807-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="bd807-114">Een Opstartklasse is anders tooyour project toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd807-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="bd807-115">Uw app.config of web.config-bestand heeft de nieuwe configuratiewaarden.</span><span class="sxs-lookup"><span data-stu-id="bd807-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="bd807-116">Hallo na configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd807-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="bd807-117">Een Azure AD-App is gemaakt</span><span class="sxs-lookup"><span data-stu-id="bd807-117">An Azure AD App was created</span></span>
<span data-ttu-id="bd807-118">Een Azure AD-toepassing is gemaakt in het Hallo-map die u hebt geselecteerd in de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd807-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="bd807-119">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd807-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="bd807-120">Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht toomy project?</span><span class="sxs-lookup"><span data-stu-id="bd807-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="bd807-121">NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up.</span><span class="sxs-lookup"><span data-stu-id="bd807-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="bd807-122">Afhankelijk van de status van de Hallo van uw project, mogelijk hebt u toomanually aanvullende verwijzingen of bestanden verwijderen of wijzigen van de code naar gelang van toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd807-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="bd807-123">NuGet-pakket verwijzingen verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="bd807-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="bd807-124">Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="bd807-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="bd807-125">Elk van de volgende bestanden is een back-up en verwijderd uit het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="bd807-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="bd807-126">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.</span><span class="sxs-lookup"><span data-stu-id="bd807-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="bd807-127">Codebestanden back-up gemaakt (die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="bd807-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="bd807-128">Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="bd807-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="bd807-129">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.</span><span class="sxs-lookup"><span data-stu-id="bd807-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="bd807-130">Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht toomy project?</span><span class="sxs-lookup"><span data-stu-id="bd807-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="bd807-131">Als u meer wijzigingen zijn aangebracht tooyour app.config of web.config</span><span class="sxs-lookup"><span data-stu-id="bd807-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="bd807-132">Hallo zijn volgende aanvullende configuratie-items toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd807-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="bd807-133">Uw App in Azure Active Directory is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="bd807-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="bd807-134">Uw App in Azure Active Directory is een bijgewerkte tooinclude hello *mapgegevens lezen* machtigingen en de sleutel is gemaakt dat vervolgens is gebruikt als Hallo *ida: wachtwoord* in Hallo `web.config` bestand.</span><span class="sxs-lookup"><span data-stu-id="bd807-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd807-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd807-135">Next steps</span></span>
- [<span data-ttu-id="bd807-136">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd807-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

