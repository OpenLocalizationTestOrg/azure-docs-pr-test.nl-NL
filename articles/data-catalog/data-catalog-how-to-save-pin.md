---
title: aaaSave zoekopdrachten en pincode gegevensassets in Azure Data Catalog | Microsoft Docs
description: Hoe tooarticle markeren mogelijkheden in Azure Data Catalog voor het opslaan van gegevensbronnen en gegevensassets voor later gebruik.
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
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="4e213-103">Zoekopdrachten en pincode gegevensassets opslaan in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="4e213-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="4e213-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="4e213-104">Introduction</span></span>
<span data-ttu-id="4e213-105">Azure Data Catalog bevat mogelijkheden voor detectie van gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="4e213-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="4e213-106">U kunt snel zoeken en filteren Hallo catalogus toolocate gegevensbronnen en begrijpen van het beoogde gebruik, waardoor het gemakkelijker toofind Hallo juiste gegevens voor Hallo taak op dat moment.</span><span class="sxs-lookup"><span data-stu-id="4e213-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="4e213-107">Maar wat gebeurt er als u tooregularly moet werken met Hallo dezelfde gegevens?</span><span class="sxs-lookup"><span data-stu-id="4e213-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="4e213-108">En wat gebeurt er als u en andere gebruikers regelmatig bij te uw kennis toohello dragen dezelfde gegevensbronnen in de catalogus Hallo?</span><span class="sxs-lookup"><span data-stu-id="4e213-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="4e213-109">In deze situaties met toorepeatedly probleem Hallo dezelfde zoekacties inefficiënt zijn.</span><span class="sxs-lookup"><span data-stu-id="4e213-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="4e213-110">Dit is waar opgeslagen zoekopdracht en vastgemaakt gegevensassets kunnen helpen.</span><span class="sxs-lookup"><span data-stu-id="4e213-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="4e213-111">Opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="4e213-111">Saved searches</span></span>
<span data-ttu-id="4e213-112">Een opgeslagen zoekopdracht in Data Catalog is een definitie van een herbruikbare, per gebruiker zoeken.</span><span class="sxs-lookup"><span data-stu-id="4e213-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="4e213-113">U kunt een zoekopdracht, zoals zoektermen, labels en andere filters definiëren en vervolgens opslaan.</span><span class="sxs-lookup"><span data-stu-id="4e213-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="4e213-114">U kunt opnieuw uitvoeren Hallo opgeslagen zoekopdracht definitie hoger tooreturn eventuele gegevensassets die overeenkomen met de zoekcriteria.</span><span class="sxs-lookup"><span data-stu-id="4e213-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="4e213-115">Maken van een opgeslagen zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="4e213-115">Create a saved search</span></span>
<span data-ttu-id="4e213-116">een opgeslagen zoekopdracht toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e213-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="4e213-117">Hello Azure Data Catalog, in portal Hallo **huidige zoekopdracht** venster, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e213-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Koppeling van huidige zoekopdracht instellingen opslaan](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="4e213-119">Voer de zoekcriteria Hallo tooreuse wilt en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e213-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Huidige zoekinstellingen opgeslagen zoeknaam](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="4e213-121">Wanneer u wordt gevraagd, typt u een naam voor de opgeslagen zoekopdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e213-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="4e213-122">Kies een naam die zinnig is en die beschrijft Hallo gegevensassets die worden geretourneerd door Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="4e213-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="4e213-123">Opgeslagen zoekopdrachten beheren</span><span class="sxs-lookup"><span data-stu-id="4e213-123">Manage saved searches</span></span>
<span data-ttu-id="4e213-124">Nadat u hebt opgeslagen zoekopdrachten voor een of meer, een **opgeslagen zoekacties** optie wordt weergegeven onder Hallo **huidige zoekopdracht** vak.</span><span class="sxs-lookup"><span data-stu-id="4e213-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="4e213-125">Wanneer het Hallo-lijst is uitgevouwen, worden alle opgeslagen zoekopdrachten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4e213-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Lijst met opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="4e213-127">Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="4e213-127">Do any of hello following:</span></span>

* <span data-ttu-id="4e213-128">tooexecute een zoekopdracht, selecteert u een opgeslagen zoekopdracht in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="4e213-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="4e213-129">tooview een lijst met opties voor een opgeslagen zoekopdracht, klikt u op Hallo omlaag Pijl volgende toohello zoeknaam.</span><span class="sxs-lookup"><span data-stu-id="4e213-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Opties voor het beheer opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="4e213-131">Selecteer een nieuwe naam voor de zoekopdracht op Hallo opgeslagen tooenter **naam**.</span><span class="sxs-lookup"><span data-stu-id="4e213-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="4e213-132">Hallo zoeken definitie is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4e213-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="4e213-133">tooremove hello opgeslagen zoekopdracht uit de lijst, selecteert **verwijderen**, en bevestig vervolgens Hallo verwijdering.</span><span class="sxs-lookup"><span data-stu-id="4e213-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="4e213-134">uw zoekopdracht standaard selecteert toomark Hallo opgeslagen zoekactie **opslaan als standaard**.</span><span class="sxs-lookup"><span data-stu-id="4e213-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="4e213-135">Als u een 'empty' zoeken op de introductiepagina van hello Azure Data Catalog uitvoert, wordt uw standaard-zoekopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e213-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="4e213-136">Bovendien Hallo zoeken die gemarkeerd als Hallo standaardzoekopdracht wordt weergegeven boven Hallo Hallo **opgeslagen zoekacties** lijst.</span><span class="sxs-lookup"><span data-stu-id="4e213-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="4e213-137">Organisatie opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="4e213-137">Organizational saved searches</span></span>
<span data-ttu-id="4e213-138">Alle gebruikers in uw organisatie kunt zoekopdrachten voor eigen gebruik opslaan.</span><span class="sxs-lookup"><span data-stu-id="4e213-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="4e213-139">Data Catalog beheerders kunnen ook gezocht naar alle gebruikers binnen de organisatie Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="4e213-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="4e213-140">Wanneer beheerders een zoekopdracht opslaat, ze worden weergegeven met een **Share binnen Hallo bedrijf** optie.</span><span class="sxs-lookup"><span data-stu-id="4e213-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="4e213-141">Deze optie shares Hallo opgeslagen zoekactie voor alle gebruikers in de organisatie Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="4e213-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Organisatie opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="4e213-143">Vastgemaakte gegevensassets</span><span class="sxs-lookup"><span data-stu-id="4e213-143">Pinned data assets</span></span>
<span data-ttu-id="4e213-144">U kunt met opgeslagen zoekopdrachten opslaan en opnieuw zoeken definities gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4e213-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="4e213-145">Hallo-gegevensassets die worden geretourneerd door Hallo zoekopdrachten kunnen worden gewijzigd na verloop van tijd als de inhoud Hallo van Hallo catalogus wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4e213-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="4e213-146">Wanneer u gegevensassets vastmaken, kunt u expliciet specifieke gegevens activa toomake identificeren ze gemakkelijker tooaccess zonder toouse een zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="4e213-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="4e213-147">Een gegevensasset vastmaken is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="4e213-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="4e213-148">tooadd hello gegevens asset tooyour vastgemaakt lijst, klikt u op Hallo **pincode** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4e213-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="4e213-149">Hallo-pictogram wordt weergegeven in de hoek Hallo van Hallo asset tegel in de weergave tile hello en in de linkerkolom Hallo in de lijstweergave Hallo in hello Azure Data Catalog-portal.</span><span class="sxs-lookup"><span data-stu-id="4e213-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![Hallo-gegevensasset Punaisepictogram](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="4e213-151">Een gegevensasset losmaken is even eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="4e213-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="4e213-152">Klik op Hallo **losmaken** pictogram tootoggle Hallo-instelling voor de geselecteerde asset Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e213-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![Hallo-gegevensasset losmaken pictogram](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="4e213-154">Hallo Mijn activa-sectie</span><span class="sxs-lookup"><span data-stu-id="4e213-154">hello My Assets section</span></span>
<span data-ttu-id="4e213-155">Hallo Data Catalog portal introductiepagina bevat een **Mijn activa** sectie waarin de activa van belang toohello huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4e213-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="4e213-156">Deze sectie bevat zowel vastgemaakt activa en opgeslagen zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="4e213-156">This section includes both pinned assets and saved searches.</span></span>

![Hallo Mijn activa-sectie op Hallo-startpagina](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="4e213-158">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4e213-158">Summary</span></span>
<span data-ttu-id="4e213-159">Azure Data Catalog bevat mogelijkheden waarmee u gemakkelijker toodiscover Hallo gegevensbronnen die u nodig, zodat u en andere leden van de organisatie kunnen minder tijd nodig voor zoekt gegevens en meer tijd ermee te werken.</span><span class="sxs-lookup"><span data-stu-id="4e213-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="4e213-160">Opgeslagen zoekopdrachten en vastgemaakt gegevens activa op deze belangrijkste mogelijkheden, bouwen zodat gebruikers de gegevensbronnen die ze met herhaaldelijk werken gemakkelijk kunnen herkennen.</span><span class="sxs-lookup"><span data-stu-id="4e213-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
