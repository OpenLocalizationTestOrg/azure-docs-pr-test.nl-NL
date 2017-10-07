---
title: Azure AD Connect Health met AD DS aaaUsing | Microsoft Docs
description: Dit is hello Azure AD Connect Health-pagina waarop wordt besproken hoe toomonitor AD DS.
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
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Azure AD Connect Health gebruiken met AD DS
Hallo volgende documentatie is specifiek toomonitoring Active Directory Domain Services met Azure AD Connect Health. Hallo ondersteunde versies van AD DS zijn: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016.

Zie [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md) (Engelstalig) voor meer informatie over het controleren van AD FS met Azure AD Connect Health. Zie [Using Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md) voor informatie over het controleren van AD Connect (Sync) met Azure AD Connect Health.

![Azure AD Connect Health voor AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Waarschuwingen voor Azure AD Connect Health voor AD DS
Hallo in de sectie waarschuwingen in Azure AD Connect Health voor AD DS, geeft u een lijst van actieve en opgeloste waarschuwingen, gerelateerde tooyour-domeincontrollers. Selecteren van een waarschuwing actief of opgelost, wordt een nieuwe blade geopend met meer informatie, samen met de stappen voor het oplossen, en koppelingen toosupporting documentatie. Elk type waarschuwing kan een of meer instanties die overeenkomen met tooeach van domeincontrollers Hallo beïnvloed door deze bepaalde waarschuwing hebben. U kunt dubbelklikken op een geïnfecteerde domain controller tooopen een extra blade met meer informatie over deze waarschuwing exemplaar aan de onderkant van de Hallo van waarschuwing blade hello.

In deze blade kunt u e-mailmeldingen voor waarschuwingen inschakelen en Hallo tijdsbereik in de weergave te wijzigen. Hallo tijdsbereik uitbreidt, kunt u toosee voorafgaande opgeloste waarschuwingen.

![Azure AD Connect-synchronisatiefout](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Dashboard voor domeincontrollers
Dit dashboard biedt een topologische weergave van uw omgeving, samen met belangrijke operationele statistieken en de status van elk van de bewaakte domeincontrollers. Hallo weergegeven metrische gegevens helpen tooquickly identificeren, de domeincontrollers die mogelijk verder onderzoek. Alleen een subset van kolommen hello wordt standaard weergegeven. U vindt echter Hallo volledige set van beschikbare kolommen door te dubbelklikken op Hallo kolommen opdracht. Hallo-kolommen die u meest belangrijk vindt Hiermee schakelt u dit dashboard in één en eenvoudig plaatsen tooview Hallo status van uw AD DS-omgeving selecteren.

![Domeincontrollers](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

-Domeincontrollers kunnen worden gegroepeerd op hun respectieve domein of de locatie, die helpen te begrijpen Hallo omgeving topologie. Ten slotte, als u dubbelklikt op Hallo blade header, Hallo dashboard maximaliseert de tooutilize Hallo beschikbaar scherm-vastgoed. Deze grote weergave is handig als u meerdere kolommen weergeeft.

## <a name="replication-status-dashboard"></a>Dashboard voor replicatiestatus
Dit dashboard geeft een overzicht van Hallo replicatie status en replicatie-topologie van uw bewaakte domeincontrollers. Hallo-status van de meest recente replicatiepoging Hallo wordt weergegeven, samen met de nuttige documentatie voor elke fout die is gevonden. U kunt dubbelklikken op een domeincontroller met een fout optreedt, tooopen een nieuwe blade met informatie, zoals: over Hallo fout, aanbevolen stappen, details en koppelingen tootroubleshooting documentatie.

![Replicatiestatus](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Bewaking
Deze functie biedt een grafische trends van verschillende prestatiemeteritems die continu worden verzameld van elk van de domeincontrollers Hallo bewaakt. Prestaties van een domeincontroller kunnen eenvoudig worden vergeleken met andere bewaakte domeincontrollers in uw forest. Bovendien ziet u verschillende prestatiemeters naast elkaar, dit is nuttig bij probleemoplossing in uw omgeving.

![Bewaking](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Standaard hebben we voorgeselecteerd, vier prestatiemeteritems; u kunt anderen echter opnemen door te klikken op Hallo filteropdracht en selecteren of uitschakel gewenste prestatiemeteritems. U kunt bovendien een prestaties teller grafiek tooopen een nieuwe blade, waaronder gegevenspunten voor elk van de domeincontrollers bewaakt Hallo dubbelklikken.

## <a name="related-links"></a>Verwante koppelingen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md) (Azure AD Connect Health-bewerkingen)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

