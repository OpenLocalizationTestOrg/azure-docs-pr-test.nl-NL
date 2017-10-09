---
title: aaaManage gegevensassets in Azure Data Catalog | Microsoft Docs
description: Hallo artikel ziet u hoe toocontrol zichtbaarheid en eigendom van gegevensassets geregistreerd in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="991c9-103">Gegevensassets in Azure Data Catalog beheren</span><span class="sxs-lookup"><span data-stu-id="991c9-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="991c9-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="991c9-104">Introduction</span></span>
<span data-ttu-id="991c9-105">Azure Data Catalog is ontworpen voor detectie van de gegevensbron, zodat u eenvoudig kunt detecteren en begrijpen van gegevensbronnen Hallo u tooperform analyse nodig hebt en beslissingen te nemen.</span><span class="sxs-lookup"><span data-stu-id="991c9-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="991c9-106">Deze mogelijkheden voor detectie maken de grootste impact Hallo wanneer u en andere gebruikers kunnen vinden en begrijpen Hallo breedste scala aan beschikbare gegevensbronnen waren.</span><span class="sxs-lookup"><span data-stu-id="991c9-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="991c9-107">Met de volgende elementen rekening is Hallo standaardgedrag van Data Catalog voor alle geregistreerde gegevensbronnen toobe zichtbaar tooand kunnen worden gedetecteerd door alle gebruikers van de catalogus.</span><span class="sxs-lookup"><span data-stu-id="991c9-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="991c9-108">Data Catalog geeft u geen toegang tot toohello gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="991c9-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="991c9-109">Gegevenstoegang wordt bepaald door de eigenaar van de gegevensbron Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="991c9-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="991c9-110">U kunt met Data Catalog gegevensbronnen detecteren en Hallo metagegevens die gerelateerde toohello bronnen die zijn geregistreerd in Hallo-catalogus weergeven.</span><span class="sxs-lookup"><span data-stu-id="991c9-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="991c9-111">Er zijn mogelijk situaties echter waar gegevensbronnen alleen zichtbaar toospecific gebruikers of toomembers van specifieke groepen worden mogen.</span><span class="sxs-lookup"><span data-stu-id="991c9-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="991c9-112">In dergelijke gevallen kunnen gebruikers eigenaar worden van geregistreerde gegevensassets binnen Hallo-catalogus en vervolgens bepalen Hallo zichtbaarheid van Hallo activa die ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="991c9-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="991c9-113">Hallo-functionaliteit die wordt beschreven in dit artikel is alleen beschikbaar in Standard-editie van Azure Data Catalog Hallo.</span><span class="sxs-lookup"><span data-stu-id="991c9-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="991c9-114">Hallo biedt editie Free geen mogelijkheden voor eigendom en gegevens asset-zichtbaarheid beperken.</span><span class="sxs-lookup"><span data-stu-id="991c9-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="991c9-115">Eigendom van gegevensassets beheren</span><span class="sxs-lookup"><span data-stu-id="991c9-115">Manage ownership of data assets</span></span>
<span data-ttu-id="991c9-116">Standaard zijn de gegevensassets die zijn geregistreerd in Data Catalog zonder eigenaar.</span><span class="sxs-lookup"><span data-stu-id="991c9-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="991c9-117">Elke gebruiker met machtigingen tooaccess Hallo catalog kan detecteren en aantekeningen toevoegen aan deze activa.</span><span class="sxs-lookup"><span data-stu-id="991c9-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="991c9-118">Gebruikers kunnen eigenaar worden van gegevensassets zonder eigenaar en vervolgens beperken Hallo zichtbaarheid van Hallo activa die ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="991c9-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="991c9-119">Wanneer u het eigendom van een activum gegevens in Data Catalog is alleen gebruikers die zijn geautoriseerd door eigenaren van Hallo Hallo asset detecteren en weergeven van de metagegevens en alleen Hallo eigenaars Hallo asset kunnen verwijderen uit de catalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="991c9-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="991c9-120">Data Catalog eigendom is van invloed op Hallo alleen metagegevens die zijn opgeslagen in de catalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="991c9-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="991c9-121">Eigenaar verleent alle machtigingen op Hallo onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="991c9-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="991c9-122">Eigenaar worden</span><span class="sxs-lookup"><span data-stu-id="991c9-122">Take ownership</span></span>
<span data-ttu-id="991c9-123">Gebruikers kunnen eigenaar worden van gegevensassets door het selecteren van Hallo **eigenaar** optie in Hallo Data Catalog-portal.</span><span class="sxs-lookup"><span data-stu-id="991c9-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="991c9-124">Er is geen speciale machtigingen zijn vereist tootake eigendom van een actief gegevens zonder eigenaar.</span><span class="sxs-lookup"><span data-stu-id="991c9-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="991c9-125">Elke gebruiker kan de eigenaar van een activum zonder eigenaar gegevens.</span><span class="sxs-lookup"><span data-stu-id="991c9-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="991c9-126">Eigenaar en mede-eigenaren toevoegen</span><span class="sxs-lookup"><span data-stu-id="991c9-126">Add owners and co-owners</span></span>
<span data-ttu-id="991c9-127">Gewoon als een gegevensasset is al het eigendom, andere gebruikers kunnen geen eigenaar.</span><span class="sxs-lookup"><span data-stu-id="991c9-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="991c9-128">Ze moeten worden toegevoegd als mede-eigenaren door de eigenaar van een bestaande.</span><span class="sxs-lookup"><span data-stu-id="991c9-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="991c9-129">Eigenaar kunt extra gebruikers of beveiligingsgroepen toevoegen als mede-eigenaren.</span><span class="sxs-lookup"><span data-stu-id="991c9-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="991c9-130">Er is een best practice toohave voor een gegevensasset die eigendom zijn van ten minste twee personen als eigenaars.</span><span class="sxs-lookup"><span data-stu-id="991c9-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="991c9-131">Eigenaars verwijderen</span><span class="sxs-lookup"><span data-stu-id="991c9-131">Remove owners</span></span>
<span data-ttu-id="991c9-132">Net zoals een activumeigenaar mede-eigenaren toevoegen kunt, kunt een activumeigenaar mede-eigenaar verwijderen.</span><span class="sxs-lookup"><span data-stu-id="991c9-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="991c9-133">De eigenaar van een asset die zichzelf als eigenaar van een verwijderd kunt Hallo asset niet langer beheren.</span><span class="sxs-lookup"><span data-stu-id="991c9-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="991c9-134">Als de activumeigenaar Hallo zichzelf als eigenaar van een verwijderd en er geen andere mede-eigenaars, terug Hallo asset tooan staat geen eigenaar ingesteld.</span><span class="sxs-lookup"><span data-stu-id="991c9-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="991c9-135">Zichtbaarheid besturingselement</span><span class="sxs-lookup"><span data-stu-id="991c9-135">Control visibility</span></span>
<span data-ttu-id="991c9-136">Gegevensasset eigenaars kunnen beheren Hallo zichtbaarheid van gegevensassets Hallo die ze eigenaar zijn.</span><span class="sxs-lookup"><span data-stu-id="991c9-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="991c9-137">toorestrict zichtbaarheid als Hallo standaard, wanneer alle Data Catalog gebruikers kunnen detecteren en weergave Hallo gegevensasset, activumeigenaar Hallo kunt schakelen Hallo zichtbaarheidsinstelling van **iedereen** te**eigenaars en deze gebruikers** in de eigenschappen van Hallo voor Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="991c9-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="991c9-138">Eigenaars kunnen vervolgens specifieke gebruikers en beveiligingsgroepen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="991c9-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="991c9-139">Indien mogelijk moeten machtigingen voor het eigendom en de zichtbaarheid van asset toosecurity groepen en niet tooindividual gebruikers worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="991c9-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="991c9-140">Beheerders van de catalogus</span><span class="sxs-lookup"><span data-stu-id="991c9-140">Catalog administrators</span></span>
<span data-ttu-id="991c9-141">Data Catalog beheerders zijn impliciet mede-eigenaren van alle activa in Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="991c9-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="991c9-142">Asset eigenaars zichtbaarheid aan beheerders niet verwijderen en beheerders kunnen beheren, eigendom en de zichtbaarheid van alle gegevens activa in Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="991c9-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="991c9-143">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="991c9-143">Summary</span></span>
<span data-ttu-id="991c9-144">Hallo Data Catalog crowdsourcing-model toometadata asset detectie en kunnen alle catalogus gebruikers toocontribute en detecteren.</span><span class="sxs-lookup"><span data-stu-id="991c9-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="991c9-145">Hallo Standard-editie van Data Catalog is ontworpen voor het eigenaarschap en beheer toolimit Hallo zichtbaarheid en het gebruik van specifieke gegevensassets.</span><span class="sxs-lookup"><span data-stu-id="991c9-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
