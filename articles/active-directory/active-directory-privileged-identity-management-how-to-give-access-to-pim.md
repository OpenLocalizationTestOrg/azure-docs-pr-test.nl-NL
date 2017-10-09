---
title: aaaHow toogive toegang tooPrivileged Identity Management - Azure | Microsoft Docs
description: Meer informatie over hoe tooadd rollen toousers met Azure Active Directory Privileged Identity Management-extensie Hallo zodat ze PIM kunnen beheren.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Geeft toegang tot toomanage Azure AD Privileged Identity Management
Hallo-hoofdbeheerder die Azure AD Privileged Identity Management (PIM) voor een organisatie automatisch kunt roltoewijzingen ophalen en toegang tot tooPIM. Niemand anders opgehaald schrijftoegang standaard, met inbegrip van andere globale beheerders. Andere globale beheerders, Beveiligingsbeheerders en beveiliging lezers hebben alleen-lezentoegang tooAzure AD PIM. toogive toegang tooPIM, die de eerste gebruiker Hallo kunt toewijzen anderen toohello **beheerder met bevoorrechte rol** rol. Deze toewijzing moet worden uitgevoerd in PIM zelf en kan niet worden gewijzigd via PowerShell of andere portals.

> [!NOTE]
> Het beheren van Azure AD PIM Azure MFA is vereist. Omdat Microsoft-accounts niet voor Azure MFA registreren, kan niet een gebruiker die zich met een Microsoft-account aanmeldt toegang tot de Azure AD PIM.
> 
> 

Zorg ervoor dat er altijd ten minste twee gebruikers in een beheerdersrol bevoorrechte rol als een gebruiker is vergrendeld of hun account is verwijderd.

## <a name="give-another-user-access-toomanage-pim"></a>Geef een andere gebruiker toegang toomanage PIM
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo **Azure AD Privileged Identity Management** app op Hallo-dashboard.
2. Selecteer **bevoorrechte rollen beheren** > **beheerder met bevoorrechte rol** > **toevoegen**.
   
    ![Toevoegen van bevoorrechte rol administrators - schermafbeelding][1]
3. Stap 1 is al voltooid op Hallo toevoegen beheerde gebruikers blade. Selecteer stap 2, **Selecteer gebruikers** en de zoekcriteria voor Hallo gebruiker gewenste tooadd.
   
    ![Selecteer de gebruikers - schermafbeelding][2]
4. Selecteer Hallo gebruiker in de zoekresultaten Hallo en klik op **gedaan**.
5. Klik op **OK** toosave uw selectie. Hallo-gebruiker die u hebt geselecteerd worden weergegeven in de lijst Hallo bevoorrechte rol beheerders.
   
   * Wanneer u een nieuwe rol toosomeone toewijst, worden ze automatisch ingesteld als in aanmerking komende tooactivate Hallo rol. Als u wilt dat toomake ze permanent in de rol hello, klikt u op Hallo-gebruiker in de lijst Hallo. Selecteer **zorg toeg** in het menu van Hallo gebruiker informatie.
6. Hallo-gebruiker te een koppeling sturen[aan de slag met Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Verwijder de toegangsrechten van een andere gebruiker voor het beheren van PIM
Voordat u uit rol van Hallo bevoorrechte rol beheerder verwijderen, zorg er altijd er wordt nog steeds twee gebruikers tooit toegewezen.

1. Hallo PIM-dashboard, klik op Hallo rol **beheerder met bevoorrechte rol**.  Hallo-lijst met gebruikers in die rol momenteel wordt weergegeven.
2. Klik op het Hallo-gebruiker in de gebruikerslijst Hallo.
3. Klik op **verwijderen**.  Een bevestigingsbericht wordt weergegeven.
4. Klik op **Ja** tooremove Hallo gebruiker uit Hallo-rol.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
