---
title: Zoekopdrachten opslaan en een pincode gegevensassets in Azure Data Catalog | Microsoft Docs
description: Hoe kan ik artikel mogelijkheden in Azure Data Catalog is gemarkeerd voor het opslaan van gegevensbronnen en gegevensassets voor later gebruik.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="08390-103">Zoekopdrachten en pincode gegevensassets opslaan in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="08390-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="08390-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="08390-104">Introduction</span></span>
<span data-ttu-id="08390-105">Azure Data Catalog bevat mogelijkheden voor detectie van gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="08390-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="08390-106">U kunt snel zoeken en filteren van de catalogus gegevensbronnen vinden en begrijpen van het beoogde gebruik, waardoor het gemakkelijker de juiste gegevens vinden voor de taak op dat moment.</span><span class="sxs-lookup"><span data-stu-id="08390-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="08390-107">Maar wat gebeurt er als u wilt regelmatig werken met dezelfde gegevens?</span><span class="sxs-lookup"><span data-stu-id="08390-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="08390-108">En wat gebeurt er als u en andere gebruikers regelmatig bij te dragen uw kennis met de dezelfde gegevensbronnen in de catalogus?</span><span class="sxs-lookup"><span data-stu-id="08390-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="08390-109">In deze situaties kan herhaaldelijk uitgeven de zoekopdrachten die dezelfde zijn inefficiënt.</span><span class="sxs-lookup"><span data-stu-id="08390-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="08390-110">Dit is waar opgeslagen zoekopdracht en vastgemaakt gegevensassets kunnen helpen.</span><span class="sxs-lookup"><span data-stu-id="08390-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="08390-111">Opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="08390-111">Saved searches</span></span>
<span data-ttu-id="08390-112">Een opgeslagen zoekopdracht in Data Catalog is een definitie van een herbruikbare, per gebruiker zoeken.</span><span class="sxs-lookup"><span data-stu-id="08390-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="08390-113">U kunt een zoekopdracht, zoals zoektermen, labels en andere filters definiëren en vervolgens opslaan.</span><span class="sxs-lookup"><span data-stu-id="08390-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="08390-114">U kunt de definitie van de opgeslagen zoekopdracht later om te retourneren van alle gegevensassets die overeenkomen met de zoekcriteria opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="08390-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="08390-115">Maken van een opgeslagen zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="08390-115">Create a saved search</span></span>
<span data-ttu-id="08390-116">Ga als volgt te werk voor het maken van een opgeslagen zoekopdracht:</span><span class="sxs-lookup"><span data-stu-id="08390-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="08390-117">In de Azure Data Catalog-portal in de **huidige zoekopdracht** venster, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="08390-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Koppeling van huidige zoekopdracht instellingen opslaan](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="08390-119">Voer de zoekcriteria die u wilt gebruiken en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="08390-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Huidige zoekinstellingen opgeslagen zoeknaam](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="08390-121">Wanneer u wordt gevraagd, typt u een naam voor de opgeslagen zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="08390-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="08390-122">Kies een naam die zinnig is en dat de gegevensassets die worden geretourneerd door de zoekopdracht beschrijft.</span><span class="sxs-lookup"><span data-stu-id="08390-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="08390-123">Opgeslagen zoekopdrachten beheren</span><span class="sxs-lookup"><span data-stu-id="08390-123">Manage saved searches</span></span>
<span data-ttu-id="08390-124">Nadat u hebt opgeslagen zoekopdrachten voor een of meer, een **opgeslagen zoekacties** optie wordt weergegeven onder de **huidige zoekopdracht** vak.</span><span class="sxs-lookup"><span data-stu-id="08390-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="08390-125">Wanneer de lijst wordt uitgevouwen, worden alle opgeslagen zoekopdrachten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08390-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Lijst met opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="08390-127">Het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="08390-127">Do any of the following:</span></span>

* <span data-ttu-id="08390-128">Selecteer een opgeslagen zoekopdracht in de lijst voor het uitvoeren van een zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="08390-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="08390-129">Een lijst van beheeropties voor een opgeslagen zoekopdracht wilt weergeven, klikt u op de pijl-omlaag naast de naam van de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="08390-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Opties voor het beheer opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="08390-131">Als u wilt een nieuwe naam voor de opgeslagen zoekopdracht invoeren, selecteert u **naam**.</span><span class="sxs-lookup"><span data-stu-id="08390-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="08390-132">De definitie van de zoekopdracht is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="08390-132">The search definition is not changed.</span></span>

* <span data-ttu-id="08390-133">Als de opgeslagen zoekopdracht uit de lijst, selecteert u **verwijderen**, en vervolgens de verwijdering te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="08390-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="08390-134">Selecteer de opgeslagen zoekopdracht als uw zoekopdracht standaard markeert, **opslaan als standaard**.</span><span class="sxs-lookup"><span data-stu-id="08390-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="08390-135">Als u een 'empty' zoekopdracht vanaf de startpagina van Azure Data Catalog uitvoert, wordt uw standaard-zoekopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08390-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="08390-136">Bovendien de zoekopdracht die gemarkeerd als de standaardzoekopdracht wordt weergegeven boven aan de **opgeslagen zoekacties** lijst.</span><span class="sxs-lookup"><span data-stu-id="08390-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="08390-137">Organisatie opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="08390-137">Organizational saved searches</span></span>
<span data-ttu-id="08390-138">Alle gebruikers in uw organisatie kunt zoekopdrachten voor eigen gebruik opslaan.</span><span class="sxs-lookup"><span data-stu-id="08390-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="08390-139">Data Catalog beheerders kunnen ook gezocht naar alle gebruikers binnen de organisatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="08390-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="08390-140">Wanneer beheerders een zoekopdracht opslaat, ze worden weergegeven met een **Share binnen het bedrijf** optie.</span><span class="sxs-lookup"><span data-stu-id="08390-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="08390-141">Als u deze optie selecteert, deelt de opgeslagen zoekopdracht voor alle gebruikers in de organisatie.</span><span class="sxs-lookup"><span data-stu-id="08390-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Organisatie opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="08390-143">Vastgemaakte gegevensassets</span><span class="sxs-lookup"><span data-stu-id="08390-143">Pinned data assets</span></span>
<span data-ttu-id="08390-144">U kunt met opgeslagen zoekopdrachten opslaan en opnieuw zoeken definities gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08390-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="08390-145">De gegevensassets die worden geretourneerd door de zoekopdrachten die kunnen worden gewijzigd na verloop van tijd als de inhoud van de wijziging van de catalogus.</span><span class="sxs-lookup"><span data-stu-id="08390-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="08390-146">Wanneer u gegevensassets vastmaken, kunt u specifieke gegevensassets te vereenvoudigen voor toegang tot een zoeken gebruiken zonder expliciet identificeren.</span><span class="sxs-lookup"><span data-stu-id="08390-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="08390-147">Een gegevensasset vastmaken is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="08390-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="08390-148">De gegevensasset toevoegen aan uw vastgemaakte lijst, klikt u op de **pincode** pictogram.</span><span class="sxs-lookup"><span data-stu-id="08390-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="08390-149">Het pictogram wordt weergegeven in de rechterbenedenhoek van de asset-tegel in de weergave tile en in de linkerkolom in de lijstweergave in de portal voor Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="08390-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Het Punaisepictogram gegevens asset](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="08390-151">Een gegevensasset losmaken is even eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="08390-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="08390-152">Klik op de **losmaken** pictogram in de instelling voor de geselecteerde asset-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="08390-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![De gegevensasset losmaken pictogram](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="08390-154">De sectie Mijn activa</span><span class="sxs-lookup"><span data-stu-id="08390-154">The My Assets section</span></span>
<span data-ttu-id="08390-155">De portal startpagina van Data Catalog bevat een **Mijn activa** sectie geeft de activa van belang bij de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="08390-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="08390-156">Deze sectie bevat zowel vastgemaakt activa en opgeslagen zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="08390-156">This section includes both pinned assets and saved searches.</span></span>

![De sectie Mijn activa op de startpagina](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="08390-158">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="08390-158">Summary</span></span>
<span data-ttu-id="08390-159">Azure Data Catalog bevat mogelijkheden waarmee het eenvoudiger is voor het detecteren van de gegevensbronnen die u nodig hebt, zodat u en andere leden van de organisatie kunnen minder tijd nodig voor zoekt gegevens en meer tijd ermee te werken.</span><span class="sxs-lookup"><span data-stu-id="08390-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="08390-160">Opgeslagen zoekopdrachten en vastgemaakt gegevens activa op deze belangrijkste mogelijkheden, bouwen zodat gebruikers de gegevensbronnen die ze met herhaaldelijk werken gemakkelijk kunnen herkennen.</span><span class="sxs-lookup"><span data-stu-id="08390-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
