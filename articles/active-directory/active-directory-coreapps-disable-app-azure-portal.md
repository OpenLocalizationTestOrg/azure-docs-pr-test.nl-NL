---
title: aaaDisable gebruikersaanmeldingen een enterprise-App in Azure Active Directory | Microsoft Docs
description: Hoe toodisable een zakelijke toepassing die geen gebruikers zich tooit in Azure Active Directory aanmelden kunnen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="98726-103">Gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen</span><span class="sxs-lookup"><span data-stu-id="98726-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="98726-104">Het is gemakkelijk toodisable een zakelijke toepassing zodat geen gebruikers zich tooit in Azure Active Directory (Azure AD aanmelden kunnen).</span><span class="sxs-lookup"><span data-stu-id="98726-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="98726-105">U moet Hallo gemachtigd toomanage Hallo enterprise app, en moet u hoofdbeheerder voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="98726-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="98726-106">Hoe schakel ik gebruikersaanmelding</span><span class="sxs-lookup"><span data-stu-id="98726-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="98726-107">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="98726-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="98726-108">Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="98726-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="98726-109">Op Hallo **Azure Active Directory** -  ***directoryname*** blade (dat wil zeggen hello Azure AD blade voor Hallo-directory die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="98726-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="98726-111">Op Hallo **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="98726-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="98726-112">U ziet een lijst met Hallo-apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="98726-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="98726-113">Op Hallo **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="98726-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="98726-114">Op Hallo ***appname*** blade (dat wil zeggen, Hallo blade met de naam van de geselecteerde app Hallo in Hallo titel Hallo), selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="98726-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Opdracht voor alle toepassingen selecteren Hallo](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="98726-116">Op Hallo ***appname*** - **eigenschappen** blade Selecteer **Nee** voor **ingeschakeld voor gebruikers toosign in?**.</span><span class="sxs-lookup"><span data-stu-id="98726-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="98726-117">Selecteer Hallo **opslaan** opdracht.</span><span class="sxs-lookup"><span data-stu-id="98726-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98726-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98726-118">Next steps</span></span>
* [<span data-ttu-id="98726-119">Mijn groepen bekijken</span><span class="sxs-lookup"><span data-stu-id="98726-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="98726-120">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="98726-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="98726-121">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="98726-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="98726-122">Hallo-naam of het logo van een enterprise-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="98726-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
