---
title: aaaUse Azure Machine Learning met SQL Data Warehouse | Microsoft Docs
description: Zelfstudie voor het gebruik van Azure Machine Learning met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="91046-103">Gebruik Azure Machine Learning met SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="91046-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="91046-104">Azure Machine Learning is een volledig beheerde predictive analytics-service dat u kunt het gebruiken van voorspellende modellen toocreate op basis van uw gegevens in SQL Data Warehouse en vervolgens als webservices gereed om te gebruiken publiceren.</span><span class="sxs-lookup"><span data-stu-id="91046-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="91046-105">U kunt de basisbegrippen Hallo van predictive analytics en machine learning door te lezen [inleiding tooMachine Learning in Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="91046-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="91046-106">Vervolgens leert u hoe toocreate, trainen, beoordelen en testen van een machine learning-model met Hallo [maken experiment zelfstudie][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="91046-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="91046-107">In dit artikel leert u hoe toodo Hallo volgen met behulp van Hallo [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="91046-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="91046-108">Gegevens lezen uit de database-toocreate, te trainen en een Voorspellend model beoordelen</span><span class="sxs-lookup"><span data-stu-id="91046-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="91046-109">Gegevens tooyour database schrijven</span><span class="sxs-lookup"><span data-stu-id="91046-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="91046-110">Lezen van gegevens uit SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="91046-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="91046-111">Leest gegevens uit de tabel Product in de database AdventureWorksDW Hallo.</span><span class="sxs-lookup"><span data-stu-id="91046-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="91046-112">Stap 1</span><span class="sxs-lookup"><span data-stu-id="91046-112">Step 1</span></span>
<span data-ttu-id="91046-113">Start een nieuw experiment door te klikken op + Nieuw onderin Hallo Hallo Machine Learning Studio-venster EXPERIMENT selecteren en selecteer vervolgens leeg Experiment.</span><span class="sxs-lookup"><span data-stu-id="91046-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="91046-114">Selecteer Hallo standaard naam Hallo boven aan het papier Hallo experiment en wijzig deze toosomething zinvolle, bijvoorbeeld fiets prijs voorspelling.</span><span class="sxs-lookup"><span data-stu-id="91046-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="91046-115">Stap 2</span><span class="sxs-lookup"><span data-stu-id="91046-115">Step 2</span></span>
<span data-ttu-id="91046-116">Leesmodule hello in Hallo palet met gegevenssets en modules op Hallo links van het experimentcanvas Hallo zoekt.</span><span class="sxs-lookup"><span data-stu-id="91046-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="91046-117">Sleep Hallo module toohello experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="91046-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="91046-118">Stap 3</span><span class="sxs-lookup"><span data-stu-id="91046-118">Step 3</span></span>
<span data-ttu-id="91046-119">Leesmodule hello Selecteer en invullen Hallo eigenschappendeelvenster.</span><span class="sxs-lookup"><span data-stu-id="91046-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="91046-120">Selecteer de Azure SQL Database als Hallo gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="91046-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="91046-121">Database-servernaam: typenaam van het Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="91046-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="91046-122">U kunt Hallo [Azure-portal] [ Azure portal] toofind dit.</span><span class="sxs-lookup"><span data-stu-id="91046-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="91046-123">Databasenaam: Type Hallo-naam van een database op Hallo-server die u zojuist hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="91046-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="91046-124">Server gebruikersaccountnaam: Typ de gebruikersnaam van een account met toegangsmachtigingen voor de database Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="91046-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="91046-125">Het wachtwoord voor gebruikersaccount server: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="91046-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="91046-126">Een servercertificaat accepteren: Gebruik deze optie (minder veilig) als u wilt dat tooskip Hallo sitecertificaat controleren voordat u uw gegevens leest.</span><span class="sxs-lookup"><span data-stu-id="91046-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="91046-127">Databasequery: Voer een SQL-instructie waarmee Hallo gegevens u wilt dat tooread worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="91046-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="91046-128">In dit geval wordt we gegevens uit de tabel Product met behulp van de volgende query Hallo lezen.</span><span class="sxs-lookup"><span data-stu-id="91046-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="91046-129">Stap 4</span><span class="sxs-lookup"><span data-stu-id="91046-129">Step 4</span></span>
1. <span data-ttu-id="91046-130">Hallo-experiment door te klikken op uitvoeren onder het experimentcanvas Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91046-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="91046-131">Wanneer het Hallo-experiment is voltooid, hebt Hallo leesmodule een groen vinkje tooindicate die het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="91046-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="91046-132">U ziet ook Hallo status uitgevoerd in de rechterbovenhoek Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="91046-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="91046-133">toosee Hallo geïmporteerde gegevens, klikt u op de uitvoerpoort Hallo HALLO hallo auto gegevensset onderaan in en selecteer visualiseren.</span><span class="sxs-lookup"><span data-stu-id="91046-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="91046-134">Maken, te trainen en een model beoordelen</span><span class="sxs-lookup"><span data-stu-id="91046-134">Create, train and score a model</span></span>
<span data-ttu-id="91046-135">Nu kunt u deze gegevensset te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="91046-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="91046-136">Een Model maken: gegevens verwerken en functies definiëren</span><span class="sxs-lookup"><span data-stu-id="91046-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="91046-137">Train Hallo model: kiezen en toepassen van een leeralgoritme</span><span class="sxs-lookup"><span data-stu-id="91046-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="91046-138">Score en test Hallo model: nieuwe fiets prijs voorspellen</span><span class="sxs-lookup"><span data-stu-id="91046-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="91046-139">meer informatie over hoe toocreate, trainen, beoordelen en testen van een machine learning-model gebruik Hallo toolearn [maken experiment zelfstudie][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="91046-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="91046-140">Schrijven van gegevens tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="91046-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="91046-141">We schrijft set Hallo-tooProductPriceForecast resultaattabel in de database AdventureWorksDW Hallo.</span><span class="sxs-lookup"><span data-stu-id="91046-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="91046-142">Stap 1</span><span class="sxs-lookup"><span data-stu-id="91046-142">Step 1</span></span>
<span data-ttu-id="91046-143">Hallo-schrijfmodule in Hallo palet met gegevenssets en modules op Hallo links van het experimentcanvas Hallo zoekt.</span><span class="sxs-lookup"><span data-stu-id="91046-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="91046-144">Sleep Hallo module toohello experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="91046-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="91046-145">Stap 2</span><span class="sxs-lookup"><span data-stu-id="91046-145">Step 2</span></span>
<span data-ttu-id="91046-146">Hallo-schrijfmodule Selecteer en invullen Hallo eigenschappendeelvenster.</span><span class="sxs-lookup"><span data-stu-id="91046-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="91046-147">Selecteer Azure SQL Database als Hallo gegevensbestemming.</span><span class="sxs-lookup"><span data-stu-id="91046-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="91046-148">Database-servernaam: typenaam van het Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="91046-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="91046-149">U kunt Hallo [Azure-portal] [ Azure portal] toofind dit.</span><span class="sxs-lookup"><span data-stu-id="91046-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="91046-150">Databasenaam: Type Hallo-naam van een database op Hallo-server die u zojuist hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="91046-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="91046-151">Server gebruikersaccountnaam: Typ de gebruikersnaam van een account met schrijfmachtigingen voor de database Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="91046-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="91046-152">Het wachtwoord voor gebruikersaccount server: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="91046-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="91046-153">Een servercertificaat (onbeveiligde) accepteren: Selecteer deze optie als u niet dat tooview Hallo certificaat wilt.</span><span class="sxs-lookup"><span data-stu-id="91046-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="91046-154">Door komma's gescheiden lijst met kolommen toobe opgeslagen: een lijst verstrekken van Hallo gegevensset of het resultaat van de kolommen die u toooutput wilt.</span><span class="sxs-lookup"><span data-stu-id="91046-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="91046-155">Data-tabelnaam: Hallo naam opgeven van Hallo gegevenstabel.</span><span class="sxs-lookup"><span data-stu-id="91046-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="91046-156">Door komma's gescheiden lijst met datatable kolommen: Hallo kolom namen toouse in de nieuwe tabel Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="91046-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="91046-157">Hello kolomnamen kunnen afwijken van Hallo die in Hallo bron gegevensset, maar u moet de lijst met hetzelfde aantal kolommen hierheen die u voor de uitvoertabel Hallo definieert Hallo.</span><span class="sxs-lookup"><span data-stu-id="91046-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="91046-158">Aantal rijen per SQL Azure-bewerking geschreven: U kunt configureren Hallo aantal rijen dat tooa SQL-database zijn geschreven in één bewerking.</span><span class="sxs-lookup"><span data-stu-id="91046-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="91046-159">Stap 3</span><span class="sxs-lookup"><span data-stu-id="91046-159">Step 3</span></span>
1. <span data-ttu-id="91046-160">Hallo-experiment door te klikken op uitvoeren onder het experimentcanvas Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91046-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="91046-161">Wanneer het Hallo-experiment is voltooid, hebben alle modules een groen vinkje tooindicate dat ze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="91046-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91046-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91046-162">Next steps</span></span>
<span data-ttu-id="91046-163">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="91046-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
