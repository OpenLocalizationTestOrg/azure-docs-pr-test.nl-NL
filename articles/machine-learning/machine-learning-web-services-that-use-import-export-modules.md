---
title: Met behulp van importeren/exporteren-gegevens in Azure Machine Learning-webservices | Microsoft Docs
description: Informatie over het gebruik van de modules die gegevens importeren en exporteren van gegevens te verzenden en ontvangen van gegevens van een webservice.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 123c8c2b1c5bae268b2a61c185743f2c3920175e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="b23e2-103">Azure ML-webservices implementeren die gebruikmaken van gegevensimport- en gegevensexportmodules</span><span class="sxs-lookup"><span data-stu-id="b23e2-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="b23e2-104">Wanneer u een Voorspellend experiment maakt, voegt u gewoonlijk toe een web service invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b23e2-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="b23e2-105">Wanneer u het experiment implementeert, kunnen consumenten gegevens verzenden en ontvangen van de webservice via de invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b23e2-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="b23e2-106">Voor sommige toepassingen van de consumer gegevens uit een gegevensfeed beschikbaar of al bevinden zich in een externe gegevensbron zoals Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b23e2-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="b23e2-107">In dergelijke gevallen hoeven ze niet lezen en schrijven van gegevens met behulp van web service in- en uitgangen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="b23e2-108">Ze kunnen in plaats daarvan Batch uitvoering Service (BES) gebruiken om te lezen van gegevens uit de gegevensbron met behulp van een module gegevens importeren en de resultaten van score berekenen schrijven naar een andere locatie met behulp van een module gegevens exporteren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="b23e2-109">De gegevens importeren en exporteren modules die gegevens lezen uit en schrijven naar verschillende gegevens locaties zoals een via HTTP, een Hive-Query, een Azure SQL-database, Azure Table storage, Azure Blob storage, een Gegevensfeed-URL opgeeft, of een lokale SQL-database.</span><span class="sxs-lookup"><span data-stu-id="b23e2-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="b23e2-110">In dit onderwerp worden de "voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' steekproef en wordt ervan uitgegaan dat de dataset al is geladen in een Azure SQL-tabel met de naam censusdata.</span><span class="sxs-lookup"><span data-stu-id="b23e2-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="b23e2-111">De trainingsexperiment maken</span><span class="sxs-lookup"><span data-stu-id="b23e2-111">Create the training experiment</span></span>
<span data-ttu-id="b23e2-112">Wanneer u opent de "voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' voorbeeld de voorbeeldgegevensset volwassenen inventarisering Income binaire classificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b23e2-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="b23e2-113">En het experiment in het canvas ziet er ongeveer als de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="b23e2-113">And the experiment in the canvas will look similar to the following image:</span></span>

![De aanvankelijke configuratie van het experiment.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="b23e2-115">De gegevens lezen uit de Azure SQL-tabel:</span><span class="sxs-lookup"><span data-stu-id="b23e2-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="b23e2-116">De dataset-module verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="b23e2-117">Typ in het zoekvak onderdelen importeren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="b23e2-118">Toevoegen van de lijst met resultaten een *importgegevens* module naar het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="b23e2-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="b23e2-119">Verbinding maken met de uitvoer van de *importgegevens* module de invoer van de *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="b23e2-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="b23e2-120">Selecteer in het eigenschappendeelvenster **Azure SQL Database** in de **gegevensbron** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b23e2-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="b23e2-121">In de **databaseservernaam**, **databasenaam**, **gebruikersnaam**, en **wachtwoord** velden, voer de juiste informatie voor uw de database.</span><span class="sxs-lookup"><span data-stu-id="b23e2-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="b23e2-122">Voer de volgende query in het databaseveld query.</span><span class="sxs-lookup"><span data-stu-id="b23e2-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="b23e2-123">Selecteer [leeftijd]</span><span class="sxs-lookup"><span data-stu-id="b23e2-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="b23e2-124">van dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="b23e2-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="b23e2-125">Klik aan de onderkant van het experimentcanvas **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="b23e2-126">De Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="b23e2-126">Create the predictive experiment</span></span>
<span data-ttu-id="b23e2-127">De volgende instellen van de Voorspellend experiment van waaruit u uw webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="b23e2-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="b23e2-128">Klik onderaan in het experimentcanvas **webservice ingesteld** en selecteer **voorspellende Web Service (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="b23e2-129">Verwijder de *Web Service invoer* en *Web Service uitvoer modules* van Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="b23e2-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="b23e2-130">Typ in het zoekvak onderdelen exporteren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="b23e2-131">Toevoegen van de lijst met resultaten een *gegevens exporteren* module naar het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="b23e2-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="b23e2-132">Verbinding maken met de uitvoer van de *Score Model* module de invoer van de *gegevens exporteren* module.</span><span class="sxs-lookup"><span data-stu-id="b23e2-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="b23e2-133">Selecteer in het eigenschappendeelvenster **Azure SQL Database** in de vervolgkeuzelijst voor het doel van gegevens.</span><span class="sxs-lookup"><span data-stu-id="b23e2-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="b23e2-134">In de **databaseservernaam**, **databasenaam**, **Server gebruikersaccountnaam**, en **Server het wachtwoord voor gebruikersaccount** velden, voer de relevante informatie voor uw database.</span><span class="sxs-lookup"><span data-stu-id="b23e2-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="b23e2-135">In de **door komma's gescheiden lijst met kolommen op te slaan** veld, typt u Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="b23e2-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="b23e2-136">In de **gegevensveld tabel naam**, typt u dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="b23e2-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="b23e2-137">Als de tabel niet bestaat, wordt deze gemaakt wanneer het experiment is uitgevoerd of de webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="b23e2-138">In de **door komma's gescheiden lijst met kolommen datatable** veld ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="b23e2-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="b23e2-139">Wanneer u een toepassing die de laatste webservice roept schrijft, is het raadzaam om op te geven van een andere invoer voor de query of een doeltabel tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="b23e2-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="b23e2-140">Wilt configureren en deze uitgangen, gebruikt u de functie Webserviceparameters om in te stellen de *importgegevens* module *gegevensbron* eigenschap en de *gegevens exporteren* modus gegevens doel-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b23e2-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="b23e2-141">Zie voor meer informatie over Webserviceparameters de [Webserviceparameters AzureML-vermelding](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) op de Cortana Intelligence en Machine Learning-Blog.</span><span class="sxs-lookup"><span data-stu-id="b23e2-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="b23e2-142">Parameters van de webservice voor de query importeren en de doeltabel configureren:</span><span class="sxs-lookup"><span data-stu-id="b23e2-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="b23e2-143">In het deelvenster met eigenschappen voor de *gegevens importeren* -module, klikt u op het pictogram aan de bovenkant rechts van de **databasequery** veld en selecteert u **instellen als web Serviceparameter**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="b23e2-144">In het deelvenster met eigenschappen voor de *gegevens exporteren* -module, klikt u op het pictogram aan de bovenkant rechts van de **gegevens tabelnaam** veld en selecteert u **instellen als web Serviceparameter**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="b23e2-145">Aan de onderkant van de *gegevens exporteren* eigenschappendeelvenster module in de **Webserviceparameters** sectie, klikt u op databasequery en wijzig deze met een Query.</span><span class="sxs-lookup"><span data-stu-id="b23e2-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="b23e2-146">Klik op **gegevens tabelnaam** en wijzig de naam **tabel**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="b23e2-147">Wanneer u klaar bent, is uw experiment moet er ongeveer als de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="b23e2-147">When you are done, your experiment should look similar to the following image:</span></span>

![Laatste uiterlijk van experiment.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="b23e2-149">U kunt nu het experiment implementeren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="b23e2-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="b23e2-150">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="b23e2-150">Deploy the web service</span></span>
<span data-ttu-id="b23e2-151">U kunt implementeren op een klassiek of een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="b23e2-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="b23e2-152">Een klassieke webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="b23e2-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="b23e2-153">Als een klassieke webservice implementeert en een toepassing gebruiken voor het maken:</span><span class="sxs-lookup"><span data-stu-id="b23e2-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="b23e2-154">Klik op uitvoeren aan de onderkant van het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="b23e2-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="b23e2-155">Wanneer de uitvoering is voltooid, klikt u op **webservice implementeren** en selecteer **webservice implementeren [klassieke]**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="b23e2-156">Zoek uw API-sleutel op het web service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b23e2-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="b23e2-157">Kopiëren en opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="b23e2-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="b23e2-158">In de **standaard eindpunt** tabel, klikt u op de **Batchuitvoering** koppeling naar de API-pagina te openen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="b23e2-159">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="b23e2-160">Op de pagina API Help vinden de **voorbeeldcode** sectie aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="b23e2-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="b23e2-161">Kopieer en plak de C#-voorbeeldcode in uw Program.cs-bestand en verwijder alle verwijzingen naar de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="b23e2-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="b23e2-162">Werk de waarde van de *apiKey* variabele met de API-sleutel eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="b23e2-163">Zoek de declaratie van de aanvraag en werk de waarden van de Webserviceparameters die worden doorgegeven aan de *importgegevens* en *gegevens exporteren* modules.</span><span class="sxs-lookup"><span data-stu-id="b23e2-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="b23e2-164">In dit geval u gebruikt u de oorspronkelijke query, maar de naam van een nieuwe tabel te definiëren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="b23e2-165">Voer de toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="b23e2-165">Run the application.</span></span> 

<span data-ttu-id="b23e2-166">Na voltooiing van de cyclus wordt een nieuwe tabel toegevoegd aan de database met de resultaten van score berekenen.</span><span class="sxs-lookup"><span data-stu-id="b23e2-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="b23e2-167">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="b23e2-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="b23e2-168">Voor het implementeren van een nieuwe webservice moet u voldoende machtigingen hebben in het abonnement waaraan u de webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="b23e2-169">Zie voor meer informatie [beheren van een webservice via de portal voor Azure Machine Learning-webservices](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="b23e2-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="b23e2-170">Als een nieuwe webservice implementeert en een toepassing gebruiken voor het maken:</span><span class="sxs-lookup"><span data-stu-id="b23e2-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="b23e2-171">Klik aan de onderkant van het experimentcanvas **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="b23e2-172">Wanneer de uitvoering is voltooid, klikt u op **webservice implementeren** en selecteer **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="b23e2-173">Voer een naam voor uw webservice op de pagina Experiment implementeren en een prijscategorie selecteren en klik vervolgens op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="b23e2-174">Op de **Quick Start** pagina, klikt u op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="b23e2-175">In de **voorbeeldcode** sectie, klikt u op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="b23e2-176">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="b23e2-177">Kopieer en plak de C#-voorbeeldcode in uw Program.cs-bestand.</span><span class="sxs-lookup"><span data-stu-id="b23e2-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="b23e2-178">Werk de waarde van de *apiKey* variabele met de **primaire sleutel** zich in de **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="b23e2-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="b23e2-179">Zoek de *scoreRequest* declaratie en werk de waarden van de Webserviceparameters die worden doorgegeven aan de *importgegevens* en *gegevens exporteren* modules.</span><span class="sxs-lookup"><span data-stu-id="b23e2-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="b23e2-180">In dit geval u gebruikt u de oorspronkelijke query, maar de naam van een nieuwe tabel te definiëren.</span><span class="sxs-lookup"><span data-stu-id="b23e2-180">In this case, you use the original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="b23e2-181">Voer de toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="b23e2-181">Run the application.</span></span> 

