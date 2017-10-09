---
title: aaaAnalyze gegevens met Azure Machine Learning | Microsoft Docs
description: Gebruik toobuild Azure Machine Learning een Voorspellend machine learning-model op basis van gegevens die zijn opgeslagen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Gegevens analyseren met Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Deze zelfstudie wordt toobuild Azure Machine Learning een Voorspellend machine learning-model op basis van gegevens die zijn opgeslagen in Azure SQL Data Warehouse. In het bijzonder het resultaat hiervan is een gerichte marketingcampagne voor Adventure Works, de fietsenwinkel hello, door te voorspellen als een klant waarschijnlijk toobuy een fiets is of niet.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Vereisten
toostep voor deze zelfstudie hebt u nodig:

* Een SQL Data Warehouse waarin AdventureWorksDW-voorbeeldgegevens zijn geladen. tooprovision deze, Zie [maken van een SQL Data Warehouse] [ Create a SQL Data Warehouse] en kies tooload Hallo voorbeeldgegevens. Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].

## <a name="1-get-hello-data"></a>1. Hallo-gegevens ophalen
Hallo-gegevens zijn in de weergave dbo.vTargetMail Hallo in de database AdventureWorksDW Hallo. tooread deze gegevens:

1. Meld u aan bij [Azure Machine Learning Studio][Azure Machine Learning studio] en klik op My experiments (Mijn experimenten).
2. Klik op **+NEW** (Nieuw) en selecteer **Blank Experiment** (Leeg experiment).
3. Voer een naam in voor uw experiment: Targeted Marketing.
4. Sleep Hallo **lezer** module op basis van het deelvenster met modules Hallo naar Hallo canvas.
5. Geef details op Hallo van uw SQL Data Warehouse-database in deelvenster Hallo-eigenschappen.
6. Geef Hallo database **query** tooread Hallo gegevens van belang.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Hallo-experiment uitvoeren door te klikken op **uitvoeren** onder het experimentcanvas Hallo.
![Hallo-experiment uitvoeren][1]

Nadat het Hallo-experiment is uitgevoerd, klikt u op de uitvoerpoort Hallo HALLO hallo leesmodule onderaan in en selecteert u **Visualize** toosee Hallo geïmporteerde gegevens.
![Geïmporteerde gegevens weergeven][3]

## <a name="2-clean-hello-data"></a>2. Schone Hallo-gegevens
tooclean hello gegevens, verwijderen kolommen die niet relevant voor Hallo model. toodo dit:

1. Sleep Hallo **Projectkolommen** module naar Hallo canvas.
2. Klik op **Launch column selector** in Hallo eigenschappen deelvenster toospecify kolommen die u wenst dat toodrop.
   ![Projectkolommen][4]
3. Sluit twee kolommen uit: CustomerAlternateKey en GeographyKey.
   ![Overbodige kolommen verwijderen][5]

## <a name="3-build-hello-model"></a>3. Hallo-model maken
We zullen Hallo gegevens 80-20 splitsen: 80% tootrain een machine learning-model en 20% tootest Hallo model. Maken we gebruik van Hallo 'Two-Class' algoritmen voor dit binair klassificatieprobleem.

1. Sleep Hallo **gesplitste** module naar Hallo canvas.
2. Typ 0,8 fractie van rijen in de eerste uitvoergegevensset Hallo in deelvenster Hallo-eigenschappen.
   ![Gegevens splitsen in trainings- en testset][6]
3. Sleep Hallo **Two-Class Boosted Decision Tree** module naar Hallo canvas.
4. Sleep Hallo **Train Model** module in Hallo canvas en geef Hallo-invoer. Klik vervolgens op **Launch column selector** in deelvenster Hallo-eigenschappen.
   * Eerste invoer: ML-algoritme.
   * Tweede invoer: gegevens tootrain Hallo algoritme op.
     ![Sluit Hallo Train Model-module][7]
5. Selecteer Hallo **BikeBuyer** Hallo kolom toopredict kolom.
   ![Selecteer de kolom toopredict][8]

## <a name="4-score-hello-model"></a>4. Hallo-score-model
Nu gaat u testen hoe Hallo model functioneert met testgegevens. Hallo-algoritme van onze keuze met een ander algoritme toosee die beter presteert gaat vergelijken.

1. Sleep **Score Model** module naar Hallo canvas.
    Eerste invoer: getraind model tweede invoer: testgegevens ![Hallo-Score-model][9]
2. Sleep Hallo **Two-Class Bayes Point Machine** naar het experimentcanvas Hallo. U gaat vergelijken hoe dit algoritme in vergelijking toohello Two-Class Boosted Decision Tree uitvoert.
3. Kopiëren en plakken Hallo modules Train Model en Score-Model in Hallo canvas.
4. Sleep Hallo **Evaluate Model** module in Hallo canvas toocompare Hallo twee algoritmen.
5. **Voer** Hallo experiment.
   ![Hallo-experiment uitvoeren][10]
6. Hallo uitvoerpoort onder Hallo van de module Evaluate Model Hallo en klik op Visualize.
   ![Evaluatieresultaten visualiseren][11]

Hallo verstrekte metrische gegevens zijn Hallo ROC-curve, precisie-/ oproepdiagram diagram en lift-curve. Deze metrische gegevens bekijkt, ziet u dat Hallo eerste model beter dan tweede Hallo uitgevoerd. toolook op Hallo wat Hallo eerste model voorspeld, klik op de uitvoerpoort van Hallo Score Model en klik op Visualize.
![Scoreresultaten visualiseren][12]

Ziet u dat twee of meer kolommen tooyour testgegevensset toegevoegd.

* Scored kansen: Hallo kans dat een klant een fiets koopt is.
* Scored Labels: Hallo classificatie gedaan door Hallo model: fietskoper (1) of niet (0). Deze drempelwaarde voor waarschijnlijkheid voor labeling too50% wordt ingesteld en kan worden aangepast.

Hallo kolom BikeBuyer (werkelijk) met Hallo Scored Labels (voorspelling) te vergelijken, kunt u zien hoe goed Hallo model heeft gepresteerd. De volgende stappen kunt u dit model toomake voorspellingen gebruiken voor nieuwe klanten en dit model publiceren als een webservice of resultaten back tooSQL datawarehouse schrijven.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het bouwen van voorspellende machine learning-modellen, te verwijzen[inleiding tooMachine Learning in Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
