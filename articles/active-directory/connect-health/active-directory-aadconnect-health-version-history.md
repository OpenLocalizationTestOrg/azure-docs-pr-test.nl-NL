---
title: aaaAzure AD Connect Health versiegeschiedenis
description: Dit document beschrijft Hallo releases voor Azure AD Connect Health en wat is opgenomen in deze versies.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Versiegeschiedenis van status Azure AD Connect
Azure AD Connect Health Hello Azure Active Directory-team regelmatig bijgewerkt met nieuwe functies en functionaliteit. Dit artikel worden Hallo-versies en onderdelen die zijn uitgebracht.

## <a name="october-2016"></a>Oktober 2016
**Agentupdate:**

* Azure AD Connect Health-agent voor AD FS \(versie 2.6.408.0\)
  1. Verbeteringen in het client-IP-adressen in verificatieaanvragen detecteren
  2. Oplossingen voor problemen gerelateerde tooAlerts
* Azure AD Connect Health-agent voor AD DS (versie 2.6.408.0)
  1. Oplossingen voor problemen die betrekking tooAlerts.
* Azure AD Connect Health-agent voor synchronisatie (versie 2.6.353.0) uitgebracht met Azure AD Connect versie 1.1.281.0
  1. Hallo vereist gegevens leveren voor Hallo foutrapporten voor synchronisatie
  2. Oplossingen voor problemen gerelateerde tooAlerts

**Nieuwe preview-functies:**

* Synchronisatie van foutrapporten voor Azure AD Connect

**Nieuwe functies:**

* Azure AD Connect Health voor AD FS - veld IP-adres is beschikbaar in Hallo rapport over top 50 van gebruikers met een onjuiste gebruikersnaam en wachtwoord.

## <a name="july-2016"></a>Juli 2016
**Nieuwe preview-functies:**

* [Azure AD Connect Health voor AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>Januari 2016
**Agentupdate:**

* Azure AD Connect Health-agent voor AD FS (versie 2.6.91.1512)

**Nieuwe functies:**

* [Hulpprogramma voor test-connectiviteit voor Azure AD Connect Health-Agents](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>November 2015
**Nieuwe functies:**

* Ondersteuning voor [toegangsbeheer op basis van rollen](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**Nieuwe preview-functies:**

* [Azure AD Connect Health voor synchroniseren](active-directory-aadconnect-health-sync.md).

**Opgeloste problemen:**

* Oplossingen voor fouten weergegeven tijdens agent registraties.

## <a name="september-2015"></a>September 2015
**Nieuwe functies:**

* Onjuiste gebruikersnaam wachtwoord rapport voor AD FS
* Ondersteuning voor tooconfigure Unauthenticated HTTP-Proxy
* Ondersteuning voor tooconfigure-agent op Server core
* Verbeteringen tooAlerts voor AD FS
* Verbeteringen in Azure AD Connect Health-Agent voor AD FS voor de verbinding en gegevens uploaden.

**Opgeloste problemen:**

* Oplossingen voor problemen in inzicht in het gebruik voor AD FS-fouttypen.

## <a name="june-2015"></a>Juni 2015
**Initiële versie van Azure AD Connect Health voor AD FS en AD FS-Proxy.**

**Nieuwe functies:**

* Waarschuwingen voor het controleren van AD FS en AD FS-Proxy-servers met e-mailmeldingen.
* Eenvoudige toegang tooAD FS topologie en patronen in AD FS-prestatiemeteritems.
* Trend van geslaagde aanvragen voor beveiligingstokens op AD FS-servers die zijn gegroepeerd op toepassingen, verificatiemethoden, aanvragen netwerk locatie enzovoort.
* Ontwikkeling van op AD FS-servers die zijn gegroepeerd op toepassingen, fout typen enzovoort van mislukte aanvragen.
* Eenvoudigere implementatie van Agent met behulp van globale beheerder van Azure AD-referenties.  

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [uw lokale identiteit infrastructuur en de synchronisatie-services bewaken in de cloud Hallo](active-directory-aadconnect-health.md).

