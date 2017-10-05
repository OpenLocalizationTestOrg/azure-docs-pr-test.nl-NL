---
title: Nieuwe gebruikers toevoegen aan Azure Active Directory | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u nieuwe gebruikers kunt toevoegen of gebruikersinformatie kunt wijzigen in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a>Nieuwe gebruikers toevoegen aan Azure Active Directory (Engelstalig artikel)
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-users-create-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-create-users.md)
>
>

In dit artikel wordt uitgelegd hoe u nieuwe gebruikers toevoegen in uw organisatie in Azure Active Directory (Azure AD). 

1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.

   ![Openen gebruikers en groepen](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. Op de **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **toevoegen**.

   ![De opdracht Add selecteren](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. Voer details voor de gebruiker, zoals **naam** en **gebruikersnaam**. Het domeingedeelte van de naam van de gebruikersnaam moet de eerste standaarddomeinnaam domain name 'foo.onmicrosoft.com' of een geverifieerde, niet-gefedereerde domeinnaam zoals 'contoso.com'.
5. Kopieer of het wachtwoord van de gebruiker gegenereerde anders opmerking zodat u deze informatie aan de gebruiker verstrekt kunt nadat dit proces voltooid is.
6. U kunt desgewenst openen en vul de informatie in de **profiel** blade de **groepen** blade of de **functie Directory** blade voor de gebruiker. Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.
7. Op de **gebruiker** blade Selecteer **maken**.
8. Het gegenereerde wachtwoord naar de nieuwe gebruiker veilig distribueren zodat de gebruiker zich kan aanmelden.

### <a name="next-steps"></a>Volgende stappen
* [Een externe gebruiker toevoegen](active-directory-users-create-external-azure-portal.md)
* [Opnieuw instellen van het wachtwoord van een gebruiker in de nieuwe Azure portal](active-directory-users-reset-password-azure-portal.md)
* [Informatie over de werkzaamheden van een gebruiker wijzigen](active-directory-users-work-info-azure-portal.md)
* [Gebruikersprofielen beheren](active-directory-users-profile-azure-portal.md)
* [Verwijderen van een gebruiker in uw Azure AD](active-directory-users-delete-user-azure-portal.md)
* [Een gebruiker toewijzen aan een rol in uw Azure AD](active-directory-users-assign-role-azure-portal.md)
