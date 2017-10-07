---
title: aaaAzure AD Xamarin aan de slag | Microsoft Docs
description: Xamarin-toepassingen die integreren met Azure AD voor aanmelden en roept u Azure AD-beveiligde API's met OAuth bouwen.
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="4260d-103">Azure AD integreren met Xamarin-apps</span><span class="sxs-lookup"><span data-stu-id="4260d-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4260d-104">Met Xamarin, kunt u mobiele apps in C# die kunnen worden uitgevoerd op iOS, Android en Windows (mobiele apparaten en pc's).</span><span class="sxs-lookup"><span data-stu-id="4260d-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="4260d-105">Als u een app met Xamarin maakt, kunt Azure Active Directory (Azure AD) u eenvoudige tooauthenticate gebruikers met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="4260d-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="4260d-106">Hallo-app kan ook veilig een web-API die wordt beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4260d-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="4260d-107">Azure AD levert voor Xamarin-apps die tooaccess beveiligde bronnen moeten, Hallo Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="4260d-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="4260d-108">Hallo enig doel van ADAL toomake is het eenvoudig voor apps tooget toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="4260d-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="4260d-109">toodemonstrate hoe eenvoudig het is dit artikel laat zien hoe toobuild DirectorySearcher apps die:</span><span class="sxs-lookup"><span data-stu-id="4260d-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="4260d-110">Voer op iOS, Android, Windows-bureaublad, Windows Phone en Windows Store.</span><span class="sxs-lookup"><span data-stu-id="4260d-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="4260d-111">Met een enkele portable class-bibliotheek (PCL) tooauthenticate gebruikers en tokens krijgen voor hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="4260d-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="4260d-112">Zoeken in een map voor gebruikers met een opgegeven UPN.</span><span class="sxs-lookup"><span data-stu-id="4260d-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="4260d-113">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="4260d-113">Before you get started</span></span>
* <span data-ttu-id="4260d-114">Hallo downloaden [basisproject](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4260d-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="4260d-115">Elke download is een Visual Studio 2013-oplossing.</span><span class="sxs-lookup"><span data-stu-id="4260d-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="4260d-116">U moet ook een Azure AD-tenant in welke toocreate gebruikers en het Hallo-app registreren.</span><span class="sxs-lookup"><span data-stu-id="4260d-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="4260d-117">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="4260d-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="4260d-118">Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende vier secties.</span><span class="sxs-lookup"><span data-stu-id="4260d-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="4260d-119">Stap 1: Uw Xamarin-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="4260d-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="4260d-120">Omdat deze zelfstudie projecten voor iOS, Android en Windows omvat, moet u zowel Visual Studio en Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4260d-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="4260d-121">toocreate hello nodig omgeving, volledige Hallo proces in [ingesteld omhoog en installeer Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="4260d-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="4260d-122">Hallo-instructies bevatten materiaal die u meer informatie over Xamarin toolearn bekijken kunt terwijl u voor Hallo installaties toobe is voltooid wacht.</span><span class="sxs-lookup"><span data-stu-id="4260d-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="4260d-123">Nadat u Hallo-installatie hebt voltooid, opent u Hallo oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4260d-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="4260d-124">Daar vindt u zes projecten: vijf platform-specifieke projecten en één PCL, DirectorySearcher.cs, die wordt gedeeld met alle platforms.</span><span class="sxs-lookup"><span data-stu-id="4260d-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="4260d-125">Stap 2: Hallo DirectorySearcher app registreren</span><span class="sxs-lookup"><span data-stu-id="4260d-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="4260d-126">tooenable hello app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="4260d-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="4260d-127">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="4260d-127">Here's how:</span></span>

1. <span data-ttu-id="4260d-128">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4260d-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4260d-129">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="4260d-129">On hello top bar, click your account.</span></span> <span data-ttu-id="4260d-130">Klik vervolgens onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.</span><span class="sxs-lookup"><span data-stu-id="4260d-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="4260d-131">Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4260d-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4260d-132">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4260d-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4260d-133">toocreate een nieuwe **systeemeigen clienttoepassing**, volg de aanwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="4260d-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="4260d-134">**Naam** Hallo app toousers beschrijft.</span><span class="sxs-lookup"><span data-stu-id="4260d-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="4260d-135">**Omleidings-URI** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden.</span><span class="sxs-lookup"><span data-stu-id="4260d-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="4260d-136">Voer een waarde (bijvoorbeeld http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="4260d-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="4260d-137">Nadat u de registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="4260d-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="4260d-138">Hallo-waarde in Hallo kopiëren **toepassing** tabblad omdat u hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="4260d-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="4260d-139">Op Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4260d-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="4260d-140">Selecteer **Microsoft Graph** zoals Hallo API.</span><span class="sxs-lookup"><span data-stu-id="4260d-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="4260d-141">Onder **gedelegeerde machtigingen**, Hallo toevoegen **Directory-gegevens lezen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="4260d-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="4260d-142">Hierdoor Hallo app tooquery Hallo Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4260d-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="4260d-143">Stap 3: Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="4260d-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="4260d-144">Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="4260d-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="4260d-145">ADAL toocommunicate tooenable in Azure AD, geef deze de enige informatie over app-registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4260d-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="4260d-146">ADAL toohello DirectorySearcher project toevoegen met behulp van Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="4260d-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="4260d-147">Opmerking dat twee bibliotheekverwijzingen tooeach project worden toegevoegd: Hallo PCL gedeelte van de ADAL en een gedeelte van de platform-specifieke.</span><span class="sxs-lookup"><span data-stu-id="4260d-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="4260d-148">Open in Hallo DirectorySearcherLib project DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="4260d-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="4260d-149">Hallo klasse lidwaarden vervangt door Hallo-waarden die u hebt ingevoerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4260d-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="4260d-150">Uw code verwijst toothese waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="4260d-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="4260d-151">Hallo *tenant* Hallo domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4260d-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="4260d-152">Hallo *clientId* is Hallo client-ID van Hallo-app, die u hebt gekopieerd uit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="4260d-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="4260d-153">Hallo *returnUri* Hallo omleidings-URI die u hebt ingevoerd in Hallo-portal (bijvoorbeeld http://DirectorySearcher) is.</span><span class="sxs-lookup"><span data-stu-id="4260d-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="4260d-154">Stap 4: Gebruik ADAL tooget tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="4260d-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="4260d-155">Bijna alle Hallo-app verificatielogica ligt in `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="4260d-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="4260d-156">Alle benodigde in Hallo platform-specifieke projecten toopass een toohello contextuele parameter is `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="4260d-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="4260d-157">Open DirectorySearcher.cs en voeg vervolgens een nieuwe parameter toohello `SearchByAlias(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="4260d-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="4260d-158">`IPlatformParameters`is contextuele Hallo-parameter die ingekapseld Hallo platform-specifieke objecten die behoeften ADAL tooperform Hallo verificatie.</span><span class="sxs-lookup"><span data-stu-id="4260d-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="4260d-159">Initialiseren `AuthenticationContext`, dit is de primaire klasse Hallo van ADAL.</span><span class="sxs-lookup"><span data-stu-id="4260d-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="4260d-160">Deze actie geeft ADAL Hallo coördineert deze behoeften toocommunicate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4260d-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="4260d-161">Roep `AcquireTokenAsync(...)`, die Hallo accepteert `IPlatformParameters` object en het Hallo-authenticatiestroom die nodig zijn tooreturn een token toohello-app wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4260d-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="4260d-162">`AcquireTokenAsync(...)`eerste pogingen tooreturn een token voor Hallo aangevraagd resource (in dit geval hello Graph API) zonder tooenter gebruikers hun referenties (via caching of oude tokens vernieuwen).</span><span class="sxs-lookup"><span data-stu-id="4260d-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="4260d-163">Indien nodig wordt gebruikers hello Azure AD-aanmeldingspagina vóór het aangevraagde Hallo-token ophalen.</span><span class="sxs-lookup"><span data-stu-id="4260d-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="4260d-164">Hallo access token toohello Graph API-aanvraag in Hallo koppelen **autorisatie** header:</span><span class="sxs-lookup"><span data-stu-id="4260d-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="4260d-165">Dit is alles wat voor Hallo `DirectorySearcher` identiteitsgerelateerde PCL en Hallo van app-code.</span><span class="sxs-lookup"><span data-stu-id="4260d-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="4260d-166">Alles wat u hoeft alleen nog toocall hello `SearchByAlias(...)` methode in elk platform weergaven en, indien nodig, tooadd code voor het verwerken van correct Hallo levenscyclus van de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="4260d-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="4260d-167">Android</span><span class="sxs-lookup"><span data-stu-id="4260d-167">Android</span></span>
1. <span data-ttu-id="4260d-168">Voeg in MainActivity.cs, een aanroep te`SearchByAlias(...)` Klik op de knop Hallo handler:</span><span class="sxs-lookup"><span data-stu-id="4260d-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="4260d-169">Hallo overschrijven `OnActivityResult` lifecycle methode tooforward verificatie wordt de juiste methode terug toohello omgeleid.</span><span class="sxs-lookup"><span data-stu-id="4260d-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="4260d-170">ADAL biedt een Help-methode voor dit in Android:</span><span class="sxs-lookup"><span data-stu-id="4260d-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="4260d-171">Windows-bureaublad</span><span class="sxs-lookup"><span data-stu-id="4260d-171">Windows Desktop</span></span>
<span data-ttu-id="4260d-172">MainWindow.xaml.cs, zorg er in een aanroep te`SearchByAlias(...)` door een `WindowInteropHelper` in van het bureaublad Hallo `PlatformParameters` object:</span><span class="sxs-lookup"><span data-stu-id="4260d-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="4260d-173">iOS</span><span class="sxs-lookup"><span data-stu-id="4260d-173">iOS</span></span>
<span data-ttu-id="4260d-174">Hallo iOS in DirSearchClient_iOSViewController.cs, `PlatformParameters` object een verwijzing toohello weergavebesturing nodig:</span><span class="sxs-lookup"><span data-stu-id="4260d-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="4260d-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="4260d-175">Windows Universal</span></span>
<span data-ttu-id="4260d-176">In Windows universele MainPage.xaml.cs openen en vervolgens implementeren Hallo `Search` methode.</span><span class="sxs-lookup"><span data-stu-id="4260d-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="4260d-177">Deze methode maakt gebruik van een Help-methode in een gedeeld project tooupdate UI indien nodig.</span><span class="sxs-lookup"><span data-stu-id="4260d-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="4260d-178">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="4260d-178">What's next</span></span>
<span data-ttu-id="4260d-179">U hebt nu een werkende Xamarin-app die u kunt verificatie van gebruikers en veilig aanroepen van web-API's met behulp van OAuth 2.0 op vijf verschillende platforms.</span><span class="sxs-lookup"><span data-stu-id="4260d-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="4260d-180">Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu Hallo tijd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="4260d-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="4260d-181">Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4260d-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="4260d-182">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="4260d-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="4260d-183">ADAL maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="4260d-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="4260d-184">Zorgt het voor alle Hallo dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="4260d-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="4260d-185">U moet tooknow één API-aanroep `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="4260d-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="4260d-186">Ter referentie: downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="4260d-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="4260d-187">U kunt nu verplaatsen op tooadditional identity-scenario's.</span><span class="sxs-lookup"><span data-stu-id="4260d-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="4260d-188">Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4260d-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
