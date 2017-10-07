---
title: aaaAzure AD Xamarin aan de slag | Microsoft Docs
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Azure AD integreren met Xamarin-apps
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Met Xamarin, kunt u mobiele apps in C# die kunnen worden uitgevoerd op iOS, Android en Windows (mobiele apparaten en pc's). Als u een app met Xamarin maakt, kunt Azure Active Directory (Azure AD) u eenvoudige tooauthenticate gebruikers met hun Azure AD-accounts. Hallo-app kan ook veilig een web-API die wordt beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure-API gebruiken.

Azure AD levert voor Xamarin-apps die tooaccess beveiligde bronnen moeten, Hallo Active Directory Authentication Library (ADAL). Hallo enig doel van ADAL toomake is het eenvoudig voor apps tooget toegangstokens. toodemonstrate hoe eenvoudig het is dit artikel laat zien hoe toobuild DirectorySearcher apps die:

* Voer op iOS, Android, Windows-bureaublad, Windows Phone en Windows Store.
* Met een enkele portable class-bibliotheek (PCL) tooauthenticate gebruikers en tokens krijgen voor hello Azure AD Graph API.
* Zoeken in een map voor gebruikers met een opgegeven UPN.

## <a name="before-you-get-started"></a>Voordat u aan de slag gaat
* Hallo downloaden [basisproject](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Elke download is een Visual Studio 2013-oplossing.
* U moet ook een Azure AD-tenant in welke toocreate gebruikers en het Hallo-app registreren. Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende vier secties.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Stap 1: Uw Xamarin-ontwikkelomgeving instellen
Omdat deze zelfstudie projecten voor iOS, Android en Windows omvat, moet u zowel Visual Studio en Xamarin. toocreate hello nodig omgeving, volledige Hallo proces in [ingesteld omhoog en installeer Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) op MSDN. Hallo-instructies bevatten materiaal die u meer informatie over Xamarin toolearn bekijken kunt terwijl u voor Hallo installaties toobe is voltooid wacht.

Nadat u Hallo-installatie hebt voltooid, opent u Hallo oplossing in Visual Studio. Daar vindt u zes projecten: vijf platform-specifieke projecten en één PCL, DirectorySearcher.cs, die wordt gedeeld met alle platforms.

## <a name="step-2-register-hello-directorysearcher-app"></a>Stap 2: Hallo DirectorySearcher app registreren
tooenable hello app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API. Dit doet u al volgt:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. Klik vervolgens onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. toocreate een nieuwe **systeemeigen clienttoepassing**, volg de aanwijzingen Hallo.
  * **Naam** Hallo app toousers beschrijft.
  * **Omleidings-URI** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden. Voer een waarde (bijvoorbeeld http://DirectorySearcher).
6. Nadat u de registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID. Hallo-waarde in Hallo kopiëren **toepassing** tabblad omdat u hebt deze later nodig.
7. Op Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.
8. Selecteer **Microsoft Graph** zoals Hallo API. Onder **gedelegeerde machtigingen**, Hallo toevoegen **Directory-gegevens lezen** machtiging.  
Hierdoor Hallo app tooquery Hallo Graph API voor gebruikers.

## <a name="step-3-install-and-configure-adal"></a>Stap 3: Installeren en configureren van ADAL
Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven. ADAL toocommunicate tooenable in Azure AD, geef deze de enige informatie over app-registratie Hallo.

1. ADAL toohello DirectorySearcher project toevoegen met behulp van Hallo Package Manager-Console.

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

    Opmerking dat twee bibliotheekverwijzingen tooeach project worden toegevoegd: Hallo PCL gedeelte van de ADAL en een gedeelte van de platform-specifieke.
2. Open in Hallo DirectorySearcherLib project DirectorySearcher.cs.
3. Hallo klasse lidwaarden vervangt door Hallo-waarden die u hebt ingevoerd in hello Azure-portal. Uw code verwijst toothese waarden wanneer deze gebruikmaakt van ADAL.

  * Hallo *tenant* Hallo domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).
  * Hallo *clientId* is Hallo client-ID van Hallo-app, die u hebt gekopieerd uit Hallo-portal.
  * Hallo *returnUri* Hallo omleidings-URI die u hebt ingevoerd in Hallo-portal (bijvoorbeeld http://DirectorySearcher) is.

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Stap 4: Gebruik ADAL tooget tokens van Azure AD
Bijna alle Hallo-app verificatielogica ligt in `DirectorySearcher.SearchByAlias(...)`. Alle benodigde in Hallo platform-specifieke projecten toopass een toohello contextuele parameter is `DirectorySearcher` PCL.

1. Open DirectorySearcher.cs en voeg vervolgens een nieuwe parameter toohello `SearchByAlias(...)` methode. `IPlatformParameters`is contextuele Hallo-parameter die ingekapseld Hallo platform-specifieke objecten die behoeften ADAL tooperform Hallo verificatie.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Initialiseren `AuthenticationContext`, dit is de primaire klasse Hallo van ADAL.  
Deze actie geeft ADAL Hallo coördineert deze behoeften toocommunicate met Azure AD.
3. Roep `AcquireTokenAsync(...)`, die Hallo accepteert `IPlatformParameters` object en het Hallo-authenticatiestroom die nodig zijn tooreturn een token toohello-app wordt aangeroepen.

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

    `AcquireTokenAsync(...)`eerste pogingen tooreturn een token voor Hallo aangevraagd resource (in dit geval hello Graph API) zonder tooenter gebruikers hun referenties (via caching of oude tokens vernieuwen). Indien nodig wordt gebruikers hello Azure AD-aanmeldingspagina vóór het aangevraagde Hallo-token ophalen.
4. Hallo access token toohello Graph API-aanvraag in Hallo koppelen **autorisatie** header:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Dit is alles wat voor Hallo `DirectorySearcher` identiteitsgerelateerde PCL en Hallo van app-code. Alles wat u hoeft alleen nog toocall hello `SearchByAlias(...)` methode in elk platform weergaven en, indien nodig, tooadd code voor het verwerken van correct Hallo levenscyclus van de gebruikersinterface.

### <a name="android"></a>Android
1. Voeg in MainActivity.cs, een aanroep te`SearchByAlias(...)` Klik op de knop Hallo handler:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Hallo overschrijven `OnActivityResult` lifecycle methode tooforward verificatie wordt de juiste methode terug toohello omgeleid. ADAL biedt een Help-methode voor dit in Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Windows-bureaublad
MainWindow.xaml.cs, zorg er in een aanroep te`SearchByAlias(...)` door een `WindowInteropHelper` in van het bureaublad Hallo `PlatformParameters` object:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
Hallo iOS in DirSearchClient_iOSViewController.cs, `PlatformParameters` object een verwijzing toohello weergavebesturing nodig:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
In Windows universele MainPage.xaml.cs openen en vervolgens implementeren Hallo `Search` methode. Deze methode maakt gebruik van een Help-methode in een gedeeld project tooupdate UI indien nodig.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Volgend onderwerp
U hebt nu een werkende Xamarin-app die u kunt verificatie van gebruikers en veilig aanroepen van web-API's met behulp van OAuth 2.0 op vijf verschillende platforms.

Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu Hallo tijd toodo dus.

1. Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers Hallo.
2. Zoeken naar andere gebruikers op basis van de UPN.

ADAL maakt het eenvoudig tooincorporate veelvoorkomende identity-functies in Hallo-app. Zorgt het voor alle Hallo dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen. U moet tooknow één API-aanroep `authContext.AcquireToken*(…)`.

Ter referentie: downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (zonder uw configuratiewaarden).

U kunt nu verplaatsen op tooadditional identity-scenario's. Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
