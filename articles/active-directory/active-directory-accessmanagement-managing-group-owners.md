---
title: aaaNext stappen voor het toegangsbeheer van met behulp van groepen | Microsoft Docs
description: Hoe geavanceerde-aan de voor het beheren van beveiligingsgroepen en hoe toouse deze groepen toomanage toegang tooa resource.
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="3143f-103">Eigenaars voor een groep beheren</span><span class="sxs-lookup"><span data-stu-id="3143f-103">Managing owners for a group</span></span>
<span data-ttu-id="3143f-104">Wanneer een resource-eigenaar heeft toegang tot tooa resource tooan Azure AD-groep is toegewezen, worden Hallo lidmaatschap van groep Hallo wordt beheerd door de Groepseigenaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="3143f-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="3143f-105">de resource-eigenaar Hallo delegeert effectief Hallo machtiging tooassign gebruikers toohello resource toohello eigenaar van de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="3143f-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3143f-106">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3143f-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="3143f-107">Het eigendom van de groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="3143f-107">Assigning group ownership</span></span>
<span data-ttu-id="3143f-108">**een groep eigenaar tooa tooadd**</span><span class="sxs-lookup"><span data-stu-id="3143f-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="3143f-109">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3143f-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="3143f-110">Selecteer Hallo **groepen** tabblad en open vervolgens Hallo-groep die u wilt dat de eigenaren van tooadd.</span><span class="sxs-lookup"><span data-stu-id="3143f-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="3143f-111">Selecteer **eigenaars toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3143f-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="3143f-112">Op Hallo **eigenaars toevoegen** pagina, selecteer Hallo gebruiker tooadd als Hallo eigenaar van deze groep wilt gebruiken en zorg ervoor dat de naam wordt toegevoegd toohello **geselecteerde** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="3143f-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="3143f-113">**tooremove een eigenaar van een groep**</span><span class="sxs-lookup"><span data-stu-id="3143f-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="3143f-114">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3143f-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="3143f-115">Selecteer Hallo **groepen** tabblad en open vervolgens Hallo groep die u wilt tooremove een eigenaar uit.</span><span class="sxs-lookup"><span data-stu-id="3143f-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="3143f-116">Selecteer Hallo **eigenaars** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3143f-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="3143f-117">Selecteer Hallo eigenaar wilt tooremove uit deze groep en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3143f-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="3143f-118">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="3143f-118">Additional information</span></span>
<span data-ttu-id="3143f-119">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3143f-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="3143f-120">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="3143f-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* <span data-ttu-id="3143f-121">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)</span><span class="sxs-lookup"><span data-stu-id="3143f-121">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)</span></span>
* <span data-ttu-id="3143f-122">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="3143f-122">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="3143f-123">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="3143f-123">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="3143f-124">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3143f-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
