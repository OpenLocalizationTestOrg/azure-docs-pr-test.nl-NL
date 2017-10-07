---
title: aaaPowerShell-module voor Machine Learning | Microsoft Docs
description: Hallo PowerShell-module voor Azure Machine Learning is beschikbaar in de openbare preview-modus. Gebruik PowerShell toocreate en werkruimten, experimenten en webservices te beheren.
keywords: experiment,lineaire regressie,machine learning-algoritmen,zelfstudie over machine learning,voorspellende modelleringstechnieken,gegevenswetenschapexperiment
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>PowerShell-module voor Microsoft Azure Machine Learning
Hallo PowerShell-module voor Azure Machine Learning is een krachtig hulpprogramma waarmee u toouse Windows PowerShell toomanage werkruimten, experimenten gegevenssets, klassieke webservices en meer.

U kunt bekijken Hallo documentatie en Hallo-module, samen met de volledige broncode hello, downloaden op [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> Hello Azure Machine Learning PowerShell-module is momenteel in voorbeeldmodus. Hallo module blijven toobe verbeterd en uitgebreid in deze preview-periode. Let op Hallo [Cortana Intelligence en Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) voor nieuws en informatie.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Wat is Machine Learning PowerShell-module voor Hallo?
Hallo Machine Learning PowerShell-module is een. Op basis van NET DLL-module waarmee u toofully beheren Azure Machine Learning werkruimten, experimenten gegevenssets, klassieke webservices en klassieke webservice-eindpunten vanuit Windows PowerShell. 

Samen met de module hello, kunt u downloaden Hallo volledige broncode foutloos gescheiden waaronder [C# API-laag](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). U kunt verwijzen naar dit dll-bestand van uw eigen .NET-project en beheren van Azure Machine Learning via .NET-code. Hallo DLL is bovendien afhankelijk van onderliggende REST-API's die u rechtstreeks vanuit uw favoriete client kunt gebruiken.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Wat kan ik doen met Hallo PowerShell-module
Hier zijn enkele Hallo kunt u taken met deze PowerShell-module uitvoeren. Bekijk Hallo [volledige documentatie](https://aka.ms/amlps) voor deze en veel meer functies.

* Een nieuwe werkruimte inrichten met behulp van een beheercertificaat ([New AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Een JSON-bestand dat een experimentgrafiek weergeeft exporteren en importeren ([Export- AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) en [Import- AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Een experiment uitvoeren ([Start AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Een webservice buiten een voorspellend experiment maken ([New AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Maken van een eindpunt op een gepubliceerde webservice ([toevoegen AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Een RRS- en/of BES-webservice-eindpunt aanroepen ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) en [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Hier volgt een kort voorbeeld van het gebruik van PowerShell toorun een bestaande experiment:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Zie voor een uitgebreidere gebruiksvoorbeeld in dit artikel over het gebruik van Hallo PowerShell-module tooautomate een taak vaak aangevraagd: [veel Machine Learning-modellen en web service-eindpunten maken van een experiment met behulp van PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Hoe ga ik aan de slag?
tooget de slag met Machine Learning PowerShell, downloaden Hallo [releasepakket](https://github.com/hning86/azuremlps/releases) van GitHub en volg Hallo [instructies voor de installatie](https://github.com/hning86/azuremlps/blob/master/README.md). Hallo instructies wordt uitgelegd hoe toounblock Hallo gedownload/uitgepakt dll-bestand en vervolgens importeren in uw PowerShell-omgeving. De meeste Hallo cmdlets vereisen dat u Hallo werkruimte-ID, Hallo werkruimte verificatietoken, geef en Azure-regio die werkruimte Hallo Hallo heeft. Hallo eenvoudigste manier tooprovide Hallo waarden is via een standaardbestand config.json. Hallo instructies wordt ook uitgelegd hoe tooconfigure dit bestand. 

En als u wilt, kunt u klonen Hallo git structuur, wijzigen Hallo code, en lokaal met behulp van Visual Studio worden gecompileerd.

## <a name="next-steps"></a>Volgende stappen
U vindt de volledige documentatie Hallo voor Hallo PowerShell-module op [https://aka.ms/amlps](https://aka.ms/amlps). 

Voor een uitgebreid voorbeeld van hoe toouse module in een Praktijkscenario hello, uitchecken Hallo diepgaande gebruiksvoorbeeld, [veel Machine Learning-modellen en web service-eindpunten maken van een experiment met behulp van PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
