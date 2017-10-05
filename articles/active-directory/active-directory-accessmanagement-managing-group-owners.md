---
title: Volgende stappen voor het toegangsbeheer van met behulp van groepen | Microsoft Docs
description: Hoe geavanceerde-aan de voor het beheren van beveiligingsgroepen en het gebruik van deze groepen voor het beheren van toegang tot een resource.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="ae2e7-103">Eigenaars voor een groep beheren</span><span class="sxs-lookup"><span data-stu-id="ae2e7-103">Managing owners for a group</span></span>
<span data-ttu-id="ae2e7-104">Wanneer een resource-eigenaar heeft toegang tot een resource aan een Azure AD-groep is toegewezen, wordt het lidmaatschap van de groep wordt beheerd door de eigenaar van de groep.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="ae2e7-105">De eigenaar van de resource delegeert effectief de machtiging gebruikers toewijzen aan de resource toe aan de eigenaar van de groep.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae2e7-106">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="ae2e7-107">Het eigendom van de groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="ae2e7-107">Assigning group ownership</span></span>
<span data-ttu-id="ae2e7-108">**Een eigenaar toevoegen aan een groep**</span><span class="sxs-lookup"><span data-stu-id="ae2e7-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="ae2e7-109">In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="ae2e7-110">Selecteer de **groepen** tabblad en open vervolgens de groep die u wilt toevoegen, eigenaren.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="ae2e7-111">Selecteer **eigenaars toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="ae2e7-112">Op de **eigenaars toevoegen** pagina, selecteert u de gebruiker die u wilt toevoegen als de eigenaar van deze groep en zorg ervoor dat deze naam wordt toegevoegd aan de **geselecteerde** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="ae2e7-113">**Een eigenaar verwijderen uit een groep**</span><span class="sxs-lookup"><span data-stu-id="ae2e7-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="ae2e7-114">In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="ae2e7-115">Selecteer de **groepen** tabblad en open vervolgens de groep die u wilt verwijderen van een eigenaar uit.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="ae2e7-116">Selecteer de **eigenaars** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="ae2e7-117">Selecteer de eigenaar die u wilt verwijderen uit deze groep en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ae2e7-118">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="ae2e7-118">Additional information</span></span>
<span data-ttu-id="ae2e7-119">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae2e7-119">These articles provide additional information on Azure Active Directory.</span></span>

* <span data-ttu-id="ae2e7-120">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)</span><span class="sxs-lookup"><span data-stu-id="ae2e7-120">[Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)</span></span>
* <span data-ttu-id="ae2e7-121">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)</span><span class="sxs-lookup"><span data-stu-id="ae2e7-121">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)</span></span>
* <span data-ttu-id="ae2e7-122">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="ae2e7-122">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="ae2e7-123">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="ae2e7-123">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="ae2e7-124">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae2e7-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
