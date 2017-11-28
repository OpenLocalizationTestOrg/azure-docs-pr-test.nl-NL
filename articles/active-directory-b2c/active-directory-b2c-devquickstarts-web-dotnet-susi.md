---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een webtoepassing met sign-up-to-date/aanmelden, bewerken en wachtwoord opnieuw instellen met behulp van Azure Active Directory B2C profiel.
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
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="8e35b-103">Een ASP.NET-web-app maken met Azure Active Directory B2C registreren, aanmelden, profiel bewerken en wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="8e35b-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="8e35b-104">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="8e35b-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e35b-105">Azure AD B2C identiteit functies tooyour web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e35b-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="8e35b-106">Registreren van uw web-app in uw Azure AD B2C-directory</span><span class="sxs-lookup"><span data-stu-id="8e35b-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="8e35b-107">Maak een gebruiker sign-up-to-date/aanmelden, profiel bewerken, en beleid voor uw web-app-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="8e35b-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e35b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8e35b-108">Prerequisites</span></span>

- <span data-ttu-id="8e35b-109">U moet uw B2C-Tenant tooan Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8e35b-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="8e35b-110">U kunt een gratis Azure-account maken [hier](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="8e35b-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="8e35b-111">U moet [Microsoft Visual Studio](https://www.visualstudio.com/) of een vergelijkbare tooview programma en voorbeeldcode Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="8e35b-112">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="8e35b-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="8e35b-113">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="8e35b-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="8e35b-114">Een directory is een container voor alle gebruikers, apps en groepen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="8e35b-115">Als u niet een al hebt, maakt u een B2C-directory voordat u in deze handleiding doorgaat.</span><span class="sxs-lookup"><span data-stu-id="8e35b-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="8e35b-116">U moet tooconnect Hallo B2C-Tenant tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e35b-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="8e35b-117">Na het selecteren van **maken**, selecteer Hallo **koppeling een bestaande Azure AD B2C-Tenant toomy Azure-abonnement** optie en klik vervolgens in Hallo **Azure AD B2C-Tenant** vervolgkeuzelijst, selecteer Hallo tenant gewenste tooassociate.</span><span class="sxs-lookup"><span data-stu-id="8e35b-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="8e35b-118">Het maken en een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="8e35b-118">Create and register an application</span></span>

<span data-ttu-id="8e35b-119">Vervolgens moet toocreate en Hallo app registreren in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="8e35b-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="8e35b-120">Hierdoor krijgt u informatie dat Azure AD B2C toosecurely moet communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="8e35b-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="8e35b-121">Wanneer u klaar bent, hebt u zowel een API en een systeemeigen toepassing in de instellingen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e35b-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="8e35b-122">Beleid op uw B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="8e35b-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="8e35b-123">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8e35b-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8e35b-124">Dit codevoorbeeld bevat drie identiteitservaringen: **aanmelding & aanmelden**, **profiel bewerken**, en **wachtwoordherstel**.</span><span class="sxs-lookup"><span data-stu-id="8e35b-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="8e35b-125">U moet toocreate één beleid voor elk type, zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8e35b-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8e35b-126">Voor elk beleid worden ervoor tooselect Hallo weergave naamkenmerk of claim en toocopy omlaag Hallo-naam van uw beleid voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="8e35b-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="8e35b-127">Id-providers toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e35b-127">Add your identity providers</span></span>

<span data-ttu-id="8e35b-128">Selecteer in de instellingen voor **identiteitsproviders** en kiest u registratie van de gebruikersnaam of e-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8e35b-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="8e35b-129">Maak een beleid voor aanmelden en aanmelden</span><span class="sxs-lookup"><span data-stu-id="8e35b-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="8e35b-130">Maken van een profiel te bewerken van beleid</span><span class="sxs-lookup"><span data-stu-id="8e35b-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="8e35b-131">Maak een beleid voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="8e35b-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="8e35b-132">Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="8e35b-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="8e35b-133">Hallo voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="8e35b-133">Download hello sample code</span></span>

<span data-ttu-id="8e35b-134">Hallo-code voor deze zelfstudie wordt bewaard in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="8e35b-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="8e35b-135">U kunt Hallo voorbeeld klonen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="8e35b-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="8e35b-136">Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart.</span><span class="sxs-lookup"><span data-stu-id="8e35b-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="8e35b-137">Hallo oplossingsbestand bevat twee projecten: `TaskWebApp` en `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="8e35b-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="8e35b-138">`TaskWebApp`is Hallo MVC-webtoepassing die gebruiker Hallo communiceert met.</span><span class="sxs-lookup"><span data-stu-id="8e35b-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="8e35b-139">`TaskService`Hallo-app back-end-web-API waarmee de takenlijst van elke gebruiker opgeslagen is.</span><span class="sxs-lookup"><span data-stu-id="8e35b-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="8e35b-140">In dit artikel wordt alleen besproken Hallo `TaskWebApp` toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e35b-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="8e35b-141">toolearn hoe toobuild `TaskService` met behulp van Azure AD B2C, Zie [onze .NET web api-zelfstudie](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8e35b-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="8e35b-142">Bijwerken van code toouse uw tenant en -beleid</span><span class="sxs-lookup"><span data-stu-id="8e35b-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="8e35b-143">Ons voorbeeld is de geconfigureerde toouse Hallo beleid en de client-ID van onze demo-tenant.</span><span class="sxs-lookup"><span data-stu-id="8e35b-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="8e35b-144">tooconnect het eigen tooyour-tenant, moet u tooopen `web.config` in Hallo `TaskWebApp` project en vervang Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="8e35b-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="8e35b-145">`ida:Tenant` door de naam van uw tenant</span><span class="sxs-lookup"><span data-stu-id="8e35b-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="8e35b-146">`ida:ClientId` door de id van uw web-app-toepassing</span><span class="sxs-lookup"><span data-stu-id="8e35b-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="8e35b-147">`ida:ClientSecret` door de geheime sleutel voor uw web-app</span><span class="sxs-lookup"><span data-stu-id="8e35b-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="8e35b-148">`ida:SignUpSignInPolicyId` door de naam van uw 'Aanmelden/registreren'-beleid</span><span class="sxs-lookup"><span data-stu-id="8e35b-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="8e35b-149">`ida:EditProfilePolicyId` door de naam van uw 'Profiel bewerken'-beleid</span><span class="sxs-lookup"><span data-stu-id="8e35b-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="8e35b-150">`ida:ResetPasswordPolicyId` door de naam van uw 'Wachtwoord opnieuw instellen'-beleid</span><span class="sxs-lookup"><span data-stu-id="8e35b-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="8e35b-151">Hallo-app starten</span><span class="sxs-lookup"><span data-stu-id="8e35b-151">Launch hello app</span></span>
<span data-ttu-id="8e35b-152">Start vanaf Hallo-app in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e35b-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="8e35b-153">Navigeer toohello takenlijst tabblad en de opmerking Hallo-URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="8e35b-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="8e35b-154">Zich registreren voor Hallo-app met behulp van de naam van uw e-mailadres of de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8e35b-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="8e35b-155">Afmelden, en vervolgens opnieuw aan te melden en Hallo profiel bewerken of Hallo wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="8e35b-156">Meld u af en meld u aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8e35b-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="8e35b-157">Sociale IDPs toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e35b-157">Add social IDPs</span></span>

<span data-ttu-id="8e35b-158">Hallo app ondersteunt momenteel alleen de gebruiker zich kunnen registreren en aanmelden met behulp van **lokale accounts**; accounts opgeslagen in uw B2C-directory die gebruikmaken van een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8e35b-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="8e35b-159">U kunt ondersteuning voor andere toevoegen met behulp van Azure AD B2C **identiteitsproviders** (IDPs) zonder uw code.</span><span class="sxs-lookup"><span data-stu-id="8e35b-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="8e35b-160">tooadd sociale IDPs tooyour app volg eerst Hallo gedetailleerde instructies in deze artikelen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="8e35b-161">Voor elke IDP gewenste toosupport, u moet een toepassing tooregister in dat systeem en verkrijgen van een client-ID.</span><span class="sxs-lookup"><span data-stu-id="8e35b-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="8e35b-162">Facebook ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="8e35b-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="8e35b-163">Google ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="8e35b-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="8e35b-164">Amazon ingesteld als een IDP</span><span class="sxs-lookup"><span data-stu-id="8e35b-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="8e35b-165">LinkedIn instellen als een IDP</span><span class="sxs-lookup"><span data-stu-id="8e35b-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="8e35b-166">Nadat u hebt toegevoegd Hallo identiteit providers tooyour B2C-directory, bewerken van uw drie beleidsregels tooinclude nieuwe IDPs Hallo zoals beschreven in Hallo [naslagartikel](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8e35b-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8e35b-167">Nadat u uw beleid opslaat, Voer u Hallo app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8e35b-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="8e35b-168">U ziet Hallo die nieuwe IDPs als opties voor aanmelden en registreren in elk van uw identiteitservaringen toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8e35b-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="8e35b-169">U kunt experimenteren met het beleid en observeren Hallo effect op uw voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="8e35b-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="8e35b-170">Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="8e35b-171">Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en OWIN met elkaar verbinden.</span><span class="sxs-lookup"><span data-stu-id="8e35b-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="8e35b-172">Voorbeeld code-overzicht</span><span class="sxs-lookup"><span data-stu-id="8e35b-172">Sample code walkthrough</span></span>
<span data-ttu-id="8e35b-173">Hallo volgende secties ziet u hoe de voorbeeldcode toepassing hello is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8e35b-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="8e35b-174">U kunt dit als richtlijn bij het ontwikkelen van toekomstige app.</span><span class="sxs-lookup"><span data-stu-id="8e35b-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="8e35b-175">Toevoegen van ondersteuning voor verificatie</span><span class="sxs-lookup"><span data-stu-id="8e35b-175">Add authentication support</span></span>

<span data-ttu-id="8e35b-176">U kunt nu uw app toouse Azure AD B2C configureren.</span><span class="sxs-lookup"><span data-stu-id="8e35b-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="8e35b-177">Uw app communiceert met Azure AD B2C door te sturen verificatieaanvragen OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8e35b-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="8e35b-178">Hallo aanvragen dicteren Hallo gebruikerservaring uw app wil tooexecute door te geven Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="8e35b-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="8e35b-179">U kunt gebruiken van Microsoft OWIN-bibliotheek toosend deze aanvragen, beleid uitvoeren, beheren van gebruikerssessies en meer.</span><span class="sxs-lookup"><span data-stu-id="8e35b-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="8e35b-180">OWIN installeren</span><span class="sxs-lookup"><span data-stu-id="8e35b-180">Install OWIN</span></span>

<span data-ttu-id="8e35b-181">toobegin, Hallo OWIN middleware NuGet-pakketten toohello project toevoegen met behulp van Hallo Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="8e35b-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="8e35b-182">Een OWIN-opstartklasse toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e35b-182">Add an OWIN startup class</span></span>

<span data-ttu-id="8e35b-183">Voeg een OWIN starten van de klasse toohello API aangeroepen `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="8e35b-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="8e35b-184">Met de rechtermuisknop op het Hallo-project, selecteer **toevoegen** en **Nieuw Item**, en zoek naar OWIN.</span><span class="sxs-lookup"><span data-stu-id="8e35b-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="8e35b-185">Hallo OWIN middleware Hallo worden ingeroepen `Configuration(…)` methode als uw app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8e35b-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="8e35b-186">In ons voorbeeld wijzigen we Hallo klassendeclaratie te`public partial class Startup` en geïmplementeerd met andere onderdelen van de klasse in Hallo Hallo `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="8e35b-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="8e35b-187">Hallo binnen `Configuration` methode, hebben we een gesprek te toegevoegd`ConfigureAuth`, die is gedefinieerd in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="8e35b-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="8e35b-188">Na het Hallo-wijzigingen `Startup.cs` Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="8e35b-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="8e35b-189">Hallo verificatiemiddleware configureren</span><span class="sxs-lookup"><span data-stu-id="8e35b-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="8e35b-190">Open Hallo bestand `App_Start\Startup.Auth.cs` en implementeren van Hallo `ConfigureAuth(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="8e35b-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="8e35b-191">parameters die u opgeeft in Hallo `OpenIdConnectAuthenticationOptions` fungeren als coördinaten voor de toocommunicate van uw app met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8e35b-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="8e35b-192">Als u bepaalde parameters niet opgeeft, wordt de standaardwaarde Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e35b-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="8e35b-193">Bijvoorbeeld: we geen Hallo opgeeft `ResponseType` in voorbeeld Hallo Hallo dus standaardwaarde `code id_token` in elke uitgaande aanvraag tooAzure AD B2C wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e35b-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="8e35b-194">U moet ook tooset van Cookieverificatie.</span><span class="sxs-lookup"><span data-stu-id="8e35b-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="8e35b-195">Hallo OpenID Connect middleware maakt gebruik van cookies toomaintain gebruikerssessies, onder andere.</span><span class="sxs-lookup"><span data-stu-id="8e35b-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="8e35b-196">In `OpenIdConnectAuthenticationOptions` , definiëren we een set callback-functies voor specifieke meldingen die worden ontvangen door Hallo OpenID Connect middleware.</span><span class="sxs-lookup"><span data-stu-id="8e35b-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="8e35b-197">Deze problemen zijn gedefinieerd met behulp van een `OpenIdConnectAuthenticationNotifications` object en opgeslagen in Hallo `Notifications` variabele.</span><span class="sxs-lookup"><span data-stu-id="8e35b-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="8e35b-198">In ons voorbeeld definiëren we drie verschillende retouraanroepen afhankelijk van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8e35b-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="8e35b-199">Met behulp van verschillende beleidsregels</span><span class="sxs-lookup"><span data-stu-id="8e35b-199">Using different policies</span></span>

<span data-ttu-id="8e35b-200">Hallo `RedirectToIdentityProvider` melding wordt geactiveerd wanneer een aanvraag wordt gedaan tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8e35b-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="8e35b-201">In de callback-functie Hallo `OnRedirectToIdentityProvider`, we in Hallo uitgaande oproep als we toouse wilt controleren of een ander beleid.</span><span class="sxs-lookup"><span data-stu-id="8e35b-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="8e35b-202">In volgorde toodo een wachtwoord opnieuw instellen of een profiel te bewerken, moet u toouse Hallo corresponderende beleid zoals Hallo wachtwoord opnieuw instellen van beleid in plaats van Hallo "Registreren of aanmelden" standaardbeleid.</span><span class="sxs-lookup"><span data-stu-id="8e35b-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="8e35b-203">In ons voorbeeld wanneer een gebruiker wil tooreset Hallo wachtwoord of Hallo-profiel te bewerken we Hallo beleid toevoegen we toouse liever naar Hallo OWIN context.</span><span class="sxs-lookup"><span data-stu-id="8e35b-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="8e35b-204">Dat kan worden gedaan door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8e35b-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="8e35b-205">En u kunt de callback-functie Hallo implementeren `OnRedirectToIdentityProvider` door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8e35b-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="8e35b-206">Afhandeling van autorisatiecodes</span><span class="sxs-lookup"><span data-stu-id="8e35b-206">Handling authorization codes</span></span>

<span data-ttu-id="8e35b-207">Hallo `AuthorizationCodeReceived` melding wordt geactiveerd wanneer een autorisatiecode wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8e35b-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="8e35b-208">Hallo OpenID Connect middleware biedt geen ondersteuning voor uitwisselen codes voor toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="8e35b-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="8e35b-209">U kunt handmatig uitwisselen Hallo-code voor het Hallo-token in een callback-functie.</span><span class="sxs-lookup"><span data-stu-id="8e35b-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="8e35b-210">Raadpleeg voor meer informatie Hallo [documentatie](active-directory-b2c-devquickstarts-web-api-dotnet.md) waarin wordt uitgelegd hoe.</span><span class="sxs-lookup"><span data-stu-id="8e35b-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="8e35b-211">Foutafhandeling</span><span class="sxs-lookup"><span data-stu-id="8e35b-211">Handling errors</span></span>

<span data-ttu-id="8e35b-212">Hallo `AuthenticationFailed` melding wordt geactiveerd wanneer de verificatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8e35b-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="8e35b-213">In de callback-methode kunt u fouten Hallo verwerken als u wilt.</span><span class="sxs-lookup"><span data-stu-id="8e35b-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="8e35b-214">U moet echter een controle voor de foutcode Hallo toevoegen `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="8e35b-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="8e35b-215">Bij het uitvoeren van Hallo "Registreren of aanmelden" beleid Hallo Hallo gebruiker Hallo kans tooselect heeft een **wachtwoord vergeten?** koppeling.</span><span class="sxs-lookup"><span data-stu-id="8e35b-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="8e35b-216">In dit geval stuurt Azure AD B2C uw app die fout die aangeeft dat uw app moet worden gebruikt voor het aanbrengen van een aanvraag met beleid voor wachtwoordherstel Hallo in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="8e35b-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
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

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="8e35b-217">Verificatie aanvragen tooAzure AD verzenden</span><span class="sxs-lookup"><span data-stu-id="8e35b-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="8e35b-218">Uw app is nu correct geconfigureerde toocommunicate met Azure AD B2C via Hallo OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="8e35b-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="8e35b-219">OWIN beheert Hallo details van verificatieberichten, het valideren van tokens van Azure AD B2C en het onderhoud van de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="8e35b-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="8e35b-220">Alles wat blijft is tooinitiate van elke gebruiker stroom.</span><span class="sxs-lookup"><span data-stu-id="8e35b-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="8e35b-221">Wanneer een gebruiker selecteert **Sign up/aanmelden**, **profiel bewerken**, of **wachtwoord opnieuw instellen** in Hallo web-app, die zijn gekoppeld Hallo actie wordt aangeroepen in de `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="8e35b-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="8e35b-222">U kunt ook OWIN toosign uit Hallo gebruiker uit Hallo app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e35b-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="8e35b-223">In `Controllers\AccountController.cs` we hebben:</span><span class="sxs-lookup"><span data-stu-id="8e35b-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="8e35b-224">In aanvulling tooexplicitly aanroepen van een beleid, kunt u een `[Authorize]` code in uw domeincontrollers die een beleid wordt uitgevoerd als Hallo gebruiker niet is aangemeld.</span><span class="sxs-lookup"><span data-stu-id="8e35b-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="8e35b-225">Open `Controllers\HomeController.cs` en voeg Hallo `[Authorize]` tag toohello claims controller.</span><span class="sxs-lookup"><span data-stu-id="8e35b-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="8e35b-226">OWIN selecteert Hallo laatste beleid geconfigureerd wanneer hello `[Authorize]` tag is bereikt.</span><span class="sxs-lookup"><span data-stu-id="8e35b-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="8e35b-227">Gebruikersgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="8e35b-227">Display user information</span></span>

<span data-ttu-id="8e35b-228">Wanneer u gebruikers verifiëren met behulp van OpenID Connect, Azure AD B2C retourneert een ID token toohello app met **claims**.</span><span class="sxs-lookup"><span data-stu-id="8e35b-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="8e35b-229">Dit zijn asserties over Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8e35b-229">These are assertions about hello user.</span></span> <span data-ttu-id="8e35b-230">Uw app kunt u claims toopersonalize gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e35b-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="8e35b-231">Open Hallo `Controllers\HomeController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="8e35b-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="8e35b-232">U hebt toegang tot gebruikersclaims in uw domeincontrollers via Hallo `ClaimsPrincipal.Current` SPN-object.</span><span class="sxs-lookup"><span data-stu-id="8e35b-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="8e35b-233">U hebt toegang tot een claim dat uw toepassing in Hallo dezelfde ontvangt manier.</span><span class="sxs-lookup"><span data-stu-id="8e35b-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="8e35b-234">Een lijst van alle Hallo claims Hallo app ontvangt is beschikbaar voor u op Hallo **Claims** pagina.</span><span class="sxs-lookup"><span data-stu-id="8e35b-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
