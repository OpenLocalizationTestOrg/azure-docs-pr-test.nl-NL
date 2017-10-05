---
title: Testen van uw VM-aanbieding voor de Marketplace | Microsoft Docs
description: Begrijpen hoe u voor het testen van uw VM-installatiekopie voor Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="21fae-103">Testen van uw VM-aanbieding voor Azure Marketplace in fasering</span><span class="sxs-lookup"><span data-stu-id="21fae-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="21fae-104">Fasering betekent dat uw SKU in een particulier 'sandbox"waar u kunt testen en valideren van de functionaliteit ervan voordat u deze implementeert in de Marketplace te implementeren.</span><span class="sxs-lookup"><span data-stu-id="21fae-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="21fae-105">De SKU wordt weergegeven in de faseringsmodus net zoals voor een klant die is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="21fae-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="21fae-106">Uw VM-installatiekopie moet worden doorgegeven voor fasering worden gecertificeerd.</span><span class="sxs-lookup"><span data-stu-id="21fae-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="21fae-107">Stap 1: Uw aanbieding voor fasering Push</span><span class="sxs-lookup"><span data-stu-id="21fae-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="21fae-108">Op de **publiceren** tabblad **Push voor fasering**.</span><span class="sxs-lookup"><span data-stu-id="21fae-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![tekenen](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="21fae-110">Als de Publishing Portal een melding van fouten, corrigeer deze.</span><span class="sxs-lookup"><span data-stu-id="21fae-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="21fae-111">In de **wie toegang heeft tot uw voorbereide aanbieding?** dialoogvenster en voer de lijst met Azure-abonnementen die u gebruiken wilt voor de preview van uw aanbieding in de [Azure preview-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21fae-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21fae-112">In geval van virtuele Machines en oplossingssjablonen, neem **niet** geaccepteerde abonnementen van het type Cryptografieprovider DreamSpark of Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="21fae-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="21fae-113">In geval van virtuele Machines, als u op de knop **PUSH FASERING**, de volgende stappen achter de scene worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="21fae-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="21fae-114">U mag de voortgang van elke stap op het tabblad publiceren weergeven bij het publiceren portal.</span><span class="sxs-lookup"><span data-stu-id="21fae-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="21fae-115">U moet controleren op deze pagina op een vast interval (totdat de status tijdelijke geeft) voor alle foutinformatie die correctie van uw nodig.</span><span class="sxs-lookup"><span data-stu-id="21fae-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="21fae-116">In eerste instantie gaat uw staging aanvraag naar het certificeringsinstantie-team dat de vhd te valideren.</span><span class="sxs-lookup"><span data-stu-id="21fae-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="21fae-117">Echter, als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens de certificeringsinstantie stap overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="21fae-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="21fae-118">Zodra de certificeringsinstantie is voltooid, start de replicatie van de aanbieding in de Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="21fae-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="21fae-119">In het algemeen neemt 24-48hours voor de replicatie is voltooid maar een week, afhankelijk van de grootte van de vhd kan duren.</span><span class="sxs-lookup"><span data-stu-id="21fae-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="21fae-120">Als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens is de replicatie echter sneller.</span><span class="sxs-lookup"><span data-stu-id="21fae-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="21fae-121">Wanneer de replicatie voltooid is, klikt u vervolgens de aanbieding is beschikbaar in de [Azure-portal](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21fae-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="21fae-122">AT die als de status in de publicatie worden voorbereid portal.</span><span class="sxs-lookup"><span data-stu-id="21fae-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="21fae-123">Een gefaseerde aanbieding is zichtbaar in de [Azure-portal](http:/portal.azure.com) alleen met behulp van de e-id('s) gekoppeld aan het abonnement waarmee de aanbieding tijdelijk worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="21fae-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="21fae-124">Aanmelden bij de [Azure preview-portal](https://portal.azure.com) via een van de Azure-abonnementen die worden vermeld in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="21fae-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="21fae-125">Zoek uw aanbieding en valideren van de VM-installatiekopie punten:</span><span class="sxs-lookup"><span data-stu-id="21fae-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="21fae-126">Zorg ervoor dat inhoud marketing correct in de Marketplace weergegeven.</span><span class="sxs-lookup"><span data-stu-id="21fae-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="21fae-127">End-to-end-implementatie van de VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="21fae-127">End-to-end deployment of the VM image.</span></span>
     
      ![IMG-kaart-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="21fae-129">Uw aanbieding blijft in de faseringsmodus totdat u Microsoft via het Publishing Portal waarschuwen [**publiceren** tabblad > Klik op de knop **'Aanvragen goedkeuring naar Push naar productie'**] bent u klaar om naar te pushen productie.</span><span class="sxs-lookup"><span data-stu-id="21fae-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="21fae-130">Dit is een ideale tijd dat alle leden van de controle van uw team via alles ter voorbereiding op uw aanbieding gaat van vermelde.</span><span class="sxs-lookup"><span data-stu-id="21fae-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="21fae-131">De test platform is ontworpen voor het testen van de aanbieding in een preview-modus door de uitgever.</span><span class="sxs-lookup"><span data-stu-id="21fae-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="21fae-132">We voorkomen raden dat deze platofrm gebruiken voor commerciële doeleinden.</span><span class="sxs-lookup"><span data-stu-id="21fae-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="21fae-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21fae-133">Next steps</span></span>
<span data-ttu-id="21fae-134">Nu dat uw aanbieding 'gefaseerde"en u de functionaliteit ervan hebt getest en marketing inhoud, kunt u doorgaan met de laatste fase van de publicatie **stap 4**: [uw aanbieding implementeren op de Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="21fae-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="21fae-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="21fae-135">See also</span></span>
* [<span data-ttu-id="21fae-136">Aan de slag: hoe een aanbieding publiceren in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="21fae-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

