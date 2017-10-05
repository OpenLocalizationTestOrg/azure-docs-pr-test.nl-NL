---
title: Gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen | Microsoft Docs
description: Het uitschakelen van een zakelijke toepassing zodat er geen gebruikers bij deze in Azure Active Directory aanmelden kunnen
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
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="5aa47-103">Gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen</span><span class="sxs-lookup"><span data-stu-id="5aa47-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="5aa47-104">Het is gemakkelijk een zakelijke toepassing uitschakelen zodat er geen gebruikers bij deze in Azure Active Directory (Azure AD aanmelden kunnen).</span><span class="sxs-lookup"><span data-stu-id="5aa47-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5aa47-105">U moet de juiste machtigingen voor het beheren van de app voor de onderneming hebben en u moet een globale beheerder voor de map.</span><span class="sxs-lookup"><span data-stu-id="5aa47-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="5aa47-106">Hoe schakel ik gebruikersaanmelding</span><span class="sxs-lookup"><span data-stu-id="5aa47-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="5aa47-107">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="5aa47-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="5aa47-108">Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5aa47-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="5aa47-109">Op de **Azure Active Directory** -  ***directoryname*** blade (dat wil zeggen, de Azure AD blade voor de map die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5aa47-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="5aa47-111">Op de **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5aa47-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="5aa47-112">U ziet een lijst met de apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="5aa47-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="5aa47-113">Op de **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="5aa47-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="5aa47-114">Op de ***appname*** blade (dat wil zeggen, de blade met de naam van de geselecteerde app in de titel), selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5aa47-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![De opdracht Alles toepassingen selecteren](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="5aa47-116">Op de ***appname*** - **eigenschappen** blade Selecteer **Nee** voor **ingeschakeld voor gebruikers om aan te melden?**.</span><span class="sxs-lookup"><span data-stu-id="5aa47-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="5aa47-117">Selecteer de **opslaan** opdracht.</span><span class="sxs-lookup"><span data-stu-id="5aa47-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5aa47-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5aa47-118">Next steps</span></span>
* [<span data-ttu-id="5aa47-119">Mijn groepen bekijken</span><span class="sxs-lookup"><span data-stu-id="5aa47-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5aa47-120">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="5aa47-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="5aa47-121">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="5aa47-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="5aa47-122">Wijzig de naam of het logo van een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="5aa47-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
