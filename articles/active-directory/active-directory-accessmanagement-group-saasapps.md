---
title: Toegang tot SaaS-toepassingen beheren met behulp van een groep | Microsoft Docs
description: "Het gebruik van groepen in Azure Active Directory Premium of Basic toewijzen van toegang tot SaaS-toepassingen die zijn geïntegreerd met Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="5cfad-103">Een groep gebruiken om SaaS-toepassingen te beheren</span><span class="sxs-lookup"><span data-stu-id="5cfad-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="5cfad-104">Met Azure Active Directory (Azure AD) met een licentie voor Azure AD Premium of Azure AD Basic, kunt u groepen gebruiken voor het toewijzen van toegang tot een SaaS-toepassing die geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cfad-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="5cfad-105">Bijvoorbeeld, als u toegang toewijzen voor de marketingafdeling vijf verschillende SaaS-toepassingen gebruiken wilt, kunt u een groep met de gebruikers van de marketingafdeling maken en vervolgens die groep toewijzen aan deze vijf SaaS-toepassingen die nodig zijn voor de marketingafdeling.</span><span class="sxs-lookup"><span data-stu-id="5cfad-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="5cfad-106">Op deze manier kunt u tijd besparen door het lidmaatschap van de marketingafdeling op één plek beheren.</span><span class="sxs-lookup"><span data-stu-id="5cfad-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="5cfad-107">Gebruikers zijn vervolgens toegewezen aan de toepassing wanneer ze zijn toegevoegd als leden van de groep marketing en hun toewijzingen verwijderd uit de toepassing wanneer ze zijn verwijderd uit de groep marketing.</span><span class="sxs-lookup"><span data-stu-id="5cfad-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cfad-108">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="5cfad-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="5cfad-109">Deze mogelijkheid kan worden gebruikt met honderden toepassingen die u uit binnen de Azure AD-Toepassingsgalerie kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5cfad-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="5cfad-110">**Toegang voor een groep toewijzen aan een SaaS-toepassing**</span><span class="sxs-lookup"><span data-stu-id="5cfad-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="5cfad-111">In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory** op de navigatiebalk aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="5cfad-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="5cfad-112">Selecteer de **Directory** tabblad en open vervolgens de directory waarin u wilt toegang voor een groep toewijzen aan een SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5cfad-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="5cfad-113">Selecteer de **toepassingen** tabblad. Selecteer een toepassing die u hebt toegevoegd uit de galerie met toepassingen en klik vervolgens op de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5cfad-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="5cfad-114">Op de **gebruikers en groepen** tabblad, in de **vanaf** veld, voer de naam van de groep waartoe u toegang wilt toewijzen en selecteer vervolgens het vinkje in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="5cfad-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="5cfad-115">U hoeft alleen te typen van het eerste deel van naam van de groep.</span><span class="sxs-lookup"><span data-stu-id="5cfad-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="5cfad-116">Selecteer de groep en vervolgens klikt u vervolgens de **toegang toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="5cfad-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="5cfad-117">Selecteer **Ja** ziet wanneer u het bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="5cfad-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="5cfad-118">Op dit moment wordt genest groepslidmaatschap niet ondersteund voor toewijzing aan een toepassing op basis van een groep.</span><span class="sxs-lookup"><span data-stu-id="5cfad-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="5cfad-119">Ook kunt u zien welke gebruikers zijn toegewezen aan de toepassing, rechtstreeks of door het lidmaatschap in een groep.</span><span class="sxs-lookup"><span data-stu-id="5cfad-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="5cfad-120">Om dit te doen, wijzig de **vervolgkeuzelijst weergeven uit 'Groepen'** naar **'Alle gebruikers'**.</span><span class="sxs-lookup"><span data-stu-id="5cfad-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="5cfad-121">De lijst staan gebruikers in de map en of elke gebruiker is toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5cfad-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="5cfad-122">In de lijst staan ook of de toegewezen gebruikers zijn toegewezen aan rechtstreeks de toepassing (toewijzingstype weergegeven als 'Direct'), of doordat groepslidmaatschap (toewijzingstype weergegeven als 'Overgenomen'.)</span><span class="sxs-lookup"><span data-stu-id="5cfad-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="5cfad-123">Nadat u Azure AD Premium of Azure AD Basic hebt ingeschakeld, kunt u het tabblad gebruikers en groepen zien.</span><span class="sxs-lookup"><span data-stu-id="5cfad-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="5cfad-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5cfad-124">Next steps</span></span>
<span data-ttu-id="5cfad-125">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cfad-125">These articles provide additional information on Azure Active Directory.</span></span>

* <span data-ttu-id="5cfad-126">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="5cfad-126">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* <span data-ttu-id="5cfad-127">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5cfad-127">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="5cfad-128">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)</span><span class="sxs-lookup"><span data-stu-id="5cfad-128">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)</span></span>
* [<span data-ttu-id="5cfad-129">Wat is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5cfad-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="5cfad-130">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cfad-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
