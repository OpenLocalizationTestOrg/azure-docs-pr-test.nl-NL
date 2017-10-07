---
title: een Machine Learning-Model aaaRetrain | Microsoft Docs
description: Meer informatie over hoe Hallo Web service toouse Hallo zojuist getrainde model in Azure Machine Learning tooretrain een model en bij te werken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Opnieuw een Machine Learning-Model te trainen
Het model is als onderdeel van het proces van uitoefening van machine learning-modellen in Azure Machine Learning Hallo getraind en opgeslagen. Vervolgens gebruikt u deze toocreate predicative Web-service. Hallo-webservice kan vervolgens worden gebruikt in websites, dashboards en mobiele apps. 

U maakt met behulp van Machine Learning modellen zijn meestal niet statisch. Zodra er nieuwe gegevens beschikbaar of wanneer de consument Hallo Hallo API heeft moet hun eigen Hallo gegevensmodel toobe retrained. 

Retraining kan vaak optreden. Met Hallo programmatische Retraining API-functie kunt u programmatisch opnieuw trainen via Hallo Retraining API's en update Hallo webservice met nieuwe getrainde model Hallo Hallo-model. 

Dit document beschrijft Hallo retraining proces en ziet u hoe toouse Hallo Retraining API's.

## <a name="why-retrain-defining-hello-problem"></a>Waarom retrain: Hallo probleem definiëren
Een model wordt getraind met een verzameling van gegevens als onderdeel van Hallo machine learning training proces. U maakt met behulp van Machine Learning modellen zijn meestal niet statisch. Zodra er nieuwe gegevens beschikbaar of wanneer de consument Hallo Hallo API heeft moet hun eigen Hallo gegevensmodel toobe retrained.

In deze scenario's, een programmatische API biedt een handige manier tooallow u of Hallo consument van uw API's toocreate een client die u kunt op eenmalige of regelmatige basis retrain Hallo-model met hun eigen gegevens. Vervolgens kunnen ze evalueren van de resultaten van de retraining Hallo en Hallo Web service API toouse Hallo zojuist getraind model bijwerken.

> [!NOTE]
> Als u een bestaande Trainingsexperiment en de nieuwe Web-service hebt, kunt u toocheck uit een bestaand voorspellende Web service in plaats van de volgende Hallo scenario vermeld in de volgende sectie Hallo Retrain.
> 
> 

## <a name="end-to-end-workflow"></a>End-to-end werkstroom
Hallo proces omvat Hallo volgende onderdelen: een Trainingsexperiment en een Voorspellend Experiment gepubliceerd als een webservice. tooenable retraining van een getraind model Hallo Trainingsexperiment moet worden gepubliceerd als een webservice met Hallo-uitvoer van een getraind model. Hierdoor API toegang toohello model voor retraining. 

Hallo stappen te volgen toepassing tooboth nieuw en klassieke Web services:

Hallo initiële voorspellende-webservice maken:

* Een trainingsexperiment maken
* Een web Voorspellend experiment maken
* Een predictive webservice implementeren

Opnieuw trainen Hallo-webservice:

* Training experiment tooallow voor retraining bijwerken
* Hallo retraining-webservice implementeren
* Hallo Batch-Service voor uitvoering van code tooretrain Hallo-model te gebruiken

Zie voor een overzicht van de vorige stappen Hallo [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

Als u een klassieke webservice geïmplementeerd:

* Een nieuw eindpunt op Hallo voorspellende webservice maken
* Hallo PATCH URL's en code ophalen
* Gebruik Hallo PATCH URL toopoint Hallo nieuwe eindpunt op Hallo retrained model 

Zie voor een overzicht van de vorige stappen Hallo [opnieuw trainen een klassieke webservice](machine-learning-retrain-a-classic-web-service.md).

Als u in een klassieke webservice retraining moeilijkheden uitvoert, Zie [probleemoplossing Hallo retraining van een Azure Machine Learning klassieke webservice](machine-learning-troubleshooting-retraining-models.md).

Als u een nieuwe webservice geïmplementeerd:

* Meld u aan tooyour Azure Resource Manager-account
* Hallo webservicedefinitie ophalen
* Hallo webservicedefinitie exporteren als JSON
* Hallo verwijzing toohello bijwerken `ilearner` blob in Hallo JSON
* Hallo JSON importeren in de definitie van een Web-Service
* Hallo webservice bijwerken met definitie van een nieuwe Web-Service

Zie voor een overzicht van de vorige stappen Hallo [opnieuw trainen Hallo Machine Learning Management PowerShell-cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).

Hallo-proces voor het instellen van de retraining voor een klassieke webservice omvat Hallo stappen te volgen:

![Overzicht van het proces retraining][1]

Hallo-proces voor het instellen van de retraining voor een nieuwe webservice omvat Hallo stappen te volgen:

![Overzicht van het proces retraining][7]

## <a name="other-resources"></a>Meer informatie
* [Retraining en bijwerken van Azure Machine Learning-modellen met Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [Groot aantal Machine Learning-modellen en web service-eindpunten maken van een experiment met behulp van PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Hallo [AML Retraining modellen met behulp van API's](https://www.youtube.com/watch?v=wwjglA8xllg) video ziet u hoe een Machine Learning-modellen tooretrain gemaakt in Azure Machine Learning met Hallo Retraining API's en PowerShell.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

