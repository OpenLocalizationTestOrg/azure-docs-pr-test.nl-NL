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
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Selfservice voor wachtwoordherstel in Azure AD-diepgaand

Hoe werkt SSPR? Wat betekent dat optie Hallo interface? Blijven lezen toofind voor meer informatie over Azure AD zelf uw wachtwoord opnieuw instellen.

## <a name="how-does-hello-password-reset-portal-work"></a>Hoe Hallo wachtwoordherstel portal werk

Wanneer een gebruiker toohello-portal voor wachtwoord opnieuw instellen navigeert, wordt een werkstroom gestarte toodetermine:

   * Hoe moet Hallo pagina gelokaliseerd?
   * Hallo-gebruikersaccount geldig is?
   * Welke organisatie behoort Hallo gebruiker tot?
   * Waar Hallo gebruikerswachtwoord wordt beheerd?
   * Hallo gelicentieerde toouse Hallo functie is?


Lees Hallo stappen hieronder toolearn over Hallo logica achter het Hallo-pagina voor het opnieuw instellen van wachtwoorden.

1. Gebruiker klikt op Hallo heeft geen toegang tot uw accountkoppeling of gaat rechtstreeks te[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Gebaseerd op Hallo browser landinstelling Hallo ervaring wordt weergegeven in de juiste taal Hallo. Hallo is wachtwoord opnieuw instellen van ervaring vertaald in dezelfde talen Hallo zoals Office 365 ondersteunt.
3. Gebruiker voert een gebruikers-id en een captcha wordt doorgegeven.
4. Azure AD verifieert of Hallo gebruiker kunnen toouse is deze functie door Hallo volgende te doen:
   * Controleert dat die Hallo de gebruiker heeft deze functie is ingeschakeld en een Azure AD-licentie toegewezen.
     * Als Hallo gebruiker beschikt niet over deze functie is ingeschakeld of een licentie is toegewezen, is het Hallo-gebruiker toocontact gevraagd hun tooreset beheerder hun wachtwoord.
   * Controleert die gebruiker Hallo Hallo rechts uitdaging gegevens op hun account in overeenstemming met de beheerdersbeleid gedefinieerd.
     * Als het beleid vereist dat slechts één uitdaging en vervolgens die Hallo de gebruiker heeft de juiste gegevens Hallo gedefinieerd voor ten minste één van de uitdagingen van Hallo ingeschakeld door het beleid voor Hallo beheerder wordt gewaarborgd.
       * Als Hallo gebruiker niet is geconfigureerd en vervolgens Hallo gebruiker wordt aangeraden toocontact hun tooreset beheerder hun wachtwoord.
     * Als Hallo beleid twee uitdagingen vereist, wordt vervolgens gewaarborgd dat die Hallo de gebruiker heeft de juiste Hallo-gegevens voor ten minste twee Hallo uitdagingen ingeschakeld door Hallo beheerdersbeleid gedefinieerd.
       * Als Hallo gebruiker is niet geconfigureerd, wordt er gebruiker Hallo wordt aangeraden toocontact hun tooreset beheerder hun wachtwoord.
   * Controleert als Hallo gebruikerswachtwoord on-premises (federatieve of wachtwoord-hash gesynchroniseerd) wordt beheerd.
     * Als u Write-back is geïmplementeerd en het wachtwoord van gebruiker Hallo on-premises wordt beheerd, Hallo gebruiker tooproceed tooauthenticate is toegestaan en hun wachtwoord opnieuw instellen.
     * Als Write-back is niet geïmplementeerd en het wachtwoord van gebruiker Hallo on-premises wordt beheerd, is Hallo gebruiker toocontact gevraagd hun tooreset beheerder hun wachtwoord.
5. Als wordt vastgesteld, kan die gebruiker Hallo toosuccessfully hun wachtwoord opnieuw instellen en Hallo gebruiker geleid door Hallo opnieuw instellen.

## <a name="authentication-methods"></a>Verificatiemethoden

Als Self-Service wachtwoord opnieuw instellen (SSPR) is ingeschakeld, moet u ten minste één van de volgende opties voor verificatiemethoden Hallo. We raden u ten minste twee verificatiemethoden kiest, zodat uw gebruikers meer flexibiliteit hebben.

* E-mail
* Mobiele telefoon
* Telefoon (werk)
* Beveiligingsvragen

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Welke velden worden gebruikt in de directory Hallo voor verificatiegegevens

* Telefoon (werk) overeenkomt met tooOffice telefoon
    * Gebruikers zijn niet kan tooset dit veld zelf moet deze worden gedefinieerd door een beheerder
* Mobiele telefoon komt overeen tooeither telefoon voor authenticatie (niet openbaar zichtbaar) of een mobiele telefoon (openbaar zichtbaar)
    * Hallo-service zoekt eerst naar telefoon voor authenticatie, vervolgens terugvalt tooMobile telefoon als niet geïnstalleerd
* Alternatief e-mailadres komt overeen tooeither verificatie-e (niet openbaar zichtbaar) of het alternatieve e-mailadres
    * Hallo service eerst voor verificatie E-mail gezocht en vervolgens back tooAlternate E-mail is mislukt

Alleen Hallo cloud-kenmerken telefoon (werk) en mobiele telefoonnummers worden standaard gesynchroniseerd tooyour clouddirectory van uw on-premises directory voor verificatiegegevens.

Gebruikers kunnen alleen opnieuw instellen van hun wachtwoord als ze gegevens aanwezig is in het Hallo-verificatiemethoden of Hallo beheerder is ingeschakeld en is vereist.

Als gebruikers niet dat hun mobiele telefoon nummer toobe zichtbaar in de directory Hallo wilt maar zou nog zoals toouse deze voor het wachtwoord opnieuw instellen, beheerders moeten het niet vullen in Hallo directory en Hallo gebruiker moet vervolgens vullen hun **telefoon voor authenticatie**  kenmerk via Hallo [registratieportal voor wachtwoordherstel](http://aka.ms/ssprsetup). Beheerders kunnen deze informatie in Hallo gebruikersprofiel zien, maar het niet ergens anders is gepubliceerd. Als een Azure-beheerdersaccount hun telefoonnummer voor verificatie registreert, worden ingevuld in het veld van de mobiele telefoon Hallo en zichtbaar is.

### <a name="number-of-authentication-methods-required"></a>Aantal verificatiemethoden vereist

Deze optie wordt bepaald Hallo minimum aantal beschikbare verificatiemethoden Hallo een gebruiker moet gaan via tooreset of hun wachtwoord ontgrendelen en tooeither 1 of 2 kan worden ingesteld.

Gebruikers kunnen kiezen toosupply meer verificatiemethoden als ze zijn ingeschakeld door Hallo beheerder.

Als een gebruiker heeft geen vereist minimaal Hallo methoden die zijn geregistreerd, zien ze een foutpagina dat ze een beheerder tooreset toorequest omgeleid hun wachtwoord.

### <a name="how-secure-are-my-security-questions"></a>Hoe veilig weet mijn beveiligingsvragen

Als u beveiligingsvragen gebruiken, raden wij deze gebruikt met een andere methode als u ze kunnen minder veilig dan andere methoden omdat sommige mensen Hallo-antwoorden tooanother gebruikers vragen weten mogelijk.

> [!NOTE] 
> Beveiligingsvragen zijn privé en veilig opgeslagen op een gebruikersobject in Hallo directory en kunnen alleen worden beantwoord door gebruikers tijdens de registratie. Er is geen manier voor een beheerder tooread of wijzigen van een gebruiker vragen of antwoorden.
>

### <a name="security-question-localization"></a>Beveiliging vraag lokalisatie

Alle vooraf gedefinieerde vragen als u worden in de volledige set van Office 365-talen op basis van de landinstellingen van de browser van de gebruiker Hallo Hallo gelokaliseerd.

* In welke stad hebt u uw eerste partner ontmoet?
* In welke stad hebben uw ouders elkaar leren kennen?
* In welke stad woont uw jongste of oudste broer of zus?
* In welke stad is uw vader geboren?
* In welke plaats hebt u uw eerste baan gehad?
* In welke stad is uw moeder geboren?
* In welke plaats was u op oudejaarsavond in 2000?
* Wat is de achternaam op Hallo van uw favoriete leraar op hoog * school?
* Wat is de naam Hallo universiteit bent u toegepast toobut niet letten?
* Wat is de naam Hallo van Hallo plaats waar u uw trouwreceptie gehouden?
* Wat is de tweede naam van uw vader?
* Wat is uw lievelingseten?
* Wat zijn de voor- en achternaam van uw oma van moederskant?
* Wat is de tweede naam van uw moeder?
* Wat is uw oudste Broer of zus geboren maand en jaar? (bijvoorbeeld November 1985)
* Wat is de tweede naam van uw oudste broer of zus?
* Wat zijn de voor- en achternaam van uw opa van vaderskant?
* Wat is de tweede naam van uw jongste broer of zus?
* Op welke school zat u in de brugklas?
* Wat is voor het eerst Hallo- en achternaam van uw beste jeugdvriend?
* Wat is voor het eerst Hallo- en achternaam van uw eerste partner?
* Wat is de achternaam van uw favoriete lagere school docent hello?
* Wat is Hallo merk en model van uw eerste auto of motor?
* Wat is de naam Hallo van Hallo eerste school?
* Wat is de naam Hallo van Hallo ziekenhuis waarin u geboren?
* Wat is de naam Hallo Hallo straat staat of opgegroeid?
* Wat is de naam Hallo van uw jeugdidool?
* Wat is Hallo-naam van uw favoriete knuffeldier?
* Wat is de naam Hallo van uw eerste huisdier?
* Wat was uw bijnaam als kind?
* Wat was uw favoriete sport op de middelbare school?
* Wat was uw eerste baan?
* Wat zijn de laatste vier cijfers van het telefoonnummer van uw Ouderlijk Hallo?
* Als u jonge zijn, wat wilde u toobe toen u klein was?
* Wie is Hallo van de grootste beroemdheid die u ooit hebt ontmoet?

### <a name="custom-security-questions"></a>Aangepaste beveiligingsvragen

Aangepaste beveiligingsvragen zijn niet gelokaliseerd voor verschillende talen. Alle aangepaste vragen worden weergegeven in Hallo dezelfde taal als ze worden ingevoerd in de interface van de gebruiker met beheerdersrechten Hallo zelfs als de landinstellingen van de browser van de gebruiker Hallo verschilt. Als u gelokaliseerde vragen, gebruik Hallo vooraf gedefinieerde vragen.

Hallo maximale lengte van een aangepaste beveiligingsvraag is 200 tekens.

### <a name="security-question-requirements"></a>Vraag de beveiligingsvereisten

* Minimale antwoord maximum aantal tekens is 3 tekens
* Maximale antwoord maximum aantal tekens is 40 tekens
* Gebruikers kunnen geen antwoord Hallo dezelfde vraag meer dan één keer
* Gebruikers kunnen geen Hallo dezelfde toomore dan één vraag te beantwoorden
* Een tekenset mogelijk gebruikte toodefine vragen en antwoorden, met inbegrip van Unicode-tekens
* Hallo aantal vragen dat is gedefinieerd moet groter zijn dan of gelijk aan het aantal vragen vereist tooregister toohello

## <a name="registration"></a>Registratie

### <a name="require-users-tooregister-when-signing-in"></a>Gebruikers tooregister vereist als u zich aanmeldt

Deze optie inschakelt, moet toocomplete Hallo wachtwoord opnieuw instellen van registratie van een gebruiker die is ingeschakeld voor wachtwoord opnieuw instellen als ze zich aanmelden met behulp van Azure AD-toosign in zoals die Volg tooapplications:

* Office 365
* Azure Portal
* Toegangsvenster
* Federatieve toepassingen
* Aangepaste toepassingen die gebruikmaken van Azure AD

Uitschakelen van deze functie wordt wel wilt toestaan dat gebruikers toomanually registreren hun contactgegevens in via [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) of door te klikken op Hallo **registreren voor wachtwoordherstel** koppeling onder Hallo profieltabblad in het toegangsvenster Hallo.

> [!NOTE]
> Gebruikers registratieportal voor wachtwoordherstel Hallo kunnen negeren door op Annuleren te klikken of sluit het venster Hallo maar telkens wanneer die ze zich aanmelden totdat ze registratie hebt voltooid, wordt gevraagd.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Aantal dagen voordat gebruikers worden gevraagd tooreconfirm hun verificatiegegevens

Deze optie bepaalt Hallo periode tussen instellen en verificatiegegevens reconfirming en is alleen beschikbaar als u Hallo inschakelt **gebruikers tooregister vereist als u zich aanmeldt** optie.

Geldige waarden zijn 0 730 dagen met 0, wat betekent dat gebruikers tooreconfirm nooit de verificatie-informatie te vragen

## <a name="notifications"></a>Meldingen

### <a name="notify-users-on-password-resets"></a>Gebruikers een melding tonen over het opnieuw instellen van hun wachtwoord

Als deze optie is ingesteld tooyes, ontvangt een melding dat hun wachtwoord is gewijzigd via Hallo SSPR portal tootheir primaire en alternatieve e-in het bestand in Azure AD mailadressen e-mailbericht met Hallo-gebruiker die hun wachtwoord opnieuw instelt. Niemand anders wordt de hoogte gesteld van deze opnieuw instellen van gebeurtenis.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Alle beheerders waarschuwen wanneer andere beheerders hun wachtwoord opnieuw instellen

Als deze optie is ingesteld tooyes, klikt u vervolgens **alle beheerders** ontvangt een e-mailadres tootheir primaire e-mailadres in het bestand in Azure AD melding dat hun wachtwoord met behulp van SSPR is gewijzigd door een andere beheerder.

Voorbeeld: Zijn er vier beheerders in een omgeving. Beheerder "A" instelt hun wachtwoord met behulp van SSPR. Beheerders B en C D ontvangen een e-mailbericht waarschuwen dat ze dit gebeurt.

## <a name="on-premises-integration"></a>On-premises integratie

Als u hebt geïnstalleerd, geconfigureerd en ingeschakeld Azure AD Connect hebt u aanvullende opties voor lokale integraties.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Terugschrijven van wachtwoorden tooyour on-premises adreslijst

Hiermee bepaalt u of wachtwoord terugschrijven is ingeschakeld voor deze map en als write-back ingeschakeld is, geeft de status Hallo van Hallo lokale Write-back-service. Dit is handig als u wilt dat tootemporarily uitschakelen Hallo wachtwoord terugschrijven zonder Azure AD Connect opnieuw te configureren.

* Als Hallo overschakelt is set-tooyes en Write-back wordt ingeschakeld, en federatieve en wachtwoord-hash gesynchroniseerd gebruikers kunnen tooreset hun wachtwoorden.
* Als Hallo overschakelt is set-toono en Write-back wordt uitgeschakeld, en federatieve en wachtwoord-hash gesynchroniseerd gebruikers tooreset kunnen niet worden hun wachtwoorden.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Gebruikers toestaan toounlock accounts zonder hun wachtwoord opnieuw instellen

Geeft aan of gebruikers die Hallo-portal voor wachtwoord opnieuw instellen bezoeken wordt gegeven Hallo optie toounlock hun lokale Active Directory accounts zonder hun wachtwoord opnieuw instellen of niet. Standaard Azure AD wordt altijd ontgrendeld accounts bij het uitvoeren van een wachtwoord opnieuw instellen, deze instelling kunt u tooseparate deze twee bewerkingen. 

* Als te ingesteld 'Ja', en vervolgens gebruikers wordt gegeven Hallo optie tooreset hun wachtwoord en Hallo-account of toounlock ontgrendelen zonder het Hallo-wachtwoord in te stellen.
* Als ingesteld te 'Nee', wordt gebruikers zich kunnen tooperform alleen een gecombineerde wachtwoord opnieuw instellen en het account bewerking ontgrendelen.

## <a name="network-requirements"></a>Netwerkvereisten

### <a name="firewall-rules"></a>Firewall-regels

[Lijst met Microsoft Office-URL's en IP-adressen](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Voor Azure AD Connect versie 1.1.443.0 en hoger, u moet HTTPS uitgaande toegang tot toohello volgende
* passwordreset.microsoftonline.com
* servicebus.Windows.NET

Voor meer gedetailleerd toegang vindt u de lijst bijgewerkt Hallo Microsoft Azure Datacenter IP-bereiken die is bijgewerkt van elke woensdag en in werking Hallo volgende geplaatst maandag [hier](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Time-outs voor niet-actieve verbindingen

Hello Azure AD Connect-hulpprogramma verzendt periodieke pings/keepalives tooServiceBus eindpunten tooensure Hallo verbindingen overleven. Moet Hallo hulpprogramma detecteert dat er te veel verbindingen zijn wordt afgesloten, wordt automatisch verhoogd Hallo frequentie van pings toohello eindpunt. Hallo laagste 'pingen intervallen' neerzetten toois 1 ping elke 60 seconden, maar we raden dat proxy's / firewalls toopersist voor inactieve verbindingen toestaan voor ten minste 2-3 minuten. * We raden vier minuten of langer voor oudere versies.

## <a name="active-directory-permissions"></a>Machtigingen voor Active Directory

Hallo-account opgegeven in hello Azure AD Connect-hulpprogramma moet hebben wachtwoord opnieuw instellen, wachtwoord wijzigen, schrijfmachtigingen op lockoutTime en schrijfmachtigingen op pwdLastSet, uitgebreide rechten op beide hoofdobject op Hallo van **elk domein** in dat forest **of** op Hallo gebruiker OE's die u wenst toobe binnen het bereik van SSPR.

Als u niet zeker weet welk account Hallo bovenstaande naar verwijst, opent u hello Azure Active Directory Connect de gebruikersinterface voor configuratie en klikt u op Hallo weergave huidige configuratie-optie Hallo account, moet je tooadd machtiging toois vermeld onder 'Mappen gesynchroniseerd'

Deze machtigingen kan Hallo MA-serviceaccount voor elk forest toomanage wachtwoorden namens de gebruikersaccounts binnen dat forest. **Als u niet tooassign deze machtigingen vervolgens terugschrijven toobe correct geconfigureerd weergegeven maar, optreden gebruikers fouten tijdens een poging de toomanage hun on-premises wachtwoorden vanuit Hallo cloud.**

> [!NOTE]
> Het kan tooan uur of langer voor deze machtigingen tooreplicate tooall objecten in uw directory duren.
>

tooset van de juiste machtigingen Hallo voor wachtwoord terugschrijven toooccur

1. Open Active Directory: gebruikers en Computers met een account met Hallo geschikt domein beheerdersrechten
2. Menu Beeld Hallo controleren dat geavanceerde functies is ingeschakeld
3. In het linkerdeelvenster Hallo met de rechtermuisknop op het Hallo-object dat Hallo hoofdmap van Hallo domein vertegenwoordigt en kies Eigenschappen
    * Klik op tabblad Hallo-beveiliging
    * Klik vervolgens op Geavanceerd.
4. Klik op toevoegen uit Hallo tabblad machtigingen
5. Selecteer Hallo-account dat machtigingen worden toegepast te (van Azure AD Connect-installatie)
6. Selecteer in de Hallo van toepassing toodrop omlaag onderliggende gebruikersobjecten
7. Klik onder machtigingen selectievakjes Hallo voor Hallo volgende
    * Unexpire wachtwoord
    * Wachtwoord opnieuw instellen
    * Wachtwoord wijzigen
    * LockoutTime schrijven
    * PwdLastSet schrijven
8. Klik op toepassen/OK via tooapply en sluit alle geopende dialoogvensters.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Hoe wachtwoord opnieuw instellen voor B2B-gebruikers?
Wachtwoord opnieuw instellen en wijzigen worden volledig ondersteund in alle B2B-configuraties.  Lees hieronder voor Hallo drie expliciete B2B gevallen wordt ondersteund door het wachtwoord opnieuw instellen.

1. **Gebruikers van een partner org met een bestaande Azure AD-tenant** : als u samenwerking met Hallo-organisatie een bestaande Azure AD-tenant heeft we **respecteren ongeacht wachtwoord opnieuw instellen van beleidsregels zijn ingeschakeld in deze tenant**. Voor wachtwoord opnieuw instellen van toowork, Hallo partner organisatie alleen behoeften toomake of Azure AD SSPR is ingeschakeld, die zonder extra kosten voor O365-klanten, en kan worden ingeschakeld door de volgende Hallo stappen in onze [aan de slag met wachtwoordbeheer ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) handleiding.
2. **Gebruikers die zich heeft aangemeld met behulp van [self-service aanmelding](active-directory-self-service-signup.md)**  : als u samenwerking met Hallo-organisatie Hallo gebruikt [self-service aanmelding](active-directory-self-service-signup.md) functie tooget in een tenant, we frameworkservice opnieuw instellen met Hallo e die ze geregistreerd.
3. **B2B-gebruikers** -nieuwe B2B gebruikers gemaakt met behulp van Hallo nieuwe [Azure AD B2B-mogelijkheden](active-directory-b2b-what-is-azure-ad-b2b.md) worden ook kunnen tooreset hun wachtwoorden met e-mailadres Hallo ze tijdens Hallo uitnodiging geregistreerd.

tootest deze, Ga toohttp://passwordreset.microsoftonline.com met een van deze partner-gebruikers. Zolang ze beschikken over een alternatieve e-mailadres of verificatie e-mailadres is gedefinieerd, heeft wachtwoord opnieuw instellen werkt zoals verwacht.

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

