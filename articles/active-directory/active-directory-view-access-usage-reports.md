---
title: aaaView toegang en gebruik rapporten | Microsoft Docs
description: Legt uit hoe tooview toegang en gebruik rapporten toogain inzicht in de Hallo integriteit en beveiliging van de directory van uw organisatie.
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
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Uw toegangs- en gebruiksrapporten weergeven
*Deze documentatie maakt deel uit van Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*

U kunt toegang tot Azure Active Directory en gebruik rapporten toogain inzicht in Hallo integriteit en beveiliging van de directory van uw organisatie gebruiken. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.

Rapporten zijn in Azure Management Portal hello onderverdeeld in Hallo volgende manieren:

* Afwijkingsdetectie rapporten – bevatten aanmelden gebeurtenissen dat we toobe afwijkende gevonden. Ons doel is toomake u rekening houden met deze activiteit en kunt u toobe kunnen toomake om te bepalen of een gebeurtenis verdacht is.
* Geïntegreerde toepassing rapporten – biedt inzicht in hoe cloud-toepassingen in uw organisatie worden gebruikt. Azure Active Directory biedt integratie met duizenden cloud-toepassingen.
* Foutenrapporten – fouten aangeven die zich voordoen kunnen bij het inrichten van accounts tooexternal toepassingen.
* Gebruikersspecifieke rapporten – weergave apparaat/aanmelden activiteitsgegevens voor een specifieke gebruiker.
* Activiteitenlogboeken – bevatten een record van alle controlegebeurtenissen binnen Hallo laatste 24 uur, afgelopen 7 dagen of afgelopen 30 dagen, evenals wijzigingen activiteit en activiteit voor wachtwoord opnieuw instellen en registratie.

> [!NOTE]
> * Sommige geavanceerde beveiligingsrapporten en resource gebruiksrapporten zijn alleen beschikbaar wanneer u inschakelt [Azure Active Directory Premium](active-directory-get-started-premium.md). Geavanceerde rapporten helpen u de toegangsbeveiliging, verbeteren toopotential bedreigingen reageert en het verkrijgen van toegang tooanalytics over gebruik van het apparaat toegang en de toepassing.
> * Edities Azure Active Directory Premium en Basic zijn beschikbaar voor klanten in China Hallo wereldwijde exemplaar van Azure Active Directory. Edities Azure Active Directory Premium en Basic worden momenteel niet ondersteund in Microsoft Azure-service Hallo beheerd door 21Vianet in China. Voor meer informatie contact met ons opnemen Hallo [Azure Active Directory-Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Rapporten
| Rapport | Beschrijving |
| --- | --- |
| **Rapporten van de afwijkende activiteit** | |
| [Aanmeldingen vanaf onbekende bronnen](active-directory-reporting-sign-ins-from-unknown-sources.md) |Kan duiden op een poging toosign in zonder wordt getraceerd. |
| [Aanmeldingen na meerdere mislukte pogingen](active-directory-reporting-sign-ins-after-multiple-failures.md) |Kan duiden op een geslaagde beveiligingsaanval. |
| [Aanmeldingen vanaf meerdere locaties](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Kan erop wijzen dat meerdere gebruikers met Hallo dezelfde aanmeldt zich account. |
| [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Kan duiden op een geslaagde aanmelding na een poging volgehouden inbraakdetectie. |
| [Aanmeldingen vanaf mogelijk geïnfecteerde apparaten](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Kan duiden op een poging toosign in vanaf mogelijk geïnfecteerde apparaten. |
| [Onregelmatige Aanmeldingsactiviteit](active-directory-reporting-irregular-sign-in-activity.md) |Kan duiden op gebeurtenissen afwijkende toousers aanmelden patronen. |
| [Gebruikers met een afwijkende Aanmeldingsactiviteit](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Hiermee geeft u gebruikers waarvan de accounts is geknoeid. |
| Gebruikers van wie de referenties zijn gelekt |Gebruikers van wie de referenties zijn gelekt |
| **Activiteitenlogboeken** | |
| Controlerapport |Controlegebeurtenissen in uw directory |
| Activiteit voor wachtwoord opnieuw instellen |Biedt een gedetailleerde weergave van wachtwoorden die in uw organisatie voorkomen. |
| Registratie-activiteit wachtwoord opnieuw instellen |Biedt dat een gedetailleerde weergave van het wachtwoord opnieuw instellen van registraties die in uw organisatie voorkomen. |
| Selfservice voor in activiteit |Voorziet in een logboek activiteit tooall groep selfservice-activiteit in uw directory |
| **Geïntegreerde toepassingen** | |
| Gebruik van de toepassing |Bevat een samenvatting van gebruik voor alle SaaS toepassingen die zijn geïntegreerd met uw directory. |
| Inrichten van de activiteit van een account |Biedt een overzicht van pogingen tooprovision accounts tooexternal toepassingen. |
| Overschakeling van de status van het wachtwoord |Bevat een gedetailleerd overzicht van automatische wachtwoord overschakeling van de status van de SaaS-toepassingen. |
| Fouten bij het inrichten van een account |Hiermee wordt aangegeven een impact toousers access tooexternal-toepassingen. |
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
<p>Hallo afwijkend melden activiteitsrapporten vlag verdachte aanmelden activiteit tooOffice365, Azure-beheerportal, Azure AD-Toegangsvenster, Sharepoint Online, Dynamics CRM Online en andere Microsoft online services.</p>

<p>Alle rapporten, behalve het rapport 'Aanmeldingen na meerdere fouten' Hallo ook markeren verdachte <i>federatieve</i> modules toohello hiervoor genoemde services, ongeacht Hallo federatieprovider ondertekenen. </p>

<p>Hallo volgende rapporten zijn beschikbaar: </p><ul>

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
| Toont een record van alle controlegebeurtenissen binnen Hallo afgelopen 24 uur, de afgelopen 7 dagen of de afgelopen 30 dagen. <br /> Zie voor meer informatie [Azure Active Directory-Controlerapportgebeurtenissen](active-directory-reporting-audit-events.md) |Directory > tabblad rapporten |

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
| Toont alle activiteit voor Hallo selfservice beheerde groepen in uw directory. |Directory > Gebruikers > <i>gebruiker</i> > tabblad apparaten |

![Selfservice voor in activiteit](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Geïntegreerde toepassingen rapporten
### <a name="application-usage-summary"></a>Toepassingsgebruik: samenvatting
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Gebruik dit rapport als u toosee gebruik voor alle Hallo SaaS-toepassingen in uw directory. Dit rapport is gebaseerd op Hallo aantal keren dat gebruikers op Hallo-toepassing in Hallo Toegangsvenster hebt geklikt. |Directory > tabblad rapporten |

Dit rapport bevat aanmeldingen te*alle* toepassingen die uw directory heeft toegang tot, inclusief vooraf geïntegreerde toepassingen van Microsoft.

Vooraf geïntegreerde toepassingen van Microsoft opnemen Office 365, Sharepoint, hello Azure-beheerportal en anderen

![Samenvatting van toepassingsgebruik](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Toepassingsgebruik: gedetailleerd
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport gebruiken als u wilt dat toosee hoeveel een bepaalde SaaS-toepassing wordt gebruikt. Dit rapport is gebaseerd op Hallo aantal keren dat gebruikers op Hallo-toepassing in Hallo Toegangsvenster hebt geklikt. |Directory > tabblad rapporten |

### <a name="application-dashboard"></a>Toepassingsdashboard
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport geeft cumulatieve aanmelding modules toohello toepassing door gebruikers in uw organisatie, gedurende een geselecteerde tijdsinterval. Hallo-grafiek op Hallo dashboardpagina kunt u trends voor voor alle informatie over het gebruik van die toepassing. |Directory > toepassing > tabblad Dashboard |

## <a name="error-reports"></a>Foutenrapporten
### <a name="account-provisioning-errors"></a>Fouten bij het inrichten van een account
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Gebruik deze toomonitor-fouten die optreden tijdens de synchronisatie van accounts Hallo van SaaS-toepassingen tooAzure Active Directory. |Directory > tabblad rapporten |

![Fouten bij het inrichten van een account](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Gebruikersspecifieke rapporten
### <a name="devices"></a>Apparaten
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Dit rapport gebruiken als u wilt dat toosee Hallo IP-adres en de geografische locatie van de apparaten waarop een specifieke gebruiker tooaccess Azure Active Directory heeft gebruikt. |Directory > Gebruikers > <i>gebruiker</i> > tabblad apparaten |

### <a name="activity"></a>Activiteit
| Beschrijving | Locatie van registratierapport |
|:--- |:--- |
| Hallo-teken bevat in activiteit voor een gebruiker. Hallo rapport bevat informatie zoals Hallo toepassing aangemeld, het apparaat dat wordt gebruikt, IP-adres en locatie. Er worden niet verzameld Hallo geschiedenis voor gebruikers die met een Microsoft-account aanmelden. |Directory > Gebruikers > <i>gebruiker</i> > tabblad activiteit |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Meld u aan gebeurtenissen die zijn opgenomen in Hallo gebruikersactiviteit rapport
Alleen bepaalde typen gebeurtenissen aanmelden weergegeven in Hallo gebruikersactiviteit rapport.

| Gebeurtenistype | Opgenomen? |
| --- | --- |
| Meld u aan modules toohello [Toegangspaneel](http://myapps.microsoft.com/) |Ja |
| Meld u aan modules toohello [Azure-beheerportal](https://manage.windowsazure.com/) |Ja |
| Meld u aan modules toohello [Microsoft Azure Portal](https://portal.azure.com/) |Ja |
| Meld u aan modules toohello [Office 365-portal](http://portal.office.com/) |Ja |
| Meld u aan modules tooa systeemeigen toepassing, zoals Outlook (Zie onderstaande uitzondering) |Ja |
| Modules tooa federatieve/ingericht app via Hallo paneel voor Apptoegang, zoals Salesforce ondertekenen |Ja |
| Modules tooa op basis van wachtwoorden-app te ondertekenen via Hallo paneel voor Apptoegang, zoals Twitter |Ja |
| Meld u aan modules tooa aangepaste business-app die toohello directory is toegevoegd |Er is geen (binnenkort) |
| Meld u aan modules tooan Azure AD-toepassingsproxy app toohello directory is toegevoegd |Er is geen (binnenkort) |

> Opmerking: tooreduce Hallo hoeveelheid ruis in dit rapport aanmeldingen door Hallo [Microsoft Online Services-aanmeldhulp](http://community.office365.com/en-us/w/sso/534.aspx) worden niet weergegeven.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Dingen tooconsider als u vermoedt dat er inbreuk op de beveiliging
Als u dat denkt een gebruikersaccount kan worden geknoeid of elk soort verdachte gebruikersactiviteit die tooa inbreuk op de beveiliging van uw directory-gegevens in de cloud Hallo kan leiden, u kunt tooconsider een of meer Hallo van de volgende activiteiten:

* Neem contact op met tooverify Hallo-Hallo gebruikersactiviteit
* Hallo gebruikerswachtwoord opnieuw instellen
* [Multi-factor authentication inschakelen](../multi-factor-authentication/multi-factor-authentication-get-started.md) voor extra beveiliging

## <a name="view-or-download-a-report"></a>Weergeven of downloaden van een rapport
1. Klik in de klassieke Azure-portal hello, **Active Directory**op Hallo-naam van de directory van uw organisatie en klik vervolgens op **rapporten**.
2. Op de pagina rapporten Hallo op Hallo rapport dat u wilt tooview en/of downloaden.
   
   > [!NOTE]
   > Als dit Hallo eerst die Hallo rapportagefunctie van Azure Active Directory is gebruikt, ziet u een tooOpt bericht In. Als u akkoord gaat, klikt u op Hallo vinkje pictogram toocontinue.
   > 
   > 
3. Klik op volgende tooInterval van Hallo vervolgkeuzelijst en selecteer vervolgens een Hallo tijdsbereik dat moeten worden gebruikt bij het genereren van dit rapport te volgen:
   
   * Afgelopen 24 uur
   * Afgelopen 7 dagen
   * Afgelopen 30 dagen
4. Klik op Hallo vinkje pictogram toorun Hallo rapport.
   * Up too1000 wordt gebeurtenissen weergegeven in Hallo klassieke Azure-portal.
5. Indien van toepassing, klikt u op **downloaden** toodownload Hallo rapport tooa gecomprimeerd bestand met door komma's gescheiden waarden (CSV)-indeling voor het offline te bekijken of te archiveren.
   * Up too75, worden 000 gebeurtenissen opgenomen in Hallo gedownload bestand.
   * Bekijk voor meer gegevens Hallo [Azure AD rapportage-API](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Een gebeurtenis negeren
Als u geen rapporten afwijkingsdetectie bekijkt, merkt u dat kunt u diverse gebeurtenissen die worden weergegeven in de gerelateerde rapporten negeren. tooignore een gebeurtenis, kaartinformatie Hallo-gebeurtenis in het Hallo-rapport en klik vervolgens op **negeren**. Hallo **negeren** knop Hallo gemarkeerde gebeurtenis wordt permanent worden verwijderd uit Hallo rapport en kan alleen worden gebruikt door de gelicentieerde globale beheerders.

## <a name="automatic-email-notifications"></a>Automatische e-mailmeldingen
Voor meer informatie over Azure AD de meldingen rapportage, Bekijk [Azure Active Directory Reporting meldingen](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Volgend onderwerp
* [Aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Huisstijl tooyour dat pagina's voor aanmelden en de Toegangsvensterpagina toevoegen](active-directory-add-company-branding.md)

