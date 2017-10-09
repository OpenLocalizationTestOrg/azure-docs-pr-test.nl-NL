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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hallo Microsoft Authentication Library (MSAL) tooget een token voor Hallo Microsoft Graph API gebruiken

Deze sectie wordt beschreven hoe toouse MSAL tooget een token Hallo Microsoft Graph API.

1.  In `MainWindow.xaml.cs`, Hallo-verwijzing voor MSAL bibliotheek toohello klasse toevoegen:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Vervang <code>MainWindow</code> code die een klasse:
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
### <a name="more-information"></a>Meer informatie
#### <a name="getting-a-user-token-interactive"></a>Een token ophalen interactieve
Aanroepen Hallo `AcquireTokenAsync` methode resulteert in een venster waarin wordt gevraagd Hallo toosign van de gebruiker in. Toepassingen zijn doorgaans vereist een gebruiker toosign in interactief Hallo eerste keer dat ze tooaccess moeten een beveiligde bron of wanneer een stille bewerking tooacquire een token mislukt (bijvoorbeeld Hallo gebruikerswachtwoord verlopen).

#### <a name="getting-a-user-token-silently"></a>Een gebruiker ophalen achtergrond token
`AcquireTokenSilentAsync`token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker worden verwerkt. Na `AcquireTokenAsync` wordt uitgevoerd voor Hallo eerst `AcquireTokenSilentAsync` Hallo gebruikelijke methode gebruikt tooobtain tokens die worden gebruikt tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.
Uiteindelijk `AcquireTokenSilentAsync` mislukt: bijvoorbeeld Hallo gebruiker heeft zich afgemeld of het wachtwoord op een ander apparaat is gewijzigd. Wanneer MSAL detecteert dat Hallo probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MsalUiRequiredException`. Uw toepassing kan verwerken van deze uitzondering op twee manieren:

1.  Een aanroep tegen `AcquireTokenAsync` onmiddellijk, wat ertoe leidt Hallo gebruiker toosign in. Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing hello beschikbaar voor Hallo-gebruiker is. Hallo voorbeeld gegenereerd met deze Begeleide installatie maakt gebruik van dit patroon: u kunt deze bekijken in actie Hallo eerste keer dat u Hallo voorbeeld uitvoert: omdat er geen gebruiker ooit toepassing hello gebruikt, `PublicClientApp.Users.FirstOrDefault()` bevat een null-waarde en een `MsalUiRequiredException` uitzondering gegenereerd. code in de steekproef Hallo Hallo vervolgens ingangen Hallo uitzondering door aan te roepen `AcquireTokenAsync` waardoor Hallo gebruiker toosign in.

2.  Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `AcquireTokenSilentAsync` op een later tijdstip. Dit wordt meestal gebruikt wanneer Hallo gebruiker andere functionaliteit van de toepassing hello gebruiken kunt zonder wordt onderbroken - bijvoorbeeld offline-inhoud in de toepassing hello beschikbaar is. In dit geval Hallo-gebruiker kunt bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource, toorefresh Hallo verouderde informatie of uw toepassing kunt bepalen tooretry `AcquireTokenSilentAsync` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen

1. Toevoegen van nieuwe methode Hallo hieronder tooyour `MainWindow.xaml.cs`. Hallo methode is gebruikte toomake een `GET` -aanvraag in voor Graph API met behulp van een autoriseren-header:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API

In deze voorbeeldtoepassing Hallo `GetHttpContentWithToken` methode is gebruikte toomake een HTTP `GET` -aanvraag in voor een beveiligde bron die een token en ga daarna terug Hallo inhoud toohello aanroeper vereist. Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*. Voor dit voorbeeld is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Een methode toosign uit Hallo gebruiker toevoegen

1. Hallo na methode tooyour toevoegen `MainWindow.xaml.cs` toosign uit Hallo gebruiker:

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
### <a name="more-info-on-sign-out"></a>Meer informatie over afmelden

`SignOutButton_Click`Hiermee verwijdert u Hallo gebruiker uit de cache van de gebruiker MSAL – dit MSAL tooforget Hallo huidige gebruiker effectief laat weten zodat een tooacquire toekomstige aanvraag een token alleen slaagt als het gaat toobe interactieve.
Hoewel het Hallo-toepassing in dit voorbeeld ondersteunt een enkele gebruiker, MSAL scenario's waar meerdere accounts aangemeld op Hallo worden kunnen ondersteunt dezelfde tijd: een voorbeeld hiervan is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Token standaardgegevens weergeven

1. Hallo na methode tootooyour toevoegen `MainWindow.xaml.cs` toodisplay basisinformatie over Hallo token:

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
### <a name="more-information"></a>Meer informatie

Tokens die zijn verkregen *OpenID Connect* bevatten ook een kleine subset van de relevante toohello gebruiker. `DisplayBasicTokenInfo`basisinformatie weergeven die zijn opgenomen in Hallo token: bijvoorbeeld Hallo van de gebruiker weergegeven naam en de ID, evenals Hallo token verloopt de datum en het Hallo type string Hallo toegangstoken zelf. Deze informatie wordt weergegeven voor u toosee. U kunt Hallo raakt *Microsoft Graph-API aanroepen* meerdere keren knop en Zie dat hetzelfde token opnieuw voor volgende aanvragen gebruikt werd Hallo. U ziet ook Hallo vervaldatum wanneer MSAL beslist dat het is tijd toorenew Hallo token wordt uitgebreid.
<!--end-collapse-->

