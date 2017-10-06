---
title: een groep voor gebruikers in Azure Active Directory aaaCreate | Microsoft Docs
description: Hoe toocreate een groep in Azure Active Directory en leden toohello groep toevoegen
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="131ea-103">Een groep maken en leden toevoegen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="131ea-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="131ea-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="131ea-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="131ea-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="131ea-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="131ea-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="131ea-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="131ea-107">Dit artikel wordt uitgelegd hoe toocreate en een nieuwe groep in Azure Active Directory te vullen.</span><span class="sxs-lookup"><span data-stu-id="131ea-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="131ea-108">Een groep tooperform beheertaken, zoals het toewijzen van licenties of machtigingen tooa aantal gebruikers of apparaten tegelijkertijd gebruiken.</span><span class="sxs-lookup"><span data-stu-id="131ea-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="131ea-109">Hoe maak ik een groep?</span><span class="sxs-lookup"><span data-stu-id="131ea-109">How do I create a group?</span></span>
1. <span data-ttu-id="131ea-110">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="131ea-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="131ea-111">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="131ea-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="131ea-113">Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="131ea-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Openen Hallo groepen blade](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="131ea-115">Op Hallo **gebruikers en groepen - alle groepen** blade, selecteer Hallo **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="131ea-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Hallo Add-opdracht selecteren](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="131ea-117">Op Hallo **groep** blade een naam en beschrijving voor Hallo groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="131ea-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="131ea-118">tooselect tooadd toohello groep leden, selecteer **toegewezen** in Hallo **lidmaatschapstype** vak en selecteer vervolgens **leden**.</span><span class="sxs-lookup"><span data-stu-id="131ea-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="131ea-119">Zie voor meer informatie over hoe toomanage lidmaatschap van een groep dynamisch Hallo [met behulp van kenmerken toocreate van geavanceerde regels voor lidmaatschap](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="131ea-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Tooadd leden selecteren](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="131ea-121">Op Hallo **leden** blade, selecteert u een of meer gebruikers of apparaten tooadd toohello groep en selecteer Hallo **Selecteer** knop Hallo Hallo blade tooadd onder aan deze groep toohello.</span><span class="sxs-lookup"><span data-stu-id="131ea-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="131ea-122">Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat.</span><span class="sxs-lookup"><span data-stu-id="131ea-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="131ea-123">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="131ea-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="131ea-124">Wanneer u klaar bent met het toevoegen van leden toohello groep, selecteert u **maken** op Hallo **groep** blade.</span><span class="sxs-lookup"><span data-stu-id="131ea-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Bevestiging van de groep maken](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="131ea-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="131ea-126">Next steps</span></span>
<span data-ttu-id="131ea-127">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="131ea-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="131ea-128">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="131ea-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="131ea-129">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="131ea-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="131ea-130">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="131ea-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="131ea-131">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="131ea-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="131ea-132">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="131ea-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
