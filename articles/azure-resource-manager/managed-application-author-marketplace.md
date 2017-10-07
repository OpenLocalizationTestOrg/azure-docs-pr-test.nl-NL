---
title: aaaAzure beheerde toepassingen in Hallo Marketplace | Microsoft Docs
description: Beschrijving van Azure beheerde toepassingen die beschikbaar via Hallo Marketplace zijn.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="7c2e3-103">Azure beheerde toepassingen in Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c2e3-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="7c2e3-104">MSPs, ISV's en systeemintegrators (SIs) kunnen gebruikmaken van Azure beheerde toepassingen toooffer hun klanten oplossingen tooall Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="7c2e3-105">Dergelijke oplossingen verminderd Hallo onderhoud en het onderhoud van de overhead voor klanten.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="7c2e3-106">Uitgevers kunnen verkopen infrastructuur- en software via Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="7c2e3-107">Deze kunnen services en toepassingen van operationele ondersteuning toomanaged koppelen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="7c2e3-108">Zie voor meer informatie [beheerde toepassingsoverzicht](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="7c2e3-109">Dit artikel wordt uitgelegd hoe een MSP, ISV of SI kunt publiceren van een toepassing toohello Marketplace, waardoor het toocustomers schaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="7c2e3-110">Vereisten voor het publiceren van een beheerde toepassing</span><span class="sxs-lookup"><span data-stu-id="7c2e3-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="7c2e3-111">Vereisten toolisting in Hallo Marketplace:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="7c2e3-112">Technische</span><span class="sxs-lookup"><span data-stu-id="7c2e3-112">Technical</span></span>

    *  <span data-ttu-id="7c2e3-113">Zie voor informatie over de basisstructuur Hallo en syntaxis van Azure Resource Manager-sjablonen, [Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="7c2e3-114">oplossingen voor tooview volledige sjabloon, Zie [Azure-snelstartsjablonen](https://azure.microsoft.com/en-us/documentation/templates/) of Hallo [Quick Start sjabloon opslagplaats](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="7c2e3-115">Zie voor meer informatie over hoe toocreate interface voor het implementeren van uw toepassing via Hallo Marketplace-klanten Hallo [definitiebestand voor de interface van een gebruiker maken](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="7c2e3-116">Niet-technische (bedrijfsvereisten)</span><span class="sxs-lookup"><span data-stu-id="7c2e3-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="7c2e3-117">Uw bedrijf of de vestiging moet zich bevinden in een land waar verkoop worden ondersteund door Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="7c2e3-118">Het product moet op een manier die compatibel is met factureringsmodellen ondersteund door Hallo Marketplace beschikken.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="7c2e3-119">U bent zelf verantwoordelijk voor het maken van de technische ondersteuning beschikbaar toocustomers in commercieel redelijke wijze.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="7c2e3-120">Hallo ondersteuning vrij, worden betaald, of via community ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="7c2e3-121">U bent zelf verantwoordelijk voor licentieverlening van uw software en eventuele afhankelijkheden software van derden.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="7c2e3-122">Inhoud die voldoet aan de criteria voor uw aanbieding toobe vermeld in de Marketplace hello en in hello Azure-portal, moet u opgeven.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="7c2e3-123">U moet akkoord gaan toohello gebruiksvoorwaarden hello Azure Marketplace deelname beleidsregels en uitgever overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="7c2e3-124">U moet akkoord gaan toocomply met gebruiksvoorwaarden hello, privacyverklaring van Microsoft en Microsoft Azure gecertificeerd programma overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="7c2e3-125">Een nieuwe aanbieding voor Azure-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="7c2e3-125">Create a new Azure application offer</span></span>

<span data-ttu-id="7c2e3-126">Wanneer u voldoet aan Hallo vereisten, bent u klaar toocreate uw aanbieding beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="7c2e3-127">U gaat nu een snel overzicht van een aanbieding en een SKU.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="7c2e3-128">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="7c2e3-128">Offer</span></span>

<span data-ttu-id="7c2e3-129">Hallo-aanbieding voor een beheerde toepassing komt overeen tooa klasse van het product aanbieden van een uitgever.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="7c2e3-130">Als u een nieuw type oplossing/toepassing die u wilt dat beschikbaar is in Hallo Marketplace toomake hebt, kunt u dit instellen als een nieuwe aanbieding.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="7c2e3-131">Een aanbieding is een verzameling van SKU's.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="7c2e3-132">Elke aanbieding wordt weergegeven als een eigen entiteit in Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="7c2e3-133">SKU</span><span class="sxs-lookup"><span data-stu-id="7c2e3-133">SKU</span></span>

<span data-ttu-id="7c2e3-134">Een SKU is Hallo kleinste over eenheid een aanbieding.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="7c2e3-135">U kunt een SKU binnen Hallo dezelfde product klasse (aanbieden) toodifferentiate tussen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="7c2e3-136">Verschillende functies die worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-136">Different features that are supported.</span></span>
* <span data-ttu-id="7c2e3-137">Hiermee wordt aangegeven of de aanbieding Hallo beheerd of onbeheerd.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="7c2e3-138">Facturering modellen die worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-138">Billing models that are supported.</span></span>

<span data-ttu-id="7c2e3-139">Een SKU wordt weergegeven onder Hallo bovenliggende aanbieding in Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="7c2e3-140">Deze wordt weergegeven als een eigen over entiteit in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="7c2e3-141">Instellen van een aanbieding</span><span class="sxs-lookup"><span data-stu-id="7c2e3-141">Set up an offer</span></span>

1. <span data-ttu-id="7c2e3-142">Meld u aan toohello [Cloud Partner-portal](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="7c2e3-143">Selecteer in het navigatievenster aan de linkerkant Hallo Hallo **+ een nieuwe aanbieding** > **Azure-toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nieuwe aanbieding](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="7c2e3-145">Hallo-formulieren die worden weergegeven op de links in Hallo Hallo invullen **Editor** weergeven.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="7c2e3-146">Verplichte velden zijn gemarkeerd met een rode asterisk (*).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Aanbieding-instellingen](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="7c2e3-148">Vier belangrijke formulieren zijn gebruikte toocreate een beheerde toepassing:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="7c2e3-149">a.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-149">a.</span></span> <span data-ttu-id="7c2e3-150">Aanbieding-instellingen</span><span class="sxs-lookup"><span data-stu-id="7c2e3-150">Offer Settings</span></span>

    <span data-ttu-id="7c2e3-151">b.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-151">b.</span></span> <span data-ttu-id="7c2e3-152">SKU 's</span><span class="sxs-lookup"><span data-stu-id="7c2e3-152">SKUs</span></span>

    <span data-ttu-id="7c2e3-153">c.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-153">c.</span></span> <span data-ttu-id="7c2e3-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c2e3-154">Marketplace</span></span>

    <span data-ttu-id="7c2e3-155">d.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-155">d.</span></span> <span data-ttu-id="7c2e3-156">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="7c2e3-156">Support</span></span>

<span data-ttu-id="7c2e3-157">Deze formulieren worden in de volgende secties Hallo uitgebreider beschreven.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="7c2e3-158">Formulier voor instellingen van aanbieding</span><span class="sxs-lookup"><span data-stu-id="7c2e3-158">Offer Settings form</span></span>
<span data-ttu-id="7c2e3-159">Gebruik deze instellingen elementaire vorm toospecify Hallo aanbieding.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="7c2e3-160">Vul Hallo **instellingen bieden** formulier.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="7c2e3-161">Hallo verschillende velden zijn:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-161">hello different fields are:</span></span>

    <span data-ttu-id="7c2e3-162">a.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-162">a.</span></span> <span data-ttu-id="7c2e3-163">**ID bieden**: deze unieke id identificeert Hallo aanbieding binnen een publisher-profiel.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="7c2e3-164">Deze ID wordt weergegeven in de product-URL's, Resource Manager-sjablonen en facturering rapporteert.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="7c2e3-165">Deze kan alleen bestaan uit alfanumerieke tekens in kleine letters of streepjes (-).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="7c2e3-166">Hallo-ID mag niet eindigen op een streepje.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="7c2e3-167">Het is beperkt tooa maximum van 50 tekens.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="7c2e3-168">Nadat een aanbieding live gaat, wordt dit veld is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="7c2e3-169">b.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-169">b.</span></span> <span data-ttu-id="7c2e3-170">**Uitgevers-ID**: Gebruik deze vervolgkeuzelijst toochoose Hallo publisher gewenste profiel toopublish deze aanbieding onder.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="7c2e3-171">Nadat een aanbieding live gaat, wordt dit veld is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="7c2e3-172">c.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-172">c.</span></span> <span data-ttu-id="7c2e3-173">**Naam**: deze weergavenaam voor uw aanbieding weergegeven in de Marketplace hello en in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="7c2e3-174">Er kunnen maximaal 50 tekens.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="7c2e3-175">Een herkenbare naam merk voor het product bevatten.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="7c2e3-176">Neem geen hier de naam van uw bedrijf tenzij hoe deze wordt gebracht.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="7c2e3-177">Als u deze aanbieding bent marketing op uw eigen website, zorg ervoor dat Hallo naam exact hoe deze wordt weergegeven op uw website.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="7c2e3-178">Selecteer **opslaan** toosave uw voortgang.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="7c2e3-179">Formulier SKU 's</span><span class="sxs-lookup"><span data-stu-id="7c2e3-179">SKUs form</span></span>
<span data-ttu-id="7c2e3-180">de volgende stap Hallo is tooadd SKU's voor uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="7c2e3-181">Selecteer **SKU's** > **nieuwe SKU**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Selecteer nieuwe SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="7c2e3-183">Voer een **SKU-ID**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="7c2e3-184">Een SKU-ID is een unieke id voor Hallo SKU binnen een aanbieding.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="7c2e3-185">Deze ID wordt weergegeven in de product-URL's, Resource Manager-sjablonen en facturering rapporteert.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="7c2e3-186">Deze kan alleen bestaan uit alfanumerieke tekens in kleine letters of streepjes (-).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="7c2e3-187">Hallo-ID mag niet eindigen op een streepje en is beperkt tooa maximum van 50 tekens.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="7c2e3-188">Nadat een aanbieding live gaat, wordt dit veld is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="7c2e3-189">U kunt meerdere SKU's binnen een aanbieding hebben.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="7c2e3-190">U moet een SKU voor elke installatiekopie u van plan bent toopublish.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="7c2e3-191">Hallo invullen **SKU Details** sectie op Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Geef nieuwe SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="7c2e3-193">Vul Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="7c2e3-194">a.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-194">a.</span></span> <span data-ttu-id="7c2e3-195">**Titel**: Voer een titel voor de SKU.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="7c2e3-196">Deze titel wordt weergegeven in de galerie Hallo voor dit item.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="7c2e3-197">b.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-197">b.</span></span> <span data-ttu-id="7c2e3-198">**Samenvatting**: Voer een korte samenvatting voor de SKU.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="7c2e3-199">Deze tekst wordt weergegeven onder Hallo titel.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="7c2e3-200">c.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-200">c.</span></span> <span data-ttu-id="7c2e3-201">**Beschrijving**: Voer een gedetailleerde beschrijving over Hallo SKU.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="7c2e3-202">d.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-202">d.</span></span> <span data-ttu-id="7c2e3-203">**SKU-Type**: Hallo toegestane waarden zijn **beheerde toepassingen** en **Oplossingssjablonen**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="7c2e3-204">Selecteer voor deze aanvraag **beheerde toepassing**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="7c2e3-205">Hallo invullen **pakketgegevens** sectie op Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Pakket](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="7c2e3-207">Vul Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="7c2e3-208">a.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-208">a.</span></span> <span data-ttu-id="7c2e3-209">**Huidige versie**: Voer een versie voor u uploaden Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="7c2e3-210">Deze moet Hallo indeling `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="7c2e3-211">b.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-211">b.</span></span> <span data-ttu-id="7c2e3-212">**Selecteer een pakketbestand**: dit pakket bevat de volgende bestanden die zijn gecomprimeerd in een ZIP-bestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="7c2e3-213">**applianceMainTemplate.json**: Hallo implementatie sjabloonbestand die toodeploy Hallo oplossing/toepassing wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="7c2e3-214">Voor informatie over het toocreate implementatie sjabloonbestanden, Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="7c2e3-215">**appliancecreateUIDefinition.json**: dit bestand wordt gebruikt door hello Azure portal toogenerate Hallo-gebruikersinterface die tooprovision deze oplossing/toepassing heeft gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="7c2e3-216">Zie voor meer informatie [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="7c2e3-217">**mainTemplate.json**: dit sjabloonbestand bevat alleen Hallo Microsoft.Solution/appliances resource.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="7c2e3-218">Hallo mainTemplate bestand bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="7c2e3-219">**type**: Gebruik **Marketplace** voor beheerde toepassingen in Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="7c2e3-220">**ManagedResourceGroupId**: deze resourcegroep in het abonnement van de klant Hallo is waarin alle Hallo resources die zijn gedefinieerd in applianceMainTemplate.json zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="7c2e3-221">**PublisherPackageId**: een unieke identificatie van deze tekenreeks Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="7c2e3-222">Geef een waarde Hallo Hallo-indeling van `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="7c2e3-223">Hallo verkrijgen **bieden ID** en **uitgevers-ID** van Hallo publiceren portal, zoals wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Aanbieding-ID](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="7c2e3-225">Hallo verkrijgen **SKU-ID**, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![SKU-ID](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="7c2e3-227">Hallo pakket verkrijgen **versie**, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Pakketversie](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="7c2e3-229">Op basis van de voorgaande voorbeelden hello, waarde van Hallo **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="7c2e3-230">Voorbeeld mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="7c2e3-231">Dit pakket bevat geen geneste sjablonen of scripts die vereist toosuccessfully zijn inrichten van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="7c2e3-232">Hallo zijn mainTemplate.json, applianceMainTemplate.json en applianceCreateUIDefinition.json bestanden aanwezig op Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="7c2e3-233">**Autorisaties**: deze eigenschap wordt gedefinieerd wie er toegang en Hallo toegangsniveau toohello resources in klanten abonnementen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="7c2e3-234">Hallo-uitgever kunt toomanage Hallo toepassing namens de klant hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="7c2e3-235">**PrincipalId**: deze eigenschap is hello Azure Active Directory (Azure AD)-ID van een gebruiker, groep of toepassing die bepaalde machtigingen op Hallo bronnen in het abonnement van de klant Hallo heeft verleend.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="7c2e3-236">Hallo roldefinitie beschrijft Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="7c2e3-237">**Roldefinitie**: deze eigenschap is een lijst met alle Hallo ingebouwde rollen gebaseerd toegangsbeheer (RBAC) rollen verstrekt door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="7c2e3-238">Hallo-rol die meest geschikte toouse toomanage Hallo bronnen namens de klant Hallo is, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="7c2e3-239">U kunt meerdere autorisaties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-239">You can add multiple authorizations.</span></span> <span data-ttu-id="7c2e3-240">Het is raadzaam dat u een AD-gebruikersgroep maken en geef de bijbehorende ID in **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="7c2e3-241">Op deze manier kunt u meer gebruikers toohello gebruikersgroep zonder Hallo nodig tooupdate Hallo SKU toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="7c2e3-242">Zie voor meer informatie over RBAC [aan de slag met RBAC in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="7c2e3-243">Formulier Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c2e3-243">Marketplace form</span></span>

<span data-ttu-id="7c2e3-244">Hallo Marketplace formulier vraagt om de velden die worden weergegeven op Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com) en op Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="7c2e3-245">Preview abonnement-id 's</span><span class="sxs-lookup"><span data-stu-id="7c2e3-245">Preview subscription IDs</span></span>

<span data-ttu-id="7c2e3-246">Geef een lijst met Azure-abonnement-id's die u toegang krijgen Hallo aanbieding tot kunt nadat deze gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="7c2e3-247">U kunt deze aanbieding abonnementen wit vermeld tootest Hallo bekeken voordat u deze maakt live.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="7c2e3-248">U kunt een witte lijst van van abonnementen in de Partnerportal Hallo too100 compileren.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="7c2e3-249">Aanbevolen categorieën</span><span class="sxs-lookup"><span data-stu-id="7c2e3-249">Suggested categories</span></span>

<span data-ttu-id="7c2e3-250">Selecteer toofive categorieën van de lijst met Hallo die uw aanbieding beste kan worden gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="7c2e3-251">Deze categorieën gebruikt toomap zijn uw aanbieding toohello productcategorieën die beschikbaar in Hallo zijn [Azure Marketplace](https://azuremarketplace.microsoft.com) en Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="7c2e3-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7c2e3-252">Azure Marketplace</span></span>

<span data-ttu-id="7c2e3-253">Samenvatting van uw beheerde toepassing Hello weergegeven Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-253">hello summary of your managed application displays hello following fields:</span></span>

![Samenvatting van Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="7c2e3-255">Hallo **overzicht** tabblad voor uw beheerde toepassing hello volgende velden worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Overzicht van Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="7c2e3-257">Hallo **plannen + prijzen** tabblad voor uw beheerde toepassing hello volgende velden worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Marketplace-abonnementen](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="7c2e3-259">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c2e3-259">Azure portal</span></span>

<span data-ttu-id="7c2e3-260">Samenvatting van uw beheerde toepassing Hello weergegeven Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-260">hello summary of your managed application displays hello following fields:</span></span>

![Portal-overzicht](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="7c2e3-262">overzicht voor de beheerde toepassing Hello weergegeven Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-262">hello overview for your managed application displays hello following fields:</span></span>

![Overzicht van de portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="7c2e3-264">Richtlijnen voor het logo</span><span class="sxs-lookup"><span data-stu-id="7c2e3-264">Logo guidelines</span></span>

<span data-ttu-id="7c2e3-265">Volg deze richtlijnen voor een logo dat u in de Cloud Partner-portal Hallo uploaden:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="7c2e3-266">Hello Azure ontwerp heeft een eenvoudige kleurenpalet.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="7c2e3-267">Hallo-nummer van primaire en secundaire kleuren op uw logo beperken.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="7c2e3-268">Hallo themakleuren van Hallo portal zijn wit en zwarte.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="7c2e3-269">Deze kleuren als achtergrondkleur Hallo niet worden gebruikt voor het logo.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="7c2e3-270">Gebruik een kleur die uw logo prominent op Hallo portal maakt.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="7c2e3-271">Het wordt aangeraden de eenvoudige primaire kleuren.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-271">We recommend simple primary colors.</span></span> <span data-ttu-id="7c2e3-272">*Als u een transparante achtergrond gebruikt, zorg ervoor dat Hallo-logo en tekst worden niet wit, zwart of blauw.*</span><span class="sxs-lookup"><span data-stu-id="7c2e3-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="7c2e3-273">Gebruik geen een kleurovergang achtergrond op Hallo-logo.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="7c2e3-274">Plaats geen tekst in het Hallo-logo, zelfs niet uw bedrijf of de naam.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="7c2e3-275">Hallo-uiterlijk van uw logo moet platte en kleurovergangen voorkomen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="7c2e3-276">Zorg ervoor dat het Hallo-logo niet is gespreid.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="7c2e3-277">Hero-logo</span><span class="sxs-lookup"><span data-stu-id="7c2e3-277">Hero logo</span></span>

<span data-ttu-id="7c2e3-278">Hallo hero logo is optioneel.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-278">hello hero logo is optional.</span></span> <span data-ttu-id="7c2e3-279">Hallo-uitgever kunt niet tooupload een hero-logo.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="7c2e3-280">Nadat Hallo hero pictogram is geüpload, kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="7c2e3-281">Op dat moment moet Hallo partner Hallo Marketplace richtlijnen voor het hero pictogrammen volgen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="7c2e3-282">Volg deze richtlijnen voor Hallo hero logo pictogram:</span><span class="sxs-lookup"><span data-stu-id="7c2e3-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="7c2e3-283">Hallo publisher weergavenaam, Hallo plan titel en Hallo aanbieding lange samenvatting worden in wit weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="7c2e3-284">Daarom niet voor de achtergrond Hallo van Hallo hero pictogram een lichte kleur te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="7c2e3-285">Een zwarte, wit of transparante achtergrond is niet toegestaan voor hero pictogrammen.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="7c2e3-286">Nadat het Hallo-aanbieding wordt weergegeven, Hallo publisher weergavenaam, Hallo plan titel, Hallo aanbieding lange samenvatting en Hallo **maken** knop programmatisch binnen Hallo hero-logo zijn ingesloten.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="7c2e3-287">Als gevolg daarvan kan niets invoert terwijl u Hallo hero logo ontwerpt.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="7c2e3-288">Laat leeg ruimte op Hallo rechts omdat tekst hello programmatisch is opgenomen in deze ruimte.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="7c2e3-289">Hallo lege ruimte voor de tekst hello moet 415 x 100 pixels op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="7c2e3-290">Er wordt met 370 pixels van Hallo links verschoven.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-290">It's offset by 370 pixels from hello left.</span></span>

    ![Voorbeeld van Hero-logo](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="7c2e3-292">Ondersteuning voor formulier</span><span class="sxs-lookup"><span data-stu-id="7c2e3-292">Support form</span></span>

<span data-ttu-id="7c2e3-293">Hallo invullen **ondersteunen** formulier met ondersteuning voor contactpersonen van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="7c2e3-294">Deze informatie kan worden engineering, contactpersonen en contactpersonen voor ondersteuning van klant.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="7c2e3-295">Een aanbieding publiceren</span><span class="sxs-lookup"><span data-stu-id="7c2e3-295">Publish an offer</span></span>

<span data-ttu-id="7c2e3-296">Nadat u alle Hallo secties invult, selecteert u **publiceren** toostart Hallo-proces waarmee uw aanbieding beschikbaar toocustomers.</span><span class="sxs-lookup"><span data-stu-id="7c2e3-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c2e3-297">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c2e3-297">Next steps</span></span>

* <span data-ttu-id="7c2e3-298">Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="7c2e3-299">Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="7c2e3-300">Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="7c2e3-301">Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="7c2e3-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
