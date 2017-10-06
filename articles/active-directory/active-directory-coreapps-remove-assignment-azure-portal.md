---
title: de toewijzing van een gebruiker of groep van een enterprise-app in Azure Active Directory aaaRemove | Microsoft Docs
description: Hoe tooremove Hallo toegang krijgen tot de toewijzing van een gebruiker of groep van een enterprise-app in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="bf512-103">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf512-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="bf512-104">Het is gemakkelijk tooremove een gebruiker of een groep toegang tooone van uw zakelijke toepassingen in Azure Active Directory (Azure AD) wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bf512-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bf512-105">U moet Hallo gemachtigd toomanage Hallo enterprise app, en moet u hoofdbeheerder voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="bf512-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="bf512-106">Hoe kan ik een gebruiker of groepstoewijzing verwijderen?</span><span class="sxs-lookup"><span data-stu-id="bf512-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="bf512-107">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="bf512-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="bf512-108">Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bf512-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="bf512-109">Op Hallo **Azure Active Directory - *directoryname***  blade (dat wil zeggen hello Azure AD blade voor Hallo-directory die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bf512-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="bf512-111">Op Hallo **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bf512-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="bf512-112">Hier ziet u een lijst met Hallo-apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="bf512-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="bf512-113">Op Hallo **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="bf512-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="bf512-114">Op Hallo ***appname*** blade (dat wil zeggen, Hallo blade met de naam van de geselecteerde app Hallo in Hallo titel Hallo), selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bf512-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Gebruikers of groepen selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="bf512-116">Op Hallo ***appname*** **-gebruiker & groepstoewijzing** blade een van meer gebruikers of groepen selecteren en selecteer vervolgens Hallo **verwijderen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="bf512-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="bf512-117">Bevestig uw beslissing Hallo een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="bf512-117">Confirm your decision at hello prompt.</span></span>

    ![De opdracht Remove Hallo selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="bf512-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf512-119">Next steps</span></span>
* [<span data-ttu-id="bf512-120">Zie al mijn groepen</span><span class="sxs-lookup"><span data-stu-id="bf512-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="bf512-121">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="bf512-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="bf512-122">Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="bf512-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="bf512-123">Hallo-naam of het logo van een enterprise-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="bf512-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
