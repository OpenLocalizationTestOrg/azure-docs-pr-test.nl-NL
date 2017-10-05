---
title: (afgeschaft) Survival-analyse met Azure Machine Learning | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="45c4b-103">(afgeschaft) Survival analyse</span><span class="sxs-lookup"><span data-stu-id="45c4b-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="45c4b-104">De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="45c4b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="45c4b-105">U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="45c4b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="45c4b-106">Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="45c4b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="45c4b-107">In veel scenario's is de belangrijkste uitkomst onder assessment de tijd op een gebeurtenis van belang.</span><span class="sxs-lookup"><span data-stu-id="45c4b-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="45c4b-108">Met andere woorden, de vraag "wanneer deze gebeurtenis wordt uitgevoerd?'</span><span class="sxs-lookup"><span data-stu-id="45c4b-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="45c4b-109">wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="45c4b-109">is asked.</span></span> <span data-ttu-id="45c4b-110">Voorbeelden, kunt u beter situaties waarbij de gegevens de verstreken tijd (dagen, jaar, kilometers, enzovoort beschrijft) tot en met de gebeurtenis van belang (ziekte relapse, PhD mate ontvangen, fout bedient pad) plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="45c4b-111">Elk exemplaar in de gegevens vertegenwoordigt een specifiek object (een geduld, een student, een auto, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="45c4b-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="45c4b-112">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) antwoord op de vraag 'Wat is de kans dat de gebeurtenis van belang wordt uitgevoerd door tijd n voor object x?'</span><span class="sxs-lookup"><span data-stu-id="45c4b-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="45c4b-113">Dankzij een voortdurende Analytics-model, kan deze webservice gebruikers op te geven gegevens voor het model trainen en te testen.</span><span class="sxs-lookup"><span data-stu-id="45c4b-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="45c4b-114">Het onderwerp van het experiment is als model voor de lengte van de verstreken tijd totdat de gebeurtenis die van belang.</span><span class="sxs-lookup"><span data-stu-id="45c4b-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="45c4b-115">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="45c4b-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="45c4b-116">Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="45c4b-117">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="45c4b-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="45c4b-118">De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.</span><span class="sxs-lookup"><span data-stu-id="45c4b-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="45c4b-119">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="45c4b-119">Consumption of web service</span></span>
<span data-ttu-id="45c4b-120">Het schema voor invoergegevens van de webservice wordt weergegeven in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="45c4b-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="45c4b-121">Zes stukjes informatie nodig zijn als de invoer: training gegevens, gegevens testen, tijd van belang, de index van 'keer' dimensie, de index van de dimensie 'gebeurtenis' en de variabele typen (doorlopende of factor).</span><span class="sxs-lookup"><span data-stu-id="45c4b-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="45c4b-122">De trainingsgegevens wordt vertegenwoordigd door een tekenreeks, waarbij de rijen worden gescheiden door komma's en de kolommen worden gescheiden door puntkomma's.</span><span class="sxs-lookup"><span data-stu-id="45c4b-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="45c4b-123">Het aantal functies van de gegevens is flexibel.</span><span class="sxs-lookup"><span data-stu-id="45c4b-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="45c4b-124">Alle elementen in de invoerreeks moet numeriek zijn.</span><span class="sxs-lookup"><span data-stu-id="45c4b-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="45c4b-125">In de trainingsgegevens geeft ' tijddimensie ' het aantal eenheden voor de tijd (dagen, jaar, kilometers, enzovoort) die zijn verstreken sinds het beginpunt van het onderzoek (een geduld medicijn behandeling programma's, ontvangen een student starten PhD onderzoek, een auto begint met het worden bestuurd, enz.) tot de gebeurtenis van belang zijn (de patiënt wordt teruggezonden naar de medicijn gebruik van de studenten verkrijgen van de mate PhD, de auto met bedient pad fout, enzovoort) plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="45c4b-126">De dimensie 'gebeurtenis' geeft aan of de gebeurtenis van belang aan het einde van het onderzoek plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="45c4b-127">De waarde ' gebeurtenis = 1 "betekent dat de gebeurtenis interessant vindt plaats op het tijdstip aangegeven in de dimensie 'keer'; "gebeurtenis = 0 ' betekent dat de gebeurtenis van belang is uitgevoerd door het tijdstip aangegeven in de dimensie 'keer'.</span><span class="sxs-lookup"><span data-stu-id="45c4b-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="45c4b-128">trainingdata - tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="45c4b-128">trainingdata - A character string.</span></span> <span data-ttu-id="45c4b-129">Rijen worden gescheiden door een komma en kolommen worden gescheiden door puntkomma's.</span><span class="sxs-lookup"><span data-stu-id="45c4b-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="45c4b-130">Elke rij bevat ' tijddimensie ' en 'gebeurtenis' dimensie manier variabelen.</span><span class="sxs-lookup"><span data-stu-id="45c4b-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="45c4b-131">testingdata - één rij met gegevens op die manier variabelen voor een bepaald object bevat.</span><span class="sxs-lookup"><span data-stu-id="45c4b-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="45c4b-132">time_of_interest - de verstreken tijd van belang n.</span><span class="sxs-lookup"><span data-stu-id="45c4b-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="45c4b-133">index_time - de kolomindex van de dimensie 'time' (vanaf 1).</span><span class="sxs-lookup"><span data-stu-id="45c4b-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="45c4b-134">index_event - de kolomindex van de 'gebeurtenis' dimensie (vanaf 1).</span><span class="sxs-lookup"><span data-stu-id="45c4b-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="45c4b-135">variable_types - tekenreeks met puntkomma's als scheidingstekens in deze.</span><span class="sxs-lookup"><span data-stu-id="45c4b-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="45c4b-136">0 geeft aan dat continue variabelen en 1 factor variabelen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="45c4b-137">De uitvoer is de kans op een gebeurtenis plaatsvindt op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="45c4b-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="45c4b-138">Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="45c4b-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="45c4b-139">Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="45c4b-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="45c4b-140">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="45c4b-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="45c4b-141">De interpretatie van deze test is als volgt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="45c4b-142">Ervan uitgaande dat het doel van de gegevens is om de verstreken tijd totdat het rendement op medicijn gebruik voor de patiënt heeft ontvangen van een van de twee behandeling programma's.</span><span class="sxs-lookup"><span data-stu-id="45c4b-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="45c4b-143">De uitvoer van de web service leesbewerkingen: patiënten wordt 35 jaar oude, met vorige productie medicijn behandeling 2 maal duurt het programma lang huis behandeling en met gebruik van zowel heroïne als cocaïne de waarschijnlijkheid geretourneerd met het gebruik van medicijn 95.64% van het dag 500.</span><span class="sxs-lookup"><span data-stu-id="45c4b-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="45c4b-144">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="45c4b-144">Creation of web service</span></span>
> <span data-ttu-id="45c4b-145">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="45c4b-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="45c4b-146">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="45c4b-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="45c4b-147">Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45c4b-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="45c4b-148">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules naar de werkruimte zijn opgehaald.</span><span class="sxs-lookup"><span data-stu-id="45c4b-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="45c4b-149">Het schema van de is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script], definieert de invoergegevens schema voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="45c4b-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="45c4b-150">Deze module wordt vervolgens gekoppeld aan de tweede [R-Script uitvoeren] [ execute-r-script] module waarmee werk grote.</span><span class="sxs-lookup"><span data-stu-id="45c4b-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="45c4b-151">Deze module biedt voorverwerking van gegevens, model bouwen en voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="45c4b-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="45c4b-152">In de voorverwerking stap van de gegevens de invoergegevens vertegenwoordigd door een lange tekenreeks getransformeerd en geconverteerd naar een gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="45c4b-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="45c4b-153">Een externe R-pakket 'survival_2.37 7.zip' is in de stap van het gebouw model eerst geïnstalleerd voor de uitvoering van survival analyse.</span><span class="sxs-lookup"><span data-stu-id="45c4b-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="45c4b-154">Vervolgens wordt de functie 'coxph' uitgevoerd na een reeks gegevensverwerkingstaken.</span><span class="sxs-lookup"><span data-stu-id="45c4b-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="45c4b-155">De details van de functie 'coxph' voor analyse van survival kunnen worden gelezen uit de R-documentatie.</span><span class="sxs-lookup"><span data-stu-id="45c4b-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="45c4b-156">Een test-exemplaar is opgegeven in het getrainde model met de functie 'surfit' in de stap voorspelling en survival curve voor dit exemplaar van de test wordt gegenereerd als de variabele 'curve'.</span><span class="sxs-lookup"><span data-stu-id="45c4b-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="45c4b-157">Ten slotte wordt wordt de waarschijnlijkheid van de tijd van belang verkregen.</span><span class="sxs-lookup"><span data-stu-id="45c4b-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="45c4b-158">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="45c4b-158">Experiment flow:</span></span>
![Experiment stroom][1]

#### <a name="module-1"></a><span data-ttu-id="45c4b-160">Module 1:</span><span class="sxs-lookup"><span data-stu-id="45c4b-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="45c4b-161">2-module:</span><span class="sxs-lookup"><span data-stu-id="45c4b-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="45c4b-162">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="45c4b-162">Limitations</span></span>
<span data-ttu-id="45c4b-163">Deze webservice kan alleen numerieke waarden duren als functie variabelen (kolommen).</span><span class="sxs-lookup"><span data-stu-id="45c4b-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="45c4b-164">De kolom 'gebeurtenis' kunnen alleen de waarde 0 of 1.</span><span class="sxs-lookup"><span data-stu-id="45c4b-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="45c4b-165">De kolom 'tijd' moet een positief geheel getal.</span><span class="sxs-lookup"><span data-stu-id="45c4b-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="45c4b-166">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="45c4b-166">FAQ</span></span>
<span data-ttu-id="45c4b-167">Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="45c4b-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

