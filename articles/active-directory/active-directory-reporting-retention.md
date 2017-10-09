---
title: bewaarbeleid voor Active Directory-rapport aaaAzure | Microsoft Docs
description: Bewaarbeleid voor gegevens in uw Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Bewaarbeleid voor Azure Active Directory rapport


Dit onderwerp vindt u antwoorden toohello Veelgestelde vragen in combinatie met Hallo Gegevensretentie voor Hallo andere activiteitsrapporten in Azure Active Directory. 

**V: hoe vind u Hallo-verzameling van gegevens over de activiteit is gestart?**

**A:**

| Azure AD-editie | Verzameling starten |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Wanneer u registreert voor een abonnement |
| Azure AD Free | eerste keer openen van Hallo Hallo [Azure Active Directory-blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) of gebruik Hallo [rapportage-API's](https://aka.ms/aadreports)  |

---
**V: waarop uw activiteitsgegevens beschikbaar is in hello Azure-portal?**

**A:**

- **Onmiddellijk** : als u al met rapporten in de klassieke Azure-portal Hallo werkt
- **Binnen 2 uur** : als u dit nog niet hebt ingeschakeld reporting in Hallo klassieke Azure-portal

---
**V: hoe vind u Hallo-verzameling van beveiliging signalen gestart?**  

**A:** voor beveiliging, signalen Hallo verzamelingsproces wordt gestart wanneer u meedoen toouse Hallo Identity Protection Center. 


---
**V: hoe lang hello verzamelde gegevens opgeslagen?**

**A:**

**Activiteitsrapporten**    

| Rapport                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Directorycontrole        | 7 dagen        | 30 dagen             | 30 dagen             |
| Aanmeldingsactiviteit       | 7 dagen        | 30 dagen             | 30 dagen             |

**Beveiliging signalen**

| Rapport         | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Gebruikers die risico lopen  | 7 dagen        | 30 dagen             | 90 dagen             |
| Riskant aanmeldingen | 7 dagen        | 30 dagen             | 90 dagen             |

---