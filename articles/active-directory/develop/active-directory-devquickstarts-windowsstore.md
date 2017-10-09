---
title: aaaAzure AD Windows Store aan de slag | Microsoft Docs
description: Build Windows Store-apps die integreren met Azure AD voor aanmelden en roept u Azure AD beveiligd met OAuth API's.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Azure AD integreren met Windows Store-apps
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Windows Store 8.1 en projecten met een eerdere versie worden niet ondersteund in Visual Studio 2017.  Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.

Als u apps voor Windows Store Hallo ontwikkelt, Azure Active Directory (Azure AD) maakt het eenvoudig en snel tooauthenticate uw gebruikers met hun Active Directory-accounts. Een app door te integreren met Azure AD, kan veilig een web-API die wordt beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API gebruiken.

Voor Windows Store-desktoptoepassingen die dat tooaccess beveiligde bronnen nodig hebt, biedt Azure AD Hallo Active Directory Authentication Library (ADAL). Hallo enig doel van ADAL is toomake gemakkelijk Hallo app tooget toegangstokens. toodemonstrate hoe eenvoudig het is dit artikel laat zien hoe toobuild een DirectorySearcher Windows Store-app die:

* Krijgt toegang tot tokens voor hello Azure AD Graph API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Zoekt een directory voor gebruikers met een opgegeven user principal name (UPN).
* Tekenen gebruikers uit.

## <a name="before-you-get-started"></a>Voordat u aan de slag gaat
* Hallo downloaden [basisproject](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), of downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Elke download is een Visual Studio 2015-oplossing.
* U moet ook een Azure AD-tenant in welke toocreate gebruikers en het Hallo-app registreren. Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

Wanneer u klaar bent, Hallo Hallo-procedures volgen in de volgende drie secties.

## <a name="step-1-register-hello-directorysearcher-app"></a>Stap 1: Hallo DirectorySearcher app registreren
tooenable hello app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API. Dit doet u al volgt:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. Klik vervolgens onder Hallo **Directory** lijst, selecteer Hallo Active Directory-tenant waar u tooregister Hallo app.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Ga als volgt Hallo prompts toocreate een **systeemeigen clienttoepassing**.
  * **Naam** Hallo app toousers beschrijft.
  * **Omleidings-URI** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden. Voer een aanduidingswaarde van de tijdelijke voor nu (bijvoorbeeld **http://DirectorySearcher**). Vervangt u de waarde hello later.
6. Nadat u Hallo-registratie hebt voltooid, wijst Azure AD Hallo app een unieke toepassings-ID. Hallo-waarde op Hallo kopiëren **toepassing** tabblad omdat u hebt deze later nodig.
7. Op Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.
8. Voor Hallo **Azure Active Directory** app, selecteer **Microsoft Graph** zoals Hallo API.
9. Onder **gedelegeerde machtigingen**, Hallo toevoegen **toegang Hallo directory als de gebruiker is aangemeld Hallo** machtiging. In dat geval kunnen Hallo app tooquery Hallo Graph API voor gebruikers.

## <a name="step-2-install-and-configure-adal"></a>Stap 2: Installeren en configureren van ADAL
Nu dat u een app in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven. ADAL toocommunicate tooenable in Azure AD, geef deze de enige informatie over app-registratie Hallo.

1. ADAL toohello DirectorySearcher project toevoegen met behulp van Hallo Package Manager-Console.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. Open in Hallo DirectorySearcher project MainPage.xaml.cs.
3. Vervang de waarden Hallo in Hallo **configuratiewaarden** regio met Hallo-waarden die u hebt ingevoerd in hello Azure-portal. Uw code verwijst toothese waarden wanneer deze gebruikmaakt van ADAL.
  * Hallo *tenant* Hallo domein van uw Azure AD-tenant (bijvoorbeeld: contoso.onmicrosoft.com).
  * Hallo *clientId* is Hallo client-ID van Hallo-app, die u hebt gekopieerd uit Hallo-portal.
4. U moet nu toodiscover Hallo callback URI voor uw Windows Store-app. Stel een onderbrekingspunt in op deze regel in Hallo `MainPage` methode:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Bouwen Hallo-oplossing, om ervoor te zorgen dat alle pakket-verwijzingen zijn hersteld. Als er pakketten ontbreken, Hallo NuGet Package Manager openen en deze terugzetten.
6. Voer Hallo-app en kopieer Hallo-waarde van `redirectUri` wanneer Hallo onderbrekingspunt is bereikt. Hallo-waarde moet er ongeveer als Hallo volgende:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Terug op Hallo **instellingen** tabblad van het Hallo-app in hello Azure-portal, Voeg een **RedirectUri** Hello vóór waarde.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Stap 3: Gebruik ADAL tooget tokens van Azure AD
Hallo basisprincipe achter ADAL is dat wanneer het Hallo-app moet een toegangstoken, aanroept `authContext.AcquireToken(…)`, en ADAL Hallo rest.  

1. Initialiseren van de app Hallo `AuthenticationContext`, dit is de primaire klasse Hallo van ADAL. Deze actie wordt doorgegeven ADAL Hallo coördinaten deze moet toocommunicate met Azure AD en meer over toocache tokens.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Zoek Hallo `Search(...)` methode die wordt opgeroepen wanneer gebruikers op Hallo **Search** knop op de gebruikersinterface van de app Hallo. Deze methode maakt een get-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint. tooquery hello Graph API een toegangstoken opnemen in Hallo-aanvraag **autorisatie** header. Dit is waar de ADAL wordt geleverd.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Wanneer Hallo app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties. Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, dit geeft een dialoogvenster aanmelden, verzamelt Hallo gebruikersreferenties en geeft aan dat een token na een verificatie geslaagde. Als ADAL niet kan tooreturn een token voor een bepaalde reden, Hallo *AuthenticationResult* status is een fout opgetreden.
3. Het is nu tijd toouse Hallo toegangstoken die u zojuist hebt opgehaald. Ook in Hallo `Search(...)` methode koppelen Hallo token toohello Graph API aanvraag ophalen in Hallo **autorisatie** header:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. U kunt Hallo `AuthenticationResult` object toodisplay informatie over het Hallo-gebruiker in het Hallo-app, zoals Hallo gebruikersnaam:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. U kunt ook ADAL toosign gebruikers buiten de Hallo app gebruiken. Wanneer Hallo gebruiker Hallo **Afmelden** knop, moet u zorgen dat Hallo volgende oproep te`AcquireTokenAsync(...)` ziet u een weergave aanmelden. Deze actie is met ADAL, net zo eenvoudig als het token Hallo-cache wissen:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Volgend onderwerp
U hebt nu een werkende Windows Store-app die u kunt verificatie van gebruikers, veilig aanroepen van web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.

Als u al uw tenant met gebruikers nog niet hebt ingevuld, is nu Hallo tijd toodo dus.
1. Uitvoeren van uw app DirectorySearcher en meld u aan met een van de gebruikers Hallo.
2. Zoeken naar andere gebruikers op basis van de UPN.
3. Hallo-app sluiten en opnieuw te starten. U ziet hoe Hallo gebruikerssessie blijft intact.
4. Met de rechtermuisknop op de balk onderaan van toodisplay Hallo afmelden en vervolgens weer aanmelden als een andere gebruiker.

ADAL maakt het eenvoudig tooincorporate deze algemene identiteit functies in Hallo-app. Zorgt het voor alle Hallo dirty werk voor u, zoals Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface en vernieuwen van tokens verlopen. U moet tooknow één API-aanroep `authContext.AcquireToken*(…)`.

Ter referentie: downloaden Hallo [voltooide voorbeeld](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (zonder uw configuratiewaarden).

U kunt nu verplaatsen op tooadditional identity-scenario's. Probeer bijvoorbeeld [beveiligen van een .NET-Web-API met Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
