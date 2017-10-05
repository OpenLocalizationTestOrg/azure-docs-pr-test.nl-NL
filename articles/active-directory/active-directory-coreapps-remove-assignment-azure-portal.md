---
title: De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory | Microsoft Docs
description: De toewijzing van de toegang van een gebruiker of groep van een enterprise-app in Azure Active Directory verwijderen
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
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="eae97-103">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eae97-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="eae97-104">Het is gemakkelijk om te verwijderen van een gebruiker of groep toegang wordt toegewezen aan een van uw zakelijke toepassingen in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eae97-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="eae97-105">U moet de juiste machtigingen voor het beheren van de app voor de onderneming hebben en u moet een globale beheerder voor de map.</span><span class="sxs-lookup"><span data-stu-id="eae97-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="eae97-106">Hoe kan ik een gebruiker of groepstoewijzing verwijderen?</span><span class="sxs-lookup"><span data-stu-id="eae97-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="eae97-107">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="eae97-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="eae97-108">Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="eae97-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="eae97-109">Op de **Azure Active Directory - *directoryname***  blade (dat wil zeggen, de Azure AD blade voor de map die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eae97-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="eae97-111">Op de **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eae97-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="eae97-112">Hier ziet u een lijst met de apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="eae97-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="eae97-113">Op de **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="eae97-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="eae97-114">Op de ***appname*** blade (dat wil zeggen, de blade met de naam van de geselecteerde app in de titel), selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="eae97-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Gebruikers of groepen selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="eae97-116">Op de ***appname*** **-gebruiker & groepstoewijzing** blade een van meer gebruikers of groepen selecteren en selecteer vervolgens de **verwijderen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="eae97-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="eae97-117">Bevestig uw beslissing bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="eae97-117">Confirm your decision at the prompt.</span></span>

    ![De opdracht Remove selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="eae97-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eae97-119">Next steps</span></span>
* [<span data-ttu-id="eae97-120">Zie al mijn groepen</span><span class="sxs-lookup"><span data-stu-id="eae97-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="eae97-121">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="eae97-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="eae97-122">Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="eae97-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="eae97-123">Wijzig de naam of het logo van een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="eae97-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
