---
title: Azure AD-Xamarin aan de slag | Microsoft Docs
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
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="5cc19-103">Azure AD integreren met Xamarin-apps</span><span class="sxs-lookup"><span data-stu-id="5cc19-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="5cc19-104">Met Xamarin, kunt u mobiele apps in C# die kunnen worden uitgevoerd op iOS, Android en Windows (mobiele apparaten en pc's).</span><span class="sxs-lookup"><span data-stu-id="5cc19-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="5cc19-105">Als u een app met Xamarin maakt, met Azure Active Directory (Azure AD) kunt u eenvoudig gebruikers worden geverifieerd met hun Azure AD-accounts kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5cc19-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="5cc19-106">De app kan ook veilig een web-API die wordt beveiligd door Azure AD, zoals de Office 365-API of de Azure-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5cc19-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="5cc19-107">Azure AD levert voor Xamarin-apps die toegang moeten krijgen tot beveiligde bronnen, de Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="5cc19-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="5cc19-108">Het enige doel van ADAL is gemakkelijk om apps te toegangstokens ophalen.</span><span class="sxs-lookup"><span data-stu-id="5cc19-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="5cc19-109">Als u wilt laten zien hoe eenvoudig het is, in dit artikel laat zien hoe DirectorySearcher apps bouwen die:</span><span class="sxs-lookup"><span data-stu-id="5cc19-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="5cc19-110">Voer op iOS, Android, Windows-bureaublad, Windows Phone en Windows Store.</span><span class="sxs-lookup"><span data-stu-id="5cc19-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="5cc19-111">Een enkele draagbare klassebibliotheek (PCL) gebruiken voor het verifiëren van gebruikers en tokens krijgen voor de Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="5cc19-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="5cc19-112">Zoeken in een map voor gebruikers met een opgegeven UPN.</span><span class="sxs-lookup"><span data-stu-id="5cc19-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="5cc19-113">Voordat u aan de slag gaat</span><span class="sxs-lookup"><span data-stu-id="5cc19-113">Before you get started</span></span>
* <span data-ttu-id="5cc19-114">Download de [basisproject](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), of download de [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5cc19-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="5cc19-115">Elke download is een Visual Studio 2013-oplossing.</span><span class="sxs-lookup"><span data-stu-id="5cc19-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="5cc19-116">U moet ook een Azure AD-tenant waarin gebruikers maken en de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="5cc19-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="5cc19-117">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5cc19-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="5cc19-118">Wanneer u klaar bent, voert u de procedures in de volgende vier secties.</span><span class="sxs-lookup"><span data-stu-id="5cc19-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="5cc19-119">Stap 1: Uw Xamarin-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="5cc19-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="5cc19-120">Omdat deze zelfstudie projecten voor iOS, Android en Windows omvat, moet u zowel Visual Studio en Xamarin.</span><span class="sxs-lookup"><span data-stu-id="5cc19-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="5cc19-121">Voltooi het proces in voor het maken van de benodigde omgeving [ingesteld omhoog en installeer Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="5cc19-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="5cc19-122">De instructies bevatten materiaal die u bekijken kunt voor meer informatie over Xamarin terwijl u voor de installatie wacht te voltooien.</span><span class="sxs-lookup"><span data-stu-id="5cc19-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="5cc19-123">Nadat u de installatie hebt voltooid, opent u de oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cc19-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="5cc19-124">Daar vindt u zes projecten: vijf platform-specifieke projecten en één PCL, DirectorySearcher.cs, die wordt gedeeld met alle platforms.</span><span class="sxs-lookup"><span data-stu-id="5cc19-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="5cc19-125">Stap 2: De app DirectorySearcher te registreren</span><span class="sxs-lookup"><span data-stu-id="5cc19-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="5cc19-126">Als u wilt inschakelen voor de app tokens krijgen, moet u eerst registreren in uw Azure AD-tenant en verleent deze machtiging voor toegang tot de Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="5cc19-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="5cc19-127">Dit doet u al volgt:</span><span class="sxs-lookup"><span data-stu-id="5cc19-127">Here's how:</span></span>

1. <span data-ttu-id="5cc19-128">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5cc19-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5cc19-129">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="5cc19-129">On the top bar, click your account.</span></span> <span data-ttu-id="5cc19-130">Klik vervolgens onder de **Directory** , selecteert u de Active Directory-tenant waar u de app te registreren.</span><span class="sxs-lookup"><span data-stu-id="5cc19-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="5cc19-131">Klik op **meer Services** in het linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cc19-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5cc19-132">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5cc19-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="5cc19-133">Maak een nieuwe **systeemeigen clienttoepassing**, volg de aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="5cc19-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="5cc19-134">**Naam** beschrijving van de app voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5cc19-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="5cc19-135">**Omleidings-URI** is een combinatie schema en de tekenreeks die gebruikmaakt van Azure AD token antwoorden retourneren.</span><span class="sxs-lookup"><span data-stu-id="5cc19-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="5cc19-136">Voer een waarde (bijvoorbeeld http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="5cc19-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="5cc19-137">Nadat u de registratie hebt voltooid, wijst Azure AD de app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="5cc19-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="5cc19-138">Kopieer de waarde van de **toepassing** tabblad omdat u hebt deze later nodig.</span><span class="sxs-lookup"><span data-stu-id="5cc19-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="5cc19-139">Op de **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5cc19-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="5cc19-140">Selecteer **Microsoft Graph** als de API.</span><span class="sxs-lookup"><span data-stu-id="5cc19-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="5cc19-141">Onder **gedelegeerde machtigingen**, voeg de **Directory-gegevens lezen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="5cc19-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="5cc19-142">Deze actie kan de app om op te vragen de Graph-API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5cc19-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="5cc19-143">Stap 3: Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="5cc19-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="5cc19-144">Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="5cc19-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="5cc19-145">Om in te schakelen ADAL om te communiceren met Azure AD, geef deze de enige informatie over de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="5cc19-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="5cc19-146">ADAL toevoegen aan het project DirectorySearcher met behulp van de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="5cc19-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

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

    <span data-ttu-id="5cc19-147">Houd er rekening mee dat de twee verwijzingen van de tapewisselaar worden toegevoegd aan elk project: het gedeelte PCL van ADAL en een deel van de platform-specifieke.</span><span class="sxs-lookup"><span data-stu-id="5cc19-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="5cc19-148">Open in het project DirectorySearcherLib DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="5cc19-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="5cc19-149">Vervang de waarden van de lid klasse met de waarden die u hebt ingevoerd in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5cc19-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="5cc19-150">Uw code verwijst naar deze waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="5cc19-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="5cc19-151">De *tenant* is het domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="5cc19-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="5cc19-152">De *clientId* is de client-ID van de app, die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="5cc19-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="5cc19-153">De *returnUri* is de omleidings-URI die u hebt ingevoerd in de portal (bijvoorbeeld http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="5cc19-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="5cc19-154">Stap 4: Gebruik ADAL tokens ophalen uit Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc19-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="5cc19-155">Bijna alle van de app verificatielogica ligt in `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="5cc19-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="5cc19-156">In de platform-specifieke projecten nodig is om door te geven van een contextuele parameter voor de `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="5cc19-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="5cc19-157">Open DirectorySearcher.cs en voeg vervolgens een nieuwe parameter voor de `SearchByAlias(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="5cc19-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="5cc19-158">`IPlatformParameters`de contextuele parameter die kapselt de platform-specifieke objecten die ADAL nodig zijn voor de verificatie is.</span><span class="sxs-lookup"><span data-stu-id="5cc19-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="5cc19-159">Initialiseren `AuthenticationContext`, dit is de primaire klasse van ADAL.</span><span class="sxs-lookup"><span data-stu-id="5cc19-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="5cc19-160">Deze actie geeft ADAL de coördinaten die kan communiceren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cc19-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="5cc19-161">Roep `AcquireTokenAsync(...)`, die accepteert de `IPlatformParameters` object en roept de authenticatiestroom dat nodig is om een token terug naar de app.</span><span class="sxs-lookup"><span data-stu-id="5cc19-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

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

    <span data-ttu-id="5cc19-162">`AcquireTokenAsync(...)`eerst probeert te retourneren van een token voor de aangevraagde bron (in dit geval de Graph-API) zonder gebruikers hun referenties invoeren (via caching of oude tokens vernieuwen).</span><span class="sxs-lookup"><span data-stu-id="5cc19-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="5cc19-163">Zo nodig toont het gebruikers de aanmeldingspagina van Azure AD voordat de aangevraagde token ophalen.</span><span class="sxs-lookup"><span data-stu-id="5cc19-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="5cc19-164">Het toegangstoken koppelen aan de Graph API-aanvraag in de **autorisatie** header:</span><span class="sxs-lookup"><span data-stu-id="5cc19-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="5cc19-165">Dit is alles wat voor de `DirectorySearcher` PCL en de app de identiteitsgerelateerde code.</span><span class="sxs-lookup"><span data-stu-id="5cc19-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="5cc19-166">Alles wat u hoeft alleen nog aan te roepen de `SearchByAlias(...)` methode in elk platform weergaven en, indien nodig, voeg code toe voor de levenscyclus van de gebruikersinterface correct verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5cc19-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="5cc19-167">Android</span><span class="sxs-lookup"><span data-stu-id="5cc19-167">Android</span></span>
1. <span data-ttu-id="5cc19-168">In MainActivity.cs, Voeg een aanroep naar `SearchByAlias(...)` op de knop klikt u op de handler:</span><span class="sxs-lookup"><span data-stu-id="5cc19-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="5cc19-169">Overschrijf de `OnActivityResult` lifecycle-methode voor het doorsturen van de verificatie die wordt omgeleid naar de juiste methode.</span><span class="sxs-lookup"><span data-stu-id="5cc19-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="5cc19-170">ADAL biedt een Help-methode voor dit in Android:</span><span class="sxs-lookup"><span data-stu-id="5cc19-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="5cc19-171">Windows-bureaublad</span><span class="sxs-lookup"><span data-stu-id="5cc19-171">Windows Desktop</span></span>
<span data-ttu-id="5cc19-172">Controleer in MainWindow.xaml.cs, een aanroep van `SearchByAlias(...)` door een `WindowInteropHelper` op het bureaublad `PlatformParameters` object:</span><span class="sxs-lookup"><span data-stu-id="5cc19-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="5cc19-173">iOS</span><span class="sxs-lookup"><span data-stu-id="5cc19-173">iOS</span></span>
<span data-ttu-id="5cc19-174">In DirSearchClient_iOSViewController.cs, het bestand iOS `PlatformParameters` object krijgt een verwijzing naar de weergavebesturing:</span><span class="sxs-lookup"><span data-stu-id="5cc19-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="5cc19-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="5cc19-175">Windows Universal</span></span>
<span data-ttu-id="5cc19-176">In Windows universele MainPage.xaml.cs openen en vervolgens implementeert u de `Search` methode.</span><span class="sxs-lookup"><span data-stu-id="5cc19-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="5cc19-177">Deze methode maakt gebruik van een Help-methode in een gedeeld project UI indien nodig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5cc19-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="5cc19-178">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="5cc19-178">What's next</span></span>
<span data-ttu-id="5cc19-179">U hebt nu een werkende Xamarin-app die u kunt verificatie van gebruikers en veilig aanroepen van web-API's met behulp van OAuth 2.0 op vijf verschillende platforms.</span><span class="sxs-lookup"><span data-stu-id="5cc19-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="5cc19-180">Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu tijd om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="5cc19-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="5cc19-181">Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5cc19-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="5cc19-182">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="5cc19-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="5cc19-183">ADAL kunt gemakkelijk veelvoorkomende identiteit functies opnemen in de app.</span><span class="sxs-lookup"><span data-stu-id="5cc19-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="5cc19-184">Zorgt het alle dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, dat de gebruiker een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="5cc19-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="5cc19-185">U moet weten slechts één API-aanroep, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="5cc19-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="5cc19-186">Ter referentie: download de [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).</span><span class="sxs-lookup"><span data-stu-id="5cc19-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="5cc19-187">U kunt nu verder met de identiteit van de aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="5cc19-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="5cc19-188">Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5cc19-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
