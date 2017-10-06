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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Hoe gerelateerd tooview gegevensassets in Azure Data Catalog?
Azure Data Catalog kunt u tooview gegevens activa gerelateerde tooa geselecteerd gegevens asset en bekijk onderlinge relaties. 

## <a name="supported-data-sources"></a>Ondersteunde gegevensbronnen 
Wanneer u gegevensassets van Hallo gegevensbronnen te volgen registreert, worden de metagegevens over join-relaties tussen Hallo geselecteerd gegevensassets Azure Data Catalog automatisch geregistreerd. 

- SQL Server
- Azure SQL Database
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Gerelateerde gegevens activa weergeven
tooview gegevensassets die gerelateerde tooa geselecteerd dataset gebruiken Hallo **relaties** tabblad zoals weergegeven in Hallo installatiekopie te volgen: 

![Azure Data Catalog - gerelateerde gegevensassets weergeven](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

In dit voorbeeld zijn twee relaties voor Hallo geselecteerd **ProductSubcategory** gegevensasset: 

- De kolom ProductSubcategoryID van Hallo producttabel heeft een refererende-sleutelrelatie met ProductSubcategoryID kolom Hallo geselecteerd ProductSubcategory tabel. 
- De kolom ProductCategoryID van Hallo ProductSubCategory tabel heeft een refererende-sleutelrelatie met ProductCategoryID kolom Hallo geselecteerd ProductCategory tabel.

> [!NOTE]
> U ziet Hallo richting van Hallo pijl in de structuurweergave Hallo-relaties.  

toosee meer details zoals Hallo volledig gekwalificeerde naam van de kolom hello, muisaanwijzer Hallo over en ziet u een pop-upvenster vergelijkbare toohello installatiekopie te volgen: 

![Azure Data Catalog - relatie pop](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relaties tussen de activa die al zijn geregistreerd, deze assets opnieuw te registreren.

## <a name="next-steps"></a>Volgende stappen
- [Hoe toomanage gegevensassets](data-catalog-how-to-manage.md)
