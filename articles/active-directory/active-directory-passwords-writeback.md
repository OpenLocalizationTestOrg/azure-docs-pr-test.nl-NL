---
title: Azure AD SSPR met wachtwoord terugschrijven | Microsoft Docs
description: Met behulp van Azure AD en Azure AD Connect wachtwoorden terugschrijven naar on-premises directory
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
ms.openlocfilehash: 6b195fdcce17184628acd98a686520528a6dadd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="password-writeback-overview"></a>Overzicht van de Write-back van wachtwoord

Wachtwoord terugschrijven kunt u Azure AD voor het schrijven van wachtwoorden met u op lokale Active Directory configureren. Verwijdert deze de noodzaak instellen en beheren van een complexe on-premises-oplossing zelf uw wachtwoord opnieuw instellen en biedt een handige manier cloud-gebaseerde voor uw gebruikers opnieuw in te stellen hun on-premises wachtwoorden waar ze ook zijn. Wachtwoord terugschrijven is een onderdeel van [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) die kunnen worden ingeschakeld en gebruikt door bestaande Premium-abonnees [Azure Active Directory-edities](active-directory-editions.md).

Wachtwoord terugschrijven biedt de volgende functies

* **Vertraging feedback nul** -wachtwoord terugschrijven is een synchrone bewerking. Uw gebruikers zijn onmiddellijk een melding als hun wachtwoord niet voldeed aan beleid of kon niet worden ingesteld of gewijzigd voor een of andere reden.
* **Ondersteunt het opnieuw instellen van wachtwoorden voor gebruikers met AD FS of andere technologieën federation** -met terugschrijven van wachtwoorden, zolang de federatieve gebruikersaccounts worden gesynchroniseerd naar Azure AD-tenant ze kunnen voor het beheren van hun on-premises AD-wachtwoorden vanuit de cloud.
* **Ondersteunt het opnieuw instellen van wachtwoorden voor gebruikers met behulp van [wachtwoordhashsynchronisatie](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  : wanneer u het wachtwoord opnieuw instellen van service detecteert dat een gesynchroniseerde gebruikersaccount is ingeschakeld voor wachtwoordhashsynchronisatie, we tegelijkertijd zowel dit account on-premises en cloud-wachtwoord instellen.
* **Ondersteunt het wijzigen van wachtwoorden van het toegangsvenster en Office 365** : wanneer federatieve of wachtwoord is gesynchroniseerd gebruikers hun wachtwoorden verlopen of niet-verlopen wijzigen we deze wachtwoorden terugschrijven naar uw lokale AD-omgeving worden geleverd.
* **Ondersteunt het terugschrijven van wachtwoorden wanneer een beheerder deze opnieuw vanuit de Azure-portal** : wanneer een beheerder stelt het wachtwoord van een gebruiker in de [Azure-portal](https://portal.azure.com), als die gebruiker is gefedereerd of wachtwoord is gesynchroniseerd, moet we het wachtwoord dat de beheerder wordt geselecteerd op uw lokale AD ook is ingesteld. Dit wordt momenteel niet ondersteund in de Office-beheerportal.
* **Dwingt uw on-premises AD-wachtwoordbeleid** : wanneer een gebruiker het wachtwoord opnieuw instelt zorgen wij ervoor dat het voldoet aan uw on-premises Active Directory-beleid alvorens toe te wijzen aan die directory. Dit omvat de geschiedenis, complexiteit, leeftijd, wachtwoordfilters en alle andere wachtwoordbeperkingen die u hebt gedefinieerd in uw lokale AD.
* **Alle firewallregels voor binnenkomend verkeer geen vereist** -wachtwoord terugschrijven een Azure Service Bus relay gebruikt als een onderliggende communicatiekanaal, wat betekent dat u niet hoeft te openen van poorten voor inkomend verkeer op uw firewall voor deze functie te gebruiken.
* **Wordt niet ondersteund voor gebruikersaccounts die zijn opgeslagen in de beveiligde groepen in uw lokale Active Directory** - Zie voor meer informatie over de beveiligde groepen [beveiligde Accounts en groepen in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>De werking van wachtwoord terugschrijven

Wanneer een federatieve of het wachtwoord-hash gesynchroniseerde gebruiker wordt geleverd opnieuw instellen of hun wachtwoord wijzigen in de cloud, gebeurt het volgende:

1. We controleren om te zien welke type wachtwoord op de gebruiker heeft.
    * Als we wordt het wachtwoord beheerd on-premises
        * We controleren of als de Write-back-service is en wordt uitgevoerd, als het, we aan de gebruiker laten gaan
        * Als de Write-back-service niet is, wordt de gebruiker melden dat hun wachtwoord kan niet worden nu opnieuw instellen
2. Vervolgens de gebruiker geeft de juiste verificatie-poorten en het wachtwoord opnieuw instellen van scherm bereikt.
3. De gebruiker selecteert een nieuw wachtwoord en bevestigt het.
4. Wanneer u op verzenden klikt, wordt het leesbare wachtwoord versleutelen met een symmetrische sleutel die is gemaakt tijdens de installatie Write-back van.
5. Nadat het wachtwoord versleutelt, opnemen we in een nettolading die via een HTTPS-kanaal wordt verzonden naar uw tenantspecifieke service bus relay (die we ook voor u ingesteld tijdens de installatie writeback). Deze relay is beveiligd met een willekeurig gegenereerd wachtwoord dat alleen de lokale installatie kent.
6. Zodra het bericht servicebus bereikt, wordt het wachtwoord opnieuw instellen van eindpunt automatisch ontwaakt en ziet dat er een aanvraag in behandeling.
7. De service zoekt vervolgens naar de gebruiker in kwestie met behulp van de cloud ankerkenmerk. Voor deze zoekactie mislukt:

    * Het gebruikersobject moet bestaan in de ruimte van AD-connector
    * Het gebruikersobject moet worden gekoppeld aan het bijbehorende MV-object
    * Het gebruikersobject moet worden gekoppeld aan het bijbehorende object van de AAD-connector.
    * De koppeling van AD-connector-object naar MV moet hebben tot de synchronisatieregel `Microsoft.InfromADUserAccountEnabled.xxx` op de koppeling. <br> <br>
    Wanneer de aanroep wordt geleverd vanuit de cloud, wordt de synchronisatie-engine gebruikt het kenmerk cloudAnchor om het object in de ruimte van AAD-connector, volgt de koppeling terug naar de MV-object te zoeken en vervolgens voert de koppeling naar het AD-object. Omdat het is mogelijk meerdere AD-objecten (met meerdere forests) voor dezelfde gebruiker, de synchronisatie-engine is afhankelijk van de `Microsoft.InfromADUserAccountEnabled.xxx` koppeling naar de juiste account kiezen.

    > [!Note]
    > Als gevolg van deze logica moet Azure AD Connect kunnen communiceren met de PDC-Emulator voor write-back van wachtwoord om te werken. Als u deze handmatig inschakelt moet, kunt u Azure AD Connect aansluiten op de PDC-Emulator door met de rechtermuisknop op de **eigenschappen** van de Active Directory-synchronisatie-connector te selecteren **mappartities configureren**. Ga van daaruit naar de sectie **Verbindingsinstellingen voor domeincontrollers** en schakel het vakje **Alleen voorkeursdomeincontrollers gebruiken** in. Zelfs als de voorkeur DC niet een PDC-emulator, probeert Azure AD Connect verbinding maken met de PDC voor write-back van wachtwoord.

8. Als het gebruikersaccount wordt gevonden, wordt er geprobeerd voor wachtwoordherstel rechtstreeks in de juiste AD-forest.
9. Als het wachtwoord set-bewerking geslaagd is, zien we de gebruiker dat het wachtwoord is gewijzigd.
    > [!NOTE]
    > In het geval wanneer het wachtwoord van de gebruiker is gesynchroniseerd naar Azure AD met Wachtwoordsynchronisatie is een kans dat het lokale wachtwoordbeleid zwakkere dan de cloud-wachtwoordbeleid is. In dit geval afdwingen we nog steeds van wat het beleid van de on-premises is en in plaats daarvan synchronisatie van wachtwoordhash om te synchroniseren van de hash van dat wachtwoord toestaan. Dit zorgt ervoor dat het beleid van uw on-premises wordt afgedwongen in de cloud, ongeacht of u Wachtwoordsynchronisatie of Federatie gebruiken voor eenmalige aanmelding.

10. Als het wachtwoord ingesteld mislukt, wordt geretourneerd met de fout aan de gebruiker en laat ze probeer het opnieuw.
    * De bewerking kan mislukken vanwege de volgende
        * De service is niet actief
        * Het wachtwoord dat ze geselecteerd voldeed niet aan beleid van organisatie
        * Er kan de gebruiker niet vinden in de lokale AD

    We hebben een specifieke bericht voor veel van deze gevallen en de gebruiker vertellen wat ze kunnen doen om het probleem te verhelpen.

## <a name="configuring-password-writeback"></a>Wachtwoord terugschrijven configureren

Het is raadzaam dat u de functie voor automatisch bijwerken van [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) als u wilt gebruiken terugschrijven van wachtwoorden.

DirSync en Azure AD Sync zijn niet langer ondersteund middel aan voor het inschakelen van wachtwoord terugschrijven het artikel [upgraden van DirSync en Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) bevat meer informatie om te helpen bij de overgang.

De volgende stappen wordt ervan uitgegaan dat u Azure AD Connect al hebt geconfigureerd in uw omgeving met de [Express](./connect/active-directory-aadconnect-get-started-express.md) of [aangepaste](./connect/active-directory-aadconnect-get-started-custom.md) instellingen.

1. Om te configureren en inschakelen van wachtwoord terugschrijven melden bij uw Azure AD Connect-server en start de **Azure AD Connect** configuratiewizard.
2. Klik op het welkomstscherm op **configureren**.
3. Op de aanvullende taken Klik scherm **aanpassen Synchronisatieopties** en kies vervolgens **volgende**.
4. Voer de referenties van een globale beheerder op het scherm verbinding maken met Azure AD en kies **volgende**.
5. Op de verbinding maken met uw directory's en het domein en OE filteren schermen kunt u **volgende**.
6. Op het scherm optionele functies Schakel het selectievakje in naast **wachtwoord terugschrijven** en klik op **volgende**.
   ![Wachtwoord terugschrijven in Azure AD Connect inschakelen][Writeback]
7. Klik op de gereed voor configuratie scherm **configureren** en wacht totdat dit proces te voltooien.
8. Wanneer er configuratie voltooien klikt u op **afsluiten**

## <a name="licensing-requirements-for-password-writeback"></a>Licentievereisten voor write-back van wachtwoord

Voor informatie over licentieverlening, Zie het onderwerp [licenties nodig zijn voor write-back van wachtwoord](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) of de volgende sites

* [Azure Active Directory-prijzen site](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Beveiligde productief Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Lokale verificatiemodi ondersteund voor write-back van wachtwoord

Wachtwoord terugschrijven werkt voor de volgende typen van de gebruiker-wachtwoord:

* **Alleen in de cloud gebruikers**: wachtwoord terugschrijven is niet van toepassing in dit geval, omdat er geen on-premises-wachtwoord
* **Het wachtwoord is gesynchroniseerd gebruikers**: wachtwoord terugschrijven ondersteund
* **Federatieve gebruikers**: wachtwoord terugschrijven ondersteund
* **Pass through-verificatie gebruikers**: wachtwoord terugschrijven ondersteund

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Gebruikers- en Admin bewerkingen die worden ondersteund voor write-back van wachtwoord

Wachtwoorden worden teruggeschreven in de volgende situaties:

* **Ondersteunde bewerkingen van eindgebruikers**
  * Alle eindgebruikers selfservice vrijwillige bewerking wachtwoord wijzigen
  * Eindgebruikers selfservice force wijzigen wachtwoord bewerkingen (bijvoorbeeld verlopen van wachtwoorden)
  * Alle eindgebruikers selfservice voor wachtwoordherstel die afkomstig zijn van de [Portal voor wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com)
* **Ondersteunde bewerkingen van de beheerder**
  * Een beheerder selfservice vrijwillige bewerking wachtwoord wijzigen
  * Een beheerder selfservice force wijzigen wachtwoord bewerking (bijvoorbeeld verlopen van wachtwoorden)
  * Een beheerder selfservice voor wachtwoordherstel die afkomstig zijn van de [Portal voor wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com)
  * Een beheerder worden geïnitieerd door eindgebruikers wachtwoord opnieuw instellen van de [klassieke Azure-portal](https://manage.windowsazure.com)
  * Een beheerder worden geïnitieerd door eindgebruikers wachtwoord opnieuw instellen van de [Azure-portal](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Gebruikers- en Admin bewerkingen worden niet ondersteund voor write-back van wachtwoord

De wachtwoorden **niet** teruggeschreven in een van de volgende situaties:

* **Niet-ondersteunde bewerkingen van eindgebruikers**
  * Iedere gebruiker opnieuw instellen van hun eigen wachtwoord met behulp van PowerShell v1, v2, of de Azure AD Graph API
* **Niet-ondersteunde bewerkingen van de beheerder**
  * Een beheerder worden geïnitieerd door eindgebruikers wachtwoord opnieuw instellen van de [Office-beheerportal](https://portal.office.com)
  * Een beheerder worden geïnitieerd door eindgebruikers voor wachtwoordherstel van PowerShell v1, v2 of de Azure AD Graph API

Terwijl we proberen te verwijderen van deze beperkingen, hoeft u niet een specifieke tijdlijn die we nog kunt delen.

## <a name="password-writeback-security-model"></a>Wachtwoord terugschrijven beveiligingsmodel

Wachtwoord terugschrijven is een maximaal beveiligde service.  Uw gegevens worden beschermd, zodat inschakelen we een beveiligingsmodel 4 lagen die wordt hieronder beschreven.

* **Tenant-specifieke service bus relay**
  * Bij het instellen van de service, u stelt een tenantspecifieke service bus relay die wordt beveiligd door een willekeurig gegenereerd sterk wachtwoord dat Microsoft nooit toegang tot heeft.
* **De versleutelingssleutel vergrendelde, cryptografisch sterk wachtwoord**
  * Nadat de service bus relay is gemaakt, maken we een sterke symmetrische sleutel die we gebruiken voor het versleutelen van het wachtwoord als ze afkomstig zijn via de kabel. Deze sleutel woont alleen in geheime store in de cloud, die sterk is vergrendeld en gecontroleerd, net als elk wachtwoord in de map van uw bedrijf.
* **De standaard TLS bedrijfstak**
  1. Wanneer u een wachtwoord opnieuw instellen of wijzigen bewerking doet zich voor in de cloud, we nemen het leesbare wachtwoord coderen met uw openbare sleutel.
  2. We vervolgens plaatsen die in een HTTPS-mailbericht wordt verzonden via een versleuteld kanaal met behulp van Microsoft SSL-certificaten voor uw service bus relay.
  3. Nadat het bericht naar Service Bus binnenkomt, uw lokale ontwaakt en de agent zich verifieert bij Service Bus het sterk wachtwoord dat eerder is gegenereerd.
  4. Lokale agent het gecodeerde bericht opneemt, ontsleutelt met behulp van de persoonlijke sleutel die wordt gegenereerd.
  5. Lokale agent probeert vervolgens via de API van AD DS SetPassword-wachtwoord instellen.
     * Deze stap is wat kunnen worden uitgevoerd op het afdwingen van uw beleid AD on-premises wachtwoord (complexiteit, leeftijd, geschiedenis, filters, enzovoort) in de cloud.
* **Het verloopbeleid bericht** 
  * Als het bericht bevindt zich in de Service Bus omdat uw on-premises service niet actief is, wordt beëindigd en worden verwijderd na enkele minuten beveiliging nog verder verbeteren.

### <a name="password-writeback-encryption-details"></a>Wachtwoord terugschrijven versleuteling details

De stappen voor het versleutelen een aanvraag voor wachtwoordherstel doorloopt nadat een gebruiker verzendt, voordat het wordt geleverd in uw on-premises-omgeving, om ervoor te zorgen maximale service betrouwbaarheid en beveiliging worden hieronder beschreven.

* **Stap 1 - wachtwoordversleuteling met 2048-bits RSA-sleutel** - zodra een gebruiker een wachtwoord worden teruggeschreven naar verzendt on-premises, eerst het opgegeven wachtwoord zelf is versleuteld met een 2048-bits RSA-sleutel.
* **Stap 2: versleuteling van het pakket op met AES-GCM** -en vervolgens het volledige pakket (wachtwoord + vereiste metagegevens) is versleuteld met AES-GCM. Dit voorkomt dat iedereen met directe toegang naar de onderliggende service bus-kanaal weergeven/knoeien met de inhoud.
* **Stap 3: alle communicatie vindt plaats via TLS / SSL** -alle communicatie met Service Bus gebeurt in een SSL/TLS-kanaal. Dit wordt de inhoud beveiligd van niet-geautoriseerde 3e partijen.
* **Automatische sleutelrollover om de zes maanden** : automatisch elke 6 maanden of elke keer dat wachtwoord terugschrijven is uitgeschakeld of opnieuw worden ingeschakeld op Azure AD Connect we rollover deze sleutels om ervoor te zorgen maximale service en veiligheid.

### <a name="password-writeback-bandwidth-usage"></a>Wachtwoord terugschrijven bandbreedtegebruik

Wachtwoord terugschrijven is een lage bandbreedte-service die aanvragen teruggestuurd naar de lokale agent alleen in de volgende omstandigheden wordt:

1. Twee berichten worden verzonden wanneer het in- of uitschakelen van de functie met Azure AD Connect.
2. Een bericht wordt elke vijf minuten als een heartbeat-service voor verzonden als de service wordt uitgevoerd.
3. Twee berichten worden verzonden op elk moment een nieuw wachtwoord wordt ingediend
    * Eerste bericht, als een aanvraag voor de bewerking uit te voeren
    * Tweede bericht die het resultaat van de bewerking bevat en worden verzonden in de volgende omstandigheden:
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een gebruiker zelf uw wachtwoord opnieuw instellen.
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een wachtwoordwijziging van gebruiker.
        * Telkens wanneer een nieuw wachtwoord wordt ingediend tijdens een beheerder geïnitieerde gebruikerswachtwoord opnieuw instellen (van de Azure-beheerder portals alleen).

#### <a name="message-size-and-bandwidth-considerations"></a>Overwegingen voor het grootte en bandbreedte van het bericht

De grootte van elk van de hierboven beschreven bericht is doorgaans onder 1 kb, zelfs onder extreme laadt, de service voor het terugschrijven van wachtwoord zelf verbruikt enkele kilobits per seconde van de bandbreedte. Omdat elk bericht wordt verzonden in realtime, is alleen indien vereist door een updatebewerking wachtwoord, en de berichtgrootte zo klein is het bandbreedtegebruik van de mogelijkheid Write-back effectief te klein voor een echte merkbare impact hebben.

## <a name="next-steps"></a>Volgende stappen

De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens**](active-directory-passwords-data.md): informatie over de gegevens die nodig zijn en hoe deze worden gebruikt voor wachtwoordbeheer
* [**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie
* [**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? - Antwoorden op vragen die u altijd wilde stellen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Wachtwoord terugschrijven in Azure AD Connect inschakelen"
