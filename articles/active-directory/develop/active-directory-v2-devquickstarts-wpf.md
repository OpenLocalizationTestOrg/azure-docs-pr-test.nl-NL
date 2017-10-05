---
title: Azure Active Directory v2.0 .NET systeemeigen App | Microsoft Docs
description: Het bouwen van een systeemeigen .NET-app die gebruikers met beide persoonlijke Microsoft-Account en werk-of schoolaccounts ondertekent.
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
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="0c7a7-103">Aanmelden toevoegen aan een Windows-bureaublad-app</span><span class="sxs-lookup"><span data-stu-id="0c7a7-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="0c7a7-104">Met het v2.0-eindpunt kunt u snel verificatie op uw bureaublad apps met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="0c7a7-105">Bovendien kunnen uw app zodat deze veilig te communiceren met een back-end web-api, evenals [Microsoft Graph](https://graph.microsoft.io) en enkele van de [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="0c7a7-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="0c7a7-106">Niet alle Azure Active Directory (AD)-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="0c7a7-107">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0c7a7-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="0c7a7-108">Voor [systeemeigen .NET-toepassingen die worden uitgevoerd op een apparaat](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD levert de Verificatiebibliotheek van Microsoft Identity of MSAL.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="0c7a7-109">MSAL van enig doel in leven is gemakkelijker voor uw app om op te halen van tokens voor het aanroepen van webservices.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="0c7a7-110">Om te demonstreren hoe eenvoudig het is, je hier we bouwt u een .NET WPF-takenlijst-app die:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="0c7a7-111">De gebruiker zich aanmeldt & opgehaald tokens met toegang tot de [OAuth 2.0-verificatieprotocol](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="0c7a7-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="0c7a7-112">Veilig een back-end takenlijst-webservice, die ook is beveiligd met OAuth 2.0-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="0c7a7-113">De gebruiker zich afmeldt.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="0c7a7-114">Voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="0c7a7-114">Download sample code</span></span>
<span data-ttu-id="0c7a7-115">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="0c7a7-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="0c7a7-116">Als u wilt volgen, kunt u [basis van de app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="0c7a7-117">De voltooide app is verstrekt aan het einde van deze zelfstudie ook.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="0c7a7-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="0c7a7-118">Register an app</span></span>
<span data-ttu-id="0c7a7-119">Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="0c7a7-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="0c7a7-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-120">Make sure to:</span></span>

* <span data-ttu-id="0c7a7-121">Noteer de **toepassings-Id** toegewezen aan uw app, moet u deze snel.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="0c7a7-122">Voeg de **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="0c7a7-123">Installeren en configureren van MSAL</span><span class="sxs-lookup"><span data-stu-id="0c7a7-123">Install & Configure MSAL</span></span>
<span data-ttu-id="0c7a7-124">Nu dat u een app geregistreerd bij Microsoft hebt, kunt u MSAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="0c7a7-125">In de volgorde voor MSAL naar het v2.0-eindpunt te communiceren, moet u voorzien enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="0c7a7-126">Beginnen met het MSAL toevoegen aan het TodoListClient-project met de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="0c7a7-127">Open in het project TodoListClient `app.config`.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="0c7a7-128">Vervang de waarden van de elementen in de `<appSettings>` sectie in overeenstemming met de waarden die u in de portal van de registratie van de app hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="0c7a7-129">Uw code zal naar deze waarden verwijzen wanneer MSAL wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="0c7a7-130">De `ida:ClientId` is de **toepassings-Id** van uw app die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="0c7a7-131">Open in het project TodoList-Service `web.config` in de hoofdmap van het project.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="0c7a7-132">Vervang de `ida:Audience` waarde met dezelfde **toepassings-Id** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="0c7a7-133">Gebruik MSAL tokens ophalen</span><span class="sxs-lookup"><span data-stu-id="0c7a7-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="0c7a7-134">Het basisprincipe achter MSAL is dat wanneer uw app een toegangstoken moet, u gewoon belt `app.AcquireToken(...)`, en MSAL doet de rest.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="0c7a7-135">In de `TodoListClient` project, open `MainWindow.xaml.cs` en zoek de `OnInitialized(...)` methode.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="0c7a7-136">De eerste stap is het initialiseren van uw app `PublicClientApplication` -MSAL van primaire klasse die systeemeigen toepassingen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="0c7a7-137">Dit is waar u MSAL de coördinaten die voor de communicatie met Azure AD en hoe deze tokens in de cache moet doorgeven.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="0c7a7-138">Wanneer de app wordt gestart, die we willen te zien als de gebruiker al in de app is ondertekend.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="0c7a7-139">Echter niet willen we nu nog een gebruikersinterface aanmelden invoke - maken we de gebruiker klikt u op 'Aanmelden' om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="0c7a7-140">Ook in de `OnInitialized(...)` methode:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
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

* <span data-ttu-id="0c7a7-141">Als de gebruiker niet is aangemeld en ze op de knop 'Aanmelden', die we willen aanroepen van een UI-aanmelding en hebben de gebruikers hun referenties invoeren.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="0c7a7-142">De knop aanmelden handler implementeren:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

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
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
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

* <span data-ttu-id="0c7a7-143">Als de gebruiker heeft zich aanmeldt, MSAL ontvangt en een token voor u in de cache en kunt u doorgaan om aan te roepen de `GetTodoList()` methode met vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="0c7a7-144">Alle die altijd ingeschakeld als u de taken van een gebruiker is het implementeren van de `GetTodoList()` methode.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

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

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

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

## <a name="run"></a><span data-ttu-id="0c7a7-145">Voer</span><span class="sxs-lookup"><span data-stu-id="0c7a7-145">Run</span></span>
<span data-ttu-id="0c7a7-146">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-146">Congratulations!</span></span> <span data-ttu-id="0c7a7-147">U hebt nu een werkende .NET WPF-app met de mogelijkheid om te verifiëren van gebruikers & veilig aanroepen van Web-API's met behulp van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="0c7a7-148">Voer beide projecten uit en meld u aan met een persoonlijk Microsoft-account of een account voor werk of school.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="0c7a7-149">Taken toevoegen aan de takenlijst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="0c7a7-150">Meld u af en meld u opnieuw aan als een andere gebruiker om hun takenlijst weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="0c7a7-151">Sluit de app en voer deze opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="0c7a7-152">U ziet hoe de gebruikerssessie blijft intact - gebeurt dit omdat de app in de cache opgeslagen tokens in een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="0c7a7-153">MSAL gemakkelijk veelvoorkomende identiteit functies opnemen in uw app met behulp van zowel privé- als -accounts.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="0c7a7-154">Dit zorgt voor al het werk dirty voor u - Cachebeheer, OAuth-protocolondersteuning, dat de gebruiker een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="0c7a7-155">Alles wat u moet weten één API-aanroep is `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="0c7a7-156">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="0c7a7-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c7a7-157">Next steps</span></span>
<span data-ttu-id="0c7a7-158">U kunt nu verplaatsen naar geavanceerdere onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="0c7a7-159">U wilt proberen:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-159">You may want to try:</span></span>

* [<span data-ttu-id="0c7a7-160">Beveiliging van de Web-API TodoListService met het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="0c7a7-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="0c7a7-161">Voor aanvullende bronnen voor uitchecken:</span><span class="sxs-lookup"><span data-stu-id="0c7a7-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="0c7a7-162">De ontwikkelaarshandleiding v2.0 >></span><span class="sxs-lookup"><span data-stu-id="0c7a7-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="0c7a7-163">StackOverflow 'msal' tag >></span><span class="sxs-lookup"><span data-stu-id="0c7a7-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="0c7a7-164">Beveiligingsupdates voor onze producten downloaden</span><span class="sxs-lookup"><span data-stu-id="0c7a7-164">Get security updates for our products</span></span>
<span data-ttu-id="0c7a7-165">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="0c7a7-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

