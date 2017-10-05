---
title: Uw toegangs- en gebruiksrapporten weergeven | Microsoft Docs
description: Legt uit hoe toegang en gebruiksrapporten weergeven inzicht te verwerven in de integriteit en beveiliging van de directory van uw organisatie.
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 038ac79ebf61c6429fbf7ca21eefe9414bcfc03a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="view-your-access-and-usage-reports"></a>Uw toegangs- en gebruiksrapporten weergeven
*Deze documentatie maakt deel uit van de [Azure Active Directory-rapportagegids](active-directory-reporting-guide.md).*

U kunt toegang tot Azure Active Directory- en gebruiksrapporten meer inzicht verkrijgen in de integriteit en beveiliging van de directory van uw organisatie. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's mogelijk liggen zodat ze voldoende plannen kunnen die risico's te beperken.

Rapporten zijn in de Azure-beheerportal onderverdeeld in de volgende manieren:

* Afwijkingsdetectie rapporten – bevatten aanmelden gebeurtenissen die we afwijkende worden gevonden. Ons doel is u rekening houden met deze activiteit en kunt u om te bepalen of een gebeurtenis verdacht is.
* Geïntegreerde toepassing rapporten – biedt inzicht in hoe cloud-toepassingen in uw organisatie worden gebruikt. Azure Active Directory biedt integratie met duizenden cloud-toepassingen.
* Foutenrapporten – fouten aangeven die zich voordoen kunnen bij het inrichten van accounts kunnen externe toepassingen.
* Gebruikersspecifieke rapporten – weergave apparaat/aanmelden activiteitsgegevens voor een specifieke gebruiker.
* Activiteitenlogboeken – bevatten een record van alle controlegebeurtenissen binnen de afgelopen 24 uur, afgelopen 7 dagen of afgelopen 30 dagen, evenals wijzigingen in groep activiteiten en activiteit voor wachtwoord opnieuw instellen en registratie.

> [!NOTE]
> * Sommige geavanceerde beveiligingsrapporten en resource gebruiksrapporten zijn alleen beschikbaar wanneer u inschakelt [Azure Active Directory Premium](active-directory-get-started-premium.md). Geavanceerde rapporten helpen u verbeterde toegangsbeveiliging, reageren op potentiële dreigingen en toegang krijgen tot analytics op het gebruik van het apparaat toegang en de toepassing.
> * De Azure Active Directory-edities Premium en Basic zijn beschikbaar voor klanten in China via het wereldwijde exemplaar van Azure Active Directory. De edities Azure Active Directory Premium en Basic worden momenteel niet ondersteund in de Microsoft Azure-service die wordt beheerd door 21Vianet in China. Neem contact met ons op via het [Azure Active Directory-forum](https://feedback.azure.com/forums/169401-azure-active-directory/) voor meer informatie.
> 
> 

## <a name="reports"></a>Rapporten
| Rapport | Beschrijving |
| --- | --- |
| **Rapporten van de afwijkende activiteit** | |
| [Aanmeldingen vanaf onbekende bronnen](active-directory-reporting-sign-ins-from-unknown-sources.md) |Kan duiden op een poging om aan te melden zonder wordt getraceerd. |
| [Aanmeldingen na meerdere mislukte pogingen](active-directory-reporting-sign-ins-after-multiple-failures.md) |Kan duiden op een geslaagde beveiligingsaanval. |
| [Aanmeldingen vanaf meerdere locaties](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Kan erop wijzen dat meerdere gebruikers met hetzelfde account aanmeldt zich. |
| [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Kan duiden op een geslaagde aanmelding na een poging volgehouden inbraakdetectie. |
| [Aanmeldingen vanaf mogelijk geïnfecteerde apparaten](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Kan duiden op een poging om aan te melden vanaf mogelijk geïnfecteerde apparaten. |
| [Onregelmatige Aanmeldingsactiviteit](active-directory-reporting-irregular-sign-in-activity.md) |Kan duiden op gebeurtenissen afwijkende om gebruikers te ondertekenen in patronen. |
| [Gebruikers met een afwijkende Aanmeldingsactiviteit](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Hiermee geeft u gebruikers waarvan de accounts is geknoeid. |
| Gebruikers van wie de referenties zijn gelekt |Gebruikers van wie de referenties zijn gelekt |
| **Activiteitenlogboeken** | |
| Controlerapport |Controlegebeurtenissen in uw directory |
| Activiteit voor wachtwoord opnieuw instellen |Biedt een gedetailleerde weergave van wachtwoorden die in uw organisatie voorkomen. |
| Registratie-activiteit wachtwoord opnieuw instellen |Biedt dat een gedetailleerde weergave van het wachtwoord opnieuw instellen van registraties die in uw organisatie voorkomen. |
| Selfservice voor in activiteit |Biedt een activiteitenlogboek op alle groep selfservice-activiteit in uw directory |
| **Geïntegreerde toepassingen** | |
| Gebruik van de toepassing |Bevat een samenvatting van gebruik voor alle SaaS toepassingen die zijn geïntegreerd met uw directory. |
| Inrichten van de activiteit van een account |Biedt een overzicht van pogingen tot het inrichten van accounts kunnen externe toepassingen. |
| Overschakeling van de status van het wachtwoord |Bevat een gedetailleerd overzicht van automatische wachtwoord overschakeling van de status van de SaaS-toepassingen. |
| Fouten bij het inrichten van een account |Hiermee geeft u een gevolgen voor gebruikers toegang tot externe toepassingen. |
| **Rights management** | |
| Gebruik van de RMS |Bevat een samenvatting voor de Rights Management-gebruik |
| Meest actieve RMS-gebruiker |Geeft een lijst van top 1000 actieve gebruikers dat de RMS-beveiligde bestanden zijn geopend |
| Gebruik van de RMS-apparaat |Een lijst met apparaten die worden gebruikt voor toegang tot bestanden die RMS-beveiliging |
| Gebruik van de toepassing RMS is ingeschakeld |Biedt informatie over het gebruik van RMS-toepassingen |

## <a name="report-editions"></a>Rapport edities
| Rapport | Gratis | Basic | Premium |
| --- | --- | --- | --- |
| **Rapporten van de afwijkende activiteit** | | | |
| Aanmeldingen vanaf onbekende bronnen |✓ |✓ |✓ |
| Aanmeldingen na meerdere mislukte pogingen |✓ |✓ |✓ |
| Aanmeldingen vanaf meerdere locaties |✓ |✓ |✓ |
| Aanmeldingen vanaf IP-adressen met verdachte activiteiten | | |✓ |
| Aanmeldingen vanaf mogelijk geïnfecteerde apparaten | | |✓ |
| Onregelmatige Aanmeldingsactiviteit | | |✓ |
| Gebruikers met een afwijkende Aanmeldingsactiviteit | | |✓ |
| Gebruikers van wie de referenties zijn gelekt | | |✓ |
| **Activiteitenlogboeken** | | | |
| Controlerapport |✓ |✓ |✓ |
| Activiteit voor wachtwoord opnieuw instellen | | |✓ |
| Registratie-activiteit wachtwoord opnieuw instellen | | |✓ |
| Selfservice voor in activiteit | | |✓ |
| **Geïntegreerde toepassingen** | | | |
| Gebruik van de toepassing | | |✓ |
| Inrichten van de activiteit van een account |✓ |✓ |✓ |
| Overschakeling van de status van het wachtwoord | | |✓ |
| Fouten bij het inrichten van een account |✓ |✓ |✓ |
| **Rights management** | | | |
| Gebruik van de RMS | | |Alleen RMS |
| Meest actieve RMS-gebruiker | | |Alleen RMS |
| Gebruik van de RMS-apparaat | | |Alleen RMS |
| Gebruik van de toepassing RMS is ingeschakeld | | |Alleen RMS |

## <a name="anomalous-activity-reports"></a>Rapporten van de afwijkende activiteit
<p>De afwijkende aanmelden activiteitsrapporten vlag verdacht in activiteit Office365, Azure-beheerportal, Azure AD-Toegangsvenster, Sharepoint Online, Dynamics CRM Online en andere Microsoft online services.</p>

<p>Alle rapporten, met uitzondering van het rapport 'Aanmeldingen na meerdere fouten' ook markeren verdachte <i>federatieve</i> aanmeldingen bij de hiervoor genoemde services, ongeacht de federatieprovider. </p>

<p>De volgende rapporten zijn beschikbaar: </p><ul>

<li>[Aanmeldingen vanaf onbekende bronnen](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Aanmeldingen na meerdere mislukte pogingen](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Aanmeldingen vanaf meerdere locaties](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Aanmeldingen vanaf IP-adressen met verdachte activiteit](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Onregelmatige Aanmeldingsactiviteit](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Aanmeldingen vanaf mogelijk geïnfecteerde apparaten](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Gebruikers met een afwijkende Aanmeldingsactiviteit](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Gebruikers van wie de referenties zijn gelekt</li></ul>

## <a name="activity-logs"></a>Activiteitenlogboeken
### <a name="audit-report"></a>Controlerapport
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Toont een record van alle controlegebeurtenissen in de afgelopen 24 uur, de afgelopen 7 dagen of de afgelopen 30 dagen. <br /> Zie voor meer informatie [Azure Active Directory-Controlerapportgebeurtenissen](active-directory-reporting-audit-events.md) |Directory > tabblad rapporten |

![Controlerapport](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Activiteit voor wachtwoord opnieuw instellen
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Bevat dat alle pogingen die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel. |Directory > tabblad rapporten |

![Activiteit voor wachtwoord opnieuw instellen](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Registratie-activiteit wachtwoord opnieuw instellen
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Bevat dat alle registraties die hebben plaatsgevonden in uw organisatie voor wachtwoordherstel |Directory > tabblad rapporten |

![Registratie-activiteit wachtwoord opnieuw instellen](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Selfservice voor in activiteit
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Geeft alle activiteiten voor de selfservice beheerde groepen in uw directory. |Directory > Gebruikers > <i>gebruiker</i> > tabblad apparaten |

![Selfservice voor in activiteit](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Geïntegreerde toepassingen rapporten
### <a name="application-usage-summary"></a>Toepassingsgebruik: samenvatting
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport gebruiken wanneer u wilt weergeven van informatie over het gebruik voor de SaaS-toepassingen in uw directory. Dit rapport is gebaseerd op het aantal keren dat gebruikers op de toepassing in het deelvenster toegang hebt geklikt. |Directory > tabblad rapporten |

Dit rapport bevat een teken aanmeldingen bij de *alle* toepassingen die uw directory heeft toegang tot, inclusief vooraf geïntegreerde toepassingen van Microsoft.

Vooraf geïntegreerde toepassingen van Microsoft opnemen Office 365, Sharepoint, de Azure-beheerportal en anderen

![Samenvatting van toepassingsgebruik](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Toepassingsgebruik: gedetailleerd
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport gebruiken als u wilt zien hoeveel een bepaalde SaaS-toepassing wordt gebruikt. Dit rapport is gebaseerd op het aantal keren dat gebruikers op de toepassing in het deelvenster toegang hebt geklikt. |Directory > tabblad rapporten |

### <a name="application-dashboard"></a>Toepassingsdashboard
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport geeft aan dat cumulatieve aanmelding aanmeldingen bij de toepassing door gebruikers in uw organisatie, gedurende een geselecteerde tijdsinterval. De grafiek op de dashboardpagina kunt u trends voor voor alle informatie over het gebruik van die toepassing. |Directory > toepassing > tabblad Dashboard |

## <a name="error-reports"></a>Foutenrapporten
### <a name="account-provisioning-errors"></a>Fouten bij het inrichten van een account
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Gebruik dit voor het bewaken van fouten die tijdens de synchronisatie van accounts van SaaS-toepassingen met Azure Active Directory optreden. |Directory > tabblad rapporten |

![Fouten bij het inrichten van een account](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Gebruikersspecifieke rapporten
### <a name="devices"></a>Apparaten
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport gebruiken wanneer u zien van de IP-adres en de geografische locatie van de apparaten die een specifieke gebruiker is gebruikt wilt voor toegang tot Azure Active Directory. |Directory > Gebruikers > <i>gebruiker</i> > tabblad apparaten |

### <a name="activity"></a>Activiteit
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Geeft het teken in activiteit voor een gebruiker. Het rapport bevat informatie zoals de toepassing aangemeld, het apparaat dat wordt gebruikt, IP-adres en locatie. Verzamelt de geschiedenis voor gebruikers die met een Microsoft-account aanmelden. |Directory > Gebruikers > <i>gebruiker</i> > tabblad activiteit |

#### <a name="sign-in-events-included-in-the-user-activity-report"></a>Meld u aan gebeurtenissen die zijn opgenomen in het rapport gebruikersactiviteit
Alleen bepaalde typen gebeurtenissen aanmelding wordt weergegeven in het rapport gebruikersactiviteit.

| Gebeurtenistype | Opgenomen? |
| --- | --- |
| Aanmeldingen naar de [Configuratiescherm openen](http://myapps.microsoft.com/) |Ja |
| Aanmeldingen naar de [Azure-beheerportal](https://manage.windowsazure.com/) |Ja |
| Aanmeldingen naar de [Microsoft Azure-Portal](https://portal.azure.com/) |Ja |
| Aanmeldingen naar de [Office 365-portal](http://portal.office.com/) |Ja |
| Aanmeldingen aan een systeemeigen toepassing, zoals Outlook (Zie onderstaande uitzondering) |Ja |
| Aanmeldingen aan een app federatieve/ingericht via het toegangsvenster zoals Salesforce |Ja |
| Aanmeldingen aan een app op basis van wachtwoorden via het toegangsvenster zoals Twitter |Ja |
| Aanmeldingen naar een aangepaste business-app die is toegevoegd aan de map |Er is geen (binnenkort) |
| Aanmeldingen naar een Azure AD-toepassingsproxy-app die is toegevoegd aan de map |Er is geen (binnenkort) |

> Opmerking: Als u de hoeveelheid ruis in dit rapport, aanmeldingen door de [Microsoft Online Services-aanmeldhulp](http://community.office365.com/en-us/w/sso/534.aspx) worden niet weergegeven.
> 
> 

## <a name="things-to-consider-if-you-suspect-security-breach"></a>Zaken die u moet overwegen als u vermoedt dat er inbreuk op de beveiliging
Als u dat denkt een gebruikersaccount kan worden geknoeid of elk soort verdachte gebruikersactiviteit die kan leiden tot een inbreuk op de beveiliging van uw directory-gegevens in de cloud, kunt u een of meer van de volgende acties overwegen:

* Neem contact op met de gebruiker om te controleren of de activiteit
* Het gebruikerswachtwoord opnieuw instellen
* [Multi-factor authentication inschakelen](../multi-factor-authentication/multi-factor-authentication-get-started.md) voor extra beveiliging

## <a name="view-or-download-a-report"></a>Weergeven of downloaden van een rapport
1. Klik in de klassieke Azure-portal op **Active Directory**, klikt u op de naam van de directory van uw organisatie en klik vervolgens op **rapporten**.
2. Klik op het rapport dat u wilt bekijken en/of downloaden op de pagina rapporten.
   
   > [!NOTE]
   > Als dit de eerste keer dat u hebt de rapportagefunctie van Azure Active Directory gebruikt, ziet u een bericht zich aanmelden. Als u akkoord gaat, klikt u op het vinkje om door te gaan.
   > 
   > 
3. Klik op de vervolgkeuzelijst naast Interval en selecteer vervolgens een van de volgende bereiken voor de tijd die moeten worden gebruikt bij het genereren van dit rapport:
   
   * Afgelopen 24 uur
   * Afgelopen 7 dagen
   * Afgelopen 30 dagen
4. Klik op het vinkje om het rapport uitvoert.
   * Maximaal 1000 gebeurtenissen wordt weergegeven in de klassieke Azure portal.
5. Indien van toepassing, klikt u op **downloaden** voor het downloaden van het rapport naar een gecomprimeerd bestand met door komma's gescheiden waarden (CSV)-indeling voor het offline te bekijken of te archiveren.
   * Maximaal 75.000 gebeurtenissen worden opgenomen in het gedownloade bestand.
   * Bekijk voor meer gegevens de [Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Een gebeurtenis negeren
Als u geen rapporten afwijkingsdetectie bekijkt, merkt u dat kunt u diverse gebeurtenissen die worden weergegeven in de gerelateerde rapporten negeren. Als u wilt dat een gebeurtenis, markeert u gewoon de gebeurtenis in het rapport en klik vervolgens op **negeren**. De **negeren** knop wordt de gemarkeerde gebeurtenis permanent verwijderd uit het rapport en kan alleen worden gebruikt door de gelicentieerde globale beheerders.

## <a name="automatic-email-notifications"></a>Automatische e-mailmeldingen
Voor meer informatie over Azure AD de meldingen rapportage, Bekijk [Azure Active Directory Reporting meldingen](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Volgend onderwerp
* [Aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md)
* [De huisstijl van uw bedrijf toevoegen aan de aanmeldingspagina en de toegangsvensterpagina’s](active-directory-add-company-branding.md)

