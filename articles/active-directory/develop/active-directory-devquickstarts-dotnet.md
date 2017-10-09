---
title: aaaAzure AD .NET aan de slag | Microsoft Docs
description: "Hoe toobuild een .NET Windows-bureaublad-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd met OAuth API's."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Azure AD integreren met een Windows-bureaublad WPF-App
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Als u een bureaubladtoepassing ontwikkelt, kunt Azure AD u eenvoudig en snel voor tooauthenticate u uw gebruikers met hun Active Directory-accounts.  Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.

Azure AD levert voor .NET-systeemeigen clients waarvoor tooaccess beveiligde bronnen, Hallo Active Directory Authentication Library of ADAL.  Enig doel in het leven van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens.  toodemonstrate hoe gemakkelijk het is, hier we je een .NET WPF-takenlijst-toepassing bouwt die:

* Krijgt toegang tot tokens voor het aanroepen van hello Azure AD Graph API met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Zoekt een directory voor gebruikers met een alias voor een gegeven.
* Tekenen gebruikers uit.

toobuild hello volledige werkende toepassing, moet u naar:

1. Uw toepassing registreren met Azure AD.
2. Installeren en configureren van ADAL.
3. Gebruik ADAL tooget tokens van Azure AD.

tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.  Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Hallo DirectorySearcher toepassing registreren
tooenable uw app tooget-tokens, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.
3. Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.
4. Klik op **App registraties** en kies **toevoegen**.
5. Volg de aanwijzingen Hallo en maak een nieuwe **systeemeigen clienttoepassing**.
  * Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers
  * Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat tooreturn token antwoorden bij Azure AD wordt gebruikt.  Voer een waarde specifieke tooyour toepassing, bijvoorbeeld `http://DirectorySearcher`.
6. Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id  U moet deze waarde in de volgende secties hello, dus kopiëren van de pagina van de toepassing hello.
7. Van Hallo **instellingen** pagina **Required Permissions** en kies **toevoegen**. Selecteer Hallo **Microsoft Graph** als Hallo API en voeg Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.  Hiermee schakelt u uw toepassing tooquery Hallo Graph API voor gebruikers.

## <a name="2-install--configure-adal"></a>2. Installeren en configureren van ADAL
Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.  Voor ADAL toobe kunnen toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.

* Beginnen met het ADAL toohello DirectorySearcher project met behulp van Hallo Package Manager-Console toe te voegen.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Open in Hallo DirectorySearcher project `app.config`.  Vervang de waarden Hallo Hallo-elementen in Hallo `<appSettings>` sectie tooreflect Hallo waarden die u hebt de invoer in hello Azure-Portal.  Uw code zal naar deze waarden verwijzen wanneer deze gebruikmaakt van ADAL.
  * Hallo `ida:Tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld contoso.onmicrosoft.com
  * Hallo `ida:ClientId` hello clientId van uw toepassing die u hebt gekopieerd uit de portal Hallo is.
  * Hallo `ida:RedirectUri` is Hallo omleidings-url die u in de portal Hallo geregistreerd.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Gebruik ADAL tooGet Tokens van AAD
Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, aanroept `authContext.AcquireTokenAsync(...)`, en ADAL Hallo rest.  

* In Hallo `DirectorySearcher` project, open `MainWindow.xaml.cs` en zoek Hallo `MainWindow()` methode.  de eerste stap Hallo tooinitialize van uw app is `AuthenticationContext` -ADAL de primaire klasse.  Dit is waar het doorgeven van ADAL Hallo coördinaten moet toocommunicate met Azure AD en meer over toocache tokens.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Nu zoeken Hallo `Search(...)` methode, die wordt aangeroepen wanneer Hallo gebruiker cliks knop "Zoeken" in de gebruikersinterface van de app Hallo Hallo.  Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.  Maar in de volgorde tooquery Hallo Graph API, moet u een access_token in Hallo tooinclude `Authorization` header Hallo-aanvraag: dit is waar de ADAL wordt geleverd.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Wanneer uw app een token aanvragen door het aanroepen van `AcquireTokenAsync(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties.  Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, wordt het weergeven van een dialoogvenster voor aanmelding, Hallo gebruikersreferenties verzamelen en retourneren een token na verificatie is geslaagd.  Als ADAL niet kan tooreturn een token voor een of andere reden is, genereert het een `AdalException`.
* U ziet dat Hallo `AuthenticationResult` object bevat een `UserInfo` -object dat kan worden gebruikt toocollect informatie uw app mogelijk nodig.  In Hallo DirectorySearcher, `UserInfo` gebruikte toocustomize Hallo gebruikersinterface van de app met de id van gebruiker Hallo is.
* Wanneer Hallo gebruiker op de knop 'Afmelden' hello, willen we tooensure die de volgende oproep te Hallo`AcquireTokenAsync(...)` Hallo gebruiker toosign in wordt gevraagd.  Met ADAL, is dit is net zo eenvoudig als het token Hallo-cache wissen:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Als Hallo gebruiker heeft niet op knop 'Afmelden' hello, wilt u echter toomaintain Hallo gebruikerssessie voor Hallo volgende keer dat ze Hallo DirectorySearcher worden uitgevoerd.  Wanneer Hallo app opent, kunt u controleren van de ADAL-tokencache voor een bestaande token en Hallo gebruikersinterface worden dienovereenkomstig bijgewerkt.  In Hallo `CheckForCachedToken()` methode te maken van een andere aanroep van`AcquireTokenAsync(...)`, ditmaal doorgeven in een Hallo `PromptBehavior.Never` parameter.  `PromptBehavior.Never`vertelt ADAL dat Hallo-gebruiker niet moet worden gevraagd voor aanmelding en ADAL moet in plaats daarvan Veroorzaak een exception als het tooreturn niet kan een token.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

Gefeliciteerd. U nu beschikken over een werkende .NET WPF-toepassing die Hallo mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.  Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.  Uitvoeren van uw app DirectorySearcher en meld u aan met een van deze gebruikers.  Zoeken naar andere gebruikers op basis van de UPN.  Hallo-app sluiten en voer deze opnieuw uit.  U ziet hoe Hallo gebruikerssessie blijft intact.  Meld u af en meld u opnieuw aan als een andere gebruiker.

ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.  Dit zorgt voor alle Hallo dirty werk voor u - Cachebeheer, OAuth-protocolondersteuning, presenteren Hallo-gebruiker met een aanmelding-gebruikersinterface vernieuwen van tokens verlopen en meer.  Alles wat u moet tooknow één API-aanroep is `authContext.AcquireTokenAsync(...)`.

Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is opgegeven [hier](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  U kunt nu verplaatsen op tooadditional scenario's.  U kunt tootry:

[Een .NET-Web-API met Azure AD beveiligen >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

