---
title: 'Dieper: Azure AD SSPR | Microsoft Docs'
description: Azure AD selfservice voor wachtwoordherstel diepgaand
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0fa05ee6a2df13845024e770a82f50ab7f75bafd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Selfservice voor wachtwoordherstel in Azure AD-diepgaand

Hoe werkt SSPR? Wat betekent dat optie in de interface? Blijven lezen voor meer informatie over Azure AD zelf uw wachtwoord opnieuw instellen.

## <a name="how-does-the-password-reset-portal-work"></a>Hoe het wachtwoord opnieuw ingesteld portal werk

Wanneer een gebruiker navigeert naar de portal voor wachtwoordherstel, een werkstroom wordt gestart om te bepalen:

   * Hoe moet u de pagina gelokaliseerd?
   * Is het gebruikersaccount geldig?
   * Welke organisatie behoort de gebruiker tot?
   * Waar het wachtwoord van gebruikers wordt beheerd?
   * Is de gebruiker een licentie voor het gebruik van de functie?


Lees de onderstaande stappen voor meer informatie over de logica achter de wachtwoordpagina opnieuw instellen.

1. Gebruiker klikt op de geen toegang tot uw accountkoppeling of gaan rechtstreeks naar [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Op basis van de landinstellingen van de browser die de ervaring wordt weergegeven in de juiste taal. De ervaring van wachtwoord opnieuw instellen is vertaald in dezelfde talen, zoals Office 365 ondersteunt.
3. Gebruiker voert een gebruikers-id en een captcha wordt doorgegeven.
4. Azure AD verifieert of de gebruiker deze functie gebruiken is als volgt:
   * Controleert of de gebruiker deze functie is ingeschakeld en een Azure AD-licentie toegewezen.
     * Als de gebruiker beschikt niet over deze functie is ingeschakeld of een licentie is toegewezen, wordt de gebruiker gevraagd contact op met de beheerder om hun wachtwoord opnieuw instellen.
   * Controleert of de gebruiker het recht heeft uitdaging gegevens op hun account in overeenstemming met de beheerdersbeleid gedefinieerd.
     * Als het beleid vereist dat slechts één uitdaging, wordt vervolgens gewaarborgd dat de gebruiker de juiste gegevens die zijn gedefinieerd voor ten minste één van de uitdagingen ingeschakeld door het beheerdersbeleid heeft.
       * Als de gebruiker niet is geconfigureerd, wordt de gebruiker aanbevolen contact opnemen met de beheerder om hun wachtwoord opnieuw instellen.
     * Als het beleid twee uitdagingen vereist, wordt vervolgens gewaarborgd dat de gebruiker de juiste gegevens die zijn gedefinieerd voor ten minste twee van de uitdagingen ingeschakeld door het beheerdersbeleid heeft.
       * Als de gebruiker niet is geconfigureerd, is er de gebruiker contact op met de beheerder om hun wachtwoord opnieuw instellen.
   * Controleert als het wachtwoord van de gebruiker on-premises (federatieve of wachtwoord-hash gesynchroniseerd) wordt beheerd.
     * Als u Write-back is geïmplementeerd en het wachtwoord van de gebruiker on-premises wordt beheerd, is de gebruiker toegestaan om door te gaan om te verifiëren en hun wachtwoord opnieuw instellen.
     * Als Write-back is niet geïmplementeerd en het wachtwoord van gebruikers wordt beheerd op on-premises, wordt de gebruiker gevraagd contact op met de beheerder om hun wachtwoord opnieuw instellen.
5. Als wordt vastgesteld dat de gebruiker kan opnieuw instellen van hun wachtwoord, wordt de gebruiker geleid door het proces opnieuw instellen.

## <a name="authentication-methods"></a>Verificatiemethoden

Als Self-Service wachtwoord opnieuw instellen (SSPR) is ingeschakeld, moet u ten minste één van de volgende opties voor verificatiemethoden. We raden u ten minste twee verificatiemethoden kiest, zodat uw gebruikers meer flexibiliteit hebben.

* E-mail
* Mobiele telefoon
* Telefoon (werk)
* Beveiligingsvragen

### <a name="what-fields-are-used-in-the-directory-for-authentication-data"></a>Welke velden worden gebruikt in de map voor verificatiegegevens

* Telefoon (werk) komt overeen met de telefoon (werk)
    * Gebruikers hebben geen Stel dit veld zelf moet deze worden gedefinieerd door een beheerder
* Mobiele telefoon komt overeen met de telefoon voor authenticatie (niet openbaar zichtbaar) of mobiele telefoon (openbaar zichtbaar)
    * De service eerst naar de telefoon voor authenticatie gezocht, vervolgens schakelt terug naar mobiele telefoon als niet geïnstalleerd
* Alternatief e-mailadres komt overeen met de verificatie-e (niet openbaar zichtbaar) of alternatieve e-mailadres
    * De service eerst voor verificatie E-mail gezocht en vervolgens terug naar het alternatieve e-mailadres is mislukt

Standaard worden alleen de cloud kenmerken telefoon (werk) en mobiele telefoonnummers voor uw clouddirectory gesynchroniseerd vanuit uw on-premises directory voor verificatiegegevens.

Gebruikers kunnen hun wachtwoord alleen opnieuw instellen als ze gegevens zijn aanwezig in de verificatiemethoden die de beheerder is ingeschakeld en is vereist.

Als gebruikers hun mobiele telefoonnummer zichtbaar in de map niet wilt, maar toch wilt gebruiken voor wachtwoord opnieuw instellen, beheerders moeten het niet vullen in de map en de gebruiker moet vervolgens vullen hun **telefoon voor authenticatie** kenmerk de [registratieportal voor wachtwoordherstel](http://aka.ms/ssprsetup). Beheerders kunnen deze informatie in het profiel van de gebruiker zien, maar het niet ergens anders is gepubliceerd. Als een Azure-beheerdersaccount hun telefoonnummer voor verificatie registreert, worden ingevuld in het veld mobiele telefoon en zichtbaar is.

### <a name="number-of-authentication-methods-required"></a>Aantal verificatiemethoden vereist

Deze optie bepaalt het minimumaantal de beschikbare verificatiemethoden een gebruiker opnieuw instellen of hun wachtwoord ontgrendelen moet doorlopen en kan worden ingesteld op 1 of 2 zijn.

Gebruikers kunnen kiezen om op te geven meer verificatiemethoden als ze zijn ingeschakeld door de beheerder.

Als een gebruiker niet de minimale vereiste methoden die zijn geregistreerd heeft, zien ze een foutpagina die ze hun wachtwoord opnieuw instellen van een beheerder vragen worden omgeleid.

### <a name="how-secure-are-my-security-questions"></a>Hoe veilig weet mijn beveiligingsvragen

Als u beveiligingsvragen gebruiken, raden wij deze gebruikt met een andere methode als ze minder veilig dan andere methoden worden kunnen omdat sommige mensen een andere gebruikers vragen worden beantwoord weet mogelijk.

> [!NOTE] 
> Beveiligingsvragen zijn privé en veilig opgeslagen op een gebruikersobject in Active directory en kunnen alleen worden beantwoord door gebruikers tijdens de registratie. Er is geen manier voor een beheerder om te lezen of wijzigen van een gebruiker vragen of antwoorden.
>

### <a name="security-question-localization"></a>Beveiliging vraag lokalisatie

Alle vooraf gedefinieerde vragen als u worden in de volledige set van Office 365-talen op basis van de browser van de gebruiker gelokaliseerd.

* In welke stad hebt u uw eerste partner ontmoet?
* In welke stad hebben uw ouders elkaar leren kennen?
* In welke stad woont uw jongste of oudste broer of zus?
* In welke stad is uw vader geboren?
* In welke plaats hebt u uw eerste baan gehad?
* In welke stad is uw moeder geboren?
* In welke plaats was u op oudejaarsavond in 2000?
* Wat is de achternaam van uw favoriete leraar op hoog * school?
* Voor welke universiteit bent u uitgeloot?
* Waar hebt u uw trouwreceptie gehouden?
* Wat is de tweede naam van uw vader?
* Wat is uw lievelingseten?
* Wat zijn de voor- en achternaam van uw oma van moederskant?
* Wat is de tweede naam van uw moeder?
* Wat is uw oudste Broer of zus geboren maand en jaar? (bijvoorbeeld November 1985)
* Wat is de tweede naam van uw oudste broer of zus?
* Wat zijn de voor- en achternaam van uw opa van vaderskant?
* Wat is de tweede naam van uw jongste broer of zus?
* Op welke school zat u in de brugklas?
* Wat zijn de voor- en achternaam van uw beste jeugdvriend?
* Wat zijn de voor- en achternaam van uw eerste partner?
* Wat is de achternaam van uw favoriete leraar op de lagere school?
* Wat zijn het merk en model van uw eerste auto of motor?
* Wat is de naam van uw eerste school?
* In welk ziekenhuis bent u geboren?
* In welke straat staat of stond het huis waar u bent opgegroeid?
* Wat is de naam van uw jeugdidool?
* Wat is de naam van uw favoriete knuffeldier?
* Wat is de naam van uw eerste huisdier?
* Wat was uw bijnaam als kind?
* Wat was uw favoriete sport op de middelbare school?
* Wat was uw eerste baan?
* Wat zijn of waren de laatste vier cijfers van het telefoonnummer van uw ouderlijk huis?
* Wat wilde u worden toen u klein was?
* Wie is de grootste beroemdheid die u ooit hebt ontmoet?

### <a name="custom-security-questions"></a>Aangepaste beveiligingsvragen

Aangepaste beveiligingsvragen zijn niet gelokaliseerd voor verschillende talen. Alle aangepaste vragen worden weergegeven in dezelfde taal als die ze worden ingevoerd in de interface van de gebruiker met beheerdersrechten, zelfs als de browser van de gebruiker verschilt. Als u gelokaliseerde vragen nodig hebt, gebruikt u de vooraf gedefinieerde vragen.

De maximale lengte van een aangepaste beveiligingsvraag is 200 tekens.

### <a name="security-question-requirements"></a>Vraag de beveiligingsvereisten

* Minimale antwoord maximum aantal tekens is 3 tekens
* Maximale antwoord maximum aantal tekens is 40 tekens
* Gebruikers kunnen niet dezelfde vraag meer dan één keer worden beantwoord
* Gebruikers kunnen niet dezelfde meer dan één vraag te beantwoorden bepalen
* Een tekenset kan worden gebruikt voor het definiëren van vragen en antwoorden, met inbegrip van Unicode-tekens
* Het aantal vragen gedefinieerd moet groter zijn dan of gelijk zijn aan het aantal vragen dat vereist is om te registreren

## <a name="registration"></a>Registratie

### <a name="require-users-to-register-when-signing-in"></a>Vereisen dat gebruiker zich bij aanmelding registreren

Deze optie inschakelt, moet registratie van een gebruiker die is ingeschakeld voor wachtwoord opnieuw instellen voor het voltooien van het wachtwoord opnieuw instellen als ze zich aanmelden voor toepassingen die gebruikmaken van Azure AD aan te melden zoals die volgen:

* Office 365
* Azure Portal
* Toegangsvenster
* Federatieve toepassingen
* Aangepaste toepassingen die gebruikmaken van Azure AD

Uitschakelen van deze functie nog steeds kunnen gebruikers hun contactgegevens handmatig registreren in via [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) of door te klikken op de **registreren voor wachtwoordherstel** koppeling onder de profieltabblad in het deelvenster toegang.

> [!NOTE]
> Gebruikers de registratieportal voor wachtwoordherstel kunnen negeren door op Annuleren te klikken of u het venster sluit, maar telkens wanneer die ze zich aanmelden totdat ze registratie hebt voltooid, wordt gevraagd.
>

### <a name="number-of-days-before-users-are-asked-to-reconfirm-their-authentication-information"></a>Het aantal dagen waarna gebruikers wordt gevraagd om de verificatiegegevens opnieuw te bevestigen

Deze optie bepaalt u de periode tussen instellen en verificatiegegevens reconfirming en is alleen beschikbaar als u inschakelt de **vereisen dat gebruikers zich registreren wanneer** optie.

Geldige waarden zijn 0 730 dagen met 0, wat betekent dat nooit gebruikers vragen om hun verificatie-informatie hebt bevestigd

## <a name="notifications"></a>Meldingen

### <a name="notify-users-on-password-resets"></a>Gebruikers een melding tonen over het opnieuw instellen van hun wachtwoord

Als deze optie is ingesteld op Ja, ontvangt een melding dat hun wachtwoord is gewijzigd via de SSPR-portal naar de primaire en alternatieve e-mailadressen in het bestand in Azure AD e-mailbericht met de gebruiker die hun wachtwoord opnieuw instelt. Niemand anders wordt de hoogte gesteld van deze opnieuw instellen van gebeurtenis.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Alle beheerders waarschuwen wanneer andere beheerders hun wachtwoord opnieuw instellen

Als deze optie is ingesteld op Ja, klikt u vervolgens **alle beheerders** ontvangt een e-mail naar het primaire e-mailadres in het bestand in Azure AD melding dat hun wachtwoord met behulp van SSPR is gewijzigd door een andere beheerder.

Voorbeeld: Zijn er vier beheerders in een omgeving. Beheerder "A" instelt hun wachtwoord met behulp van SSPR. Beheerders B en C D ontvangen een e-mailbericht waarschuwen dat ze dit gebeurt.

## <a name="on-premises-integration"></a>On-premises integratie

Als u hebt geïnstalleerd, geconfigureerd en ingeschakeld Azure AD Connect hebt u aanvullende opties voor lokale integraties.

### <a name="write-back-passwords-to-your-on-premises-directory"></a>Wachtwoorden terugschrijven naar uw on-premises directory

Hiermee bepaalt u of wachtwoord terugschrijven is ingeschakeld voor deze map en als write-back ingeschakeld is, geeft de status van de on-premises Write-back-service. Dit is handig als u het terugschrijven van wachtwoorden tijdelijk uitschakelen wilt zonder de Azure AD Connect opnieuw te configureren.

* Als de switch is ingesteld op Ja, vervolgens Write-back wordt ingeschakeld, en federatieve en wachtwoord-hash gesynchroniseerd gebruikers kunnen hun wachtwoorden opnieuw kunnen instellen.
* Als de switch is ingesteld op Nee, vervolgens Write-back wordt uitgeschakeld, en federatieve en wachtwoord-hash gesynchroniseerd gebruikers zich niet hun wachtwoord opnieuw instellen.

### <a name="allow-users-to-unlock-accounts-without-resetting-their-password"></a>Toestaan dat gebruikers voor het ontgrendelen van accounts zonder hun wachtwoord opnieuw instellen

Geeft aan of gebruikers die de portal voor wachtwoord opnieuw instellen van bezoeken moeten krijgt de mogelijkheid voor het ontgrendelen van de lokale Active Directory-accounts zonder hun wachtwoord opnieuw instellen of niet. Standaard Azure AD wordt altijd ontgrendelen van accounts bij het uitvoeren van een wachtwoord opnieuw instellen, deze instelling kunt u voor het scheiden van deze twee bewerkingen. 

* Indien ingesteld op 'Ja', vervolgens gebruikers de mogelijkheid hun wachtwoord opnieuw instellen en het account ontgrendelen of krijgt voor het ontgrendelen zonder het wachtwoord opnieuw instellen.
* Als ingesteld op "Nee" en vervolgens gebruikers is alleen mogelijk om uit te voeren van een gecombineerde wachtwoord opnieuw instellen en ontgrendelen van het account opnieuw.

## <a name="network-requirements"></a>Netwerkvereisten

### <a name="firewall-rules"></a>Firewall-regels

[Lijst met Microsoft Office-URL's en IP-adressen](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Voor Azure AD Connect versie 1.1.443.0 en hoger, u moet uitgaande HTTPS toegang tot de volgende
* passwordreset.microsoftonline.com
* servicebus.Windows.NET

Voor meer gedetailleerd toegang vindt u de bijgewerkte lijst met Microsoft Azure Datacenter IP-bereiken die elke woensdag wordt bijgewerkt en de volgende tot stand is gebracht maandag [hier](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Time-outs voor niet-actieve verbindingen

Het hulpprogramma Azure AD Connect verzendt periodieke pings/keepalives naar Service Bus-eindpunten om ervoor te zorgen dat de verbindingen actief blijven. Als het hulpprogramma detecteert dat er te veel verbindingen worden afgesloten, wordt de frequentie van pings naar het eindpunt automatisch verhoogd. De laagste 'pingen intervallen' vallen, is 1 ping elke 60 seconden, maar we raden dat proxy's / firewalls niet-actieve verbindingen om vast te leggen voor ten minste 2-3 minuten zijn toegestaan. * We raden vier minuten of langer voor oudere versies.

## <a name="active-directory-permissions"></a>Machtigingen voor Active Directory

Het account opgegeven in het Azure AD Connect-hulpprogramma moet wachtwoord opnieuw instellen, wachtwoord wijzigen, schrijfmachtigingen hebben op lockoutTime en schrijfmachtigingen op pwdLastSet, uitgebreide rechten van een object in de root van **elk domein** in dat forest **of** op de organisatie-eenheden u wilt gebruiken als binnen het bereik van de SSPR-gebruiker.

Als u niet zeker weet welk account de bovenstaande naar verwijst de Azure Active Directory Connect configuratiegebruikersinterface openen en klik op de huidige configuratie-optie voor weergave. Het account dat u wilt toevoegen, mag wordt vermeld onder 'Mappen gesynchroniseerd'

Deze machtigingen kan het MA-serviceaccount voor elk forest de wachtwoorden beheren namens de gebruikersaccounts in dat forest. **Als u niet de volgende machtigingen toe te wijzen, klikt u vervolgens terugschrijven weergegeven correct worden geconfigureerd, maar gebruikers er fouten optreden bij een poging tot het beheren van hun on-premises wachtwoorden vanuit de cloud.**

> [!NOTE]
> Het kan duren tot een uur of meer voor de machtigingen zijn gerepliceerd naar alle objecten in uw directory.
>

Voor het instellen van de juiste machtigingen voor write-back van wachtwoord om te worden uitgevoerd

1. Open Active Directory: gebruikers en Computers met een account met de juiste machtigingen voor domeinbeheer
2. Controleer of dat geavanceerde functies is ingeschakeld op in het menu Beeld
3. In het linkerdeelvenster met de rechtermuisknop op het object waarmee de hoofdmap van het domein en kies Eigenschappen
    * Klik op het tabblad Beveiliging
    * Klik vervolgens op Geavanceerd.
4. Klik op toevoegen op het tabblad machtigingen
5. Het account kiezen dat machtigingen worden toegepast op (van Azure AD Connect-installatie)
6. Selecteer in de van toepassing op de vervolgkeuzelijst onderliggende gebruikersobjecten
7. Schakel de selectievakjes voor de volgende onder machtigingen
    * Unexpire wachtwoord
    * Wachtwoord opnieuw instellen
    * Wachtwoord wijzigen
    * LockoutTime schrijven
    * PwdLastSet schrijven
8. Klik op toepassen/OK via wilt toepassen en sluit alle geopende dialoogvensters.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Hoe wachtwoord opnieuw instellen voor B2B-gebruikers?
Wachtwoord opnieuw instellen en wijzigen worden volledig ondersteund in alle B2B-configuraties.  Lees hieronder voor de drie expliciete B2B gevallen wordt ondersteund door het wachtwoord opnieuw instellen.

1. **Gebruikers van een partner org met een bestaande Azure AD-tenant** - als de organisatie die u samenwerking met een bestaande Azure AD-tenant we **respecteren ongeacht wachtwoord opnieuw instellen van beleidsregels zijn ingeschakeld in deze tenant**. Voor wachtwoord opnieuw instellen om te werken, de partner organisatie alleen behoeften om te controleren of Azure AD SSPR is ingeschakeld, die zonder extra kosten voor O365-klanten, en kan worden ingeschakeld door de stappen in onze [aan de slag met wachtwoordbeheer](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords)handleiding.
2. **Gebruikers die zich heeft aangemeld met behulp van [self-service aanmelding](active-directory-self-service-signup.md)**  - als de organisatie die u zijn samenwerking met gebruikte de [self-service aanmelding](active-directory-self-service-signup.md) om toegang te krijgen tot een tenant, laten we opnieuw instellen met de e-mailbericht die ze geregistreerd.
3. **B2B-gebruikers** -nieuwe B2B gebruikers gemaakt met behulp van de nieuwe [Azure AD B2B-mogelijkheden](active-directory-b2b-what-is-azure-ad-b2b.md) is ook mogelijk om in te stellen hun wachtwoorden met het e-mailbericht ze tijdens de uitnodiging hebt geregistreerd.

U kunt dit testen, gaat u naar http://passwordreset.microsoftonline.com met een van deze partner-gebruikers. Zolang ze beschikken over een alternatieve e-mailadres of verificatie e-mailadres is gedefinieerd, heeft wachtwoord opnieuw instellen werkt zoals verwacht.

## <a name="next-steps"></a>Volgende stappen

De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens**](active-directory-passwords-data.md): informatie over de gegevens die nodig zijn en hoe deze worden gebruikt voor wachtwoordbeheer
* [**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory
* [**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? - Antwoorden op vragen die u altijd wilde stellen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel

