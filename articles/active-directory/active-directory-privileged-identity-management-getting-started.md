---
title: aaaGet slag met Azure AD Privileged Identity Management | Microsoft Docs
description: Meer informatie over hoe toomanage bevoegde identiteiten met Azure Active Directory Privileged Identity Management-toepassing hello in Azure-portal.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Aan de slag met Azure AD Privileged Identity Management
Met Azure Active Directory (AD) Privileged Identity Management kunt u toegang binnen de organisatie beheren, controleren en bewaken. Dit bereik omvat toegang tooresources in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune.

In dit artikel leest u hoe tooadd hello Azure AD PIM-app tooyour Azure-portaldashboard.

## <a name="add-hello-privileged-identity-management-application"></a>Hallo Privileged Identity Management-toepassing toevoegen
Voordat u Azure AD Privileged Identity Management gebruikt, moet u tooadd Hallo toepassing tooyour Azure-portaldashboard.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) als globale beheerder van uw directory.
2. Als uw organisatie meer dan één map heeft, selecteert u uw gebruikersnaam in Hallo rechterbovenhoek Hallo Azure-portal. Selecteer waar u toouse PIM Hallo-directory.
3. Selecteer **meer services** en gebruik Hallo Filter textbox toosearch voor **Azure AD Privileged Identity Management**.
4. Controleer **pincode toodashboard** en klik vervolgens op **maken**. Hallo Privileged Identity Management-toepassing wordt geopend.

Als u bent eerste persoon toouse Azure AD Privileged Identity Management hello in uw directory, wordt u automatisch aangeduid Hallo **beveiligingsbeheerder** en **beheerder met bevoorrechte rol** rollen in de map Hallo. Alleen beheerders met bevoegdheid kunnen roltoewijzingen van gebruikers beheren. Bovendien kunt u toorun hello [beveiligingswizard.](active-directory-privileged-identity-management-security-wizard.md) die helpt u bij de initiële detectie en toewijzing ervaring Hallo.

## <a name="navigate-tooyour-tasks"></a>Navigeer tooyour taken
Nadat Azure AD Privileged Identity Management is ingesteld, ziet u Hallo navigatie blade wanneer u de toepassing hello opent. Gebruik deze blade tooaccomplish uw identiteit beheertaken.

![Taken op het hoogste niveau voor PIM - schermopname](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Mijn rollen** gaat u verder tooa lijst met rollen die tooyou zijn toegewezen. Dit gedeelte is waar u alle functies activeert waarvoor u in aanmerking komt.
* **Aanvragen goedkeuren (preview)**: hiermee geeft u een lijst weer met openstaande activeringsaanvragen van gebruikers in uw map. [Meer informatie.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **In behandeling zijnde aanvragen (Preview)** alle huidige aanvragen toohave aangebracht tooactivate wordt weergegeven.
* **Controleer toegang** vergt tooany in behandeling zijnde toegang moet u toocomplete, controleert of de beoordeling van toegang voor uzelf of naar iemand anders.
* **Azure AD-Directory-functies** zich onder de sectie 'Beheren' Hallo Hallo dashboard voor bevoorrechte rol beheerders toomanage roltoewijzingen, rol activering-wijzigingsinstellingen en start toegang beoordelingen is. Hallo-opties op dit dashboard zijn voor iedereen die een beheerder met bevoorrechte rol is niet uitgeschakeld.

## <a name="next-steps"></a>Volgende stappen
Hallo [overzicht van Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) bevat meer informatie over hoe u beheerderstoegang in uw organisatie kunt beheren.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
