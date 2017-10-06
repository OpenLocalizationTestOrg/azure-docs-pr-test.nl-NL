---
title: aaaHow tooadd of een gebruikersrol verwijderen | Microsoft Docs
description: Meer informatie over hoe tooadd rollen tooprivileged identiteiten met Azure Active Directory Privileged Identity Management-toepassing hello.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Hoe tooadd of een gebruikersrol verwijderen
Met Azure Active Directory (AD), een algemeen beheerder (of bedrijfsbeheerder) kunt bijwerken die gebruikers **permanent** tooroles toegewezen in Azure AD. Dit wordt gedaan met PowerShell-cmdlets, zoals `Add-MsolRoleMember` en `Remove-MsolRoleMember`. Of ze Hallo klassieke Azure-portal kunnen gebruiken, zoals beschreven in [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management-toepassing Hello beheerders bevoorrechte rol toomake permanente roltoewijzingen, evenals. Bovendien bevoorrechte rol administrators gebruikers kunnen aanbrengen **in aanmerking komende** voor beheerdersrollen. Een in aanmerking komende beheerder kunt Hallo rol activeren wanneer nodig en vervolgens hun machtigingen verlopen zodra ze klaar bent.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Rollen met PIM in hello Azure-portal beheren
In uw organisatie, kunt u gebruikers toewijzen toodifferent beheerdersrollen in Azure AD, Office 365 en andere Microsoft-services en toepassingen.  Meer informatie over de beschikbare rollen Hallo kunnen worden gevonden op [rollen in Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd of verwijderen van een gebruiker een rol met Privileged Identity Management online zetten van de Hallo PIM-dashboard. Vervolgens klikt u op Hallo **gebruikers in beheerdersrollen** knop of Selecteer een specifieke rol (zoals hoofdbeheerder) Hallo rollen tabel.

> [!NOTE]
> Als u nog PIM in hello Azure-portal nog niet hebt ingeschakeld, gaat u verder te[aan de slag met Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) voor meer informatie.

Als u een andere gebruiker toegang tooPIM zelf Hallo rollen waarvoor u PIM Hallo gebruiker toohave worden beschreven verder in toogive wilt [hoe toogive toegang krijgen tot tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Een gebruikersrol tooa toevoegen
1. In Hallo [Azure-portal](https://portal.azure.com/), selecteer Hallo **Azure AD Privileged Identity Management** tegel op Hallo-dashboard.
2. Selecteer **bevoorrechte rollen beheren**.
3. In Hallo **Overzicht rollen** tabel, de gewenste toomanage Selecteer Hallo-rol.
4. Selecteer Hallo rol Blade **toevoegen**.
5. Klik op **Selecteer gebruikers** en zoek naar de gebruiker Hallo op Hallo **Selecteer gebruikers** blade.  
6. Selecteer Hallo gebruiker in de lijst met zoekresultaten Hallo en klik op **gedaan**.
7. Klik op **OK** toosave uw selectie. Hallo-gebruiker die u hebt geselecteerd worden weergegeven in de lijst Hallo als in aanmerking komen voor Hallo-rol.

> [!NOTE]
> Er zijn alleen nieuwe gebruikers met een rol in aanmerking komen voor de rol Hallo standaard. Als u toomake Hallo functie permanent wilt, klikt u op gebruiker in de lijst Hallo Hallo. Hallo gebruikersgegevens wordt weergegeven in een nieuwe blade. Selecteer **zorg toeg** in het menu van Hallo gebruiker informatie.  
> Als een gebruiker niet voor Azure multi-factor Authentication (MFA registreren kan) of met behulp van een Microsoft-account (meestal @outlook.com), moet u toomake ze in alle hun rollen permanent. Tijdens de activering gevraagd in aanmerking komende admins tooregister voor MFA.

Nu dat de gebruiker is hello in aanmerking komen voor een rol, laten weten dat ze kunnen worden geactiveerd volgens de instructies in toohello [hoe tooactivate een rol of deactiveren](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Een gebruiker vanuit een functie verwijderen
U kunt gebruikers van in aanmerking komende roltoewijzingen verwijderen, maar zorg ervoor dat er altijd ten minste één gebruiker aan wie een permanente globale beheerder.

Volg deze stappen tooremove een specifieke gebruiker uit een rol:

1. Toohello rol in de lijst van de functie Hallo navigeren door het selecteren van een rol in Azure AD PIM-dashboard Hallo of door te klikken op Hallo **gebruikers in beheerdersrollen** knop.
2. Klik op het Hallo-gebruiker in de gebruikerslijst Hallo.
3. Klik op **verwijderen**. Een bericht wordt u gevraagd tooconfirm.
4. Klik op **Ja** tooremove Hallo rol van Hallo-gebruiker.

Als u niet zeker weet welke gebruikers moeten nog steeds hun roltoewijzingen, dan u kunt [een revisie toegang voor Hallo rol starten](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

