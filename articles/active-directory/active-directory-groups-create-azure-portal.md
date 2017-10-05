---
title: Maakt een groep voor gebruikers in Azure Active Directory | Microsoft Docs
description: Het maken van een groep in Azure Active Directory en leden toevoegen aan de groep
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="4776e-103">Een groep maken en leden toevoegen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4776e-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4776e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4776e-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="4776e-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4776e-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="4776e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4776e-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="4776e-107">In dit artikel wordt uitgelegd hoe u maakt en vult een nieuwe groep in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4776e-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="4776e-108">Een groep gebruiken voor beheertaken uitvoert zoals het toewijzen van licenties of machtigingen voor een aantal gebruikers of apparaten in één keer.</span><span class="sxs-lookup"><span data-stu-id="4776e-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="4776e-109">Hoe maak ik een groep?</span><span class="sxs-lookup"><span data-stu-id="4776e-109">How do I create a group?</span></span>
1. <span data-ttu-id="4776e-110">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="4776e-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4776e-111">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4776e-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="4776e-113">Op de **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="4776e-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![De blade groepen openen](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="4776e-115">Op de **gebruikers en groepen - alle groepen** blade, selecteer de **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="4776e-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![De opdracht Add selecteren](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="4776e-117">Op de **groep** blade een naam en beschrijving voor de groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4776e-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="4776e-118">Als u wilt leden toevoegen aan de groep selecteert, selecteert u **toegewezen** in de **lidmaatschapstype** vak en selecteer vervolgens **leden**.</span><span class="sxs-lookup"><span data-stu-id="4776e-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="4776e-119">Zie voor meer informatie over het beheren van het lidmaatschap van een groep dynamisch [kenmerken gebruiken voor het maken van geavanceerde regels voor lidmaatschap](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4776e-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Leden toevoegen selecteren](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="4776e-121">Op de **leden** blade, selecteer een of meer gebruikers of apparaten aan de groep wilt toevoegen en selecteer de **Selecteer** knop aan de onderkant van de blade aan toe te voegen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="4776e-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="4776e-122">De **gebruiker** vak gefilterd op basis van overeenkomst van uw invoer voor een deel van de naam van een gebruiker of het apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4776e-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="4776e-123">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="4776e-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="4776e-124">Wanneer u klaar bent met het toevoegen van leden aan de groep, selecteert u **maken** op de **groep** blade.</span><span class="sxs-lookup"><span data-stu-id="4776e-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Bevestiging van de groep maken](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="4776e-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4776e-126">Next steps</span></span>
<span data-ttu-id="4776e-127">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4776e-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4776e-128">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="4776e-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4776e-129">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4776e-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="4776e-130">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4776e-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="4776e-131">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4776e-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="4776e-132">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4776e-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
