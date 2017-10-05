---
title: Wijzigingen in een MVC-project, wanneer u verbinding met Azure AD maakt | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt met uw MVC-project wanneer u verbinding met Azure AD maakt met behulp van Visual Studio verbonden services
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="0cf3c-103">Wat is er gebeurd met mijn MVC-project (Visual Studio Azure Active Directory verbonden service)?</span><span class="sxs-lookup"><span data-stu-id="0cf3c-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cf3c-104">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="0cf3c-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="0cf3c-105">Wat is er gebeurd</span><span class="sxs-lookup"><span data-stu-id="0cf3c-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="0cf3c-106">Verwijzingen zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="0cf3c-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="0cf3c-107">NuGet-pakket met verwijzingen</span><span class="sxs-lookup"><span data-stu-id="0cf3c-107">NuGet package references</span></span>
* <span data-ttu-id="0cf3c-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0cf3c-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0cf3c-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0cf3c-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0cf3c-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0cf3c-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0cf3c-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-114">**Owin**</span></span>
* <span data-ttu-id="0cf3c-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="0cf3c-116">.NET-verwijzingen</span><span class="sxs-lookup"><span data-stu-id="0cf3c-116">.NET references</span></span>
* <span data-ttu-id="0cf3c-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0cf3c-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0cf3c-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0cf3c-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0cf3c-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0cf3c-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0cf3c-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-123">**Owin**</span></span>
* <span data-ttu-id="0cf3c-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="0cf3c-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="0cf3c-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="0cf3c-127">Code is toegevoegd</span><span class="sxs-lookup"><span data-stu-id="0cf3c-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="0cf3c-128">Codebestanden zijn toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="0cf3c-128">Code files were added to your project</span></span>
<span data-ttu-id="0cf3c-129">Een verificatie-Opstartklasse **App_Start/Startup.Auth.cs** is toegevoegd aan uw project met starten van de logica voor Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="0cf3c-130">Ook een controllerklasse, Controllers/AccountController.cs is toegevoegd die bevat **SignIn()** en **SignOut()** methoden.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="0cf3c-131">Ten slotte een gedeeltelijke weergave **Views/Shared/_LoginPartial.cshtml** is toegevoegd met de actiekoppeling van een voor aanmelding/SignOut.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="0cf3c-132">Starten van de code is toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="0cf3c-132">Startup code was added to your project</span></span>
<span data-ttu-id="0cf3c-133">Als u al een Opstartklasse in uw project de **configuratie** methode is bijgewerkt met een aanroep van **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="0cf3c-134">Anders wordt is een Opstartklasse toegevoegd aan uw project.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="0cf3c-135">Uw app.config of web.config heeft nieuwe configuratiewaarden</span><span class="sxs-lookup"><span data-stu-id="0cf3c-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="0cf3c-136">De volgende configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="0cf3c-137">Een Azure Active Directory (AD)-App is gemaakt</span><span class="sxs-lookup"><span data-stu-id="0cf3c-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="0cf3c-138">Een Azure AD-toepassing is gemaakt in de map die u hebt geselecteerd in de wizard.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0cf3c-139">Als ik gecontroleerd *afzonderlijke gebruikersaccounts verificatie uit te schakelen*, welke aanvullende wijzigingen zijn aangebracht aan mijn project?</span><span class="sxs-lookup"><span data-stu-id="0cf3c-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0cf3c-140">NuGet-pakket met verwijzingen zijn verwijderd en de bestanden zijn verwijderd en een back-up.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="0cf3c-141">Afhankelijk van de status van uw project, kunt u wellicht handmatig verwijderen van aanvullende verwijzingen of bestanden of code desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="0cf3c-142">NuGet-pakket verwijzingen verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="0cf3c-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="0cf3c-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="0cf3c-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="0cf3c-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="0cf3c-146">Codebestanden back-up gemaakt en verwijderd (voor die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="0cf3c-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="0cf3c-147">Elk van de volgende bestanden is een back-up en verwijderd uit het project.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="0cf3c-148">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap van de directory van het project.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0cf3c-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="0cf3c-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="0cf3c-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="0cf3c-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="0cf3c-153">Codebestanden back-up gemaakt (die aanwezig)</span><span class="sxs-lookup"><span data-stu-id="0cf3c-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="0cf3c-154">Elk van de volgende bestanden is een back-up maken voordat het wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="0cf3c-155">Back-upbestanden bevinden zich in een map 'Back-up' in de hoofdmap van de directory van het project.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0cf3c-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-156">**Startup.cs**</span></span>
* <span data-ttu-id="0cf3c-157">**App_Start\Startup.auth.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="0cf3c-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="0cf3c-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0cf3c-160">Als ik gecontroleerd *mapgegevens lezen*, welke aanvullende wijzigingen zijn aangebracht aan mijn project?</span><span class="sxs-lookup"><span data-stu-id="0cf3c-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0cf3c-161">Aanvullende verwijzingen zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="0cf3c-162">Aanvullende naslaginformatie voor NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="0cf3c-162">Additional NuGet package references</span></span>
* <span data-ttu-id="0cf3c-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-163">**EntityFramework**</span></span>
* <span data-ttu-id="0cf3c-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0cf3c-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0cf3c-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0cf3c-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0cf3c-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0cf3c-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="0cf3c-170">Aanvullende naslaginformatie voor .NET</span><span class="sxs-lookup"><span data-stu-id="0cf3c-170">Additional .NET references</span></span>
* <span data-ttu-id="0cf3c-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-171">**EntityFramework**</span></span>
* <span data-ttu-id="0cf3c-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="0cf3c-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0cf3c-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0cf3c-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0cf3c-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0cf3c-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0cf3c-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="0cf3c-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0cf3c-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="0cf3c-180">Aanvullende codebestanden zijn toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="0cf3c-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="0cf3c-181">Twee bestanden zijn toegevoegd ter ondersteuning van token opslaan in cache: **Models\ADALTokenCache.cs** en **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="0cf3c-182">Een extra domeincontroller en de weergave zijn toegevoegd ter illustratie van toegang tot gebruikersprofielgegevens met Azure graph API's.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="0cf3c-183">Deze bestanden zijn **Controllers\UserProfileController.cs** en **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="0cf3c-184">Aanvullende starten van de code is toegevoegd aan uw project</span><span class="sxs-lookup"><span data-stu-id="0cf3c-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="0cf3c-185">In de **startup.auth.cs** bestand, een nieuwe **OpenIdConnectAuthenticationNotifications** object is toegevoegd aan de **meldingen** lid is van de  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="0cf3c-186">Dit is het inschakelen van de OAuth-code ontvangen en het uitwisselen van een toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="0cf3c-187">Als u meer wijzigingen zijn aangebracht in uw app.config of web.config</span><span class="sxs-lookup"><span data-stu-id="0cf3c-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="0cf3c-188">De volgende aanvullende configuratie-items zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="0cf3c-189">De volgende configuratiesecties en de verbindingsreeks zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="0cf3c-190">Uw App in Azure Active Directory is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="0cf3c-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="0cf3c-191">Uw App in Azure Active Directory is bijgewerkt met de *mapgegevens lezen* machtigingen en de sleutel is gemaakt is die wordt gebruikt als de *ida: ClientSecret* in de  **Web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="0cf3c-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf3c-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cf3c-192">Next steps</span></span>
- [<span data-ttu-id="0cf3c-193">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cf3c-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

