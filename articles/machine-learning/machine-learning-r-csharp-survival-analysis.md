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
# <a name="deprecated-survival-analysis"></a>(afgeschaft) Survival analyse

> [!NOTE]
> De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

In veel scenario's is de belangrijkste uitkomst onder assessment de tijd op een gebeurtenis van belang. Met andere woorden, de vraag "wanneer deze gebeurtenis wordt uitgevoerd?' wordt gevraagd. Voorbeelden, kunt u beter situaties waarbij de gegevens de verstreken tijd (dagen, jaar, kilometers, enzovoort beschrijft) tot en met de gebeurtenis van belang (ziekte relapse, PhD mate ontvangen, fout bedient pad) plaatsvindt. Elk exemplaar in de gegevens vertegenwoordigt een specifiek object (een geduld, een student, een auto, enzovoort).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) antwoord op de vraag 'Wat is de kans dat de gebeurtenis van belang wordt uitgevoerd door tijd n voor object x?' Dankzij een voortdurende Analytics-model, kan deze webservice gebruikers op te geven gegevens voor het model trainen en te testen. Het onderwerp van het experiment is als model voor de lengte van de verstreken tijd totdat de gebeurtenis die van belang. 

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Het schema voor invoergegevens van de webservice wordt weergegeven in de volgende tabel. Zes stukjes informatie nodig zijn als de invoer: training gegevens, gegevens testen, tijd van belang, de index van 'keer' dimensie, de index van de dimensie 'gebeurtenis' en de variabele typen (doorlopende of factor). De trainingsgegevens wordt vertegenwoordigd door een tekenreeks, waarbij de rijen worden gescheiden door komma's en de kolommen worden gescheiden door puntkomma's. Het aantal functies van de gegevens is flexibel. Alle elementen in de invoerreeks moet numeriek zijn. In de trainingsgegevens geeft ' tijddimensie ' het aantal eenheden voor de tijd (dagen, jaar, kilometers, enzovoort) die zijn verstreken sinds het beginpunt van het onderzoek (een geduld medicijn behandeling programma's, ontvangen een student starten PhD onderzoek, een auto begint met het worden bestuurd, enz.) tot de gebeurtenis van belang zijn (de patiënt wordt teruggezonden naar de medicijn gebruik van de studenten verkrijgen van de mate PhD, de auto met bedient pad fout, enzovoort) plaatsvindt. De dimensie 'gebeurtenis' geeft aan of de gebeurtenis van belang aan het einde van het onderzoek plaatsvindt. De waarde ' gebeurtenis = 1 "betekent dat de gebeurtenis interessant vindt plaats op het tijdstip aangegeven in de dimensie 'keer'; "gebeurtenis = 0 ' betekent dat de gebeurtenis van belang is uitgevoerd door het tijdstip aangegeven in de dimensie 'keer'.

* trainingdata - tekenreeks. Rijen worden gescheiden door een komma en kolommen worden gescheiden door puntkomma's. Elke rij bevat ' tijddimensie ' en 'gebeurtenis' dimensie manier variabelen.
* testingdata - één rij met gegevens op die manier variabelen voor een bepaald object bevat.
* time_of_interest - de verstreken tijd van belang n.
* index_time - de kolomindex van de dimensie 'time' (vanaf 1).
* index_event - de kolomindex van de 'gebeurtenis' dimensie (vanaf 1).
* variable_types - tekenreeks met puntkomma's als scheidingstekens in deze. 0 geeft aan dat continue variabelen en 1 factor variabelen vertegenwoordigt.

De uitvoer is de kans op een gebeurtenis plaatsvindt op een bepaald moment. 

> Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
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




De interpretatie van deze test is als volgt. Ervan uitgaande dat het doel van de gegevens is om de verstreken tijd totdat het rendement op medicijn gebruik voor de patiënt heeft ontvangen van een van de twee behandeling programma's. De uitvoer van de web service leesbewerkingen: patiënten wordt 35 jaar oude, met vorige productie medicijn behandeling 2 maal duurt het programma lang huis behandeling en met gebruik van zowel heroïne als cocaïne de waarschijnlijkheid geretourneerd met het gebruik van medicijn 95.64% van het dag 500.

## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.
> 
> 

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules naar de werkruimte zijn opgehaald. Het schema van de is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script], definieert de invoergegevens schema voor de webservice. Deze module wordt vervolgens gekoppeld aan de tweede [R-Script uitvoeren] [ execute-r-script] module waarmee werk grote. Deze module biedt voorverwerking van gegevens, model bouwen en voorspellingen. In de voorverwerking stap van de gegevens de invoergegevens vertegenwoordigd door een lange tekenreeks getransformeerd en geconverteerd naar een gegevensframe. Een externe R-pakket 'survival_2.37 7.zip' is in de stap van het gebouw model eerst geïnstalleerd voor de uitvoering van survival analyse. Vervolgens wordt de functie 'coxph' uitgevoerd na een reeks gegevensverwerkingstaken. De details van de functie 'coxph' voor analyse van survival kunnen worden gelezen uit de R-documentatie. Een test-exemplaar is opgegeven in het getrainde model met de functie 'surfit' in de stap voorspelling en survival curve voor dit exemplaar van de test wordt gegenereerd als de variabele 'curve'. Ten slotte wordt wordt de waarschijnlijkheid van de tijd van belang verkregen. 

### <a name="experiment-flow"></a>Stroom experiment:
![Experiment stroom][1]

#### <a name="module-1"></a>Module 1:
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

#### <a name="module-2"></a>2-module:
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




## <a name="limitations"></a>Beperkingen
Deze webservice kan alleen numerieke waarden duren als functie variabelen (kolommen). De kolom 'gebeurtenis' kunnen alleen de waarde 0 of 1. De kolom 'tijd' moet een positief geheel getal.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

