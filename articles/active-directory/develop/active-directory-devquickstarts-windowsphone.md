---
title: aaaAzure AD Windows Phone-aan de slag | Microsoft Docs
description: "Hoe toobuild een Windows Phone-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd met OAuth API's."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Azure AD integreren met een Windows Phone-App
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Projecten met Windows Phone 8.1 en een eerdere versie worden niet ondersteund in Visual Studio 2017.  Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.

Als u een Windows Phone 8.1-app ontwikkelt, kunt Azure AD u eenvoudig en snel voor tooauthenticate u uw gebruikers met hun Active Directory-accounts.  Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.

> [!NOTE]
> Deze voorbeeldcode maakt gebruik van ADAL versie 2.0.  Voor de nieuwste technologie hello, kunt u tooinstead Probeer onze [universele Windows-zelfstudie met behulp van ADAL v3.0](active-directory-devquickstarts-windowsstore.md).  Als u een app voor Windows Phone 8.1 inderdaad bouwt, is dit de juiste plaats Hallo.  ADAL v2.0 wordt nog steeds volledig ondersteund en hello aanbevolen manier van ontwikkelen apps agianst Windows Phone 8.1 gebruikmaakt van Azure AD.
> 
> 

Azure AD levert voor .NET-systeemeigen clients waarvoor tooaccess beveiligde bronnen, Hallo Active Directory Authentication Library of ADAL.  Enig doel in het leven van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens.  toodemonstrate hoe gemakkelijk het is, hier gaan we gaat verder met een 'Directory Searcher' Windows Phone 8.1-app die:

* Krijgt toegang tot tokens voor het aanroepen van hello Azure AD Graph API met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Zoekt een directory voor gebruikers met een opgegeven UPN.
* Tekenen gebruikers uit.

toobuild hello volledige werkende toepassing, moet u naar:

1. Uw toepassing registreren met Azure AD.
2. Installeren en configureren van ADAL.
3. Gebruik ADAL tooget tokens van Azure AD.

tooget gestart, [een basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Elk is een Visual Studio 2013-oplossing.  U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.  Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Hallo Directory Searcher-toepassing registreren
tooenable uw app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.
3. Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.
4. Klik op **App registraties** en kies **toevoegen**.
5. Volg de aanwijzingen Hallo en maak een nieuwe **systeemeigen clienttoepassing**.
  * Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers
  * Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat tooreturn token antwoorden bij Azure AD wordt gebruikt.  Een tijdelijke aanduidingswaarde opgeven voor nu, bijvoorbeeld `http://DirectorySearcher`.  We Vervang deze waarde hoger.
6. Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id  U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.
7. Van Hallo **instellingen** pagina **Required Permissions** en kies **toevoegen**. Selecteer Hallo **Microsoft Graph** als Hallo API en voeg Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.  Hiermee schakelt u uw toepassing tooquery Hallo Graph API voor gebruikers.

## <a name="2-install--configure-adal"></a>2. Installeren en configureren van ADAL
Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.  Voor ADAL toobe kunnen toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.

* Beginnen met het ADAL toohello DirectorySearcher project met behulp van Hallo Package Manager-Console toe te voegen.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Open in Hallo DirectorySearcher project `MainPage.xaml.cs`.  Vervang de waarden Hallo in Hallo `Config Values` regio tooreflect Hallo waarden die u hebt de invoer in hello Azure-Portal.  Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.
  * Hallo `tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld contoso.onmicrosoft.com
  * Hallo `clientId` hello clientId van uw toepassing die u hebt gekopieerd uit de portal Hallo is.
* U moet nu toodiscover Hallo callback uri voor uw Windows Phone-app.  Stel een onderbrekingspunt in op deze regel in Hallo `MainPage` methode:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Voer Hallo-app en kopieer gereserveerd Hallo-waarde van `redirectUri` wanneer Hallo onderbrekingspunt is bereikt.  Moet er ongeveer als

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Terug op Hallo **configureren** tabblad van uw toepassing in hello Azure-beheerportal, vervang de waarde Hallo Hallo **RedirectUri** met deze waarde.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Gebruik ADAL tooGet Tokens van AAD
Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, aanroept `authContext.AcquireToken(…)`, en ADAL Hallo rest.  

* de eerste stap Hallo tooinitialize van uw app is `AuthenticationContext` -ADAL de primaire klasse.  Dit is waar het doorgeven van ADAL Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Nu zoeken Hallo `Search(...)` methode, die wordt aangeroepen wanneer Hallo gebruiker cliks knop "Zoeken" in de gebruikersinterface van de app Hallo Hallo.  Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.  Maar in de volgorde tooquery Hallo Graph API, moet u een access_token in Hallo tooinclude `Authorization` header Hallo-aanvraag: dit is waar de ADAL wordt geleverd.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Als interactieve verificatie nodig is, ADAL van Windows Phone Web Authentication Broker (Windows-Adresboek) wordt gebruikt en [voortzetting model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD aanmeldingspagina.  Wanneer Hallo gebruiker zich aanmeldt, moet uw app toopass ADAL Hallo resultaten van de interactie van de Windows-Adresboek Hallo.  Dit is net zo eenvoudig als het implementeren van Hallo `ContinueWebAuthentication` interface:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Nu gaat u tijd toouse hello `AuthenticationResult` dat ADAL tooyour app geretourneerd.  In Hallo `QueryGraph(...)` retouraanroep, koppel Hallo access_token verkregen van toohello GET-aanvraag in Hallo autorisatie-header:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* U kunt ook Hallo `AuthenticationResult` object toodisplay informatie over Hallo-gebruiker in uw app. In Hallo `QueryGraph(...)` methode, gebruik Hallo resultaat tooshow Hallo-id van gebruiker op de pagina Hallo:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Ten slotte kunt u ADAL toosign Hallo gebruiker buiten de toepassing ook gebruiken.  Wanneer Hallo gebruiker op de knop 'Afmelden' hello, willen we tooensure die de volgende oproep te Hallo`AcquireTokenSilentAsync(...)` zal mislukken.  Met ADAL, is dit is net zo eenvoudig als het token Hallo-cache wissen:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Gefeliciteerd. U nu beschikken over een werkende Windows Phone-app die Hallo mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.  Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.  Uitvoeren van uw app DirectorySearcher en meld u aan met een van deze gebruikers.  Zoeken naar andere gebruikers op basis van de UPN.  Hallo-app sluiten en voer deze opnieuw uit.  U ziet hoe Hallo gebruikerssessie blijft intact.  Meld u af en meld u opnieuw aan als een andere gebruiker.

ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.  Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.  Alles wat u moet tooknow één API-aanroep is `authContext.AcquireToken*(…)`.

Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is opgegeven [hier](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  U kunt nu verplaatsen op tooadditional identity-scenario's.  U kunt tootry:

[Een .NET-Web-API met Azure AD beveiligen >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

