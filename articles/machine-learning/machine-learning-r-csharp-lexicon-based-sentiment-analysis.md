---
title: AAA(deprecated) Lexicon analyse op basis van gevoel - Azure | Microsoft Docs
description: (afgeschaft) Lexicon gebaseerd gevoel analyse
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="96482-103">(afgeschaft) Lexicon gebaseerd gevoel analyse</span><span class="sxs-lookup"><span data-stu-id="96482-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="96482-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="96482-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="96482-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="96482-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="96482-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="96482-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="96482-107">Hoe kunt u gebruikers adviezen en meten houding naar merken of onderwerpen in de online sociale netwerken, zoals Facebook boekt, tweets, revisies, enz.?</span><span class="sxs-lookup"><span data-stu-id="96482-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="96482-108">Gevoel analyse biedt een methode voor het analyseren van dergelijke vragen.</span><span class="sxs-lookup"><span data-stu-id="96482-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="96482-109">Er zijn doorgaans twee methoden voor gevoel analyse.</span><span class="sxs-lookup"><span data-stu-id="96482-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="96482-110">Een gebruikt een algoritme leren met supervisie en andere Hallo kan worden behandeld als zonder supervisie learning.</span><span class="sxs-lookup"><span data-stu-id="96482-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="96482-111">Een algoritme leren met supervisie een model classificatie wordt doorgaans bouwt voort op een grote aantekeningen corpus.</span><span class="sxs-lookup"><span data-stu-id="96482-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="96482-112">De nauwkeurigheid is voornamelijk gebaseerd op Hallo kwaliteit Hallo aantekening en meestal Hallo trainingsproces duurt lang duren.</span><span class="sxs-lookup"><span data-stu-id="96482-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="96482-113">Behalve dat wanneer we toepassing hello algoritme tooanother domein is Hallo resultaat doorgaans niet goed.</span><span class="sxs-lookup"><span data-stu-id="96482-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="96482-114">Vergeleken toosupervised learning, lexicon gebaseerde zonder supervisie learning maakt gebruik van een woordenboek gevoel, die niet vereist voor het opslaan van een grote hoeveelheden gegevens corpus en training - waardoor Hallo hele proces veel sneller.</span><span class="sxs-lookup"><span data-stu-id="96482-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="96482-115">Onze [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is gebouwd op Hallo MPQA subjectieve aspect Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), een van de meest gebruikte Hallo subjectieve aspect lexicons.</span><span class="sxs-lookup"><span data-stu-id="96482-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="96482-116">Er zijn 5097 negatieve en 2533 positief woorden in MPQA.</span><span class="sxs-lookup"><span data-stu-id="96482-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="96482-117">En al deze woorden zijn voorzien van een sterke of zwakke polariteit.</span><span class="sxs-lookup"><span data-stu-id="96482-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="96482-118">Hallo hele corpus ligt onder de GNU General Public License.</span><span class="sxs-lookup"><span data-stu-id="96482-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="96482-119">Hallo-webservice kan worden toegepast tooany korte zinnen, zoals tweets en Facebook-berichten.</span><span class="sxs-lookup"><span data-stu-id="96482-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="96482-120">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="96482-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="96482-121">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="96482-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="96482-122">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="96482-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="96482-123">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="96482-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="96482-124">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="96482-124">Consumption of web service</span></span>
<span data-ttu-id="96482-125">Hallo invoergegevens kan geen tekst, maar Hallo webservice beter werkt met korte zinnen.</span><span class="sxs-lookup"><span data-stu-id="96482-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="96482-126">Hallo-uitvoer is een numerieke waarde tussen 1 en 1 liggen.</span><span class="sxs-lookup"><span data-stu-id="96482-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="96482-127">Een waarde lager dan 0 geeft aan dat Hallo gevoel van tekst hello negatief is; positief indien hoger dan 0.</span><span class="sxs-lookup"><span data-stu-id="96482-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="96482-128">Hallo absolute waarde van Hallo resultaat geeft Hallo sterkte van gevoel Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="96482-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="96482-129">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="96482-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="96482-130">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="96482-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="96482-131">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="96482-131">Starting C# code for web service consumption:</span></span>
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



<span data-ttu-id="96482-132">Hallo-invoer is 'Vandaag is een goede dag'.</span><span class="sxs-lookup"><span data-stu-id="96482-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="96482-133">Hallo-uitvoer is '1', waarmee wordt aangegeven van een positieve gevoel Hallo invoer zin gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="96482-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="96482-134">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="96482-134">Creation of web service</span></span>
> <span data-ttu-id="96482-135">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="96482-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="96482-136">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="96482-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="96482-137">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="96482-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="96482-138">In Azure Machine Learning, is een nieuw, leeg experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96482-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="96482-139">Hallo afbeelding hieronder toont Hallo experiment stroom van lexicon gebaseerde gevoel analyse.</span><span class="sxs-lookup"><span data-stu-id="96482-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="96482-140">Hallo 'sent_dict.csv' bestand Hallo MPQA subjectieve aspect lexicon is en is ingesteld als een van de invoerwaarden Hallo van [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="96482-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="96482-141">Een andere invoer is een steekproef revisie uit Hallo Amazon revisie gegevensset voor test, waar we selectie kolom naam wijziging, en bewerkingen splitsen.</span><span class="sxs-lookup"><span data-stu-id="96482-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="96482-142">We gebruiken een hash-pakket toostore Hallo subjectieve aspect lexicon in het Hallo-geheugen en Hallo score berekening proces versnellen.</span><span class="sxs-lookup"><span data-stu-id="96482-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="96482-143">volledige tekst Hello wordt tokenized door 'tm' pakket en vergeleken met de Hallo woord in Hallo gevoel woordenboek.</span><span class="sxs-lookup"><span data-stu-id="96482-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="96482-144">Ten slotte wordt een score berekend door toe te voegen Hallo gewicht van elk woord subjectieve Hallo tekst.</span><span class="sxs-lookup"><span data-stu-id="96482-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="96482-145">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="96482-145">Experiment flow:</span></span>
![Experiment stroom][2]

#### <a name="module-1"></a><span data-ttu-id="96482-147">Module 1:</span><span class="sxs-lookup"><span data-stu-id="96482-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="96482-148">Hash-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="96482-148">Install hash package</span></span>
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="96482-149">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="96482-149">Limitations</span></span>
<span data-ttu-id="96482-150">Op basis van het lexicon gevoel analyse is vanuit het perspectief van een algoritme wordt een algemene gevoel analysis tool, die niet sneller dan Hallo classificatiemethode voor specifieke velden.</span><span class="sxs-lookup"><span data-stu-id="96482-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="96482-151">Hallo negatie probleem niet goed wordt behandeld.</span><span class="sxs-lookup"><span data-stu-id="96482-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="96482-152">We hardcode verschillende negatie woorden in onze programma, maar een betere manier is met behulp van een woordenboek negatie en bouwen van een of meer regels.</span><span class="sxs-lookup"><span data-stu-id="96482-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="96482-153">Hallo-webservice presteert beter op korte en eenvoudige zinnen, zoals tweets en Facebook-berichten, dan op de lange en complexe zinnen zoals Amazon beoordelingen.</span><span class="sxs-lookup"><span data-stu-id="96482-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="96482-154">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="96482-154">FAQ</span></span>
<span data-ttu-id="96482-155">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="96482-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


