---
title: aaaALM in Azure Machine Learning | Microsoft Docs
description: Aanbevolen procedures van de levenscyclus van Toepassingsbeheer in Azure Machine Learning Studio toepassen
keywords: Versiebeheer voor Azure ML, levenscyclus van Toepassingsbeheer, ALM AML,
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Levenscyclus van Toepassingsbeheer in Azure Machine Learning Studio
Azure Machine Learning Studio is een hulpprogramma voor het ontwikkelen van machine learning-experimenten die zijn geoperationaliseerd in hello Azure-cloud-platform. Het lijkt dan Hallo Visual Studio IDE en schaalbare cloudservice samenvoegen in één enkel platform. U kunt de standaardprocedures van toepassing Lifecycle Management (ALM), van versioning verschillende activa tooautomated uitvoeren en implementatie, opnemen in Azure Machine Learning Studio. In dit artikel worden enkele Hallo-opties en methoden besproken.

## <a name="versioning-experiment"></a>Versiebeheer experiment
Er zijn twee manieren aanbevolen tooversion uw experimenten. U kunt ingebouwde uitvoeringsgeschiedenis zijn afhankelijk van of exporteren van Hallo experiment in JSON JavaScript Object Notation ()-indeling en extern beheren. Elke benadering wordt geleverd met de voor- en nadelen.

### <a name="experiment-snapshots-using-run-history"></a>Experiment momentopnamen aan de hand van de geschiedenis uitvoeren
In Hallo uitvoering model van Azure Machine Learning Studio learning-experiment, telkens wanneer u klikt op Hallo Hallo **uitvoeren** knop in momentopname van een niet-wijzigbaar van Hallo experiment-editor experiment Hallo is verzonden toohello Taakplanner. U kunt deze lijst van momentopnamen weergeven door te klikken op Hallo **geschiedenis uitvoeren** knop op de opdrachtbalk Hallo in Hallo experiment editor weergeven.

![Knop Geschiedenis uitvoeren](media/machine-learning-version-control/runhistory.png)

U kunt en vervolgens open Hallo momentopname in de modus vergrendeld door te klikken op Hallo-naam van het Hallo-experiment op Hallo tijd Hallo experiment is verzonden toorun en Hallo momentopname werd gemaakt. Merk op dat alleen Hallo eerste item in de lijst hello, dat de huidige experiment Hallo vertegenwoordigt, heeft een status worden bewerkt. U ziet dat elke momentopname kan zich in verschillende Status wordt ook statussen, met inbegrip van de voltooide (gedeeltelijk uitvoeren), is mislukt, mislukt (gedeeltelijk uitvoeren), of concept.

![Lijst met de geschiedenis uitvoeren](media/machine-learning-version-control/runhistorylist.png)

Nadat deze is geopend, kunt u Hallo momentopname experiment als een nieuw experiment opslaan en vervolgens te wijzigen. Als uw experiment momentopname activa zoals een getraind model, transformeren of gegevensset die versies bijgewerkt bevat, behoudt Hallo momentopname Hallo verwijst naar toohello oorspronkelijke versie wanneer Hallo momentopname werd gemaakt. Als u Hallo vergrendeld opslaat momentopname maken als een nieuw experiment Azure Machine Learning Studio detecteert Hallo bestaan van een nieuwere versie van deze elementen en wordt deze automatisch in nieuw experiment Hallo bijgewerkt.

Als u een experiment Hallo verwijdert, worden alle momentopnamen van die experiment verwijderd.

### <a name="exportimport-experiment-in-json-format"></a>Exporteren/importeren experiment in JSON-indeling
momentopnamen van de rapportgeschiedenis Hallo uitvoeren Houd een niet-wijzigbaar versie van het Hallo-experiment in Azure Machine Learning Studio telkens wanneer dit ingediende toorun is. U kunt ook een lokale kopie van Hallo experiment opslaan en inchecken tooyour favoriete bronbeheersysteem, zoals Team Foundation Server en later op een experiment die lokaal bestand opnieuw te maken. U kunt Hallo [Azure Machine Learning PowerShell](http://aka.ms/amlps) commandlets [ *Export AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) en [  *Importeren AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish die.

Hallo JSON-bestand is een tekstweergave van Hallo experimenteren grafiek, waaronder een tooassets verwijzing in de werkruimte Hallo zoals een dataset of een getraind model. Bevat een geserialiseerde versie is van Hallo actief. Als u tooimport Hallo JSON-document in Hallo workspace probeert, Hallo waarnaar wordt verwezen activa moeten al bestaan Hello dezelfde asset id's waarnaar wordt verwezen in Hallo experiment. Anders worden niet kunnen tooaccess Hallo geïmporteerd experiment.

## <a name="versioning-trained-model"></a>Versiebeheer getrainde model
Een getraind model in Azure Machine Learning wordt omgezet in een indeling die een bestand .iLearner genoemd en wordt opgeslagen in hello Azure Blob storage-account die is gekoppeld aan het Hallo-werkruimte. Er is een eenrichtingssessie tooget een kopie van Hallo .iLearner bestand via Hallo retraining API. [In dit artikel](machine-learning-retrain-models-programmatically.md) wordt uitgelegd hoe Hallo retraining API werkt. Hallo hoofdstappen:

1. Instellen van uw trainingsexperiment.
2. Voeg een web service uitvoer poort toohello Train Model-module of Hallo-module die produceert Hallo getrainde model, zoals Tune Model Hyperparameter of R-Model maken.
3. Voer uw trainingsexperiment en vervolgens te implementeren als een model training-webservice.
4. Hallo BES endpoint van Hallo training webservice aanroepen en geef Hallo gewenste .iLearner bestandsnaam en Blob storage-accountlocatie waar deze wordt opgeslagen.
5. Oogst Hallo geproduceerd .iLearner bestand na het aanroepen van Hallo BES is voltooid.

Een andere manier tooretrieve hello .iLearner bestand is via de PowerShell-commandlet Hallo [ *downloaden AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Dit wordt mogelijk gemakkelijker als u alleen een kopie van Hallo .iLearner bestand zonder Hallo nodig tooretrain Hallo model programmatisch tooget wilt.

Nadat u Hallo .iLearner bestand met de Hallo getrainde model hebt, kunt u vervolgens de strategie van uw eigen versiebeheer gebruiken. Hallo-strategie kan net zo eenvoudig als een vooraf/postfix als een naamgevingsconventie toepassen en laat Hallo .iLearner bestand in Blob storage of kopiëren/u deze importeert in uw versiebeheersysteem zijn.

Hallo opgeslagen .iLearner bestand kan vervolgens worden gebruikt voor het scoren via geïmplementeerde web-services.

## <a name="versioning-web-service"></a>Versiebeheer-webservice
U kunt twee soorten webservices van een Azure Machine Learning-experiment implementeren. Hallo-classic-webservice is nauw samen met de Hallo experiment, evenals Hallo-werkruimte. nieuwe webservice-Hallo hello Azure Resource Manager-framework gebruikt, en deze niet meer is gekoppeld aan de oorspronkelijke experiment Hallo of Hallo-werkruimte.

### <a name="classic-web-service"></a>Klassieke webservice
een klassieke webservice tooversion, kunt u profiteren van Hallo web service-eindpunt constructie. Hier volgt een typische stroom:

1. U implementeert een nieuwe klassieke webservice, waarin een standaardeindpunt van uw Voorspellend experiment.
2. U maakt een nieuw eindpunt met de naam ep2 waarmee de huidige versie Hallo van Hallo experiment/getraind model.
3. U gaat u terug en werk uw Voorspellend experiment en het getrainde model.
4. U Hallo Voorspellend experiment, Hallo standaardeindpunt vervolgens update opnieuw implementeren. Maar dit heeft geen invloed op ep2.
5. U maakt een extra eindpunt met de naam ep3 die beschrijft de nieuwe versie van de Hallo van Hallo experiment en getrainde model.
6. Ga terug toostep 3 indien nodig.

Gedurende een periode, moet u mogelijk veel eindpunten is gemaakt in Hallo dezelfde webservice. Elk eindpunt vertegenwoordigt een punt in tijd kopie van die Hallo punt in tijd versie van het getrainde model Hallo Hallo-experiment. Vervolgens kunt u externe logica toodetermine welke toocall eindpunt, waardoor effectief selecteren van een versie van Hallo getraind model voor het Hallo scoren uitvoeren.

U kunt ook veel identiek webservice-eindpunten maken en vervolgens patch verschillende versies van Hallo .iLearner bestand toohello eindpunt tooachieve vergelijkbaar effect. [In dit artikel](machine-learning-create-models-and-endpoints-with-powershell.md) in meer detail uitgelegd hoe tooaccomplish die.

### <a name="new-web-service"></a>Nieuwe webservice
Als u een nieuwe Azure Resource Manager gebaseerde web-service maakt, is Hallo eindpunt constructie niet meer beschikbaar. In plaats daarvan kunt u web service (WSD) definitiebestanden, in JSON-indeling genereren van uw Voorspellend experiment met behulp van Hallo [Export AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) PowerShell-cmdlet of met behulp van Hallo [ *Export AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) PowerShell-cmdlet van een geïmplementeerde Resource Manager gebaseerde webservice.

Nadat u hebt geëxporteerd Hallo WSD bestands- en -versie beheren, kunt u ook Hallo WSD implementeren als een nieuwe webservice in een ander web service-abonnement in een andere Azure-regio. Zorg ervoor dat u opgeeft Hallo juiste opslagaccount evenals Hallo nieuwe web-service-abonnement-ID. toopatch in verschillende .iLearner bestanden, kunt u Hallo WSD-bestand en update Hallo Locatieverwijzing Hallo getraind model en als een nieuwe webservice implementeren.

## <a name="automate-experiment-execution-and-deployment"></a>Experiment uitvoeren en implementatie automatiseren
Een belangrijk aspect van ALM is toobe kunnen tooautomate Hallo uitvoering en implementatieproces van de toepassing hello. In Azure Machine Learning, u kunt dit doen met behulp van Hallo [PowerShell-module](http://aka.ms/amlps). Hier volgt een voorbeeld van end-to-end-stappen die zich relevante tooa ALM automatische uitvoering/implementatie standaardproces Hallo met [Azure Machine Learning Studio PowerShell-module](http://aka.ms/amlps). Elke stap wordt de gekoppelde tooone of meer PowerShell commandlets waarmee u kunt tooaccomplish die stap.

1. [Uploaden van een gegevensset](https://github.com/hning86/azuremlps#upload-amldataset).
2. Kopiëren van een trainingsexperiment Hallo-werkruimte van een [werkruimte](https://github.com/hning86/azuremlps#copy-amlexperiment) of van [galerie](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), of [importeren](https://github.com/hning86/azuremlps#import-amlexperimentgraph) een [geëxporteerd](https://github.com/hning86/azuremlps#export-amlexperimentgraph) experimenteren uit lokale schijf.
3. [Hallo gegevensset bijwerken](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) Hallo training experiment.
4. [Voer Hallo trainingsexperiment](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Hallo getrainde model promoveren](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Kopiëren van een Voorspellend experiment](https://github.com/hning86/azuremlps#copy-amlexperiment) Hallo werkruimte te openen.
7. [Update Hallo getrainde model](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) in Hallo Voorspellend experiment.
8. [Hallo Voorspellend experiment uitvoeren](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Een webservice implementeren](https://github.com/hning86/azuremlps#new-amlwebservice) van Hallo Voorspellend experiment.
10. Hallo webservice testen [RRS](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) of [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) eindpunt.

## <a name="next-steps"></a>Volgende stappen
* Hallo downloaden [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) module en start tooautomate ALM taken.
* Meer informatie over hoe te[maken en beheren van grote aantallen ML modellen met behulp van slechts een enkele experiment](machine-learning-create-models-and-endpoints-with-powershell.md) via PowerShell en de retraining API.
* Meer informatie over [Azure Machine Learning-webservices implementeren](machine-learning-publish-a-machine-learning-web-service.md).
