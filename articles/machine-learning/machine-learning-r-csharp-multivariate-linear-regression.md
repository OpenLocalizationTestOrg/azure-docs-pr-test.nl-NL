---
title: AAA(deprecated) Multivariate Linear Regression - Azure | Microsoft Docs
description: (afgeschaft) Multidimensionale lineaire regressie
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
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
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="0919a-103">(afgeschaft) Multidimensionale lineaire regressie</span><span class="sxs-lookup"><span data-stu-id="0919a-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="0919a-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="0919a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0919a-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0919a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0919a-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0919a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0919a-107">Stel dat u hebt een gegevensset en zou zoals tooquickly voorspellen een afhankelijke variabele (y) voor elke afzonderlijke (i) op basis van onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="0919a-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="0919a-108">Lineaire regressie is een populair statistische techniek voor dergelijke voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="0919a-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0919a-109">Hallo afhankelijke variabele y wordt hier uitgegaan van een doorlopende waarde toobe.</span><span class="sxs-lookup"><span data-stu-id="0919a-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0919a-110">Een eenvoudig scenario mogelijk waarin Hallo onderzoeker probeert toopredict Hallo gewicht van een persoon (y), op basis van hun hoogte (x).</span><span class="sxs-lookup"><span data-stu-id="0919a-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="0919a-111">Een meer geavanceerde scenario mogelijk waarbij Hallo onderzoeker bevat extra informatie voor Hallo afzonderlijke (zoals gewicht, geslacht, race) en probeert toopredict Hallo gewicht van Hallo afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="0919a-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="0919a-112">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) past Hallo lineaire regressie toohello modelgegevens en uitvoer Hallo voorspelde waarde (y) voor elk Hallo metingen in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="0919a-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="0919a-113">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="0919a-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0919a-114">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="0919a-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="0919a-115">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="0919a-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0919a-116">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="0919a-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0919a-117">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="0919a-117">Consumption of web service</span></span>
<span data-ttu-id="0919a-118">Deze web-service biedt Hallo voorspelde waarden van Hallo afhankelijke variabele op basis van onafhankelijke variabelen Hallo voor alle Hallo opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="0919a-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="0919a-119">Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;).</span><span class="sxs-lookup"><span data-stu-id="0919a-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="0919a-120">Hallo-webservice 1 rij tegelijk verwacht en Hallo eerste kolom toobe Hallo afhankelijke variabele verwacht.</span><span class="sxs-lookup"><span data-stu-id="0919a-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="0919a-121">Een voorbeeld van de gegevensset kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="0919a-121">An example dataset could look like this:</span></span>

![Voorbeeldgegevens][1]

<span data-ttu-id="0919a-123">Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y.</span><span class="sxs-lookup"><span data-stu-id="0919a-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0919a-124">Hallo gegevens invoeren voor Hallo hierboven gegevensset zou worden Hallo de volgende tekenreeks: "10, 5, 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2, 1, N.V.T.; 3; 4 '.</span><span class="sxs-lookup"><span data-stu-id="0919a-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="0919a-125">Hallo-uitvoer is hello voorspelde waarde voor elk van de rijen Hallo gebaseerd op Hallo onafhankelijke variabelen.</span><span class="sxs-lookup"><span data-stu-id="0919a-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="0919a-126">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="0919a-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0919a-127">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0919a-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0919a-128">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="0919a-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="0919a-129">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="0919a-129">Creation of web service</span></span>
> <span data-ttu-id="0919a-130">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0919a-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0919a-131">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0919a-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0919a-132">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="0919a-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="0919a-133">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules op Hallo werkruimte zijn opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0919a-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="0919a-134">Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script.</span><span class="sxs-lookup"><span data-stu-id="0919a-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0919a-135">Er zijn 2-onderdelen toothis experimenteren: schemadefinitie, en training model + score berekenen.</span><span class="sxs-lookup"><span data-stu-id="0919a-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0919a-136">de eerste module Hallo Hallo verwacht-structuur van Hallo invoergegevensset, waarbij de eerste variabele Hallo Hallo afhankelijke variabele en resterende Hallo-variabelen zijn onafhankelijk wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0919a-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="0919a-137">Hallo tweede module past een algemene lineair regressiemodel voor Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="0919a-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Experiment stroom][3]

#### <a name="module-1"></a><span data-ttu-id="0919a-139">Module 1:</span><span class="sxs-lookup"><span data-stu-id="0919a-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="0919a-140">Schemadefinitie</span><span class="sxs-lookup"><span data-stu-id="0919a-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0919a-141">2-module:</span><span class="sxs-lookup"><span data-stu-id="0919a-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="0919a-142">LM-model</span><span class="sxs-lookup"><span data-stu-id="0919a-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="0919a-143">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="0919a-143">Limitations</span></span>
<span data-ttu-id="0919a-144">Dit is een zeer eenvoudig voorbeeld van een meerdere lineaire regressie-webservice.</span><span class="sxs-lookup"><span data-stu-id="0919a-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="0919a-145">Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo van dit web de service.</span><span class="sxs-lookup"><span data-stu-id="0919a-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="0919a-146">Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0919a-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0919a-147">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0919a-147">FAQ</span></span>
<span data-ttu-id="0919a-148">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0919a-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

