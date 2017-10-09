---
title: aaaExtend U-SQL-scripts met R in Azure Data Lake Analytics | Microsoft Docs
description: Meer informatie over hoe toorun R code in de U-SQL-Scripts
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="14e41-103">Zelfstudie: Aan de slag met de U-SQL met R uitbreiden</span><span class="sxs-lookup"><span data-stu-id="14e41-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="14e41-104">Hallo volgende voorbeeld illustreert Hallo basisstappen voor het implementeren van R-code:</span><span class="sxs-lookup"><span data-stu-id="14e41-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="14e41-105">Gebruik Hallo `REFERENCE ASSEMBLY` instructie tooenable R uitbreidingen voor Hallo U-SQL-Script.</span><span class="sxs-lookup"><span data-stu-id="14e41-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="14e41-106">Gebruik de` REDUCE` bewerking toopartition Hallo invoergegevens voor een sleutel.</span><span class="sxs-lookup"><span data-stu-id="14e41-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="14e41-107">Hallo R-uitbreidingen voor de U-SQL bevatten een ingebouwde reducer (`Extension.R.Reducer`) die op elke hoekpunt toegewezen toohello reducer R code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14e41-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="14e41-108">Informatie over het gebruik van speciale met de naam gegevensframes aangeroepen `inputFromUSQL` en `outputToUSQL `respectievelijk toopass gegevens tussen de U-SQL en R. invoer en uitvoer DataFrame id-namen zijn opgelost (dat wil zeggen, gebruikers niet wijzigen van deze vooraf gedefinieerde namen van de invoer en uitvoer DataFrame id's).</span><span class="sxs-lookup"><span data-stu-id="14e41-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="14e41-109">R code insluiten in Hallo U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="14e41-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="14e41-110">U kunt Hallo R Inlinecode uw U-SQL-script met behulp van de opdrachtparameter Hallo Hallo `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="14e41-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="14e41-111">U kunt bijvoorbeeld Hallo R-script als een string-variabele te declareren en geven deze als een parameter toohello Reducer.</span><span class="sxs-lookup"><span data-stu-id="14e41-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="14e41-112">Hallo R-code in een afzonderlijk bestand behouden en verwijst u Hallo U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="14e41-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="14e41-113">Hallo volgende voorbeeld ziet u een complexere gebruik.</span><span class="sxs-lookup"><span data-stu-id="14e41-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="14e41-114">In dit geval is Hallo R-code geïmplementeerd als een RESOURCE die Hallo U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="14e41-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="14e41-115">Sla deze R-code als een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="14e41-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="14e41-116">Gebruik een U-SQL-script toodeploy die R-script met Hallo implementeren RESOURCE-instructie.</span><span class="sxs-lookup"><span data-stu-id="14e41-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="14e41-117">Hoe R integreert met U-SQL</span><span class="sxs-lookup"><span data-stu-id="14e41-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="14e41-118">Gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="14e41-118">Datatypes</span></span>
* <span data-ttu-id="14e41-119">Zo worden geconverteerd als tekenreeks en numerieke kolommen uit de U-SQL-tussen R DataFrame en U-SQL [ondersteunde typen: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="14e41-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="14e41-120">Hallo `Factor` gegevenstype wordt niet ondersteund in de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="14e41-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="14e41-121">`byte[]`Als een base64-codering moet worden geserialiseerd `string`.</span><span class="sxs-lookup"><span data-stu-id="14e41-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="14e41-122">U-SQL-tekenreeksen geconverteerde toofactors in R-code kunnen worden wanneer U-SQL maakt R invoer dataframe of door de instelling Hallo reducer parameter `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="14e41-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="14e41-123">Schema 's</span><span class="sxs-lookup"><span data-stu-id="14e41-123">Schemas</span></span>
* <span data-ttu-id="14e41-124">U-SQL-gegevenssets kunnen geen dubbele kolomnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="14e41-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="14e41-125">U-SQL gegevenssets kolomnamen moeten tekenreeksen zijn.</span><span class="sxs-lookup"><span data-stu-id="14e41-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="14e41-126">Kolomnamen moet hetzelfde zijn in de U-SQL en R scripts Hallo.</span><span class="sxs-lookup"><span data-stu-id="14e41-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="14e41-127">ReadOnly-kolom kan niet worden opgenomen Hallo uitvoer dataframe.</span><span class="sxs-lookup"><span data-stu-id="14e41-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="14e41-128">Omdat readonly-kolommen worden automatisch terug in de U-SQL-tabel Hallo geïnjecteerd als het uitvoerschema van van UDO deel uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="14e41-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="14e41-129">Functionele beperkingen</span><span class="sxs-lookup"><span data-stu-id="14e41-129">Functional limitations</span></span>
* <span data-ttu-id="14e41-130">Hallo R-Engine kan niet worden gemaakt tweemaal in hetzelfde proces Hallo.</span><span class="sxs-lookup"><span data-stu-id="14e41-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="14e41-131">U-SQL biedt momenteel geen ondersteuning voor Combiner UDO's voor de prognose gepartitioneerde modellen die worden gegenereerd met Reducer UDO's met.</span><span class="sxs-lookup"><span data-stu-id="14e41-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="14e41-132">Gebruikers kunnen Hallo gepartitioneerd modellen declareren als bron en deze gebruiken in hun R-Script (Zie voorbeeldcode `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="14e41-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="14e41-133">R-versies</span><span class="sxs-lookup"><span data-stu-id="14e41-133">R Versions</span></span>
<span data-ttu-id="14e41-134">Alleen R 3.2.2 wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="14e41-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="14e41-135">Standaard-R-modules</span><span class="sxs-lookup"><span data-stu-id="14e41-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="14e41-136">Invoer en uitvoer groottebeperkingen</span><span class="sxs-lookup"><span data-stu-id="14e41-136">Input and Output size limitations</span></span>
<span data-ttu-id="14e41-137">Elke hoekpunt heeft een beperkte hoeveelheid geheugen die tooit is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="14e41-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="14e41-138">Omdat hello invoer en uitvoer DataFrames moet bestaan in het geheugen van Hallo R code, kan niet Hallo totale voor Hallo invoer en uitvoer groter zijn dan 500 MB.</span><span class="sxs-lookup"><span data-stu-id="14e41-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="14e41-139">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="14e41-139">Sample Code</span></span>
<span data-ttu-id="14e41-140">Meer voorbeelden van code is beschikbaar in uw Data Lake Store-account nadat u Hallo U-SQL Advanced Analytics extensions installeren.</span><span class="sxs-lookup"><span data-stu-id="14e41-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="14e41-141">Hallo-pad voor meer voorbeelden van code is: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="14e41-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="14e41-142">Aangepaste R-modules met U-SQL implementeren</span><span class="sxs-lookup"><span data-stu-id="14e41-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="14e41-143">Eerst maakt u een aangepaste R-module en het zip- en vervolgens uploaden Hallo ingepakte R aangepaste module tooyour ADL archief.</span><span class="sxs-lookup"><span data-stu-id="14e41-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="14e41-144">In voorbeeld Hallo wordt we uploaden magittr_1.5.zip toohello hoofdmap van Hallo standaard ADLS-account voor Hallo ADLA account dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="14e41-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="14e41-145">Zodra u Hallo module tooADL store uploadt, declareert u deze RESOURCE implementeren toomake gebruiken deze beschikbaar zijn in uw U-SQL-script en de aanroep `install.packages` tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="14e41-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="14e41-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14e41-146">Next Steps</span></span>
* [<span data-ttu-id="14e41-147">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="14e41-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="14e41-148">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14e41-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="14e41-149">U-SQL-vensterfuncties gebruiken voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="14e41-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
