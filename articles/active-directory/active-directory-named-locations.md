---
title: aaaNamed locaties in Azure Active Directory | Microsoft Docs
description: Door te configureren met de naam locaties, kunt u voorkomen dat IP-adressen die eigendom zijn van uw organisatie valse positieven genereren voor Hallo onmogelijke reis tooatypical locaties gebeurtenistype risico.
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
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="8a116-103">Benoemde locaties in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a116-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="8a116-104">Met Hallo met de naam locaties functie van Azure Active Directory, kunt u een vertrouwde IP-adresbereiken label in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="8a116-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="8a116-105">In uw omgeving, kunt u met de naam locaties in de context van Hallo van Hallo detectie van [bestaat de kans dat gebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="8a116-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="8a116-106">Hallo functie vermindert het aantal gerapporteerde fout-positieven voor Hallo Hallo *onmogelijke reis tooatypical locaties* gebeurtenistype risico.</span><span class="sxs-lookup"><span data-stu-id="8a116-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="8a116-107">Configuratie</span><span class="sxs-lookup"><span data-stu-id="8a116-107">Configuration</span></span>

<span data-ttu-id="8a116-108">tooconfigure een benoemde locatie:</span><span class="sxs-lookup"><span data-stu-id="8a116-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="8a116-109">Meld u aan toohello [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="8a116-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="8a116-110">Klik in het linkerdeelvenster Hallo **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a116-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory-koppeling in het linkerdeelvenster Hallo](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="8a116-112">Op Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie, klikt u op **voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="8a116-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Hallo opdracht voorwaardelijke toegang](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="8a116-114">Op Hallo **voorwaardelijke toegang** blade in Hallo **beheren** sectie, klikt u op **locaties met de naam**.</span><span class="sxs-lookup"><span data-stu-id="8a116-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Hallo benoemde locaties opdracht](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="8a116-116">Op Hallo **locaties met de naam** blade, klikt u op **nieuwe locatie**.</span><span class="sxs-lookup"><span data-stu-id="8a116-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Hallo nieuwe locatie-opdracht](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="8a116-118">Op Hallo **nieuw** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a116-118">On hello **New** blade, do hello following:</span></span>

    ![Nieuwe blade Hallo](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="8a116-120">a.</span><span class="sxs-lookup"><span data-stu-id="8a116-120">a.</span></span> <span data-ttu-id="8a116-121">In Hallo **naam** typt u een naam voor uw benoemde locatie.</span><span class="sxs-lookup"><span data-stu-id="8a116-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="8a116-122">b.</span><span class="sxs-lookup"><span data-stu-id="8a116-122">b.</span></span> <span data-ttu-id="8a116-123">In Hallo **IP-adresbereiken** typt u een IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="8a116-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="8a116-124">Hallo IP-adresbereik moet toobe in Hallo *Classless Inter-Domain Routing* notatie (Classless).</span><span class="sxs-lookup"><span data-stu-id="8a116-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="8a116-125">c.</span><span class="sxs-lookup"><span data-stu-id="8a116-125">c.</span></span> <span data-ttu-id="8a116-126">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a116-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="8a116-127">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="8a116-127">What you should know</span></span>

<span data-ttu-id="8a116-128">**Bulksgewijs updates**: wanneer u maken of bijwerken van de benoemde locaties, voor bulksgewijze updates, kunt u uploaden of downloaden van een CSV-bestand met de Hallo IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="8a116-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="8a116-129">Een upload voegt Hallo IP-adresbereiken in Hallo bestandslijst toohello in plaats van het Hallo-lijst wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="8a116-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Hallo uploaden en downloaden van koppelingen](./media/active-directory-named-locations/09.png)


<span data-ttu-id="8a116-131">**Beperkingen**: U kunt maximaal 60 benoemde locaties, met één IP-bereik dat is toegewezen tooeach hiervan definiëren.</span><span class="sxs-lookup"><span data-stu-id="8a116-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="8a116-132">Als u slechts één benoemde locatie geconfigureerd hebt, kunt u geen too500 IP-bereiken definiëren voor deze.</span><span class="sxs-lookup"><span data-stu-id="8a116-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8a116-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a116-133">Next steps</span></span>

<span data-ttu-id="8a116-134">Zie toolearn meer informatie over de risico's [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="8a116-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

