---
title: aaaA voorspellende oplossing voor kredietrisico met Machine Learning | Microsoft Docs
description: Een gedetailleerde procedure hoe toocreate predictive analytics-oplossing voor tegoed risicoanalyse in Azure Machine Learning Studio.
keywords: kredietrisico, predictive analytics-oplossing, risico-evaluatie
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Procedure: een predictive analytics-oplossing opzetten voor kredietrisicobeoordeling in Azure Machine Learning

In dit overzicht nemen we een uitgebreide blik op Hallo-proces voor het ontwikkelen van een predictive analytics-oplossing in Machine Learning Studio. We een eenvoudige model in Machine Learning Studio ontwikkelen en vervolgens te implementeren als een Azure Machine Learning-webservice waar Hallo model voorspellingen met nieuwe gegevens kunt maken. 

In deze rondleiding gaan we ervan uit dat u Machine Learning Studio al minstens één keer hebt gebruikt en dat u enig inzicht hebt in de concepten van machine learning. Er wordt niet van uitgegaan dat u een expert bent.

Als u nog nooit hebt gebruikt **Azure Machine Learning Studio** voordat toostart met Hallo zelfstudie, kunt u [maken uw eerste gegevenswetenschap experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md). Deze zelfstudie leert u Machine Learning Studio voor Hallo eerst. Hier ziet u Hallo basisprincipes van hoe toodrag-en-neerzetten modules naar uw experiment ze met elkaar verbinden, Hallo experiment uitvoeren en bekijkt hello resultaten. Een ander hulpprogramma die mogelijk nuttig voor het aan de slag is een diagram waarin u een van Hallo-mogelijkheden van Machine Learning Studio overzicht. U kunt dit hier downloaden en afdrukken: [Overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Als u nieuwe toohello veld van machine learning in het algemeen, moet u er een video series die mogelijk nuttig tooyou is. Wordt aangeroepen [Gegevenswetenschap voor beginnende gebruikers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) en deze krijgt u een goede inleiding toomachine learning met alledaagse taal en -concepten.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>Hallo probleem

Stel dat u iemands kredietrisico op basis van Hallo informatie die ze in een kredietaanvraag heeft toopredict nodig.  

Kredietrisicobeoordeling is een complex probleem, maar in het kader van deze rondleiding stellen we de zaken wat eenvoudiger voor. We nemen kredietrisicobeoordeling als voorbeeld van hoe u een predictive analytics-oplossing kunt maken met behulp van Microsoft Azure Machine Learning. toodo, gebruiken we Azure Machine Learning Studio en een Machine Learning-webservice.  

## <a name="hello-solution"></a>Hallo-oplossing

In deze gedetailleerde rondleiding beginnen we met openbaar beschikbare kredietrisicogegevens, en ontwikkelen en trainen we op basis van die gegevens een voorspellend model. Vervolgens we Hallo model implementeren als een webservice zodat deze kan worden gebruikt door anderen voor kredietrisicobeoordeling.

toocreate deze oplossing voor kredietrisicobeoordeling, er als volgt te werk:  

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)
3. [Een experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
6. [Toegang Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> U vindt een werkexemplaar van Hallo experiment die we ontwikkelen in dit scenario in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Ga te**[scenario - tegoed risico voorspelling](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  en klik op **openen in Studio** toodownload een kopie van het Hallo-experiment in uw werkruimte van Machine Learning Studio.
> 
> In dit scenario is gebaseerd op een vereenvoudigde versie van het voorbeeldexperiment hello, [binaire classificatie: Credit risico voorspelling](http://go.microsoft.com/fwlink/?LinkID=525270), ook beschikbaar in Hallo [galerie](http://gallery.cortanaintelligence.com/).
