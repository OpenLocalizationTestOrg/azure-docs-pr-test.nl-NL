---
title: Azure Active Directory B2C | Microsoft Docs
description: Het bouwen van een webtoepassing met sign-up-to-date/aanmelden, profiel bewerken en wachtwoord opnieuw instellen met behulp van Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="74aa1-103">Een ASP.NET-web-app maken met Azure Active Directory B2C registreren, aanmelden, profiel bewerken en wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="74aa1-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="74aa1-104">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="74aa1-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74aa1-105">Azure AD B2C identiteit functies toevoegen aan uw web-app</span><span class="sxs-lookup"><span data-stu-id="74aa1-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="74aa1-106">Registreren van uw web-app in uw Azure AD B2C-directory</span><span class="sxs-lookup"><span data-stu-id="74aa1-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="74aa1-107">Maak een gebruiker sign-up-to-date/aanmelden, profiel bewerken, en beleid voor uw web-app-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="74aa1-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74aa1-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="74aa1-108">Prerequisites</span></span>

- <span data-ttu-id="74aa1-109">U moet uw B2C-Tenant verbinden met een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="74aa1-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="74aa1-110">U kunt een gratis Azure-account maken [hier](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="74aa1-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="74aa1-111">U moet [Microsoft Visual Studio](https://www.visualstudio.com/) of een vergelijkbaar programma weergeven en wijzigen van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="74aa1-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="74aa1-112">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="74aa1-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="74aa1-113">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="74aa1-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="74aa1-114">Een directory is een container voor alle gebruikers, apps en groepen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="74aa1-115">Als u niet een al hebt, maakt u een B2C-directory voordat u in deze handleiding doorgaat.</span><span class="sxs-lookup"><span data-stu-id="74aa1-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="74aa1-116">U moet verbinding maken met de B2C-Tenant van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="74aa1-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="74aa1-117">Na het selecteren van **maken**, selecteer de **koppeling een bestaande Azure AD B2C-Tenant met mijn Azure-abonnement** optie en klik vervolgens in de **Azure AD B2C-Tenant** vervolgkeuzelijst, selecteer de tenant die u wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="74aa1-118">Het maken en een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="74aa1-118">Create and register an application</span></span>

<span data-ttu-id="74aa1-119">Vervolgens moet u maken en registreren van de app in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="74aa1-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="74aa1-120">Dit bevat informatie die Azure AD B2C moet veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="74aa1-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="74aa1-121">Wanneer u klaar bent, hebt u zowel een API en een systeemeigen toepassing in de instellingen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="74aa1-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="74aa1-122">Beleid op uw B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="74aa1-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="74aa1-123">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="74aa1-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="74aa1-124">Dit codevoorbeeld bevat drie identiteitservaringen: **aanmelding & aanmelden**, **profiel bewerken**, en **wachtwoordherstel**.</span><span class="sxs-lookup"><span data-stu-id="74aa1-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="74aa1-125">U moet één beleidsregel maken voor elk type, zoals wordt beschreven in het [naslagartikel voor beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="74aa1-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="74aa1-126">Voor elk beleid moet u de weergave naamkenmerk of claim kunt selecteren en kopiëren van de naam van uw beleid voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="74aa1-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="74aa1-127">Id-providers toevoegen</span><span class="sxs-lookup"><span data-stu-id="74aa1-127">Add your identity providers</span></span>

<span data-ttu-id="74aa1-128">Selecteer in de instellingen voor **identiteitsproviders** en kiest u registratie van de gebruikersnaam of e-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="74aa1-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="74aa1-129">Maak een beleid voor aanmelden en aanmelden</span><span class="sxs-lookup"><span data-stu-id="74aa1-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="74aa1-130">Maken van een profiel te bewerken van beleid</span><span class="sxs-lookup"><span data-stu-id="74aa1-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="74aa1-131">Maak een beleid voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="74aa1-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="74aa1-132">Nadat u uw beleid hebt gemaakt, bent u klaar om uw app te bouwen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="74aa1-133">De voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="74aa1-133">Download the sample code</span></span>

<span data-ttu-id="74aa1-134">De code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="74aa1-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="74aa1-135">U kunt het voorbeeld klonen door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="74aa1-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="74aa1-136">Nadat u de voorbeeldcode hebt gedownload, opent u het SLN-bestand in Visual Studio om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="74aa1-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="74aa1-137">Het oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="74aa1-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="74aa1-138">`TaskWebApp`is de MVC-webtoepassing die de gebruiker werkt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="74aa1-139">`TaskService` is de web-API voor de back-end van de app waarin elke takenlijst van de gebruiker wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="74aa1-140">In dit artikel wordt alleen de `TaskWebApp`-toepassing beschreven.</span><span class="sxs-lookup"><span data-stu-id="74aa1-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="74aa1-141">Voor meer informatie over het bouwen van `TaskService` met behulp van Azure AD B2C, Zie [onze .NET web api-zelfstudie](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="74aa1-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="74aa1-142">Update-code voor het gebruik van uw tenant en -beleid</span><span class="sxs-lookup"><span data-stu-id="74aa1-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="74aa1-143">Ons voorbeeld is geconfigureerd voor gebruik van het beleid en de client-id van onze demo-tenant.</span><span class="sxs-lookup"><span data-stu-id="74aa1-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="74aa1-144">Als u wilt verbinden met uw eigen tenant, moet u openen `web.config` in de `TaskWebApp` project en vervang de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="74aa1-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="74aa1-145">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="74aa1-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="74aa1-146">`ida:ClientId` door de id van uw web-app-toepassing</span><span class="sxs-lookup"><span data-stu-id="74aa1-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="74aa1-147">`ida:ClientSecret` door de geheime sleutel voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="74aa1-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="74aa1-148">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="74aa1-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="74aa1-149">`ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid</span><span class="sxs-lookup"><span data-stu-id="74aa1-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="74aa1-150">`ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid</span><span class="sxs-lookup"><span data-stu-id="74aa1-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="74aa1-151">Start de app</span><span class="sxs-lookup"><span data-stu-id="74aa1-151">Launch the app</span></span>
<span data-ttu-id="74aa1-152">Start de app in Visual Studio uit.</span><span class="sxs-lookup"><span data-stu-id="74aa1-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="74aa1-153">Navigeer naar het tabblad takenlijst en noteert u de URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="74aa1-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="74aa1-154">Zich registreren voor de app met behulp van de naam van uw e-mailadres of de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74aa1-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="74aa1-155">Meld u af, en vervolgens opnieuw aan te melden en het profiel bewerken of het wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="74aa1-156">Meld u af en meld u aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74aa1-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="74aa1-157">Sociale IDPs toevoegen</span><span class="sxs-lookup"><span data-stu-id="74aa1-157">Add social IDPs</span></span>

<span data-ttu-id="74aa1-158">De app ondersteunt momenteel alleen de gebruiker zich kunnen registreren en aanmelden met behulp van **lokale accounts**; accounts opgeslagen in uw B2C-directory die gebruikmaken van een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="74aa1-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="74aa1-159">U kunt ondersteuning voor andere toevoegen met behulp van Azure AD B2C **identiteitsproviders** (IDPs) zonder uw code.</span><span class="sxs-lookup"><span data-stu-id="74aa1-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="74aa1-160">Volg de gedetailleerde instructies in deze artikelen wilt sociale IDPs toevoegen aan uw app, eerst.</span><span class="sxs-lookup"><span data-stu-id="74aa1-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="74aa1-161">Voor elke IDP die u wilt ondersteunen, moet u een toepassing registreren in dat systeem en het verkrijgen van een client-ID.</span><span class="sxs-lookup"><span data-stu-id="74aa1-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="74aa1-162">Facebook ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="74aa1-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="74aa1-163">Google ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="74aa1-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="74aa1-164">Amazon ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="74aa1-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="74aa1-165">LinkedIn instellen als een IDP</span><span class="sxs-lookup"><span data-stu-id="74aa1-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="74aa1-166">Nadat u de id-providers aan uw B2C-directory toevoegen, bewerk elk van de drie beleidsregels om op te nemen van de nieuwe IDPs, zoals beschreven de [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="74aa1-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="74aa1-167">Nadat u uw beleid opslaat, voer de app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="74aa1-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="74aa1-168">U ziet nu de nieuwe IDPs toegevoegd als aanmelden en aanmeldingsopties in elk van uw identiteit ervaringen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="74aa1-169">U kunt experimenteren met het beleid en bekijk het effect op uw voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="74aa1-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="74aa1-170">Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="74aa1-171">Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en OWIN met elkaar verbinden.</span><span class="sxs-lookup"><span data-stu-id="74aa1-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="74aa1-172">Voorbeeld code-overzicht</span><span class="sxs-lookup"><span data-stu-id="74aa1-172">Sample code walkthrough</span></span>
<span data-ttu-id="74aa1-173">De volgende secties ziet u hoe de voorbeeldcode van de toepassing is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="74aa1-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="74aa1-174">U kunt dit als richtlijn bij het ontwikkelen van toekomstige app.</span><span class="sxs-lookup"><span data-stu-id="74aa1-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="74aa1-175">Toevoegen van ondersteuning voor verificatie</span><span class="sxs-lookup"><span data-stu-id="74aa1-175">Add authentication support</span></span>

<span data-ttu-id="74aa1-176">U kunt nu uw app voor het gebruik van Azure AD B2C configureren.</span><span class="sxs-lookup"><span data-stu-id="74aa1-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="74aa1-177">Uw app communiceert met Azure AD B2C door te sturen verificatieaanvragen OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="74aa1-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="74aa1-178">De ervaring van de gebruiker die de app wil uitvoeren door te geven van het beleid wordt bepaald door de aanvragen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="74aa1-179">OWIN-bibliotheek van Microsoft kunt u deze aanvragen verzenden, het beleid uitvoeren, het beheren van gebruikerssessies en meer.</span><span class="sxs-lookup"><span data-stu-id="74aa1-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="74aa1-180">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="74aa1-180">Install OWIN</span></span>

<span data-ttu-id="74aa1-181">Om te beginnen, moet u de OWIN middleware NuGet pakketten toevoegen aan het project met behulp van de Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="74aa1-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="74aa1-182">Een OWIN-opstartklasse toevoegen</span><span class="sxs-lookup"><span data-stu-id="74aa1-182">Add an OWIN startup class</span></span>

<span data-ttu-id="74aa1-183">Voeg aan de API een OWIN-opstartklasse toe met de naam `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="74aa1-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="74aa1-184">Klik met de rechtermuisknop op het project, selecteer achtereenvolgens **Toevoegen** en **Nieuw item** en zoek naar OWIN.</span><span class="sxs-lookup"><span data-stu-id="74aa1-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="74aa1-185">De OWIN-middleware roept de `Configuration(…)`-methode aan als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="74aa1-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="74aa1-186">In ons voorbeeld hebben we de klasseverklaring gewijzigd in `public partial class Startup` en het andere deel van de klasse geïmplementeerd in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="74aa1-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="74aa1-187">In de `Configuration`-methode hebben we een aanroep toegevoegd aan `ConfigureAuth`, die is gedefinieerd in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="74aa1-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="74aa1-188">Na de wijzigingen ziet `Startup.cs` er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="74aa1-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="74aa1-189">De verificatiemiddleware configureren</span><span class="sxs-lookup"><span data-stu-id="74aa1-189">Configure the authentication middleware</span></span>

<span data-ttu-id="74aa1-190">Open het bestand `App_Start\Startup.Auth.cs` en implementeren van de `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="74aa1-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="74aa1-191">De parameters die u opgeeft in `OpenIdConnectAuthenticationOptions` fungeren als coördinaten voor uw app om te communiceren met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="74aa1-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="74aa1-192">Als u bepaalde parameters niet opgeeft, wordt de standaardwaarde gebruikt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="74aa1-193">Bijvoorbeeld: we niet opgeven de `ResponseType` in het voorbeeld zodat de standaardwaarde `code id_token` in elke uitgaande aanvraag aan Azure AD B2C wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="74aa1-194">U moet ook Cookieverificatie instellen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="74aa1-195">De middleware OpenID Connect maakt gebruik van cookies gebruikerssessies, onder andere onderhouden.</span><span class="sxs-lookup"><span data-stu-id="74aa1-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="74aa1-196">In `OpenIdConnectAuthenticationOptions` , definiëren we een set callback-functies voor specifieke meldingen die worden ontvangen door de middleware OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="74aa1-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="74aa1-197">Deze problemen zijn gedefinieerd met behulp van een `OpenIdConnectAuthenticationNotifications` object en opgeslagen in de `Notifications` variabele.</span><span class="sxs-lookup"><span data-stu-id="74aa1-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="74aa1-198">In ons voorbeeld definiëren we drie verschillende retouraanroepen, afhankelijk van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="74aa1-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="74aa1-199">Met behulp van verschillende beleidsregels</span><span class="sxs-lookup"><span data-stu-id="74aa1-199">Using different policies</span></span>

<span data-ttu-id="74aa1-200">De `RedirectToIdentityProvider` melding wordt geactiveerd wanneer een aanvraag wordt gedaan aan Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="74aa1-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="74aa1-201">In de functie voor retouraanroepen `OnRedirectToIdentityProvider`, we controleren in de uitgaande oproep als we wilt gebruiken een ander beleid.</span><span class="sxs-lookup"><span data-stu-id="74aa1-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="74aa1-202">Om te kunnen doen wachtwoordherstel of een profiel te bewerken, moet u gebruikmaken van het bijbehorende beleid, zoals het wachtwoord opnieuw instellen van beleid in plaats van het standaardbeleid voor "Registreren of aanmelden".</span><span class="sxs-lookup"><span data-stu-id="74aa1-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="74aa1-203">In ons voorbeeld wanneer een gebruiker wil het wachtwoord opnieuw instellen of het profiel bewerken toevoegen we het beleid dat we de voorkeur geeft aan in de context OWIN.</span><span class="sxs-lookup"><span data-stu-id="74aa1-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="74aa1-204">Dat kan worden gedaan door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="74aa1-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="74aa1-205">En u kunt de functie voor retouraanroepen implementeren `OnRedirectToIdentityProvider` door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="74aa1-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="74aa1-206">Afhandeling van autorisatiecodes</span><span class="sxs-lookup"><span data-stu-id="74aa1-206">Handling authorization codes</span></span>

<span data-ttu-id="74aa1-207">De `AuthorizationCodeReceived` melding wordt geactiveerd wanneer een autorisatiecode wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="74aa1-208">Het OpenID Connect middleware biedt geen ondersteuning voor uitwisselen codes voor toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="74aa1-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="74aa1-209">U kunt de code voor het token in een callback-functie handmatig uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="74aa1-210">Voor meer informatie, Zie de [documentatie](active-directory-b2c-devquickstarts-web-api-dotnet.md) waarin wordt uitgelegd hoe.</span><span class="sxs-lookup"><span data-stu-id="74aa1-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="74aa1-211">Foutafhandeling</span><span class="sxs-lookup"><span data-stu-id="74aa1-211">Handling errors</span></span>

<span data-ttu-id="74aa1-212">De `AuthenticationFailed` melding wordt geactiveerd wanneer de verificatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="74aa1-213">In de callback-methode kunt u de fouten verwerken als u wilt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="74aa1-214">U moet echter een controle voor de foutcode toevoegen `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="74aa1-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="74aa1-215">Tijdens het uitvoeren van het beleid 'Registreren of aanmelden', de gebruiker heeft de mogelijkheid om te selecteren een **wachtwoord vergeten?** koppeling.</span><span class="sxs-lookup"><span data-stu-id="74aa1-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="74aa1-216">In dit geval stuurt Azure AD B2C uw app die fout die aangeeft dat uw app moet worden gebruikt voor het aanbrengen van een aanvraag met het beleid voor wachtwoordherstel in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="74aa1-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="74aa1-217">Verificatieaanvragen verzenden naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="74aa1-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="74aa1-218">Uw app is nu geconfigureerd voor communicatie met Azure AD B2C met behulp van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="74aa1-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="74aa1-219">OWIN beheert de details van verificatieberichten, het valideren van tokens van Azure AD B2C en het onderhoud van de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="74aa1-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="74aa1-220">Alles wat u hoeft alleen nog stroom voor elke gebruiker te initiëren.</span><span class="sxs-lookup"><span data-stu-id="74aa1-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="74aa1-221">Wanneer een gebruiker selecteert **Sign up/aanmelden**, **profiel bewerken**, of **wachtwoord opnieuw instellen** in de web-app, de bijbehorende actie is aangeroepen `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="74aa1-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="74aa1-222">U kunt ook OWIN gebruiken voor het ondertekenen van de gebruiker uit de app.</span><span class="sxs-lookup"><span data-stu-id="74aa1-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="74aa1-223">In `Controllers\AccountController.cs` we hebben:</span><span class="sxs-lookup"><span data-stu-id="74aa1-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="74aa1-224">Naast het expliciet aanroepen van een beleid, kunt u een `[Authorize]` code in uw domeincontrollers die een beleid wordt uitgevoerd als de gebruiker niet aangemeld.</span><span class="sxs-lookup"><span data-stu-id="74aa1-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="74aa1-225">Open `Controllers\HomeController.cs` en voeg de `[Authorize]` tag met de claims-controller.</span><span class="sxs-lookup"><span data-stu-id="74aa1-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="74aa1-226">OWIN selecteert het laatste beleid geconfigureerd wanneer de `[Authorize]` tag is bereikt.</span><span class="sxs-lookup"><span data-stu-id="74aa1-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="74aa1-227">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="74aa1-227">Display user information</span></span>

<span data-ttu-id="74aa1-228">Als u gebruikers verifiëren met behulp van OpenID Connect, Azure AD B2C een token ID terug naar de app die bevat **claims**.</span><span class="sxs-lookup"><span data-stu-id="74aa1-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="74aa1-229">Dit zijn asserties over de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74aa1-229">These are assertions about the user.</span></span> <span data-ttu-id="74aa1-230">U kunt de claims kunt gebruiken voor het aanpassen van uw app.</span><span class="sxs-lookup"><span data-stu-id="74aa1-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="74aa1-231">Open het `Controllers\HomeController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="74aa1-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="74aa1-232">U hebt toegang tot gebruikersclaims in uw domeincontrollers via de `ClaimsPrincipal.Current` SPN-object.</span><span class="sxs-lookup"><span data-stu-id="74aa1-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="74aa1-233">U kunt een claim die uw toepassing op dezelfde manier krijgt openen.</span><span class="sxs-lookup"><span data-stu-id="74aa1-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="74aa1-234">Een lijst van alle claims de app ontvangt is beschikbaar voor u op de **Claims** pagina.</span><span class="sxs-lookup"><span data-stu-id="74aa1-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
