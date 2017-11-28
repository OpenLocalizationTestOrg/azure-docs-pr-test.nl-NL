---
title: Het uitvoeren van een onderzoek toegang | Microsoft Docs
description: Nadat u een revisie toegang in Azure AD Privileged Identity Management gestart, informatie over het voltooien en de resultaten bekijken
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="931bf-103">Het uitvoeren van een revisie toegang in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="931bf-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="931bf-104">Bevoorrechte rol beheerders kunnen bekijken voor bevoorrechte toegang eenmaal een [beveiligingsbeoordeling is gestart](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="931bf-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="931bf-105">Azure AD Privileged Identity Management (PIM) stuurt automatisch een e-mailbericht gebruikers om te controleren van de toegang te vragen.</span><span class="sxs-lookup"><span data-stu-id="931bf-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="931bf-106">Als een gebruiker niet een e-mailbericht ontvangt is, kunt u ze de instructies in verzenden [het uitvoeren van een beveiligingsbeoordeling](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="931bf-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="931bf-107">Nadat de periode van beveiliging controleren of alle gebruikers klaar bent met hun eigen bekijken, de stappen in dit artikel voor het beheren van de controle en de resultaten te zien.</span><span class="sxs-lookup"><span data-stu-id="931bf-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="931bf-108">Beoordelingen van beveiliging beheren</span><span class="sxs-lookup"><span data-stu-id="931bf-108">Manage security reviews</span></span>
1. <span data-ttu-id="931bf-109">Ga naar de [Azure-portal](https://portal.azure.com/) en selecteer de **Azure AD Privileged Identity Management** toepassing op uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="931bf-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="931bf-110">Selecteer de **toegang tot beoordelingen** sectie van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="931bf-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="931bf-111">Selecteer de controle van toegang dat u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="931bf-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="931bf-112">Op de toegang-revisie detail blade zijn er een aantal opties voor het beheren van deze evaluatie.</span><span class="sxs-lookup"><span data-stu-id="931bf-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![PIM toegang controleren knoppen - schermafbeelding][1]

### <a name="remind"></a><span data-ttu-id="931bf-114">Herinneren</span><span class="sxs-lookup"><span data-stu-id="931bf-114">Remind</span></span>
<span data-ttu-id="931bf-115">Als een onderzoek toegang is ingesteld, zodat de gebruikers zelf, Controleer de **herinnering sturen** knop verstuurt een melding.</span><span class="sxs-lookup"><span data-stu-id="931bf-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="931bf-116">Stoppen</span><span class="sxs-lookup"><span data-stu-id="931bf-116">Stop</span></span>
<span data-ttu-id="931bf-117">Alle beoordelingen van toegang tot een einddatum hebben, maar u kunt de **stoppen** knop vroeg voltooid.</span><span class="sxs-lookup"><span data-stu-id="931bf-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="931bf-118">Als gebruikers zich nog niet op dit tijdstip zijn gecontroleerd, ze niet mogelijk om te na het stoppen van de controle.</span><span class="sxs-lookup"><span data-stu-id="931bf-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="931bf-119">U kunt een beoordeling niet opnieuw starten nadat deze gestopt.</span><span class="sxs-lookup"><span data-stu-id="931bf-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="931bf-120">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="931bf-120">Apply</span></span>
<span data-ttu-id="931bf-121">Nadat een revisie access is voltooid, omdat u de einddatum is bereikt of handmatig gestopt omdat de **toepassen** knop implementeert de uitkomst van de evaluatie.</span><span class="sxs-lookup"><span data-stu-id="931bf-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="931bf-122">Als een gebruiker toegang is geweigerd in de evaluatie, is dit de stap die hun roltoewijzing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="931bf-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="931bf-123">Exporteren</span><span class="sxs-lookup"><span data-stu-id="931bf-123">Export</span></span>
<span data-ttu-id="931bf-124">Als u de resultaten van de beveiligingsbeoordeling handmatig toepassen wilt, kunt u de controle exporteren.</span><span class="sxs-lookup"><span data-stu-id="931bf-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="931bf-125">De **exporteren** knop downloaden van een CSV-bestand wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="931bf-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="931bf-126">U kunt de resultaten in Excel of andere programma's die CSV-bestanden beheren.</span><span class="sxs-lookup"><span data-stu-id="931bf-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="931bf-127">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="931bf-127">Delete</span></span>
<span data-ttu-id="931bf-128">Als u niet geïnteresseerd in de revisie verdere bent, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="931bf-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="931bf-129">De **verwijderen** knop verwijdert u de controle van de PIM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="931bf-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="931bf-130">U wordt niet ophalen van een waarschuwing alvorens deze wordt verwijderd, dus wees zeker dat u wilt verwijderen van deze evaluatie.</span><span class="sxs-lookup"><span data-stu-id="931bf-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="931bf-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="931bf-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
