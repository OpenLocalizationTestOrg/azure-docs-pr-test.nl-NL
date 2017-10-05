---
title: Een gebruiker of groep toewijzen aan een enterprise-app in Azure Active Directory | Microsoft Docs
description: Hoe u een enterprise app selecteren om een gebruiker of groep aan toewijzen in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="d3721-103">Een gebruiker of groep toewijzen aan een enterprise-app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3721-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="d3721-104">Het is gemakkelijk een gebruiker of een groep toewijzen aan uw zakelijke toepassingen in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3721-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d3721-105">U moet de juiste machtigingen voor het beheren van de app voor de onderneming hebben en u moet een globale beheerder voor de map.</span><span class="sxs-lookup"><span data-stu-id="d3721-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="d3721-106">Hoe wijs ik gebruikerstoegang naar een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d3721-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="d3721-107">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="d3721-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d3721-108">Selecteer **meer services**, Azure Active Directory invoeren in het tekstvak en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d3721-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="d3721-109">Op de **Azure Active Directory - *directoryname***  blade (dat wil zeggen, de Azure AD blade voor de map die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d3721-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="d3721-111">Op de **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d3721-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="d3721-112">Hier ziet u een lijst met de apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="d3721-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="d3721-113">Op de **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="d3721-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="d3721-114">Op de ***appname*** blade (dat wil zeggen, de blade met de naam van de geselecteerde app in de titel), selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d3721-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![De opdracht Alles toepassingen selecteren](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="d3721-116">Op de ***appname*** **-gebruiker & groepstoewijzing** blade, selecteer de **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="d3721-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="d3721-117">Op de **toevoegen toewijzing** blade Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d3721-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Een gebruiker of groep toewijzen aan de app.](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="d3721-119">Op de **gebruikers en groepen** blade gebruikers of groepen uit de lijst selecteren en selecteer vervolgens de **Selecteer** knop aan de onderkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="d3721-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="d3721-120">Op de **toevoegen toewijzing** blade Selecteer **rol**.</span><span class="sxs-lookup"><span data-stu-id="d3721-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="d3721-121">Klik op de **rol selecteren** blade, selecteert u een rol op de geselecteerde gebruikers of groepen wilt toepassen en selecteer vervolgens de **OK** knop aan de onderkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="d3721-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="d3721-122">Op de **toevoegen toewijzing** blade, selecteer de **toewijzen** knop aan de onderkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="d3721-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="d3721-123">De toegewezen gebruikers of groepen heeft de machtigingen die zijn gedefinieerd door de geselecteerde rol voor deze app voor de onderneming.</span><span class="sxs-lookup"><span data-stu-id="d3721-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3721-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3721-124">Next steps</span></span>
* [<span data-ttu-id="d3721-125">Zie al mijn groepen</span><span class="sxs-lookup"><span data-stu-id="d3721-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d3721-126">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d3721-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="d3721-127">Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d3721-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="d3721-128">Wijzig de naam of het logo van een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d3721-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
