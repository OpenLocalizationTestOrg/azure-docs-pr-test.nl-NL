---
title: 'Get Insights: Rapporten Azure AD-wachtwoordbeheer | Microsoft Docs'
description: Dit artikel wordt beschreven hoe u rapporten met inzicht verkrijgen in beheerbewerkingen wachtwoord in uw organisatie.
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: ae83df618e3c392fe89878bcd1be0d6c6cb1edb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-get-operational-insights-with-password-management-reports"></a>Rapporten operationeel inzicht verkrijgen met wachtwoordbeheer
> [!IMPORTANT]
> **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Deze sectie wordt beschreven hoe u Azure Active Directory-wachtwoord-rapporten kunt gebruiken om weer te geven hoe gebruikers gebruikt wachtwoord opnieuw instellen en wijzigen in uw organisatie.

* [**Overzicht van rapporten wachtwoord**](#overview-of-password-management-reports)
* [**Wachtwoord-rapporten weergeven in de nieuwe Azure portal**](#how-to-view-password-management-reports)
 * [Directory-functies mogen rapporten lezen](#directory-roles-allowed-to-read-reports)
* [**Selfservice wachtwoordbeheer activiteitstypen in de nieuwe Azure-Portal**](#self-service-password-management-activity-types)
 * [Geen toegang tot selfservice voor wachtwoordherstel](#activity-type-blocked-from-self-service-password-reset)
 * [Wachtwoord wijzigen (self-service)](#activity-type-change-password-self-service)
 * [Wachtwoord opnieuw instellen (door de beheerder)](#activity-type-reset-password-by-admin)
 * [Wachtwoord (self-service) opnieuw instellen](#activity-type-reset-password-self-service)
 * [Eigen beheer wachtwoordherstel stroom activiteit uitgevoerd](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Ontgrendelen van gebruikersaccount (self-service)](#activity-type-unlock-user-account-self-service)
 * [Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel](#activity-type-user-registered-for-self-service-password-reset)
* [**Het ophalen van gebeurtenissen voor wachtwoord van de Azure AD-rapporten en gebeurtenissen API**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Rapportage-API-beperkingen voor gegevens ophalen](#reporting-api-data-retrieval-limitations)
* [**Het downloaden van wachtwoord opnieuw instellen van inschrijving gebeurtenissen snel met PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Het wachtwoord-rapporten weergeven in de klassieke portal**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Registratie-activiteit in uw organisatie in de klassieke portal voor wachtwoordherstel weergeven**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Activiteit in uw organisatie in de klassieke portal voor wachtwoordherstel weergeven**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Overzicht van de wachtwoord-rapporten
Als u opnieuw instellen van wachtwoorden implementeert, is de meest voorkomende volgende stappen uit om te zien hoe deze wordt gebruikt in uw organisatie.  U wilt bijvoorbeeld inzicht te krijgen in hoe gebruikers zijn registreren voor wachtwoordherstel of hoeveel wachtwoord opnieuw instellen hebt uitgevoerd in de afgelopen paar dagen.  Hier volgen enkele van de algemene vragen die u kunnen beantwoorden met de wachtwoord-rapporten die zijn opgenomen in de [Azure Management Portal](https://manage.windowsazure.com) vandaag:

* Hoeveel mensen hebben geregistreerd voor het wachtwoord opnieuw instellen?
* Die is geregistreerd voor het wachtwoord opnieuw instellen?
* Welke gegevens registreert personen?
* Hoeveel mensen dat op het in de afgelopen 7 dagen hun wachtwoord opnieuw instellen?
* Wat zijn de meest voorkomende methoden gebruikers of beheerders gebruiken hun wachtwoorden opnieuw kunnen instellen?
* Wat zijn veelvoorkomende problemen met gebruikers of beheerders face bij een poging tot het gebruik van wachtwoord opnieuw instellen?
* Wat beheerders zijn opnieuw instellen van hun eigen wachtwoorden vaak?
* Is er een verdachte activiteit gebeurt met wachtwoord opnieuw instellen?

## <a name="how-to-view-password-management-reports"></a>Het wachtwoord-rapporten weergeven
In het nieuwe [Azure Portal](https://portal.azure.com) ervaring hebben we een betere manier om weer te geven voor wachtwoordherstel en registratie-activiteit wachtwoord opnieuw instellen.  Volg onderstaande stappen voor het vinden van het wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van gebeurtenissen in het nieuwe [Azure Portal](https://portal.azure.com):

1. Navigeer naar [ **portal.azure.com**](https://portal.azure.com)
2. Klik op de **meer services** menu op de belangrijkste navigatie aan de linkerkant Azure Portal
3. Zoeken naar **Azure Active Directory** in de lijst met services en dit selecteren
4. Klik op **gebruikers en groepen** uit het navigatiemenu Azure Active Directory
5. Klik op de **controlelogboeken** navigatie-item van het navigatiemenu gebruikers en groepen. Hier ziet u alle van de audit gebeurtenissen die zich kunnen voordoen met alle gebruikers in uw directory. U kunt deze weergeven voor een overzicht van alle de wachtwoord-gerelateerde gebeurtenissen ook filteren.
6. Als u wilt filteren deze weergave zodanig dat alleen de wachtwoordbeheer gebeurtenissen gerelateerde, klikt u op de **Filter** knop aan de bovenkant van de blade.
7. Van de **Filter** selecteert u de **categorie** vervolgkeuzelijst en wijzig dit in de **Self-service wachtwoordbeheer** categorietype.
8. Eventueel verdere filter de lijst door het kiezen van de specifieke **activiteit** u geïnteresseerd bent
### <a name="direct-link-to-user-audit-blade"></a>Directe koppeling naar de gebruiker Audit-blade
Als u bent aangemeld bij uw portal, is hier een directe koppeling naar de gebruiker audit-blade waar u deze gebeurtenissen kunt zien:

* [Ga naar de gebruiker audit Beheerweergave rechtstreeks](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-to-read-reports"></a>Directory-functies mogen rapporten lezen
De volgende rollen in de directory kunnen op dit moment lezen van Azure AD-wachtwoordbeheer rapporten in de klassieke Azure-portal:

* Globale beheerder

Om te kunnen lezen van deze rapporten, een globale beheerder in het bedrijf moet hebt gekozen aan voor deze gegevens worden opgehaald voor de hele organisatie door naar het tabblad rapportage of controlelogboeken ten minste één keer te gaan. Pas als u dit doet, worden geen gegevens verzameld voor uw organisatie.

Voor meer informatie over de functies van de directory en wat ze kunnen doen, Zie [beheerdersrollen toewijzen in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Wachtwoordbeheer activiteitstypen selfservice
De volgende activiteitstypen worden weergegeven in de **Self-Service wachtwoordbeheer** audit gebeurteniscategorie.  Hier volgt een beschrijving op voor elk van deze.

* [**Selfservice voor wachtwoordherstel geblokkeerd** ](#activity-type-blocked-from-self-service-password-reset) -geeft aan een gebruiker heeft geprobeerd een wachtwoord opnieuw instellen, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* [**Wachtwoord (self-service) wijzigen** ](#activity-type-change-password-self-service) -geeft aan een gebruiker een vrijwillige uitgevoerd of gedwongen (als gevolg van verlopen) wijzigen van wachtwoorden.
* [**Wachtwoord opnieuw instellen (door admin)** ](#activity-type-reset-password-by-admin) -geeft aan dat een beheerder een namens een gebruiker vanuit de Azure Portal voor wachtwoordherstel uitgevoerd.
* [**Wachtwoord opnieuw instellen (self-service)** ](#activity-type-reset-password-self-service) -geeft aan een gebruiker gereset zijn of haar wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* [**Eigen beheer wachtwoordherstel stroom activiteit uitgevoerd** ](#activity-type-self-serve-password-reset-flow-activity-progress) -geeft aan elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het wachtwoord opnieuw instellen van proces.
* [**Ontgrendelen van gebruikersaccount (self-service)** ](#activity-type-unlock-user-account-self-service) -geeft aan een gebruiker zijn of haar Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van zijn of haar wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met de [AD-account ontgrendelen zonder reset](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) functie.
* [**Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel** ](#activity-type-user-registered-for-self-service-password-reset) -geeft aan een gebruiker is geregistreerd de vereiste informatie om te kunnen stellen zijn of haar wachtwoord in overeenstemming met het wachtwoord van de tenant momenteel opgegeven beleid opnieuw instellen.

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
* **Activiteit Actor** -de gebruiker die gewijzigd zijn of haar wachtwoord. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die gewijzigd zijn of haar wachtwoord. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker zijn of haar wachtwoord is gewijzigd
 * _Fout_ -aangeeft dat een gebruiker zijn of haar wachtwoord te wijzigen is mislukt. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.
* **Reden van de activiteit Status Fout** -
 * _FuzzyPolicyViolationInvalidPassword_ -de gebruiker een wachtwoord op dat automatisch is verboden als gevolg van Microsoft zijn Geband wachtwoord detectiemogelijkheden vinden om te worden te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-reset-password-by-admin"></a>Activiteitstype: wachtwoord opnieuw instellen (door de beheerder)
De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een beheerder een namens een gebruiker vanuit de Azure Portal voor wachtwoordherstel uitgevoerd.
* **Activiteit Actor** -beheerder het wachtwoord opnieuw instellen namens een andere eindgebruiker of beheerder uitgevoerd. Moet een globale beheerder, een wachtwoordbeheerder, een Gebruikersbeheerder of een beheerder van de helpdesk.
* **Doel van de activiteit** -de gebruiker waarvan het wachtwoord is opnieuw ingesteld. Mogelijk een eindgebruiker of een andere beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft een beheerder is opnieuw ingesteld wachtwoord van een gebruiker
 * _Fout_ -geeft een beheerder kan niet het wachtwoord van een gebruiker wijzigen. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.

### <a name="activity-type-reset-password-self-service"></a>Activiteitstype: wachtwoord opnieuw instellen (self-service)
De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker zijn of haar wachtwoord van gereset de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* **Activiteit Actor** -de gebruiker die zijn of haar wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die zijn of haar wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker met succes zijn of haar eigen wachtwoord opnieuw instellen
 * _Fout_ -aangeeft dat een gebruiker zijn of haar eigen wachtwoord opnieuw instellen is mislukt. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.
* **Reden van de activiteit Status Fout** -
 * _FuzzyPolicyViolationInvalidPassword_ -admin geselecteerd een wachtwoord op dat automatisch als gevolg van Microsoft zijn Geband wachtwoord detectiemogelijkheden vinden om te worden te veel voorkomt of vooral zwakke is verboden.

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

* **Beschrijving van de activiteit** – geeft aan dat een gebruiker zijn of haar Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van zijn of haar wachtwoord van de [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met behulp van de [AD-account ontgrendelen zonder reset](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) functie.
* **Activiteit Actor** -de gebruiker die zijn of haar account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die zijn of haar account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker zijn of haar eigen account is ontgrendeld
 * _Fout_ -geeft aan een gebruiker is mislukt om zijn of haar account te ontgrendelen. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Activiteitstype: gebruiker is geregistreerd voor selfservice voor wachtwoordherstel
De volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** : geeft aan dat een gebruiker is geregistreerd de vereiste informatie om te kunnen stellen zijn of haar wachtwoord in overeenstemming met het wachtwoord van de tenant momenteel opgegeven beleid herstellen.
* **Activiteit Actor** -de gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -de gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker is geregistreerd voor wachtwoordherstel in overeenstemming met het huidige beleid.
 * _Fout_ -geeft aan een gebruiker kan niet worden geregistreerd voor wachtwoordherstel. Op de rij te klikken, kunt u zien de **activiteit statusreden** categorie voor meer informatie over waarom de fout is opgetreden. Opmerking: dit betekent niet dat een gebruiker kan niet opnieuw in te stellen zijn of haar eigen wachtwoord alleen die hij of zij het registratieproces is niet voltooid. Als er niet-geverifieerde gegevens op hun account juist (zoals een telefoonnummer die niet worden gevalideerd), ondanks dat ze dit telefoonnummer niet hebt gecontroleerd, software kan nog steeds worden gebruikt om hun wachtwoord te stellen. Zie voor meer informatie [wat er gebeurt wanneer een gebruiker registreert?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Het ophalen van gebeurtenissen voor wachtwoord van de Azure AD-rapporten en gebeurtenissen API
Vanaf augustus 2015 geldt de Azure AD-rapporten en gebeurtenissen API biedt nu ondersteuning bij het ophalen van alle gegevens die zijn opgenomen in het wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van rapporten. U kunt afzonderlijke wachtwoordherstel downloaden en gebeurtenissen voor de integratie met de reporting-technologie van uw choce registratie voor wachtwoord opnieuw instellen met behulp van deze API.

### <a name="how-to-get-started-with-the-reporting-api"></a>Hoe u aan de slag met de rapportage-API
Toegang tot deze gegevens, moet u een kleine app of het script voor het ophalen van onze servers worden geschreven. [Meer informatie over het aan de slag met de Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

Zodra u een werkende script hebt, wilt u naast de wachtwoord opnieuw instellen en registratie gebeurtenissen onderzoeken die u ophalen kunt om te voldoen aan uw scenario's.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): geeft een lijst van de beschikbare kolommen voor wachtwoord opnieuw instellen van gebeurtenissen
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): geeft een lijst van de beschikbare kolommen voor gebeurtenissen van de registratie voor wachtwoord opnieuw instellen

### <a name="reporting-api-data-retrieval-limitations"></a>Rapportage-API-beperkingen voor gegevens ophalen
Op dit moment wordt de Azure AD-rapporten en gebeurtenissen API haalt maximaal **75.000 afzonderlijke gebeurtenissen** van de [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) en [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typen, spanning de **afgelopen 30 dagen**.

Als u wilt ophalen of gegevens buiten dit venster opslaan, het is raadzaam het persistent maken in een externe database en de API gebruiken om op te vragen van de delta's die het resultaat. Er is een best practice om te beginnen bij het ophalen van deze gegevens bij het starten van uw wachtwoord opnieuw instellen van het registratieproces in uw organisatie, extern behouden en ga vervolgens door met het bijhouden van de delta's vanaf dit punt.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Het downloaden van wachtwoord opnieuw instellen van inschrijving gebeurtenissen snel met PowerShell
Naast het rechtstreeks gebruik van de Azure AD-rapporten en gebeurtenissen API, u kunt ook de onderstaande PowerShell-script voor een recente registratie gebeurtenissen in uw directory. Dit is handig als u zien wie onlangs is geregistreerd of wilt ervoor te zorgen wilt dat uw wachtwoord opnieuw instellen van implementatie plaatsvindt zoals verwacht.

* [Azure AD SSPR-registratie activiteit PowerShell-Script](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-to-view-password-management-reports-in-the-classic-portal"></a>Het wachtwoord-rapporten weergeven in de klassieke portal
Ga voor de wachtwoord-rapporten de volgende stappen uit te voeren:

1. Klik op de **Active Directory** extensie in de [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer uw directory in de lijst die wordt weergegeven in de portal.
3. Klik op de **rapporten** tabblad.
4. Zoek in de **activiteitenlogboeken** sectie.
5. Selecteer de **activiteit wachtwoord opnieuw instellen** rapport of de **registratie activiteit voor wachtwoordherstel** rapport.

## <a name="view-password-reset-registration-activity-in-the-classic-portal"></a>Registratie-activiteit in de klassieke portal voor wachtwoordherstel weergeven
Wachtwoord opnieuw instellen van inschrijving activiteit dit rapport bevat dat alle wachtwoordherstel registraties die hebben plaatsgevonden in uw organisatie.  De registratie van een wachtwoord opnieuw instellen in dit rapport wordt weergegeven voor elke gebruiker die zich heeft geregistreerd. verificatie-informatie op het wachtwoord opnieuw instellen van registratieportal ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns"></a>Beschrijving van de kolommen
De volgende lijst wordt elk van de rapportkolommen in detail uitgelegd:

* **Gebruiker** – de gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen van bewerking voor de registratie.
* **Rol** : de rol van de gebruiker in de directory.
* **Datum en tijd** – de datum en tijd van de poging.
* **Geregistreerde gegevens** : registratie van welke verificatiegegevens die de gebruiker tijdens het wachtwoord opgegeven opnieuw instellen.

### <a name="description-of-report-values"></a>Beschrijving van rapport waarden
De volgende tabel beschrijft de verschillende waarden voor elke kolom toegestaan:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Gegevens die zijn geregistreerd |**Alternatief e-mailadres** – gebruiker alternatieve e-mailadres of verificatie e-mailadres gebruikt om te verifiëren<p><p>**Telefoon (werk)**– telefoon (werk) gebruiker gebruikt om te verifiëren<p>**Mobiele telefoon** -gebruiker gebruikt mobiele telefoon of telefoon voor authenticatie om te verifiëren<p>**Beveiligingsvragen** – gebruiker beveiligingsvragen gebruikt om te verifiëren<p>**Een combinatie van de bovenstaande (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven, ziet u welke twee methoden voor de gebruiker gebruikt voor verificatie aanvraag zijn/haar wachtwoord opnieuw instellen. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Activiteit in de klassieke portal voor wachtwoordherstel weergeven
Dit rapport geeft dat alle pogingen die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel.

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns"></a>Beschrijving van de kolommen
De volgende lijst wordt elk van de rapportkolommen in detail uitgelegd:

1. **Gebruiker** – de gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen voor bewerking (op basis van het veld User ID is opgegeven bij de gebruiker een wachtwoord opnieuw instellen).
2. **Rol** : de rol van de gebruiker in de directory.
3. **Datum en tijd** – de datum en tijd van de poging.
4. **Methode(n) gebruikt** – welke verificatiemethoden die de gebruiker voor deze gebruikt bewerking opnieuw.
5. **Resultaat** – het eindresultaat van het wachtwoord opnieuw instellen.
6. **Details** : meer informatie over waarom het wachtwoord opnieuw instellen in de waarde die het heeft geleid.  Tevens alle stappen die u nemen kunt voor het oplossen van een onverwachte fout.

### <a name="description-of-report-values"></a>Beschrijving van rapport waarden
De volgende tabel beschrijft de verschillende waarden voor elke kolom toegestaan:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Methoden die worden gebruikt |**Alternatief e-mailadres** – gebruiker alternatieve e-mailadres of verificatie e-mailadres gebruikt om te verifiëren<p>**Telefoon (werk)** – telefoon (werk) gebruiker gebruikt om te verifiëren<p>**Mobiele telefoon** – gebruiker gebruikt mobiele telefoon of telefoon voor authenticatie om te verifiëren<p>**Beveiligingsvragen** – gebruiker beveiligingsvragen gebruikt om te verifiëren<p>**Een combinatie van de bovenstaande (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven, ziet u welke twee methoden voor de gebruiker gebruikt voor verificatie aanvraag zijn/haar wachtwoord opnieuw instellen. |
| Resultaat |**Afgebroken** – gebruiker opnieuw instellen van wachtwoorden is gestart maar wordt gestopt halverwege via zonder te voltooien<p>**Geblokkeerd** : gebruikersaccount is geblokkeerd voor het gebruik van wachtwoord opnieuw instellen als gevolg van probeert te gebruiken van de wachtwoordpagina opnieuw instellen of een enkel wachtwoord opnieuw instellen in gate te vaak een periode van 24 uur<p>**Geannuleerd** – wachtwoord opnieuw instellen is gestart, maar vervolgens geklikt op de knop Annuleren als u wilt annuleren van de sessie gedeeltelijk manier tot en met de gebruiker <p>**Verbinding gemaakt met de beheerder** – gebruiker heeft een probleem opgetreden tijdens de sessie die hij kan niet worden omgezet, zodat de gebruiker heeft geklikt voor de koppeling 'Contact op met uw beheerder' in plaats van het voltooien van het wachtwoord opnieuw instellen stroom<p>**Kan geen** – gebruiker kon niet opnieuw instellen van een wachtwoord, waarschijnlijk omdat de gebruiker niet is geconfigureerd voor het gebruik van de functie (bv. Er is geen licentie, ontbrekende informatie voor verificatie, wachtwoord beheerd on-premises, maar Write-back is uitgeschakeld).<p>**Geslaagd** – wachtwoordherstel is geslaagd. |
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
| De gebruiker geannuleerd voordat deze de vereiste verificatiemethoden |Geannuleerd |
| De gebruiker geannuleerd voor het verzenden van een nieuw wachtwoord |Geannuleerd |
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

## <a name="next-steps"></a>Volgende stappen
Hieronder vindt u koppelingen naar alle Azure AD-documentatiepagina’s over wachtwoordherstel:

* **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Hoe werkt het?**](active-directory-passwords-how-it-works.md): meer informatie over de zes verschillende onderdelen van de service en wat elke service biedt
* [**Aan de slag** ](active-directory-passwords-getting-started.md) -informatie over het kunt u gebruikers wilt herstellen en hun cloud of on-premises wachtwoorden wijzigen
* [**Aanpassen**](active-directory-passwords-customize.md): informatie over het aanpassen van de weergave en het gedrag van de service om aan de behoeften van uw organisatie te voldoen
* [**Aanbevolen procedures**](active-directory-passwords-best-practices.md): informatie over het snel implementeren en effectief beheren van wachtwoorden in uw organisatie
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): verkrijg antwoord op veelgestelde vragen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het snel oplossen van problemen met de service
* [**Meer informatie**](active-directory-passwords-learn-more.md): meer informatie over de technische details van de werking van de service
