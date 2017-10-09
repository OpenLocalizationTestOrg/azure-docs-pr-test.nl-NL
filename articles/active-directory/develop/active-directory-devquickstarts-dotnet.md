---
title: aaaAzure AD .NET aan de slag | Microsoft Docs
description: "Hoe toobuild een .NET Windows-bureaublad-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd met OAuth API's."
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
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="b26ed-103">Azure AD integreren met een Windows-bureaublad WPF-App</span><span class="sxs-lookup"><span data-stu-id="b26ed-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b26ed-104">Als u een bureaubladtoepassing ontwikkelt, kunt Azure AD u eenvoudig en snel voor tooauthenticate u uw gebruikers met hun Active Directory-accounts.</span><span class="sxs-lookup"><span data-stu-id="b26ed-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="b26ed-105">Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="b26ed-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="b26ed-106">Azure AD levert voor .NET-systeemeigen clients waarvoor tooaccess beveiligde bronnen, Hallo Active Directory Authentication Library of ADAL.</span><span class="sxs-lookup"><span data-stu-id="b26ed-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="b26ed-107">Enig doel in het leven van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="b26ed-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="b26ed-108">toodemonstrate hoe gemakkelijk het is, hier we je een .NET WPF-takenlijst-toepassing bouwt die:</span><span class="sxs-lookup"><span data-stu-id="b26ed-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="b26ed-109">Krijgt toegang tot tokens voor het aanroepen van hello Azure AD Graph API met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b26ed-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b26ed-110">Zoekt een directory voor gebruikers met een alias voor een gegeven.</span><span class="sxs-lookup"><span data-stu-id="b26ed-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="b26ed-111">Tekenen gebruikers uit.</span><span class="sxs-lookup"><span data-stu-id="b26ed-111">Signs users out.</span></span>

<span data-ttu-id="b26ed-112">toobuild hello volledige werkende toepassing, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="b26ed-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="b26ed-113">Uw toepassing registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b26ed-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="b26ed-114">Installeren en configureren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="b26ed-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="b26ed-115">Gebruik ADAL tooget tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b26ed-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="b26ed-116">tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b26ed-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="b26ed-117">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="b26ed-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="b26ed-118">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b26ed-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="b26ed-119">1. Hallo DirectorySearcher toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="b26ed-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="b26ed-120">tooenable uw app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="b26ed-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="b26ed-121">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b26ed-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b26ed-122">Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b26ed-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="b26ed-123">Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b26ed-124">Klik op **App registraties** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="b26ed-125">Volg de aanwijzingen Hallo en maak een nieuwe **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="b26ed-126">Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers</span><span class="sxs-lookup"><span data-stu-id="b26ed-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="b26ed-127">Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat tooreturn token antwoorden bij Azure AD wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b26ed-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="b26ed-128">Voer een waarde specifieke tooyour toepassing, bijvoorbeeld `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="b26ed-129">Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="b26ed-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="b26ed-130">U moet deze waarde in de volgende secties hello, dus kopiëren van de pagina van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b26ed-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="b26ed-131">Van Hallo **instellingen** pagina **Required Permissions** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="b26ed-132">Selecteer Hallo **Microsoft Graph** als Hallo API en voeg Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="b26ed-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b26ed-133">Hiermee schakelt u uw toepassing tooquery Hallo Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b26ed-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="b26ed-134">2. Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="b26ed-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="b26ed-135">Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="b26ed-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="b26ed-136">Voor ADAL toobe kunnen toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="b26ed-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="b26ed-137">Beginnen met het ADAL toohello DirectorySearcher project met behulp van Hallo Package Manager-Console toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b26ed-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="b26ed-138">Open in Hallo DirectorySearcher project `app.config`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="b26ed-139">Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u hebt de invoer in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="b26ed-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="b26ed-140">Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="b26ed-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b26ed-141">Hallo `ida:Tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="b26ed-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="b26ed-142">Hallo `ida:ClientId` hello clientId van uw toepassing die u hebt gekopieerd uit de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="b26ed-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="b26ed-143">Hallo `ida:RedirectUri` is Hallo omleidings-url die u in de portal Hallo geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="b26ed-144">3.    Gebruik ADAL tooGet Tokens van AAD</span><span class="sxs-lookup"><span data-stu-id="b26ed-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="b26ed-145">Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, aanroept `authContext.AcquireTokenAsync(...)`, en ADAL Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="b26ed-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="b26ed-146">In Hallo `DirectorySearcher` project, open `MainWindow.xaml.cs` en zoek Hallo `MainWindow()` methode.</span><span class="sxs-lookup"><span data-stu-id="b26ed-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="b26ed-147">de eerste stap Hallo tooinitialize van uw app is `AuthenticationContext` -ADAL de primaire klasse.</span><span class="sxs-lookup"><span data-stu-id="b26ed-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="b26ed-148">Dit is waar het doorgeven van ADAL Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="b26ed-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="b26ed-149">Nu zoeken Hallo `Search(...)` methode, die wordt aangeroepen wanneer Hallo gebruiker cliks knop "Zoeken" in de gebruikersinterface van de app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b26ed-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="b26ed-150">Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.</span><span class="sxs-lookup"><span data-stu-id="b26ed-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="b26ed-151">Maar in de volgorde tooquery Hallo Graph API, moet u een access_token in Hallo tooinclude `Authorization` header Hallo-aanvraag: dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="b26ed-152">Wanneer uw app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties.</span><span class="sxs-lookup"><span data-stu-id="b26ed-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="b26ed-153">Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, wordt het weergeven van een dialoogvenster voor aanmelding, Hallo gebruikersreferenties verzamelen en retourneren een token na verificatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="b26ed-154">Als ADAL niet kan tooreturn een token voor een of andere reden is, genereert het een `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="b26ed-155">U ziet dat Hallo `AuthenticationResult` object bevat een `UserInfo` -object dat kan worden gebruikt toocollect informatie uw app mogelijk nodig.</span><span class="sxs-lookup"><span data-stu-id="b26ed-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="b26ed-156">In Hallo DirectorySearcher, `UserInfo` gebruikte toocustomize Hallo gebruikersinterface van de app met de id van gebruiker Hallo is.</span><span class="sxs-lookup"><span data-stu-id="b26ed-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="b26ed-157">Wanneer Hallo gebruiker op de knop 'Afmelden' hello, willen we tooensure die de volgende oproep te Hallo`AcquireTokenAsync(...)` Hallo gebruiker toosign in wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="b26ed-158">Met ADAL, is dit is net zo eenvoudig als het token Hallo-cache wissen:</span><span class="sxs-lookup"><span data-stu-id="b26ed-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="b26ed-159">Als Hallo gebruiker heeft niet op knop 'Afmelden' hello, wilt u echter toomaintain Hallo gebruikerssessie voor Hallo volgende keer dat ze Hallo DirectorySearcher worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="b26ed-160">Wanneer Hallo app opent, kunt u controleren van de ADAL-tokencache voor een bestaande token en Hallo gebruikersinterface worden dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b26ed-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="b26ed-161">In Hallo `CheckForCachedToken()` methode te maken van een andere aanroep van`AcquireTokenAsync(...)`, ditmaal doorgeven in een Hallo `PromptBehavior.Never` parameter.</span><span class="sxs-lookup"><span data-stu-id="b26ed-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="b26ed-162">`PromptBehavior.Never`vertelt ADAL dat Hallo-gebruiker niet moet worden gevraagd voor aanmelding en ADAL moet in plaats daarvan Veroorzaak een exception als het tooreturn niet kan een token.</span><span class="sxs-lookup"><span data-stu-id="b26ed-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
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

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="b26ed-163">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b26ed-163">Congratulations!</span></span> <span data-ttu-id="b26ed-164">U nu beschikken over een werkende .NET WPF-toepassing die Hallo mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="b26ed-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="b26ed-165">Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b26ed-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="b26ed-166">Uitvoeren van uw app DirectorySearcher en meld u aan met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b26ed-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="b26ed-167">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="b26ed-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="b26ed-168">Hallo-app sluiten en voer deze opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="b26ed-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="b26ed-169">U ziet hoe Hallo gebruikerssessie blijft intact.</span><span class="sxs-lookup"><span data-stu-id="b26ed-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="b26ed-170">Meld u af en meld u opnieuw aan als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b26ed-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="b26ed-171">ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b26ed-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="b26ed-172">Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="b26ed-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="b26ed-173">Alles wat u moet tooknow één API-aanroep is `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="b26ed-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="b26ed-174">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is opgegeven [hier](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b26ed-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="b26ed-175">U kunt nu verplaatsen op tooadditional scenario's.</span><span class="sxs-lookup"><span data-stu-id="b26ed-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="b26ed-176">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="b26ed-176">You may want tootry:</span></span>

[<span data-ttu-id="b26ed-177">Een .NET-Web-API met Azure AD beveiligen >></span><span class="sxs-lookup"><span data-stu-id="b26ed-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

