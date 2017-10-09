---
title: AAA(deprecated) clustermodel - Azure | Microsoft Docs
description: (afgeschaft) Clustermodel
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="06ee9-103">(afgeschaft) Clustermodel</span><span class="sxs-lookup"><span data-stu-id="06ee9-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="06ee9-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="06ee9-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="06ee9-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="06ee9-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="06ee9-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="06ee9-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="06ee9-107">Hoe kunnen we groepen tegoed kaarthouders gedrag in volgorde tooreduce Hallo-uitstaand risico creditcard verleners voorspellen?</span><span class="sxs-lookup"><span data-stu-id="06ee9-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="06ee9-108">Hoe kunnen we groepen definiëren karakter kenmerken van werknemers in volgorde tooimprove hun prestaties op het werk?</span><span class="sxs-lookup"><span data-stu-id="06ee9-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="06ee9-109">Hoe kunnen arts patiënten classificeren in groepen op basis van kenmerken van hun ziekten Hallo</span><span class="sxs-lookup"><span data-stu-id="06ee9-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="06ee9-110">In principe kunnen al deze vragen worden beantwoord door cluster analyse.</span><span class="sxs-lookup"><span data-stu-id="06ee9-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="06ee9-111">Analyse van de cluster deelt een set van metingen in twee of meer sluiten elkaar wederzijds uit onbekende groepen op basis van combinaties van variabelen.</span><span class="sxs-lookup"><span data-stu-id="06ee9-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="06ee9-112">Hallo-doel van de cluster analyse is toodiscover een systeem van opmerkingen, meestal personen of hun kenmerken te organiseren in groepen, waar leden van groepen Hallo eigenschappen gemeen delen.</span><span class="sxs-lookup"><span data-stu-id="06ee9-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="06ee9-113">Dit [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) gebruikt Hallo K-Means methodologie, een techniek voor vaak gebruikte clustering toocluster willekeurige gegevens in groepen.</span><span class="sxs-lookup"><span data-stu-id="06ee9-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="06ee9-114">Hallo-gegevens voor deze webservice worden gehaald en Hallo k aantal clusters als invoer en produceert voorspellingen waarvan Hallo k groepen toowhich elke waarnemingen behoort.</span><span class="sxs-lookup"><span data-stu-id="06ee9-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="06ee9-115">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="06ee9-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="06ee9-116">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="06ee9-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="06ee9-117">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="06ee9-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="06ee9-118">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="06ee9-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="06ee9-119">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="06ee9-119">Consumption of web service</span></span>
<span data-ttu-id="06ee9-120">Deze webservice groepeert Hallo gegevens in een set k groepen en uitvoer Hallo groepstoewijzing voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="06ee9-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="06ee9-121">Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;).</span><span class="sxs-lookup"><span data-stu-id="06ee9-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="06ee9-122">Hallo-webservice verwacht 1 rij tegelijk.</span><span class="sxs-lookup"><span data-stu-id="06ee9-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="06ee9-123">Een voorbeeld van de gegevensset kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="06ee9-123">An example dataset could look like this:</span></span>

![Voorbeeldgegevens][1]

<span data-ttu-id="06ee9-125">Stel Hallo gebruiker wilden tooseparate deze gegevens in groepen van 3 sluiten elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="06ee9-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="06ee9-126">Hallo gegevensinvoer voor Hallo hierboven gegevensset Hallo volgende zijn: waarde = '10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4'; k = "3".</span><span class="sxs-lookup"><span data-stu-id="06ee9-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="06ee9-127">Hallo-uitvoer is voorspelde groepslidmaatschap Hallo voor elk Hallo rijen.</span><span class="sxs-lookup"><span data-stu-id="06ee9-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="06ee9-128">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="06ee9-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="06ee9-129">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="06ee9-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="06ee9-130">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="06ee9-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="06ee9-131">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="06ee9-131">Creation of web service</span></span>
> <span data-ttu-id="06ee9-132">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06ee9-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="06ee9-133">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="06ee9-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="06ee9-134">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="06ee9-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="06ee9-135">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald op Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="06ee9-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="06ee9-136">Hallo gegevensschema is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="06ee9-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="06ee9-137">Vervolgens Hallo gegevensschema gekoppelde toohello is cluster model sectie opnieuw gemaakt met een [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="06ee9-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="06ee9-138">In Hallo [R-Script uitvoeren] [ execute-r-script] gebruikt voor het clustermodel hello, Hallo webservice vervolgens maakt gebruik van 'k-means' Hallo-functie, die vooraf gedefinieerde in Hallo is [R-Script uitvoeren] [ execute-r-script] van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06ee9-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Experiment stroom][3]

#### <a name="module-1"></a><span data-ttu-id="06ee9-140">Module 1:</span><span class="sxs-lookup"><span data-stu-id="06ee9-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="06ee9-141">2-module:</span><span class="sxs-lookup"><span data-stu-id="06ee9-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="06ee9-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="06ee9-142">Limitations</span></span>
<span data-ttu-id="06ee9-143">Dit is een zeer eenvoudig voorbeeld van een web-clusteringservice.</span><span class="sxs-lookup"><span data-stu-id="06ee9-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="06ee9-144">Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo van dit web de service.</span><span class="sxs-lookup"><span data-stu-id="06ee9-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="06ee9-145">Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="06ee9-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="06ee9-146">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="06ee9-146">FAQ</span></span>
<span data-ttu-id="06ee9-147">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="06ee9-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

