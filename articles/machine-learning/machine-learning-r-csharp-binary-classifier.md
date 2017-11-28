---
title: AAA(deprecated) binaire classificatie - Azure | Microsoft Docs
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
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="88034-103">(afgeschaft) Binaire classificatie</span><span class="sxs-lookup"><span data-stu-id="88034-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="88034-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="88034-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="88034-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="88034-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="88034-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="88034-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="88034-107">Stel dat u hebt een gegevensset en wilt toopredict een binaire afhankelijke variabele op basis van Hallo onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="88034-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="88034-108">'Logistic Regression' is een populair statistische techniek voor dergelijke voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="88034-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="88034-109">Hier Hallo afhankelijke variabele binary of dichotomous, en p Hallo kans van de aanwezigheid van Hallo-kenmerk van belang.</span><span class="sxs-lookup"><span data-stu-id="88034-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="88034-110">Een eenvoudig scenario mogelijk waarin een onderzoeker probeert toopredict of een potentiële student waarschijnlijk tooaccept een toelating aanbieding tooa universiteit op basis van gegevens is (GPA in middelbare school, familie inkomsten, residente status gendervraagstukken).</span><span class="sxs-lookup"><span data-stu-id="88034-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="88034-111">Hallo voorspelde uitkomst is de kans op Hallo van Hallo potentiële student Hallo toelating aanbieding accepteren.</span><span class="sxs-lookup"><span data-stu-id="88034-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="88034-112">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/log_regression) past Hallo logistic regression toohello modelgegevens en uitvoer Hallo waarschijnlijkheidswaarde (y) voor elk Hallo metingen in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="88034-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="88034-113">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="88034-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="88034-114">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="88034-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="88034-115">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="88034-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="88034-116">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="88034-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="88034-117">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="88034-117">Consumption of web service</span></span>
<span data-ttu-id="88034-118">Deze web-service biedt Hallo voorspelde waarden van Hallo afhankelijke variabele op basis van onafhankelijke variabelen Hallo voor alle Hallo opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="88034-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="88034-119">Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door komma (,) en kolommen worden gescheiden door puntkomma (;).</span><span class="sxs-lookup"><span data-stu-id="88034-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="88034-120">Hallo-webservice 1 rij tegelijk verwacht en Hallo eerste kolom toobe Hallo afhankelijke variabele verwacht.</span><span class="sxs-lookup"><span data-stu-id="88034-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="88034-121">Een voorbeeld van de gegevensset kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="88034-121">An example dataset could look like this:</span></span>

![Voorbeeldgegevens][1]

<span data-ttu-id="88034-123">Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y.</span><span class="sxs-lookup"><span data-stu-id="88034-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="88034-124">Hallo gegevens invoeren voor Hallo hierboven gegevensset zou worden Hallo de volgende tekenreeks: '1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, N.V.T.; 3; 4'.</span><span class="sxs-lookup"><span data-stu-id="88034-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="88034-125">Hallo-uitvoer is hello voorspelde waarde voor elk van de rijen Hallo gebaseerd op Hallo onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="88034-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="88034-126">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="88034-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="88034-127">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="88034-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="88034-128">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="88034-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="88034-129">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="88034-129">Creation of web service</span></span>
> <span data-ttu-id="88034-130">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="88034-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="88034-131">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="88034-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="88034-132">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="88034-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="88034-133">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald op Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="88034-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="88034-134">Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script.</span><span class="sxs-lookup"><span data-stu-id="88034-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="88034-135">Er zijn 2-onderdelen toothis experimenteren: schemadefinitie, en training model + score berekenen.</span><span class="sxs-lookup"><span data-stu-id="88034-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="88034-136">de eerste module Hallo Hallo verwacht-structuur van Hallo invoergegevensset, waarbij de eerste variabele Hallo Hallo afhankelijke variabele en resterende Hallo-variabelen zijn onafhankelijk wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="88034-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="88034-137">Hallo tweede module past een algemene logistic regressiemodel voor Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="88034-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Experiment stroom][2]

#### <a name="module-1"></a><span data-ttu-id="88034-139">Module 1:</span><span class="sxs-lookup"><span data-stu-id="88034-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="88034-140">2-module:</span><span class="sxs-lookup"><span data-stu-id="88034-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="88034-141">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="88034-141">Limitations</span></span>
<span data-ttu-id="88034-142">Dit is een zeer eenvoudig voorbeeld van een binaire classificatie-webservice.</span><span class="sxs-lookup"><span data-stu-id="88034-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="88034-143">Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles een binary/continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo gemaakt van deze Web-service.</span><span class="sxs-lookup"><span data-stu-id="88034-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="88034-144">Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="88034-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="88034-145">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="88034-145">FAQ</span></span>
<span data-ttu-id="88034-146">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="88034-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

