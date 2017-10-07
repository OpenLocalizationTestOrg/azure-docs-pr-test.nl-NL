---
title: Azure AD Connect Health met het synchroniseren van aaaUsing | Microsoft Docs
description: Dit is hello Azure AD Connect Health-pagina waarop wordt besproken hoe toomonitor Azure AD Connect synchroniseren.
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>De Azure AD Connect synchronisatie met Azure AD Connect Health bewaken
Hallo volgende documentatie is specifiek toomonitoring Azure AD Connect (Sync) met Azure AD Connect Health.  Zie [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md) (Engelstalig) voor informatie over het controleren van AD FS met Azure AD Connect Health. Zie ook [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md) voor informatie over het bewaken van Active Directory Domain Services met Azure AD Connect Health.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Waarschuwingen voor Azure AD Connect Health voor synchroniseren
Hello Azure AD waarschuwingen Connect Health voor synchroniseren sectie biedt Hallo van lijst met actieve waarschuwingen. Elke waarschuwing omvat relevante informatie, stappen voor het oplossen en koppelingen toorelated documentatie. Door het selecteren van een actieve of opgeloste waarschuwing ziet u een nieuwe blade met aanvullende informatie, evenals de mogelijke stappen tooresolve Hallo waarschuwing en koppelingen tooadditional documentatie. U kunt ook historische gegevens weergeven voor waarschuwingen die in de afgelopen Hallo zijn opgelost.

Als u een waarschuwing u met aanvullende informatie zoals stappen krijgt selecteert kunt u nemen tooresolve Hallo waarschuwing en links tooadditional documentatie.

![Azure AD Connect-synchronisatiefout](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Beperkte evaluatie van waarschuwingen
Als Azure AD Connect is de standaardconfiguratie Hallo niet gebruikt (bijvoorbeeld als het kenmerkfilter is gewijzigd van Hallo standaard configuratie tooa aangepaste configuratie), wordt vervolgens hello Azure AD Connect Health-agent niet uploaden Hallo fout gebeurtenissen gerelateerde tooAzure AD Connect.

Dit beperkt Hallo evaluatie van waarschuwingen door Hallo-service. Zou ziet u een banner waarin deze situatie in hello Azure-Portal onder uw service.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/banner.png)

U kunt dit wijzigen door te klikken op 'Instellingen' en Azure AD Connect Health agent tooupload zodat alle foutlogboeken.

![Azure AD Connect Health voor synchroniseren](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Inzicht in synchronisatie
Beheerders vaak wilt tooknow over Hallo duurt toosync wijzigingen tooAzure AD en Hallo hoeveelheid wijzigingen plaatsvinden. Deze functie biedt een eenvoudige manier toovisualize dit Hallo onder grafieken met:   

* Latentie van de synchronisatiebewerkingen
* Trend van objectwijziging

### <a name="sync-latency"></a>Synchronisatielatentie
Deze functie biedt een grafische trend weergegeven van de latentie van Hallo van synchronisatiebewerkingen (import, export, enzovoort) voor connectors.  Dit biedt een snelle en eenvoudige manier toounderstand Hallo niet alleen latentie van uw bewerkingen (groter als er een groot aantal veranderingen), maar ook een manier toodetect afwijkingen in Hallo latentie die nader moeten worden onderzocht.

![Synchronisatielatentie](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Alleen Hallo latentie van 'Exporteren' Hallo-bewerking voor hello Azure AD-connector wordt standaard weergegeven.  toosee meer bewerkingen op Hallo connector of tooview-bewerkingen van andere connectoren met de rechtermuisknop op Hallo grafiek, selecteer grafiek bewerken of klik op Hallo 'Latentie grafiek bewerken' knop en kies de specifieke bewerking Hallo en connectors.

### <a name="sync-object-changes"></a>Synchronisatie van objectwijzigingen
Deze functie biedt een grafische trend weergegeven van het aantal wijzigingen die wordt geëvalueerd en geëxporteerd tooAzure AD Hallo.  Vandaag, poging toogather deze informatie wordt uit de synchronisatielogboeken Hallo is moeilijk.  Hallo grafiek biedt niet alleen een eenvoudigere manier om bewaking Hallo aantal wijzigingen die plaatsvinden in uw omgeving, maar ook een visuele weergave van Hallo fouten die zich voordoen.

![Synchronisatielatentie](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Synchronisatiefoutenrapport op objectniveau (Preview)
Deze functie genereert een rapport over synchronisatiefouten die zich voordoen wanneer identiteitsgegevens worden gesynchroniseerd tussen Windows Server AD en Azure AD met Azure AD Connect.

* Hallo rapport bevat informatie over fouten die zijn geregistreerd door Hallo sync-client (Azure AD Connect versie 1.1.281.0 of hoger)
* Hallo-fouten die zijn opgetreden in de laatste synchronisatiebewerking Hallo op Hallo synchronisatie-engine opgenomen. ('Exporteren' op Hallo Azure AD-Connector.)
* Azure AD Connect Health-agent voor synchronisatie moet uitgaande verbinding toohello vereiste eindpunten voor Hallo rapport tooinclude Hallo meest recente gegevens hebben.
* Hallo-rapport is **bijgewerkte na elke 30 minuten** met behulp van Hallo gegevens geüpload door Azure AD Connect Health for sync-agent. Het biedt Hallo volgen de belangrijkste mogelijkheden

  * Classificatie van fouten
  * Lijst van objecten met fouten per categorie
  * Alle Hallo gegevens over fouten op één plek Hallo
  * Vergelijking van de kant van objecten met de fout gevolg tooa conflict naast
  * Hallo foutenrapport downloaden als een CSV-volume (binnenkort)

### <a name="categorization-of-errors"></a>Classificatie van fouten
Hallo rapport categoriseert Hallo bestaande synchronisatiefouten in Hallo volgende categorieën:

| Category | Beschrijving |
| --- | --- |
| Dubbel-kenmerk |Fouten wanneer Azure AD Connect objecten probeert te maken of bij te werken met dubbele waarden in een of meer kenmerken in Azure AD die uniek moeten zijn in een tenant, zoals proxyAddresses, UserPrincipalName. |
| Gegevens komen niet overeen |Fouten als Hallo soft-match toomatch-objecten die in synchronisatiefouten resulteren is mislukt. |
| Gegevensvalidatiefout |Fouten vanwege tooinvalid gegevens, zoals niet-ondersteunde tekens in belangrijke kenmerken, zoals UserPrincipalName, opmaken fouten die validatie voordat het wordt geschreven in Azure AD is mislukt. |
| Groot-kenmerk |Fouten bij een of meer kenmerken groter dan Hallo zijn toegestane grootte, de lengte of count. |
| Overige |Alle andere fouten die niet in Hallo boven de categorieën passen. Op basis van feedback wordt deze categorie in subcategorieën gesplitst. |

![Overzicht van synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Categorieën in synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lijst van objecten met fouten per categorie
Dieper ingegaan op elke categorie bieden Hallo-lijst met objecten met Hallo fout in die categorie.
![Lijst in synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Foutdetails
Volgt gegevens is beschikbaar in Hallo detailweergave voor elke fout

* Id's voor Hallo *AD-Object* betrokken
* Id's voor Hallo *Azure AD-Object* betrokken (indien van toepassing)
* Beschrijving van de fout en hoe toofix
* Verwante artikelen:

![Details van synchronisatiefoutenrapport](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Hallo foutenrapport downloaden als CSV
Door het selecteren van Hallo 'exporteren' knop kunt u een CSV-bestand met alle Hallo details over alle Hallo fouten downloaden.

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