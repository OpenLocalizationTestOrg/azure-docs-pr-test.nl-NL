---
title: Active Directory aaaAzure v2.0 scopes, machtigingen en toestemming | Microsoft Docs
description: Een beschrijving van de autorisatie in hello Azure AD v2.0-eindpunt, met inbegrip van bereiken, machtigingen en toestemming.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Scopes, machtigingen en toestemming in hello Azure Active Directory v2.0-eindpunt
Apps die zijn geïntegreerd met Azure Active Directory (Azure AD) voert u een autorisatie-model waarmee gebruikers controle over hoe een app toegang krijgen hun gegevens tot. Hallo v2.0 implementatie van Hallo autorisatie-model is bijgewerkt en verandert hoe een app moet communiceren met Azure AD. In dit artikel bevat informatie over de basisconcepten Hallo van dit model autorisatie, waaronder bereiken, machtigingen en toestemming.

> [!NOTE]
> Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen. toodetermine of Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Scopes en -machtigingen
Azure AD implementeert Hallo [OAuth 2.0](active-directory-v2-protocols.md) (authorization protocol). OAuth 2.0 is een methode waarmee een app van derden toegang web gehoste bronnen namens een gebruiker tot. Een web gehost resource die kan worden geïntegreerd met Azure AD heeft een bron-id of *Application ID URI*. Bijvoorbeeld: Microsoft website wordt gehost resources onder andere:

* Hallo Office 365 Unified Mail API:`https://outlook.office.com`
* Hello Azure AD Graph API:`https://graph.windows.net`
* Microsoft Graph:`https://graph.microsoft.com`

Hallo geldt voor alle resources van derden die zijn geïntegreerd met Azure AD. Een van deze resources kunt ook een reeks machtigingen die gebruikt toodivide Hallo functionaliteit van die resource in kleinere reeksen worden kunnen definiëren. Als u bijvoorbeeld [Microsoft Graph](https://graph.microsoft.io) is gedefinieerd machtigingen toodo Hallo na taken, onder andere:

* Lezen van een gebruiker kalender
* Schrijven van de gebruiker tooa kalender
* E-mail met een gebruiker als afzender verzenden

Door het definiëren van deze typen machtigingen heeft Hallo resource fijnmazig controle over de gegevens en hoe Hallo gegevens wordt weergegeven. Een app van derden kunt u deze machtigingen aanvragen bij een app-gebruiker. Hallo app gebruiker moet Hallo machtigingen goedkeuren voordat Hallo app kan namens Hallo van de gebruiker. Door de verdeling in segmenten van de bron van het Hallo-functionaliteit in kleinere machtigingensets, kunnen apps van derden ingebouwde toorequest alleen Hallo specifieke machtigingen die zij nodig hebben tooperform hun werking zijn. App-gebruikers kunnen weten precies wijze waarop een app gebruikmaakt van hun gegevens en deze te vertrouwen dat die Hallo-app werkt anders met kwade bedoelingen.

In Azure AD en OAuth, deze typen machtigingen worden genoemd *scopes*. Soms ook zijn waarnaar wordt verwezen tooas *oAuth2Permissions*. Een scope wordt weergegeven in Azure AD als een string-waarde. Hallo Microsoft Graph voorbeeld voortzet, is Hallo bereikwaarde voor elke machtiging:

* Lezen van een gebruiker kalender met`Calendar.Read`
* Met schrijven van de gebruiker tooa kalender`Mail.ReadWrite`
* E-mail verzenden namens een gebruiker met door`Mail.Send`

Een app kunt u deze machtigingen aanvragen door te geven Hallo scopes in aanvragen toohello v2.0-eindpunt.

## <a name="openid-connect-scopes"></a>Scopes OpenID Connect
Hallo v2.0 implementatie van OpenID Connect, is enkele goed gedefinieerde scopes die specifieke tooa-bron niet van toepassing: `openid`, `email`, `profile`, en `offline_access`.

### <a name="openid"></a>openid
Als een app aanmelden met behulp van uitvoert [OpenID Connect](active-directory-v2-protocols.md), moet het Hallo aanvragen `openid` bereik. Hallo `openid` scope wordt weergegeven op Hallo werkaccount pagina toestemming te geven als de machtiging 'Aanmelden u' Hallo en toestemming pagina op Hallo persoonlijke Microsoft-account omdat de machtiging 'Uw profiel weergeven en verbinding maken met tooapps en services met behulp van uw Microsoft-account' Hallo. Met deze machtiging een app een unieke id voor de gebruiker Hallo kan ontvangen in de vorm Hallo Hallo `sub` claim. Dit biedt ook Hallo app toegang toohello gebruikersgegevens eindpunt. Hallo `openid` bereik op Hallo v2.0-tokeneindpunt tooacquire ID-tokens, die gebruikt toosecure HTTP-aanroepen tussen de verschillende onderdelen van een app worden kunnen kan worden gebruikt.

### <a name="email"></a>E-mail
Hallo `email` bereik kan worden gebruikt met Hallo `openid` bereik en alle andere. Het primaire e-mailadres Hallo app toegang toohello van de gebruiker in de vorm Hallo Hallo biedt `email` claim. Hallo `email` claim is opgenomen in een token alleen als een e-mailadres is gekoppeld aan de gebruikersaccount hello, die niet altijd Hallo-aanvraag. Als hierbij Hallo `email` bereik, uw app moet worden voorbereid toohandle een aanvraag in welke Hallo `email` claim bestaat niet in het Hallo-token.

### <a name="profile"></a>Profiel
Hallo `profile` bereik kan worden gebruikt met Hallo `openid` bereik en alle andere. Dit biedt Hallo app toegang tooa aanzienlijke hoeveelheid informatie over Hallo-gebruiker. toegang tot Hallo-informatie bevat, maar is niet beperkt de voornaam van de gebruiker, achternaam, voorkeur gebruikersnaam Hallo en object-id Zie voor een volledige lijst van Hallo profiel claims die beschikbaar zijn in de Hallo id_tokens parameter voor een specifieke gebruiker Hallo [v2.0 tokens verwijzing](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Hallo [ `offline_access` bereik](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) resulteert in uw app toegang tooresources namens de gebruiker Hallo voor langere tijd. Op Hallo werk toestemming accountpagina verschijnt dit bereik de machtiging 'Toegang tot uw gegevens op elk gewenst moment' Hallo. Op Hallo persoonlijke Microsoft-account toestemming pagina, wordt deze weergegeven als de machtiging 'Altijd toegang tot je gegevens' Hallo. Wanneer een gebruiker Hallo goedkeurt `offline_access` bereik, uw app vernieuwen van tokens van token Hallo v2.0-eindpunt kunt ontvangen. Vernieuwen van tokens zijn lange levensduur hebben. Uw app kan nieuwe toegangstokens ophalen wanneer oudere zijn verlopen.

Als uw app geen Hallo heeft aangevraagd `offline_access` bereik, het ontvangt geen vernieuwen van tokens. Dit betekent dat wanneer u een autorisatiecode in Hallo inwisselen [OAuth 2.0-autorisatiecodestroom](active-directory-v2-protocols.md), ontvangt u alleen een toegangstoken van Hallo `/token` eindpunt. Hallo toegangstoken is geldig voor een korte periode. Hallo toegangstoken verloopt meestal binnen één uur. Op dat moment uw app moet tooredirect Hallo gebruiker back toohello `/authorize` eindpunt tooget een nieuwe autorisatiecode. Tijdens deze omleiding, afhankelijk van Hallo type app kan Hallo gebruiker moet tooenter hun referenties opnieuw of opnieuw toestemming geven toopermissions.

Zie voor meer informatie over hoe tooget en gebruik tokens vernieuwen Hallo [v2.0 protocolnaslaginformatie](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Afzonderlijke gebruikers toestemming wordt gevraagd
In een [OpenID Connect of OAuth 2.0](active-directory-v2-protocols.md) autorisatie aanvraagt, een app kan aanvragen Hallo machtigingen moet met behulp van Hallo `scope` queryparameter. Bijvoorbeeld, wanneer een gebruiker zich aanmeldt tooan app, Hallo app stuurt een aanvraag zoals Hallo voorbeeld (met regeleinden toegevoegd voor de leesbaarheid) te volgen:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Hallo `scope` parameter is een door spaties gescheiden lijst met bereiken die Hallo app vraagt. Elke scope wordt aangegeven door Hallo bereik waarde toohello van de bron-id (hello toepassing-ID-URI) toe te voegen. In Hallo aanvraag bijvoorbeeld Hallo app behoeften machtiging tooread Hallo van gebruiker agenda en mail verzenden als Hallo-gebruiker.

Nadat de gebruiker Hallo hun referenties invoert, Hallo v2.0-eindpunt controleert of een overeenkomende record van *toestemming van de gebruiker*. Als de gebruiker Hallo niet heeft ingestemd tooany Hallo aangevraagd machtigingen in de afgelopen, Hallo Hallo v2.0-eindpunt wordt gevraagd Hallo gebruiker toogrant Hallo aangevraagd machtigingen.

![Account toestemming werken](../../media/active-directory-v2-flows/work_account_consent.png)

Wanneer gebruiker Hallo Hallo machtiging goedkeurt, wordt toestemming Hallo vastgelegd zodat hello gebruiker heeft geen tooconsent opnieuw op de volgende accountaanmeldingen.

## <a name="requesting-consent-for-an-entire-tenant"></a>Toestemming voor een volledige-tenant aanvragen
Wanneer een organisatie een licentie of abonnement voor een toepassing koopt, wil Hallo organisatie vaak toofully inrichten Hallo-toepassing voor de werknemers. Als onderdeel van dit proces kan een beheerder toestemming voor Hallo toepassing tooact namens een werknemer verlenen. Als Hallo beheerder toestemming voor de hele tenant hello verleent, zien niet Hallo medewerkers een pagina toestemming voor de toepassing hello.

toorequest toestemming voor alle gebruikers in een tenant, uw app kunt Hallo toestemming beheereindpunt gebruiken.

## <a name="admin-restricted-scopes"></a>Scopes administrator beperkt
Sommige hoge privileges machtigingen in Hallo Microsoft ecosysteem te kunnen worden ingesteld*administrator beperkt*. Voorbeelden van dergelijke bereiken zijn Hallo volgende machtigingen:

* Directory-gegevens voor een organisatie worden gelezen door`Directory.Read`
* Schrijven van gegevens tooan directory van de organisatie met behulp van`Directory.ReadWrite`
* Beveiligingsgroepen in de map van een organisatie worden gelezen door`Groups.Read.All`

Hoewel een consumer-gebruiker een toepassing toegang toothis soort gegevens verlenen kan, worden de organisatie-gebruikers beperkt verlenen van toegang toohello dezelfde van gevoelige bedrijfsgegevens set. Als uw toepassing toegang tooone van deze machtigingen van een organisatie-gebruiker vraagt, ontvangt Hallo een foutbericht dat ze zijn geen geautoriseerde tooconsent tooyour app-machtigingen.

Als uw app tooadmin beperkt toegangsbereiken voor organisaties vereist, moet u aanvragen ze rechtstreeks vanuit de bedrijfsbeheerder van een, ook door het gebruik van het Hallo-beheerder toestemming eindpunt hieronder wordt beschreven.

Wanneer een beheerder verleent dat deze machtigingen via Hallo beheerder eindpunt toestemming geeft, wordt toestemming verleend voor alle gebruikers in het Hallo-tenant.

## <a name="using-hello-admin-consent-endpoint"></a>Gebruik van het Hallo-beheerder toestemming eindpunt
Als u deze stappen hebt uitgevoerd, kan uw app-machtigingen voor alle gebruikers in een tenant, met inbegrip van de administrator beperkt scopes verzamelen. toosee een codevoorbeeld waarin Hallo stappen implementeert, Zie Hallo [administrator beperkt scopes voorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Hallo machtigingen in Hallo-portal voor registratie van app
1. Ga tooyour toepassing in Hallo [toepassing-Portal voor Wachtwoordregistratie](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of [maken van een app](active-directory-v2-app-registration.md) als u dat nog niet gedaan hebt.
2. Zoek Hallo **Microsoft Graph machtigingen** sectie en voeg vervolgens Hallo machtigingen die vereist dat uw app.
3. Zorg ervoor dat u **opslaan** Hallo van app-registratie.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Aanbevolen: Meld u Hallo gebruiker in tooyour app
Normaal gesproken wanneer u een toepassing bouwt die gebruikmaakt van Hallo toestemming beheereindpunt, Hallo app moet een pagina of weergave in welke Hallo beheerder Hallo-app-machtigingen kan goedkeuren. Deze pagina kan onderdeel van de registratie stroom Hallo-app, onderdeel van het Hallo-app-instellingen, of het kan worden toegewezen 'verbinding' stroom. In veel gevallen kan zinvol het voor Hallo app tooshow dit "verbinding maken' weergave alleen nadat een gebruiker is aangemeld met een werk- of school Microsoft-account.

Wanneer u zich Hallo-gebruiker in de app tooyour aanmeldt, kunt u identificeren Hallo organisatie toowhich Hallo beheerder voordat het verzoek om de benodigde machtigingen voor tooapprove Hallo behoort. Hoewel niet strikt noodzakelijk is, kunt u u bij het maken van een intuïtieve ervaring voor gebruikers van uw organisatie. toosign hello gebruiker in Volg ons [v2.0 protocol zelfstudies](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Hallo-machtigingen voor aanvragen van een directory-beheerder
Wanneer u klaar toorequest machtigingen van de beheerder van uw organisatie bent, kunt u Hallo gebruiker toohello v2.0 omleiden *toestemming beheereindpunt*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parameter | Voorwaarde | Beschrijving |
| --- | --- | --- |
| Tenant |Vereist |Hallo directory-tenant die u wilt dat de machtiging toorequest van. Kan worden opgegeven in de beschrijvende naam van de indeling of GUID. |
| client_id |Vereist |Hallo toepassing-ID die Hallo [toepassing Registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour app toegewezen. |
| redirect_uri |Vereist |Hallo omleidings-URI waar u Hallo antwoord toobe voor uw app toohandle verzonden. Deze moet exact overeenkomen met een Hallo omleidings-URI's die u hebt geregistreerd in de portal voor wachtwoordregistratie Hallo-app. |
| state |Aanbevolen |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd. Een tekenreeks van alle inhoud die u wilt dat kan zijn. Gebruik Hallo status tooencode informatie over de status van de gebruiker van het Hallo in Hallo-app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |

Azure AD vereist op dit moment een tenant administrator toosign in toocomplete Hallo-aanvraag. Hallo beheerder wordt gevraagd alle machtigingen die u hebt aangevraagd voor uw app in app-registratieportal Hallo Hallo tooapprove.

#### <a name="successful-response"></a>Geslaagde reactie
Hallo beheerder goedkeurt Hallo machtigingen voor uw app, Hallo geslaagd antwoord ziet er uit als volgt:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parameter | Beschrijving |
| --- | --- | --- |
| Tenant |Hallo directory-tenant die uw toepassing hello worden machtigingen verleend deze aangevraagd, in GUID-indeling. |
| state |Een waarde die is opgenomen in Hallo-aanvraag die ook in het token antwoord Hallo worden geretourneerd. Een tekenreeks van alle inhoud die u wilt dat kan zijn. Hallo-status is gebruikte tooencode informatie over de status van de gebruiker van het Hallo in Hallo app voordat Hallo verificatieverzoek opgetreden, zoals het Hallo-pagina of weergave op. |
| admin_consent |Te worden ingesteld**true**. |

#### <a name="error-response"></a>Foutbericht
Als Hallo beheerder Hallo machtigingen voor uw app niet goedkeurt, mislukt de Hallo antwoord ziet er als volgt:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parameter | Beschrijving |
| --- | --- | --- |
| error |Een tekenreeks van de fout code die zijn gebruikt tooclassify typen fouten die optreden en kan gebruikte tooreact tooerrors. |
| error_description |Een specifiek foutbericht waarmee een ontwikkelaar kan identificeren Hallo hoofdoorzaak van een fout. |

Nadat u een geslaagde reactie van Hallo beheerder toestemming eindpunt ontvangen hebt, is deze aangevraagd Hallo-machtigingen heeft gekregen uw app. U kunt vervolgens een token voor Hallo-bron die u wilt aanvragen.

## <a name="using-permissions"></a>Met behulp van machtigingen
Nadat het Hallo-gebruiker akkoord gaat toopermissions voor uw app, kan uw app toegangstokens met daarin uw app machtiging tooaccess een resource in sommige capaciteit verkrijgen. Een toegangstoken kan alleen worden gebruikt voor één resource, maar elke machtiging die uw app is verleend voor die bron gecodeerd binnen Hallo toegangstoken is. een toegangstoken tooacquire, uw app kunt maken aan een aanvraag toohello v2.0 token-eindpunt, als volgt:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

U kunt resulterende toegangstoken hello gebruiken in HTTP-aanvragen toohello bron. Betrouwbaar geeft aan dat uw app Hallo juiste machtiging tooperform een specifieke taak heeft toohello-resource.  

Voor meer informatie over Hallo OAuth 2.0-protocol en hoe tooget toegangstokens, Hallo zien [v2.0 protocol eindpuntreferentie](active-directory-v2-protocols.md).
