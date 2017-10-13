---
title: Azure AD Connect Health gebruiken met AD DS | Microsoft Docs
description: Dit is de Azure AD Connect Health-pagina waarop wordt besproken hoe AD DS kunt controleren.
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9e5b45d71b978c383932409f0037a4f6f32d0cb3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Azure AD Connect Health gebruiken met AD DS
De volgende documentatie is specifiek voor het controleren van Active Directory Domain Services met Azure AD Connect Health. De ondersteunde versies van AD DS zijn: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016.

Zie [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md) (Engelstalig) voor meer informatie over het controleren van AD FS met Azure AD Connect Health. Zie [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md) voor informatie over het controleren van AD Connect (Sync) met Azure AD Connect Health.

![Azure AD Connect Health voor AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Waarschuwingen voor Azure AD Connect Health voor AD DS
De sectie waarschuwingen in Azure AD Connect Health voor AD DS biedt u een lijst met actieve en opgeloste waarschuwingen die betrekking hebben op uw domeincontrollers. Bij het selecteren van een actieve of opgeloste waarschuwing wordt een nieuwe blade geopend met aanvullende informatie, samen met stappen om het probleem op te lossen en koppelingen naar ondersteunende documentatie. Elk type waarschuwing kan een of meer exemplaren hebben die overeenstemmen met elk van de domeincontrollers die betrekking hebben op die waarschuwing. Onderaan de waarschuwingsblade kunt u dubbelklikken op een betrokken domeincontroller om een nieuwe blade te openen met aanvullende informatie over het waarschuwingsexemplaar.

Op deze blade kunt u e-mailmeldingen inschakelen voor waarschuwingen en het tijdsbereik in de weergave wijzigen. Als u het tijdsbereik vergroot, kunt u eerdere waarschuwingen die zijn opgelost weergeven.

![Azure AD Connect-synchronisatiefout](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Dashboard voor domeincontrollers
Dit dashboard biedt een topologische weergave van uw omgeving, samen met belangrijke operationele statistieken en de status van elk van de bewaakte domeincontrollers. De aangeboden metrische gegevens helpen om snel alle domeincontrollers die mogelijk verder onderzocht moeten worden te identificeren. Standaard wordt alleen een subset van de kolommen weergegeven. U kunt echter de gehele set met beschikbare kolommen vinden door te dubbelklikken op de opdracht voor kolommen. Door de voor u meest interessante kolommen te selecteren wordt dit dashboard een handige plek om de status van uw AD DS-omgeving te bekijken.

![Domeincontrollers](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Domeincontrollers kunnen worden gegroepeerd op hun respectievelijke domein of de site, wat nuttig is voor het begrijpen van de topologie van de omgeving. Als u ten slotte dubbelklikt u op de bladekop, wordt het dashboard gemaximaliseerd om de beschikbare schermruimte te gebruiken. Deze grote weergave is handig als u meerdere kolommen weergeeft.

## <a name="replication-status-dashboard"></a>Dashboard voor replicatiestatus
Dit dashboard geeft een overzicht van de replicatiestatus en -topologie van uw bewaakte domeincontrollers. De status van de meest recente replicatiepoging wordt weergegeven, samen met nuttige documentatie voor elke fout die is gevonden. U kunt dubbelklikken op een domeincontroller met een fout om een nieuwe blade te openen met informatie, zoals details over de fout, aanbevolen stappen om het probleem te verhelpen en koppelingen naar documentatie over het oplossen van problemen.

![Replicatiestatus](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Bewaking
Deze functie biedt grafische trends van verschillende prestatiemeters, die voortdurend worden verzameld van elke bewaakte domeincontroller. Prestaties van een domeincontroller kunnen eenvoudig worden vergeleken met andere bewaakte domeincontrollers in uw forest. Bovendien ziet u verschillende prestatiemeters naast elkaar, dit is nuttig bij probleemoplossing in uw omgeving.

![Bewaking](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Standaard hebben we vier prestatiemeters vooraf geselecteerd; u kunt echter andere meters opnemen door op de filteropdracht te klikken en de gewenste meters te (de)selecteren. Als u klikt op de grafiek van een prestatiemeter, wordt een nieuwe blade geopend. Deze bevat de gegevenspunten voor elke bewaakte domeincontroller.

## <a name="related-links"></a>Verwante koppelingen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md) (Azure AD Connect Health-bewerkingen)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

