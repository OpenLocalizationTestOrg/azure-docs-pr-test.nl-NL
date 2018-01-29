---
title: Azure AD Connect Health gebruiken met synchronisatie | Microsoft Docs
description: Dit is de Azure AD Connect Health-pagina waarop wordt besproken hoe u synchronisatie met Azure AD Connect kunt controleren.
services: active-directory
documentationcenter: 
author: karavar
manager: mtillman
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 821d4bd7e6b526ad826caf005456edf8235291b8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/11/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>De Azure AD Connect synchronisatie met Azure AD Connect Health bewaken
De volgende documentatie is specifiek voor het bewaken van Azure AD Connect-synchronisatie met Azure AD Connect Health.  Zie [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md) (Engelstalig) voor informatie over het controleren van AD FS met Azure AD Connect Health. Zie ook [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md) voor informatie over het bewaken van Active Directory Domain Services met Azure AD Connect Health.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Waarschuwingen voor Azure AD Connect Health voor synchroniseren
In de sectie Waarschuwingen van Azure AD Connect Health voor synchroniseren vindt u een lijst met actieve waarschuwingen. Elke waarschuwing omvat relevante informatie, stappen voor het oplossen van het probleem en koppelingen naar gerelateerde documentatie. Als u een actieve of opgeloste waarschuwing selecteert, ziet u een nieuwe blade met aanvullende informatie. Ook ziet u stappen die u kunt nemen voor het oplossen van het probleem en koppelingen naar aanvullende documentatie. U kunt ook u historische gegevens bekijken voor waarschuwingen die in het verleden zijn opgelost.

Als u een waarschuwing selecteert, ziet u aanvullende informatie. Ook ziet u stappen die u kunt nemen voor het oplossen van het probleem en koppelingen naar aanvullende documentatie.

![Azure AD Connect-synchronisatiefout](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Beperkte evaluatie van waarschuwingen
Als Azure AD Connect NIET wordt gebruikt met de standaardconfiguratie (bijvoorbeeld als het kenmerkfilter is gewijzigd van de standaardconfiguratie in een aangepaste configuratie), worden met de Azure AD Connect Health-agent geen fouten geüpload die zijn gerelateerd aan Azure AD Connect.

Dit beperkt de evaluatie van waarschuwingen door de service. In Azure Portal ziet u onder uw service een banner waarin deze situatie wordt beschreven.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/banner.png)

U kunt dit wijzigen door te klikken op 'Instellingen' en de Azure AD Connect Health-agent toestemming te verlenen om alle foutlogboeken te uploaden.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Inzicht in synchronisatie
Beheerders willen vaak weten hoe lang het duurt om wijzigingen te synchroniseren met Azure AD en hoeveel wijzigingen er worden uitgevoerd. Deze functie biedt een eenvoudige manier om dit te visualiseren met behulp van onderstaande grafieken:   

* Latentie van de synchronisatiebewerkingen
* Trend van objectwijziging

### <a name="sync-latency"></a>Synchronisatielatentie
Met deze functie wordt een grafische trend weergegeven van de latentie van de synchronisatiebewerkingen (import, export, enzovoort) voor connectoren.  Dit biedt een snelle en eenvoudige manier om niet alleen inzicht te krijgen in de latentie van uw bewerkingen (groter als er een grote set wijzigingen moet worden uitgevoerd), maar het is ook een manier om onregelmatigheden in de latentie te ontdekken die nader moeten worden onderzocht.

![Synchronisatielatentie](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Standaard wordt alleen de latentie van de bewerking 'Exporteren' voor de Azure AD-connector weergegeven.  Als u meer bewerkingen wilt bekijken voor de connector of als u bewerkingen van andere connectoren wilt zien, klikt u met de rechtermuisknop in de grafiek en kiest u Grafiek bewerken. U kunt ook op de knop Latentiediagram bewerken klikken en de specifieke bewerking en connectoren selecteren.

### <a name="sync-object-changes"></a>Synchronisatie van objectwijzigingen
Deze functie biedt een grafisch weergegeven trend van het aantal wijzigingen dat wordt geëvalueerd en geëxporteerd naar Azure AD.  Op dit moment is het verzamelen van deze informatie uit de synchronisatielogboeken nog moeilijk.  De grafiek biedt niet alleen een eenvoudigere manier om het aantal wijzigingen in uw omgeving te controleren, maar ook een visuele weergave van de fouten die zich voordoen.

![Synchronisatielatentie](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Synchronisatiefoutenrapport op objectniveau (Preview)
Deze functie genereert een rapport over synchronisatiefouten die zich voordoen wanneer identiteitsgegevens worden gesynchroniseerd tussen Windows Server AD en Azure AD met Azure AD Connect.

* Het rapport bevat informatie over fouten die zijn vastgelegd door de synchronisatieclient (Azure AD Connect versie 1.1.281.0 of later)
* Het bevat de fouten die zijn opgetreden tijdens de laatste synchronisatie op de synchronisatie-engine. ('Exporteren' op de Azure AD-connector.)
* Azure AD Connect Health-agent voor synchronisatie moet uitgaande connectiviteit hebben met de vereiste eindpunten om de meest recente gegevens in het rapport te kunnen opnemen.
* Het rapport wordt **elke 30 minuten bijgewerkt** met de gegevens die door Azure AD Connect Health-agent voor synchronisatie zijn geüpload. Het bevat de volgende hoofdmogelijkheden

  * Classificatie van fouten
  * Lijst van objecten met fouten per categorie
  * Alle gegevens over de fouten op één plek
  * Vergelijking naast elkaar van objecten die fouten hebben vanwege een conflict
  * De mogelijkheid om het foutenrapport te downloaden als een CSV (binnenkort)

### <a name="categorization-of-errors"></a>Classificatie van fouten
In het rapport worden de bestaande synchronisatiefouten in de volgende categorieën onderverdeeld:

| Category | Beschrijving |
| --- | --- |
| Dubbel-kenmerk |Fouten wanneer Azure AD Connect objecten probeert te maken of bij te werken met dubbele waarden in een of meer kenmerken in Azure AD die uniek moeten zijn in een tenant, zoals proxyAddresses, UserPrincipalName. |
| Gegevens komen niet overeen |Fouten wanneer de zachte match er niet in slaagt om objecten te koppelen die synchronisatiefouten opleveren. |
| Gegevensvalidatiefout |Fouten vanwege ongeldige gegevens, zoals niet-ondersteunde tekens in essentiële kenmerken, zoals UserPrincipalName, indelingsfouten die de validatie niet doorstaan voordat ze naar Azure AD worden geschreven. |
| Groot-kenmerk |Fouten wanneer een of meer kenmerken groter zijn dan de toegestane grootte, lengte of aantal. |
| Overige |Alle andere fouten die niet in de bovenstaande categorieën passen. Op basis van feedback wordt deze categorie in subcategorieën gesplitst. |

![Overzicht van synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Categorieën in synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lijst van objecten met fouten per categorie
Als u op een categorie inzoomt, wordt de lijst weergegeven met objecten die de fout in die categorie vertonen.
![Lijst in synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Foutdetails
De volgende gegevens zijn beschikbaar in de gedetailleerde weergave van elke fout

* Id's voor het betrokken *AD-object*
* Id's voor betrokken *Azure AD-object* (indien van toepassing)
* Beschrijving van de fout en de oplossing
* Verwante artikelen:

![Details van synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a>Het foutenrapport downloaden als een CSV
Als u op Exporteren klikt, downloadt u een CSV-bestand met alle informatie over alle fouten.

## <a name="related-links"></a>Verwante koppelingen
* [Troubleshooting Errors during synchronization](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md) (Synchronisatiefouten oplossen)
* [Duplicate Attribute Resiliency](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) (Tolerantie van Dubbel-kenmerk)
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md) (Azure AD Connect Health-bewerkingen)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)