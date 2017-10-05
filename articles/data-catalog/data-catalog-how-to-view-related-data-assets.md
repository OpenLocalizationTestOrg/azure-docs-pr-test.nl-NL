---
title: Gerelateerde gegevens activa weergeven in Azure Data Catalog | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u gerelateerde gegevensassets van een activum geselecteerde gegevens weergeven in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="38131-103">Hoe gerelateerde gegevens activa weergeven in Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="38131-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="38131-104">Azure Data Catalog kunt u gegevensassets die betrekking hebben op een geselecteerde gegevens asset en bekijk de relaties tussen deze twee weergeven.</span><span class="sxs-lookup"><span data-stu-id="38131-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="38131-105">Ondersteunde gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="38131-105">Supported data sources</span></span> 
<span data-ttu-id="38131-106">Wanneer u gegevensassets van de volgende gegevensbronnen registreert, worden de metagegevens over join-relaties tussen de geselecteerde gegevensassets Azure Data Catalog automatisch geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="38131-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="38131-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="38131-107">SQL Server</span></span>
- <span data-ttu-id="38131-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38131-108">Azure SQL Database</span></span>
- <span data-ttu-id="38131-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="38131-109">MySQL</span></span>
- <span data-ttu-id="38131-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="38131-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="38131-111">Gerelateerde gegevens activa weergeven</span><span class="sxs-lookup"><span data-stu-id="38131-111">View related data assets</span></span>
<span data-ttu-id="38131-112">Als u wilt weergeven van gegevensassets die zijn gerelateerd aan een geselecteerde gegevensset, gebruiken de **relaties** tabblad zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="38131-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog - gerelateerde gegevensassets weergeven](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="38131-114">In dit voorbeeld zijn er twee relaties voor het geselecteerde **ProductSubcategory** gegevensasset:</span><span class="sxs-lookup"><span data-stu-id="38131-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="38131-115">ProductSubcategoryID kolom van de Product-tabel heeft een refererende-sleutelrelatie met ProductSubcategoryID kolom van de geselecteerde ProductSubcategory-tabel.</span><span class="sxs-lookup"><span data-stu-id="38131-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="38131-116">ProductCategoryID kolom van de tabel ProductSubCategory heeft een refererende-sleutelrelatie met ProductCategoryID kolom van de geselecteerde ProductCategory-tabel.</span><span class="sxs-lookup"><span data-stu-id="38131-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="38131-117">U ziet de richting van de pijl in de structuurweergave relaties.</span><span class="sxs-lookup"><span data-stu-id="38131-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="38131-118">Beweeg de muisaanwijzer over voor meer informatie zoals de volledig gekwalificeerde naam van de kolom, en u ziet een pop-up die vergelijkbaar is met de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="38131-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog - relatie pop](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="38131-120">Als u wilt opnemen relaties tussen de activa die al zijn geregistreerd, deze assets opnieuw te registreren.</span><span class="sxs-lookup"><span data-stu-id="38131-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38131-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38131-121">Next steps</span></span>
- [<span data-ttu-id="38131-122">Gegevensassets beheren</span><span class="sxs-lookup"><span data-stu-id="38131-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)