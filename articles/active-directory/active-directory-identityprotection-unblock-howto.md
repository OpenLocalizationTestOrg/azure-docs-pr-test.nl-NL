---
title: 'Active Directory: Identity Protection - aaaAzure hoe gebruikers toounblock | Microsoft Docs'
description: 'Meer informatie over hoe de blokkering opheffen gebruikers die zijn geblokkeerd door een Azure Active Directory: Identity Protection-beleid.'
services: active-directory
keywords: beveiliging van Azure active directory-identiteit, deblokkeren van gebruiker
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory: Identity Protection - hoe toounblock gebruikers
U kunt met Azure Active Directory: Identity Protection beleid tooblock gebruikers als Hallo geconfigureerd voorwaarden is voldaan. Normaal gesproken een geblokkeerde gebruiker contactpersonen help helpdesk toobecome gedeblokkeerd. Dit onderwerp wordt uitgelegd Hallo stappen kunt u een geblokkeerde gebruiker toounblock uitvoeren.

## <a name="determine-hello-reason-for-blocking"></a>Hallo reden voor het blokkeren van bepalen
Als een eerste stap toounblock een gebruiker moet u toodetermine Hallo type Hallo gebruiker is geblokkeerd omdat de volgende stappen zijn afhankelijk van het beleid.
Met Azure Active Directory: Identity Protection, kan een gebruiker ofwel worden geblokkeerd door een beleid voor aanmelden risico of gebruikersbeleid risico.

U kunt krijgen Hallo type beleid dat een gebruiker uit het Hallo-kop in Hallo dialoogvenster dat toohello gebruiker is opgegeven tijdens een aanmeldingspoging is geblokkeerd:

| Beleid | Gebruikersdialoogvenster |
| --- | --- |
| Aanmelden risico |![Geblokkeerde aanmelden](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Gebruiker risico |![Geblokkeerde account](./media/active-directory-identityprotection-unblock-howto/104.png) |

Een gebruiker die is geblokkeerd door:

* Een beleid aanmelden risico wordt ook wel bekend als verdachte aanmelden
* Gebruikersbeleid risico wordt ook wel een account risico

## <a name="unblocking-suspicious-sign-ins"></a>Deblokkeren verdachte aanmeldingen
toounblock een verdachte aanmelden, hebt u Hallo volgende opties:

1. **Aanmelden van een vertrouwde locatie of het apparaat** -een veelvoorkomende reden voor geblokkeerde verdachte aanmeldingen zijn aanmeldpogingen vanaf onbekende locaties of apparaten. Uw gebruikers kunnen snel bepalen of dit Hallo reden worden geblokkeerd door de toosign in van een vertrouwde locatie of het apparaat is.
2. **Uitsluiten van beleid** : als u denkt dat de huidige configuratie Hallo van uw beleid voor aanmelden wordt veroorzaakt door problemen voor specifieke gebruikers, kunt u gebruikers Hallo uitsluiten van deze. Zie [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) voor meer informatie.
3. **Schakel beleid** : als u denkt dat de configuratie van uw beleid wordt veroorzaakt door problemen voor alle gebruikers, kunt u beleid Hallo uitschakelen. Zie [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) voor meer informatie.

## <a name="unblocking-accounts-at-risk"></a>Deblokkeren accounts risico
toounblock de account die risico hebt u Hallo volgende opties:

1. **Wachtwoord opnieuw instellen** -kunt u het wachtwoord van Hallo gebruiker opnieuw instellen. Zie [handmatige beveiligd wachtwoord opnieuw instellen](active-directory-identityprotection.md#manual-secure-password-reset) voor meer informatie.
2. **Alle risicogebeurtenissen negeren** -Hallo risico gebruikersbeleid een gebruiker wordt geblokkeerd als Hallo geconfigureerd gebruiker risiconiveau voor het blokkeren van toegang is bereikt. U kunt verkleinen dat een gebruiker het risiconiveau door handmatig sluiten risicogebeurtenissen die worden gerapporteerd. Zie voor meer informatie [risicogebeurtenissen handmatig sluiten](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Uitsluiten van beleid** : als u denkt dat de huidige configuratie Hallo van uw beleid voor aanmelden wordt veroorzaakt door problemen voor specifieke gebruikers, kunt u gebruikers Hallo uitsluiten van deze. Zie [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) voor meer informatie.
4. **Schakel beleid** : als u denkt dat de configuratie van uw beleid wordt veroorzaakt door problemen voor alle gebruikers, kunt u beleid Hallo uitschakelen. Zie [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
 Wilt u meer informatie over Azure AD Identity Protection tooknow? Bekijk [Azure Active Directory: Identity Protection](active-directory-identityprotection.md).
