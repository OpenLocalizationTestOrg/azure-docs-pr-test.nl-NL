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
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Aanmelden tooa Windows Desktop app toevoegen
U kunt snel verificatie tooyour desktop-apps met ondersteuning voor beide persoonlijke Microsoft-accounts en werk-of schoolaccounts met Hallo Hallo v2.0-eindpunt toevoegen.  Deze ook kan uw app toosecurely communiceren met een back-end web-api, evenals [Microsoft Graph Hallo](https://graph.microsoft.io) en enkele Hallo [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Niet alle Azure Active Directory (AD)-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

Voor [systeemeigen .NET-toepassingen die worden uitgevoerd op een apparaat](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD levert Hallo Microsoft Identity-Verificatiebibliotheek of MSAL.  MSAL van enig doel in leven is toomake gemakkelijk voor uw app tooget tokens voor het aanroepen van webservices.  toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een .NET WPF-takenlijst-app die:

* Tekenen Hallo gebruiker in & krijgt toegang tot tokens met Hallo [OAuth 2.0-verificatieprotocol](active-directory-v2-protocols.md).
* Veilig een back-end takenlijst-webservice, die ook is beveiligd met OAuth 2.0-aanroepen.
* Hallo-gebruiker meldt zich uit.

## <a name="download-sample-code"></a>Voorbeeldcode downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

Hallo voltooid app wordt op Hallo einde van deze zelfstudie ook aangeboden.

## <a name="register-an-app"></a>Een app registreren
Maakt een nieuwe app op [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of als volgt [gedetailleerde stappen](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Noteer Hallo **toepassings-Id** toegewezen tooyour app, moet u deze snel.
* Hallo toevoegen **Mobile** platform voor uw app.

## <a name="install--configure-msal"></a>Installeren en configureren van MSAL
Nu dat u een app geregistreerd bij Microsoft hebt, kunt u MSAL installeert en uw identiteitsgerelateerde code schrijven.  Voor MSAL toobe kunnen toocommunicate Hallo v2.0-eindpunt, moet u tooprovide met enige informatie over de registratie van uw app.

* Beginnen met het MSAL toohello TodoListClient project met behulp van Hallo Package Manager-Console toe te voegen.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* Open in Hallo TodoListClient project `app.config`.  Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u hebt invoer in de portal voor wachtwoordregistratie Hallo-app.  Uw code zal naar deze waarden verwijzen wanneer MSAL wordt gebruikt.
  
  * Hallo `ida:ClientId` Hallo is **toepassings-Id** van uw app die u hebt gekopieerd uit Hallo-portal.
* Open in Hallo TodoList-Service-project `web.config` in Hallo hoofdmap van Hallo-project.  
  
  * Vervang Hallo `ida:Audience` waarde Hello dezelfde **toepassings-Id** van Hallo-portal.

## <a name="use-msal-tooget-tokens"></a>Gebruik MSAL tooget tokens
Hallo basisprincipe achter MSAL is dat wanneer uw app een toegangstoken moet, u gewoon belt `app.AcquireToken(...)`, en MSAL Hallo rest.  

* In Hallo `TodoListClient` project, open `MainWindow.xaml.cs` en zoek Hallo `OnInitialized(...)` methode.  de eerste stap Hallo tooinitialize van uw app is `PublicClientApplication` -MSAL van primaire klasse die systeemeigen toepassingen vertegenwoordigt.  Dit is waar u MSAL doorgeven Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Wanneer u Hallo app start, we toocheck wilt en Zie als Hallo gebruiker al in Hallo app is ondertekend.  Maar we tooinvoke een gebruikersinterface aanmeldingspagina nu nog niet willen - maken we Hallo gebruiker dus klikt u op 'Aanmelden' toodo.  Ook in Hallo `OnInitialized(...)` methode:

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

* Als Hallo gebruiker niet is aangemeld en ze op knop 'Aanmelden' hello, we wilt tooinvoke een UI-aanmelding en hebben Hallo-gebruikers hun referenties invoeren.  Hallo aanmelden knop handler implementeren:

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

* Als Hallo gebruiker heeft zich aanmeldt, MSAL ontvangt en een token voor u in de cache en u kunt verdergaan toocall hello `GetTodoList()` methode met vertrouwen.  Alles wat tooget taken van een gebruiker heeft verlaten tooimplement Hallo is `GetTodoList()` methode.

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

## <a name="run"></a>Voer
Gefeliciteerd. U hebt nu een werkende .NET WPF-app met Hallo mogelijkheid tooauthenticate gebruikers & veilig aanroepen van Web-API's met behulp van OAuth 2.0.  Voer beide projecten uit en meld u aan met een persoonlijk Microsoft-account of een account voor werk of school.  Takenlijst taken toothat gebruiker toevoegen.  Meld u af en meld u opnieuw aan als een andere gebruiker tooview hun takenlijst.  Hallo-app sluiten en voer deze opnieuw uit.  U ziet hoe Hallo gebruikerssessie blijft intact - namelijk Hallo app tokens in een lokaal bestand in de cache opslaat.

MSAL maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in uw app met behulp van zowel privé- als -accounts.  Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.  Alles wat u moet tooknow één API-aanroep is `app.AcquireTokenAsync(...)`.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Volgende stappen
U kunt nu verplaatsen naar geavanceerdere onderwerpen.  U kunt tootry:

* [Hallo TodoListService Web-API met Hallo v2.0-eindpunt beveiligen](active-directory-v2-devquickstarts-dotnet-api.md)

Voor aanvullende bronnen voor uitchecken:  

* [Hallo v2.0 ontwikkelaarshandleiding >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow 'msal' tag >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Beveiligingsupdates voor onze producten downloaden
We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

