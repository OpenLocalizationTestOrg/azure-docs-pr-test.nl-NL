---
title: Beheren van gegevensassets in Azure Data Catalog | Microsoft Docs
description: Het artikel wordt uitgelegd hoe u instellingen voor zichtbaarheid en de eigenaar te worden van gegevensassets die zijn geregistreerd in Azure Data Catalog.
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
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="59cfa-103">Gegevensassets in Azure Data Catalog beheren</span><span class="sxs-lookup"><span data-stu-id="59cfa-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="59cfa-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="59cfa-104">Introduction</span></span>
<span data-ttu-id="59cfa-105">Azure Data Catalog is ontworpen voor detectie van de gegevensbron, zodat u gemakkelijk detecteren en begrijpen van de gegevensbronnen die u moet analyses uitvoeren en beslissingen te nemen.</span><span class="sxs-lookup"><span data-stu-id="59cfa-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="59cfa-106">Deze mogelijkheden voor detectie maken de grootste impact wanneer u en andere gebruikers kunnen vinden en begrijpen waren van een breed scala aan gegevensbronnen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="59cfa-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="59cfa-107">Met de volgende elementen in gedachten is het standaardgedrag van Data Catalog voor alle geregistreerde gegevensbronnen zijn zichtbaar voor en kunnen worden gedetecteerd door alle gebruikers van de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="59cfa-108">Data Catalog biedt niet krijgt u toegang tot de gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="59cfa-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="59cfa-109">Gegevenstoegang wordt bepaald door de eigenaar van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="59cfa-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="59cfa-110">U kunt met Data Catalog gegevensbronnen detecteren en weergeven van de metagegevens met betrekking tot de bronnen die zijn geregistreerd in de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="59cfa-111">Er zijn mogelijk situaties echter waar gegevensbronnen alleen zichtbaar voor specifieke gebruikers of leden van specifieke groepen zijn moeten.</span><span class="sxs-lookup"><span data-stu-id="59cfa-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="59cfa-112">In dergelijke gevallen kunnen gebruikers eigenaar worden van geregistreerde gegevensassets in de catalogus en vervolgens bepalen de zichtbaarheid van de activa die ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="59cfa-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="59cfa-113">De functionaliteit die is beschreven in dit artikel is alleen beschikbaar in de Standard-editie van Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="59cfa-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="59cfa-114">De editie Free biedt geen mogelijkheden voor eigenaar en beperking gegevens asset-zichtbaarheid.</span><span class="sxs-lookup"><span data-stu-id="59cfa-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="59cfa-115">Eigendom van gegevensassets beheren</span><span class="sxs-lookup"><span data-stu-id="59cfa-115">Manage ownership of data assets</span></span>
<span data-ttu-id="59cfa-116">Standaard zijn de gegevensassets die zijn geregistreerd in Data Catalog zonder eigenaar.</span><span class="sxs-lookup"><span data-stu-id="59cfa-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="59cfa-117">Een gebruiker met machtigingen voor toegang tot de catalogus kan detecteren en aantekeningen toevoegen aan deze activa.</span><span class="sxs-lookup"><span data-stu-id="59cfa-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="59cfa-118">Gebruikers kunnen eigenaar worden van gegevensassets zonder eigenaar en vervolgens de zichtbaarheid van de activa die ze eigenaar te beperken.</span><span class="sxs-lookup"><span data-stu-id="59cfa-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="59cfa-119">Wanneer u het eigendom van een activum gegevens in Data Catalog is alleen gebruikers die zijn geautoriseerd door de eigenaren van de asset detecteren en weergeven van de metagegevens en alleen de eigenaren van de activa kunnen verwijderen uit de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="59cfa-120">Data Catalog eigendom is van invloed op alleen de metagegevens die zijn opgeslagen in de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="59cfa-121">Eigenaar verleent alle machtigingen op de onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="59cfa-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="59cfa-122">Eigenaar worden</span><span class="sxs-lookup"><span data-stu-id="59cfa-122">Take ownership</span></span>
<span data-ttu-id="59cfa-123">Gebruikers kunnen eigenaar worden van gegevensassets door het selecteren van de **eigenaar** optie in de portal voor Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="59cfa-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="59cfa-124">Geen speciale machtigingen zijn vereist om de eigenaar van een activum zonder eigenaar gegevens.</span><span class="sxs-lookup"><span data-stu-id="59cfa-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="59cfa-125">Elke gebruiker kan de eigenaar van een activum zonder eigenaar gegevens.</span><span class="sxs-lookup"><span data-stu-id="59cfa-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="59cfa-126">Eigenaar en mede-eigenaren toevoegen</span><span class="sxs-lookup"><span data-stu-id="59cfa-126">Add owners and co-owners</span></span>
<span data-ttu-id="59cfa-127">Gewoon als een gegevensasset is al het eigendom, andere gebruikers kunnen geen eigenaar.</span><span class="sxs-lookup"><span data-stu-id="59cfa-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="59cfa-128">Ze moeten worden toegevoegd als mede-eigenaren door de eigenaar van een bestaande.</span><span class="sxs-lookup"><span data-stu-id="59cfa-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="59cfa-129">Eigenaar kunt extra gebruikers of beveiligingsgroepen toevoegen als mede-eigenaren.</span><span class="sxs-lookup"><span data-stu-id="59cfa-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="59cfa-130">Het is een best practice om ten minste twee personen als eigenaars voor een willekeurige gegevensasset in eigendom van.</span><span class="sxs-lookup"><span data-stu-id="59cfa-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="59cfa-131">Eigenaars verwijderen</span><span class="sxs-lookup"><span data-stu-id="59cfa-131">Remove owners</span></span>
<span data-ttu-id="59cfa-132">Net zoals een activumeigenaar mede-eigenaren toevoegen kunt, kunt een activumeigenaar mede-eigenaar verwijderen.</span><span class="sxs-lookup"><span data-stu-id="59cfa-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="59cfa-133">Een asset-eigenaar die zichzelf als eigenaar van een verwijderd kan niet meer beheren voor de asset.</span><span class="sxs-lookup"><span data-stu-id="59cfa-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="59cfa-134">Als de activumeigenaar zichzelf als eigenaar van een verwijderd en er geen andere mede-eigenaars, wordt de asset terug naar de status zonder eigenaar.</span><span class="sxs-lookup"><span data-stu-id="59cfa-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="59cfa-135">Zichtbaarheid besturingselement</span><span class="sxs-lookup"><span data-stu-id="59cfa-135">Control visibility</span></span>
<span data-ttu-id="59cfa-136">Gegevensasset eigenaren kunnen bepalen de zichtbaarheid van de gegevensassets die ze eigenaar zijn.</span><span class="sxs-lookup"><span data-stu-id="59cfa-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="59cfa-137">Als u wilt beperken zichtbaarheid als de standaardconfiguratie, waarbij alle gebruikers van Data Catalog detecteren en weergeven van de gegevensasset, de activumeigenaar de zichtbaarheidsinstelling van kunt schakelen **iedereen** naar **eigenaars en deze gebruikers** in de eigenschappen voor de asset.</span><span class="sxs-lookup"><span data-stu-id="59cfa-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="59cfa-138">Eigenaars kunnen vervolgens specifieke gebruikers en beveiligingsgroepen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="59cfa-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="59cfa-139">Indien mogelijk moeten asset eigendom en zichtbaarheid machtigingen worden toegewezen aan beveiligingsgroepen en niet naar afzonderlijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="59cfa-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="59cfa-140">Beheerders van de catalogus</span><span class="sxs-lookup"><span data-stu-id="59cfa-140">Catalog administrators</span></span>
<span data-ttu-id="59cfa-141">Data Catalog beheerders zijn impliciet mede-eigenaren van alle activa in de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="59cfa-142">Asset eigenaars kunnen visibility niet verwijderen uit beheerders en beheerders kunnen beheren, eigendom en de zichtbaarheid van alle gegevensassets in de catalogus.</span><span class="sxs-lookup"><span data-stu-id="59cfa-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="59cfa-143">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="59cfa-143">Summary</span></span>
<span data-ttu-id="59cfa-144">De Data Catalog crowdsourcing-model voor detectie van metagegevens en activa kan alle catalogusgebruikers bijdragen en detecteren.</span><span class="sxs-lookup"><span data-stu-id="59cfa-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="59cfa-145">De Standard-editie van Data Catalog is ontworpen voor het eigenaarschap en beheer beperken de zichtbaarheid van en het gebruik van specifieke gegevensassets.</span><span class="sxs-lookup"><span data-stu-id="59cfa-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
