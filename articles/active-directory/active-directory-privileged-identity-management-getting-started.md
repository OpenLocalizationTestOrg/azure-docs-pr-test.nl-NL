---
title: Aan de slag met Azure AD Privileged Identity Management | Microsoft Docs
description: Informatie over het beheren van bevoegde identiteiten met de Azure Active Directory Privileged Identity Management-toepassing in de Azure Portal.
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
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Aan de slag met Azure AD Privileged Identity Management
Met Azure Active Directory (AD) Privileged Identity Management kunt u toegang binnen de organisatie beheren, controleren en bewaken. Dit bereik is inclusief toegang tot resources in Azure AD en andere Microsoft-onlineservices zoals Office 365 en Microsoft Intune.

In dit artikel leest u hoe u de PIM-app van Azure AD toevoegt aan uw Azure Portal-dashboard.

## <a name="add-the-privileged-identity-management-application"></a>De Privileged Identity Management-toepassing toevoegen
Voordat u Azure AD Privileged Identity Management gebruikt, moet u de toepassing toevoegen aan uw Azure Portal-dashboard.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/) als globale beheerder van uw directory.
2. Als uw organisatie meerdere directory's heeft, selecteert u uw gebruikersnaam rechtsboven in de Azure Portal. Selecteer de map waar u PIM gaat gebruiken.
3. Selecteer **Meer services** en gebruik het tekstvak Filteren om te zoeken naar **Azure AD Privileged Identity Management**.
4. Schakel **Vastmaken aan dashboard** in en klik op de knop **Maken**. De Privileged Identity Management-toepassing wordt geopend.

Als u de eerste persoon bent die het gebruik van Azure AD Privileged Identity Management in uw map gebruikt, krijgt u automatisch de wollen **Beveiligingsbeheerder** en **Beheerder met bevoegdheid** toegewezen in de map. Alleen beheerders met bevoegdheid kunnen roltoewijzingen van gebruikers beheren. Bovendien kunt u de [beveiligingswizard](active-directory-privileged-identity-management-security-wizard.md) uitvoeren. Deze helpt u bij de eerste ervaring met detectie en toewijzing.

## <a name="navigate-to-your-tasks"></a>Navigeer naar uw taken
Nadat Azure AD Privileged Identity Management is ingesteld, ziet u de navigatieblade telkens wanneer u de toepassing opent. Gebruik deze blade om de taken voor identiteitsbeheer te voltooien.

![Taken op het hoogste niveau voor PIM - schermopname](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Mijn rollen**: hiermee gaat u naar de lijst met functies die aan u zijn toegewezen. Dit gedeelte is waar u alle functies activeert waarvoor u in aanmerking komt.
* **Aanvragen goedkeuren (preview)**: hiermee geeft u een lijst weer met openstaande activeringsaanvragen van gebruikers in uw map. [Meer informatie.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **Aanvragen in behandeling (preview)**: hiermee geeft u alle huidige aanvragen voor activering weer.
* **Toegang beoordelen**: hiermee gaat u naar eventuele in behandeling zijnde toegangsbeoordelingen die u moet voltooien, of u nu de toegang beoordeelt voor uzelf of voor iemand anders.
* **Azure AD Directory-rollen**: dit dashboard bevindt zich onder het gedeelte 'Beheren’. Hiermee kunnen beheerders met bevoorrechte rollen roltoewijzingen beheren, instellingen voor rolactivering wijzigen, toegangsbeoordelingen starten en meer. De opties in dit dashboard zijn uitgeschakeld voor iedereen die geen beheerder met een bevoorrechte rol is.

## <a name="next-steps"></a>Volgende stappen
Het [overzicht van Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) bevat meer informatie over het beheren van beheerderstoegang in uw organisatie.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
