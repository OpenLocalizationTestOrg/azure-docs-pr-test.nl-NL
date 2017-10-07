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
# <a name="manage-server-administrators"></a><span data-ttu-id="7b57c-103">Serverbeheerders beheren</span><span class="sxs-lookup"><span data-stu-id="7b57c-103">Manage server administrators</span></span>
<span data-ttu-id="7b57c-104">Serverbeheerders moet een geldige gebruiker of groep in hello Azure Active Directory (Azure AD) voor Hallo tenant in welke Hallo-server zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="7b57c-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="7b57c-105">U kunt **Analysis Services-beheerders** Hallo besturingselement blade voor uw server in Azure-portal of de eigenschappen van de Server in SSMS toomanage serverbeheerders.</span><span class="sxs-lookup"><span data-stu-id="7b57c-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="7b57c-106">Serverbeheerders tooadd met behulp van Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b57c-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="7b57c-107">Klik op Hallo besturingselementblade voor uw server **Analysis Services-beheerders**.</span><span class="sxs-lookup"><span data-stu-id="7b57c-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="7b57c-108">In Hallo  **\<servername >-Analysis Services-beheerders** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b57c-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="7b57c-109">In Hallo **serverbeheerders toevoegen** blade, selecteert u gebruikersaccounts in uw Azure AD of externe gebruikers uitnodigen door e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="7b57c-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Beheerders van de server in Azure-portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="7b57c-111">Serverbeheerders tooadd met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="7b57c-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="7b57c-112">Klik met de rechtermuisknop Hallo server > **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b57c-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="7b57c-113">In **eigenschappen van Analysis Server**, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="7b57c-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="7b57c-114">Klik op **toevoegen**, en Voer Hallo e-mailadres voor een gebruiker of groep in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b57c-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Serverbeheerders in SSMS toevoegen](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="7b57c-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b57c-116">Next steps</span></span> 
[<span data-ttu-id="7b57c-117">Verificatie en gebruikersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="7b57c-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="7b57c-118">Databaserollen en gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="7b57c-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="7b57c-119">Op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="7b57c-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

