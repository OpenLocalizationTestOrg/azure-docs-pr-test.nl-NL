---
title: uw virtuele machine biedt voor Hallo Marketplace aaaTest | Microsoft Docs
description: Begrijpen hoe tootest uw virtuele machine voor beelden hello Azure Marketplace.
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
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="4b77e-103">Testen van uw VM-aanbieding voor Azure Marketplace Hallo in fasering</span><span class="sxs-lookup"><span data-stu-id="4b77e-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="4b77e-104">Fasering betekent dat het implementeren van uw SKU in een particulier 'sandbox"waar u kunt testen en valideren van de functionaliteit ervan voordat u deze toohello Marketplace implementeert.</span><span class="sxs-lookup"><span data-stu-id="4b77e-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="4b77e-105">Hallo SKU wordt weergegeven in de faseringsmodus net zoals tooa klant die is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4b77e-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="4b77e-106">Uw VM-installatiekopie moet toostaging gecertificeerde toobe gepusht.</span><span class="sxs-lookup"><span data-stu-id="4b77e-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="4b77e-107">Stap 1: Uw aanbieding toostaging Push</span><span class="sxs-lookup"><span data-stu-id="4b77e-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="4b77e-108">Op Hallo **publiceren** tabblad **tooStaging Push**.</span><span class="sxs-lookup"><span data-stu-id="4b77e-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![tekenen](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="4b77e-110">Als Hallo Publishing Portal een melding van fouten, corrigeer deze.</span><span class="sxs-lookup"><span data-stu-id="4b77e-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="4b77e-111">In Hallo **wie toegang heeft tot uw voorbereide aanbieding?** dialoogvenster Voer Hallo lijst met Azure-abonnementen die u toopreview uw aanbieding in Hallo gebruikt [Azure preview-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b77e-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4b77e-112">In geval van virtuele Machines en oplossingssjablonen, neem **niet** geaccepteerde abonnementen van het type Cryptografieprovider DreamSpark of Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="4b77e-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="4b77e-113">In geval van virtuele Machines, als u op de knop Hallo **PUSH tooSTAGING**, Hallo stappen uit te voeren achter Hallo scene worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b77e-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="4b77e-114">U zult kunnen tooview Hallo voortgang van elke stap Hallo publiceren tabblad in Hallo portal publiceren.</span><span class="sxs-lookup"><span data-stu-id="4b77e-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="4b77e-115">U moet controleren op deze pagina op een vast interval (totdat het Hallo-status geeft tijdelijke) voor alle foutinformatie die nodig correctie van uw.</span><span class="sxs-lookup"><span data-stu-id="4b77e-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="4b77e-116">In eerste instantie gaat uw staging aanvraag toohello certificeringsinstantie team dat Hallo vhd valideren.</span><span class="sxs-lookup"><span data-stu-id="4b77e-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="4b77e-117">Echter, als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens Hallo certificeringsinstantie stap overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4b77e-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="4b77e-118">Zodra de Hallo certificeringsinstantie is voltooid, Hallo replicatie van Hallo aanbieding starten voor alle Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="4b77e-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="4b77e-119">In het algemeen neemt 24-48hours voor Hallo replicatie toocomplete maar tooa week, afhankelijk van de grootte op Hallo van Hallo vhd kan duren.</span><span class="sxs-lookup"><span data-stu-id="4b77e-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="4b77e-120">Als uw aanvraag is alleen marketing wijzigen, klikt u vervolgens is Hallo-replicatie echter sneller.</span><span class="sxs-lookup"><span data-stu-id="4b77e-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="4b77e-121">Wanneer het Hallo-replicatie is voltooid, klikt u vervolgens Hallo aanbieding is beschikbaar in Hallo [Azure-portal](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b77e-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="4b77e-122">Op dat moment Hallo status worden voorbereid in Hallo portal publiceren.</span><span class="sxs-lookup"><span data-stu-id="4b77e-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="4b77e-123">Een gefaseerde aanbieding is zichtbaar in Hallo [Azure-portal](http:/portal.azure.com) alleen met Hallo e id('s) welke Hello aanbieding gefaseerde Hallo-abonnement gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4b77e-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="4b77e-124">Meld u aan toohello [Azure preview-portal](https://portal.azure.com) met behulp van een hello Azure-abonnementen die worden vermeld in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b77e-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="4b77e-125">Zoek uw aanbieding en valideren van de VM-installatiekopie punten:</span><span class="sxs-lookup"><span data-stu-id="4b77e-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="4b77e-126">Zorg ervoor dat inhoud marketing correct in Hallo Marketplace weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4b77e-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="4b77e-127">End-to-end-implementatie van Hallo VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4b77e-127">End-to-end deployment of hello VM image.</span></span>
     
      ![IMG-kaart-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="4b77e-129">Uw aanbieding blijft in de faseringsmodus totdat u Microsoft via Hallo Publishing Portal waarschuwen [**publiceren** tabblad > Klik op de knop Hallo **"Aanvragen goedkeuring tooPush tooProduction"**] dat u klaar toopush bent tooproduction.</span><span class="sxs-lookup"><span data-stu-id="4b77e-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="4b77e-130">Dit is een ideale tijd toohave die alle leden van uw team via alles ter voorbereiding op uw aanbieding gaat van vermelde controleren.</span><span class="sxs-lookup"><span data-stu-id="4b77e-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="4b77e-131">Hallo staging-platform is ontworpen voor testen Hallo aanbieding in een preview-modus door Hallo uitgever.</span><span class="sxs-lookup"><span data-stu-id="4b77e-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="4b77e-132">We voorkomen raden dat deze platofrm gebruiken voor commerciële doeleinden.</span><span class="sxs-lookup"><span data-stu-id="4b77e-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4b77e-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b77e-133">Next steps</span></span>
<span data-ttu-id="4b77e-134">Nu uw aanbieding 'gefaseerde' en dat u de functionaliteit en marketing van inhoud hebt getest, kunt u doorgaan met de uiteindelijke publicatie toohello fase **stap 4**: [implementeren van uw aanbieding toohello Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="4b77e-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4b77e-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4b77e-135">See also</span></span>
* [<span data-ttu-id="4b77e-136">Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4b77e-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

