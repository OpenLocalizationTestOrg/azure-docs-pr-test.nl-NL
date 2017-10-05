---
title: Beheerders van de server in Azure Analysis Services beheren | Microsoft Docs
description: Informatie over het beheren van server-beheerders voor een Analysis Services-server in Azure.
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="6f0ed-103">Serverbeheerders beheren</span><span class="sxs-lookup"><span data-stu-id="6f0ed-103">Manage server administrators</span></span>
<span data-ttu-id="6f0ed-104">Serverbeheerders moet een geldige gebruiker of groep in de Azure Active Directory (Azure AD) voor de tenant waarin de server zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="6f0ed-105">U kunt **Analysis Services-beheerders** in de besturingselementblade voor uw server in Azure-portal of servereigenschappen in SSMS serverbeheerders beheren.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="6f0ed-106">Serverbeheerders toevoegen met behulp van Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6f0ed-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="6f0ed-107">Klik op de besturingselementblade voor uw server **Analysis Services-beheerders**.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="6f0ed-108">In de  **\<servername >-Analysis Services-beheerders** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="6f0ed-109">In de **serverbeheerders toevoegen** blade, selecteert u gebruikersaccounts in uw Azure AD of externe gebruikers uitnodigen door e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Beheerders van de server in Azure-portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="6f0ed-111">Serverbeheerders toevoegen met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="6f0ed-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="6f0ed-112">Met de rechtermuisknop op de server > **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="6f0ed-113">In **eigenschappen van Analysis Server**, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="6f0ed-114">Klik op **toevoegen**, en voer het e-mailadres voor een gebruiker of groep in uw Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f0ed-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Serverbeheerders in SSMS toevoegen](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="6f0ed-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f0ed-116">Next steps</span></span> 
[<span data-ttu-id="6f0ed-117">Verificatie en gebruikersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="6f0ed-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="6f0ed-118">Databaserollen en gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="6f0ed-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="6f0ed-119">Op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="6f0ed-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

