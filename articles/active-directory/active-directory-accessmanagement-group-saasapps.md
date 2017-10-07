---
title: een groep toomanage toegang tooSaaS toepassingen aaaUsing | Microsoft Docs
description: "Hoe toouse groepen in Azure Active Directory Premium of Basic tooassign toegang krijgen tot tooSaaS toepassingen die zijn geïntegreerd met Azure Active Directory."
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
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="a9297-103">Met behulp van een groep toomanage access tooSaaS-toepassingen</span><span class="sxs-lookup"><span data-stu-id="a9297-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="a9297-104">Met Azure Active Directory (Azure AD) met een licentie voor Azure AD Premium of Azure AD Basic, kunt u groepen tooassign toegang tooa SaaS-toepassing die geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9297-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="a9297-105">Bijvoorbeeld, als u toegang tooassign voor Hallo marketing afdeling toouse vijf verschillende SaaS-toepassingen wilt, kunt u een groep met gebruikers in de marketingafdeling Hallo Hallo maken en wijs die groep toothese vijf SaaS-toepassingen die zijn door de marketingafdeling Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="a9297-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="a9297-106">Op deze manier kunt u tijd besparen door Hallo lidmaatschap van Hallo marketing afdeling op één plek beheren.</span><span class="sxs-lookup"><span data-stu-id="a9297-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="a9297-107">Gebruikers worden vervolgens toegewezen toohello toepassing wanneer ze zijn toegevoegd als leden van marketing groep Hallo en hun toewijzingen verwijderd van de toepassing hello wanneer ze zijn verwijderd uit de groep marketing Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9297-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9297-108">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a9297-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="a9297-109">Deze mogelijkheid kan worden gebruikt met honderden toepassingen die u uit binnen hello Azure AD-Toepassingsgalerie kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a9297-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="a9297-110">**tooassign toegang voor een groep tooa SaaS-toepassing**</span><span class="sxs-lookup"><span data-stu-id="a9297-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="a9297-111">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory** op Hallo navigatiebalk aan de linkerzijde Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9297-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="a9297-112">Selecteer Hallo **Directory** tabblad en open vervolgens Hallo map waarin u tooassign toegang voor een groep tooa SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a9297-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="a9297-113">Selecteer Hallo **toepassingen** tabblad. Selecteer een toepassing die u vanuit het Hallo-Toepassingsgalerie hebt toegevoegd en klik vervolgens op Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a9297-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="a9297-114">Op Hallo **gebruikers en groepen** tabblad in Hallo **vanaf** Hallo naam Hallo groep toowhich dat u wilt dat tooassign toegang en vervolgens selecteert vinkje in de rechterbovenhoek Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9297-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="a9297-115">U hoeft alleen tootype Hallo eerste deel van naam van de groep.</span><span class="sxs-lookup"><span data-stu-id="a9297-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="a9297-116">Hallo groep selecteert en vervolgens klikt u vervolgens Hallo **toegang toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="a9297-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="a9297-117">Selecteer **Ja** wanneer er Hallo bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="a9297-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="a9297-118">Genest groepslidmaatschap worden niet ondersteund voor toewijzing op basis van een groep tooapplications op dit moment.</span><span class="sxs-lookup"><span data-stu-id="a9297-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="a9297-119">Ook kunt u zien welke gebruikers toohello toepassing, zijn toegewezen, rechtstreeks of door het lidmaatschap in een groep.</span><span class="sxs-lookup"><span data-stu-id="a9297-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="a9297-120">toodo deze, Hallo wijziging **vervolgkeuzelijst weergeven uit 'Groepen'** te**'Alle gebruikers'**.</span><span class="sxs-lookup"><span data-stu-id="a9297-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="a9297-121">Hallo-lijst bevat de gebruikers in Hallo directory en of elke gebruiker is toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="a9297-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="a9297-122">Hallo-lijst bevat ook Hallo toegewezen gebruikers toohello toepassing rechtstreeks (toewijzingstype weergegeven als 'Direct') worden toegewezen, of doordat groepslidmaatschap (toewijzingstype weergegeven als 'Overgenomen'.)</span><span class="sxs-lookup"><span data-stu-id="a9297-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="a9297-123">U ziet Hallo gebruikers en groepen tabblad pas nadat u Azure AD Premium of Azure AD Basic hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a9297-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="a9297-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9297-124">Next steps</span></span>
<span data-ttu-id="a9297-125">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9297-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a9297-126">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="a9297-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* <span data-ttu-id="a9297-127">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="a9297-127">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="a9297-128">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)</span><span class="sxs-lookup"><span data-stu-id="a9297-128">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)</span></span>
* [<span data-ttu-id="a9297-129">Wat is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9297-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a9297-130">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9297-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
