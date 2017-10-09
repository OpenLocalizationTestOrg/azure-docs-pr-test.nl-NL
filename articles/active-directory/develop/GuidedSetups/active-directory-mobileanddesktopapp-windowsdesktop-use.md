---
title: aaaAzure AD v2 Windows Desktop aan de slag - gebruik | Microsoft Docs
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
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="8bfd8-103">Hallo Microsoft Authentication Library (MSAL) tooget een token voor Hallo Microsoft Graph API gebruiken</span><span class="sxs-lookup"><span data-stu-id="8bfd8-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="8bfd8-104">Deze sectie wordt beschreven hoe toouse MSAL tooget een token Hallo Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="8bfd8-105">In `MainWindow.xaml.cs`, Hallo-verwijzing voor MSAL bibliotheek toohello klasse toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="8bfd8-106">Vervang <code>MainWindow</code> code die een klasse:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
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
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
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
### <a name="more-information"></a><span data-ttu-id="8bfd8-107">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="8bfd8-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="8bfd8-108">Een token ophalen interactieve</span><span class="sxs-lookup"><span data-stu-id="8bfd8-108">Getting a user token interactive</span></span>
<span data-ttu-id="8bfd8-109">Aanroepen Hallo `AcquireTokenAsync` methode resulteert in een venster waarin wordt gevraagd Hallo toosign van de gebruiker in.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="8bfd8-110">Toepassingen zijn doorgaans vereist een gebruiker toosign in interactief Hallo eerste keer dat ze tooaccess moeten een beveiligde bron of wanneer een stille bewerking tooacquire een token mislukt (bijvoorbeeld Hallo gebruikerswachtwoord verlopen).</span><span class="sxs-lookup"><span data-stu-id="8bfd8-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="8bfd8-111">Een gebruiker ophalen achtergrond token</span><span class="sxs-lookup"><span data-stu-id="8bfd8-111">Getting a user token silently</span></span>
<span data-ttu-id="8bfd8-112">`AcquireTokenSilentAsync`token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="8bfd8-113">Na `AcquireTokenAsync` wordt uitgevoerd voor Hallo eerst `AcquireTokenSilentAsync` Hallo gebruikelijke methode gebruikt tooobtain tokens die worden gebruikt tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="8bfd8-114">Uiteindelijk `AcquireTokenSilentAsync` mislukt: bijvoorbeeld Hallo gebruiker heeft zich afgemeld of het wachtwoord op een ander apparaat is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="8bfd8-115">Wanneer MSAL detecteert dat Hallo probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="8bfd8-116">Uw toepassing kan verwerken van deze uitzondering op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="8bfd8-117">Een aanroep tegen `AcquireTokenAsync` onmiddellijk, wat ertoe leidt Hallo gebruiker toosign in.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="8bfd8-118">Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing hello beschikbaar voor Hallo-gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="8bfd8-119">Hallo voorbeeld gegenereerd met deze Begeleide installatie maakt gebruik van dit patroon: u kunt deze bekijken in actie Hallo eerste keer dat u Hallo voorbeeld uitvoert: omdat er geen gebruiker ooit toepassing hello gebruikt, `PublicClientApp.Users.FirstOrDefault()` bevat een null-waarde en een `MsalUiRequiredException` uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="8bfd8-120">code in de steekproef Hallo Hallo vervolgens ingangen Hallo uitzondering door aan te roepen `AcquireTokenAsync` waardoor Hallo gebruiker toosign in.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="8bfd8-121">Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `AcquireTokenSilentAsync` op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="8bfd8-122">Dit wordt meestal gebruikt wanneer Hallo gebruiker andere functionaliteit van de toepassing hello gebruiken kunt zonder wordt onderbroken - bijvoorbeeld offline-inhoud in de toepassing hello beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="8bfd8-123">In dit geval Hallo-gebruiker kunt bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource, toorefresh Hallo verouderde informatie of uw toepassing kunt bepalen tooretry `AcquireTokenSilentAsync` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="8bfd8-124">Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen</span><span class="sxs-lookup"><span data-stu-id="8bfd8-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="8bfd8-125">Toevoegen van nieuwe methode Hallo hieronder tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="8bfd8-126">Hallo methode is gebruikte toomake een `GET` -aanvraag in voor Graph API met behulp van een autoriseren-header:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="8bfd8-127">Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API</span><span class="sxs-lookup"><span data-stu-id="8bfd8-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="8bfd8-128">In deze voorbeeldtoepassing Hallo `GetHttpContentWithToken` methode is gebruikte toomake een HTTP `GET` -aanvraag in voor een beveiligde bron die een token en ga daarna terug Hallo inhoud toohello aanroeper vereist.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="8bfd8-129">Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="8bfd8-130">Voor dit voorbeeld is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="8bfd8-131">Een methode toosign uit Hallo gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="8bfd8-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="8bfd8-132">Hallo na methode tooyour toevoegen `MainWindow.xaml.cs` toosign uit Hallo gebruiker:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="8bfd8-133">Meer informatie over afmelden</span><span class="sxs-lookup"><span data-stu-id="8bfd8-133">More info on Sign-Out</span></span>

<span data-ttu-id="8bfd8-134">`SignOutButton_Click`Hiermee verwijdert u Hallo gebruiker uit de cache van de gebruiker MSAL – dit MSAL tooforget Hallo huidige gebruiker effectief laat weten zodat een tooacquire toekomstige aanvraag een token alleen slaagt als het gaat toobe interactieve.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="8bfd8-135">Hoewel het Hallo-toepassing in dit voorbeeld ondersteunt een enkele gebruiker, MSAL scenario's waar meerdere accounts aangemeld op Hallo worden kunnen ondersteunt dezelfde tijd: een voorbeeld hiervan is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="8bfd8-136">Token standaardgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="8bfd8-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="8bfd8-137">Hallo na methode tootooyour toevoegen `MainWindow.xaml.cs` toodisplay basisinformatie over Hallo token:</span><span class="sxs-lookup"><span data-stu-id="8bfd8-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
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
### <a name="more-information"></a><span data-ttu-id="8bfd8-138">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="8bfd8-138">More Information</span></span>

<span data-ttu-id="8bfd8-139">Tokens die zijn verkregen *OpenID Connect* bevatten ook een kleine subset van de relevante toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="8bfd8-140">`DisplayBasicTokenInfo`basisinformatie weergeven die zijn opgenomen in Hallo token: bijvoorbeeld Hallo van de gebruiker weergegeven naam en de ID, evenals Hallo token verloopt de datum en het Hallo type string Hallo toegangstoken zelf.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="8bfd8-141">Deze informatie wordt weergegeven voor u toosee.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="8bfd8-142">U kunt Hallo raakt *Microsoft Graph-API aanroepen* meerdere keren knop en Zie dat hetzelfde token opnieuw voor volgende aanvragen gebruikt werd Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="8bfd8-143">U ziet ook Hallo vervaldatum wanneer MSAL beslist dat het is tijd toorenew Hallo token wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="8bfd8-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

