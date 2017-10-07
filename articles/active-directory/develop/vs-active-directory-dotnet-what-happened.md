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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="11551-103">Wat is er gebeurd toomy MVC-project (Visual Studio Azure Active Directory verbonden service)?</span><span class="sxs-lookup"><span data-stu-id="11551-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11551-104">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="11551-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="11551-105">Wat is er gebeurd</span><span class="sxs-lookup"><span data-stu-id="11551-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="11551-106">Verwijzingen zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="11551-107">NuGet-pakket met verwijzingen</span><span class="sxs-lookup"><span data-stu-id="11551-107">NuGet package references</span></span>
* <span data-ttu-id="11551-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="11551-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="11551-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="11551-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="11551-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="11551-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="11551-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="11551-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="11551-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="11551-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="11551-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="11551-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="11551-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="11551-114">**Owin**</span></span>
* <span data-ttu-id="11551-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="11551-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="11551-116">.NET-verwijzingen</span><span class="sxs-lookup"><span data-stu-id="11551-116">.NET references</span></span>
* <span data-ttu-id="11551-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="11551-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="11551-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="11551-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="11551-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="11551-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="11551-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="11551-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="11551-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="11551-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="11551-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="11551-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="11551-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="11551-123">**Owin**</span></span>
* <span data-ttu-id="11551-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="11551-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="11551-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="11551-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="11551-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="11551-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="11551-127">Code is toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="11551-128">Codebestanden zijn tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-128">Code files were added tooyour project</span></span>
<span data-ttu-id="11551-129">Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** tooyour project met starten van de logica voor Azure AD-verificatie is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="11551-130">Ook een controllerklasse, Controllers/AccountController.cs is toegevoegd die bevat **SignIn()** en **SignOut()** methoden.</span><span class="sxs-lookup"><span data-stu-id="11551-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="11551-131">Ten slotte een gedeeltelijke weergave **Views/Shared/_LoginPartial.cshtml** is toegevoegd met de actiekoppeling van een voor aanmelding/SignOut.</span><span class="sxs-lookup"><span data-stu-id="11551-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="11551-132">Starten van de code is tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="11551-133">Als u al een Opstartklasse in uw project, Hallo **configuratie** methode is een aanroep van bijgewerkte tooinclude te**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="11551-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="11551-134">Een Opstartklasse is anders tooyour project toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="11551-135">Uw app.config of web.config heeft nieuwe configuratiewaarden</span><span class="sxs-lookup"><span data-stu-id="11551-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="11551-136">Hallo na configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="11551-137">Een Azure Active Directory (AD)-App is gemaakt</span><span class="sxs-lookup"><span data-stu-id="11551-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="11551-138">Een Azure AD-toepassing is gemaakt in het Hallo-map die u hebt geselecteerd in de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="11551-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="11551-139">Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht toomy project?</span><span class="sxs-lookup"><span data-stu-id="11551-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="11551-140">NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up.</span><span class="sxs-lookup"><span data-stu-id="11551-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="11551-141">Afhankelijk van de status van de Hallo van uw project, mogelijk hebt u toomanually aanvullende verwijzingen of bestanden verwijderen of wijzigen van de code naar gelang van toepassing.</span><span class="sxs-lookup"><span data-stu-id="11551-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="11551-142">NuGet-pakket verwijzingen verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="11551-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="11551-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="11551-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="11551-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="11551-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="11551-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="11551-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="11551-146">Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="11551-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="11551-147">Elk van de volgende bestanden is een back-up en verwijderd uit het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="11551-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="11551-148">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.</span><span class="sxs-lookup"><span data-stu-id="11551-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="11551-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="11551-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="11551-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="11551-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="11551-153">Codebestanden back-up gemaakt (die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="11551-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="11551-154">Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="11551-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="11551-155">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap Hallo van Hallo projectmap.</span><span class="sxs-lookup"><span data-stu-id="11551-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="11551-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-156">**Startup.cs**</span></span>
* <span data-ttu-id="11551-157">**App_Start\Startup.auth.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="11551-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="11551-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="11551-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="11551-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="11551-160">Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht toomy project?</span><span class="sxs-lookup"><span data-stu-id="11551-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="11551-161">Aanvullende verwijzingen zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="11551-162">Aanvullende naslaginformatie voor NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="11551-162">Additional NuGet package references</span></span>
* <span data-ttu-id="11551-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="11551-163">**EntityFramework**</span></span>
* <span data-ttu-id="11551-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="11551-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="11551-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="11551-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="11551-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="11551-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="11551-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="11551-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="11551-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="11551-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="11551-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="11551-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="11551-170">Aanvullende naslaginformatie voor .NET</span><span class="sxs-lookup"><span data-stu-id="11551-170">Additional .NET references</span></span>
* <span data-ttu-id="11551-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="11551-171">**EntityFramework**</span></span>
* <span data-ttu-id="11551-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="11551-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="11551-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="11551-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="11551-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="11551-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="11551-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="11551-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="11551-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="11551-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="11551-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="11551-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="11551-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="11551-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="11551-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="11551-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="11551-180">Aanvullende bestanden van de Code zijn tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="11551-181">Er zijn twee bestanden toegevoegd toosupport token opslaan in cache: **Models\ADALTokenCache.cs** en **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="11551-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="11551-182">Een extra domeincontroller en de weergave zijn tooillustrate toegang tot gebruikersprofielgegevens met Azure graph API's toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="11551-183">Deze bestanden zijn **Controllers\UserProfileController.cs** en **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="11551-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="11551-184">Aanvullende opstartcode is tooyour project toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11551-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="11551-185">In Hallo **startup.auth.cs** bestand, een nieuwe **OpenIdConnectAuthenticationNotifications** object werd toegevoegd toohello **meldingen** lid is van Hallo  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="11551-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="11551-186">Dit is tooenable Hallo OAuth code ontvangen en het uitwisselen van een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="11551-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="11551-187">Als u meer wijzigingen zijn aangebracht tooyour app.config of web.config</span><span class="sxs-lookup"><span data-stu-id="11551-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="11551-188">Hallo zijn volgende aanvullende configuratie-items toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="11551-189">Hallo zijn volgende configuratiesecties en de verbindingsreeks toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11551-189">hello following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="11551-190">Uw App in Azure Active Directory is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="11551-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="11551-191">Uw App in Azure Active Directory is een bijgewerkte tooinclude hello *mapgegevens lezen* machtigingen en de sleutel is gemaakt dat vervolgens is gebruikt als Hallo *ida: ClientSecret* in Hallo  **Web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="11551-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11551-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11551-192">Next steps</span></span>
- [<span data-ttu-id="11551-193">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11551-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

