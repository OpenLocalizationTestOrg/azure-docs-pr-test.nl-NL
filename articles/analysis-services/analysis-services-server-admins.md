---
title: aaaManage server beheerders in Azure Analysis Services | Microsoft Docs
description: Meer informatie over hoe toomanage server-beheerders voor een Analysis Services-server in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>Serverbeheerders beheren
Serverbeheerders moet een geldige gebruiker of groep in hello Azure Active Directory (Azure AD) voor Hallo tenant in welke Hallo-server zich bevindt. U kunt **Analysis Services-beheerders** Hallo besturingselement blade voor uw server in Azure-portal of de eigenschappen van de Server in SSMS toomanage serverbeheerders. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>Serverbeheerders tooadd met behulp van Azure portal
1. Klik op Hallo besturingselementblade voor uw server **Analysis Services-beheerders**.
2. In Hallo  **\<servername >-Analysis Services-beheerders** blade, klikt u op **toevoegen**.
3. In Hallo **serverbeheerders toevoegen** blade, selecteert u gebruikersaccounts in uw Azure AD of externe gebruikers uitnodigen door e-mailadres.

    ![Beheerders van de server in Azure-portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>Serverbeheerders tooadd met behulp van SSMS
1. Klik met de rechtermuisknop Hallo server > **eigenschappen**.
2. In **eigenschappen van Analysis Server**, klikt u op **beveiliging**.
3. Klik op **toevoegen**, en Voer Hallo e-mailadres voor een gebruiker of groep in uw Azure AD.
   
    ![Serverbeheerders in SSMS toevoegen](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Volgende stappen 
[Verificatie en gebruikersmachtigingen](analysis-services-manage-users.md)  
[Databaserollen en gebruikers beheren](analysis-services-database-users.md)  
[Op rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-what-is.md)  

