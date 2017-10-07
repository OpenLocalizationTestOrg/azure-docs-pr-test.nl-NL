---
title: aaaAzure Active Directory v2.0 systeemeigen .NET-App | Microsoft Docs
description: Hoe toobuild een systeemeigen .NET-app die zich aanmeldt gebruikers met beide persoonlijke Microsoft-Account en werk- of schoolaccount accounts.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="a7d5b-103">Aanmelden tooa Windows Desktop app toevoegen</span><span class="sxs-lookup"><span data-stu-id="a7d5b-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="a7d5b-104">U kunt snel verificatie tooyour desktop-apps met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccounts met Hallo Hallo v2.0-eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a7d5b-105">Deze ook kan uw app toosecurely communiceren met een back-end web-api, evenals [Microsoft Graph Hallo](https://graph.microsoft.io) en enkele Hallo [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="a7d5b-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="a7d5b-106">Niet alle Azure Active Directory (AD)-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="a7d5b-107">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a7d5b-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="a7d5b-108">Voor [systeemeigen .NET-toepassingen die worden uitgevoerd op een apparaat](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD levert Hallo Microsoft Identity-Verificatiebibliotheek of MSAL.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="a7d5b-109">MSAL van enig doel in leven is toomake gemakkelijk voor uw app tooget tokens voor het aanroepen van webservices.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="a7d5b-110">toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een .NET WPF-takenlijst-app die:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="a7d5b-111">Tekenen Hallo gebruiker in & krijgt toegang tot tokens met Hallo [OAuth 2.0-verificatieprotocol](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a7d5b-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="a7d5b-112">Veilig een back-end takenlijst-webservice, die ook is beveiligd met OAuth 2.0-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="a7d5b-113">Hallo-gebruiker meldt zich uit.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="a7d5b-114">Voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="a7d5b-114">Download sample code</span></span>
<span data-ttu-id="a7d5b-115">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a7d5b-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="a7d5b-116">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="a7d5b-117">Hallo voltooid app wordt op Hallo einde van deze zelfstudie ook aangeboden.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="a7d5b-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="a7d5b-118">Register an app</span></span>
<span data-ttu-id="a7d5b-119">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a7d5b-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a7d5b-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-120">Make sure to:</span></span>

* <span data-ttu-id="a7d5b-121">Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="a7d5b-122">Hallo toevoegen **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="a7d5b-123">Installeren en configureren van MSAL</span><span class="sxs-lookup"><span data-stu-id="a7d5b-123">Install & Configure MSAL</span></span>
<span data-ttu-id="a7d5b-124">Nu dat u een app geregistreerd bij Microsoft hebt, kunt u MSAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="a7d5b-125">Voor MSAL toobe kunnen toocommunicate Hallo v2.0-eindpunt, moet u tooprovide met enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="a7d5b-126">Beginnen met het MSAL toohello TodoListClient project met behulp van Hallo Package Manager-Console toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="a7d5b-127">Open in Hallo TodoListClient project `app.config`.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="a7d5b-128">Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u hebt invoer in de portal voor wachtwoordregistratie Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="a7d5b-129">Uw code zal naar deze waarden verwijzen wanneer MSAL wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="a7d5b-130">Hallo `ida:ClientId` Hallo is **toepassings-Id** van uw app die u hebt gekopieerd uit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="a7d5b-131">Open in Hallo TodoList-Service-project `web.config` in Hallo hoofdmap van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="a7d5b-132">Vervang Hallo `ida:Audience` waarde Hello dezelfde **toepassings-Id** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="a7d5b-133">Gebruik MSAL tooget tokens</span><span class="sxs-lookup"><span data-stu-id="a7d5b-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="a7d5b-134">Hallo basisprincipe achter MSAL is dat wanneer uw app een toegangstoken moet, u gewoon belt `app.AcquireToken(...)`, en MSAL Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="a7d5b-135">In Hallo `TodoListClient` project, open `MainWindow.xaml.cs` en zoek Hallo `OnInitialized(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="a7d5b-136">de eerste stap Hallo tooinitialize van uw app is `PublicClientApplication` -MSAL van primaire klasse die systeemeigen toepassingen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="a7d5b-137">Dit is waar u MSAL doorgeven Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="a7d5b-138">Wanneer u Hallo app start, we toocheck wilt en Zie als Hallo gebruiker al in Hallo app is ondertekend.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="a7d5b-139">Maar we tooinvoke een gebruikersinterface aanmeldingspagina nu nog niet willen - maken we Hallo gebruiker dus klikt u op 'Aanmelden' toodo.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="a7d5b-140">Ook in Hallo `OnInitialized(...)` methode:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="a7d5b-141">Als Hallo gebruiker niet is aangemeld en ze op knop 'Aanmelden' hello, we wilt tooinvoke een UI-aanmelding en hebben Hallo-gebruikers hun referenties invoeren.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="a7d5b-142">Hallo aanmelden knop handler implementeren:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="a7d5b-143">Als Hallo gebruiker heeft zich aanmeldt, MSAL ontvangt en een token voor u in de cache en u kunt verdergaan toocall hello `GetTodoList()` methode met vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="a7d5b-144">Alles wat tooget taken van een gebruiker heeft verlaten tooimplement Hallo is `GetTodoList()` methode.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="a7d5b-145">Voer</span><span class="sxs-lookup"><span data-stu-id="a7d5b-145">Run</span></span>
<span data-ttu-id="a7d5b-146">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-146">Congratulations!</span></span> <span data-ttu-id="a7d5b-147">U hebt nu een werkende .NET WPF-app met Hallo mogelijkheid tooauthenticate gebruikers & veilig aanroepen van Web-API's met behulp van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="a7d5b-148">Voer beide projecten uit en meld u aan met een persoonlijk Microsoft-account of een account voor werk of school.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="a7d5b-149">Takenlijst taken toothat gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="a7d5b-150">Meld u af en meld u opnieuw aan als een andere gebruiker tooview hun takenlijst.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="a7d5b-151">Hallo-app sluiten en voer deze opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="a7d5b-152">U ziet hoe Hallo gebruikerssessie blijft intact - namelijk Hallo app tokens in een lokaal bestand in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="a7d5b-153">MSAL maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in uw app met behulp van zowel privé- als -accounts.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="a7d5b-154">Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="a7d5b-155">Alles wat u moet tooknow één API-aanroep is `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="a7d5b-156">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="a7d5b-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7d5b-157">Next steps</span></span>
<span data-ttu-id="a7d5b-158">U kunt nu verplaatsen naar geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="a7d5b-159">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-159">You may want tootry:</span></span>

* [<span data-ttu-id="a7d5b-160">Hallo TodoListService Web-API met Hallo v2.0-eindpunt beveiligen</span><span class="sxs-lookup"><span data-stu-id="a7d5b-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="a7d5b-161">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="a7d5b-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="a7d5b-162">Hallo v2.0 ontwikkelaarshandleiding >></span><span class="sxs-lookup"><span data-stu-id="a7d5b-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a7d5b-163">StackOverflow 'msal' tag >></span><span class="sxs-lookup"><span data-stu-id="a7d5b-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a7d5b-164">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="a7d5b-164">Get security updates for our products</span></span>
<span data-ttu-id="a7d5b-165">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="a7d5b-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

