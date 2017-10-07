---
title: "aaaBuild oplossingen geïntegreerd met SQL Data Warehouse | Microsoft Docs"
description: "Hulpprogramma's en partners met oplossingen die zijn geïntegreerd met SQL Data Warehouse. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Gebruikmaken van andere services met SQL Data Warehouse
Bovendien tooits functionaliteit core, SQL Data Warehouse kunnen gebruikers tooleverage veel van andere services in Azure ernaast Hallo.  In het bijzonder hebben we stappen toodeeply integreren met de volgende Hallo momenteel genomen:

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Azure Stream Analytics

We werken tooconnect met meer services via hello Azure-ecosysteem.

## <a name="power-bi"></a>Power BI
Integratie van Power BI kunt u tooleverage Hallo rekencapaciteit van SQL Data Warehouse met dynamische Hallo-rapportage en visualisatie van Power BI. Power BI-integratie omvat momenteel:

* **Verbinding maken met directe**: een meer geavanceerde verbinding met logische naar beneden duwen tegen SQL Data Warehouse.  Dit biedt sneller analyse op grotere schaal.
* **Openen in Power BI**: 'Te openen in Power BI' Hallo-knop exemplaar informatie tooPower BI, waardoor het een meer naadloze verbinding is geslaagd.

Zie [integreren met Power BI](sql-data-warehouse-integrate-power-bi.md) of Hallo [Power BI-documentatie](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) voor meer informatie.

## <a name="azure-data-factory"></a>Azure Data Factory
Azure Data Factory biedt gebruikers een beheerd platform toocreate die complexe Extract belasting pijplijnen.  SQL Data Warehouse-integratie met Azure Data Factory bevat Hallo volgende:

* **Opgeslagen Procedures**: indelen Hallo uitvoering van opgeslagen procedures op de SQL Data Warehouse.
* **Kopiëren**: gebruik ADF toomove gegevens in SQL Data Warehouse.  Deze bewerking kunt ADF standaardgegevens gegevensverplaatsing mechanisme gebruiken of PolyBase onder Hallo worden behandeld. 

Zie [integreren met Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) of Hallo [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) voor meer informatie.

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning is een volledig beheerde analytics-service waarmee gebruikers toocreate complexe modellen gebruik te maken van een groot aantal voorspellende hulpprogramma's.  SQL Data Warehouse wordt ondersteund als een bron- en doel voor deze modellen Hello functionaliteit te volgen:

* **Gegevens lezen:** modellen station op grote schaal met T-SQL met SQL Data Warehouse.
* **Schrijven van gegevens:** wijzigingen van een model back-tooSQL Data Warehouse.

Zie [integreren met Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) of Hallo [Azure Machine Learning-documentatie](https://azure.microsoft.com/services/machine-learning/) voor meer informatie.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
Azure Stream Analytics is een volledig beheerde complexe infrastructuur voor het verwerken en gebruiken van gebeurtenisgegevens die zijn gegenereerd uit Azure Event Hub.  Integratie met SQL Data Warehouse kan voor streaming gegevens toobe effectief verwerkt en opgeslagen samen met relationele gegevens beter inschakelen, meer geavanceerde analyse.  

* **Taakuitvoer:** verzenden uitvoer van de Stream Analytics taken rechtstreeks tooSQL Data Warehouse.

Zie [integreren met Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) of Hallo [Azure Stream Analytics-documentatie](https://azure.microsoft.com/documentation/services/stream-analytics/) voor meer informatie.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
