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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Zelfstudie: Aan de slag met de U-SQL met R uitbreiden

Hallo volgende voorbeeld illustreert Hallo basisstappen voor het implementeren van R-code:
* Gebruik Hallo `REFERENCE ASSEMBLY` instructie tooenable R uitbreidingen voor Hallo U-SQL-Script.
* Gebruik de` REDUCE` bewerking toopartition Hallo invoergegevens voor een sleutel.
* Hallo R-uitbreidingen voor de U-SQL bevatten een ingebouwde reducer (`Extension.R.Reducer`) die op elke hoekpunt toegewezen toohello reducer R code wordt uitgevoerd. 
* Informatie over het gebruik van speciale met de naam gegevensframes aangeroepen `inputFromUSQL` en `outputToUSQL `respectievelijk toopass gegevens tussen de U-SQL en R. invoer en uitvoer DataFrame id-namen zijn opgelost (dat wil zeggen, gebruikers niet wijzigen van deze vooraf gedefinieerde namen van de invoer en uitvoer DataFrame id's).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>R code insluiten in Hallo U-SQL-script

U kunt Hallo R Inlinecode uw U-SQL-script met behulp van de opdrachtparameter Hallo Hallo `Extension.R.Reducer`. U kunt bijvoorbeeld Hallo R-script als een string-variabele te declareren en geven deze als een parameter toohello Reducer.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Hallo R-code in een afzonderlijk bestand behouden en verwijst u Hallo U-SQL-script

Hallo volgende voorbeeld ziet u een complexere gebruik. In dit geval is Hallo R-code geïmplementeerd als een RESOURCE die Hallo U-SQL-script.

Sla deze R-code als een afzonderlijk bestand.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Gebruik een U-SQL-script toodeploy die R-script met Hallo implementeren RESOURCE-instructie.

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

## <a name="how-r-integrates-with-u-sql"></a>Hoe R integreert met U-SQL

### <a name="datatypes"></a>Gegevenstypen
* Zo worden geconverteerd als tekenreeks en numerieke kolommen uit de U-SQL-tussen R DataFrame en U-SQL [ondersteunde typen: `double`, `string`, `bool`, `integer`, `byte`].
* Hallo `Factor` gegevenstype wordt niet ondersteund in de U-SQL.
* `byte[]`Als een base64-codering moet worden geserialiseerd `string`.
* U-SQL-tekenreeksen geconverteerde toofactors in R-code kunnen worden wanneer U-SQL maakt R invoer dataframe of door de instelling Hallo reducer parameter `stringsAsFactors: true`.

### <a name="schemas"></a>Schema 's
* U-SQL-gegevenssets kunnen geen dubbele kolomnamen hebben.
* U-SQL gegevenssets kolomnamen moeten tekenreeksen zijn.
* Kolomnamen moet hetzelfde zijn in de U-SQL en R scripts Hallo.
* ReadOnly-kolom kan niet worden opgenomen Hallo uitvoer dataframe. Omdat readonly-kolommen worden automatisch terug in de U-SQL-tabel Hallo geïnjecteerd als het uitvoerschema van van UDO deel uitmaakt.

### <a name="functional-limitations"></a>Functionele beperkingen
* Hallo R-Engine kan niet worden gemaakt tweemaal in hetzelfde proces Hallo. 
* U-SQL biedt momenteel geen ondersteuning voor Combiner UDO's voor de prognose gepartitioneerde modellen die worden gegenereerd met Reducer UDO's met. Gebruikers kunnen Hallo gepartitioneerd modellen declareren als bron en deze gebruiken in hun R-Script (Zie voorbeeldcode `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>R-versies
Alleen R 3.2.2 wordt ondersteund.

### <a name="standard-r-modules"></a>Standaard-R-modules

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

### <a name="input-and-output-size-limitations"></a>Invoer en uitvoer groottebeperkingen
Elke hoekpunt heeft een beperkte hoeveelheid geheugen die tooit is toegewezen. Omdat hello invoer en uitvoer DataFrames moet bestaan in het geheugen van Hallo R code, kan niet Hallo totale voor Hallo invoer en uitvoer groter zijn dan 500 MB.

### <a name="sample-code"></a>Voorbeeldcode
Meer voorbeelden van code is beschikbaar in uw Data Lake Store-account nadat u Hallo U-SQL Advanced Analytics extensions installeren. Hallo-pad voor meer voorbeelden van code is: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Aangepaste R-modules met U-SQL implementeren

Eerst maakt u een aangepaste R-module en het zip- en vervolgens uploaden Hallo ingepakte R aangepaste module tooyour ADL archief. In voorbeeld Hallo wordt we uploaden magittr_1.5.zip toohello hoofdmap van Hallo standaard ADLS-account voor Hallo ADLA account dat wordt gebruikt. Zodra u Hallo module tooADL store uploadt, declareert u deze RESOURCE implementeren toomake gebruiken deze beschikbaar zijn in uw U-SQL-script en de aanroep `install.packages` tooinstall deze.

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

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [U-SQL-vensterfuncties gebruiken voor Azure Data Lake Analytics-taken](data-lake-analytics-use-window-functions.md)
