---
title: 'Stap 6: Toegang tot Hallo Machine Learning-webservice | Microsoft Docs'
description: 'Stap 6 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: toegang tot een actieve Azure Machine Learning-webservice.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Overzicht stap 6: Toegang tot hello Azure Machine Learning-webservice

Dit is de laatste stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)
3. [Een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
6. **Toegang tot Hallo-webservice**

- - -
In de vorige stap Hallo in dit scenario wordt een webservice die gebruikmaakt van onze voorspelling van tegoed risicomodel geïmplementeerd. Nu dat gebruikers kunnen toosend gegevens tooit zijn en resultaten krijgen. 

Hallo-webservice is een Azure-web-service die u kunt ontvangen en retourneren van gegevens met behulp van REST-API's op twee manieren:  

* **Aanvragen/reacties** - Hallo gebruiker verzendt een of meer rijen met tegoed gegevens toohello service via een HTTP-protocol en Hallo service reageert met een of meer sets van resultaten.
* **Batchuitvoering** - Hallo gebruiker opslaat een of meer rijen tegoed gegevens in een Azure blob- en stuurt vervolgens Hallo blob locatie toohello-service. Hallo service scores die alle rijen van de gegevens in Hallo Hallo blob-invoerbron, winkels hello resulteert in een andere blob- en retourneert de URL van de container waarin Hallo.  

snelste en gemakkelijkste manier tooaccess een klassiek webservice via Hallo is Hallo [Web-App voor Azure ML aanvragen en antwoorden Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) of [Azure ML Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Deze web-app-sjablonen kunnen maken van een aangepaste web-app die u kent uw webservice invoergegevens en wat wordt geretourneerd. Toodo hoeft u access tooyour-webservice en gegevens bieden en Hallo sjabloon Hallo rest.

Zie voor meer informatie over het gebruik van de app websjablonen Hallo [een webservice Azure Machine Learning met een web-app-sjabloon gebruiken](machine-learning-consume-web-service-with-web-app-template.md).

U kunt ook een aangepaste toepassing tooaccess Hallo webservice met starter code voorzien in R, C# en Python programmeertalen ontwikkelen.

U vindt meer informatie in [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

