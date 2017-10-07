---
title: Azure AD SSPR met wachtwoord terugschrijven | Microsoft Docs
description: Met behulp van Azure AD en Azure AD Connect toowriteback wachtwoorden tooon-premises directory
services: active-directory
keywords: Wachtwoordbeheer Active directory, wachtwoordbeheer, Azure AD self service voor wachtwoordherstel
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Overzicht van de Write-back van wachtwoord

Wachtwoord terugschrijven kunt dat u Azure AD tooconfigure toowrite wachtwoorden een back-tooyou op lokale Active Directory. Worden Hallo nodig tooset up verwijderd en een gecompliceerde on-premises-oplossing voor het opnieuw instellen van selfservice voor wachtwoordherstel te beheren, en biedt een handige manier cloud-gebaseerde voor uw gebruikers tooreset hun on-premises wachtwoorden waar ze ook zijn. Wachtwoord terugschrijven is een onderdeel van [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) die kunnen worden ingeschakeld en gebruikt door bestaande Premium-abonnees [Azure Active Directory-edities](active-directory-editions.md).

Wachtwoord terugschrijven biedt Hallo volgende kenmerken

* **Vertraging feedback nul** -wachtwoord terugschrijven is een synchrone bewerking. Uw gebruikers zijn onmiddellijk een melding als hun wachtwoord niet voldeed aan beleid of is niet mogelijk toobe opnieuw instellen of gewijzigd voor een of andere reden.
* **Ondersteunt het opnieuw instellen van wachtwoorden voor gebruikers met AD FS of andere technologieën federation** -waaraan wachtwoord terugschrijven zolang hello federatieve gebruikersaccounts zijn gesynchroniseerd naar Azure AD-tenant zijn kunnen toomanage hun on-premises AD dat wachtwoorden van Hallo cloud.
* **Ondersteunt het opnieuw instellen van wachtwoorden voor gebruikers met behulp van [wachtwoordhashsynchronisatie](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  : wanneer Hallo wachtwoord opnieuw instellen van service detecteert dat een gesynchroniseerde gebruikersaccount is ingeschakeld voor wachtwoordhashsynchronisatie, we beide dit account opnieuw instellen on-premises en tegelijkertijd wachtwoord cloud.
* **Ondersteunt het wijzigen van wachtwoorden van Hallo toegang Configuratiescherm en Office 365** : wanneer federatieve of wachtwoord gesynchroniseerd toochange van gebruikers afkomstig zijn van hun wachtwoorden verlopen of niet is verlopen, we schrijven die wachtwoorden back tooyour lokale AD-omgeving.
* **Ondersteunt het terugschrijven van wachtwoorden wanneer een beheerder niet opnieuw van instellen Azure-portal Hallo** : wanneer een beheerder het wachtwoord van een gebruiker in Hallo stelt [Azure-portal](https://portal.azure.com), als die gebruiker is gefedereerd of het wachtwoord is gesynchroniseerd, moet we Hallo instellen wachtwoord Hallo beheerder wordt op uw lokale AD ook geselecteerd. Dit wordt momenteel niet ondersteund in Hallo Office-beheerportal.
* **Dwingt uw on-premises AD-wachtwoordbeleid** : wanneer een gebruiker het wachtwoord opnieuw instelt zorgen wij ervoor dat het voldoet aan uw on-premises Active Directory-beleid voordat u deze toothat directory doorvoert. Dit omvat de geschiedenis, complexiteit, leeftijd, wachtwoordfilters en alle andere wachtwoordbeperkingen die u hebt gedefinieerd in uw lokale AD.
* **Alle firewallregels voor binnenkomend verkeer geen vereist** -wachtwoord terugschrijven een Azure Service Bus relay gebruikt als een onderliggende communicatiekanaal, wat betekent dat u geen tooopen poorten voor inkomend verkeer op uw firewall voor deze functie toowork hebt.
* **Wordt niet ondersteund voor gebruikersaccounts die zijn opgeslagen in de beveiligde groepen in uw lokale Active Directory** - Zie voor meer informatie over de beveiligde groepen [beveiligde Accounts en groepen in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>De werking van wachtwoord terugschrijven

Wanneer een federatieve of het wachtwoord-hash gesynchroniseerd wordt gebruiker tooreset wordt geleverd of hun wachtwoord wijzigen in Hallo cloud, gebeurt Hallo volgende:

1. We controleren toosee wat voor soort wachtwoord Hallo gebruiker heeft.
    * Als we wordt Hallo wachtwoord on-premises beheerd
        * We controleren als hello Write-back-service is en uitgevoerd, als het we Hallo aan gebruiker laten gaan
        * Als Hallo Write-back-service niet is, we Hallo gebruiker melden dat hun wachtwoord kan niet worden nu opnieuw instellen
2. Vervolgens Hallo gebruiker de juiste verificatiepoorten Hallo en doorgegeven welkomstscherm opnieuw instellen van wachtwoord is bereikt.
3. Hallo-gebruiker selecteert een nieuw wachtwoord en bevestigt het.
4. Wanneer u op verzenden klikt, versleutelen we Hallo leesbare wachtwoord met een symmetrische sleutel die is gemaakt tijdens het Hallo Write-back-installatieproces.
5. Na versleuteling Hallo wachtwoord, opnemen we in een nettolading die wordt verzonden via een HTTPS-kanaal tooyour tenantspecifieke service bus relay (die we ook voor u ingesteld tijdens Hallo Write-back-installatieproces). Deze relay is beveiligd met een willekeurig gegenereerd wachtwoord dat alleen de lokale installatie kent.
6. Zodra het Hallo-bericht servicebus bereikt, hello wachtwoord opnieuw instellen van endpoint automatisch ontwaakt en ziet dat er een aanvraag in behandeling.
7. Hallo-service zoekt vervolgens naar Hallo gebruiker betrokken via ankerkenmerk Hallo-cloud. Voor deze toosucceed lookup:

    * Hallo gebruikersobject moet aanwezig zijn in AD connectorruimte Hallo
    * Hallo gebruikersobject moet gekoppelde toohello bijbehorende MV-object worden
    * Hallo gebruikersobject moet gekoppelde toohello bijbehorende AAD-connectorobject.
    * Hallo koppeling van AD-connector object tooMV moet hebben Hallo synchronisatieregel `Microsoft.InfromADUserAccountEnabled.xxx` op Hallo-koppeling. <br> <br>
    Hallo-oproep uit Hallo cloud binnenkomt, Hallo synchronisatie-engine gebruikt Hallo cloudAnchor kenmerk toolook Hallo AAD-connector ruimte object, volgt Hallo link back toohello MV-object als volgt Hallo link back toohello AD-object. Omdat er mogelijk meerdere AD-objecten (met meerdere forests) voor dezelfde gebruiker Hallo synchronisatie-engine is afhankelijk van Hallo Hallo `Microsoft.InfromADUserAccountEnabled.xxx` koppeling toopick Hallo een te corrigeren.

    > [!Note]
    > Als gevolg van deze logica moet Azure AD Connect kunnen toocommunicate Hello PDC-Emulator voor wachtwoord terugschrijven toowork. Als u dit handmatig tooenable nodig, kunt u Azure AD Connect toohello PDC-Emulator door met de rechtermuisknop op Hallo **eigenschappen** Hallo Active Directory-synchronisatie connector, selecteren **configureren mappartities**. Van daaruit zoekt Hallo **verbinding domeincontrollerinstellingen** sectie en Hallo selectievakje met de titel **alleen gebruiken voorkeurs-domeincontrollers**. Zelfs als Hallo primaire dat domeincontroller niet een PDC-emulator is, probeert Azure AD Connect tooconnect toohello PDC voor write-back van wachtwoord.

8. Als het gebruikersaccount hello wordt gevonden, proberen we tooreset Hallo wachtwoord rechtstreeks in de juiste AD-forest Hallo.
9. Als Hallo wachtwoord set-bewerking geslaagd is, zien we Hallo gebruikers dat hun wachtwoord is gewijzigd.
    > [!NOTE]
    > In geval van Hallo wanneer het wachtwoord van gebruiker Hallo gesynchroniseerde tooAzure AD met Wachtwoordsynchronisatie kans dat beleid voor on-premises wachtwoord Hallo zwakkere dan Hallo cloud wachtwoordbeleid is is. In dit geval afdwingen we nog steeds van elk beleid Hallo on-premises is en wachtwoord in plaats daarvan hash synchronisatie toosynchronize Hallo hash van dat wachtwoord toegestaan. Dit zorgt ervoor dat het beleid van uw on-premises wordt afgedwongen op Hallo cloud, ongeacht als u de synchronisatie of federation tooprovide wachtwoord gebruikt eenmalige aanmelding.

10. Als Hallo wachtwoord ingesteld mislukt, we Hallo fout toohello gebruiker retourneren en laat ze probeer het opnieuw.
    * Hallo-bewerking kan mislukken vanwege de volgende Hallo
        * Hallo-service is niet actief
        * ze geselecteerde Hallo-wachtwoord voldeed niet aan beleid van organisatie
        * Er is geen Hallo gebruiker gevonden in Hallo lokale AD

    We hebben een specifieke bericht voor veel van deze gevallen en Hallo gebruiker vertellen wat ze kunnen doen tooresolve Hallo probleem.

## <a name="configuring-password-writeback"></a>Wachtwoord terugschrijven configureren

Het is raadzaam dat u het Hallo-functie voor automatisch bijwerken van [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) als u wilt dat toouse wachtwoord terugschrijven.

DirSync en Azure AD Sync zijn niet langer ondersteund middel aan voor het inschakelen van wachtwoord terugschrijven Hallo artikel [upgraden van DirSync en Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) heeft meer informatie toohelp met de overgang.

Hallo onderstaande stappen wordt ervan uitgegaan dat u Azure AD Connect al hebt geconfigureerd in uw omgeving met Hallo [Express](./connect/active-directory-aadconnect-get-started-express.md) of [aangepaste](./connect/active-directory-aadconnect-get-started-custom.md) instellingen.

1. tooconfigure en schakel wachtwoord terugschrijven aanmelden tooyour Azure AD Connect-server en start Hallo **Azure AD Connect** configuratiewizard.
2. Klik op het welkomstscherm Hallo **configureren**.
3. Op Hallo aanvullende taken Klik scherm **aanpassen Synchronisatieopties** en kies vervolgens **volgende**.
4. Voer de referenties van een globale beheerder op het welkomstscherm Connect tooAzure AD en kies **volgende**.
5. Op Hallo verbinding maken met de mappen en het domein en OE filteren schermen kunt u **volgende**.
6. Op het welkomstscherm van optionele functies selectievakje Hallo naast te**wachtwoord terugschrijven** en klik op **volgende**.
   ![Wachtwoord terugschrijven in Azure AD Connect inschakelen][Writeback]
7. Klik op gereed tooconfigure welkomstscherm **configureren** en wachten op Hallo proces toocomplete.
8. Wanneer er configuratie voltooien klikt u op **afsluiten**

## <a name="licensing-requirements-for-password-writeback"></a>Licentievereisten voor write-back van wachtwoord

Voor informatie over licentieverlening, Zie Hallo onderwerp [licenties nodig zijn voor write-back van wachtwoord](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) of Hallo na sites

* [Azure Active Directory-prijzen site](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Beveiligde productief Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Lokale verificatiemodi ondersteund voor write-back van wachtwoord

Wachtwoord terugschrijven werkt voor Hallo gebruikerstypen wachtwoord te volgen:

* **Alleen in de cloud gebruikers**: wachtwoord terugschrijven is niet van toepassing in dit geval, omdat er geen on-premises-wachtwoord
* **Het wachtwoord is gesynchroniseerd gebruikers**: wachtwoord terugschrijven ondersteund
* **Federatieve gebruikers**: wachtwoord terugschrijven ondersteund
* **Pass through-verificatie gebruikers**: wachtwoord terugschrijven ondersteund

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Gebruikers- en Admin bewerkingen die worden ondersteund voor write-back van wachtwoord

Wachtwoorden worden teruggeschreven in alle Hallo volgende situaties:

* **Ondersteunde bewerkingen van eindgebruikers**
  * Alle eindgebruikers selfservice vrijwillige bewerking wachtwoord wijzigen
  * Eindgebruikers selfservice force wijzigen wachtwoord bewerkingen (bijvoorbeeld verlopen van wachtwoorden)
  * Alle door eindgebruikers selfservice voor wachtwoordherstel die afkomstig zijn van Hallo [Portal voor wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com)
* **Ondersteunde bewerkingen van de beheerder**
  * Een beheerder selfservice vrijwillige bewerking wachtwoord wijzigen
  * Een beheerder selfservice force wijzigen wachtwoord bewerking (bijvoorbeeld verlopen van wachtwoorden)
  * Een beheerder selfservice voor wachtwoordherstel die afkomstig zijn van Hallo [Portal voor wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com)
  * Een beheerder worden geïnitieerd door eindgebruikers voor wachtwoordherstel van Hallo [klassieke Azure-portal](https://manage.windowsazure.com)
  * Een beheerder worden geïnitieerd door eindgebruikers voor wachtwoordherstel van Hallo [Azure-portal](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Gebruikers- en Admin bewerkingen worden niet ondersteund voor write-back van wachtwoord

De wachtwoorden **niet** geschreven in een van de volgende situaties Hallo:

* **Niet-ondersteunde bewerkingen van eindgebruikers**
  * Iedere gebruiker opnieuw instellen van hun eigen wachtwoord met behulp van PowerShell v1, v2 of hello Azure AD Graph API
* **Niet-ondersteunde bewerkingen van de beheerder**
  * Een beheerder worden geïnitieerd door eindgebruikers voor wachtwoordherstel van Hallo [Office-beheerportal](https://portal.office.com)
  * Een beheerder worden geïnitieerd door eindgebruikers voor wachtwoordherstel van PowerShell v1, v2 of hello Azure AD Graph API

Terwijl we tooremove deze beperkingen werkt, hoeft u niet een specifieke tijdlijn die we nog kunt delen.

## <a name="password-writeback-security-model"></a>Wachtwoord terugschrijven beveiligingsmodel

Wachtwoord terugschrijven is een maximaal beveiligde service.  tooensure die uw gegevens worden beschermd, we inschakelen voor een beveiligingsmodel 4 lagen die hieronder wordt beschreven.

* **Tenant-specifieke service bus relay**
  * Bij het instellen van de service hello, u stelt een tenantspecifieke service bus relay die wordt beveiligd door een willekeurig gegenereerd sterk wachtwoord dat Microsoft nooit toegang tot heeft.
* **De versleutelingssleutel vergrendelde, cryptografisch sterk wachtwoord**
  * Nadat Hallo service bus relay is gemaakt, maken we een sterke symmetrische sleutel gebruiken we tooencrypt Hallo wachtwoord als ze via de kabel Hallo afkomstig zijn. Deze sleutel zich alleen in geheime archief Hallo cloud, die sterk is vergrendeld en gecontroleerd, net zoals een wachtwoord in Hallo directory van uw bedrijf.
* **De standaard TLS bedrijfstak**
  1. Wanneer u een wachtwoord opnieuw instellen of wijzigen bewerking plaatsvindt in de cloud hello, we nemen Hallo leesbare wachtwoord coderen met uw openbare sleutel.
  2. We vervolgens plaatsen die in een HTTPS-mailbericht wordt verzonden via een versleuteld kanaal met Microsoft SSL-certificaten klant tooyour service bus relay.
  3. Nadat het Hallo-bericht binnenkomt naar uw lokale agent Service Bus de slaapstand worden opgeheven en verifieert tooService met behulp van Bus Hallo sterk wachtwoord dat eerder is gegenereerd.
  4. Lokale agent versleutelde het Hallo-bericht opneemt, ontsleutelt met behulp van Hallo persoonlijke sleutel die wordt gegenereerd.
  5. Lokale agent probeert vervolgens tooset Hallo wachtwoord via Hallo SetPassword API van AD DS.
     * Deze stap is wat we tooenforce kunnen uw AD wachtwoordbeleid on-premises (complexiteit, leeftijd, geschiedenis, filters, enzovoort) in de cloud Hallo.
* **Het verloopbeleid bericht** 
  * Als het Hallo-bericht bevindt zich in de Service Bus omdat uw on-premises service niet actief is, wordt beëindigd en worden verwijderd na enkele minuten tooincrease beveiliging nog verder.

### <a name="password-writeback-encryption-details"></a>Wachtwoord terugschrijven versleuteling details

stappen voor het versleutelen Hallo een aanvraag voor wachtwoordherstel doorloopt nadat een gebruiker verzendt, voordat deze in uw on-premises omgeving, tooensure maximale service betrouwbaarheid en beveiliging binnenkomt, worden hieronder beschreven.

* **Stap 1 - wachtwoordversleuteling met 2048-bits RSA-sleutel** - zodra een gebruiker verzendt een wachtwoord toobe teruggeschreven tooon-premises eerst Hallo ingediende wachtwoord zelf is versleuteld met een 2048-bits RSA-sleutel.
* **Stap 2: versleuteling van het pakket op met AES-GCM** - en volledige pakket hello (wachtwoord + vereiste metagegevens) is versleuteld met AES-GCM. Dit voorkomt dat iedereen met directe toegang toohello onderliggende ServiceBus-kanaal weergeven/gemanipuleerde Hallo inhoud.
* **Stap 3: alle communicatie vindt plaats via TLS / SSL** -alle Hallo communicatie met Service Bus gebeurt in een SSL/TLS-kanaal. Dit beveiligt Hallo inhoud van niet-geautoriseerde 3e partijen.
* **Automatische sleutelrollover om de zes maanden** : automatisch elke 6 maanden of elke keer dat wachtwoord terugschrijven is uitgeschakeld of opnieuw worden ingeschakeld op Azure AD Connect we rollover deze sleutels tooensure maximale servicebeveiliging en veiligheid.

### <a name="password-writeback-bandwidth-usage"></a>Wachtwoord terugschrijven bandbreedtegebruik

Wachtwoord terugschrijven is een lage bandbreedte-service die aanvragen back toohello lokale agent alleen onder de volgende omstandigheden Hallo verzendt:

1. Twee berichten worden verzonden wanneer het in- of uitschakelen van de functie Hallo met Azure AD Connect.
2. Een bericht verzonden elke vijf minuten als een heartbeat-service voor zolang Hallo-service wordt uitgevoerd.
3. Twee berichten worden verzonden op elk moment een nieuw wachtwoord wordt ingediend
    * Eerste bericht, als een aanvraag tooperform Hallo-bewerking
    * Tweede bericht die Hallo resultaat van Hallo-bewerking bevat en worden verzonden in Hallo volgende omstandigheden:
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een gebruiker zelf uw wachtwoord opnieuw instellen.
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een wachtwoordwijziging van gebruiker.
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een beheerder geïnitieerde gebruikerswachtwoord opnieuw instellen (van alleen hello Azure admin portals).

#### <a name="message-size-and-bandwidth-considerations"></a>Overwegingen voor het grootte en bandbreedte van het bericht

Hallo-grootte van elk van die hierboven worden beschreven het Hallo-bericht is doorgaans onder 1 kb, zelfs onder extreme laadt, Hallo wachtwoord terugschrijven service zelf verbruikt enkele kilobits per seconde van de bandbreedte. Omdat elk bericht wordt verzonden in real-time, alleen indien vereist door een updatebewerking wachtwoord en omdat de berichtgrootte Hallo zo klein is, Hallo bandbreedtegebruik van Hallo Write-back-capaciteit is in feite te klein toohave echt merkbare impact.

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Wachtwoord terugschrijven in Azure AD Connect inschakelen"
