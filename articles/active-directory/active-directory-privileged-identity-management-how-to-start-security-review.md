---
title: aaaHow toostart een onderzoek toegang | Microsoft Docs
description: Meer informatie over hoe toocreate een toegang bekijken voor bevoegde identiteiten met Azure Privileged Identity Management-toepassing hello.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="1efa7-103">Hoe toostart een toegang controleren in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="1efa7-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="1efa7-104">Roltoewijzingen worden 'verouderde' wanneer gebruikers uitgebreide toegang dat ze niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1efa7-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="1efa7-105">In de volgorde tooreduce Hallo risico dat samenhangt met deze verouderde roltoewijzingen, neem bevoorrechte rol beheerders regelmatig Hallo-functies die gebruikers hebben gekregen.</span><span class="sxs-lookup"><span data-stu-id="1efa7-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="1efa7-106">Dit document bevat informatie over Hallo stappen voor het starten van een onderzoek toegang in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="1efa7-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="1efa7-107">Een revisie toegang starten</span><span class="sxs-lookup"><span data-stu-id="1efa7-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="1efa7-108">Als u dit nog niet hebt Hallo PIM toepassingendashboard tooyour toegevoegd in hello Azure-portal, Zie Hallo stappen in [aan de slag met Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="1efa7-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="1efa7-109">Hallo PIM toepassing hoofdpagina van zijn er drie manieren toostart een onderzoek toegang:</span><span class="sxs-lookup"><span data-stu-id="1efa7-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="1efa7-110">**Toegang tot beoordelingen** > **toevoegen**</span><span class="sxs-lookup"><span data-stu-id="1efa7-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="1efa7-111">**Rollen** > **revisie** knop</span><span class="sxs-lookup"><span data-stu-id="1efa7-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="1efa7-112">Selecteer Hallo specifieke rol toobe verwijderd uit de lijst van de rollen Hallo > **revisie** knop</span><span class="sxs-lookup"><span data-stu-id="1efa7-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="1efa7-113">Wanneer u klikt op op Hallo **bekijken** knop hello **een revisie toegang starten** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1efa7-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="1efa7-114">Op deze blade u bent momenteel tooconfigure Hallo controleren met een naam en tijd limiet, kiest u een rol tooreview en beslissen wie verantwoordelijk is voor Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="1efa7-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Starten van de evaluatie van een access - schermafbeelding][1]

### <a name="configure-hello-review"></a><span data-ttu-id="1efa7-116">Hallo controle configureren</span><span class="sxs-lookup"><span data-stu-id="1efa7-116">Configure hello review</span></span>
<span data-ttu-id="1efa7-117">toocreate een toegang controleren, moet u tooname deze en stel de begin- en datum.</span><span class="sxs-lookup"><span data-stu-id="1efa7-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Configureren van de evaluatie - schermafbeelding][2]

<span data-ttu-id="1efa7-119">Controleer de lengte van de Hallo Hallo bekijken lang genoeg zijn voor gebruikers toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1efa7-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="1efa7-120">Als u klaar voor de einddatum Hallo bent, kunt u Hallo controleren vroeg altijd stoppen.</span><span class="sxs-lookup"><span data-stu-id="1efa7-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="1efa7-121">Kies een tooreview rol</span><span class="sxs-lookup"><span data-stu-id="1efa7-121">Choose a role tooreview</span></span>
<span data-ttu-id="1efa7-122">Iedere evaluatie is gericht op slechts één rol.</span><span class="sxs-lookup"><span data-stu-id="1efa7-122">Each review focuses on only one role.</span></span> <span data-ttu-id="1efa7-123">Tenzij u Hallo toegang controleren vanuit een specifieke rolblade hebt gestart, moet u nu toochoose een rol.</span><span class="sxs-lookup"><span data-stu-id="1efa7-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="1efa7-124">Navigeer te**lidmaatschap van de gebruikersrol controleren**</span><span class="sxs-lookup"><span data-stu-id="1efa7-124">Navigate too**Review role membership**</span></span>
   
    ![Bekijk rollidmaatschap - schermafbeelding][3]
2. <span data-ttu-id="1efa7-126">Kies één rol uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="1efa7-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="1efa7-127">Bepalen wie verantwoordelijk is voor Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="1efa7-127">Decide who will perform hello review</span></span>
<span data-ttu-id="1efa7-128">Er zijn drie opties voor het uitvoeren van een beoordeling.</span><span class="sxs-lookup"><span data-stu-id="1efa7-128">There are three options for performing a review.</span></span> <span data-ttu-id="1efa7-129">U kunt Hallo revisie toosomeone toewijzen anders toocomplete zelf doen, of u kunt elke gebruiker die hun eigen toegang controleren.</span><span class="sxs-lookup"><span data-stu-id="1efa7-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="1efa7-130">Navigeer te**revisoren selecteren**</span><span class="sxs-lookup"><span data-stu-id="1efa7-130">Navigate too**Select reviewers**</span></span>
   
    ![Selecteer revisoren - schermafbeelding][4]
2. <span data-ttu-id="1efa7-132">Kies een van de Hallo opties:</span><span class="sxs-lookup"><span data-stu-id="1efa7-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="1efa7-133">**Selecteer revisor**: Gebruik deze optie als u niet weet die toegang nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="1efa7-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="1efa7-134">Met deze optie kunt u Hallo revisie tooa resource-eigenaar of groep manager toocomplete toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1efa7-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="1efa7-135">**Mij**: handig als u wilt dat toopreview hoe toegang werk controleert of u wilt dat tooreview namens mensen die niet kan.</span><span class="sxs-lookup"><span data-stu-id="1efa7-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="1efa7-136">**Leden lees zelf**: Gebruik deze optie toohave Hallo-evaluatie met gebruikers hun eigen roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="1efa7-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="1efa7-137">Hallo revisie starten</span><span class="sxs-lookup"><span data-stu-id="1efa7-137">Start hello review</span></span>
<span data-ttu-id="1efa7-138">U hebt ten slotte Hallo optie toorequire dat gebruikers een reden opgeven als ze hun toegang wordt goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="1efa7-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="1efa7-139">Indien gewenst een beschrijving van Hallo Lees toevoegen en selecteer **Start**.</span><span class="sxs-lookup"><span data-stu-id="1efa7-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="1efa7-140">Zorg ervoor dat u uw gebruikers weten dat er een wachten tot ze toegang-controleren en te laten laten [hoe tooperform een toegang controleren](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="1efa7-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="1efa7-141">Hallo toegang controleren beheren</span><span class="sxs-lookup"><span data-stu-id="1efa7-141">Manage hello access review</span></span>
<span data-ttu-id="1efa7-142">U kunt Hallo voortgang volgen als Hallo revisoren hun beoordelingen in hello Azure AD PIM-dashboard hebt voltooid, in Hallo toegang sectie beoordeelt.</span><span class="sxs-lookup"><span data-stu-id="1efa7-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="1efa7-143">Geen toegangsrechten worden gewijzigd in de map Hallo tot [Hallo controleren is voltooid](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="1efa7-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="1efa7-144">Totdat Hallo controleperiode afgelopen is, kunt u gebruikers toocomplete hun revisie herinneren of stop Hallo revisie vroeg tegen toegang Hallo beoordeelt sectie.</span><span class="sxs-lookup"><span data-stu-id="1efa7-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="1efa7-145">PIM inhoudsopgave</span><span class="sxs-lookup"><span data-stu-id="1efa7-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
