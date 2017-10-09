---
title: aaaHow tooconfigure beveiligingswaarschuwingen | Microsoft Docs
description: Meer informatie over hoe tooconfigure beveiligingswaarschuwingen voor Azure Privileged Identity Management-extensie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>Hoe tooconfigure beveiligingswaarschuwingen in Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Beveiligingswaarschuwingen
Azure Privileged Identity Management (PIM) genereert waarschuwingen wanneer er verdachte of unsafe activiteiten in uw omgeving. Wanneer een waarschuwing wordt geactiveerd, wordt deze weergegeven op Hallo PIM-dashboard. Selecteer Hallo waarschuwing toosee een rapport dat een lijst met gebruikers of rollen die Hallo waarschuwing heeft geactiveerd Hallo.

![PIM-dashboard beveiligingswaarschuwingen - schermafbeelding][1]

| Waarschuwing | Trigger | Aanbeveling |
| --- | --- | --- |
| **Rollen zijn momenteel toegewezen buiten PIM** |Een beheerder is permanent toegewezen tooa-functie buiten Hallo PIM-interface. |Bekijk het nieuwe roltoewijzing Hallo. Omdat andere services alleen permanente beheerders toewijst kunnen, het in aanmerking komende toewijzing tooan indien nodig wijzigen. |
| **Rollen worden te vaak geactiveerd** |Er zijn te veel heractiveringen Hallo dezelfde rol binnen Hallo tijd toegestaan in Hallo-instellingen. |Neem contact op met Hallo gebruiker toosee waarom ze hebben geactiveerd Hallo rol zo vaak. Misschien Hallo tijd van de limiet is te kort voor hen toocomplete hun taken, of misschien ze gebruikmaakt van scripts tooautomatically een rol activeren. |
| **Rollen niet is vereist van MFA voor activering** |Er zijn functies zonder MFA ingeschakeld in Hallo-instellingen. |We MFA vereisen voor uitgebreide beheerdersmogelijkheden meest Hallo rollen, maar raden MFA voor activering voor alle functies in te schakelen. |
| **Beheerders hun bevoorrechte rollen niet gebruiken** |Er zijn in aanmerking komende beheerders die hun rollen onlangs nog niet geactiveerd. |Start een toegang controleren toodetermine Hallo gebruikers die geen toegang meer nodig. |
| **Er zijn te veel globale beheerders** |Er zijn meer globale beheerders dan aanbevolen. |Als u een groot aantal globale beheerders hebt, is het waarschijnlijk dat gebruikers wel meer machtigingen dan ze nodig hebben. Verplaatsen gebruikers tooless bevoegde rollen, of zorg enkele ervan voor de rol Hallo in plaats van in aanmerking komende permanent zijn toegewezen. |

## <a name="configure-security-alert-settings"></a>Waarschuwing beveiligingsinstellingen configureren
U kunt sommige Hallo beveiligingswaarschuwingen in PIM toowork met uw omgeving en beveiligingsdoelen aanpassen. Volg deze stappen tooreach Hallo-blade met instellingen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo **Azure AD Privileged Identity Management** tegel vanuit Hallo-dashboard.
2. Selecteer **beheerd bevoorrechte rollen** > **instellingen** > **waarschuwingen instellingen**.
   
    ![Navigeer toosecurity-instellingen voor waarschuwingen][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Waarschuwing 'Rollen worden geactiveerd te vaak'
Deze waarschuwing triggers als een gebruiker activeren Hallo dezelfde bevoorrechte rol meerdere keren binnen een opgegeven periode. U kunt beide Hallo tijd periode en Hallo aantal activeringen configureren.

* **Activering vernieuwing tijdsbestek**: Geef in dagen, uren, minuten en nogmaals Hallo periode gewenste toouse tootrack verdachte vernieuwingen.
* **Aantal vernieuwingen activering**: Geef het aantal activeringen van 2 too100, waarmee u rekening houden leveringsopties waarschuwing binnen Hallo periode die u hebt gekozen Hallo. U kunt deze instelling door bewegende Hallo schuifregelaar of een getal te typen in het tekstvak Hallo wijzigen.

### <a name="there-are-too-many-global-administrators-alert"></a>'Er zijn te veel globale beheerders' waarschuwing
PIM geeft deze waarschuwing als twee verschillende criteria is voldaan en kunt u beide parameters configureren. U moet eerst een bepaalde drempelwaarde globale beheerders tooreach. Ten tweede moet een bepaald percentage van uw totale roltoewijzingen globale beheerders. Als u alleen een van deze metingen aan, weergegeven Hallo waarschuwing niet.  

* **Minimum aantal globale beheerders**: Hallo aantal globale beheerders, 2 too100, dat u rekening houden met een onveilige bedrag opgeven.
* **Percentage globale beheerders**: Geef Hallo percentage van de beheerders die hoofdbeheerders van 0% too100%, die is niet veilig in uw omgeving.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Waarschuwing 'Beheerders zijn niet met behulp van hun bevoorrechte rollen'
Deze waarschuwing wordt geactiveerd wanneer een gebruiker een bepaalde hoeveelheid tijd gaat zonder een rol activeren.

* **Aantal dagen**: Geef het aantal dagen van 0 too100, die een gebruiker kan gaan zonder te activeren van een rol Hallo.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
