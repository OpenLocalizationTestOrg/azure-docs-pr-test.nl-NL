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
ms.openlocfilehash: ba7b36e654aa0bf3b74d42a2b0ae96ae2a9b6241
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Rapportageopties voor Azure AD-wachtwoordbeheer

Na de implementatie veel organisaties willen weten hoe of als SSPR echt wordt gebruikt. Azure AD levert rapportagefuncties die u helpen bij het beantwoorden van vragen met behulp van voorgedefinieerde rapporten en u op de juiste wijze een licentie, kunt u aangepaste query's maken.

Kunnen de volgende vragen worden beantwoord door rapporten die zijn opgenomen in de [Azure portal] (https://portal.azure.com/).

> [!NOTE]
> U moet [een globale beheerder](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) en moet aanmelden voor deze gegevens worden verzameld namens uw organisatie door naar de logboeken van de reporting tabblad of audit ten minste één keer te gaan. Pas als u dit doet, wordt geen gegevens verzameld voor uw organisatie

* Hoeveel mensen hebben geregistreerd voor het wachtwoord opnieuw instellen?
* Die is geregistreerd voor het wachtwoord opnieuw instellen?
* Welke gegevens registreert personen?
* Hoeveel mensen dat op het in de afgelopen zeven dagen hun wachtwoord opnieuw instellen?
* Wat zijn de meest voorkomende methoden gebruikers of beheerders gebruiken hun wachtwoorden opnieuw kunnen instellen?
* Wat zijn veelvoorkomende problemen met gebruikers of beheerders face bij een poging tot het gebruik van wachtwoord opnieuw instellen?
* Wat beheerders zijn opnieuw instellen van hun eigen wachtwoorden vaak?
* Is er een verdachte activiteit gebeurt met wachtwoord opnieuw instellen?

## <a name="how-to-view-password-management-reports-in-the-azure-portal"></a>Wachtwoord-rapporten weergeven in de Azure-portal

In de Azure portal ervaring hebben we een betere manier om weer te geven voor wachtwoordherstel en registratie-activiteit wachtwoord opnieuw instellen.  Volg onderstaande stappen voor het vinden van dat het wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen registratie gebeurtenissen:

1. Navigeer naar [ **portal.azure.com**](https://portal.azure.com)
2. Klik op de **meer services** menu op de belangrijkste Azure portal linkermenubalk
3. Zoeken naar **Azure Active Directory** in de lijst met services en dit selecteren
4. Klik op **gebruikers en groepen** uit het navigatiemenu Azure Active Directory
5. Klik op de **controlelogboeken** navigatie-item van het navigatiemenu gebruikers en groepen. Hiermee geeft u alle van de controlegebeurtenissen die plaatsvinden op basis van de gebruikers in uw directory. U kunt deze weergeven voor een overzicht van alle de wachtwoord-gerelateerde gebeurtenissen ook filteren.
6. Als u wilt filteren deze weergave zodanig dat alleen het wachtwoord opnieuw instellen van gerelateerde gebeurtenissen, klikt u op de **Filter** knop aan de bovenkant van de blade.
7. Van de **Filter** selecteert u de **categorie** vervolgkeuzelijst en wijzig dit in de **Self-service wachtwoordbeheer** categorietype.
8. Eventueel verdere filter de lijst door het kiezen van de specifieke **activiteit** u geïnteresseerd bent

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Het ophalen van gebeurtenissen voor wachtwoord van de Azure AD-rapporten en gebeurtenissen API

De Azure AD-rapporten en gebeurtenissen API ondersteunt bij het ophalen van de gegevens die zijn opgenomen in het wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van rapporten. Met behulp van deze API kunt u afzonderlijke wachtwoordherstel downloaden en gebeurtenissen voor de integratie met de reporting-technologie van uw keuze registratie voor wachtwoord opnieuw instellen.

### <a name="how-to-get-started-with-the-reporting-api"></a>Hoe u aan de slag met de rapportage-API

Voor toegang tot deze gegevens, moet u een kleine app of het script voor het ophalen van onze servers worden geschreven. [Meer informatie over het aan de slag met de Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

Zodra u een werkende script hebt, wilt u naast de wachtwoord opnieuw instellen en registratie gebeurtenissen onderzoeken die u ophalen kunt om te voldoen aan uw scenario's.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): geeft een lijst van de beschikbare kolommen voor wachtwoord opnieuw instellen van gebeurtenissen
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): geeft een lijst van de beschikbare kolommen voor gebeurtenissen van de registratie voor wachtwoord opnieuw instellen

### <a name="reporting-api-data-retrieval-limitations"></a>Rapportage-API-beperkingen voor gegevens ophalen

Op dit moment wordt de Azure AD-rapporten en gebeurtenissen API haalt maximaal **75.000 afzonderlijke gebeurtenissen** van de [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) en [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typen, spanning de **afgelopen 30 dagen**.

Als u wilt ophalen of gegevens buiten dit venster opslaan, het is raadzaam het persistent maken in een externe database en de API gebruiken om op te vragen van de delta's die het resultaat. Onze aanbeveling is begonnen met het ophalen van deze gegevens wanneer u begint met behulp van SSPR in uw organisatie, extern behouden en vervolgens doorgaan met het bijhouden van de delta's vanaf dit punt.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Het downloaden van wachtwoord opnieuw instellen van inschrijving gebeurtenissen snel met PowerShell

Naast het rechtstreeks gebruik van de Azure AD-rapporten en gebeurtenissen API, u kunt ook de onderstaande PowerShell-script voor een recente registratie gebeurtenissen in uw directory. Dit is handig als u zien wie onlangs is geregistreerd of wilt ervoor te zorgen wilt dat uw wachtwoord opnieuw instellen van implementatie plaatsvindt zoals verwacht.

* [Azure AD SSPR-registratie activiteit PowerShell-Script](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Beschrijving van de kolommen in Azure-portal

De volgende lijst wordt elk van de rapportkolommen in detail uitgelegd:

* **Gebruiker** – de gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen van bewerking voor de registratie.
* **Rol** : de rol van de gebruiker in de directory.
* **Datum en tijd** – de datum en tijd van de poging.
* **Geregistreerde gegevens** : registratie van welke verificatiegegevens die de gebruiker tijdens het wachtwoord opgegeven opnieuw instellen.

### <a name="description-of-report-values-in-azure-portal"></a>Beschrijving van de waarden in Azure-portal

De volgende tabel beschrijft de verschillende waarden voor elke kolom toegestaan:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Gegevens die zijn geregistreerd |**Alternatief e-mailadres** – gebruiker alternatieve e-mailadres of verificatie e-mailadres gebruikt om te verifiëren<p><p>**Telefoon (werk)**– telefoon (werk) gebruiker gebruikt om te verifiëren<p>**Mobiele telefoon** -gebruiker gebruikt mobiele telefoon of telefoon voor authenticatie om te verifiëren<p>**Beveiligingsvragen** – gebruiker beveiligingsvragen gebruikt om te verifiëren<p>**Een combinatie van de bovenstaande (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven, ziet u welke twee methoden voor de gebruiker gebruikt voor verificatie aanvraag hun wachtwoord opnieuw instellen. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Activiteit in de klassieke portal voor wachtwoordherstel weergeven

Dit rapport geeft dat alle pogingen die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel.

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Beschrijving van de kolommen in de klassieke Azure-portal

De volgende lijst wordt elk van de rapportkolommen in detail uitgelegd:

1. **Gebruiker** – de gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen voor bewerking (op basis van het veld User ID is opgegeven bij de gebruiker een wachtwoord opnieuw instellen).
2. **Rol** : de rol van de gebruiker in de directory.
3. **Datum en tijd** – de datum en tijd van de poging.
4. **Methoden gebruikt** – welke verificatiemethoden die de gebruiker voor deze gebruikt bewerking opnieuw.
5. **Resultaat** : het resultaat van het wachtwoord opnieuw instellen.
6. **Details** : meer informatie over waarom het wachtwoord opnieuw instellen in de waarde die het heeft geleid.  Tevens alle stappen die u nemen kunt voor het oplossen van een onverwachte fout.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Beschrijving van het rapport waarden in de klassieke Azure-portal

De volgende tabel beschrijft de verschillende waarden voor elke kolom toegestaan:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Methoden die worden gebruikt |**Alternatief e-mailadres** – gebruiker alternatieve e-mailadres of verificatie e-mailadres gebruikt om te verifiëren<p>**Telefoon (werk)** – telefoon (werk) gebruiker gebruikt om te verifiëren<p>**Mobiele telefoon** – gebruiker gebruikt mobiele telefoon of telefoon voor authenticatie om te verifiëren<p>**Beveiligingsvragen** – gebruiker beveiligingsvragen gebruikt om te verifiëren<p>**Een combinatie van de bovenstaande (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven, ziet u welke twee methoden voor de gebruiker gebruikt voor verificatie aanvraag hun wachtwoord opnieuw instellen. |
| Resultaat |**Afgebroken** – gebruiker opnieuw instellen van wachtwoorden is gestart maar wordt gestopt halverwege via zonder te voltooien<p>**Geblokkeerd** : gebruikersaccount is geblokkeerd voor het gebruik van wachtwoord opnieuw instellen als gevolg van probeert te gebruiken van de wachtwoordpagina opnieuw instellen of een enkel wachtwoord opnieuw instellen in gate te vaak een periode van 24 uur<p>**Geannuleerd** – wachtwoord opnieuw instellen is gestart, maar vervolgens geklikt op de knop Annuleren als u wilt annuleren van de sessie gedeeltelijk manier tot en met de gebruiker <p>**Verbinding gemaakt met de beheerder** – gebruiker heeft een probleem opgetreden tijdens de sessie die hij kan niet worden omgezet, zodat de gebruiker heeft geklikt voor de koppeling 'Contact op met uw beheerder' in plaats van het voltooien van het wachtwoord opnieuw instellen stroom<p>**Kan geen** – gebruiker kon niet opnieuw instellen van een wachtwoord, waarschijnlijk omdat de gebruiker niet is geconfigureerd voor het gebruik van de functie (bijvoorbeeld geen licentie, ontbrekende gegevens voor verificatie, wachtwoord beheerd on-premises maar Write-back is uitgeschakeld).<p>**Geslaagd** – wachtwoordherstel is geslaagd. |
| Details |Zie de onderstaande tabel |

### <a name="allowed-values-for-details-column"></a>Toegestane waarden voor de kolom voor meer informatie

Hieronder vindt u de lijst met resultaattypen verwacht wanneer activiteitenrapport met het wachtwoord opnieuw:

| Details | Resultaattype |
| --- | --- |
| Gebruiker afgebroken na het voltooien van de optie voor e-verificatie |Afgebroken |
| Gebruiker afgebroken na het voltooien van de mobiele optie van de SMS-verificatie |Afgebroken |
| Gebruiker afgebroken na het voltooien van de optie mobiele stem aanroep verificatie |Afgebroken |
| Gebruiker afgebroken na het voltooien van de optie voor verificatie van office stem aanroep |Afgebroken |
| Gebruiker afgebroken na het voltooien van de beveiliging optie vragen |Afgebroken |
| Gebruiker afgebroken na het invoeren van hun gebruikers-ID |Afgebroken |
| Gebruiker afgebroken na het starten van de optie voor e-verificatie |Afgebroken |
| Gebruiker afgebroken na het starten van de mobiele optie van de SMS-verificatie |Afgebroken |
| Gebruiker afgebroken na het starten van de optie mobiele stem aanroep verificatie |Afgebroken |
| Gebruiker afgebroken na het starten van de optie voor verificatie van office stem aanroep |Afgebroken |
| Gebruiker afgebroken na het starten van de beveiliging optie vragen |Afgebroken |
| Gebruiker is afgebroken voordat u een nieuw wachtwoord |Afgebroken |
| Gebruiker afgebroken bij het selecteren van een nieuw wachtwoord |Afgebroken |
| Gebruiker heeft te veel ongeldige SMS verificatiecodes ingevoerd en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd voice-verificatie van mobiele telefoon en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft te vaak geprobeerd stem verificatie via de telefoon office en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft geprobeerd te beantwoorden van beveiligingsvragen te vaak en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft geprobeerd om te controleren of een telefoonnummer te vaak en 24 uur is geblokkeerd |Geblokkeerd |
| Gebruiker heeft geannuleerd voordat deze de vereiste verificatiemethoden |Geannuleerd |
| Gebruiker heeft geannuleerd vóór het verzenden van een nieuw wachtwoord |Geannuleerd |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd het e-verificatieoptie |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd de optie voor verificatie van mobiele SMS |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd de verificatieoptie mobiele stem aanroep |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd de verificatieoptie office stem aanroep |Verbinding met admin |
| Gebruiker verbinding gemaakt met een beheerder nadat u hebt geprobeerd de beveiligingsoptie van de vraag-verificatie |Verbinding met admin |
| Wachtwoord opnieuw instellen is niet ingeschakeld voor deze gebruiker. Wachtwoord opnieuw instellen op het tabblad configureren om op te lossen dit inschakelen |Is mislukt |
| Gebruiker beschikt niet over een licentie. U kunt een licentie toevoegen aan de gebruiker kan dit probleem oplossen |Is mislukt |
| De gebruiker heeft geprobeerd om in te stellen van een apparaat zonder cookies zijn ingeschakeld |Is mislukt |
| Gebruikersaccount heeft onvoldoende verificatiemethoden die zijn gedefinieerd. Verificatie-informatie om dit probleem oplossen toevoegen |Is mislukt |
| Het wachtwoord van gebruiker is on-premises worden beheerd. U kunt wachtwoord terugschrijven oplossing inschakelen |Is mislukt |
| Uw on-premises wachtwoord opnieuw instellen-service kan niet worden bereikt. Controleer het gebeurtenislogboek van de synchronisatie-computer |Is mislukt |
| Er is een probleem opgetreden tijdens het opnieuw instellen van de gebruiker lokale wachtwoord. Controleer het gebeurtenislogboek van de synchronisatie-computer |Is mislukt |
| Deze gebruiker is geen lid van de gebruikersgroep voor wachtwoord opnieuw instellen. Deze gebruiker toevoegen aan die groep oplossing. |Is mislukt |
| Wachtwoord opnieuw instellen is volledig voor deze tenant is uitgeschakeld. Zie [hier](http://aka.ms/ssprtroubleshoot) oplossing. |Is mislukt |
| Gebruiker is opnieuw ingesteld wachtwoord |Geslaagd |

## <a name="self-service-password-management-activity-types"></a>Wachtwoordbeheer activiteitstypen selfservice

De volgende activiteitstypen worden weergegeven in de **Self-Service wachtwoordbeheer** audit gebeurteniscategorie.  Een beschrijving voor elk volgt.

* [**Selfservice voor wachtwoordherstel geblokkeerd** ](#activity-type-blocked-from-self-service-password-reset) -geeft aan een gebruiker heeft geprobeerd een wachtwoord opnieuw instellen, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* [**Wachtwoord (self-service) wijzigen** ](#activity-type-change-password-self-service) -geeft aan een gebruiker een vrijwillige uitgevoerd of gedwongen (als gevolg van verlopen) wijzigen van wachtwoorden.
* [**Wachtwoord opnieuw instellen (door admin)** ](#activity-type-reset-password-by-admin) -geeft aan dat een beheerder een namens een gebruiker vanuit de Azure-portal voor wachtwoordherstel uitgevoerd.
* [**Wachtwoord opnieuw instellen (self-service)** ](#activity-type-reset-password-self-service) -geeft aan een gebruiker gereset hun wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* [**Selfservice voor wachtwoordherstel stroom activiteit uitgevoerd** ](#activity-type-self-serve-password-reset-flow-activity-progress) -geeft aan elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het wachtwoord opnieuw instellen van proces.
* [**Ontgrendelen van gebruikersaccount (self-service)** ](#activity-type-unlock-user-account-self-service) -geeft aan een gebruiker de Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van het wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met behulp van het AD-account ontgrendelen zonder de functie.
* [**Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel** ](#activity-type-user-registered-for-self-service-password-reset) -geeft aan een gebruiker de vereiste informatie om te kunnen hun wachtwoord in overeenstemming met het beleid voor wachtwoordherstel momenteel opgegeven tenant is geregistreerd.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Activiteitstype: geen toegang tot selfservice voor wachtwoordherstel

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker heeft geprobeerd te uw wachtwoord opnieuw instellen, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* **Activiteit Actor** -bewerkingen door de gebruiker die is beperkt uit te voeren aanvullende opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -bewerkingen door de gebruiker die is beperkt uit te voeren aanvullende opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker is beperkt uit te voeren eventuele aanvullende opnieuw ingesteld, geen extra verificatiemethoden proberen of eventuele extra telefoonnummers valideren voor de eerstvolgende 24 uur.
* **Reden van de activiteit Status Fout** : niet van toepassing

### <a name="activity-type-change-password-self-service"></a>Activiteitstype: wachtwoord wijzigen (self-service)

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – Hiermee geeft u een gebruiker vrijwillig uitgevoerd of gedwongen (als gevolg van verlopen) wijzigen van wachtwoorden.
* **Activiteit Actor** -de gebruiker die hun wachtwoord gewijzigd. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die hun wachtwoord gewijzigd. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker het wachtwoord is gewijzigd
  * _Fout_ -geeft aan een gebruiker is mislukt om hun wachtwoord te wijzigen. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.
* **Reden van de activiteit Status Fout** - 
  * _FuzzyPolicyViolationInvalidPassword_ -de gebruiker een wachtwoord dat automatisch is verboden als gevolg van Microsoft zijn Geband wachtwoord detectiemogelijkheden vinden om te worden te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-reset-password-by-admin"></a>Activiteitstype: wachtwoord opnieuw instellen (door de beheerder)

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een beheerder een namens een gebruiker vanuit de Azure-portal voor wachtwoordherstel uitgevoerd.
* **Activiteit Actor** -beheerder het wachtwoord opnieuw instellen namens een andere gebruiker of beheerder uitgevoerd. Moet een globale beheerder, een wachtwoordbeheerder, een Gebruikersbeheerder of een beheerder van de helpdesk.
* **Doel van de activiteit** -de gebruiker waarvan het wachtwoord is opnieuw ingesteld. Mogelijk een eindgebruiker of een andere beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft een beheerder is opnieuw ingesteld wachtwoord van een gebruiker
  * _Fout_ -geeft een beheerder kan niet het wachtwoord van een gebruiker wijzigen. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.

### <a name="activity-type-reset-password-self-service"></a>Activiteitstype: wachtwoord opnieuw instellen (self-service)

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker hun wachtwoord van gereset de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* **Activiteit Actor** -de gebruiker die hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker met succes hun eigen wachtwoord opnieuw instellen
  * _Fout_ -aangeeft dat hun eigen wachtwoord opnieuw instellen van een gebruiker is mislukt. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.
* **Reden van de activiteit Status Fout** -
  * _FuzzyPolicyViolationInvalidPassword_ -admin geselecteerd een wachtwoord dat automatisch als gevolg van Microsoft zijn Geband wachtwoord detectiemogelijkheden vinden om te worden te veel voorkomt of vooral zwakke is verboden.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Activiteitstype: eigen wachtwoord opnieuw instellen van stroom activiteit uitgevoerd beheer

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het wachtwoord opnieuw instellen van proces aan.
* **Activiteit Actor** -stroom door de gebruiker die heeft uitgevoerd deel van het wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -stroom door de gebruiker die heeft uitgevoerd deel van het wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker een specifieke stap van de stroom van wachtwoord opnieuw instellen is voltooid.
  * _Fout_ -geeft aan een specifieke stap van het wachtwoord opnieuw instellen van stroom is mislukt. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.
* **Activiteit statusredenen toegestaan**
  * Zie onderstaande tabel voor [alle toegestaan activiteit opnieuw instellen van statusredenen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Activiteitstype: ontgrendelen gebruikersaccount (self-service)

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker de Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van het wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met behulp van het AD-account ontgrendelen zonder de functie.
* **Activiteit Actor** -de gebruiker die het account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die het account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker een eigen account is ontgrendeld
  * _Fout_ -geeft aan een gebruiker is mislukt om hun account te ontgrendelen. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Activiteitstype: gebruiker is geregistreerd voor selfservice voor wachtwoordherstel

De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker de vereiste informatie om te kunnen hun wachtwoord in overeenstemming met het beleid voor wachtwoordherstel momenteel opgegeven tenant is geregistreerd. 
* **Activiteit Actor** -de gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
  * _Geslaagde_ -geeft aan een gebruiker is geregistreerd voor wachtwoordherstel in overeenstemming met het huidige beleid. 
  * _Fout_ -geeft aan een gebruiker kan niet worden geregistreerd voor wachtwoordherstel. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden. Opmerking: dit betekent niet dat een gebruiker zich niet alleen hun eigen wachtwoord opnieuw instellen, dat ze niet het registratieproces is voltooid. Als er niet-geverifieerde gegevens op hun account juist (zoals een telefoonnummer die niet worden gevalideerd), ondanks dat ze dit telefoonnummer niet hebt gecontroleerd, software kan nog steeds worden gebruikt om hun wachtwoord te stellen. Zie voor meer informatie [wat er gebeurt wanneer een gebruiker registreert?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Volgende stappen

De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD

* [Snelkoppeling naar de gebruiker management controlelogboeken](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - Ga direct naar uw tenant Gebruikersbeheer controlelogboeken
* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens**](active-directory-passwords-data.md): informatie over de gegevens die nodig zijn en hoe deze worden gebruikt voor wachtwoordbeheer
* [**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie
* [**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.
* [**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? - Antwoorden op vragen die u altijd wilde stellen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
