---
title: Azure AD Connect Synchronization Service Manager-bewerkingen | Microsoft Docs
description: Hallo Operations tabblad in Hallo Synchronization Service Manager begrijpen voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Met behulp van Hallo tabblad Synchronisatie Service Manager-bewerkingen

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

Hallo operations tabblad toont Hallo resultaten van de meest recente Hallo-bewerkingen. Op dit tabblad is sleutel toounderstand en oplossen van problemen.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Hallo informatie zichtbaar is in het tabblad Hallo-bewerkingen begrijpen
het bovenste gedeelte Hallo toont alle wordt uitgevoerd in chronologische volgorde. Standaard Hallo operations logboek bevat gegevens over de Hallo afgelopen zeven dagen, maar deze instelling kan worden gewijzigd met de Hallo [scheduler](active-directory-aadconnectsync-feature-scheduler.md). U wilt toolook voor alle uitvoeren die een status geslaagd niet weergegeven. U kunt Hallo sorteren door te klikken op Hallo headers wijzigen.

Hallo **Status** kolom Hallo meest belangrijke informatie en toont Hallo ernstigste probleem voor een run. Hier volgt een korte samenvatting van de meest voorkomende statussen Hallo in volgorde van prioriteit tooinvestigate (waarbij * enkele mogelijke fout tekenreeksen geven).

| Status | Opmerking |
| --- | --- |
| Stop-* |Hallo uitvoeren kan niet worden voltooid. Bijvoorbeeld, als hello extern systeem niet actief is en kan geen verbinding worden gemaakt. |
| gestopt fout limiet |Er zijn meer dan 5000 fouten. Hallo uitvoeren is automatisch gestopt vanwege het grote aantal fouten toohello. |
| voltooide -\*-fouten |Hallo voltooide uitgevoerd, maar er zijn fouten (minder dan 5000) die moeten worden onderzocht. |
| voltooide -\*-waarschuwingen |Hallo uitvoeren voltooid, maar sommige gegevens is niet in staat Hallo verwacht. Als u fouten hebt, klikt u vervolgens dit bericht is meestal slechts een symptoom zijn. Totdat u fouten hebt opgelost, moet u de waarschuwingen niet onderzoeken. |
| voltooid |Geen problemen. |

Wanneer u een rij selecteert, updates Hallo onder tooshow Hallo details van die worden uitgevoerd. Hallo onder toohello ver linksboven, hebt u mogelijk een lijst met de melding **stap #**. Deze lijst wordt alleen weergegeven als er meerdere domeinen in uw forest waar elk domein wordt vertegenwoordigd door een stap. Hallo-domeinnaam vindt u onder de kop Hallo **partitie**. Onder **Synchronisatiestatistieken**, vindt u meer informatie over Hallo aantal wijzigingen dat is verwerkt. U kunt klikken op Hallo koppelingen tooget een lijst met objecten Hallo gewijzigd. Als u objecten met fouten hebt, deze fouten worden weergegeven onder **synchronisatiefouten**.

Zie voor meer informatie [oplossen van een object dat niet kan worden gesynchroniseerd](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
