---
title: Wijzigingen die zijn aangebracht aan een project WebApi wanneer u verbinding met Azure AD maakt | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt met uw project WebApi wanneer u verbinding met Azure AD maakt met behulp van Visual Studio
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
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="09057-103">Wat is er gebeurd met mijn WebApi-project (Visual Studio Azure Active Directory verbonden service)</span><span class="sxs-lookup"><span data-stu-id="09057-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09057-104">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="09057-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="09057-105">Wat is er gebeurd</span><span class="sxs-lookup"><span data-stu-id="09057-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="09057-106">Verwijzingen zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="09057-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="09057-107">NuGet-pakket met verwijzingen</span><span class="sxs-lookup"><span data-stu-id="09057-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="09057-108">.NET-verwijzingen</span><span class="sxs-lookup"><span data-stu-id="09057-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="09057-109">Codewijzigingen</span><span class="sxs-lookup"><span data-stu-id="09057-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="09057-110">Codebestanden zijn toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="09057-110">Code files were added to your project</span></span>
<span data-ttu-id="09057-111">Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** is toegevoegd aan uw project met starten van de logica voor Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="09057-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="09057-112">Starten van de code is toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="09057-112">Startup code was added to your project</span></span>
<span data-ttu-id="09057-113">Als u al een Opstartklasse in uw project de **configuratie** methode is bijgewerkt met een aanroep van `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="09057-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="09057-114">Anders wordt is een Opstartklasse toegevoegd aan uw project.</span><span class="sxs-lookup"><span data-stu-id="09057-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="09057-115">Uw app.config of web.config-bestand heeft de nieuwe configuratiewaarden.</span><span class="sxs-lookup"><span data-stu-id="09057-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="09057-116">De volgende configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="09057-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="09057-117">Een Azure AD-App is gemaakt</span><span class="sxs-lookup"><span data-stu-id="09057-117">An Azure AD App was created</span></span>
<span data-ttu-id="09057-118">Een Azure AD-toepassing is gemaakt in de map die u hebt geselecteerd in de wizard.</span><span class="sxs-lookup"><span data-stu-id="09057-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="09057-119">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09057-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="09057-120">Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht aan mijn project?</span><span class="sxs-lookup"><span data-stu-id="09057-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="09057-121">NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up.</span><span class="sxs-lookup"><span data-stu-id="09057-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="09057-122">Afhankelijk van de status van uw project, kunt u wellicht handmatig verwijderen van aanvullende verwijzingen of bestanden of code desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="09057-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="09057-123">NuGet-pakket verwijzingen verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="09057-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="09057-124">Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="09057-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="09057-125">Elk van de volgende bestanden is een back-up en verwijderd uit het project.</span><span class="sxs-lookup"><span data-stu-id="09057-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="09057-126">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap van de directory van het project.</span><span class="sxs-lookup"><span data-stu-id="09057-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="09057-127">Codebestanden back-up gemaakt (die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="09057-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="09057-128">Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="09057-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="09057-129">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap van de directory van het project.</span><span class="sxs-lookup"><span data-stu-id="09057-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="09057-130">Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht aan mijn project?</span><span class="sxs-lookup"><span data-stu-id="09057-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="09057-131">Als u meer wijzigingen zijn aangebracht in uw app.config of web.config</span><span class="sxs-lookup"><span data-stu-id="09057-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="09057-132">De volgende aanvullende configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="09057-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="09057-133">Uw App in Azure Active Directory is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="09057-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="09057-134">Uw App in Azure Active Directory is bijgewerkt met de *mapgegevens lezen* machtigingen en de sleutel is gemaakt is die wordt gebruikt als de *ida: wachtwoord* in de `web.config` bestand.</span><span class="sxs-lookup"><span data-stu-id="09057-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09057-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09057-135">Next steps</span></span>
- [<span data-ttu-id="09057-136">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09057-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

