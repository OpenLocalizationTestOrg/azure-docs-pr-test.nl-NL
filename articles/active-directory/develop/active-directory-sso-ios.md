---
title: aaaHow tooenable SSO cross-app voor iOS met ADAL | Microsoft Docs
description: 'Hoe Hallo toouse Hallo functies van ADAL SDK tooenable eenmalige aanmelding via uw toepassingen. '
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a>Hoe tooenable SSO cross-app voor iOS met ADAL
Eenmalige aanmelding (SSO) bieden zodat gebruikers alleen tooenter eenmaal hun referenties nodig en deze referenties automatisch werk verschillende toepassingen hebben wordt nu door klanten verwacht. Hallo problemen in hun gebruikersnaam en wachtwoord invoeren op een klein scherm, vaak keren gecombineerd met een extra factor (2FA), zoals een telefoongesprek of ge-code, resulteert in een snelle ergernis als een gebruiker heeft toodo dit meer dan één keer voor het product.

Bovendien, als u een identiteitsplatform die van andere toepassingen zoals Microsoft-Accounts of een werkaccount van Office365 gebruikmaken mogelijk toepast, verwachten klanten dat deze referenties toobe toouse beschikbaar op alle toepassingen met hun Hallo leverancier niet van belang.

Hallo Microsoft Identity-platform, samen met onze SDK's van Microsoft Identity komt dit harde werk voor u en geeft u de mogelijkheid toodelight Hallo uw klanten met eenmalige aanmelding bij uw eigen suite van toepassingen, of als met onze broker-functie en de verificator toepassingen in het hele apparaat Hallo.

In dit scenario wordt uitgelegd hoe tooconfigure onze SDK in uw toepassing tooprovide deze voordeel tooyour klanten.

In dit scenario is van toepassing op:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Voorwaardelijke toegang voor Azure Active Directory

Hallo document voorgaande wordt ervan uitgegaan dat u weet hoe te[inrichten van toepassingen in de oude portal Hallo voor Azure Active Directory](active-directory-how-to-integrate.md) en uw toepassing Hello geïntegreerd [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>SSO-concepten in Hallo Identiteitsplatform van Microsoft
### <a name="microsoft-identity-brokers"></a>Microsoft Identity Beleggingsmakelaars
Microsoft biedt voor elk mobiel platform-toepassingen die voor Hallo bridging van referenties voor toepassingen van verschillende leveranciers en kunt voor speciale verbeterde functies waarvoor een enkele veilige plaats waar toovalidate referenties. We noemen deze **beleggingsmakelaars**. Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die enkele of alle Hallo apparaat voor hun werknemers beheert. Deze beleggingsmakelaars ondersteuning voor het beheer van beveiliging voor sommige toepassingen of de hele Hallo-apparaat op basis van wat de IT-beheerders willen. In Windows, wordt deze functionaliteit verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.

We gebruiken deze beleggingsmakelaars en hoe uw klanten mogelijk ze in hun aanmelding stroom voor Hallo Microsoft Identity platform Lees verder voor meer informatie over het.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Patronen voor logboekregistratie in op mobiele apparaten
Toegang toocredentials op apparaten als volgt twee basispatronen voor Hallo Microsoft Identity-platform:

* Niet-broker assisted-aanmeldingen
* Assisted aanmeldingen Broker

#### <a name="non-broker-assisted-logins"></a>Niet-broker assisted-aanmeldingen
Niet-broker assisted aanmeldingen zijn aanmelding ervaringen die inline met de toepassing hello gebeuren en Hallo lokale opslag op Hallo-apparaat voor die toepassing gebruiken. Deze opslag kan worden gedeeld tussen toepassingen maar Hallo referenties zijn nauw gebonden toohello app of suite van apps met behulp van deze referentie. U hebt waarschijnlijk is dit in veel mobiele toepassingen wanneer u een gebruikersnaam en wachtwoord in Hallo toepassing zelf invoert.

Deze aanmeldingen hebben Hallo volgende voordelen:

* Er bestaat een gebruikerservaring volledig in de toepassing hello.
* Referenties kunnen worden gedeeld door toepassingen die zijn ondertekend door Hallo hetzelfde certificaat, een ervaring voor eenmalige aanmelding tooyour reeks toepassingen bieden.
* Besturingselement rond Hallo ervaring met het aanmelden wordt verstrekt toohello toepassing vóór en na het aanmelden.

Deze aanmeldingen hebben Hallo volgende nadelen:

* Kan niet-gebruikerservaring eenmalige aanmelding via alle apps die gebruikmaken van een Microsoft-Identity alleen via de Microsoft-Identities die uw toepassing is geconfigureerd.
* Uw toepassing kan niet worden gebruikt met meer geavanceerde zakelijke functies zoals voorwaardelijke toegang of gebruik Hallo InTune reeks producten.
* Uw toepassing ondersteunt geen verificatie op basis van certificaten voor zakelijke gebruikers.

Hier volgt een weergave over de werking van Hallo Microsoft Identity SDK's met Hallo gedeelde opslag van uw toepassingen tooenable eenmalige aanmelding:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Assisted aanmeldingen Broker
Aanmeldingen Broker-ondersteunde zijn aanmelding ervaringen die optreden in Hallo broker toepassing en Hallo opslag en beveiliging van Hallo broker tooshare referenties gebruiken voor alle toepassingen die van toepassing hello Microsoft Identity platform op Hallo apparaat. Dit betekent dat uw toepassingen afhankelijk zijn van Hallo broker toosign gebruikers in. Op iOS en Android worden deze beleggingsmakelaars opgegeven downloadbare toepassingen dat klanten afzonderlijk installeren of toohello apparaat kunnen worden geactiveerd door een bedrijf die Hallo-apparaat voor de gebruiker beheert. Een voorbeeld van dit type toepassing is Hallo Microsoft Authenticator-toepassing op iOS. In Windows worden deze functionaliteit wordt verstrekt door een ingebouwd toohello-besturingssysteem en technisch wel Hallo Web Authentication Broker kiezen.
Hallo-ervaring varieert per platform en kan verstoren toousers soms zijn als het niet correct worden beheerd. U kunt waarschijnlijk meest bekend zijn met dit patroon als u Hallo Facebook-toepassing is geïnstalleerd en Facebook-verbinding van een andere toepassing. Hallo Hallo platform maakt gebruik van Microsoft Identity hetzelfde patroon.

Voor iOS leidt dit tooa 'overgang' animatie waarbij uw toepassing wordt verzonden toohello achtergrond tijdens Hallo Microsoft Authenticator toepassingen wordt geleverd toohello voorgrond voor Hallo gebruiker tooselect welk account wil toosign met.  

Voor Android en Windows hello account kiezer boven op uw toepassing minder verstoren toohello gebruiker weergegeven.

#### <a name="how-hello-broker-gets-invoked"></a>Hoe Hallo broker opgehaald aangeroepen
Als een compatibel broker is geïnstalleerd op het Hallo-apparaat, zoals Hallo Microsoft Authenticator-toepassing hello Microsoft Identity-SDK's automatisch wordt werk van het Hallo-broker voor u wordt aangeroepen wanneer een gebruiker dat zij toolog aangeeft aan met een account van wensen Hallo Hallo Microsoft Identity-platform. Dit account kan worden een persoonlijk Microsoft-Account, werk of schoolaccount of een account dat u opgeeft en host in Azure met behulp van onze producten B2C en B2B. 

 #### <a name="how-we-ensure-hello-application-is-valid"></a>Hoe we zorgen dat de toepassing hello is geldig
 
 Hallo nodig tooensure Hallo identiteit van een toepassing aanroep Hallo broker is cruciaal toohello beveiliging we in broker assisted-aanmeldingen bieden. Geen iOS of Android zorgt ervoor dat unieke id's die alleen geldig voor een bepaalde toepassing zijn zodat schadelijke toepassingen mogelijk '' een legitieme toepassings-id vervalsen en Hallo-tokens die zijn bedoeld voor legitieme toepassing hello ontvangen. tooensure die we altijd met de juiste toepassing hello tijdens runtime communiceren, vragen we Hallo developer tooprovide een aangepaste redirectURI bij het registreren van de toepassing met Microsoft. **Hoe ontwikkelaars deze omleidings-URI moeten stellen wordt hieronder in detail besproken.** Deze aangepaste redirectURI Hallo bundel-ID van de toepassing hello bevat en wordt ervoor gezorgd dat toobe unieke toohello toepassing door Hallo Apple App Store. Wanneer u een toepassing aanroepen Hallo-broker Hallo broker wordt gevraagd Hallo iOS system tooprovide besturingssysteem met bundel-ID die aangeroepen Hallo broker Hallo. Hallo broker vindt deze tooMicrosoft bundel-ID in Hallo aanroep tooour identiteitssysteem. Als Hallo bundel-ID van de toepassing hello komt niet overeen met het Hallo-bundel-ID door de ontwikkelaar Hallo toous tijdens de registratie opgegeven, wordt de toegang weigert toohello tokens voor Hallo resource Hallo toepassing vraagt. Deze controle zorgt ervoor dat alleen Hallo toepassing die zijn geregistreerd door de ontwikkelaar Hallo tokens ontvangt.

**Hallo developer heeft Hallo keuze van als Hallo Microsoft Identity SDK Hallo broker aanroepen of Hallo geen broker assisted stroom wordt gebruikt.** Echter als Hallo developer ervoor geen toouse Hallo broker-ondersteunde stroom kiest gaat Hallo voordeel verloren van het gebruik van eenmalige aanmelding referenties die gebruiker Hallo mogelijk al toegevoegd op Hallo-apparaat en wordt voorkomen dat de toepassing wordt gebruikt met business functies van Microsoft biedt zijn klanten zoals voorwaardelijke toegang, beheermogelijkheden voor Intune en verificatie op basis van certificaten.

Deze aanmeldingen hebben Hallo volgende voordelen:

* Gebruiker merkt dat eenmalige aanmelding via hun toepassingen ongeacht Hallo leverancier.
* Uw toepassing kunt meer geavanceerde zakelijke functies zoals voorwaardelijke toegang gebruiken of Hallo InTune productreeks gebruikt.
* Uw toepassing kan ondersteuning voor verificatie op basis van certificaten voor zakelijke gebruikers.
* Veel veiligere aanmelden als Hallo identiteit van de toepassing hello en Hallo gebruiker zijn geverifieerd door Hallo broker toepassing met algoritmen voor extra beveiliging en versleuteling.

Deze aanmeldingen hebben Hallo volgende nadelen:

* In iOS-gebruiker Hallo overgegaan buiten de ervaring van uw toepassing, terwijl referenties worden gekozen.
* Verlies van Hallo mogelijkheid toomanage Hallo aanmelding optreden voor uw klanten in uw toepassing.

Hier volgt een weergave van hoe Hallo Microsoft Identity-SDK's werken met Hallo toepassingen tooenable SSO broker:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

. Met deze achtergrondinformatie moet u kunnen toobetter begrijpen en eenmalige aanmelding implementeren in uw toepassing met behulp van Microsoft Identity-platform Hallo en SDK's.

## <a name="enabling-cross-app-sso-using-adal"></a>Inschakelen van verschillende Apps eenmalige aanmelding met ADAL
Hier gebruiken we Hallo ADAL iOS SDK naar:

* Geen broker assisted eenmalige aanmelding voor uw suite van apps inschakelen
* Ondersteuning voor broker-ondersteunde eenmalige aanmelding inschakelen

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Eenmalige aanmelding inschakelen voor niet-broker ondersteund eenmalige aanmelding
Voor niet-broker assisted eenmalige aanmelding via toepassingen beheren Hallo Microsoft Identity-SDK's veel van de complexiteit Hallo van eenmalige aanmelding voor u. Dit omvat Hallo rechts gebruiker zoeken in de cache Hallo en onderhouden van een lijst met aangemelde gebruikers voor u tooquery.

tooenable SSO alle toepassingen die u bezit, moet u toodo hello te volgen:

1. Zorg ervoor dat alle uw toepassingen gebruiker Hallo dezelfde Client-ID of id van toepassing.
2. Zorg ervoor dat alle uw toepassingen delen Hallo dezelfde ondertekening van het certificaat van Apple zodat u sleutelhangers kan delen
3. Aanvragen Hallo dezelfde sleutelhanger recht voor elk van uw toepassingen.
4. Vertel Hallo Microsoft Identity SDK's over Hallo gedeelde sleutelhanger wilt u ons toouse.

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Met behulp van hetzelfde Client-ID Hallo / toepassing-ID voor alle toepassingen in uw pakket apps Hallo
Hallo Microsoft Identity platform tooknow wordt dat het tooshare tokens toegestaan voor uw toepassingen, elke toepassing moet tooshare Hallo dezelfde Client-ID of id van toepassing. Dit is Hallo unieke id die is opgegeven tooyou bij de registratie van uw eerste toepassing in Hallo-portal.

U vraagt zich misschien af hoe u verschillende apps wordt geïdentificeerd toohello Microsoft Identity-service als hierbij Hallo dezelfde toepassing-ID. Hallo-antwoord is Hello **omleidings-URI's**. Elke toepassing kan meerdere omleidings-URI's geregistreerd in Hallo onboarding portal hebben. Elke app in de suite hebben een verschillende omleidings-URI. Een voorbeeld van hoe dit eruitziet lager is dan:

App1 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp`

App2 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp2`

App3 omleidings-URI:`x-msauth-mytestiosapp://com.myapp.mytestapp3`

....

Deze zijn genest onder dezelfde client-ID Hallo / toepassings-ID en opgezocht op basis van Hallo omleidings-URI die u in uw configuratie SDK toous retourneren.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Let op Hallo van de indeling van deze omleidings-URI's worden hieronder beschreven. U mag een omleidings-URI gebruiken, tenzij u wenst dat toosupport Hallo broker, in welk geval ze moeten er ongeveer zo uitzien Hallo bovenstaande*

#### <a name="create-keychain-sharing-between-applications"></a>Sleutelhanger delen tussen toepassingen maken
Inschakelen van het delen van sleutelketens valt buiten het bereik van dit document Hallo en in het document wordt gedekt door Apple [mogelijkheden toevoegen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html). Wat is het belangrijk is dat u bepalen wat u uw sleutelhanger toobe aangeroepen en die mogelijkheid voor alle uw toepassingen toevoegen.

Wanneer u hebt rechten instellen correct u ziet een bestand in uw projectmap recht `entitlements.plist` die iets dat op Hallo volgende lijkt bevat:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

Zodra u Hallo sleutelhanger recht ingeschakeld in elk van uw toepassingen hebt en u klaar toouse SSO bent, vertellen Hallo Microsoft Identity SDK de sleutelketen met behulp van de volgende instelling in Hallo uw `ADAuthenticationSettings` Hello instelling te volgen:

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> Wanneer u een sleutelhanger in uw toepassingen delen kan elke toepassing of verwijderen gebruikers slechter alle Hallo tokens inlezen in uw toepassing. Dit is vooral rampzalig zijn als u toepassingen die afhankelijk van Hallo tokens toodo achtergrondwerk zijn hebt. Een sleutelhanger delen verwijderen betekent dat u voorzichtig in alle moet bewerkingen via Hallo Microsoft Identity SDK's.
> 
> 

Dat is alles. Hallo Microsoft Identity SDK wordt nu referenties delen in al uw toepassingen. Hallo-gebruikerslijst wordt ook gedeeld met exemplaren van een toepassing.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Eenmalige aanmelding inschakelen voor broker ondersteund eenmalige aanmelding
mogelijkheid voor een toepassing toouse broker die is geïnstalleerd op Hallo apparaat is Hallo **standaard uitgeschakeld**. In volgorde toouse uw toepassing met Hallo broker moet u enkele aanvullende configuratiestappen doen en sommige code tooyour toepassing toe te voegen.

Hallo stappen toofollow zijn:

1. Schakel de broker-modus in uw toepassingscode aanroep toohello MS-SDK.
2. Tot stand brengen van een nieuwe omleidings-URI en geef die tooboth Hallo-app en de registratie van uw app.
3. Een URL-schema wordt geregistreerd.
4. Ondersteuning voor iOS9: een machtiging tooyour info.plist-bestand toevoegen.

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Stap 1: Broker-modus inschakelen in uw toepassing
Hallo mogelijkheid voor uw toepassing toouse Hallo broker is ingeschakeld wanneer u Hallo 'context' of de eerste installatie van de verificatie-object maakt. U doen dit door het instellen van het type van uw referenties in uw code:

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
Hallo `AD_CREDENTIALS_AUTO` instelling zorgt dat de Hallo Microsoft Identity SDK tootry toocall uit toohello broker, `AD_CREDENTIALS_EMBEDDED` wordt voorkomen dat Hallo Microsoft Identity SDK toohello broker aanroepen.

#### <a name="step-2-registering-a-url-scheme"></a>Stap 2: Registreren van een URL-schema
Hallo Microsoft Identity-platform gebruikt de URL's tooinvoke Hallo broker en ga daarna terug besturingselement back tooyour toepassing. toofinish die u moet u een URL-schema retouren geregistreerd voor de toepassing die Hallo Microsoft Identity platform weten over. Dit kan worden bovendien tooany andere app-schema's kan u eerder hebt geregistreerd met uw toepassing.

> [!WARNING]
> Is het raadzaam om Hallo URL-schema redelijk unieke toominimize Hallo kans op een andere app Hallo met dezelfde URL-schema. Apple worden niet afgedwongen door Hallo Uniekheid van URL-schema's die zijn geregistreerd in Hallo appstore.
> 
> 

Hieronder volgt een voorbeeld van hoe deze wordt weergegeven in de projectconfiguratie van uw. U kunt dit ook doen in XCode ook:

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a>Stap 3: Een nieuwe omleidings-URI met URL-schema vaststellen
In de volgorde tooensure dat we altijd retourneren Hallo referentie tokens toohello juiste toepassingsnaam, moeten we toomake ervoor dat we terugbellen tooyour toepassing op een manier die Hallo iOS-besturingssysteem kunt controleren. Hallo iOS-besturingssysteem rapporten toohello Microsoft broker toepassingen Hallo bundel-ID van het aanroepen van het Hallo-toepassing. Dit kan niet door een rogue-toepassing worden vervalst. Daarom we maken gebruik van dit samen met de Hallo-URI van onze broker toepassing tooensure dat Hallo tokens toohello juiste toepassingsnaam worden geretourneerd. Moet u tooestablish deze unieke omleidings-URI in uw toepassing en een set als een omleidings-URI in onze portal voor ontwikkelaars.

Hallo juiste vorm van de omleidings-URI moet zijn:

`<app-scheme>://<your.bundle.id>`

Voorbeeld: *x-msauth-mytestiosapp://com.myapp.mytestapp*

Deze omleidings-URI moet toobe opgegeven in de registratie van uw app met behulp van Hallo [Azure-portal](https://portal.azure.com/). Zie voor meer informatie over Azure AD-app-registratie [integreren met Azure Active Directory](active-directory-how-to-integrate.md).

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a>Stap 3a: Voeg een omleidings-URI in uw app en Developer portal toosupport verificatie op basis
toosupport certificaat gebaseerde verificatie een tweede 'msauth' moet toobe geregistreerd in uw toepassing en het Hallo [Azure-portal](https://portal.azure.com/) toohandle certificaatverificatie desgewenst tooadd die ondersteuning bieden in uw toepassing.

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

Voorbeeld: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a>Stap 4: iOS9: een configuratie parameter tooyour app toevoegen
– CanOpenURL maakt gebruik van ADAL: toocheck als Hallo broker op Hallo-apparaat is geïnstalleerd. In iOS vergrendeld 9 Apple wat schema's een toepassing kunnen opvragen. U moet tooadd 'msauth' toohello LSApplicationQueriesSchemes gedeelte van uw `info.plist file`.

<key>LSApplicationQueriesSchemes</key>

<array><string>msauth</string>
</array>

### <a name="youve-configured-sso"></a>U kunt eenmalige aanmelding hebt geconfigureerd.
Nu Hallo Microsoft Identity SDK automatisch zowel referenties delen in uw toepassingen en Hallo broker aanroepen, indien aanwezig zijn op hun apparaat.

