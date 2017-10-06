---
title: 'Reporting: Azure AD SSPR | Microsoft Docs'
description: Rapportage van Azure AD zelf uw wachtwoord opnieuw instellen gebeurtenissen
services: active-directory
keywords: 
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
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Rapportageopties voor Azure AD-wachtwoordbeheer

Na de implementatie veel organisaties wilt tooknow hoe of als SSPR echt wordt gebruikt. Azure AD biedt rapportagefuncties die helpen u tooanswer vragen met behulp van rapporten blik en als u op de juiste wijze een licentie, kunt u toocreate aangepaste query's.

Hallo volgende vragen kunnen worden beantwoord door rapporten die zijn opgenomen in Hallo [Azure portal] (https://portal.azure.com/).

> [!NOTE]
> U moet [een globale beheerder](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) en moet opt-in voor dit toobe gegevens verzameld namens uw organisatie door bezoekende Hallo tabblad of audit reporting ten minste één keer registreert. Pas als u dit doet, wordt geen gegevens verzameld voor uw organisatie

* Hoeveel mensen hebben geregistreerd voor het wachtwoord opnieuw instellen?
* Die is geregistreerd voor het wachtwoord opnieuw instellen?
* Welke gegevens registreert personen?
* Hoeveel mensen hun wachtwoord opnieuw instellen in Hallo afgelopen zeven dagen?
* Wat zijn de meest voorkomende methoden gebruikers Hallo of beheerders hun wachtwoorden tooreset gebruiken?
* Wat zijn veelvoorkomende problemen met gebruikers of beheerders face tijdens een poging de toouse wachtwoord opnieuw instellen?
* Wat beheerders zijn opnieuw instellen van hun eigen wachtwoorden vaak?
* Is er een verdachte activiteit gebeurt met wachtwoord opnieuw instellen?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Hoe tooview wachtwoordbeheer rapporten in hello Azure-portal

In Azure portal ervaring hello hebben we een betere manier tooview wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van inschrijving activiteit.  Hallo stappen hieronder toofind Hallo wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van gebeurtenissen:

1. Navigeer te[**portal.azure.com**](https://portal.azure.com)
2. Klik op Hallo **meer services** menu op Hallo belangrijkste Azure portal linkermenubalk
3. Zoeken naar **Azure Active Directory** in de lijst met services Hallo en selecteert u het
4. Klik op **gebruikers en groepen** van hello Azure Active Directory-navigatiemenu
5. Klik op Hallo **controlelogboeken** navigatie-item van navigatiemenu Hallo gebruikers en groepen. Hiermee geeft u alle controlegebeurtenissen Hallo plaatsvindt tegen alle Hallo gebruikers in uw directory. U kunt deze toosee weergave alle Hallo wachtwoord-gerelateerde gebeurtenissen, evenals filteren.
6. toofilter gerelateerde gebeurtenissen voor deze weergave tooonly Hallo-wachtwoord opnieuw instellen, klikt u op Hallo **Filter** knop Hallo boven aan het Hallo-blade.
7. Van Hallo **Filter** menu, selecteer Hallo **categorie** vervolgkeuzelijst en wijzig deze toohello **Self-service wachtwoordbeheer** categorietype.
8. Eventueel verdere Hallo-filterlijst door te kiezen Hallo specifieke **activiteit** u geïnteresseerd bent

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Hoe tooretrieve wachtwoord management gebeurtenissen van Azure AD-rapporten en gebeurtenissen API Hallo

Hello Azure AD-rapporten en gebeurtenissen API biedt ondersteuning voor het ophalen van alle Hallo gegevens die zijn opgenomen in het wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van rapporten. U kunt afzonderlijke wachtwoordherstel downloaden met behulp van deze API en wachtwoord opnieuw instellen van registratie van gebeurtenissen voor integratie met Hallo reporting technologie van uw keuze.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Hoe tooget gestart Hello rapportage-API

tooaccess deze gegevens, of u kunt een kort app toowrite script tooretrieve op onze servers. [Meer informatie over hoe tooget gestart Hello Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

Zodra u een werkscript hebt, moet u naast tooexamine Hallo wachtwoord opnieuw instellen en registratie van gebeurtenissen, dat u toomeet uw scenario's ophalen kunt.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): geeft een lijst van beschikbare Hallo kolommen voor wachtwoord opnieuw instellen van gebeurtenissen
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): geeft een lijst van beschikbare Hallo kolommen voor gebeurtenissen van de registratie voor wachtwoord opnieuw instellen

### <a name="reporting-api-data-retrieval-limitations"></a>Rapportage-API-beperkingen voor gegevens ophalen

Op dit moment hello Azure AD-rapporten en gebeurtenissen API haalt te**75.000 afzonderlijke gebeurtenissen** Hallo [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) en [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typen , Hallo spanning **afgelopen 30 dagen**.

Als u tooretrieve moet of gegevens buiten dit venster opslaan, het is raadzaam het persistent maken in een externe database en het gebruik van Hallo API tooquery Hallo delta's die het resultaat. Onze aanbeveling is toobegin deze gegevens ophalen van SSPR gebruiken in uw organisatie, extern behouden en ga vervolgens verder met tootrack Hallo delta's vanaf dit punt doorsturen.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Hoe toodownload wachtwoordherstel registratie gebeurtenissen snel met PowerShell

Bovendien toousing Azure AD-rapporten en gebeurtenissen API rechtstreeks Hallo, u kunt ook Hallo onderstaande PowerShell-script toorecent registratie gebeurtenissen in uw directory. Dit is handig als u wilt dat toosee die onlangs is geregistreerd of u wilt dat uw wachtwoord opnieuw instellen van implementatie tooensure optreedt zoals verwacht.

* [Azure AD SSPR-registratie activiteit PowerShell-Script](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Beschrijving van de kolommen in Azure-portal

Hallo volgt een lijst met elk van de Hallo rapportkolommen in detail:

* **Gebruiker** – Hallo-gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen van bewerking voor de registratie.
* **Rol** – Hallo-rol van Hallo Hallo-directory-gebruiker.
* **Datum en tijd** – Hallo-datum en tijd van de Hallo poging.
* **Geregistreerde gegevens** : registratie van welke verificatie gegevens Hallo gebruiker is opgegeven tijdens het wachtwoord opnieuw instellen.

### <a name="description-of-report-values-in-azure-portal"></a>Beschrijving van de waarden in Azure-portal

Hallo staan volgende tabel verschillende Hallo-waarden toegestaan voor elke kolom:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Gegevens die zijn geregistreerd |**Alternatief e-mailadres** – gebruiker gebruikt alternatieve e-mailadres of verificatie e tooauthenticate<p><p>**Telefoon (werk)**– gebruiker gebruikt office phone tooauthenticate<p>**Mobiele telefoon** -gebruiker mobiele telefoon of verificatie phone tooauthenticate gebruikt<p>**Beveiligingsvragen** – gebruikt gebruikersbeveiliging tooauthenticate vragen<p>**Een combinatie van Hallo hierboven (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven en ziet u welke twee methoden Hallo gebruiker gebruikt tooauthentication verzoek voor hun wachtwoord opnieuw instellen. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>De activiteit in de klassieke portal Hallo weergave wachtwoord opnieuw instellen

Dit rapport geeft dat alle pogingen die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel.

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Beschrijving van de kolommen in de klassieke Azure-portal

Hallo volgt een lijst met elk van de Hallo rapportkolommen in detail:

1. **Gebruiker** – Hallo-gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen voor bewerking (op basis van veld Hallo-gebruikers-ID als Hallo gebruiker afkomstig tooreset een wachtwoord is opgegeven).
2. **Rol** – Hallo-rol van Hallo Hallo-directory-gebruiker.
3. **Datum en tijd** – Hallo-datum en tijd van de Hallo poging.
4. **Methoden gebruikt** – welke verificatiemethoden Hallo gebruiker gebruikt voor deze bewerking opnieuw instellen.
5. **Resultaat** – Hallo resultaat van het Hallo-wachtwoord opnieuw instellen.
6. **Details** – Hallo details van waarom Hallo wachtwoordherstel resulteerde in Hallo waarde dat het geval was.  Omvat ook eventuele risicobeperking stappen mogelijk tooresolve is een onverwachte fout.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Beschrijving van het rapport waarden in de klassieke Azure-portal

Hallo staan volgende tabel verschillende Hallo-waarden toegestaan voor elke kolom:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Methoden die worden gebruikt |**Alternatief e-mailadres** – gebruiker gebruikt alternatieve e-mailadres of verificatie e tooauthenticate<p>**Telefoon (werk)** – gebruiker gebruikt office phone tooauthenticate<p>**Mobiele telefoon** – gebruiker de mobiele telefoon of verificatie phone tooauthenticate gebruikt<p>**Beveiligingsvragen** – gebruikt gebruikersbeveiliging tooauthenticate vragen<p>**Een combinatie van Hallo hierboven (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven en ziet u welke twee methoden Hallo gebruiker gebruikt tooauthentication verzoek voor hun wachtwoord opnieuw instellen. |
| Resultaat |**Afgebroken** – gebruiker opnieuw instellen van wachtwoorden is gestart maar wordt gestopt halverwege via zonder te voltooien<p>**Geblokkeerd** : gebruikersaccount is toouse wachtwoordherstel vanwege tooattempting toouse Hallo wachtwoord opnieuw instellen van pagina of een enkel wachtwoord opnieuw instellen in gate te vaak een periode van 24 uur<p>**Geannuleerd** – wachtwoord opnieuw instellen is gestart, maar vervolgens geklikt op Hallo annuleren knop toocancel Hallo sessie gedeeltelijk manier tot en met de gebruiker <p>**Verbinding gemaakt met de beheerder** – gebruiker heeft een probleem opgetreden tijdens de sessie die hij kan niet worden omgezet, zodat de gebruiker Hallo geklikt 'Contact op met uw beheerder' Hallo-koppeling niet is voltooid Hallo wachtwoordherstel stroom<p>**Kan geen** : gebruiker is niet kunnen tooreset een wachtwoord, waarschijnlijk omdat Hallo gebruiker niet geconfigureerd toouse Hallo-functie is (bijvoorbeeld geen licentie, ontbrekende gegevens voor verificatie, wachtwoord beheerd on-premises maar Write-back is uitgeschakeld).<p>**Geslaagd** – wachtwoordherstel is geslaagd. |
| Details |Zie de onderstaande tabel |

### <a name="allowed-values-for-details-column"></a>Toegestane waarden voor de kolom voor meer informatie

Hierna volgt de lijst Hallo van u verwachten mag wanneer het Hallo-wachtwoord opnieuw instellen activiteitenrapport resultaattypen:

| Details | Resultaattype |
| --- | --- |
| Gebruiker afgebroken na het voltooien van e-verificatieoptie Hallo |Afgebroken |
| Gebruiker afgebroken na het voltooien van de mobiele SMS Hallo-verificatieoptie |Afgebroken |
| Gebruiker afgebroken na het voltooien van Hallo mobiele stem aanroep verificatieoptie |Afgebroken |
| Gebruiker afgebroken na het voltooien van de optie voor verificatie van Hallo office stem aanroep |Afgebroken |
| Gebruiker afgebroken na het voltooien van de beveiligingsoptie vragen Hallo |Afgebroken |
| Gebruiker afgebroken na het invoeren van hun gebruikers-ID |Afgebroken |
| Gebruiker afgebroken na het starten van e-verificatieoptie Hallo |Afgebroken |
| Gebruiker afgebroken na het starten van de mobiele SMS Hallo-verificatieoptie |Afgebroken |
| Gebruiker afgebroken na het Hallo mobiele stem aanroep verificatieoptie starten |Afgebroken |
| Gebruiker afgebroken na het starten van de optie voor verificatie van Hallo office stem aanroep |Afgebroken |
| Gebruiker afgebroken na het starten van de beveiligingsoptie vragen Hallo |Afgebroken |
| Gebruiker is afgebroken voordat u een nieuw wachtwoord |Afgebroken |
| Gebruiker afgebroken bij het selecteren van een nieuw wachtwoord |Afgebroken |
| Gebruiker heeft te veel ongeldige SMS verificatiecodes ingevoerd en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd voice-verificatie van mobiele telefoon en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd stem verificatie via de telefoon office en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd tooanswer beveiligingsvragen en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd tooverify een telefoonnummer en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft geannuleerd voordat deze verificatiemethoden Hallo vereist |Geannuleerd |
| Gebruiker heeft geannuleerd vóór het verzenden van een nieuw wachtwoord |Geannuleerd |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd Hallo e-verificatieoptie |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd Hallo mobiele SMS-verificatieoptie |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd Hallo mobiele stem aanroep verificatieoptie |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd Hallo office stem aanroep verificatie-optie |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd Hallo beveiliging vraag verificatieoptie |Verbinding met admin |
| Wachtwoord opnieuw instellen is niet ingeschakeld voor deze gebruiker. Inschakelen voor wachtwoordherstel onder Hallo tabblad tooresolve dit configureren |Is mislukt |
| Gebruiker beschikt niet over een licentie. U kunt een licentie toohello gebruiker tooresolve dit toevoegen |Is mislukt |
| Gebruiker heeft geprobeerd een tooreset van een apparaat zonder cookies zijn ingeschakeld |Is mislukt |
| Gebruikersaccount heeft onvoldoende verificatiemethoden die zijn gedefinieerd. Deze verificatie info tooresolve toevoegen |Is mislukt |
| Het wachtwoord van gebruiker is on-premises worden beheerd. U kunt wachtwoord terugschrijven tooresolve dit inschakelen |Is mislukt |
| Uw on-premises wachtwoord opnieuw instellen-service kan niet worden bereikt. Controleer het gebeurtenislogboek van de synchronisatie-computer |Is mislukt |
| Er is een probleem opgetreden bij het opnieuw instellen van de gebruiker Hallo on-premises wachtwoord. Controleer het gebeurtenislogboek van de synchronisatie-computer |Is mislukt |
| Deze gebruiker is geen lid van groep van Hallo wachtwoord opnieuw instellen van gebruikers. Voeg deze gebruiker toothat groep tooresolve deze. |Is mislukt |
| Wachtwoord opnieuw instellen is volledig voor deze tenant is uitgeschakeld. Zie [hier](http://aka.ms/ssprtroubleshoot) tooresolve dit. |Is mislukt |
| Gebruiker is opnieuw ingesteld wachtwoord |Geslaagd |

## <a name="self-service-password-management-activity-types"></a>Wachtwoordbeheer activiteitstypen selfservice

Hallo volgende activiteitstypen worden weergegeven in Hallo **Self-Service wachtwoordbeheer** audit gebeurteniscategorie.  Een beschrijving voor elk volgt.

* [**Selfservice voor wachtwoordherstel geblokkeerd** ](#activity-type-blocked-from-self-service-password-reset) -geeft aan een gebruiker heeft geprobeerd een tooreset een wachtwoord, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* [**Wachtwoord (self-service) wijzigen** ](#activity-type-change-password-self-service) -geeft aan een gebruiker een vrijwillige uitgevoerd of gedwongen (vanwege tooexpiry) wijzigen van wachtwoorden.
* [**Wachtwoord opnieuw instellen (door admin)** ](#activity-type-reset-password-by-admin) -geeft aan dat een beheerder een namens een gebruiker uit hello Azure-portal voor wachtwoordherstel uitgevoerd.
* [**Wachtwoord opnieuw instellen (self-service)** ](#activity-type-reset-password-self-service) -geeft aan een gebruiker gereset hun wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* [**Selfservice voor wachtwoordherstel stroom activiteit uitgevoerd** ](#activity-type-self-serve-password-reset-flow-activity-progress) -geeft aan elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het Hallo-wachtwoord opnieuw instellen van proces.
* [**Ontgrendelen van gebruikersaccount (self-service)** ](#activity-type-unlock-user-account-self-service) -geeft aan een gebruiker de Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van het wachtwoord van Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) gebruiken Hallo AD-account ontgrendelen zonder de functie.
* [**Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel** ](#activity-type-user-registered-for-self-service-password-reset) -geeft aan een gebruiker is geregistreerd alle Hallo vereist informatie toobe kunnen tooreset hun wachtwoord in overeenstemming met Hallo opgegeven momenteel tenant wachtwoord opnieuw instellen van beleid.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Activiteitstype: geen toegang tot selfservice voor wachtwoordherstel

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker heeft geprobeerd tooreset een wachtwoord, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* **Activiteit Actor** -resetbewerkingen Hallo-gebruiker die uit te voeren extra is beperkt. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -resetbewerkingen Hallo-gebruiker die uit te voeren extra is beperkt. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker is beperkt van eventuele aanvullende opnieuw uitvoert, probeert een extra verificatiemethoden of eventuele extra telefoonnummers voor Hallo valideren binnen 24 uur.
* **Reden van de activiteit Status Fout** : niet van toepassing

### <a name="activity-type-change-password-self-service"></a>Activiteitstype: wachtwoord wijzigen (self-service)

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – Hiermee geeft u een gebruiker vrijwillig uitgevoerd of gedwongen (vanwege tooexpiry) wijzigen van wachtwoorden.
* **Activiteit Actor** -Hallo-gebruiker die hun wachtwoord gewijzigd. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die hun wachtwoord gewijzigd. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker het wachtwoord is gewijzigd
  * _Fout_ -geeft aan een gebruiker is mislukt toochange hun wachtwoord. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Reden van de activiteit Status Fout** - 
  * _FuzzyPolicyViolationInvalidPassword_ -Hallo gebruiker een wachtwoord dat automatisch is verboden vervaldatum van tooMicrosoft verboden wachtwoord detectiemogelijkheden vinden toobe te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-reset-password-by-admin"></a>Activiteitstype: wachtwoord opnieuw instellen (door de beheerder)

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een beheerder een namens een gebruiker uit hello Azure-portal voor wachtwoordherstel uitgevoerd.
* **Activiteit Actor** -Hallo beheerder Hallo wachtwoordherstel namens een andere gebruiker of beheerder uitgevoerd. Moet een globale beheerder, een wachtwoordbeheerder, een Gebruikersbeheerder of een beheerder van de helpdesk.
* **Doel van de activiteit** -Hallo gebruiker waarvan het wachtwoord is opnieuw ingesteld. Mogelijk een eindgebruiker of een andere beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft een beheerder is opnieuw ingesteld wachtwoord van een gebruiker
  * _Fout_ -aangeeft dat een beheerder is mislukt toochange wachtwoord van een gebruiker. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.

### <a name="activity-type-reset-password-self-service"></a>Activiteitstype: wachtwoord opnieuw instellen (self-service)

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker gereset hun wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* **Activiteit Actor** -Hallo-gebruiker die hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker met succes hun eigen wachtwoord opnieuw instellen
  * _Fout_ -geeft aan een gebruiker is mislukt tooreset hun eigen wachtwoord. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Reden van de activiteit Status Fout** -
  * _FuzzyPolicyViolationInvalidPassword_ -Hallo beheerder een wachtwoord dat automatisch is verboden vervaldatum van tooMicrosoft verboden wachtwoord detectiemogelijkheden vinden toobe te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Activiteitstype: eigen wachtwoord opnieuw instellen van stroom activiteit uitgevoerd beheer

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het Hallo-wachtwoord opnieuw instellen van proces aan.
* **Activiteit Actor** -Hallo-gebruiker die heeft uitgevoerd deel uit van het Hallo-wachtwoord opnieuw instellen van stroom. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die heeft uitgevoerd deel uit van het Hallo-wachtwoord opnieuw instellen van stroom. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker een specifieke stap van de stroom van Hallo wachtwoord opnieuw instellen is voltooid.
  * _Fout_ -geeft aan een specifieke stap Hallo wachtwoord opnieuw instellen van stroom is mislukt. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Activiteit statusredenen toegestaan**
  * Zie onderstaande tabel voor [alle toegestaan activiteit opnieuw instellen van statusredenen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Activiteitstype: ontgrendelen gebruikersaccount (self-service)

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker de Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van het wachtwoord van Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met Hallo AD-account ontgrendelen zonder opnieuw instellen functie.
* **Activiteit Actor** -Hallo-gebruiker die het account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die het account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker een eigen account is ontgrendeld
  * _Fout_ -geeft aan een gebruiker is mislukt toounlock hun account. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Activiteitstype: gebruiker is geregistreerd voor selfservice voor wachtwoordherstel

Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker is geregistreerd alle Hallo vereist informatie toobe kunnen tooreset hun wachtwoord in overeenstemming met Hallo opgegeven momenteel tenant wachtwoord opnieuw instellen van beleid. 
* **Activiteit Actor** -Hallo-gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker is geregistreerd voor wachtwoordherstel in overeenstemming met het huidige beleid Hallo. 
  * _Fout_ -geeft aan een gebruiker is mislukt-tooregister voor wachtwoordherstel. Te klikken op Hallo rij kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden. Opmerking: dit betekent niet dat een gebruiker kan niet tooreset hun eigen wachtwoord, net is ze niet Hallo registratieproces voltooid is. Als er niet-geverifieerde gegevens op hun account juist (zoals een telefoonnummer die niet worden gevalideerd), zelfs als ze dit telefoonnummer niet hebt gecontroleerd, ze kunnen nog steeds gebruiken deze tooreset hun wachtwoord. Zie voor meer informatie [wat er gebeurt wanneer een gebruiker registreert?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [Snelkoppeling toouser management controlelogboeken](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - Ga direct controlelogboeken van de tenant tooyour Gebruikersbeheer
* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
