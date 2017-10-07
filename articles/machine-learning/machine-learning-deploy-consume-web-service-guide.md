---
title: 'Azure Machine Learning-webservices: De implementatie en het verbruik | Microsoft Docs'
description: Bronnen voor het implementeren en gebruiken van web-services.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Azure Machine Learning-webservices: implementatie en verbruik
U kunt Azure Machine Learning toodeploy machine learning-werkstromen en modellen als webservices gebruiken. Deze webservices kunnen vervolgens gebruikte toocall Hallo machine learning-modellen van toepassingen worden via Hallo Internet toodo voorspellingen in realtime of in de batchmodus. Omdat de webservices Hallo RESTful, kunt u ze aanroepen uit verschillende programmeertalen en platforms, zoals .NET en Java, en toepassingen, zoals Excel.

Hallo volgende secties vindt u koppelingen toowalkthroughs, code en documentatie toohelp slag ophalen.

## <a name="deploy-a-web-service"></a>Een webservice implementeren
### <a name="with-azure-machine-learning-studio"></a>Met Azure Machine Learning Studio
Machine Learning Studio en het Hallo-portal voor Microsoft Azure Machine Learning-webservices te implementeren en beheren van een webservice zonder code te schrijven.

Hallo volgende koppelingen vindt u algemene informatie over het toodeploy een nieuwe webservice:

* Voor een overzicht van hoe toodeploy een nieuwe webservice die gebaseerd op Azure Resource Manager, Zie [implementeren van een nieuwe webservice](machine-learning-webservice-deploy-a-web-service.md).
* Voor een overzicht over het toodeploy een webservice, Zie [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).
* Voor een overzicht over het toocreate en implementeren van een webservice, Zie [scenario stap 1: een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md).
* Zie voor specifieke voorbeelden die een webservice implementeert:

  * [Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
  * [Hoe toodeploy een web service toomultiple regio 's](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Met web services resourceprovider API's (Azure Resource Manager-API's)
Hello Azure Machine Learning resourceprovider voor web-services kan implementatie en beheer van web-services via REST API-aanroepen. Zie voor meer informatie de [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) verwijzing.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Met PowerShell-cmdlets
Azure Machine Learning-resourceprovider voor webservices kunt implementatie en beheer van web-services met behulp van PowerShell-cmdlets.

toouse hello cmdlets, u moet zich eerst aanmelden tooyour Azure-account uit binnen Hallo PowerShell-omgeving met behulp van Hallo [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Als u niet bekend bent met het hoe toocall PowerShell-opdrachten die op Resource Manager zijn gebaseerd, Zie [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport uw Voorspellend experiment, gebruikt u [deze voorbeeldcode](https://github.com/ritwik20/AzureML-WebServices). Nadat u Hallo .exe-bestand van het Hallo-code hebt gemaakt, kunt u het volgende typen:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Hallo toepassing uitvoert, maakt een web service JSON-sjabloon. toouse hello sjabloon toodeploy een webservice, moet u Hallo volgende informatie toevoegen:

* Naam van het opslagaccount en de sleutel

    U kunt Hallo opslagaccountnaam en sleutel ophalen van beide Hallo [Azure-portal](https://portal.azure.com/) of Hallo [klassieke Azure-portal](http://manage.windowsazure.com/).
* Het streven plan-ID

    U kunt Hallo plan-ID ophalen uit Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal aanmelden en de naam van een abonnement op.

Deze toohello JSON-sjabloon toevoegen als onderliggende Hallo *eigenschappen* knooppunt op Hallo van hetzelfde niveau als Hallo *MachineLearningWorkspace* knooppunt.

Hier volgt een voorbeeld:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Zie Hallo artikelen te volgen en voorbeeldcode voor meer informatie:

* [Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN
* Voorbeeld [scenario](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) op GitHub

## <a name="consume-hello-web-services"></a>Hallo-webservices gebruiken
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Hallo van Azure Machine Learning Web Services UI (getest)
U kunt uw webservice vanuit hello Azure Machine Learning-webservices portal testen. Dit omvat Hallo aanvraag en antwoord-service (RSS) testen en batchuitvoeringsservice (BES)-interfaces.

* [Een nieuwe webservice implementeren](machine-learning-webservice-deploy-a-web-service.md)
* [Een Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md)
* [Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Vanuit Excel
U kunt een Excel-sjabloon die de webservice Hallo verbruikt downloaden:

* [Een Azure Machine Learning-webservice vanuit Excel gebruiken](machine-learning-consuming-from-excel.md)
* [Excel-invoegtoepassing voor Azure Machine Learning-webservices](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Van een REST-client
Azure Machine Learning-webservices zijn RESTful-API's. U kunt deze API's van verschillende platforms, zoals .NET, Python, R, Java, enz. Hallo verbruiken **verbruiken** pagina voor uw webservice op Hallo [portal voor Microsoft Azure Machine Learning-webservices](https://services.azureml.net) voorbeeld heeft code die u kan helpen aan de slag. Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).
