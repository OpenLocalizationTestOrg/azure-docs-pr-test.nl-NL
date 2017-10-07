---
title: aaaAzure Active Directory-rapportage latenties | Microsoft Docs
description: Meer informatie over Hallo hoeveelheid tijd die nodig is voor het melden van gebeurtenissen tooshow up in uw Azure-portal
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Azure Active Directory-rapportage latenties

Met [reporting](active-directory-preview-explainer.md) hello Azure Active Directory, u alle benodigde toodetermine hoe uw omgeving doet Hallo gegevens opvragen. Hallo hoeveelheid tijd die nodig is voor het melden van gegevens tooshow omhoog in hello Azure-portal wordt ook wel latentie. 

Dit onderwerp staan Hallo latentiegegevens Hallo alle reporting categorieën in hello Azure-portal. 


## <a name="activity-reports"></a>Activiteitsrapporten

Er zijn twee gebieden van de activiteit reporting:

- **Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden
- **Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten

Hallo volgende tabel vindt u Hallo latentiegegevens voor activiteitsrapporten.

| Rapport | Minimum | Gemiddelde | Maximum |
| :-- | --- | --- | --- |
| Controlelogboeken             | 30 minuten  | 45 minuten | 1 uur     |
| Aanmeldingen               | 15 minuten  | 15 minuten | 2 uur *   |

>[!NOTE]
> Voor sommige activiteitsgegevens voor aanmeldingen afkomstig is van de oudere office-toepassingen, kan het Hallo gegevens tooshow rapporteert too8 uur duren voordat. 


## <a name="security-reports"></a>Beveiligingsrapporten

Er zijn twee soorten beveiliging reporting:

- **Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount. 
- **Gebruikers voor wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. 

Hallo volgende tabel geeft een lijst Hallo latentiegegevens beveiligingsrapporten.

| Rapport | Minimum | Gemiddelde | Maximum |
| :-- | --- | --- | --- |
| Gebruikers die risico lopen          | 5 minuten   | 15 minuten  | 2 uur  |
| Riskant aanmeldingen         | 5 minuten   | 15 minuten  | 2 uur  |

## <a name="risk-events"></a>Risico 's

Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect verdachte acties die gerelateerd tooyour gebruikersaccounts zijn. Elke verdachte actie wordt opgeslagen in een gebeurtenis vastleggen genoemd risico gedetecteerd.

Hallo volgende tabel geeft een lijst Hallo latentiegegevens risico's.

| Rapport | Minimum | Gemiddelde | Maximum |
| :-- | --- | --- | --- |
| Aanmeldingen vanaf anonieme IP-adressen |5 minuten |15 minuten |2 uur |
| Aanmeldingen vanaf onbekende locaties |5 minuten |15 minuten |2 uur |
| Gebruikers van wie de referenties zijn gelekt |2 uur |4 uur |8 uur |
| Onmogelijke reis tooatypical locaties |5 minuten |1 uur |8 uur  |
| Aanmeldingen vanaf geïnfecteerde apparaten |2 uur |4 uur |8 uur  |
| Aanmeldingen van IP-adressen met verdachte activiteit |2 uur |4 uur |8 uur  |



## <a name="next-steps"></a>Volgende stappen

Als u meer over Hallo activiteitsrapporten in Azure-portal Hallo tooknow wilt, Zie:

- [Rapporten in Azure Active Directory-beheerportal Hallo aanmeldingsactiviteiten](active-directory-reporting-activity-sign-ins.md)
- [Activiteitsrapporten in Azure Active Directory-beheerportal Hallo controleren](active-directory-reporting-activity-audit-logs.md)

Als u meer informatie over de beveiligingsrapporten Hallo in hello Azure-portal tooknow wilt, Zie:

- [Gebruikers op risico beveiligingsrapport in hello Azure Active Directory-portal](active-directory-reporting-security-user-at-risk.md)
- [Rapport van riskante aanmeldingen in hello Azure Active Directory-portal](active-directory-reporting-security-risky-sign-ins.md)

Als u meer informatie over de risico's tooknow wilt, Zie [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).
