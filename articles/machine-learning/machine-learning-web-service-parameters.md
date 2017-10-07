---
title: Parameters voor Azure Machine Learning Web Service aaaUse | Microsoft Docs
description: Hoe Hallo toouse Azure Machine Learning Webserviceparameters toomodify gedrag van uw model wanneer Hallo-webservice wordt geopend.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Parameters voor Azure Machine Learning-webservice
Een Azure Machine Learning-webservice wordt gemaakt door het publiceren van een experiment die modules met configureerbare parameters bevat. In sommige gevallen kunt u toochange Hallo module gedrag tijdens het Hallo-webservice wordt uitgevoerd. *Web-Service Parameters* kunt u toodo deze taak. 

Een veelvoorkomend voorbeeld tot stand brengen van Hallo [importgegevens] [ reader] module dus die gebruiker Hallo Hallo gepubliceerd web-service een andere gegevensbron kunt opgeven wanneer Hallo-webservice wordt geopend. Of het configureren van Hallo [gegevens exporteren] [ writer] module zodat een andere bestemming kan worden opgegeven. Enkele andere voorbeelden zijn als u het aantal bits voor Hallo Hallo [hash-functie] [ feature-hashing] module of Hallo aantal gewenste functies voor Hallo [Functieselectie op basis van het Filter] [ filter-based-feature-selection] module. 

U kunt de Parameters van de Web-Service en koppel deze aan een of meer moduleparameters in uw experiment en kunt u opgeven of ze vereist of optioneel zijn. gebruiker van de webservice Hallo Hallo kunt vervolgens waarden opgeven voor deze parameters wanneer ze Hallo-webservice aanroept. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Hoe tooset en gebruik Webserviceparameters
U definieert u een Web Service-Parameter op Hallo pictogram volgende toohello-parameter voor een module en selecteer 'Instellen als web Serviceparameter'. Hiermee maakt u een nieuwe Web Service-Parameter en toothat module parameter is verbonden. Vervolgens als Hallo-webservice wordt geopend, Hallo-gebruiker kan een waarde voor Hallo Web Service Parameter opgeven en het toegepaste toohello module parameter is.

Als u een Parameter van Web Service definieert, is beschikbaar tooany andere module-parameter in Hallo-experiment. Als u een Web Service-Parameter die is gekoppeld aan een parameter voor één module definieert, kunt u die dezelfde Web Service-Parameter voor module, zolang Hallo parameter Hallo dezelfde waarde soort verwacht. Bijvoorbeeld, als Hallo Web Service Parameter een numerieke waarde is, kan klikt u vervolgens alleen worden gebruikt voor de parameters van de module die een numerieke waarde verwacht. Wanneer het Hallo-gebruiker een waarde voor Hallo Web Service Parameter wordt ingesteld, zal de parameters van de module toegepaste tooall die zijn gekoppeld zijn.

U kunt bepalen of een standaard tooprovide waarde voor Hallo Web Service-Parameter. Als u dit doet, klikt u vervolgens Hallo is parameter optioneel voor gebruiker Hallo van Hallo-webservice. Als u een standaardwaarde niet opgeeft, is Hallo gebruiker vereist tooenter een waarde wanneer Hallo-webservice wordt geopend.

Hallo API-documentatie voor de webservice Hallo bevat informatie voor Hallo web servicegebruiker op hoe toospecify Hallo Web Service Parameter programmatisch bij het openen van Hallo-webservice.

> [!NOTE]
> Hallo API-documentatie voor een klassieke webservice is opgegeven via Hallo **API help-pagina** koppeling in de webservice Hallo **DASHBOARD** in Machine Learning Studio. Hallo API-documentatie voor een nieuwe webservice is opgegeven via Hallo [Azure Machine Learning-webservices](https://services.azureml.net/Quickstart) portal op Hallo **verbruiken** en **Swagger API** pagina's voor uw Web-service.
> 
> 

## <a name="example"></a>Voorbeeld
Een voorbeeld: Stel hebben we een experiment met een [gegevens exporteren] [ writer] module die u informatie tooAzure blob-opslag verzendt. Definiëren we Web Service Parameter met de naam 'Blob-pad' waarmee Hallo web service gebruiker toochange Hallo pad toohello blobopslag wanneer Hallo-service wordt geopend.

1. Klik op Hallo in Machine Learning Studio [gegevens exporteren] [ writer] module tooselect deze. De eigenschappen worden weergegeven in Hallo eigenschappen deelvenster toohello rechts van het experimentcanvas Hallo.
2. Geef Hallo opslagtype:
   
   * Onder **Geef gegevensbestemming**, selecteert u 'Azure Blob Storage'.
   * Onder **Geef verificatietype**, selecteert u 'Account'.
   * Geef gegevens op Hallo voor hello Azure blob-opslag. 
     <p />
3.Klik op Hallo pictogram toohello rechts van Hallo **pad tooblob die begint met de parameter container**. Als volgt uitziet:
   
   ![Web Service Parameter-pictogram][icon]
   
   Selecteer 'Instellen als web Serviceparameter'.
   
   Een item wordt toegevoegd onder **Webserviceparameters** Hallo Hallo eigenschappendeelvenster waarvan Hallo 'pad tooblob begint met container' onderaan in. Dit Hallo Web Service-Parameter die is nu is gekoppeld aan dit [gegevens exporteren] [ writer] module-parameter.
4. toorename Hallo Web Service Parameter, klikt u op naam hello, voer 'Blob-pad' en druk op Hallo **Enter** sleutel. 
5. tooprovide een standaardwaarde voor Hallo Web Service-Parameter, klikt u op Hallo pictogram toohello rechts van het Hallo-naam, selecteer 'Provide standaardwaarde', voer een waarde (bijvoorbeeld ' container1/output1.csv') en druk op Hallo **Enter** sleutel.
   
   ![Web Service-Parameter][parameter]
6. Klik op **Run**. 
7. Klik op **webservice implementeren** en selecteer **webservice implementeren [klassieke]** of **Web Service implementeren [New]** toodeploy Hallo-webservice.

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

gebruiker van de webservice Hallo Hallo kunt nu een nieuwe bestemming voor Hallo opgeven [gegevens exporteren] [ writer] module bij het openen van Hallo-webservice.

## <a name="more-information"></a>Meer informatie
Zie voor een uitgebreider voorbeeld Hallo [Webserviceparameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) vermelding in Hallo [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Zie voor meer informatie over de toegang tot een Machine Learning-webservice [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

