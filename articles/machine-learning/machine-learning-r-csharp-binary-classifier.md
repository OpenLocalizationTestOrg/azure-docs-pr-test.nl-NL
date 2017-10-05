---
title: (afgeschaft) Binaire classificatie - Azure | Microsoft Docs
description: (afgeschaft) Binaire classificatie
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="0120d-103">(afgeschaft) Binaire classificatie</span><span class="sxs-lookup"><span data-stu-id="0120d-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="0120d-104">De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="0120d-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0120d-105">U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0120d-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0120d-106">Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0120d-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0120d-107">Stel dat u hebt een gegevensset en zou willen voorspellen van een binaire afhankelijke variabele op basis van de onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="0120d-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="0120d-108">'Logistic Regression' is een populair statistische techniek voor dergelijke voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="0120d-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0120d-109">Hier de afhankelijke variabele is binary of dichotomous en p is de kans van de aanwezigheid van het kenmerk van belang.</span><span class="sxs-lookup"><span data-stu-id="0120d-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0120d-110">Een eenvoudig scenario mogelijk waarin een onderzoeker probeert te voorspellen of een potentiële student waarschijnlijk een aanbieding toelating om een universiteit op basis van gegevens is (GPA in middelbare school, familie inkomsten, residente status gendervraagstukken) te accepteren.</span><span class="sxs-lookup"><span data-stu-id="0120d-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="0120d-111">Het verwachte resultaat is de kans van de potentiële student de toelating-aanbieding accepteren.</span><span class="sxs-lookup"><span data-stu-id="0120d-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="0120d-112">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/log_regression) past het logistic regressiemodel in de gegevens en de waarschijnlijkheidswaarde (y) voor elk van de metingen in de gegevens levert.</span><span class="sxs-lookup"><span data-stu-id="0120d-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="0120d-113">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="0120d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0120d-114">Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0120d-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="0120d-115">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="0120d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0120d-116">De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.</span><span class="sxs-lookup"><span data-stu-id="0120d-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0120d-117">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="0120d-117">Consumption of web service</span></span>
<span data-ttu-id="0120d-118">Deze webservice geeft de voorspelde waarden van de afhankelijke variabele op basis van de onafhankelijke variabelen voor alle van de metingen.</span><span class="sxs-lookup"><span data-stu-id="0120d-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="0120d-119">De webservice voor verwacht de eindgebruiker voor het invoeren van gegevens als een tekenreeks waarin rijen worden gescheiden door komma (,) en kolommen worden gescheiden door puntkomma (;).</span><span class="sxs-lookup"><span data-stu-id="0120d-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="0120d-120">De webservice 1 rij verwacht op een tijdstip en de eerste kolom van de afhankelijke variabele worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="0120d-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="0120d-121">Een voorbeeld van de gegevensset kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="0120d-121">An example dataset could look like this:</span></span>

![Voorbeeldgegevens][1]

<span data-ttu-id="0120d-123">Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y.</span><span class="sxs-lookup"><span data-stu-id="0120d-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0120d-124">De gegevens die invoer voor de bovenstaande gegevensset zou de volgende tekenreeks zijn: '1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, N.V.T.; 3; 4'.</span><span class="sxs-lookup"><span data-stu-id="0120d-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="0120d-125">De uitvoer is de voorspelde waarde voor elk van de rijen op basis van de onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="0120d-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="0120d-126">Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="0120d-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0120d-127">Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0120d-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0120d-128">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="0120d-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="0120d-129">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="0120d-129">Creation of web service</span></span>
> <span data-ttu-id="0120d-130">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0120d-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0120d-131">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0120d-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0120d-132">Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0120d-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="0120d-133">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald naar de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0120d-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="0120d-134">Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script.</span><span class="sxs-lookup"><span data-stu-id="0120d-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0120d-135">Er zijn 2-onderdelen voor dit experiment: schemadefinitie, en training model + score berekenen.</span><span class="sxs-lookup"><span data-stu-id="0120d-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0120d-136">De eerste module definieert de verwachte structuur van de invoergegevensset, waarbij de eerste variabele de afhankelijke variabele en de resterende variabelen onafhankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="0120d-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="0120d-137">De tweede module past een algemene logistic regressiemodel van de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="0120d-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Experiment stroom][2]

#### <a name="module-1"></a><span data-ttu-id="0120d-139">Module 1:</span><span class="sxs-lookup"><span data-stu-id="0120d-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0120d-140">2-module:</span><span class="sxs-lookup"><span data-stu-id="0120d-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="0120d-141">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="0120d-141">Limitations</span></span>
<span data-ttu-id="0120d-142">Dit is een zeer eenvoudig voorbeeld van een binaire classificatie-webservice.</span><span class="sxs-lookup"><span data-stu-id="0120d-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="0120d-143">Zoals u kunt zien van de bovenstaande voorbeeldcode, er is geen fout vastgelegd is geïmplementeerd en wordt de service wordt ervan uitgegaan dat alles een binary/continue variabele (geen categorische functies toegestaan), als de service alleen invoer numerieke waarden op het moment van het maken van deze webservice .</span><span class="sxs-lookup"><span data-stu-id="0120d-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="0120d-144">Ook de service momenteel worden verwerkt beperkt gegevensgrootte, behoren tot de aard van de aanvraag/antwoord van de aanroep van webservice en het feit dat het model is wordt passen elke keer dat de webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0120d-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0120d-145">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0120d-145">FAQ</span></span>
<span data-ttu-id="0120d-146">Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0120d-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

