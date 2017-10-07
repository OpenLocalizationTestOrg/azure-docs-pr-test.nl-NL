---
title: 'Azure Active Directory-rapportage: aan de slag | Microsoft Docs'
description: Een lijst met Hallo diverse beschikbare rapporten in Azure Active Directory-rapportage
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Aan de slag met Azure Active Directory-rapportage
## <a name="what-it-is"></a>Wat is het?
Azure Active Directory (Azure AD) bevat beveiligings-, activiteits- en controlerapporten voor uw directory. Hier volgt een lijst met opgenomen Hallo-rapporten:

### <a name="security-reports"></a>Beveiligingsrapporten
* Aanmeldingen van onbekende bronnen
* Aanmeldingen na meerdere mislukte pogingen
* Aanmeldingen vanuit meerdere locaties
* Aanmeldingen van IP-adressen met verdachte activiteit
* Onregelmatige aanmeldingsactiviteiten
* Aanmeldingen vanaf mogelijk geïnfecteerde apparaten
* Gebruikers met afwijkende aanmeldingsactiviteiten

### <a name="activity-reports"></a>Activiteitsrapporten
* Toepassingsgebruik: samenvatting
* Toepassingsgebruik: gedetailleerd
* Toepassingsdashboard
* Fouten bij het inrichten van een account
* Afzonderlijke gebruikersapparaten
* Afzonderlijke gebruikersactiviteiten
* Rapport met groepsactiviteiten
* Rapport voor de registratie van opnieuw ingestelde wachtwoorden
* Activiteit voor wachtwoord opnieuw instellen

### <a name="audit-reports"></a>Controlerapporten
* Directorycontrolerapport

> [!TIP]
> Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.
> 
> 

## <a name="how-it-works"></a>Hoe werkt het?
### <a name="reporting-pipeline"></a>Rapportagepijplijn
Hallo-rapportagepijplijn bestaat uit drie hoofdstappen. Telkens wanneer een gebruiker zich aanmeldt of een verificatie wordt uitgevoerd, wordt Hallo volgende gebeurt:

* Eerst Hallo gebruiker is geverifieerd (geslaagd of mislukt) en Hallo resultaat opgeslagen in hello Azure Active Directory-servicedatabases.
* Op vaste intervallen worden alle recente aanmeldingen verwerkt. Op dit punt worden met onze algoritmen voor beveiliging en afwijkende activiteiten alle recente aanmeldingen doorzocht op verdachte activiteiten.
* Na de verwerking zijn Hallo rapporten geschreven, in de cache opgeslagen en weergegeven in de klassieke Azure-portal Hallo.

### <a name="report-generation-times"></a>Tijden waarop rapporten worden gegenereerd
Vervaldatum toohello groot aantal verificaties en meld u dat modules verwerkt door hello Azure AD-platform, zijn Hallo meest recente verwerkte aanmeldingen, gemiddeld een uur oud. In zeldzame gevallen kan het too8 uren tooprocess Hallo meest recente aanmeldingen duren.

U vindt aanmeldingspagina Hallo meest recente verwerkt door in de help-tekst hello Hallo boven aan elk rapport.

![Help-tekst hello boven aan elk rapport](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.
> 
> 

## <a name="getting-started"></a>Aan de slag
### <a name="sign-into-hello-azure-classic-portal"></a>Meld u aan bij Hallo klassieke Azure-portal
Eerst moet u toosign in Hallo [klassieke Azure-portal](https://manage.windowsazure.com) als een globale beheerder of compliancebeheerder. U moet ook een Azure-abonnement servicebeheerder of medebeheerder of gebruikmaken van Hallo 'toegang tooAzure AD' Azure-abonnement.

### <a name="navigate-tooreports"></a>Navigeer tooReports
tooview rapporten, navigeer toohello rapporten tabblad Hallo boven aan uw directory.

Als dit de eerste keer Hallo rapporten weergeven, moet u tooagree tooa dialoogvenster voordat u Hallo rapporten kunt weergeven. Dit is dat het is acceptabel voor beheerders in uw organisatie tooview tooensure deze gegevens worden beschouwd als persoonlijke gegevens in sommige landen.

![Dialoogvenster](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Elk rapport verkennen
Navigeer in elk rapport toosee Hallo gegevens worden verzameld en Hallo aanmeldingen verwerkt. U vindt een [lijst met alle rapporten Hallo hier](active-directory-reporting-guide.md).

![Alle rapporten](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Hallo rapporten downloaden als CSV
Elk rapport kan worden gedownload als een CSV-bestand (door komma's gescheiden waarden). U kunt deze bestanden in Excel, Power BI of van derden analysis toofurther programma's analyseren van uw gegevens.

toodownload een rapport als een CSV toohello rapport navigeren en klik op 'Downloaden' hello onderaan.

![Knop Downloaden](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.
> 
> 

## <a name="next-steps"></a>Volgende stappen
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Waarschuwingen voor afwijkende aanmeldingsactiviteiten aanpassen
Navigeer toohello 'Configureren' tabblad van uw directory.

Schuif in de sectie 'Meldingen' toohello.

In- of uitschakelen van Hallo 'E-mailmeldingen van afwijkende aanmeldingen' sectie.

![Hallo sectie meldingen](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Hallo integreren met Azure AD rapportage-API
Zie [rapportage-API aan de slag met Hallo](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Multi-Factor Authentication inschakelen voor gebruikers
Selecteer een gebruiker in een rapport.

Klik op Hallo 'MFA inschakelen' hello onder welkomstscherm aan.

![Hallo multi-Factor Authentication knop aan de onderkant Hallo van welkomstscherm](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.
> 
> 

## <a name="learn-more"></a>Meer informatie
### <a name="audit-events"></a>Controlegebeurtenissen
Meer informatie over de gebeurtenissen worden gecontroleerd in de map Hallo in [Azure Active Directory Reporting controlegebeurtenissen](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>API-integratie
Zie [rapportage-API aan de slag met Hallo](active-directory-reporting-api-getting-started.md) en Hallo [API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Contact opnemen
Stuur een e-mail naar [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) voor feedback, hulp of als u nog andere vragen hebt.

> [!TIP]
> Bekijk [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) voor meer documentatie over Azure AD-rapportage.
> 
> 

