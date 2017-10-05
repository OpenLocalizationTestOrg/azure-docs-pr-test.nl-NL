---
title: Met de naam locaties in Azure Active Directory | Microsoft Docs
description: Door te configureren met de naam locaties, kunt u voorkomen dat IP-adressen die eigendom zijn van uw organisatie genereren valse positieven voor de Impossible reis naar ongewone locaties risico gebeurtenistype.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="a7ff4-103">Benoemde locaties in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7ff4-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="a7ff4-104">Met de functie benoemde locaties van Azure Active Directory kunt u een vertrouwde IP-adresbereiken in uw organisaties label.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="a7ff4-105">In uw omgeving, kunt u met de naam locaties in de context van de detectie van [bestaat de kans dat gebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="a7ff4-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="a7ff4-106">De functie vermindert het aantal gerapporteerde fout-positieven voor de *Impossible op reis naar ongewone locaties* gebeurtenistype risico.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="a7ff4-107">Configuratie</span><span class="sxs-lookup"><span data-stu-id="a7ff4-107">Configuration</span></span>

<span data-ttu-id="a7ff4-108">Voor het configureren van een benoemde locatie:</span><span class="sxs-lookup"><span data-stu-id="a7ff4-108">To configure a named location:</span></span>

1. <span data-ttu-id="a7ff4-109">Aanmelden bij de [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="a7ff4-110">Klik in het linkerdeelvenster op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![De Azure Active Directory-koppeling in het linkerdeelvenster](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="a7ff4-112">Op de **Azure Active Directory** blade in de **beveiliging** sectie, klikt u op **voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![De opdracht voorwaardelijke toegang](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="a7ff4-114">Op de **voorwaardelijke toegang** blade in de **beheren** sectie, klikt u op **locaties met de naam**.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![De benoemde locaties-opdracht](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="a7ff4-116">Op de **locaties met de naam** blade, klikt u op **nieuwe locatie**.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-116">On the **Named locations** blade, click **New location**.</span></span>

    ![De nieuwe locatie-opdracht](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="a7ff4-118">Op de **nieuw** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a7ff4-118">On the **New** blade, do the following:</span></span>

    ![De nieuwe blade](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="a7ff4-120">a.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-120">a.</span></span> <span data-ttu-id="a7ff4-121">In de **naam** typt u een naam voor uw benoemde locatie.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="a7ff4-122">b.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-122">b.</span></span> <span data-ttu-id="a7ff4-123">In de **IP-adresbereiken** typt u een IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="a7ff4-124">De IP-adresbereik moet zich in de *Classless Inter-Domain Routing* notatie (Classless).</span><span class="sxs-lookup"><span data-stu-id="a7ff4-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="a7ff4-125">c.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-125">c.</span></span> <span data-ttu-id="a7ff4-126">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="a7ff4-127">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="a7ff4-127">What you should know</span></span>

<span data-ttu-id="a7ff4-128">**Bulksgewijs updates**: wanneer u maken of bijwerken van de benoemde locaties, voor bulksgewijze updates, kunt u uploaden of downloaden van een CSV-bestand met de IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="a7ff4-129">Een upload wordt het IP-adresbereiken in het bestand toegevoegd aan de lijst in plaats van de lijst wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![De koppelingen uploaden en downloaden](./media/active-directory-named-locations/09.png)


<span data-ttu-id="a7ff4-131">**Beperkingen**: U kunt maximaal 60 benoemde locaties, met één IP-bereik dat is toegewezen aan elk van deze definiëren.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="a7ff4-132">Als u slechts één benoemde locatie geconfigureerd hebt, kunt u maximaal 500 IP-adresbereiken voor definiëren.</span><span class="sxs-lookup"><span data-stu-id="a7ff4-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7ff4-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7ff4-133">Next steps</span></span>

<span data-ttu-id="a7ff4-134">Zie voor meer informatie over de risico's, [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="a7ff4-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

