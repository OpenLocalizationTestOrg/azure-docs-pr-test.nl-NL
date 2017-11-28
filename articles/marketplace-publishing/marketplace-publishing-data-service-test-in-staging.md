---
title: Testen van uw Data-Service-aanbieding voor de Marketplace | Microsoft Docs
description: Begrijpen hoe u voor het testen van uw Data-Service-aanbieding voor Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="99ab6-103">Testen van uw Data-Service-aanbieding in fasering</span><span class="sxs-lookup"><span data-stu-id="99ab6-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="99ab6-104">**Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.**</span><span class="sxs-lookup"><span data-stu-id="99ab6-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="99ab6-105">Als u een SaaS business-toepassing die u wilt publiceren op AppSource hebt u meer informatie vindt [hier](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="99ab6-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="99ab6-106">Als u beschikt over een IaaS-toepassingen of developer-service die u wilt publiceren op Azure Marketplace u meer informatie vindt [hier](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="99ab6-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="99ab6-107">Na het voltooien van de eerste twee stappen van [maken van uw account Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) en [maken van uw gegevens Service bieden in Publishing Portal](marketplace-publishing-data-service-creation.md) u klaar bent om uw aanbieding beschikbaar zijn in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="99ab6-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="99ab6-108">In dit onderwerp helpt u bij de eerste, tussenliggende, naam 'Staging' stap</span><span class="sxs-lookup"><span data-stu-id="99ab6-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="99ab6-109">Fasering betekent het implementeren van uw aanbieding in een particulier 'sandbox"waar u kunt testen en de functionaliteit ervan controleren voordat u deze naar productie.</span><span class="sxs-lookup"><span data-stu-id="99ab6-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="99ab6-110">De aanbieding wordt weergegeven in de faseringsmodus net zoals voor een klant die is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="99ab6-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="99ab6-111">Step 1.</span><span class="sxs-lookup"><span data-stu-id="99ab6-111">Step 1.</span></span> <span data-ttu-id="99ab6-112">Uw aanbieding voor fasering pushen</span><span class="sxs-lookup"><span data-stu-id="99ab6-112">Pushing your offer to staging</span></span>
<span data-ttu-id="99ab6-113">Uw aanbieding voor fasering pushen, kunt u de aanbieding te testen voordat deze beschikbaar voor toekomstige abonnees.</span><span class="sxs-lookup"><span data-stu-id="99ab6-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="99ab6-114">U kunt zien hoe uw aanbieding wordt weergegeven en werken voor degenen abonneren op uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="99ab6-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="99ab6-116">Aanmelden bij de [Portal publiceren](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="99ab6-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="99ab6-117">Selecteer **Data Services** in het venster linkernavigatiegedeelte</span><span class="sxs-lookup"><span data-stu-id="99ab6-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="99ab6-118">Selecteer uw aanbieding die u wilt pushen voor fasering.</span><span class="sxs-lookup"><span data-stu-id="99ab6-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="99ab6-119">Hier ziet u de bovenstaande scherm.</span><span class="sxs-lookup"><span data-stu-id="99ab6-119">You will see the above screen.</span></span>
4. <span data-ttu-id="99ab6-120">Klik op **Push fasering** knop.</span><span class="sxs-lookup"><span data-stu-id="99ab6-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="99ab6-121">Als er problemen met de aanbieding die worden voltooid zijn moeten voordat het pushen voor fasering, ziet u een lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="99ab6-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="99ab6-122">Corrigeer deze items door te klikken op elk item in de lijst.</span><span class="sxs-lookup"><span data-stu-id="99ab6-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="99ab6-123">Wanneer alle correcties zijn aangebracht, klikt u op **Push voor fasering** knop opnieuw.</span><span class="sxs-lookup"><span data-stu-id="99ab6-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="99ab6-124">Als er geen problemen met uw aanbieding zijn ziet u het onderstaande pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="99ab6-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="99ab6-125">Als u bent niet plannen/niet goedgekeurd voor uw aanbieding in Azure Portal surface (momenteel heeft beperkte capaciteit), sluit u alleen het pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="99ab6-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="99ab6-126">Test uw Data-Service in Azure Portal (in aanvulling op de portal DataMarket), moet u een Azure-abonnements-ID om mee te testen.</span><span class="sxs-lookup"><span data-stu-id="99ab6-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="99ab6-127">Dit abonnement-ID wordt de account die is toegestaan voor het testen van uw aanbieding identificeren.</span><span class="sxs-lookup"><span data-stu-id="99ab6-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="99ab6-128">Knippen en plakken van uw abonnements-ID en klik op het vinkje om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="99ab6-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="99ab6-130">Deze id Azure-abonnementen zijn alleen vereist voor het testen en fasering in de [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99ab6-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="99ab6-131">Ze zijn niet vereist om te testen in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="99ab6-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="99ab6-132">Het volgende scherm wordt weergegeven ziet publicatie is plaatsvinden door het pictogram 'wordt uitgevoerd' weer te geven dat hieronder geel gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="99ab6-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="99ab6-133">Pushen voor fasering duurt tussen 10 tot 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="99ab6-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="99ab6-134">Als het duurt langer, moet u eerst uw browser (druk op F5 in Internet Explorer) vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="99ab6-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="99ab6-135">Klik op de koppeling naar contact in het zeldzame gevallen waarin uw aanbieding nog steeds wordt gepusht voor fasering na een uur, laat ons weten dat er een probleem is.</span><span class="sxs-lookup"><span data-stu-id="99ab6-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="99ab6-137">Wanneer de Staging-Push het pictogram 'wordt uitgevoerd' is voltooid wordt stop verplaatsen en de status wordt bijgewerkt naar 'Tijdelijke'.</span><span class="sxs-lookup"><span data-stu-id="99ab6-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="99ab6-138">U bent nu klaar voor het testen van uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="99ab6-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="99ab6-139">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="99ab6-139">Step 2.</span></span> <span data-ttu-id="99ab6-140">Testen van uw voorbereide aanbieding in DataMarket</span><span class="sxs-lookup"><span data-stu-id="99ab6-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="99ab6-141">Klik op de koppeling die na de tekst **' Zie uw service bieden op... '**</span><span class="sxs-lookup"><span data-stu-id="99ab6-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="99ab6-142">om weer te geven in het scherm dat de abonnee ziet wanneer uw aanbieding overschakelt naar de productie en in DataMarket wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="99ab6-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="99ab6-144">Testen of Controleer of elk van de 12 items gemarkeerd hierboven om te controleren of alle logo's, prijzen/transacties, tekst, afbeeldingen, documentatie en koppelingen correct zijn en werken goed.</span><span class="sxs-lookup"><span data-stu-id="99ab6-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="99ab6-145">Dit is een goed moment om te controleren of een testwaarden die u hebt ingevoerd bij het maken van uw aanbieding zijn vervangen door feitelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="99ab6-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="99ab6-146">Aanbieding-logo</span><span class="sxs-lookup"><span data-stu-id="99ab6-146">Offer logo</span></span>
2. <span data-ttu-id="99ab6-147">De aanbiedingsnaam van de</span><span class="sxs-lookup"><span data-stu-id="99ab6-147">Offer name</span></span>
3. <span data-ttu-id="99ab6-148">Publisher naam/koppeling naar de website van uw bedrijf</span><span class="sxs-lookup"><span data-stu-id="99ab6-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="99ab6-149">Categorieën voor uw aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-149">Search categories for your offer</span></span>
5. <span data-ttu-id="99ab6-150">Uw aanbieding ondersteuning koppeling om te helpen abonnees</span><span class="sxs-lookup"><span data-stu-id="99ab6-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="99ab6-151">Contextafhankelijke beschrijving voor uw aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="99ab6-152">Plan factureringsgegevens van aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="99ab6-153">Koppelen aan implementatiecode</span><span class="sxs-lookup"><span data-stu-id="99ab6-153">Link to implementation code</span></span>
9. <span data-ttu-id="99ab6-154">Voorbeeld-installatiekopieën die aangeven gebruiken van gegevens van aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="99ab6-155">I/o-metagegevens voor elke service binnen de aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="99ab6-156">De gebruiksvoorwaarden van aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="99ab6-157">Voorbeeld van gegevens van de aanbieding</span><span class="sxs-lookup"><span data-stu-id="99ab6-157">Preview of the offer's data</span></span>

<span data-ttu-id="99ab6-158">Controleer ten slotte dat de service werkt via de Datamarket door te klikken op de koppeling 'Deze GEGEVENSSET VERKENNEN'.</span><span class="sxs-lookup"><span data-stu-id="99ab6-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="99ab6-159">Een nieuw venster wordt geopend in het hulpprogramma noemen we 'Service Explorer' zodat u de resultaten van een query bij uw service kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="99ab6-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="99ab6-160">U kunt hier de parameters invoeren en de resultaten van een query op uw service weergegeven.</span><span class="sxs-lookup"><span data-stu-id="99ab6-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="99ab6-161">Weergegeven is ook de URL voor uw Query.</span><span class="sxs-lookup"><span data-stu-id="99ab6-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="99ab6-162">Zorg ervoor dat de tekstbeschrijving van de service die wordt weergegeven boven bekijken.</span><span class="sxs-lookup"><span data-stu-id="99ab6-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="99ab6-163">En als uw aanbieding bestaat uit meer dan één service aanroepen, klikt u op de tabbladen aan de onderkant overschakelen naar de volgende service om te controleren en te testen.</span><span class="sxs-lookup"><span data-stu-id="99ab6-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="99ab6-164">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="99ab6-164">Next step</span></span>
<span data-ttu-id="99ab6-165">Als u problemen ondervindt en hebt u hulp nodig fouten op te lossen neemt contact op met [ondersteuning van Azure Publisher](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="99ab6-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="99ab6-166">Als u tevreden en gereed voor het publiceren van uw aanbieding Lees bent de [goedkeuring aanvragen naar productie Push](marketplace-publishing-push-to-production.md) documentatie.</span><span class="sxs-lookup"><span data-stu-id="99ab6-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="99ab6-167">Zie ook</span><span class="sxs-lookup"><span data-stu-id="99ab6-167">See Also</span></span>
* [<span data-ttu-id="99ab6-168">Aan de slag: Hoe een aanbieding publiceren in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="99ab6-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

