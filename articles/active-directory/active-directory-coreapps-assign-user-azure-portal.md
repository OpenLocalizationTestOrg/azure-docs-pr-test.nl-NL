---
title: een gebruiker of groep tooan enterprise-app in Azure Active Directory aaaAssign | Microsoft Docs
description: Hoe tooselect een enterprise-app tooassign een gebruiker of groep tooit in Azure Active Directory
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
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="c8e87-103">Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e87-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="c8e87-104">Het is gemakkelijk tooassign een gebruiker of een groep tooyour zakelijke toepassingen in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8e87-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c8e87-105">U moet Hallo gemachtigd toomanage Hallo enterprise app, en moet u hoofdbeheerder voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c8e87-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="c8e87-106">Hoe wijs ik gebruiker access tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="c8e87-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="c8e87-107">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c8e87-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c8e87-108">Selecteer **meer services**, Azure Active Directory in het tekstvak Hallo invoeren en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="c8e87-109">Op Hallo **Azure Active Directory - *directoryname***  blade (dat wil zeggen hello Azure AD blade voor Hallo-directory die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="c8e87-111">Op Hallo **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="c8e87-112">Hier ziet u een lijst met Hallo-apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="c8e87-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="c8e87-113">Op Hallo **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="c8e87-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="c8e87-114">Op Hallo ***appname*** blade (dat wil zeggen, Hallo blade met de naam van de geselecteerde app Hallo in Hallo titel Hallo), selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Opdracht voor alle toepassingen selecteren Hallo](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="c8e87-116">Op Hallo ***appname*** **-gebruiker & groepstoewijzing** blade, selecteer Hallo **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="c8e87-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="c8e87-117">Op Hallo **toevoegen toewijzing** blade Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Toewijzen van een gebruiker of groep toohello-app](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="c8e87-119">Op Hallo **gebruikers en groepen** blade, selecteer een of meer gebruikers of groepen van Hallo lijst en selecteer vervolgens Hallo **Selecteer** knop Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c8e87-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="c8e87-120">Op Hallo **toevoegen toewijzing** blade Selecteer **rol**.</span><span class="sxs-lookup"><span data-stu-id="c8e87-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="c8e87-121">Klik vervolgens op Hallo **rol selecteren** blade, selecteer een rol tooapply toohello gebruikers of groepen hebt geselecteerd, en selecteer vervolgens Hallo **OK** knop Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c8e87-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="c8e87-122">Op Hallo **toevoegen toewijzing** blade, selecteer Hallo **toewijzen** knop Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="c8e87-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="c8e87-123">Hallo toegewezen gebruikers of groepen wordt gedefinieerd door de geselecteerde rol voor deze app enterprise Hallo Hallo-machtigingen hebben.</span><span class="sxs-lookup"><span data-stu-id="c8e87-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e87-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8e87-124">Next steps</span></span>
* [<span data-ttu-id="c8e87-125">Zie al mijn groepen</span><span class="sxs-lookup"><span data-stu-id="c8e87-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c8e87-126">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="c8e87-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="c8e87-127">Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="c8e87-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="c8e87-128">Hallo-naam of het logo van een enterprise-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="c8e87-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
