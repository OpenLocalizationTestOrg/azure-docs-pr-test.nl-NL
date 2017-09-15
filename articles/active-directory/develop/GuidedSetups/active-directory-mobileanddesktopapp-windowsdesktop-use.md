---
title: Azure AD v2 Windows Desktop ophalen gestart - gebruiken | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 826ba0a00b26993d4f37f0a8ce587d7bb77e7eb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="6ed51-103">De Microsoft Authentication Library (MSAL) gebruiken voor het ophalen van een token voor de Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="6ed51-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="6ed51-104">Deze sectie wordt beschreven hoe MSAL gebruiken voor een token de Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="6ed51-104">This section shows how to use MSAL to get a token the Microsoft Graph API.</span></span>

1.  <span data-ttu-id="6ed51-105">In `MainWindow.xaml.cs`, voeg de referentie voor MSAL bibliotheek toe aan de klasse:</span><span class="sxs-lookup"><span data-stu-id="6ed51-105">In `MainWindow.xaml.cs`, add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="6ed51-106">Vervang <code>MainWindow</code> code die een klasse:</span><span class="sxs-lookup"><span data-stu-id="6ed51-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set the API Endpoint to Graph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set the scope for API call to user.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - to acquire a token requiring user to sign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need to call AcquireTokenAsync to acquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6ed51-107">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="6ed51-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="6ed51-108">Een token ophalen interactieve</span><span class="sxs-lookup"><span data-stu-id="6ed51-108">Getting a user token interactive</span></span>
<span data-ttu-id="6ed51-109">Het aanroepen van de `AcquireTokenAsync` methode resulteert in een venster vraagt de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="6ed51-109">Calling the `AcquireTokenAsync` method results in a window prompting the user to sign in.</span></span> <span data-ttu-id="6ed51-110">Toepassingen vereisen meestal een gebruiker zich aanmelden interactief de eerste keer dat ze nodig hebben voor toegang tot een beveiligde bron, of wanneer een achtergrond-bewerking te verkrijgen van een token mislukt (bijvoorbeeld van de gebruiker het wachtwoord verlopen).</span><span class="sxs-lookup"><span data-stu-id="6ed51-110">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="6ed51-111">Een gebruiker ophalen achtergrond token</span><span class="sxs-lookup"><span data-stu-id="6ed51-111">Getting a user token silently</span></span>
<span data-ttu-id="6ed51-112">`AcquireTokenSilentAsync`token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6ed51-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="6ed51-113">Na `AcquireTokenAsync` wordt uitgevoerd voor de eerste keer `AcquireTokenSilentAsync` is de gebruikelijke methode gebruikt voor het verkrijgen van tokens die worden gebruikt voor toegang tot beveiligde bronnen voor volgende aanroepen - aanroepen aan te vragen of vernieuwen van tokens op de achtergrond worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="6ed51-113">After `AcquireTokenAsync` is executed for the first time, `AcquireTokenSilentAsync` is the usual method used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="6ed51-114">Uiteindelijk `AcquireTokenSilentAsync` mislukt: bijvoorbeeld de gebruiker heeft zich afgemeld, of het wachtwoord op een ander apparaat is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6ed51-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="6ed51-115">Wanneer MSAL detecteert dat het probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="6ed51-115">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="6ed51-116">Uw toepassing kan verwerken van deze uitzondering op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="6ed51-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="6ed51-117">Een aanroep tegen `AcquireTokenAsync` onmiddellijk, wat ertoe leidt de gebruiker om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="6ed51-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting the user to sign-in.</span></span> <span data-ttu-id="6ed51-118">Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing beschikbaar is voor de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="6ed51-118">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="6ed51-119">Dit patroon maakt gebruik van de steekproef die worden gegenereerd door deze Begeleide instelprocedure: u kunt deze bekijken in actie de eerste keer dat u het voorbeeld uitvoert: omdat er geen gebruiker ooit de toepassing gebruikt `PublicClientApp.Users.FirstOrDefault()` bevat een null-waarde en een `MsalUiRequiredException` uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="6ed51-119">The sample generated by this guided setup uses this pattern: you can see it in action the first time you execute the sample: because no user ever used the application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="6ed51-120">De code in het voorbeeld de uitzondering wordt verwerkt door het aanroepen van `AcquireTokenAsync` waardoor vraagt de gebruiker om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="6ed51-120">The code in the sample then handles the exception by calling `AcquireTokenAsync` resulting in prompting the user to sign-in.</span></span>

2.  <span data-ttu-id="6ed51-121">Toepassingen kunnen ook een visuele indicatie maken voor de gebruiker die een interactief aanmelden is vereist, zodat de gebruiker het juiste moment aan te melden kunt selecteren of de toepassing opnieuw kunt `AcquireTokenSilentAsync` op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="6ed51-121">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="6ed51-122">Dit wordt meestal gebruikt wanneer de gebruiker andere functies van de toepassing gebruiken kunt zonder wordt onderbroken - bijvoorbeeld offline inhoud beschikbaar is in de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="6ed51-122">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="6ed51-123">In dit geval wordt de gebruiker kunt bepalen wanneer ze willen aanmelden voor toegang tot de beveiligde bron, of om de verouderde gegevens te vernieuwen of uw toepassing kunt ervoor kiezen om opnieuw te proberen `AcquireTokenSilentAsync` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="6ed51-123">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="6ed51-124">De Microsoft Graph API met behulp van het token dat u zojuist hebt verkregen aanroepen</span><span class="sxs-lookup"><span data-stu-id="6ed51-124">Call the Microsoft Graph API using the token you just obtained</span></span>

1. <span data-ttu-id="6ed51-125">Toevoegen van de nieuwe methode hieronder uw `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="6ed51-125">Add the new method below to your `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="6ed51-126">De methode wordt gebruikt om een `GET` -aanvraag in voor Graph API met behulp van een autoriseren-header:</span><span class="sxs-lookup"><span data-stu-id="6ed51-126">The method is used to make a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request to a URL using an HTTP Authorization header
/// </summary>
/// <param name="url">The URL</param>
/// <param name="token">The token</param>
/// <returns>String containing the results of the GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add the token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="6ed51-127">Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API</span><span class="sxs-lookup"><span data-stu-id="6ed51-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="6ed51-128">In deze voorbeeldtoepassing de `GetHttpContentWithToken` methode wordt gebruikt voor het maken van een HTTP `GET` aanvragen op basis van een beveiligde bron die is een token vereist en vervolgens de inhoud naar de aanroeper wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6ed51-128">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="6ed51-129">Met deze methode wordt het token verkregen in de *HTTP-autorisatie-header*.</span><span class="sxs-lookup"><span data-stu-id="6ed51-129">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="6ed51-130">Voor dit voorbeeld wordt de resource is de Microsoft Graph API *mij* eindpunt – waarin informatie over het profiel van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6ed51-130">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="6ed51-131">Een methode voor het ondertekenen van de gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ed51-131">Add a method to sign out the user</span></span>

1. <span data-ttu-id="6ed51-132">Voeg de volgende methode voor uw `MainWindow.xaml.cs` afmelden van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="6ed51-132">Add the following method to your `MainWindow.xaml.cs` to sign out the user:</span></span>

```csharp
/// <summary>
/// Sign out the current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="6ed51-133">Meer informatie over afmelden</span><span class="sxs-lookup"><span data-stu-id="6ed51-133">More info on Sign-Out</span></span>

<span data-ttu-id="6ed51-134">`SignOutButton_Click`verwijdert de gebruiker uit MSAL gebruikerscache – dit effectief MSAL laat weten om de huidige gebruiker vergeet, zodat een toekomstige aanvraag voor een token verkrijgen alleen lukt als het gaat interactief zijn.</span><span class="sxs-lookup"><span data-stu-id="6ed51-134">`SignOutButton_Click` removes the user from MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>
<span data-ttu-id="6ed51-135">Hoewel de toepassing in dit voorbeeld een enkele gebruiker ondersteunt, ondersteunt MSAL scenario's waarbij meerdere accounts kunnen worden aangemeld op hetzelfde moment: een voorbeeld is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.</span><span class="sxs-lookup"><span data-stu-id="6ed51-135">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="6ed51-136">Token standaardgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="6ed51-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="6ed51-137">Toevoegen van de volgende methode voor uw `MainWindow.xaml.cs` om algemene informatie over het token weer te geven:</span><span class="sxs-lookup"><span data-stu-id="6ed51-137">Add the following method to to your `MainWindow.xaml.cs` to display basic information about the token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in the token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6ed51-138">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="6ed51-138">More Information</span></span>

<span data-ttu-id="6ed51-139">Tokens die zijn verkregen *OpenID Connect* bevatten ook een kleine subset van de informatie die relevant zijn voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6ed51-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent to the user.</span></span> <span data-ttu-id="6ed51-140">`DisplayBasicTokenInfo`algemene informatie opgenomen in het token wordt weergegeven: bijvoorbeeld de weergavenaam van de gebruiker en-ID, evenals de vervaldatum van token en de toegang tot het type string token zelf.</span><span class="sxs-lookup"><span data-stu-id="6ed51-140">`DisplayBasicTokenInfo` displays basic information contained in the token: for example, the user's display name and ID, as well as the token expiration date and the string representing the access token itself.</span></span> <span data-ttu-id="6ed51-141">Deze informatie wordt weergegeven voor u om te zien.</span><span class="sxs-lookup"><span data-stu-id="6ed51-141">This information is displayed for you to see.</span></span> <span data-ttu-id="6ed51-142">U kunt raakt de *Microsoft Graph-API aanroepen* meerdere keren knop en Zie dat hetzelfde token opnieuw is gebruikt voor volgende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6ed51-142">You can hit the *Call Microsoft Graph API* button multiple times and see that the same token was reused for subsequent requests.</span></span> <span data-ttu-id="6ed51-143">U ziet ook de verloopdatum wordt verlengd wanneer MSAL het beslist is tijd om het token te verlengen.</span><span class="sxs-lookup"><span data-stu-id="6ed51-143">You can also see the expiration date being extended when MSAL decides it is time to renew the token.</span></span>
<!--end-collapse-->

