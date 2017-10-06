---
title: aaaAzure Active Directory B2C | Microsoft Docs
description: Hoe toobuild een Windows-bureaubladtoepassingen die bevat aanmelding, registratie en beheer met behulp van Azure Active Directory B2C-profiel.
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: Een Windows desktop app bouwen
U kunt met behulp van Azure Active Directory (Azure AD) B2C bureaublad tooyour-app van de krachtige Self-service identiteitsbeheer management-functies toevoegen in slechts enkele korte stappen. In dit artikel wordt uitgelegd hoe u toocreate een 'Takenlijst'.NET Windows Presentation Foundation (WPF)-app die gebruikersregistratie, aanmelding en Profielbeheer bevat. Hallo-app biedt ondersteuning voor zich kunnen registreren en aanmelden met een gebruikersnaam of e-mailbericht. Het biedt ook ondersteuning voor zich kunnen registreren en aanmelden via sociale accounts zoals Facebook en Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken
Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.  Een directory is een container voor alle gebruikers, apps, groepen en meer. Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u doorgaat in deze handleiding.

## <a name="create-an-application"></a>Een app maken
Vervolgens moet u een app toocreate in uw B2C-directory. Hiermee geeft u Azure AD-informatie of deze behoeften toosecurely met uw app communiceren. toocreate een app, volg [deze instructies](active-directory-b2c-app-registration.md).  Zorg ervoor dat:

* Omvatten een **native client** in Hallo-toepassing.
* Kopiëren Hallo **omleidings-URI** `urn:ietf:wg:oauth:2.0:oob`. Het is Hallo-standaard-URL voor dit codevoorbeeld.
* Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. U hebt dit later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken
In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Dit codevoorbeeld bevat drie identiteitservaringen: registreren, aanmelden en profiel bewerken. U moet toocreate een beleid voor elk type, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Wanneer u Hallo drie beleidsregels maakt, moet u:

* Kies een **gebruikers-ID registreren** of **registratie via E-mail** in de blade met identiteitsproviders Hallo.
* Kiest u **Weergavenaam** en andere registratiekenmerken in het registratiebeleid.
* Kiest u **Weergavenaam**- en **Object-id**-claims als toepassingsclaims voor elk beleid. U kunt ook andere claims kiezen.
* Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt. Het voorvoegsel Hallo heeft `b2c_1_`.  U hebt deze beleidsnamen later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u hebt gemaakt Hallo drie beleidsregels, bent u klaar toobuild uw app.

## <a name="download-hello-code"></a>Hallo code downloaden
code voor deze zelfstudie Hallo [wordt bewaard in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). toobuild hello voorbeeld als u gaat, kunt u [een basisproject downloaden als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). U kunt Hallo basisproject ook klonen:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

Hallo voltooid app is ook [beschikbaar als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) of op Hallo `complete` vertakking van Hallo dezelfde opslagplaats.

Nadat u Hallo voorbeeldcode hebt gedownload, open Hallo Visual Studio .sln-bestand tooget is gestart. Hallo `TaskClient` project is Hallo WPF-bureaubladtoepassing die gebruiker Hallo communiceert met. Aangeroepen voor Hallo toepassing van deze zelfstudie wordt een taak back-end-web-API, gehost in Azure die de takenlijst van elke gebruiker opslaat.  U hoeft geen toobuild Hallo web-API, we hebben al actief voor u.

toolearn hoe aanvragen voor een web-API veilig verifieert met behulp van Azure AD B2C, bekijk de [web-API aan de slag artikel](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Uitvoeren van beleid
Uw app communiceert met Azure AD B2C door te sturen verificatieberichten die ze willen tooexecute als onderdeel van Hallo HTTP-aanvraag Hallo het beleid opgeven. Voor .NET-desktoptoepassingen, kunt u Hallo Microsoft Authentication Library (MSAL) toosend OAuth 2.0-verificatieberichten bekijken, beleid uitvoeren en tokens verkrijgen voor de web-API's van deze aanroep.

### <a name="install-msal"></a>MSAL installeren
Toevoegen van MSAL toohello `TaskClient` project met behulp van Hallo Visual Studio Package Manager-Console.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Uw B2C-gegevens invoeren
Open Hallo bestand `Globals.cs` en elk Hallo eigenschapswaarden vervangen door uw eigen. Deze klasse wordt gebruikt in `TaskClient` tooreference gebruikte waarden.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Hallo PublicClientApplication maken
de primaire klasse Hallo van MSAL is `PublicClientApplication`. Deze klasse vertegenwoordigt de toepassing in Azure AD B2C Hallo-systeem. Wanneer hello app initalizes, maak een instantie van `PublicClientApplication` in `MainWindow.xaml.cs`. Dit kan worden gebruikt in de gehele Hallo-venster.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Een registratie stroom initiëren
Wanneer een gebruiker toosigns up kiest, wilt u tooinitiate een aanmelding stroom die gebruikmaakt van Hallo registratiebeleid die u hebt gemaakt. Met behulp van MSAL die u zojuist hebt aanroepen `pca.AcquireTokenAsync(...)`. parameters die u te doorgeeft Hallo`AcquireTokenAsync(...)` bepalen welk token wordt weergegeven, Hallo-beleid gebruikt in de verificatieaanvraag Hallo en meer.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a>Starten van een stroom aanmelden
U kunt een stroom aanmelden in Hallo starten dezelfde manier als dat u een aanmelding stroom initiëren. Wanneer een gebruiker zich aanmeldt, moet dezelfde Hallo aanroepen tooMSAL, ditmaal met behulp van uw beleid voor aanmelden:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Starten van een stroom profiel bewerken
Opnieuw uitvoeren van een beleid voor het profiel bewerken in Hallo dezelfde manier:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

In al deze gevallen retourneert MSAL ofwel een token in `AuthenticationResult` of er een uitzondering gegenereerd. Telkens wanneer u een token via MSAL krijgen, kunt u Hallo `AuthenticationResult.User` tooupdate Hallo gebruikersgegevens in Hallo-app, zoals Hallo UI-object. ADAL ook caches Hallo token voor gebruik in andere gedeelten van de toepassing hello.

### <a name="check-for-tokens-on-app-start"></a>Controleer voor tokens op app starten
U kunt ook MSAL tookeep bijhouden van Hallo aanmelden gebruikersstatus gebruiken.  In deze app willen we Hallo gebruiker tooremain aangemeld nadat ze Hallo-app sluiten en opnieuw openen.  Terug in Hallo `OnInitialized` overschrijven, gebruikt u de MSAL `AcquireTokenSilent` methode toocheck voor tokens in de cache:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a>Hallo taak API aanroepen
U hebt nu MSAL tooexecute beleidsregels gebruikt en tokens verkrijgen.  Wanneer u toouse een deze tokens toocall Hallo taak API wilt, kunt u opnieuw gebruiken van MSAL `AcquireTokenSilent` methode toocheck voor tokens in de cache:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

Wanneer de aanroep te Hallo`AcquireTokenSilentAsync(...)` is gelukt en een token gevonden in cache hello, kunt u Hallo token toohello toevoegen `Authorization` koptekst van Hallo HTTP-aanvraag. Hallo taak web-API gebruikt deze header tooauthenticate Hallo aanvraag tooread Hallo de takenlijst gebruiker:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Meld u Hallo gebruiker af
Ten slotte kunt u MSAL tooend een gebruikerssessie met Hallo app wanneer de gebruiker Hallo selecteert **Afmelden**.  Wanneer u MSAL gebruikt, wordt dit wordt bereikt door het wissen van alle Hallo tokens van Hallo tokencache:

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Hallo voorbeeld-app uitvoeren
Ten slotte bouwen en uitvoeren van Hallo-voorbeeld.  Zich registreren voor Hallo-app met behulp van de naam van een e-adres of de gebruiker. Meld u af en meld u weer aan als Hallo dezelfde gebruiker. Profiel van de gebruiker bewerken. Meld u af en meld u aan met behulp van een andere gebruiker.

## <a name="add-social-idps"></a>Sociale IDPs toevoegen
Op dit moment Hallo app ondersteunt alleen gebruiker registreren en aanmelden met **lokale accounts**. Dit zijn opgeslagen in uw B2C-directory accounts die gebruikmaken van een gebruikersnaam en wachtwoord. U kunt met behulp van Azure AD B2C, ondersteuning voor andere id-providers (IDPs) toevoegen zonder uw code.

tooadd sociale IDPs tooyour app volg eerst Hallo gedetailleerde instructies in deze artikelen. Voor elke IDP gewenste toosupport, u moet een toepassing tooregister in dat systeem en verkrijgen van een client-ID.

* [Facebook ingesteld als een IDP](active-directory-b2c-setup-fb-app.md)
* [Google ingesteld als een IDP](active-directory-b2c-setup-goog-app.md)
* [Amazon ingesteld als een IDP](active-directory-b2c-setup-amzn-app.md)
* [LinkedIn instellen als een IDP](active-directory-b2c-setup-li-app.md)

Nadat u Hallo identiteit providers tooyour B2C-directory toevoegt, moet u elk van de drie beleidsregels tooinclude Hallo nieuwe IDPs als in Hallo beschreven tooedit [naslagartikel](active-directory-b2c-reference-policies.md). Nadat u uw beleid opslaat, Voer u Hallo app opnieuw. U ziet Hallo die nieuwe IDPs als opties voor aanmelden en registreren in elk van uw identiteitservaringen toegevoegd.

U kunt experimenteren met het beleid en observeren Hallo gevolgen voor uw voorbeeld-app. Toevoegen of verwijderen van IDPs, toepassingsclaims bewerken of registratiekenmerken wijzigen. Experiment totdat u kunt zien hoe beleidsregels, verificatieaanvragen en MSAL met elkaar verbinden.

Ter referentie: voltooid Hallo voorbeeld [wordt geleverd als ZIP-bestand](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). U kunt dit ook klonen van GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
