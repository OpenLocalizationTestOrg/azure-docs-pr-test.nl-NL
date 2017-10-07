---
title: aaaHow toouse Hallo auditlogboek in Azure AD Privileged Identity Management | Microsoft Docs
description: Meer informatie over hoe toouse Hallo van het controlelogboek in hello Azure Privileged Identity Management-uitbreiding.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Met behulp van het controlelogboek Hallo in PIM
U kunt Hallo Privileged Identity Management (PIM) audit log toosee alle Hallo gebruikerstoewijzingen en activeringen binnen een bepaalde periode. Als u wilt dat toosee Hallo volledige controlegeschiedenis van activiteit in uw tenant, met inbegrip van de beheerder, eindgebruikers en synchronisatieactiviteiten, kunt u Hallo [Azure Active Directory-toegang en gebruik rapporten.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Het controlelogboek toohello navigeren
Van Hallo [Azure-portal](https://portal.azure.com) dashboard, selecteer Hallo **Azure AD Privileged Identity Management** app. Van daaruit toegang krijgen tot het controlelogboek Hallo door te klikken op **bevoorrechte rollen beheren** > **controlegeschiedenis** in Hallo PIM-dashboard.

## <a name="hello-audit-log-graph"></a>Hallo audit log-grafiek
U kunt Hallo audit log tooview Hallo totaal activeringen, max activeringen per dag en gemiddelde activeringen per dag gebruiken in een lijndiagram.  U kunt ook Hallo gegevens filteren per rol als er meer dan één rol in de controlegeschiedenis Hallo.

Gebruik Hallo **tijd**, **actie**, en **rol** knoppen toosort Hallo logboek.

## <a name="hello-audit-log-list"></a>Hallo audit log-lijst
Hallo-kolommen in Hallo audit log lijst zijn:

* **Aanvrager** -Hallo-gebruiker die heeft aangevraagd Hallo rol activeren of wijzigen.  Als het Hallo-waarde is 'Azure systeem', controleert u hello Azure controlelogboek voor meer informatie.
* **Gebruiker** -Hallo-gebruiker die wordt geactiveerd of tooa rol is toegewezen.
* **Rol** -Hallo rol toegewezen of geactiveerd door Hallo-gebruiker.
* **Actie** - Hallo-acties die door de aanvrager Hallo. Het kan hierbij gaan toewijzing, ongedaan maken, activeren of deactiveren.
* **Tijd** : wanneer het Hallo-actie is opgetreden.
* **Redeneren** -als de tekst in Hallo reden veld is ingevoerd tijdens de activering, deze hier wordt weergegeven.
* **Vervaldatum** - alleen relevant voor de activering van rollen.

## <a name="filter-hello-audit-log"></a>Hallo-controlelogboek filteren
U kunt Hallo informatie filteren die wordt weergegeven in het controlelogboek Hallo door te klikken op Hallo **Filter** knop.  Hallo **Update grafiek parameters blade** wordt weergegeven.

Wanneer u filters Hallo ingesteld, klikt u op **Update** toofilter Hallo gegevens in Hallo logboek.  Als het Hallo-gegevens worden niet meteen weergegeven, moet u Hallo pagina vernieuwen.

### <a name="change-hello-date-range"></a>Hallo datumbereik wijzigen
Gebruik Hallo **vandaag**, **afgelopen Week**, **afgelopen maand**, of **aangepaste** toochange Hallo tijdsbereik van het controlelogboek Hallo knoppen.

Wanneer u kiest voor Hallo **aangepaste** knop, krijgt u een **van** datumveld en een **naar** veld toospecify een datumbereik voor Hallo logboek datum.  U kunt Hallo datums opgeven in de notatie DD-MM-jjjj of klik op Hallo **kalender** pictogram en kies Hallo datum in een kalender.

### <a name="change-hello-roles-included-in-hello-log"></a>Hallo-functies die zijn opgenomen in het logboek Hallo wijzigen
Schakel Hallo of **rol** zich aanmelden op Hallo selectievakje volgende tooeach rol tooinclude of uitsluiten.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

