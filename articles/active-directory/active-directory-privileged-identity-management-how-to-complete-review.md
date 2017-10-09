---
title: aaaHow toocomplete een onderzoek toegang | Microsoft Docs
description: Nadat u een revisie toegang in Azure AD Privileged Identity Management gestart, informatie over hoe toocomplete deze en bekijkt hello resultaten
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Hoe toocomplete een toegang controleren in Azure AD Privileged Identity Management
Bevoorrechte rol beheerders kunnen bekijken voor bevoorrechte toegang eenmaal een [beveiligingsbeoordeling is gestart](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) stuurt automatisch een e-mailbericht waarin wordt gevraagd tooreview gebruikers toegang krijgen. Als een gebruiker niet een e-mailbericht ontvangt is, kunt u deze instructies Hallo in verzenden [hoe tooperform beveiliging controleren](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Nadat Hallo beveiliging controleren periode of alle gebruikers van Hallo klaar bent met hun eigen bekijken, Hallo stappen in dit artikel hebt gecontroleerd toomanage hello en Hallo resultaten te zien.

## <a name="manage-security-reviews"></a>Beoordelingen van beveiliging beheren
1. Ga toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo **Azure AD Privileged Identity Management** toepassing op uw dashboard.
2. Selecteer Hallo **toegang tot beoordelingen** sectie van het Hallo-dashboard.
3. Selecteer Hallo toegang controleren dat u wilt dat toomanage.

Op Hallo toegang controleren detail blade zijn er een aantal opties voor het beheren van deze evaluatie.

![PIM toegang controleren knoppen - schermafbeelding][1]

### <a name="remind"></a>Herinneren
Als een evaluatie van de toegang is ingesteld zodat Hallo gebruikers zelf bekijken, Hallo **herinnering sturen** knop verstuurt een melding. 

### <a name="stop"></a>Stoppen
Alle beoordelingen van toegang tot een einddatum hebben, maar kunt u Hallo **stoppen** knop toofinish deze vroeg. Als gebruikers zich nog niet is gecontroleerd op dit tijdstip, ze niet kunnen tooafter u stopt met het Hallo-revisie. U kunt een beoordeling niet opnieuw starten nadat deze gestopt.

### <a name="apply"></a>Aanvragen
Nadat een revisie access is voltooid, ofwel omdat u Hallo-einddatum is bereikt of handmatig gestopt Hallo **toepassen** knop Hallo resultaten van Hallo onderzoek implementeert. Als een gebruiker toegang is geweigerd Hallo gecontroleerd, is dit Hallo stap die hun roltoewijzing wordt verwijderd.  

### <a name="export"></a>Exporteren
Als u handmatig tooapply Hallo resultaten van beveiligingsbeoordeling hello wilt, kunt u Hallo revisie exporteren. Hallo **exporteren** knop downloaden van een CSV-bestand wordt gestart. Hallo resultaten in Excel of andere programma's die CSV-bestanden worden geopend, kunt u beheren.

### <a name="delete"></a>Verwijderen
Als u niet bent geïnteresseerd in Hallo nader bekijken, verwijderen. Hallo **verwijderen** knop Hallo revisie verwijdert uit Hallo PIM-toepassing.

> [!IMPORTANT]
> U wordt niet ophalen van een waarschuwing alvorens deze wordt verwijderd, dus wees zeker dat u wilt dat toodelete die bekijken. 

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
