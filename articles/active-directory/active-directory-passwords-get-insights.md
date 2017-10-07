---
title: 'Get Insights: Rapporten Azure AD-wachtwoordbeheer | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toouse rapporteert tooget inzicht in de beheerbewerkingen wachtwoord in uw organisatie.
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
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Hoe tooget operationeel inzicht met wachtwoordbeheer rapporten
> [!IMPORTANT]
> **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Deze sectie wordt beschreven hoe u kunt Azure Active Directory-wachtwoordbeheer rapporten tooview hoe gebruikers gebruikt wachtwoord opnieuw instellen en wijzigen in uw organisatie.

* [**Overzicht van rapporten wachtwoord**](#overview-of-password-management-reports)
* [**Hoe tooview wachtwoordbeheer rapporten in de nieuwe Azure portal Hallo**](#how-to-view-password-management-reports)
 * [Directory-functies tooread rapporten toegestaan](#directory-roles-allowed-to-read-reports)
* [**Selfservice wachtwoordbeheer activiteitstypen in Hallo nieuwe Azure-Portal**](#self-service-password-management-activity-types)
 * [Geen toegang tot selfservice voor wachtwoordherstel](#activity-type-blocked-from-self-service-password-reset)
 * [Wachtwoord wijzigen (self-service)](#activity-type-change-password-self-service)
 * [Wachtwoord opnieuw instellen (door de beheerder)](#activity-type-reset-password-by-admin)
 * [Wachtwoord (self-service) opnieuw instellen](#activity-type-reset-password-self-service)
 * [Eigen beheer wachtwoordherstel stroom activiteit uitgevoerd](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Ontgrendelen van gebruikersaccount (self-service)](#activity-type-unlock-user-account-self-service)
 * [Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel](#activity-type-user-registered-for-self-service-password-reset)
* [**Hoe tooretrieve wachtwoord management gebeurtenissen van Azure AD-rapporten en gebeurtenissen API Hallo**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Rapportage-API-beperkingen voor gegevens ophalen](#reporting-api-data-retrieval-limitations)
* [**Hoe toodownload wachtwoordherstel registratie gebeurtenissen snel met PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Hoe tooview wachtwoordbeheer rapporten in de klassieke portal Hallo**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Registratie van activiteit in uw organisatie in de klassieke portal Hallo weergave wachtwoord opnieuw instellen**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**De activiteit in uw organisatie in de klassieke portal Hallo weergave wachtwoord opnieuw instellen**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Overzicht van de wachtwoord-rapporten
Nadat u opnieuw instellen van wachtwoorden implementeert, is een van de meest voorkomende Vervolgstappen Hallo toosee hoe deze wordt gebruikt in uw organisatie.  Bijvoorbeeld, kunt u tooget inzicht in hoe gebruikers zijn registreren voor wachtwoordherstel of hoeveel wachtwoord opnieuw instellen in de afgelopen paar dagen Hallo zijn doorlopen.  Hier volgen enkele Hallo Veelgestelde vragen die u kunt tooanswer met Hallo wachtwoord-rapporten die zijn opgenomen in Hallo [Azure Management Portal](https://manage.windowsazure.com) vandaag:

* Hoeveel mensen hebben geregistreerd voor het wachtwoord opnieuw instellen?
* Die is geregistreerd voor het wachtwoord opnieuw instellen?
* Welke gegevens registreert personen?
* Hoeveel mensen hun wachtwoord opnieuw instellen in Hallo afgelopen 7 dagen?
* Wat zijn de meest voorkomende methoden gebruikers Hallo of beheerders hun wachtwoorden tooreset gebruiken?
* Wat zijn veelvoorkomende problemen met gebruikers of beheerders face tijdens een poging de toouse wachtwoord opnieuw instellen?
* Wat beheerders zijn opnieuw instellen van hun eigen wachtwoorden vaak?
* Is er een verdachte activiteit gebeurt met wachtwoord opnieuw instellen?

## <a name="how-tooview-password-management-reports"></a>Hoe tooview wachtwoordbeheer rapporten
In de nieuwe Hallo [Azure Portal](https://portal.azure.com) ondervindt, we hebben een betere manier tooview wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van inschrijving activiteit.  Hallo stappen hieronder toofind Hallo wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van gebeurtenissen in de nieuwe Hallo [Azure Portal](https://portal.azure.com):

1. Navigeer te[**portal.azure.com**](https://portal.azure.com)
2. Klik op Hallo **meer services** menu op Hallo belangrijkste Azure-Portal linkerkant navigatie
3. Zoeken naar **Azure Active Directory** in de lijst met services Hallo en selecteert u het
4. Klik op **gebruikers en groepen** van hello Azure Active Directory-navigatiemenu
5. Klik op Hallo **controlelogboeken** navigatie-item van navigatiemenu Hallo gebruikers en groepen. Hier ziet u alle Hallo audit gebeurtenissen die zich kunnen voordoen tegen alle Hallo gebruikers in uw directory. U kunt deze toosee weergave alle Hallo wachtwoord-gerelateerde gebeurtenissen, evenals filteren.
6. toofilter deze wachtwoordbeheer weergave tooonly Hallo gerelateerde gebeurtenissen, klikt u op Hallo **Filter** knop Hallo boven aan het Hallo-blade.
7. Van Hallo **Filter** menu, selecteer Hallo **categorie** vervolgkeuzelijst en wijzig deze toohello **Self-service wachtwoordbeheer** categorietype.
8. Eventueel verdere Hallo-filterlijst door te kiezen Hallo specifieke **activiteit** u geïnteresseerd bent
### <a name="direct-link-toouser-audit-blade"></a>Directe koppeling tooUser Audit-blade
Als u tooyour portal bent aangemeld, is hier een directe koppeling toohello gebruiker audit blade waar u deze gebeurtenissen kunt zien:

* [Ga toouser management weergave rechtstreeks controleren](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Directory-functies tooread rapporten toegestaan
Op dit moment kunnen hello volgende directory rollen lezen Azure AD-wachtwoordbeheer rapporten in de klassieke Azure portal Hallo:

* Globale beheerder

Voordat deze kunnen tooread deze rapporten, een globale beheerder in bedrijf Hallo moet hebt gekozen aan voor deze gegevens toobe namens Hallo organisatie via Hallo tabblad of audit logboeken ten minste eenmaal reporting opgehaald. Pas als u dit doet, worden geen gegevens verzameld voor uw organisatie.

meer informatie over de functies van de directory en kunnen ze zien tooread [beheerdersrollen toewijzen in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Wachtwoordbeheer activiteitstypen selfservice
Hallo volgende activiteitstypen worden weergegeven in Hallo **Self-Service wachtwoordbeheer** audit gebeurteniscategorie.  Hier volgt een beschrijving op voor elk van deze.

* [**Selfservice voor wachtwoordherstel geblokkeerd** ](#activity-type-blocked-from-self-service-password-reset) -geeft aan een gebruiker heeft geprobeerd een tooreset een wachtwoord, een specifieke poort gebruiken of een telefoonnummer valideren meer dan 5 totale aantal keren in 24 uur.
* [**Wachtwoord (self-service) wijzigen** ](#activity-type-change-password-self-service) -geeft aan een gebruiker een vrijwillige uitgevoerd of gedwongen (vanwege tooexpiry) wijzigen van wachtwoorden.
* [**Wachtwoord opnieuw instellen (door admin)** ](#activity-type-reset-password-by-admin) -geeft aan dat een beheerder een namens een gebruiker uit hello Azure-Portal voor wachtwoordherstel uitgevoerd.
* [**Wachtwoord opnieuw instellen (self-service)** ](#activity-type-reset-password-self-service) -geeft aan een gebruiker gereset zijn of haar wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* [**Eigen beheer wachtwoordherstel stroom activiteit uitgevoerd** ](#activity-type-self-serve-password-reset-flow-activity-progress) -geeft aan elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het Hallo-wachtwoord opnieuw instellen van proces.
* [**Ontgrendelen van gebruikersaccount (self-service)** ](#activity-type-unlock-user-account-self-service) -geeft aan een gebruiker zijn of haar Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van zijn of haar wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met behulp van Hallo [AD-account ontgrendelen zonder reset](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) functie.
* [**Gebruiker is geregistreerd voor selfservice voor wachtwoordherstel** ](#activity-type-user-registered-for-self-service-password-reset) -geeft aan een gebruiker is geregistreerd alle Hallo vereist informatie toobe kunnen tooreset zijn of haar wachtwoord in overeenstemming met beleid voor wachtwoordherstel voor Hallo tenant momenteel opgegeven.

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
* **Activiteit Actor** -Hallo-gebruiker die gewijzigd zijn of haar wachtwoord. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die gewijzigd zijn of haar wachtwoord. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker zijn of haar wachtwoord is gewijzigd
 * _Fout_ -geeft aan een gebruiker is mislukt toochange zijn of haar wachtwoord. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Reden van de activiteit Status Fout** -
 * _FuzzyPolicyViolationInvalidPassword_ -Hallo gebruiker een wachtwoord op dat automatisch is verboden vervaldatum van tooMicrosoft verboden wachtwoord detectiemogelijkheden vinden toobe te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-reset-password-by-admin"></a>Activiteitstype: wachtwoord opnieuw instellen (door de beheerder)
Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan dat een beheerder een namens een gebruiker uit hello Azure-Portal voor wachtwoordherstel uitgevoerd.
* **Activiteit Actor** -Hallo beheerder Hallo wachtwoordherstel namens een andere eindgebruiker of beheerder uitgevoerd. Moet een globale beheerder, een wachtwoordbeheerder, een Gebruikersbeheerder of een beheerder van de helpdesk.
* **Doel van de activiteit** -Hallo gebruiker waarvan het wachtwoord is opnieuw ingesteld. Mogelijk een eindgebruiker of een andere beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft een beheerder is opnieuw ingesteld wachtwoord van een gebruiker
 * _Fout_ -aangeeft dat een beheerder is mislukt toochange wachtwoord van een gebruiker. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.

### <a name="activity-type-reset-password-self-service"></a>Activiteitstype: wachtwoord opnieuw instellen (self-service)
Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker gereset zijn of haar wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com).
* **Activiteit Actor** -Hallo-gebruiker die zijn of haar wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die zijn of haar wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker met succes zijn of haar eigen wachtwoord opnieuw instellen
 * _Fout_ -geeft aan een gebruiker is mislukt tooreset zijn of haar eigen wachtwoord. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Reden van de activiteit Status Fout** -
 * _FuzzyPolicyViolationInvalidPassword_ -Hallo beheerder een wachtwoord op dat automatisch is verboden vervaldatum van tooMicrosoft verboden wachtwoord detectiemogelijkheden vinden toobe te veel voorkomt of vooral zwakke geselecteerd.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Activiteitstype: eigen wachtwoord opnieuw instellen van stroom activiteit uitgevoerd beheer
Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft elke specifieke stap van een gebruiker doorlopen (zoals het doorgeven van een specifiek wachtwoord opnieuw instellen van verificatiepoort) als onderdeel van het Hallo-wachtwoord opnieuw instellen van proces aan.
* **Activiteit Actor** -Hallo-gebruiker die heeft uitgevoerd deel uit van het Hallo-wachtwoord opnieuw instellen van stroom. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die heeft uitgevoerd deel uit van het Hallo-wachtwoord opnieuw instellen van stroom. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker een specifieke stap van de stroom van Hallo wachtwoord opnieuw instellen is voltooid.
 * _Fout_ -geeft aan een specifieke stap Hallo wachtwoord opnieuw instellen van stroom is mislukt. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.
* **Activiteit statusredenen toegestaan**
 * Zie onderstaande tabel voor [alle toegestaan activiteit opnieuw instellen van statusredenen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Activiteitstype: ontgrendelen gebruikersaccount (self-service)
Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker zijn of haar Active Directory-account is ontgrendeld zonder de fabrieksinstellingen van zijn of haar wachtwoord uit Hallo [Portal Azure AD-wachtwoord opnieuw instellen](https://passwordreset.microsoftonline.com) met Hallo [AD account ontgrendelen zonder reset](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) functie.
* **Activiteit Actor** -Hallo-gebruiker die zijn of haar account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die zijn of haar account ontgrendeld zonder hun wachtwoord opnieuw instellen. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker zijn of haar eigen account is ontgrendeld
 * _Fout_ -geeft aan een gebruiker is mislukt toounlock zijn of haar account. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Activiteitstype: gebruiker is geregistreerd voor selfservice voor wachtwoordherstel
Hallo volgende lijst wordt deze activiteit in detail uitgelegd:

* **Beschrijving van de activiteit** – geeft aan een gebruiker is geregistreerd alle Hallo vereist informatie toobe kunnen tooreset zijn of haar wachtwoord in overeenstemming met beleid voor wachtwoordherstel voor Hallo tenant momenteel opgegeven.
* **Activiteit Actor** -Hallo-gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Doel van de activiteit** -Hallo-gebruiker die zich hebben geregistreerd voor wachtwoordherstel. Mogelijk een eindgebruiker of een beheerder.
* **Toegestane activiteit statussen**
 * _Geslaagde_ -geeft aan een gebruiker is geregistreerd voor wachtwoordherstel in overeenstemming met het huidige beleid Hallo.
 * _Fout_ -geeft aan een gebruiker is mislukt-tooregister voor wachtwoordherstel. Op Hallo rij te klikken kunt u toosee hello **activiteit statusreden** categorie toolearn meer informatie over waarom Hallo is een fout opgetreden. Opmerking: dit betekent niet dat een gebruiker is niet mogelijk tooreset zijn of haar eigen alleen dat hij of zij is niet voltooid Hallo registratieproces wachtwoord. Als er niet-geverifieerde gegevens op hun account juist (zoals een telefoonnummer die niet worden gevalideerd), zelfs als ze dit telefoonnummer niet hebt gecontroleerd, ze kunnen nog steeds gebruiken deze tooreset hun wachtwoord. Zie voor meer informatie [wat er gebeurt wanneer een gebruiker registreert?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Hoe tooretrieve wachtwoord management gebeurtenissen van Azure AD-rapporten en gebeurtenissen API Hallo
Vanaf augustus 2015 geldt hello Azure AD-rapporten en gebeurtenissen API biedt nu ondersteuning bij het ophalen van alle Hallo informatie is opgenomen in Hallo wachtwoord opnieuw instellen en het wachtwoord opnieuw instellen van registratie van rapporten. U kunt afzonderlijke wachtwoordherstel downloaden met behulp van deze API en wachtwoord opnieuw instellen van registratie van gebeurtenissen voor integratie met Hallo technologie van uw choce reporting.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Hoe tooget gestart Hello rapportage-API
tooaccess deze gegevens, u moet een kleine app toowrite of script tooretrieve op onze servers. [Meer informatie over hoe tooget gestart Hello Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

Zodra u een werkscript hebt, moet u naast tooexamine Hallo wachtwoord opnieuw instellen en registratie van gebeurtenissen, dat u toomeet uw scenario's ophalen kunt.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): geeft een lijst van beschikbare Hallo kolommen voor wachtwoord opnieuw instellen van gebeurtenissen
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): geeft een lijst van beschikbare Hallo kolommen voor gebeurtenissen van de registratie voor wachtwoord opnieuw instellen

### <a name="reporting-api-data-retrieval-limitations"></a>Rapportage-API-beperkingen voor gegevens ophalen
Op dit moment hello Azure AD-rapporten en gebeurtenissen API haalt te**75.000 afzonderlijke gebeurtenissen** Hallo [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) en [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typen , Hallo spanning **afgelopen 30 dagen**.

Als u tooretrieve moet of gegevens buiten dit venster opslaan, het is raadzaam het persistent maken in een externe database en het gebruik van Hallo API tooquery Hallo delta's die het resultaat. Er is een best practice toobegin bij het ophalen van deze gegevens bij het starten van uw wachtwoord opnieuw instellen van het registratieproces in uw organisatie, extern behouden en volg tootrack Hallo delta's vanaf dit punt doorsturen.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Hoe toodownload wachtwoordherstel registratie gebeurtenissen snel met PowerShell
Bovendien toousing Azure AD-rapporten en gebeurtenissen API rechtstreeks Hallo, u kunt ook Hallo onderstaande PowerShell-script toorecent registratie gebeurtenissen in uw directory. Dit is handig als u wilt dat toosee die onlangs is geregistreerd of u wilt dat uw wachtwoord opnieuw instellen van implementatie tooensure optreedt zoals verwacht.

* [Azure AD SSPR-registratie activiteit PowerShell-Script](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Hoe tooview wachtwoordbeheer rapporten in de klassieke portal Hallo
toofind hello wachtwoord-rapporten stappen Hallo volgende:

1. Klik op Hallo **Active Directory** de extensie in de Hallo [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer uw directory in Hallo lijst die wordt weergegeven in het Hallo-portal.
3. Klik op Hallo **rapporten** tabblad.
4. Zoek in Hallo **activiteitenlogboeken** sectie.
5. Selecteer beide Hallo **activiteit voor wachtwoordherstel** rapport of Hallo **registratie activiteit wachtwoord opnieuw instellen** rapport.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Registratie van activiteit in de klassieke portal Hallo weergave wachtwoord opnieuw instellen
Hallo wachtwoord opnieuw instellen van inschrijving activiteitenrapport geeft dat alle wachtwoordherstel registraties die hebben plaatsgevonden in uw organisatie.  De registratie van een wachtwoord opnieuw instellen in dit rapport wordt weergegeven voor elke gebruiker die zich heeft geregistreerd. verificatiegegevens op Hallo wachtwoord opnieuw instellen van registratieportal ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns"></a>Beschrijving van de kolommen
Hallo volgt een lijst met elk van de Hallo rapportkolommen in detail:

* **Gebruiker** – Hallo-gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen van bewerking voor de registratie.
* **Rol** – Hallo-rol van Hallo Hallo-directory-gebruiker.
* **Datum en tijd** – Hallo-datum en tijd van de Hallo poging.
* **Geregistreerde gegevens** : registratie van welke verificatie gegevens Hallo gebruiker is opgegeven tijdens het wachtwoord opnieuw instellen.

### <a name="description-of-report-values"></a>Beschrijving van rapport waarden
Hallo staan volgende tabel verschillende Hallo-waarden toegestaan voor elke kolom:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Gegevens die zijn geregistreerd |**Alternatief e-mailadres** – gebruiker gebruikt alternatieve e-mailadres of verificatie e tooauthenticate<p><p>**Telefoon (werk)**– gebruiker gebruikt office phone tooauthenticate<p>**Mobiele telefoon** -gebruiker mobiele telefoon of verificatie phone tooauthenticate gebruikt<p>**Beveiligingsvragen** – gebruikt gebruikersbeveiliging tooauthenticate vragen<p>**Een combinatie van Hallo hierboven (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven en ziet u welke twee methoden Hallo gebruiker gebruikt tooauthentication verzoek voor zijn/haar wachtwoord opnieuw instellen. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>De activiteit in de klassieke portal Hallo weergave wachtwoord opnieuw instellen
Dit rapport geeft dat alle pogingen die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel.

* **Tijdsbereik Max**: 30 dagen
* **Maximumaantal rijen**: 75.000
* **Downloadbare**: Ja, via de CSV-bestand

### <a name="description-of-report-columns"></a>Beschrijving van de kolommen
Hallo volgt een lijst met elk van de Hallo rapportkolommen in detail:

1. **Gebruiker** – Hallo-gebruiker die heeft geprobeerd een wachtwoord opnieuw instellen voor bewerking (op basis van veld Hallo-gebruikers-ID als Hallo gebruiker afkomstig tooreset een wachtwoord is opgegeven).
2. **Rol** – Hallo-rol van Hallo Hallo-directory-gebruiker.
3. **Datum en tijd** – Hallo-datum en tijd van de Hallo poging.
4. **Methode(n) gebruikt** – welke verificatiemethoden Hallo gebruiker gebruikt voor deze bewerking opnieuw instellen.
5. **Resultaat** – Hallo eindresultaat van Hallo wachtwoord opnieuw instellen.
6. **Details** – Hallo details van waarom Hallo wachtwoordherstel resulteerde in Hallo waarde dat het geval was.  Omvat ook eventuele risicobeperking stappen mogelijk tooresolve is een onverwachte fout.

### <a name="description-of-report-values"></a>Beschrijving van rapport waarden
Hallo staan volgende tabel verschillende Hallo-waarden toegestaan voor elke kolom:

| Kolom | Toegestane waarden en hun betekenis |
| --- | --- |
| Methoden die worden gebruikt |**Alternatief e-mailadres** – gebruiker gebruikt alternatieve e-mailadres of verificatie e tooauthenticate<p>**Telefoon (werk)** – gebruiker gebruikt office phone tooauthenticate<p>**Mobiele telefoon** – gebruiker de mobiele telefoon of verificatie phone tooauthenticate gebruikt<p>**Beveiligingsvragen** – gebruikt gebruikersbeveiliging tooauthenticate vragen<p>**Een combinatie van Hallo hierboven (bijvoorbeeld alternatieve e-mail + mobiele telefoon)** – treedt op wanneer een beleid 2-gate is opgegeven en ziet u welke twee methoden Hallo gebruiker gebruikt tooauthentication verzoek voor zijn/haar wachtwoord opnieuw instellen. |
| Resultaat |**Afgebroken** – gebruiker opnieuw instellen van wachtwoorden is gestart maar wordt gestopt halverwege via zonder te voltooien<p>**Geblokkeerd** : gebruikersaccount is toouse wachtwoordherstel vanwege tooattempting toouse Hallo wachtwoord opnieuw instellen van pagina of een enkel wachtwoord opnieuw instellen in gate te vaak een periode van 24 uur<p>**Geannuleerd** – wachtwoord opnieuw instellen is gestart, maar vervolgens geklikt op Hallo annuleren knop toocancel Hallo sessie gedeeltelijk manier tot en met de gebruiker <p>**Verbinding gemaakt met de beheerder** – gebruiker heeft een probleem opgetreden tijdens de sessie die hij kan niet worden omgezet, zodat de gebruiker Hallo geklikt 'Contact op met uw beheerder' Hallo-koppeling niet is voltooid Hallo wachtwoordherstel stroom<p>**Kan geen** : gebruiker is niet kunnen tooreset een wachtwoord, waarschijnlijk omdat Hallo gebruiker niet geconfigureerd toouse Hallo-functie is (bv. Er is geen licentie, ontbrekende informatie voor verificatie, wachtwoord beheerd on-premises, maar Write-back is uitgeschakeld).<p>**Geslaagd** – wachtwoordherstel is geslaagd. |
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
| De gebruiker geannuleerd voordat deze verificatiemethoden Hallo vereist |Geannuleerd |
| De gebruiker geannuleerd voor het verzenden van een nieuw wachtwoord |Geannuleerd |
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

## <a name="next-steps"></a>Volgende stappen
Hieronder staan koppelingen tooall Hallo documentatie van Azure AD-wachtwoord opnieuw instellen:

* **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Hoe het werkt** ](active-directory-passwords-how-it-works.md) -informatie over Hallo zes verschillende onderdelen van het Hallo-service en wat elk biedt
* [**Aan de slag** ](active-directory-passwords-getting-started.md) -informatie over hoe tooallow u tooreset gebruikers en hun cloud of on-premises wachtwoorden wijzigen
* [**Aanpassen** ](active-directory-passwords-customize.md) - informatie over hoe toocustomize Hallo eruit zien & is vernieuwd en het gedrag van Hallo service tooyour de behoeften van organisatie
* [**Aanbevolen procedures** ](active-directory-passwords-best-practices.md) -informatie over hoe tooquickly implementeren en effectief beheren van wachtwoorden in uw organisatie
* [**Veelgestelde vragen over** ](active-directory-passwords-faq.md) -antwoorden toofrequently vragen
* [**Het oplossen van problemen** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooquickly problemen oplossen met Hallo-service
* [**Meer informatie** ](active-directory-passwords-learn-more.md) : meer informatie over Hallo technische details van de werking van Hallo-service
