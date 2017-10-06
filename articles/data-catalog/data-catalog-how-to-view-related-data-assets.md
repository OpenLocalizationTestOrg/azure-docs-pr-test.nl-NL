---
title: aaaHow tooview gerelateerde gegevensassets in Azure Data Catalog | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooview gegevensassets van een geselecteerde gegevensasset in Azure Data Catalog gerelateerd.
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
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="a4573-103">Hoe gerelateerd tooview gegevensassets in Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="a4573-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="a4573-104">Azure Data Catalog kunt u tooview gegevens activa gerelateerde tooa geselecteerd gegevens asset en bekijk onderlinge relaties.</span><span class="sxs-lookup"><span data-stu-id="a4573-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="a4573-105">Ondersteunde gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="a4573-105">Supported data sources</span></span> 
<span data-ttu-id="a4573-106">Wanneer u gegevensassets van Hallo gegevensbronnen te volgen registreert, worden de metagegevens over join-relaties tussen Hallo geselecteerd gegevensassets Azure Data Catalog automatisch geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a4573-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="a4573-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a4573-107">SQL Server</span></span>
- <span data-ttu-id="a4573-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4573-108">Azure SQL Database</span></span>
- <span data-ttu-id="a4573-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="a4573-109">MySQL</span></span>
- <span data-ttu-id="a4573-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="a4573-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="a4573-111">Gerelateerde gegevens activa weergeven</span><span class="sxs-lookup"><span data-stu-id="a4573-111">View related data assets</span></span>
<span data-ttu-id="a4573-112">tooview gegevensassets die gerelateerde tooa geselecteerd dataset gebruiken Hallo **relaties** tabblad zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4573-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog - gerelateerde gegevensassets weergeven](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="a4573-114">In dit voorbeeld zijn twee relaties voor Hallo geselecteerd **ProductSubcategory** gegevensasset:</span><span class="sxs-lookup"><span data-stu-id="a4573-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="a4573-115">De kolom ProductSubcategoryID van Hallo producttabel heeft een refererende-sleutelrelatie met ProductSubcategoryID kolom Hallo geselecteerd ProductSubcategory tabel.</span><span class="sxs-lookup"><span data-stu-id="a4573-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="a4573-116">De kolom ProductCategoryID van Hallo ProductSubCategory tabel heeft een refererende-sleutelrelatie met ProductCategoryID kolom Hallo geselecteerd ProductCategory tabel.</span><span class="sxs-lookup"><span data-stu-id="a4573-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="a4573-117">U ziet Hallo richting van Hallo pijl in de structuurweergave Hallo-relaties.</span><span class="sxs-lookup"><span data-stu-id="a4573-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="a4573-118">toosee meer details zoals Hallo volledig gekwalificeerde naam van de kolom hello, muisaanwijzer Hallo over en ziet u een pop-upvenster vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4573-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog - relatie pop](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="a4573-120">tooinclude relaties tussen de activa die al zijn geregistreerd, deze assets opnieuw te registreren.</span><span class="sxs-lookup"><span data-stu-id="a4573-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4573-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4573-121">Next steps</span></span>
- [<span data-ttu-id="a4573-122">Hoe toomanage gegevensassets</span><span class="sxs-lookup"><span data-stu-id="a4573-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
