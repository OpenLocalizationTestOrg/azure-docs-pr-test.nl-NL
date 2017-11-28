---
title: (afgeschaft) Model - Azure-cluster | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="1debc-103">(afgeschaft) Clustermodel</span><span class="sxs-lookup"><span data-stu-id="1debc-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="1debc-104">De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="1debc-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="1debc-105">U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1debc-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1debc-106">Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="1debc-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="1debc-107">Hoe kunnen we groepen tegoed kaarthouders gedrag voorspellen om de risico-uitstaand creditcard uitgevers van certificaten te reduceren?</span><span class="sxs-lookup"><span data-stu-id="1debc-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="1debc-108">Hoe definiëren we groepen van kenmerken karakter van werknemers om te verbeteren de prestaties op het werk?</span><span class="sxs-lookup"><span data-stu-id="1debc-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="1debc-109">Hoe kunnen arts patiënten classificeren in groepen op basis van de kenmerken van hun ziekten</span><span class="sxs-lookup"><span data-stu-id="1debc-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="1debc-110">In principe kunnen al deze vragen worden beantwoord door cluster analyse.</span><span class="sxs-lookup"><span data-stu-id="1debc-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="1debc-111">Analyse van de cluster deelt een set van metingen in twee of meer sluiten elkaar wederzijds uit onbekende groepen op basis van combinaties van variabelen.</span><span class="sxs-lookup"><span data-stu-id="1debc-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="1debc-112">Het doel van de cluster-analyse is voor het detecteren van een systeem van opmerkingen, meestal personen of hun kenmerken te organiseren in groepen, waar leden van de groepen eigenschappen gemeen delen.</span><span class="sxs-lookup"><span data-stu-id="1debc-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="1debc-113">Dit [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) maakt gebruik van de methodologie K-Means, een veelgebruikte clustering techniek tot willekeurige gegevens van de cluster in groepen.</span><span class="sxs-lookup"><span data-stu-id="1debc-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="1debc-114">Deze webservice neemt de gegevens en het aantal k clusters als invoer en produceert voorspellingen waarvan de k groepen waartoe elke waarnemingen behoort.</span><span class="sxs-lookup"><span data-stu-id="1debc-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="1debc-115">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1debc-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="1debc-116">Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1debc-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="1debc-117">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="1debc-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="1debc-118">De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.</span><span class="sxs-lookup"><span data-stu-id="1debc-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="1debc-119">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="1debc-119">Consumption of web service</span></span>
<span data-ttu-id="1debc-120">Deze webservice worden de gegevens in een set k groepen gegroepeerd en levert de groepstoewijzing van de voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="1debc-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="1debc-121">De webservice voor verwacht de eindgebruiker voor het invoeren van gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;).</span><span class="sxs-lookup"><span data-stu-id="1debc-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="1debc-122">De webservice verwacht 1 rij tegelijk.</span><span class="sxs-lookup"><span data-stu-id="1debc-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="1debc-123">Een voorbeeld van de gegevensset kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="1debc-123">An example dataset could look like this:</span></span>

![Voorbeeldgegevens][1]

<span data-ttu-id="1debc-125">Stel dat de gebruiker wil deze gegevens verdelen in groepen van 3 sluiten elkaar wederzijds uit.</span><span class="sxs-lookup"><span data-stu-id="1debc-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="1debc-126">De invoer voor de bovenstaande gegevensset de volgende zijn gegevens: waarde = '10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4'; k = "3".</span><span class="sxs-lookup"><span data-stu-id="1debc-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="1debc-127">De uitvoer is de voorspelde groepslidmaatschap voor elk van de rijen.</span><span class="sxs-lookup"><span data-stu-id="1debc-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="1debc-128">Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="1debc-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="1debc-129">Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1debc-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="1debc-130">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="1debc-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="1debc-131">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="1debc-131">Creation of web service</span></span>
> <span data-ttu-id="1debc-132">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1debc-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="1debc-133">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="1debc-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="1debc-134">Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1debc-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="1debc-135">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald naar de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="1debc-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="1debc-136">Het schema van de is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="1debc-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="1debc-137">Vervolgens, wordt het schema van de is gekoppeld aan de sectie cluster model, opnieuw worden gemaakt met een [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="1debc-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="1debc-138">In de [R-Script uitvoeren] [ execute-r-script] gebruikt voor het clustermodel, de webservice vervolgens maakt gebruik van de functie 'k-means', dat vooraf gedefinieerde in de [R-Script uitvoeren] [ execute-r-script] van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1debc-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Experiment stroom][3]

#### <a name="module-1"></a><span data-ttu-id="1debc-140">Module 1:</span><span class="sxs-lookup"><span data-stu-id="1debc-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="1debc-141">2-module:</span><span class="sxs-lookup"><span data-stu-id="1debc-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="1debc-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1debc-142">Limitations</span></span>
<span data-ttu-id="1debc-143">Dit is een zeer eenvoudig voorbeeld van een web-clusteringservice.</span><span class="sxs-lookup"><span data-stu-id="1debc-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="1debc-144">Zoals u kunt zien van de bovenstaande voorbeeldcode, er is geen fout vastgelegd is geïmplementeerd en de service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als de service alleen invoer numerieke waarden op het moment van het maken van deze webservice.</span><span class="sxs-lookup"><span data-stu-id="1debc-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="1debc-145">Ook de service momenteel worden verwerkt beperkt gegevensgrootte, behoren tot de aard van de aanvraag/antwoord van de aanroep van webservice en het feit dat het model is wordt passen elke keer dat de webservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1debc-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="1debc-146">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="1debc-146">FAQ</span></span>
<span data-ttu-id="1debc-147">Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1debc-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

