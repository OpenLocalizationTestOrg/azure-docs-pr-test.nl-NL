---
title: Azure AD .NET aan de slag | Microsoft Docs
description: "Het bouwen van een toepassing .NET Windows-bureaublad, die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd met OAuth API's."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="84184-103">Azure AD integreren met een Windows-bureaublad WPF-App</span><span class="sxs-lookup"><span data-stu-id="84184-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="84184-104">Als u een bureaubladtoepassing ontwikkelt, kunt Azure AD u eenvoudig en snel voor u om uw gebruikers met hun Active Directory-account te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="84184-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="84184-105">Ook kunt uw toepassing veilig gebruiken voor een web-API die zijn beveiligd door Azure AD, zoals de Office 365-API of de Azure-API.</span><span class="sxs-lookup"><span data-stu-id="84184-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="84184-106">Voor .NET systeemeigen clients die toegang moeten krijgen tot beveiligde bronnen, levert Azure AD de Active Directory Authentication Library of ADAL.</span><span class="sxs-lookup"><span data-stu-id="84184-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="84184-107">Enig doel in het leven van ADAL is gemakkelijker voor uw app toegangstokens ophalen.</span><span class="sxs-lookup"><span data-stu-id="84184-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="84184-108">Als u wilt laten zien hoe eenvoudig het is, hier we je een .NET WPF-takenlijst-toepassing bouwt die:</span><span class="sxs-lookup"><span data-stu-id="84184-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="84184-109">Krijgt toegang tot tokens voor het aanroepen van de Azure AD Graph API met behulp van de [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="84184-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="84184-110">Zoekt een directory voor gebruikers met een alias voor een gegeven.</span><span class="sxs-lookup"><span data-stu-id="84184-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="84184-111">Tekenen gebruikers uit.</span><span class="sxs-lookup"><span data-stu-id="84184-111">Signs users out.</span></span>

<span data-ttu-id="84184-112">De volledige werkende toepassing bouwen, moet u het:</span><span class="sxs-lookup"><span data-stu-id="84184-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="84184-113">Uw toepassing registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84184-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="84184-114">Installeren en configureren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="84184-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="84184-115">ADAL gebruikt om tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84184-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="84184-116">Aan de slag [de basis van de app downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) of [het voltooide voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="84184-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="84184-117">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="84184-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="84184-118">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="84184-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="84184-119">1. De toepassing DirectorySearcher registreren</span><span class="sxs-lookup"><span data-stu-id="84184-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="84184-120">Als u wilt inschakelen voor uw app tokens krijgen, moet u eerst registreren in uw Azure AD-tenant en verleent deze machtiging voor toegang tot de Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="84184-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="84184-121">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84184-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="84184-122">Klik op de bovenste balk op je account en klikt u onder de **Directory** kiest u de Active Directory-tenant waar u wilt uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="84184-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="84184-123">Klik op **meer Services** in de nav linkerkant en kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84184-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="84184-124">Klik op **App registraties** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84184-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="84184-125">Volg de aanwijzingen en maak een nieuwe **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="84184-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="84184-126">De **naam** van de toepassing bevat een beschrijving van uw toepassing aan eindgebruikers</span><span class="sxs-lookup"><span data-stu-id="84184-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="84184-127">De **omleidings-Uri** is een combinatie schema en de tekenreeks die door Azure AD wordt gebruikt om te retourneren van reacties token.</span><span class="sxs-lookup"><span data-stu-id="84184-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="84184-128">Voer van een specifieke waarde in voor uw toepassing bijvoorbeeld `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="84184-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="84184-129">Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="84184-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="84184-130">U moet deze waarde in de volgende secties, dus kopiëren van de toepassingspagina.</span><span class="sxs-lookup"><span data-stu-id="84184-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="84184-131">Van de **instellingen** pagina **Required Permissions** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84184-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="84184-132">Selecteer de **Microsoft Graph** als de API en voeg de **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="84184-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="84184-133">Hiermee schakelt u uw toepassing query uitvoeren op de Graph-API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="84184-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="84184-134">2. Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="84184-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="84184-135">Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="84184-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="84184-136">In de volgorde voor ADAL om te communiceren met Azure AD, moet u voorzien enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="84184-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="84184-137">Beginnen met het ADAL toevoegen aan het DirectorySearcher-project met de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="84184-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="84184-138">Open in het project DirectorySearcher `app.config`.</span><span class="sxs-lookup"><span data-stu-id="84184-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="84184-139">Vervang de waarden van de elementen in de `<appSettings>` sectie in overeenstemming met de waarden die u in de Azure-Portal hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="84184-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="84184-140">Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="84184-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="84184-141">De `ida:Tenant` is het domein van uw Azure AD-tenant, bijvoorbeeld contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="84184-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="84184-142">De `ida:ClientId` is de clientId van uw toepassing die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="84184-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="84184-143">De `ida:RedirectUri` is de omleiding url die u hebt geregistreerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="84184-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="84184-144">3.    Gebruikmaken van ADAL Tokens van AAD ophalen</span><span class="sxs-lookup"><span data-stu-id="84184-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="84184-145">Het basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, aanroept `authContext.AcquireTokenAsync(...)`, en doet de rest van ADAL.</span><span class="sxs-lookup"><span data-stu-id="84184-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="84184-146">In de `DirectorySearcher` project, open `MainWindow.xaml.cs` en zoek de `MainWindow()` methode.</span><span class="sxs-lookup"><span data-stu-id="84184-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="84184-147">De eerste stap is het initialiseren van uw app `AuthenticationContext` -ADAL de primaire klasse.</span><span class="sxs-lookup"><span data-stu-id="84184-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="84184-148">Dit is waar het doorgeven van ADAL de coördinaten nodig om te communiceren met Azure AD en hoe deze tokens in de cache.</span><span class="sxs-lookup"><span data-stu-id="84184-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="84184-149">Nu zoeken de `Search(...)` methode, die wordt aangeroepen wanneer de gebruiker cliks de "zoeken" in de gebruikersinterface van de app.</span><span class="sxs-lookup"><span data-stu-id="84184-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="84184-150">Deze methode maakt een GET-aanvraag voor Azure AD Graph API aan query voor gebruikers wiens UPN met de opgegeven zoekterm begint.</span><span class="sxs-lookup"><span data-stu-id="84184-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="84184-151">Maar om de Graph API een query uitvoert, moet u een access_token in de `Authorization` header van de aanvraag - dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="84184-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="84184-152">Wanneer uw app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert te retourneren van een token zonder dat de gebruiker om referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="84184-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="84184-153">Als ADAL wordt vastgesteld dat de gebruiker zich aanmelden moet bij een token verkrijgen, wordt het een aanmelding weergegeven, verzamelen van referenties van de gebruiker en retourneren een token na verificatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="84184-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="84184-154">Als ADAL kunnen niet worden geretourneerd van een token voor een of andere reden is, genereert het een `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="84184-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="84184-155">U ziet dat de `AuthenticationResult` object bevat een `UserInfo` -object dat kan worden gebruikt voor het verzamelen van informatie die uw app mogelijk nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="84184-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="84184-156">In de DirectorySearcher `UserInfo` wordt gebruikt voor het aanpassen van de gebruikersinterface van de app met de id van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="84184-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="84184-157">Wanneer de gebruiker op de knop 'Afmelden', willen we ervoor te zorgen dat de volgende aanroep `AcquireTokenAsync(...)` vraagt de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="84184-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="84184-158">Met ADAL, is dit is net zo eenvoudig als het token cache wissen:</span><span class="sxs-lookup"><span data-stu-id="84184-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="84184-159">Echter, als de gebruiker heeft niet op de knop 'Afmelden', wilt u de sessie van de gebruiker voor de volgende keer dat ze de DirectorySearcher worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="84184-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="84184-160">Wanneer de app opent, kunt u controleren van de ADAL-tokencache voor een bestaande token en de gebruikersinterface worden dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="84184-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="84184-161">In de `CheckForCachedToken()` methode, moet u een andere aanroep van `AcquireTokenAsync(...)`, ditmaal doorgeven in de `PromptBehavior.Never` parameter.</span><span class="sxs-lookup"><span data-stu-id="84184-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="84184-162">`PromptBehavior.Never`vertelt ADAL dat de gebruiker niet moet worden gevraagd voor aanmelding en ADAL moet in plaats daarvan Veroorzaak een exception wanneer het niet lukt om te retourneren van een token.</span><span class="sxs-lookup"><span data-stu-id="84184-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="84184-163">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="84184-163">Congratulations!</span></span> <span data-ttu-id="84184-164">U nu beschikken over een werkende .NET WPF-toepassing met de mogelijkheid om te verifiëren van gebruikers, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en algemene informatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="84184-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="84184-165">Als u nog niet gedaan hebt, is nu de tijd voor het vullen van uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="84184-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="84184-166">Uitvoeren van uw app DirectorySearcher en meld u aan met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="84184-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="84184-167">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="84184-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="84184-168">Sluit de app en voer deze opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="84184-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="84184-169">U ziet hoe de gebruikerssessie blijft intact.</span><span class="sxs-lookup"><span data-stu-id="84184-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="84184-170">Meld u af en meld u opnieuw aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="84184-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="84184-171">ADAL kunt eenvoudig gebruikmaken van al deze algemene identiteit functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="84184-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="84184-172">Dit zorgt voor al het werk dirty voor u - Cachebeheer, OAuth-protocolondersteuning, dat de gebruiker een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="84184-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="84184-173">Alles wat u moet weten één API-aanroep is `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="84184-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="84184-174">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) is opgegeven [hier](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="84184-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="84184-175">U kunt nu verder met aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="84184-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="84184-176">U wilt proberen:</span><span class="sxs-lookup"><span data-stu-id="84184-176">You may want to try:</span></span>

[<span data-ttu-id="84184-177">Een .NET-Web-API met Azure AD beveiligen >></span><span class="sxs-lookup"><span data-stu-id="84184-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

