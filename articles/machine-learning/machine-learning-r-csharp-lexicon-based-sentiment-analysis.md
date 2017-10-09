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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(afgeschaft) Lexicon gebaseerd gevoel analyse

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hoe kunt u gebruikers adviezen en meten houding naar merken of onderwerpen in de online sociale netwerken, zoals Facebook boekt, tweets, revisies, enz.? Gevoel analyse biedt een methode voor het analyseren van dergelijke vragen.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Er zijn doorgaans twee methoden voor gevoel analyse. Een gebruikt een algoritme leren met supervisie en andere Hallo kan worden behandeld als zonder supervisie learning. Een algoritme leren met supervisie een model classificatie wordt doorgaans bouwt voort op een grote aantekeningen corpus. De nauwkeurigheid is voornamelijk gebaseerd op Hallo kwaliteit Hallo aantekening en meestal Hallo trainingsproces duurt lang duren. Behalve dat wanneer we toepassing hello algoritme tooanother domein is Hallo resultaat doorgaans niet goed. Vergeleken toosupervised learning, lexicon gebaseerde zonder supervisie learning maakt gebruik van een woordenboek gevoel, die niet vereist voor het opslaan van een grote hoeveelheden gegevens corpus en training - waardoor Hallo hele proces veel sneller. 

Onze [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is gebouwd op Hallo MPQA subjectieve aspect Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), een van de meest gebruikte Hallo subjectieve aspect lexicons. Er zijn 5097 negatieve en 2533 positief woorden in MPQA. En al deze woorden zijn voorzien van een sterke of zwakke polariteit. Hallo hele corpus ligt onder de GNU General Public License. Hallo-webservice kan worden toegepast tooany korte zinnen, zoals tweets en Facebook-berichten. 

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Hallo invoergegevens kan geen tekst, maar Hallo webservice beter werkt met korte zinnen. Hallo-uitvoer is een numerieke waarde tussen 1 en 1 liggen. Een waarde lager dan 0 geeft aan dat Hallo gevoel van tekst hello negatief is; positief indien hoger dan 0. Hallo absolute waarde van Hallo resultaat geeft Hallo sterkte van gevoel Hallo die zijn gekoppeld. 

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
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



Hallo-invoer is 'Vandaag is een goede dag'. Hallo-uitvoer is '1', waarmee wordt aangegeven van een positieve gevoel Hallo invoer zin gekoppeld. 

## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.
> 
> 

In Azure Machine Learning, is een nieuw, leeg experiment gemaakt. Hallo afbeelding hieronder toont Hallo experiment stroom van lexicon gebaseerde gevoel analyse. Hallo 'sent_dict.csv' bestand Hallo MPQA subjectieve aspect lexicon is en is ingesteld als een van de invoerwaarden Hallo van [R-Script uitvoeren][execute-r-script]. Een andere invoer is een steekproef revisie uit Hallo Amazon revisie gegevensset voor test, waar we selectie kolom naam wijziging, en bewerkingen splitsen. We gebruiken een hash-pakket toostore Hallo subjectieve aspect lexicon in het Hallo-geheugen en Hallo score berekening proces versnellen. volledige tekst Hello wordt tokenized door 'tm' pakket en vergeleken met de Hallo woord in Hallo gevoel woordenboek. Ten slotte wordt een score berekend door toe te voegen Hallo gewicht van elk woord subjectieve Hallo tekst. 

### <a name="experiment-flow"></a>Stroom experiment:
![Experiment stroom][2]

#### <a name="module-1"></a>Module 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Hash-pakket installeren
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



## <a name="limitations"></a>Beperkingen
Op basis van het lexicon gevoel analyse is vanuit het perspectief van een algoritme wordt een algemene gevoel analysis tool, die niet sneller dan Hallo classificatiemethode voor specifieke velden. Hallo negatie probleem niet goed wordt behandeld. We hardcode verschillende negatie woorden in onze programma, maar een betere manier is met behulp van een woordenboek negatie en bouwen van een of meer regels. Hallo-webservice presteert beter op korte en eenvoudige zinnen, zoals tweets en Facebook-berichten, dan op de lange en complexe zinnen zoals Amazon beoordelingen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


