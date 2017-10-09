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
# <a name="deprecated-survival-analysis"></a>(afgeschaft) Survival analyse

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Onder veel scenario's is de belangrijkste uitkomst Hallo onder assessment Hallo tijd tooan gebeurtenis van belang. Met andere woorden, Hallo vraag 'wanneer deze gebeurtenis wordt uitgevoerd?' wordt gevraagd. Voorbeelden, kunt u beter situaties waarbij gegevens Hallo Hallo verstreken tijd (dagen, jaar, kilometers, enzovoort) beschrijft tot Hallo gebeurtenis van belang (ziekte relapse, PhD mate ontvangen, bedient pad fout). Elk exemplaar in Hallo gegevens vertegenwoordigt een specifiek object (een geduld, een student, een auto, enzovoort).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) beantwoordt Hallo vraag 'Wat is er Hallo-kans dat Hallo gebeurtenis van belang optreden bij tijd n voor object x?' Dankzij een voortdurende Analytics-model, deze webservice kunt gebruikers toosupply tootrain Hallo gegevensmodel en testen. Hallo belangrijkste thema van Hallo experiment is toomodel Hallo Hallo verstreken tijd totdat Hallo van belang gebeurtenis. 

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Hallo invoergegevens schema van Hallo-webservice wordt weergegeven in de volgende tabel Hallo. Zes stukjes informatie nodig zijn als Hallo invoer: trainingsgegevens, testgegevens, tijd van belang, de index van de dimensie 'time' hello, Hallo index van de dimensie 'gebeurtenis' en Hallo variabele typen (doorlopende of factor). Hallo trainingsgegevens wordt vertegenwoordigd door een tekenreeks, waarbij Hallo rijen worden gescheiden door een komma en Hallo kolommen worden gescheiden door puntkomma's. Hallo aantal kenmerken van Hallo gegevens is flexibel. Alle Hallo-elementen in de invoerreeks Hallo moet numeriek zijn. Hallo trainingsgegevens wijst dimensie Hallo 'time' Hallo aantal tijdseenheden (dagen, jaar, kilometers, enz.) is verstreken sinds beginpunt Hallo Hallo bestuderen (een geduld ontvangen medicijn behandeling-programma's, een student begin PhD onderzoek, een auto toobe starten aangedreven, enz.) totdat hello van belang (Hallo geduld retourneren toodrug gebruik, Hallo studenten verkrijgen Hallo PhD mate, Hallo auto met bedient pad fout, enzovoort) gebeurtenis. Hallo 'gebeurtenis' dimensie geeft aan of Hallo-gebeurtenis van belang achter Hallo Hallo onderzoek plaatsvindt. De waarde ' gebeurtenis = 1 "betekent dat de gebeurtenis van belang Hallo deze gebeurtenis treedt op tijdens het Hallo aangegeven door de dimensie 'time' hello; "gebeurtenis = 0 ' betekent dat Hallo gebeurtenis van belang is niet door Hallo tijd aangegeven door de dimensie 'time' hello opgetreden.

* trainingdata - tekenreeks. Rijen worden gescheiden door een komma en kolommen worden gescheiden door puntkomma's. Elke rij bevat ' tijddimensie ' en 'gebeurtenis' dimensie manier variabelen.
* testingdata - één rij met gegevens op die manier variabelen voor een bepaald object bevat.
* time_of_interest - Hallo verstreken tijd van belang n.
* index_time - Hallo kolomindex van de dimensie 'time' hello (vanaf 1).
* index_event - Hallo kolomindex van Hallo 'gebeurtenis' dimensie (vanaf 1).
* variable_types - tekenreeks met puntkomma's als scheidingstekens in deze. 0 geeft aan dat continue variabelen en 1 factor variabelen vertegenwoordigt.

Hallo-uitvoer is de kans op Hallo van een gebeurtenis optreedt op een bepaald moment. 

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

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




Hallo interpretatie van deze test is als volgt. Ervan uitgaande dat Hallo Hallo gegevens is bedoeld toomodel Hallo verstreken tijd tot Hallo toodrug gebruik retourneren voor Hallo patiënten heeft ontvangen van een van twee Hallo behandeling programma's. Hallo uitvoer Hallo web service leesbewerkingen: voor patiënten wordt 35 jaar oude, met vorige productie medicijn behandeling 2 maal duurt Hallo lang huis behandeling programma, en met gebruik van zowel heroïne als cocaïne Hallo kans retourneren toohello medicijn gebruik 95.64% door is dag 500.

## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.
> 
> 

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules op Hallo werkruimte zijn opgehaald. Hallo gegevensschema is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script], definieert een Hallo invoergegevens schema voor Hallo-webservice. Deze module wordt vervolgens gekoppeld toohello tweede [R-Script uitvoeren] [ execute-r-script] module waarmee werk grote. Deze module biedt voorverwerking van gegevens, model bouwen en voorspellingen. In Hallo gegevens voorverwerking stap Hallo invoergegevens vertegenwoordigd door een lange tekenreeks getransformeerd en geconverteerd naar een gegevensframe. Een externe R-pakket 'survival_2.37 7.zip' is in Hallo model bouwen stap eerst geïnstalleerd voor de uitvoering van survival analyse. De functie 'coxph' hello wordt vervolgens uitgevoerd na een reeks gegevensverwerkingstaken. Hallo details van de functie 'coxph' Hallo voor survival analyse kunnen worden gelezen uit Hallo R-documentatie. Een test-exemplaar is opgegeven in het getrainde model met de functie 'surfit' Hallo Hallo in Hallo voorspelling stap en Hallo survival curve voor dit exemplaar van de test wordt gegenereerd als de variabele 'curve'. Ten slotte de kans op Hallo van Hallo-tijd van belang wordt verkregen. 

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

    maml.mapOutputPort("sampleInput"); #send data toooutput port

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




## <a name="limitations"></a>Beperkingen
Deze webservice kan alleen numerieke waarden duren als functie variabelen (kolommen). de kolom 'event' Hello kan duren voordat de waarde 0 of 1. Hallo 'time'-kolom moet een positief geheel getal toobe.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

