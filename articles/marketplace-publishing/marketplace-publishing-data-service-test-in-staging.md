---
title: uw Data-Service bieden voor Hallo Marketplace aaaTesting | Microsoft Docs
description: Begrijpen hoe tootest uw Data-Service bieden voor hello Azure Marketplace.
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
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="a883a-103">Testen van uw Data-Service-aanbieding in fasering</span><span class="sxs-lookup"><span data-stu-id="a883a-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a883a-104">**Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.**</span><span class="sxs-lookup"><span data-stu-id="a883a-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="a883a-105">Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="a883a-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="a883a-106">Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="a883a-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="a883a-107">Na het voltooien van de eerste twee stappen Hallo van [maken van uw account Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) en [maken van uw gegevens Service bieden in Publishing Portal](marketplace-publishing-data-service-creation.md) u klaar bent om uw aanbieding in Hallo beschikbaar Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a883a-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="a883a-108">In dit onderwerp wordt stapsgewijs Hallo eerst, tussenliggende, naam 'Staging' stap</span><span class="sxs-lookup"><span data-stu-id="a883a-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="a883a-109">Fasering manier uw aanbieding in een particulier 'sandbox"waar u kunt testen en de functionaliteit ervan controleren voordat u deze tooproduction implementeren.</span><span class="sxs-lookup"><span data-stu-id="a883a-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="a883a-110">Hallo aanbieding wordt weergegeven in de faseringsmodus net zoals tooa klant die is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a883a-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="a883a-111">Step 1.</span><span class="sxs-lookup"><span data-stu-id="a883a-111">Step 1.</span></span> <span data-ttu-id="a883a-112">Uw aanbieding toostaging pushen</span><span class="sxs-lookup"><span data-stu-id="a883a-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="a883a-113">Uw aanbieding toostaging pushen kunt u tootest Hallo aanbieding daarna deze beschikbaar toofuture abonnees wordt.</span><span class="sxs-lookup"><span data-stu-id="a883a-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="a883a-114">U kunt zien hoe uw aanbieding wordt weergegeven en werken voor de tooyour gegevens te abonneren.</span><span class="sxs-lookup"><span data-stu-id="a883a-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="a883a-116">Aanmelden bij Hallo [Publishing Portal](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="a883a-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="a883a-117">Selecteer **Data Services** in Hallo linkernavigatievenster venster</span><span class="sxs-lookup"><span data-stu-id="a883a-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="a883a-118">Selecteer de gewenste toopush toostaging aanbieding.</span><span class="sxs-lookup"><span data-stu-id="a883a-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="a883a-119">Hallo boven scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a883a-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="a883a-120">Klik op **tooStaging Push** knop.</span><span class="sxs-lookup"><span data-stu-id="a883a-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="a883a-121">Als er problemen zijn met Hallo aanbieding die nodig toobe zijn voorafgaande toopushing toostaging voltooid, ziet u een lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a883a-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="a883a-122">Corrigeer deze items door te klikken op elk item in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="a883a-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="a883a-123">Wanneer alle correcties zijn aangebracht, klikt u op **tooStaging Push** knop opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a883a-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="a883a-124">Als er geen problemen met uw aanbieding zijn ziet u hieronder Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="a883a-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="a883a-125">Als u niet bent planning/niet goedgekeurd toosurface uw aanbieding in Azure-Portal (momenteel heeft beperkte capaciteit), en vervolgens net sluiten Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="a883a-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="a883a-126">tootest uw gegevens in Azure Portal-Service (in aanvulling toohello DataMarket portal), moet u een Azure-abonnements-ID tootest met.</span><span class="sxs-lookup"><span data-stu-id="a883a-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="a883a-127">Dit abonnement-ID wordt geïdentificeerd Hallo-account dat wordt toegestaan tootest uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="a883a-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="a883a-128">Knippen en plakken van uw abonnements-ID en klikt u op Hallo vinkje toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a883a-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="a883a-130">Deze id Azure-abonnementen zijn alleen vereist voor het testen en fasering in Hallo [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a883a-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a883a-131">Ze zijn geen vereiste tootest in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a883a-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="a883a-132">Hallo volgende scherm ziet u dat publicatie plaatsvindt door Hallo 'wordt uitgevoerd' weer te geven pictogram onderstaande geel gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="a883a-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="a883a-133">Toostaging pushen duurt tussen 10 too15 minuten.</span><span class="sxs-lookup"><span data-stu-id="a883a-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="a883a-134">Als het duurt langer, moet u eerst uw browser (druk op F5 in Internet Explorer) vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="a883a-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="a883a-135">Hallo zeldzame gevallen waarin uw aanbieding is nog steeds worden gepusht toostaging na een uur, klikt u op de koppeling toolet ons weten dat er een probleem Hallo contact is.</span><span class="sxs-lookup"><span data-stu-id="a883a-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="a883a-137">Wanneer Hallo Push tooStaging Hallo is voltooid 'wordt uitgevoerd' pictogram wordt gestopt met het verplaatsen van en Hallo status wordt bijgewerkt te 'gefaseerde'.</span><span class="sxs-lookup"><span data-stu-id="a883a-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="a883a-138">U bent nu klaar tootest uw aanbieding.</span><span class="sxs-lookup"><span data-stu-id="a883a-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="a883a-139">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="a883a-139">Step 2.</span></span> <span data-ttu-id="a883a-140">Testen van uw voorbereide aanbieding in DataMarket</span><span class="sxs-lookup"><span data-stu-id="a883a-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="a883a-141">Klik op de koppeling Hallo na de tekst hello **' Zie uw service bieden op... '**</span><span class="sxs-lookup"><span data-stu-id="a883a-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="a883a-142">welkomstscherm toodisplay die Hallo abonnee ziet wanneer uw aanbieding tooproduction gaat en wordt weergegeven in DataMarket.</span><span class="sxs-lookup"><span data-stu-id="a883a-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="a883a-144">Testen of Controleer of elk van Hallo 12 items gemarkeerd hierboven tooensure alle logo's, prijzen/transacties, tekst, afbeeldingen, documentatie en koppelingen correct zijn en werken goed.</span><span class="sxs-lookup"><span data-stu-id="a883a-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="a883a-145">Dit is een goed moment tooensure een testwaarden die u hebt ingevoerd bij het maken van uw aanbieding zijn vervangen door feitelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="a883a-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="a883a-146">Aanbieding-logo</span><span class="sxs-lookup"><span data-stu-id="a883a-146">Offer logo</span></span>
2. <span data-ttu-id="a883a-147">De aanbiedingsnaam van de</span><span class="sxs-lookup"><span data-stu-id="a883a-147">Offer name</span></span>
3. <span data-ttu-id="a883a-148">Publisher naam/link tooyour website van bedrijf</span><span class="sxs-lookup"><span data-stu-id="a883a-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="a883a-149">Categorieën voor uw aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-149">Search categories for your offer</span></span>
5. <span data-ttu-id="a883a-150">Uw aanbieding ondersteuning koppeling tooassist abonnees</span><span class="sxs-lookup"><span data-stu-id="a883a-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="a883a-151">Contextafhankelijke beschrijving voor uw aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="a883a-152">Plan factureringsgegevens van aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="a883a-153">Koppeling tooimplementation code</span><span class="sxs-lookup"><span data-stu-id="a883a-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="a883a-154">Voorbeeld-installatiekopieën die aangeven gebruiken van gegevens van aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="a883a-155">I/o-metagegevens voor elke service binnen Hallo aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="a883a-156">De gebruiksvoorwaarden van aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="a883a-157">Voorbeeld van gegevens Hallo-aanbieding</span><span class="sxs-lookup"><span data-stu-id="a883a-157">Preview of hello offer's data</span></span>

<span data-ttu-id="a883a-158">Controleer ten slotte Hallo service werkt via Hallo Datamarket door te klikken op Hallo 'Deze GEGEVENSSET VERKENNEN'.</span><span class="sxs-lookup"><span data-stu-id="a883a-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="a883a-159">Een nieuw venster wordt geopend in Hallo hulpprogramma noemen we 'Service Explorer' zodat u een voorbeeld Hallo resultaten van een query bij uw service bekijken kunt.</span><span class="sxs-lookup"><span data-stu-id="a883a-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="a883a-160">In dit venster kunt u Hallo parameters nodig en Hallo resultaten weergegeven van een query op uw service te zien.</span><span class="sxs-lookup"><span data-stu-id="a883a-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="a883a-161">Weergegeven is bovendien Hallo-URL voor uw Query.</span><span class="sxs-lookup"><span data-stu-id="a883a-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="a883a-162">Worden ervoor tooreview Hallo tekstbeschrijving van weergegeven boven het Hallo Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="a883a-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="a883a-163">En als uw aanbieding uit meer dan één service bestaat aanroepen, klikt u op de tabbladen Hallo op Hallo onder tooswitch toohello volgende service tooreview en testen.</span><span class="sxs-lookup"><span data-stu-id="a883a-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="a883a-164">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="a883a-164">Next step</span></span>
<span data-ttu-id="a883a-165">Als u problemen ondervindt en hebt u hulp nodig fouten op te lossen neemt contact op met [ondersteuning van Azure Publisher](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="a883a-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="a883a-166">Als u tevreden bent en gereed toopublish uw aanbieding Lees Hallo [goedkeuring aanvragen tooPush tooProduction](marketplace-publishing-push-to-production.md) documentatie.</span><span class="sxs-lookup"><span data-stu-id="a883a-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="a883a-167">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a883a-167">See Also</span></span>
* [<span data-ttu-id="a883a-168">Aan de slag: Hoe toopublish een aanbieding toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a883a-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

