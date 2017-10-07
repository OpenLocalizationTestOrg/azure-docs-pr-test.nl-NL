---
title: aaaUsing Import/Export-gegevens in Azure Machine Learning-webservices | Microsoft Docs
description: Ontdek hoe toouse Hallo modules toosend voor gegevens importeren en exporteren van gegevens en gegevens ontvangen van een webservice.
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
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="f6e54-103">Azure ML-webservices implementeren die gebruikmaken van gegevensimport- en gegevensexportmodules</span><span class="sxs-lookup"><span data-stu-id="f6e54-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="f6e54-104">Wanneer u een Voorspellend experiment maakt, voegt u gewoonlijk toe een web service invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f6e54-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="f6e54-105">Wanneer u een experiment Hallo implementeert, kunnen consumenten verzenden en ontvangen van gegevens van de webservice Hallo via Hallo invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f6e54-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="f6e54-106">Voor sommige toepassingen van de consumer gegevens uit een gegevensfeed beschikbaar of al bevinden zich in een externe gegevensbron zoals Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f6e54-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="f6e54-107">In dergelijke gevallen hoeven ze niet lezen en schrijven van gegevens met behulp van web service in- en uitgangen.</span><span class="sxs-lookup"><span data-stu-id="f6e54-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="f6e54-108">Ze kunnen in plaats daarvan Hallo Batch uitvoering Service (BES) tooread gegevens uit het Hallo-gegevensbron met behulp van een module gegevens importeren gebruiken en schrijf Hallo score berekenen voor resultaten andere gegevenslocatie tooa met behulp van een module gegevens exporteren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="f6e54-109">Hallo kunnen gegevens importeren en exporteren gegevens modules, lezen uit en schrijven toovarious gegevens locaties zoals een via HTTP, een Hive-Query, een Azure SQL-database, Azure Table storage, Azure Blob storage, een Gegevensfeed-URL opgeven of een lokale SQL-database.</span><span class="sxs-lookup"><span data-stu-id="f6e54-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="f6e54-110">In dit onderwerp maakt gebruik van Hallo ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' steekproef en wordt ervan uitgegaan dat Hallo dataset al is geladen in een Azure SQL-tabel met de naam censusdata.</span><span class="sxs-lookup"><span data-stu-id="f6e54-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="f6e54-111">Hallo trainingsexperiment maken</span><span class="sxs-lookup"><span data-stu-id="f6e54-111">Create hello training experiment</span></span>
<span data-ttu-id="f6e54-112">Wanneer u opent Hallo ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' voorbeeld van gebruikt Hallo voorbeeldgegevensset volwassenen inventarisering Income binaire classificatie.</span><span class="sxs-lookup"><span data-stu-id="f6e54-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="f6e54-113">En Hallo experiment in Hallo canvas eruit vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6e54-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![De aanvankelijke configuratie van Hallo experiment.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="f6e54-115">tooread hello gegevens uit hello Azure SQL-tabel:</span><span class="sxs-lookup"><span data-stu-id="f6e54-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="f6e54-116">Hallo gegevensset module verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f6e54-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="f6e54-117">Typ in Hallo-onderdelen in het zoekvak importeren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="f6e54-118">Lijst met resultaten Hallo toevoegen een *importgegevens* module toohello experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="f6e54-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="f6e54-119">Verbinding maken met de uitvoer van Hallo *importgegevens* module-invoer Hallo Hallo *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="f6e54-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="f6e54-120">Selecteer in het eigenschappendeelvenster **Azure SQL Database** in Hallo **gegevensbron** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f6e54-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="f6e54-121">In Hallo **databaseservernaam**, **databasenaam**, **gebruikersnaam**, en **wachtwoord** velden, voer de juiste gegevens Hallo voor uw database.</span><span class="sxs-lookup"><span data-stu-id="f6e54-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="f6e54-122">Voer in query-databaseveld met Hallo Hallo volgende query.</span><span class="sxs-lookup"><span data-stu-id="f6e54-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="f6e54-123">Selecteer [leeftijd]</span><span class="sxs-lookup"><span data-stu-id="f6e54-123">select [age],</span></span>
   
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
     <span data-ttu-id="f6e54-124">van dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="f6e54-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="f6e54-125">Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="f6e54-126">Hallo Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="f6e54-126">Create hello predictive experiment</span></span>
<span data-ttu-id="f6e54-127">De volgende instellen van Hallo Voorspellend experiment van waaruit u uw webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="f6e54-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="f6e54-128">Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **voorspellende Web Service (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="f6e54-129">Hallo verwijderen *Web Service invoer* en *Web Service uitvoer modules* van Hallo Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="f6e54-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="f6e54-130">Typ in Hallo-onderdelen in het zoekvak exporteren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="f6e54-131">Lijst met resultaten Hallo toevoegen een *gegevens exporteren* module toohello experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="f6e54-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="f6e54-132">Verbinding maken met de uitvoer van Hallo *Score Model* module-invoer Hallo Hallo *gegevens exporteren* module.</span><span class="sxs-lookup"><span data-stu-id="f6e54-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="f6e54-133">Selecteer in het eigenschappendeelvenster **Azure SQL Database** Hallo gegevens bestemming vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f6e54-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="f6e54-134">In Hallo **databaseservernaam**, **databasenaam**, **Server gebruikersaccountnaam**, en **Server het wachtwoord voor gebruikersaccount** velden invoeren Hallo relevante informatie voor uw database.</span><span class="sxs-lookup"><span data-stu-id="f6e54-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="f6e54-135">In Hallo **met door komma's gescheiden lijst met kolommen toobe opgeslagen** veld, typt u Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="f6e54-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="f6e54-136">In Hallo **gegevensveld tabel naam**, typt u dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="f6e54-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="f6e54-137">Als Hallo tabel niet bestaat, wordt deze gemaakt wanneer Hallo experiment wordt uitgevoerd of Hallo-webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f6e54-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="f6e54-138">In Hallo **door komma's gescheiden lijst met kolommen datatable** veld ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="f6e54-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="f6e54-139">Wanneer u een toepassing schrijft dat aanroepen laatste webservice hello, kunt u toospecify een andere query- of doelserver invoertabel tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="f6e54-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="f6e54-140">tooconfigure deze invoer en uitvoer, gebruik Hallo Webserviceparameters functie tooset hello *importgegevens* module *gegevensbron* eigenschap en Hallo *gegevens exporteren* modus de eigenschap destination gegevens.</span><span class="sxs-lookup"><span data-stu-id="f6e54-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="f6e54-141">Zie voor meer informatie over Webserviceparameters hello [Webserviceparameters AzureML-vermelding](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) op Hallo Cortana Intelligence en Machine Learning-Blog.</span><span class="sxs-lookup"><span data-stu-id="f6e54-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="f6e54-142">tooconfigure hello Webserviceparameters voor Hallo importeren query en doeltabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="f6e54-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="f6e54-143">In het eigenschappendeelvenster Hallo voor Hallo *gegevens importeren* -module, klik op Hallo Hallo pictogram rechts van Hallo top **databasequery** veld en selecteert u **instellen als web Serviceparameter**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="f6e54-144">In het eigenschappendeelvenster Hallo voor Hallo *gegevens exporteren* -module, klik op Hallo Hallo pictogram rechts van Hallo top **gegevens tabelnaam** veld en selecteert u **instellen als web service**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="f6e54-145">Hallo Hallo onderaan in *gegevens exporteren* eigenschappendeelvenster van de module in Hallo **Webserviceparameters** sectie, klikt u op databasequery en wijzig deze met een Query.</span><span class="sxs-lookup"><span data-stu-id="f6e54-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="f6e54-146">Klik op **gegevens tabelnaam** en wijzig de naam **tabel**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="f6e54-147">Wanneer u klaar bent, ziet uw experiment vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6e54-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Laatste uiterlijk van experiment.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="f6e54-149">U kunt nu Hallo experiment implementeren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="f6e54-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="f6e54-150">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="f6e54-150">Deploy hello web service</span></span>
<span data-ttu-id="f6e54-151">U kunt tooeither een klassiek of nieuw webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="f6e54-152">Een klassieke webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="f6e54-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="f6e54-153">toodeploy als een klassieke webservice en maken van een toepassing tooconsume het:</span><span class="sxs-lookup"><span data-stu-id="f6e54-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="f6e54-154">Klik op uitvoeren Hallo onderaan Hallo experimentcanvas in.</span><span class="sxs-lookup"><span data-stu-id="f6e54-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="f6e54-155">Wanneer Hallo uitgevoerd is voltooid, klikt u op **webservice implementeren** en selecteer **webservice implementeren [klassieke]**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="f6e54-156">Zoek uw API-sleutel op Hallo web servicedashboard.</span><span class="sxs-lookup"><span data-stu-id="f6e54-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="f6e54-157">Kopieer en sla toouse later.</span><span class="sxs-lookup"><span data-stu-id="f6e54-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="f6e54-158">In Hallo **standaard eindpunt** tabel, klikt u op Hallo **Batchuitvoering** koppeling tooopen Hallo API Help-pagina.</span><span class="sxs-lookup"><span data-stu-id="f6e54-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="f6e54-159">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="f6e54-160">Hallo zoeken op Hallo API Help-pagina, **voorbeeldcode** sectie Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f6e54-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="f6e54-161">Kopiëren en plakken Hallo C#-voorbeeldcode in uw Program.cs-bestand, en verwijder alle verwijzingen toohello blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f6e54-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="f6e54-162">Werk de waarde Hallo Hallo *apiKey* variabele met Hallo API-sleutel eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f6e54-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="f6e54-163">Zoek Hallo aanvraag declaratie en bij te werken Hallo waarden van Web Service Parameters die zijn doorgegeven toohello *importgegevens* en *gegevens exporteren* modules.</span><span class="sxs-lookup"><span data-stu-id="f6e54-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="f6e54-164">In dit geval u Hallo oorspronkelijke query gebruiken, maar de naam van een nieuwe tabel definiëren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="f6e54-165">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-165">Run hello application.</span></span> 

<span data-ttu-id="f6e54-166">Na voltooiing van Hallo uitvoert, wordt een nieuwe tabel toohello database Hallo score berekenen resultaten met toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f6e54-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="f6e54-167">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="f6e54-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="f6e54-168">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="f6e54-169">Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f6e54-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="f6e54-170">toodeploy als een nieuwe webservice en maken van een toepassing tooconsume het:</span><span class="sxs-lookup"><span data-stu-id="f6e54-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="f6e54-171">Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="f6e54-172">Wanneer Hallo uitgevoerd is voltooid, klikt u op **webservice implementeren** en selecteer **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="f6e54-173">Voer een naam voor uw web-service op Hallo implementeren Experiment pagina en een prijscategorie selecteren en klik vervolgens op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="f6e54-174">Op Hallo **Quick Start** pagina, klikt u op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="f6e54-175">In Hallo **voorbeeldcode** sectie, klikt u op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="f6e54-176">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f6e54-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="f6e54-177">Kopieer en plak Hallo C# voorbeeldcode in uw Program.cs-bestand.</span><span class="sxs-lookup"><span data-stu-id="f6e54-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="f6e54-178">Werk de waarde Hallo Hallo *apiKey* variabele Hello **primaire sleutel** zich in Hallo **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="f6e54-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="f6e54-179">Zoek Hallo *scoreRequest* declaratie en update Hallo-waarden van de Webserviceparameters die zijn doorgegeven toohello *importgegevens* en *gegevens exporteren* modules.</span><span class="sxs-lookup"><span data-stu-id="f6e54-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="f6e54-180">In dit geval u Hallo oorspronkelijke query gebruiken, maar de naam van een nieuwe tabel definiëren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-180">In this case, you use hello original query, but define a new table name.</span></span>
   
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
10. <span data-ttu-id="f6e54-181">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6e54-181">Run hello application.</span></span> 

