---
title: ontwikkelaarsaccounts aaaAuthorize met behulp van OAuth 2.0 in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooauthorize gebruikers met behulp van OAuth 2.0 in API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Hoe tooauthorize developer gebruikersaccounts via OAuth 2.0 in Azure API Management
Ondersteuning voor veel API's [OAuth 2.0](http://oauth.net/2/) toosecure Hallo API en ervoor te zorgen dat alleen geldige gebruikers toegang hebben en ze alleen toegang resources toowhich tot ze bent recht. In volgorde toouse Azure API Management van interactieve Developer-Console met deze API's Hallo service kunt u tooconfigure uw service-exemplaar toowork met uw OAuth 2.0 API ingeschakeld.

## <a name="prerequisites"></a>Vereisten
Deze handleiding laat zien u hoe tooconfigure uw API Management-service-exemplaar toouse OAuth 2.0-autorisatie voor ontwikkelaars accounts, maar niet weergegeven. u hoe tooconfigure een OAuth 2.0-provider. Hallo-configuratie voor elke OAuth 2.0-provider verschillend zijn, is Hoewel Hallo stappen vergelijkbaar zijn en Hallo vereist stukjes informatie die wordt gebruikt bij het configureren van OAuth 2.0 in uw API Management-service-exemplaar zijn Hallo dezelfde. Dit onderwerp bevat voorbeelden met Azure Active Directory als een OAuth 2.0-provider.

> [!NOTE]
> Zie voor meer informatie over het configureren van OAuth 2.0 met Azure Active Directory Hallo [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] voorbeeld.
> 
> 

## <a name="step1"></a>Een OAuth 2.0-autorisatie-server configureren in API Management
tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> [!NOTE]
> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **beveiliging** van Hallo **API Management** menu aan de linkerkant, klik op Hallo **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie server**.

![OAuth 2.0][api-management-oauth2]

Wanneer u op **toevoegen autorisatie server**, Hallo nieuwe autorisatie serverformulier wordt weergegeven.

![Nieuwe server][api-management-oauth2-server-1]

Voer een naam en een optionele beschrijving in Hallo **naam** en **beschrijving** velden. 

> [!NOTE]
> Deze velden zijn gebruikte tooidentify Hallo OAuth 2.0 autorisatie server binnen het huidige exemplaar van API Management-service Hallo en hun waarden niet afkomstig van Hallo OAuth 2.0-server.
> 
> 

Voer Hallo **Client de registratie van URL**. Deze pagina is waar gebruikers kunnen maken en beheren van hun account, varieert, afhankelijk van Hallo OAuth 2.0-provider die wordt gebruikt. Hallo **Client de registratie van URL** punten toohello pagina die door gebruikers kunnen toocreate gebruiken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts. Sommige organisaties niet configureert of deze functionaliteit te gebruiken, zelfs als Hallo OAuth 2.0-provider wordt ondersteund. Als uw OAuth 2.0-provider geen Gebruikersbeheer van accounts die zijn geconfigureerd heeft, voert u een tijdelijke aanduiding voor URL hier, zoals het Hallo-URL van uw bedrijf of een URL, zoals `https://placeholder.contoso.com`.

de volgende sectie Hallo van Hallo formulier bevat Hallo **autorisatiecode verlenen typen**, **autorisatie eindpunt-URL**, en **aanvraag autorisatiemethode** instellingen.

![Nieuwe server][api-management-oauth2-server-2]

Geef Hallo **autorisatiecode verlenen typen** door te controleren Hallo gewenst typen. **Autorisatiecode** standaard is opgegeven.

Voer Hallo **autorisatie eindpunt-URL**. Voor Azure Active Directory, worden deze URL vergelijkbare toohello-URL, te volgen waarbij `<client_id>` is vervangen door Hallo client-id die uw toepassing toohello OAuth 2.0-server wordt aangeduid.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Hallo **aanvraag autorisatiemethode** geeft aan hoe Hallo autorisatieaanvraag toohello OAuth 2.0-server is verzonden. Standaard **ophalen** is geselecteerd.

de volgende sectie Hallo is waar hello **Token eindpunt-URL**, **Client verificatiemethoden**, **toegangstoken verzenden methode**, en **standaardbereik** zijn opgegeven.

![Nieuwe server][api-management-oauth2-server-3]

Voor een Azure Active Directory OAuth 2.0-server Hallo **Token eindpunt-URL** Hallo volgende indeling hebben waar `<APPID>` heeft Hallo-indeling van `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

standaardinstelling voor Hallo **Client verificatiemethoden** is **Basic**, en **toegangstoken verzenden methode** is **autorisatie-header**. Deze waarden zijn geconfigureerd op deze sectie van Hallo formulier, samen met de Hallo **standaardbereik**.

Hallo **clientreferenties** sectie bevat Hallo **Client-ID** en **clientgeheim**, die zijn verkregen tijdens Hallo maken en de configuratie van uw OAuth 2.0 -Server. Eenmaal Hallo **Client-ID** en **clientgeheim** zijn opgegeven, hello **redirect_uri** voor Hallo **autorisatiecode** wordt gegenereerd. Deze URI wordt gebruikte tooconfigure Hallo antwoord-URL in de configuratie van uw OAuth 2.0-server.

![Nieuwe server][api-management-oauth2-server-4]

Als **autorisatiecode verlenen typen** te is ingesteld,**Resource eigenaarswachtwoord**, Hallo **wachtwoordreferenties Resource-eigenaar** sectie is gebruikte toospecify die gegevens worden gebruikt. anders kunt u het leeg laten.

![Nieuwe server][api-management-oauth2-server-5]

Zodra het Hallo-formulier is voltooid, klikt u op **opslaan** toosave Hallo API Management OAuth 2.0-autorisatie-serverconfiguratie. Zodra Hallo-serverconfiguratie is opgeslagen, kunt u configureren API's toouse deze configuratie, zoals wordt weergegeven in de volgende sectie Hallo.

## <a name="step2"></a>Een API-toouse OAuth 2.0-gebruikersautorisatie configureren
Klik op **API's** van Hallo **API Management** menu op Hallo van links, klikt u op naam van Hallo gewenst API hello, klik op **beveiliging**, en controleer vervolgens in Hallo voor **OAuth 2.0**.

![Gebruikersautorisatie][api-management-user-authorization]

Selecteer Hallo gewenst **autorisatie server** in de vervolgkeuzelijst Hallo en klik op **opslaan**.

![Gebruikersautorisatie][api-management-user-authorization-save]

## <a name="step3"></a>Hello OAuth 2.0-gebruikersautorisatie testen in Hallo-Portal voor ontwikkelaars
Zodra u hebt uw OAuth 2.0-autorisatie-server is geconfigureerd en uw API-toouse die server is geconfigureerd, kunt u het testen door te gaan toohello Developer-Portal en een API aanroepen.  Klik op **ontwikkelaarsportal** in Hallo menu rechtsboven.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** in Hallo bovenste menu en selecteer **Echo-API**.

![Echo-API][api-management-apis-echo-api]

> [!NOTE]
> Als er slechts één API is geconfigureerd of zichtbaar tooyour-account op de API's te klikken u rechtstreeks toohello bewerkingen voor die API gaat.
> 
> 

Selecteer Hallo **GET Resource** bewerking, klikt u op **Console openen**, en selecteer vervolgens **autorisatiecode** Hallo vervolgkeuzelijst.

![Console openen][api-management-open-console]

Wanneer **autorisatiecode** is geselecteerd, wordt een pop-upvenster weergegeven met Hallo aanmelden vorm van Hallo OAuth 2.0-provider. In dit voorbeeld wordt Hallo aanmelden formulier verstrekt door Azure Active Directory.

> [!NOTE]
> Als u pop-ups hebt uitgeschakeld, u zult gevraagd tooenable ze door Hallo browser. Nadat u deze wilt inschakelen, selecteert u **autorisatiecode** opnieuw en hello aanmelden formulier worden weergegeven.
> 
> 

![Aanmelden][api-management-oauth2-signin]

Zodra u zich hebt aangemeld, Hallo **aanvraagheaders** zijn gevuld met een `Authorization : Bearer` Hallo aanvraag machtigt-header.

![Token voor verbindingsverzoeken-header][api-management-request-header-token]

U kunt op dit moment Hallo gewenst waarden voor Hallo resterende parameters configureren en Hallo aanvraag indienen. 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van OAuth 2.0 en API Management Hallo volgende video en bijbehorende [artikel](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

