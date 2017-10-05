---
title: Uitbreiden met R in Azure Data Lake Analytics U-SQL-scripts | Microsoft Docs
description: Meer informatie over het R-code in de U-SQL-Scripts uitvoeren
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="d3830-103">Zelfstudie: Aan de slag met de U-SQL met R uitbreiden</span><span class="sxs-lookup"><span data-stu-id="d3830-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="d3830-104">Het volgende voorbeeld wordt de basisstappen voor het implementeren van R-code:</span><span class="sxs-lookup"><span data-stu-id="d3830-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="d3830-105">Gebruik de `REFERENCE ASSEMBLY` instructie R uitbreidingen inschakelen voor de U-SQL-Script.</span><span class="sxs-lookup"><span data-stu-id="d3830-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="d3830-106">Gebruik de` REDUCE` bewerking voor het partitioneren van de invoergegevens voor een sleutel.</span><span class="sxs-lookup"><span data-stu-id="d3830-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="d3830-107">De R-uitbreidingen voor de U-SQL bevatten een ingebouwde reducer (`Extension.R.Reducer`) die op elk hoekpunt toegewezen aan de reducer R code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3830-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="d3830-108">Informatie over het gebruik van speciale met de naam gegevensframes aangeroepen `inputFromUSQL` en `outputToUSQL `respectievelijk naar het doorgeven van gegevens tussen de U-SQL en R. invoer en uitvoer DataFrame id-namen zijn opgelost (dat wil zeggen, gebruikers niet wijzigen van deze vooraf gedefinieerde namen van de invoer en uitvoer DataFrame-id's).</span><span class="sxs-lookup"><span data-stu-id="d3830-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="d3830-109">R code insluiten in de U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="d3830-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="d3830-110">U kunt de R code de U-SQL-script met behulp van de opdrachtparameter inline de `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="d3830-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="d3830-111">U kunt bijvoorbeeld het R-script als een string-variabele te declareren en als een parameter doorgeven aan de Reducer.</span><span class="sxs-lookup"><span data-stu-id="d3830-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="d3830-112">De R-code in een afzonderlijk bestand opslaan en verwijzen naar de U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="d3830-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="d3830-113">Het volgende voorbeeld ziet u een complexere gebruik.</span><span class="sxs-lookup"><span data-stu-id="d3830-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="d3830-114">In dit geval wordt de R-code geïmplementeerd als een RESOURCE die de U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="d3830-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="d3830-115">Sla deze R-code als een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="d3830-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="d3830-116">Gebruik een U-SQL-script wilt implementeren die R-script met de instructie RESOURCE implementeren.</span><span class="sxs-lookup"><span data-stu-id="d3830-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="d3830-117">Hoe R integreert met U-SQL</span><span class="sxs-lookup"><span data-stu-id="d3830-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="d3830-118">Gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="d3830-118">Datatypes</span></span>
* <span data-ttu-id="d3830-119">Zo worden geconverteerd als tekenreeks en numerieke kolommen uit de U-SQL-tussen R DataFrame en U-SQL [ondersteunde typen: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="d3830-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="d3830-120">De `Factor` gegevenstype wordt niet ondersteund in de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d3830-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="d3830-121">`byte[]`Als een base64-codering moet worden geserialiseerd `string`.</span><span class="sxs-lookup"><span data-stu-id="d3830-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="d3830-122">U-SQL-tekenreeksen kunnen worden geconverteerd naar factoren in R code, wanneer U-SQL maakt R invoer dataframe of door de parameter reducer `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="d3830-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="d3830-123">Schema 's</span><span class="sxs-lookup"><span data-stu-id="d3830-123">Schemas</span></span>
* <span data-ttu-id="d3830-124">U-SQL-gegevenssets kunnen geen dubbele kolomnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="d3830-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="d3830-125">U-SQL gegevenssets kolomnamen moeten tekenreeksen zijn.</span><span class="sxs-lookup"><span data-stu-id="d3830-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="d3830-126">Kolomnamen moet hetzelfde zijn in U-SQL en R-scripts.</span><span class="sxs-lookup"><span data-stu-id="d3830-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="d3830-127">ReadOnly-kolom kan geen deel uitmaken van de dataframe uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d3830-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="d3830-128">Omdat readonly-kolommen worden automatisch terug in de U-SQL-tabel ingevoegd als het een deel van het uitvoerschema van UDO.</span><span class="sxs-lookup"><span data-stu-id="d3830-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="d3830-129">Functionele beperkingen</span><span class="sxs-lookup"><span data-stu-id="d3830-129">Functional limitations</span></span>
* <span data-ttu-id="d3830-130">De R-Engine kan niet tweemaal in hetzelfde proces worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3830-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="d3830-131">U-SQL biedt momenteel geen ondersteuning voor Combiner UDO's voor de prognose gepartitioneerde modellen die worden gegenereerd met Reducer UDO's met.</span><span class="sxs-lookup"><span data-stu-id="d3830-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="d3830-132">Gebruikers kunnen de gepartitioneerde modellen declareren als bron en deze gebruiken in hun R-Script (Zie voorbeeldcode `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="d3830-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="d3830-133">R-versies</span><span class="sxs-lookup"><span data-stu-id="d3830-133">R Versions</span></span>
<span data-ttu-id="d3830-134">Alleen R 3.2.2 wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d3830-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="d3830-135">Standaard-R-modules</span><span class="sxs-lookup"><span data-stu-id="d3830-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="d3830-136">Invoer en uitvoer groottebeperkingen</span><span class="sxs-lookup"><span data-stu-id="d3830-136">Input and Output size limitations</span></span>
<span data-ttu-id="d3830-137">Elke hoekpunt heeft een beperkte hoeveelheid geheugen die zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d3830-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="d3830-138">Omdat de invoer en uitvoer DataFrames moet bestaan in het geheugen van de R-code, kan de totale grootte voor de invoer en uitvoer kan niet groter zijn dan 500 MB.</span><span class="sxs-lookup"><span data-stu-id="d3830-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="d3830-139">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="d3830-139">Sample Code</span></span>
<span data-ttu-id="d3830-140">Meer voorbeelden van code is beschikbaar in uw Data Lake Store-account nadat u de U-SQL Advanced Analytics extensions installeren.</span><span class="sxs-lookup"><span data-stu-id="d3830-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="d3830-141">Het pad voor meer voorbeelden van code is: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="d3830-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="d3830-142">Aangepaste R-modules met U-SQL implementeren</span><span class="sxs-lookup"><span data-stu-id="d3830-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="d3830-143">Maak eerst een aangepaste R-module en het zip- en vervolgens het gecomprimeerde R aangepaste module-bestand uploaden naar uw winkel ADL.</span><span class="sxs-lookup"><span data-stu-id="d3830-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="d3830-144">In het voorbeeld gaat we magittr_1.5.zip uploaden naar de hoofdmap van het standaard ADLS-account voor het ADLA-account dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d3830-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="d3830-145">Zodra u de module naar ADL store uploaden, declareert u deze als RESOURCE implementeren zodat deze beschikbaar in de U-SQL-scripts en aanroep gebruik `install.packages` om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="d3830-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="d3830-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3830-146">Next Steps</span></span>
* [<span data-ttu-id="d3830-147">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d3830-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d3830-148">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3830-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="d3830-149">U-SQL-vensterfuncties gebruiken voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="d3830-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
