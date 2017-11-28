---
title: Wijzig de naam of het logo van een enterprise-app in Azure Active Directory | Microsoft Docs
description: Het wijzigen van de naam of het logo voor een aangepaste enterprise-app in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="68c47-103">De naam of het logo van een enterprise-app in Azure Active Directory wijzigen</span><span class="sxs-lookup"><span data-stu-id="68c47-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="68c47-104">Het is gemakkelijk om te wijzigen van de naam of het logo voor een aangepaste toepassing in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68c47-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="68c47-105">U moet de juiste machtigingen voor u deze wijzigingen hebben en u moet de maker van de aangepaste app.</span><span class="sxs-lookup"><span data-stu-id="68c47-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="68c47-106">Hoe wijzig ik de naam of het logo een enterprise-app?</span><span class="sxs-lookup"><span data-stu-id="68c47-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="68c47-107">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="68c47-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="68c47-108">Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="68c47-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="68c47-109">Op de **Azure Active Directory - *directoryname***  blade (dat wil zeggen, de Azure AD blade voor de map die u beheert), selecteer **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="68c47-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Openen zakelijke apps](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="68c47-111">Op de **bedrijfstoepassingen** blade Selecteer **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="68c47-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="68c47-112">Hier ziet u een lijst met de apps die u kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="68c47-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="68c47-113">Op de **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.</span><span class="sxs-lookup"><span data-stu-id="68c47-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="68c47-114">Op de ***appname*** blade (dat wil zeggen, de blade met de naam van de geselecteerde app in de titel), selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="68c47-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![De opdracht Eigenschappen selecteren](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="68c47-116">Op de ***appname*** **-eigenschappen** blade, blader naar een bestand om te gebruiken als een nieuwe logo of bewerken van de app-naam of beide.</span><span class="sxs-lookup"><span data-stu-id="68c47-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Het wijzigen van de app-logo of nameproperties-opdracht](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="68c47-118">Selecteer de **opslaan** opdracht.</span><span class="sxs-lookup"><span data-stu-id="68c47-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68c47-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68c47-119">Next steps</span></span>
* [<span data-ttu-id="68c47-120">Zie al mijn groepen</span><span class="sxs-lookup"><span data-stu-id="68c47-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="68c47-121">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="68c47-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="68c47-122">De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="68c47-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="68c47-123">Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="68c47-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
