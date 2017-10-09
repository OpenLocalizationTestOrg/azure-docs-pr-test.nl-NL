---
title: AAA(deprecated) Survival analyse met Azure Machine Learning | Microsoft Docs
description: (afgeschaft) Survival Analysis gebeurtenis exemplaar kans
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="4d40d-103">(afgeschaft) Survival analyse</span><span class="sxs-lookup"><span data-stu-id="4d40d-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="4d40d-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="4d40d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4d40d-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4d40d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4d40d-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4d40d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4d40d-107">Onder veel scenario's is de belangrijkste uitkomst Hallo onder assessment Hallo tijd tooan gebeurtenis van belang.</span><span class="sxs-lookup"><span data-stu-id="4d40d-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="4d40d-108">Met andere woorden, Hallo vraag 'wanneer deze gebeurtenis wordt uitgevoerd?'</span><span class="sxs-lookup"><span data-stu-id="4d40d-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="4d40d-109">wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="4d40d-109">is asked.</span></span> <span data-ttu-id="4d40d-110">Voorbeelden, kunt u beter situaties waarbij gegevens Hallo Hallo verstreken tijd (dagen, jaar, kilometers, enzovoort) beschrijft tot Hallo gebeurtenis van belang (ziekte relapse, PhD mate ontvangen, bedient pad fout).</span><span class="sxs-lookup"><span data-stu-id="4d40d-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="4d40d-111">Elk exemplaar in Hallo gegevens vertegenwoordigt een specifiek object (een geduld, een student, een auto, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="4d40d-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4d40d-112">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) beantwoordt Hallo vraag 'Wat is er Hallo-kans dat Hallo gebeurtenis van belang optreden bij tijd n voor object x?'</span><span class="sxs-lookup"><span data-stu-id="4d40d-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="4d40d-113">Dankzij een voortdurende Analytics-model, deze webservice kunt gebruikers toosupply tootrain Hallo gegevensmodel en testen.</span><span class="sxs-lookup"><span data-stu-id="4d40d-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="4d40d-114">Hallo belangrijkste thema van Hallo experiment is toomodel Hallo Hallo verstreken tijd totdat Hallo van belang gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4d40d-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="4d40d-115">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="4d40d-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4d40d-116">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="4d40d-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="4d40d-117">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="4d40d-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4d40d-118">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="4d40d-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4d40d-119">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="4d40d-119">Consumption of web service</span></span>
<span data-ttu-id="4d40d-120">Hallo invoergegevens schema van Hallo-webservice wordt weergegeven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d40d-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="4d40d-121">Zes stukjes informatie nodig zijn als Hallo invoer: trainingsgegevens, testgegevens, tijd van belang, de index van de dimensie 'time' hello, Hallo index van de dimensie 'gebeurtenis' en Hallo variabele typen (doorlopende of factor).</span><span class="sxs-lookup"><span data-stu-id="4d40d-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="4d40d-122">Hallo trainingsgegevens wordt vertegenwoordigd door een tekenreeks, waarbij Hallo rijen worden gescheiden door een komma en Hallo kolommen worden gescheiden door puntkomma's.</span><span class="sxs-lookup"><span data-stu-id="4d40d-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="4d40d-123">Hallo aantal kenmerken van Hallo gegevens is flexibel.</span><span class="sxs-lookup"><span data-stu-id="4d40d-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="4d40d-124">Alle Hallo-elementen in de invoerreeks Hallo moet numeriek zijn.</span><span class="sxs-lookup"><span data-stu-id="4d40d-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="4d40d-125">Hallo trainingsgegevens wijst dimensie Hallo 'time' Hallo aantal tijdseenheden (dagen, jaar, kilometers, enz.) is verstreken sinds beginpunt Hallo Hallo bestuderen (een geduld ontvangen medicijn behandeling-programma's, een student begin PhD onderzoek, een auto toobe starten aangedreven, enz.) totdat hello van belang (Hallo geduld retourneren toodrug gebruik, Hallo studenten verkrijgen Hallo PhD mate, Hallo auto met bedient pad fout, enzovoort) gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4d40d-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="4d40d-126">Hallo 'gebeurtenis' dimensie geeft aan of Hallo-gebeurtenis van belang achter Hallo Hallo onderzoek plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="4d40d-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="4d40d-127">De waarde ' gebeurtenis = 1 "betekent dat de gebeurtenis van belang Hallo deze gebeurtenis treedt op tijdens het Hallo aangegeven door de dimensie 'time' hello; "gebeurtenis = 0 ' betekent dat Hallo gebeurtenis van belang is niet door Hallo tijd aangegeven door de dimensie 'time' hello opgetreden.</span><span class="sxs-lookup"><span data-stu-id="4d40d-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="4d40d-128">trainingdata - tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4d40d-128">trainingdata - A character string.</span></span> <span data-ttu-id="4d40d-129">Rijen worden gescheiden door een komma en kolommen worden gescheiden door puntkomma's.</span><span class="sxs-lookup"><span data-stu-id="4d40d-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="4d40d-130">Elke rij bevat ' tijddimensie ' en 'gebeurtenis' dimensie manier variabelen.</span><span class="sxs-lookup"><span data-stu-id="4d40d-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="4d40d-131">testingdata - één rij met gegevens op die manier variabelen voor een bepaald object bevat.</span><span class="sxs-lookup"><span data-stu-id="4d40d-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="4d40d-132">time_of_interest - Hallo verstreken tijd van belang n.</span><span class="sxs-lookup"><span data-stu-id="4d40d-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="4d40d-133">index_time - Hallo kolomindex van de dimensie 'time' hello (vanaf 1).</span><span class="sxs-lookup"><span data-stu-id="4d40d-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="4d40d-134">index_event - Hallo kolomindex van Hallo 'gebeurtenis' dimensie (vanaf 1).</span><span class="sxs-lookup"><span data-stu-id="4d40d-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="4d40d-135">variable_types - tekenreeks met puntkomma's als scheidingstekens in deze.</span><span class="sxs-lookup"><span data-stu-id="4d40d-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="4d40d-136">0 geeft aan dat continue variabelen en 1 factor variabelen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="4d40d-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="4d40d-137">Hallo-uitvoer is de kans op Hallo van een gebeurtenis optreedt op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="4d40d-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="4d40d-138">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="4d40d-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4d40d-139">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4d40d-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4d40d-140">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="4d40d-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="4d40d-141">Hallo interpretatie van deze test is als volgt.</span><span class="sxs-lookup"><span data-stu-id="4d40d-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="4d40d-142">Ervan uitgaande dat Hallo Hallo gegevens is bedoeld toomodel Hallo verstreken tijd tot Hallo toodrug gebruik retourneren voor Hallo patiënten heeft ontvangen van een van twee Hallo behandeling programma's.</span><span class="sxs-lookup"><span data-stu-id="4d40d-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="4d40d-143">Hallo uitvoer Hallo web service leesbewerkingen: voor patiënten wordt 35 jaar oude, met vorige productie medicijn behandeling 2 maal duurt Hallo lang huis behandeling programma, en met gebruik van zowel heroïne als cocaïne Hallo kans retourneren toohello medicijn gebruik 95.64% door is dag 500.</span><span class="sxs-lookup"><span data-stu-id="4d40d-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="4d40d-144">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="4d40d-144">Creation of web service</span></span>
> <span data-ttu-id="4d40d-145">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4d40d-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4d40d-146">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4d40d-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4d40d-147">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="4d40d-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="4d40d-148">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules op Hallo werkruimte zijn opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4d40d-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="4d40d-149">Hallo gegevensschema is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script], definieert een Hallo invoergegevens schema voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="4d40d-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="4d40d-150">Deze module wordt vervolgens gekoppeld toohello tweede [R-Script uitvoeren] [ execute-r-script] module waarmee werk grote.</span><span class="sxs-lookup"><span data-stu-id="4d40d-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="4d40d-151">Deze module biedt voorverwerking van gegevens, model bouwen en voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="4d40d-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="4d40d-152">In Hallo gegevens voorverwerking stap Hallo invoergegevens vertegenwoordigd door een lange tekenreeks getransformeerd en geconverteerd naar een gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="4d40d-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="4d40d-153">Een externe R-pakket 'survival_2.37 7.zip' is in Hallo model bouwen stap eerst geïnstalleerd voor de uitvoering van survival analyse.</span><span class="sxs-lookup"><span data-stu-id="4d40d-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="4d40d-154">De functie 'coxph' hello wordt vervolgens uitgevoerd na een reeks gegevensverwerkingstaken.</span><span class="sxs-lookup"><span data-stu-id="4d40d-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="4d40d-155">Hallo details van de functie 'coxph' Hallo voor survival analyse kunnen worden gelezen uit Hallo R-documentatie.</span><span class="sxs-lookup"><span data-stu-id="4d40d-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="4d40d-156">Een test-exemplaar is opgegeven in het getrainde model met de functie 'surfit' Hallo Hallo in Hallo voorspelling stap en Hallo survival curve voor dit exemplaar van de test wordt gegenereerd als de variabele 'curve'.</span><span class="sxs-lookup"><span data-stu-id="4d40d-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="4d40d-157">Ten slotte de kans op Hallo van Hallo-tijd van belang wordt verkregen.</span><span class="sxs-lookup"><span data-stu-id="4d40d-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="4d40d-158">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="4d40d-158">Experiment flow:</span></span>
![Experiment stroom][1]

#### <a name="module-1"></a><span data-ttu-id="4d40d-160">Module 1:</span><span class="sxs-lookup"><span data-stu-id="4d40d-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="4d40d-161">2-module:</span><span class="sxs-lookup"><span data-stu-id="4d40d-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="4d40d-162">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="4d40d-162">Limitations</span></span>
<span data-ttu-id="4d40d-163">Deze webservice kan alleen numerieke waarden duren als functie variabelen (kolommen).</span><span class="sxs-lookup"><span data-stu-id="4d40d-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="4d40d-164">de kolom 'event' Hello kan duren voordat de waarde 0 of 1.</span><span class="sxs-lookup"><span data-stu-id="4d40d-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="4d40d-165">Hallo 'time'-kolom moet een positief geheel getal toobe.</span><span class="sxs-lookup"><span data-stu-id="4d40d-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="4d40d-166">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="4d40d-166">FAQ</span></span>
<span data-ttu-id="4d40d-167">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4d40d-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

