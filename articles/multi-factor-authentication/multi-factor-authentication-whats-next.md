---
title: Azure MFA aaaConfigure | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die wat toodo naast met MFA beschrijft.  Dit omvat rapporten, fraudewaarschuwing, eenmalig overslaan, aangepaste spraakberichten caching, vertrouwde IP-adressen en app-wachtwoorden.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: 7f6d0b0975a2c1da2de9b52e978b84475c79b218
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Azure multi-factor Authentication-instellingen configureren
Dit artikel helpt u bij het beheren van Azure multi-factor Authentication nu dat u actief zijn.  Deze heeft verschillende onderwerpen die u helpen bij tooget Hallo optimaal gebruik van Azure multi-factor Authentication.  Niet al deze functies zijn beschikbaar in elke versie van Azure multi-factor Authentication.

| Functie | Beschrijving | 
|:--- |:--- |
| [Fraudewaarschuwing](#fraud-alert) |Fraudewaarschuwing worden geconfigureerd en zo instellen dat uw gebruikers frauduleuze pogingen tooaccess hun resources rapporteren kunnen. |
| [Eenmalig overslaan](#one-time-bypass) |Met eenmalig overslaan kan een tooauthenticate gebruiker één keer door te multi-factor authentication 'negeren'. |
| [Aangepaste spraakberichten](#custom-voice-messages) |Aangepaste spraakberichten kunnen u toouse uw eigen opnamen of begroetingen met meervoudige verificatie. |
| [Opslaan in cache](#caching-in-azure-multi-factor-authentication) |Opslaan in cache kunt u tooset een bepaalde periode zodat latere authenticatiepogingen automatisch slagen. |
| [Goedgekeurde IP-adressen](#trusted-ips) |Beheerders van een beheerd of federatieve tenant kunnen verificatie in twee stappen van goedgekeurde IP-adressen toobypass gebruiken voor gebruikers die zich via van het bedrijf Hallo lokaal intranet aanmelden. |
| [App-wachtwoorden](#app-passwords) |Een app-wachtwoord kan een toepassing die niet MFA-bewuste toobypass multi-factor authentication-server en blijven werken. |
| [Houd er rekening mee multi-factor Authentication voor onthouden apparaten en browsers](#remember-multi-factor-authentication-for-devices-that-users-trust) |Hiermee kunt u tooremember apparaten voor een bepaald aantal dagen nadat een gebruiker heeft aangemeld met MFA. |
| [Selecteerbare verificatiemethoden](#selectable-verification-methods) |Hiermee kunt u toochoose Hallo verificatiemethoden die beschikbaar voor gebruikers toouse zijn. |

## <a name="access-hello-azure-mfa-management-portal"></a>Toegang tot hello Azure MFA-beheerportal

Hallo-functies die in dit artikel worden geconfigureerd in hello Azure multi-factor Authentication-beheerportal. Er zijn twee manieren tooaccess Hallo MFA-beheerportal via Hallo klassieke Azure-portal. Hallo is eerst door het beheer van een multi-factor Authentication-Provider. Hallo is het tweede via Hallo MFA-service-instellingen. 

### <a name="use-an-auth-provider"></a>Gebruik een Authentication-Provider

Als u een multi-factor Authentication-Provider voor meervoudige verificatie op basis van verbruik gebruikt, gebruikt u deze methode tooaccess Hallo-beheerportal.

tooaccess Hallo MFA-beheerportal via een Azure multi-factor Authentication-Provider, meld u aan bij Hallo klassieke Azure-portal als administrator en selecteer Hallo Active Directory-optie. Klik op Hallo **multi-factor Auth-Providers** tabblad Selecteer vervolgens de map en klikt u op Hallo **beheren** knop Hallo onder aan.

### <a name="use-hello-mfa-service-settings-page"></a>Pagina van de MFA-Service-instellingen hello gebruiken 

Als u een multi-factor Authentication-Provider of een Azure MFA, Azure AD Premium of Enterprise Mobility + Security-licentie hebt, kunt u deze instellingenpagina van methode tooaccess Hallo MFA-service gebruiken.

tooaccess MFA-beheerportal via de pagina Service-instellingen voor MFA Meld u aan bij de klassieke Azure-portal als beheerder Hallo HALLO hallo en selecteer Hallo Active Directory-optie. Klik op de map en klik vervolgens op Hallo **configureren** tabblad. Selecteer onder de sectie multi-factor authentication hello, **service-instellingen beheren**. Aan de onderkant van de Hallo van Hallo MFA-Service-instellingen pagina, klikt u op Hallo **Ga toohello portal** koppeling.


## <a name="fraud-alert"></a>Fraudewaarschuwing
Fraudewaarschuwing worden geconfigureerd en zo instellen dat uw gebruikers frauduleuze pogingen tooaccess hun resources rapporteren kunnen.  Gebruikers kunnen rapporteren van fraude Hallo mobiele App of via hun telefoon.

### <a name="set-up-fraud-alert"></a>Fraudewaarschuwing instellen
1. Navigeer toohello MFA-beheerportal per Hallo instructies Hallo boven aan deze pagina.
2. Klik in de Azure multi-factor Authentication-beheerportal hello, **instellingen** onder Hallo sectie configureren.
3. Controleer onder Hallo fraudewaarschuwing sectie van de pagina instellingen hello, Hallo **gebruikers toestaan Fraudewaarschuwingen toosubmit** selectievakje.
4. Selecteer **opslaan** tooapply uw wijzigingen. 

### <a name="configuration-options"></a>Configuratie-opties

- **Gebruiker blokkeren wanneer fraude wordt gemeld** - als een gebruiker rapporten fraude, hun account is geblokkeerd.
- **Code van fraude tijdens de eerste begroeting tooReport** -gebruikers normaal gesproken druk op # tooconfirm in twee stappen verificatie. Als ze tooreport fraude willen, invoeren ze een code voordat u op #. Deze code is **0** standaard, maar u kunt deze aanpassen.

> [!NOTE]
> Microsoft standaard gesproken begroetingen vertelt gebruikers toopress 0# toosubmit een fraudewaarschuwing voor. Als u toouse een code dan 0 wilt, moet u registreren en uw eigen aangepaste gesproken begroetingen met instructies voor het juiste uploaden.

![Waarschuwingsopties fraude - schermafbeelding](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Hoe gebruikers fraude rapporteren 
Fraudewaarschuwing kan op twee manieren worden gerapporteerd.  Hetzij via Hallo mobiele app of via de telefoon Hallo.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Melden van fraude Hallo mobiele App
1. Wanneer een verificatie tooyour telefoon verzonden wordt, selecteert u deze tooopen Hallo Microsoft Authenticator-app.
2. Selecteer **weigeren** op Hallo-melding. 
3. Selecteer **melden van fraude**.
4. Sluit Hallo-app.

#### <a name="report-fraud-with-a-phone"></a>Melden van fraude met een telefoon
1. Als een aanroep van verificatie tooyour telefoon binnenkomt, beantwoordt u deze.  
2. tooreport fraude, Voer Hallo fraudecode (de standaardwaarde is 0) en vervolgens Hallo teken #. U wordt gewaarschuwd dat een fraudewaarschuwing is ingediend.
3. Hallo oproep beëindigen.

### <a name="view-fraud-reports"></a>Fraude-rapporten weergeven
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer aan de linkerkant hello, Active Directory.
3. Op de bovenste Selecteer Hallo **multi-factor Auth-Providers**. Hiermee wordt een lijst met uw multi-factor Auth-Providers.
4. Selecteer uw multi-factor Authentication-Provider en klik op **beheren** Hallo Hallo pagina onderaan in. Hello Azure multi-factor Authentication-beheerportal geopend.
5. Klik op Hallo Azure multi-factor Authentication-beheerportal, onder weergave een rapport **fraudewaarschuwing**.
6. Hallo datumbereik dat u wenst dat tooview in Hallo rapport opgeven. U kunt ook gebruikersnamen, telefoonnummers en de status van de gebruiker Hallo opgeven.
7. Klik op **Run**. Hiermee wordt een rapport van Fraudewaarschuwingen. Klik op **tooCSV exporteren** desgewenst tooexport Hallo rapport.

## <a name="one-time-bypass"></a>Eenmalig overslaan
Met eenmalig overslaan kan een tooauthenticate gebruiker één keer zonder verificatie in twee stappen uitvoeren. Hallo bypass is tijdelijk en verloopt na een opgegeven aantal seconden. In situaties waar Hallo mobiele app of telefoonnummer niet een melding of telefoongesprek ontvangt, kunt u een eenmalig overslaan inschakelen zodat Hallo gebruiker toegang heeft tot Hallo gewenst resource.

### <a name="create-a-one-time-bypass"></a>Maken van een eenmalig overslaan
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-beheerportal per Hallo instructies Hallo boven aan deze pagina.
3. In hello Azure multi-factor Authentication-beheerportal, dat als er Hallo-naam van uw tenant of Azure MFA-Provider op Hallo achtergelaten met een  **+**  volgende tooit, klikt u op Hallo  **+**  Zie andere replicatiegroepen voor MFA-Server en hello Azure Default groep. Selecteer de juiste groep Hallo.
4. Selecteer onder beheer van de gebruiker **eenmalige**.
5. Op de pagina eenmalig overslaan Hallo op **nieuwe eenmalige**.

  ![Cloud](./media/multi-factor-authentication-whats-next/create1.png)

6. Hallo gebruikersnaam invoeren, Hallo aantal seconden dat Hallo bypass wordt bestaan en Hallo reden voor Hallo overslaan. Klik op **Bypass**.
7. Hallo ingaan tijdslimiet onmiddellijk geval Hallo-gebruiker die behoeften toosign in voordat Hallo eenmalig overslaan verloopt. 

### <a name="view-hello-one-time-bypass-report"></a>Weergave Hallo eenmalig overslaan rapport
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer aan de linkerkant hello, Active Directory.
3. Op de bovenste Selecteer Hallo **multi-factor Auth-Providers**. Hiermee wordt een lijst met uw multi-factor Auth-Providers.
4. Selecteer uw multi-factor Authentication-Provider en klik op **beheren** Hallo Hallo pagina onderaan in. Hello Azure multi-factor Authentication-beheerportal geopend.
5. Op Hallo Azure multi-factor Authentication-beheerportal op Hallo links onder A-rapport weergeven, klikt u op **eenmalige**.
6. Hallo datumbereik dat u wenst dat tooview in Hallo rapport opgeven. U kunt ook gebruikersnamen, telefoonnummers en de status van de gebruiker Hallo opgeven.
7. Klik op **Run**. Hiermee wordt een rapport van omleidingen. Klik op **tooCSV exporteren** desgewenst tooexport Hallo rapport.

## <a name="custom-voice-messages"></a>Aangepaste spraakberichten
Aangepaste spraakberichten kunnen u toouse uw eigen opnamen of begroeting voor verificatie in twee stappen. Deze kunnen worden gebruikt in toevoeging tooor tooreplace Hallo Microsoft records.

Voordat u begint rekening mee worden van de volgende Hallo:

* Hallo ondersteunde bestandsindelingen zijn .wav en .mp3.
* maximale bestandsgrootte Hallo is 5 MB.
* Verificatieberichten moet korter zijn dan 20 seconden. Iets langer dan dit ertoe leiden Hallo verificatie toofail dat kan omdat Hallo gebruiker reageert niet voordat het Hallo-bericht is voltooid, waardoor Hallo verificatie tootime uit.

### <a name="set-up-a-custom-message"></a>Een aangepast bericht instellen

Er zijn twee onderdelen toocreating uw aangepaste bericht. Eerst uploaden van het Hallo-bericht en vervolgens u inschakelen voor uw gebruikers.

tooupload uw aangepaste bericht:

1. Maak een aangepaste gesproken-bericht met een ondersteund Hallo-bestandsindelingen.
2. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
3. Navigeer toohello MFA-beheerportal per Hallo instructies Hallo boven aan deze pagina.
4. Klik in de Azure multi-factor Authentication-beheerportal hello, **spraakberichten** onder Hallo sectie configureren.
5. Op Hallo configureren: stem berichten pagina, klikt u op **Nieuw spraakbericht**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom1.png)
6. Op Hallo configureren: nieuwe spraakberichten pagina, klikt u op **geluidsbestanden beheren**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom2.png)
7. Op Hallo configureren: geluid pagina bestanden, klikt u op **geluidsbestand uploaden**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom3.png)
8. Op Hallo configureren: geluidsbestand uploaden, klikt u op **Bladeren** en tooyour spraakbericht navigeren, klikt u op **Open**.
9. Voeg een beschrijving toe en klik op **uploaden**.
10. Zodra deze is voltooid, wordt een bericht wordt bevestigd dat u hebt geüpload Hallo-bestand.

tooturn Hallo-bericht op voor uw gebruikers:

1. Klik aan de linkerkant Hallo op **spraakberichten**.
2. Hallo spraakberichten sectie, klik op **Nieuw spraakbericht**.
3. Hallo taal vervolgkeuzelijst, selecteer een taal.
4. Als dit bericht voor een specifieke toepassing is, geeft u het Hallo-toepassing.
5. Selecteer in de vervolgkeuzelijst voor berichttype Hallo, Hallo-bericht type toobe overschreven met uw nieuwe aangepaste bericht.
6. Selecteer in Hallo geluidsbestand vervolgkeuzelijst, Hallo geluidsbestand die u hebt geüpload in het eerste deel Hallo.
7. Klik op **Create**. Een bericht wordt bevestigd dat u hebt een spraakbericht gemaakt.
    ![Cloud](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Opslaan in cache in Azure multi-factor Authentication
Opslaan in cache kunt u tooset een bepaalde periode zodat latere authenticatiepogingen binnen deze periode automatisch slagen. Dit wordt hoofdzakelijk gebruikt wanneer de on-premises systemen zoals VPN verzenden meerdere aanvragen voor verificatie, terwijl de eerste aanvraag hello nog steeds uitgevoerd wordt. Hierdoor kunnen automatisch Hallo volgende aanvragen toosucceed nadat Hallo gebruiker Hallo eerste verificatie uitgevoerd is geslaagd. 

Opslaan in cache is niet bedoeld toobe gebruikt voor aanmeldingen tooAzure AD.

### <a name="set-up-caching"></a>Opslaan in cache instellen 
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-beheerportal per Hallo instructies Hallo boven aan deze pagina.
3. Klik in de Azure multi-factor Authentication-beheerportal hello, **opslaan in cache** onder Hallo sectie configureren.
4. Klik op Hallo configureren pagina caching op **nieuwe Cache**.
5. Selecteer Hallo cachetype en Hallo aantal cache-seconden. Klik op **Create**.

<center>![Cloud](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>Goedgekeurde IP-adressen
Goedgekeurde IP-adressen is een functie van Azure MFA die beheerders van een tenant beheerd of federatieve verificatie voor toobypass in twee stappen voor gebruikers die vanaf een lokaal intranet van het bedrijf Hallo aanmelden zich kunnen gebruiken. Deze functie is beschikbaar met Hallo volledige versie van Azure multi-factor Authentication, gratis versie niet Hallo voor beheerders. Zie voor meer informatie over hoe tooget volledige versie van Azure multi-factor Authentication Hallo [Azure multi-factor Authentication](multi-factor-authentication.md).

| Type van Azure AD-Tenant | Beschikbare goedgekeurde IP-opties |
|:--- |:--- |
| Managed |<li>Specifiek IP-adresbereiken: beheerders kunnen een bereik met IP-adressen die verificatie in twee stappen voor gebruikers die vanaf Hallo bedrijfsintranet aanmelden zich omzeilen opgeven.</li> |
| Federatieve |<li>Alle federatieve gebruikers: alle federatieve gebruikers die zich aanmeldt in uit binnen Hallo organisatie wordt overslaan verificatie in twee stappen met behulp van een claim uitgegeven door AD FS.</li><br><li>Specifiek IP-adresbereiken: beheerders kunnen een bereik met IP-adressen die verificatie in twee stappen voor gebruikers die vanaf Hallo bedrijfsintranet aanmelden zich omzeilen opgeven. |

Dit werkt alleen in binnen het intranet van een bedrijf overslaan. Als u alle federatieve gebruikers geselecteerd en een gebruiker zich aanmeldt via externe Hallo bedrijfsintranet, heeft die gebruiker tooauthenticate met verificatie in twee stappen ook als Hallo gebruiker een claim voor AD FS geeft. 

**De eindgebruikerservaring voor binnen corpnet:**

Wanneer de goedgekeurde IP-adressen is uitgeschakeld, verificatie in twee stappen is vereist voor de browser stromen en app-wachtwoorden vereist zijn voor oudere interactieve apps. 

Wanneer de goedgekeurde IP-adressen is ingeschakeld, wordt verificatie in twee stappen is *niet* vereist voor browser-stromen en app-wachtwoorden zijn *niet* vereist voor oudere rijke ClientApps, mits hello gebruiker nog niet al gemaakt een App-wachtwoord. Nadat een app-wachtwoord gebruikt wordt, blijft deze vereiste. 

**Eindgebruikerservaring buiten corpnet:**

Verificatie in twee stappen is vereist voor de browser stromen of goedgekeurde IP-adressen is ingeschakeld of niet, en app-wachtwoorden vereist zijn voor oudere interactieve apps. 

### <a name="tooenable-trusted-ips"></a>tooenable vertrouwde IP-adressen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-Service-instellingen pagina per Hallo instructies aan Hallo begin van dit artikel.
3. Op Hallo pagina Service-instellingen onder goedgekeurde IP-adressen, hebt u twee opties:
   
   * **Voor aanvragen van federatieve gebruikers die afkomstig zijn van mijn intranet** – Hallo selectievakje. Alle federatieve gebruikers die vanaf het bedrijfsnetwerk hello aanmelden zich wordt verificatie in twee stappen met behulp van een claim uitgegeven door AD FS overslaan.
   * **Voor aanvragen van een specifiek bereik van openbare IP-adressen** – Voer Hallo IP-adressen in het tekstvak Hallo opgegeven CIDR-notatie. Bijvoorbeeld: xxx.xxx.xxx.0/24 voor IP-adressen in Hallo bereik xxx.xxx.xxx.1 – xxx.xxx.xxx.254 of xxx.xxx.xxx.xxx/32 voor een enkel IP-adres. U kunt maximaal too50 IP-adresbereiken invoeren. Gebruikers die zich via deze IP-adressen aanmelden overslaan verificatie in twee stappen.
4. Klik op **Opslaan**.
5. Zodra het Hallo-updates zijn toegepast, klikt u op **sluiten**.

![Goedgekeurde IP-adressen](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>App-wachtwoorden
Bepaalde apps, zoals Office 2010 of ouder en Apple Mail ondersteunen geen verificatie in twee stappen. Ze zijn geconfigureerd tooaccept een tweede verificatie niet. toouse deze apps, moet u toouse 'app-wachtwoorden' in plaats van uw traditionele wachtwoord. Hallo app-wachtwoord kunt Hallo toepassing toobypass verificatie in twee stappen en blijven werken.

> [!NOTE]
> Moderne verificatie voor Hallo Office 2013-Clients
> 
> Office 2013-clients (inclusief Outlook) en nieuwere ondersteuning moderne verificatieprotocollen en kan worden ingeschakeld toowork met verificatie in twee stappen. Eenmaal is ingeschakeld, zijn app-wachtwoorden niet vereist voor deze clients.  Zie voor meer informatie [Office 2013 modern authentication openbare preview aangekondigd](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Belangrijke opmerkingen tooknow over app-wachtwoorden
Hallo Hieronder volgt een lijst met belangrijke dingen die u over app-wachtwoorden weten moet.

* App-wachtwoorden hoeft alleen toobe één keer per app worden opgegeven. Gebruikers bijhouden tookeep van deze heb en deze elke keer invoeren.
* Hallo werkelijke wachtwoord wordt automatisch gegenereerd en is niet geleverd door de gebruiker Hallo. Dit is omdat Hallo automatisch gegenereerde wachtwoorden moeilijker voor een aanvaller tooguess en beter te beveiligen.
* Er is een limiet van 40 wachtwoorden per gebruiker. 
* Apps die wachtwoorden en gebruik die in scenario's voor lokale mislukken kan omdat Hallo app-wachtwoord is niet bekend is buiten de organisatie Hallo-id in de cache. Een voorbeeld e-mailberichten voor het Exchange die zich on-premises maar Hallo gearchiveerde e-mail is in Hallo cloud. Hallo werkt hetzelfde wachtwoord niet.
* Zodra multi-factor authentication-server is ingeschakeld voor een gebruikersaccount, app-wachtwoorden kunnen worden gebruikt met de meeste niet-browserclients zoals Outlook en Lync, maar kunnen niet worden beheertaken uitgevoerd met behulp van app-wachtwoorden via niet-browsertoepassingen zoals Windows PowerShell, zelfs als die gebruiker over een Administrator-account.  Zorg ervoor dat u een service-account maken met een sterk wachtwoord toorun PowerShell-scripts en dat account voor verificatie in twee stappen niet inschakelt.

> [!WARNING]
> App-wachtwoorden werken niet in hybride omgevingen waarin clients communiceren met zowel on-premises en in de cloud autodiscover-eindpunten. Dit is omdat domeinwachtwoorden vereist tooauthenticate lokale zijn en app-wachtwoorden vereist tooauthenticate met Hallo cloud.

### <a name="naming-guidance-for-app-passwords"></a>Richtlijnen voor App-wachtwoorden voor de naamgeving
Namen van App-wachtwoord moeten overeenkomen met Hallo-apparaat waarop ze worden gebruikt. Als u een laptop met niet-browsertoepassingen zoals Outlook, Word en Excel hebt, bijvoorbeeld één app-wachtwoord met de naam Laptop maken en dit app-wachtwoord gebruiken in deze toepassingen. Vervolgens maakt u een andere app-wachtwoord met de naam Desktop voor Hallo dezelfde toepassingen op uw pc. 

Microsoft raadt u aan één appwachtwoord per apparaat, niet één appwachtwoord per toepassing maken.

### <a name="federated-sso-app-passwords"></a>App-wachtwoorden voor federatieve (SSO)
Azure AD biedt ondersteuning voor federatie (eenmalige aanmelding) met het lokale Windows Server Active Directory Domain Services (AD DS). Als uw organisatie is gefedereerd met Azure AD en u gaat toobe met Azure multi-factor Authentication en Hallo is volgende informatie over app-wachtwoorden belangrijk voor u. Deze sectie geldt alleen klanten toofederated (SSO).

* App-wachtwoorden worden geverifieerd door Azure AD en daarom federation overslaan. Federatie wordt alleen actief gebruikt bij het instellen van app-wachtwoorden.
* Voor federatieve gebruikers (SSO) gaan we nooit toohello identiteitsprovider (IdP), in tegenstelling tot Hallo passieve stroom. Hallo wachtwoorden worden opgeslagen in de organisatie Hallo-id. Als de gebruiker Hallo Hallo bedrijf verlaat, heeft dat info tooflow tooorganizational id met behulp van DirSync in realtime. Account uitschakelen/verwijderen kan duren voordat toothree uren toosync, vertragen uitschakelen/verwijderen van App-wachtwoord in Azure AD.
* On-premises instellingen voor toegangsbeheer van client worden niet herkend door het app-wachtwoord.
* Er is geen lokale verificatie mogelijkheid logboekregistratie/controle is beschikbaar voor App-wachtwoord.
* Bepaalde geavanceerde architectuur ontwerpen moet mogelijk een combinatie van organisatie-gebruikersnaam en wachtwoorden app bij het gebruik van verificatie in twee stappen met clients, afhankelijk van waar ze verifiëren. Voor clients die worden geverifieerd bij een on-premises infrastructuur, gebruikt u een organisatie-gebruikersnaam en wachtwoord. Voor clients die worden geverifieerd bij Azure AD, zou u Hallo app-wachtwoord gebruiken.

  Stel bijvoorbeeld dat u hebt een architectuur die uit de volgende Hallo bestaat:

  * U federeert uw lokale exemplaar van Active Directory met Azure AD
  * U via Exchange online
  * U gebruikt Lync specifiek on-premises
  * U gebruikt Azure multi-factor Authentication

  ![Proofup](./media/multi-factor-authentication-whats-next/federated.png)

  In dergelijke gevallen moet u doen Hallo volgende:

  * Als u zich aanmeldt-in tooLync, gebruikt u de gebruikersnaam en wachtwoord van uw organisatie.
  * Wanneer u probeert het Hallo-adresboek tooaccess via een Outlook-client die verbinding tooExchange online maakt, gebruikt u een app-wachtwoord.

### <a name="allow-app-password-creation"></a>Maken van app-wachtwoord toestaan
Gebruikers kunnen geen app-wachtwoorden maken standaard. Deze functie moet zijn ingeschakeld. tooallow gebruikers Hallo mogelijkheid toocreate app-wachtwoorden, gebruikt u Hallo procedure te volgen:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-Service-instellingen pagina per Hallo instructies aan Hallo begin van dit artikel.
3. Selecteer het keuzerondje Hallo naast te**kunnen gebruikers toocreate app-wachtwoorden toosign in niet-browsertoepassingen**.

![App-wachtwoorden maken](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>App-wachtwoorden maken
Gebruikers kunnen app-wachtwoorden maken tijdens de initiële inschrijving. Een optie achter Hallo Hallo registratieproces waarmee ze de app-wachtwoorden toocreate wordt verstrekt.

Gebruikers kunnen ook app-wachtwoorden maken na de registratie door hun instellingen in hello Azure portal of Hallo Office 365-portal te wijzigen. Zie voor meer informatie en gedetailleerde stappen voor uw gebruikers [wat zijn app-wachtwoorden in Azure multi-factor Authentication](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Houd er rekening mee multi-factor Authentication voor apparaten die gebruikers vertrouwen
Onthoud multi-factor Authentication voor apparaten en browsers dat gebruikers vertrouwensrelatie een gratis functie voor alle gebruikers van MFA is. Hiermee kunt u toogive gebruikers Hallo optie tooby pass MFA voor een bepaald aantal dagen na het uitvoeren van een geslaagde aanmelden met MFA. Dit kan de bruikbaarheid verbeteren door het aantal keren dat een gebruiker verificatie in twee stappen op Hallo uitvoeren kan Hallo minimaliseren hetzelfde apparaat.

Echter, als een account of apparaat is geknoeid, onthoud MFA voor vertrouwde apparaten kan invloed hebben op beveiliging. Als een zakelijke account wordt aangetast of een vertrouwd apparaat is zoekgeraakt of gestolen, moet u [multi-factor Authentication herstellen op alle apparaten](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Deze actie intrekken Hallo vertrouwde status van alle apparaten en Hallo-gebruiker is vereist tooperform verificatie in twee stappen opnieuw. U kunt ook opgeven dat uw gebruikers toorestore MFA op hun eigen apparaten met instructies voor het Hallo in [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Hoe werkt het?

Onthouden van multi-factor Authentication werkt door het instellen van een permanente cookie op Hallo browser wanneer een gebruiker gecontroleerd Hallo ' niet opnieuw vragen voor **X** dagen ' vak bij het aanmelden. Hallo gebruiker niet gevraagd voor MFA opnieuw in die browser totdat Hallo cookie verloopt. Als Hallo gebruiker opent een andere browser op Hallo hetzelfde apparaat of wist hun cookies ze na vragen aan gebruiker tooverify weer worden. 

Hallo ' niet opnieuw vragen voor **X** dagen ' checkbox wordt niet weergegeven op niet-browsertoepassingen, al dan niet ondersteuning van moderne verificatie. Deze apps gebruik vernieuwen van tokens die nieuwe toegangstokens om het uur leveren. Wanneer een vernieuwingstoken wordt gevalideerd, valt Azure AD-controleert of de laatste verificatie van de tijd in twee stappen Hallo is uitgevoerd binnen aantal dagen Hallo geconfigureerd. 

Daarom MFA onthouden op vertrouwde apparaten vermindert het aantal authenticaties op web-apps (die normaal gesproken vragen telkens) Hallo maar toeneemt Hallo aantal authenticaties voor verificatieclients (die normaal gesproken vragen om de 90 dagen).

> [!NOTE]
>Deze functie is niet compatibel met 'Aangemeld blijven' Hallo-functie van AD FS wanneer gebruikers de verificatie in twee stappen voor AD FS via hello Azure MFA-Server of een oplossing van derden MFA uitvoert. Als uw gebruikers "Aangemeld blijven" Selecteer op de AD FS en ook voor MFA hun apparaat als vertrouwd markeren, niet kunnen tooverify worden nadat Hallo 'MFA onthouden' het aantal dagen is verlopen. Azure AD de verificatie van een nieuwe in twee stappen aanvraagt, maar de AD FS retourneert een token met het oorspronkelijke MFA claim Hallo en de datum in plaats van het uitvoeren van verificatie in twee stappen weer. Hiermee stelt u uit een lus verificatie tussen Azure AD en AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Onthoud dat multi-factor authentication inschakelen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-Service-instellingen pagina per Hallo instructies aan Hallo begin van dit artikel.
3. Op de pagina Service-instellingen Hallo gebruikersinstellingen apparaat onder beheren, moet u controleren Hallo **tooremember meervoudige verificatie van gebruikers toestaan op vertrouwde apparaten** vak.
   ![Onthouden van apparaten](./media/multi-factor-authentication-whats-next/remember.png)
4. Hallo aantal dagen dat u de verificatie van tooallow Hallo vertrouwde apparaten toobypass in twee stappen wilt instellen. Hallo standaardwaarde is 14 dagen.
5. Klik op **Opslaan**.
6. Klik op **Sluiten**.

### <a name="mark-a-device-as-trusted"></a>Een apparaat als vertrouwd is ingeschakeld

Zodra u deze functie inschakelt, gebruikers wilt markeren een apparaat als vertrouwde wanneer ze zich aanmelden door te controleren **niet opnieuw vragen**.

![Niet opnieuw vragen - schermafbeelding](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Selecteerbare verificatiemethoden
U kunt kiezen welke verificatiemethoden zijn beschikbaar voor uw gebruikers. Hallo in de volgende tabel geeft een kort overzicht van elke methode.

Wanneer uw gebruikers hun account voor MFA registreren, kies ze hun methode voorkeursoptie voor verificatie buiten het Hallo-opties die u hebt ingeschakeld. Hallo-richtlijnen voor het registratieproces wordt beschreven in [Mijn account voor verificatie in twee stappen instellen](multi-factor-authentication-end-user-first-time.md)

| Methode | Beschrijving |
|:--- |:--- |
| Aanroep toophone |Een geautomatiseerd telefoongesprek plaatst. Hallo gebruiker antwoorden Hallo aanroepen en drukt # in op Hallo phone toetsenblok tooauthenticate. Dit telefoonnummer is niet gesynchroniseerd tooon lokale Active Directory. |
| Tekst bericht toophone |Verzendt een SMS-bericht met een verificatiecode. Hallo-gebruiker is na vragen aan gebruiker tooeither antwoord toohello SMS-bericht met de Hallo verificatiecode of tooenter Hallo verificatiecode in Hallo-aanmelden-interface. |
| Melding via de mobiele app |Een push notification tooyour telefoon of geregistreerd apparaat verzendt. Hallo gebruiker bekijkt hello melding en **controleren** toocomplete verificatie. <br>Hallo Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Verificatiecode via mobiele app |Hallo Microsoft Authenticator-app genereert elke 30 seconden een nieuwe OATH-verificatiecode uit. Hallo gebruiker voert deze bevestigingscode in Hallo-aanmelden-interface.<br>Hallo Microsoft Authenticator-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Hoe verificatiemethoden tooenable-of uitschakelen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello MFA-Service-instellingen pagina per Hallo instructies aan Hallo begin van dit artikel.
3. Op Hallo pagina Service-instellingen onder verificatie-opties selecteren/uitschakelen Hallo-opties die u wenst dat toouse.
   ![Verificatie-opties](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Klik op **Opslaan**.
5. Klik op **Sluiten**.

