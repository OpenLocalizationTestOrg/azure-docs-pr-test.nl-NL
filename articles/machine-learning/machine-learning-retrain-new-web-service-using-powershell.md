---
title: aaaRetrain een nieuwe Azure Machine Learning-webservice met PowerShell | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically een model en update Hallo web service toouse Hallo zojuist getraind model in Azure Machine Learning met Machine Learning Management PowerShell-cmdlets voor Hallo opnieuw trainen.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Een nieuwe Resource Manager gebaseerde webservice met Machine Learning Management PowerShell-cmdlets voor Hallo opnieuw trainen
Wanneer u een nieuwe webservice opnieuw trainen, werkt u Hallo voorspellende web service definitie tooreference Hallo nieuwe getrainde model.  

## <a name="prerequisites"></a>Vereisten
U moet instellen van een trainingsexperiment en een Voorspellend experiment zoals weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> Hallo Voorspellend experiment moet worden geïmplementeerd als een Azure Resource Manager (nieuw) op basis van machine learning-webservice. toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

Dit proces vereist dat u hello Azure Machine Learning-Cmdlets zijn geïnstalleerd. Zie voor informatie over het installeren van de Machine Learning-cmdlets Hallo Hallo [Azure Machine Learning-Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) -verwijzingen op MSDN.

Gekopieerde Hallo volgende informatie uit Hallo retraining uitvoer:

* BaseLocation
* RelativeLocation

Hallo stappen zijn:

1. Meld u aan tooyour Azure Resource Manager-account.
2. Hallo webservicedefinitie ophalen
3. Hallo webservicedefinitie exporteren als JSON
4. Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.
5. Hallo JSON importeren in de definitie van een Web-Service
6. Hallo webservice bijwerken met definitie van een nieuwe Web-Service

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Meld u aan tooyour Azure Resource Manager-account
U moet eerst tooyour Azure-account uit binnen Hallo PowerShell-omgeving met Hallo aanmelden [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition"></a>Hallo webservicedefinitie ophalen
Vervolgens ophalen Hallo Web Service door de aanroepende Hallo [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Hallo webservicedefinitie is een interne representatie van het getrainde model van de webservice Hallo Hallo en kan niet rechtstreeks worden gewijzigd. Zorg ervoor dat u voor uw Voorspellend experiment en niet uw trainingsexperiment Hallo webservicedefinitie ophaalt.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Resourcegroepnaam van een bestaande webservice Hallo Get AzureRmMlWebService cmdlet zonder parameters toodisplay Hallo webservices uitvoeren in uw abonnement. Zoek Hallo webservice en zoek vervolgens naar de web service-ID. Hallo-naam van de resourcegroep Hallo Hallo vierde element in het Hallo-ID is direct na Hallo *resourceGroups* element. Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

U kunt ook toodetermine hello Resourcegroepnaam van een bestaande webservice aanmelden toohello Microsoft Azure Machine Learning Web Services-portal. Hallo-webservice selecteren. naam resourcegroep Hallo Hallo vijfde element van het Hallo-URL van webservice hello, wordt direct na Hallo *resourceGroups* element. Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Hallo webservicedefinitie exporteren als JSON
toomodify hello definitie toohello getraind model toouse Hallo zojuist getrainde Model, moet u eerst hello gebruiken [Export AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport het bestand tooa JSON-indeling.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.
Zoek in Hallo activa, Hallo [getraind model] update Hallo *uri* waarde in Hallo *locationInfo* knooppunt met Hallo URI van Hallo ilearner-blob. Hallo URI gegenereerd door een combinatie van Hallo *BaseLocation* en Hallo *RelativeLocation* van uitvoer Hallo Hallo BES retraining-aanroep. Hiermee werkt Hallo pad tooreference Hallo nieuwe getrainde model.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>Hallo JSON importeren in de definitie van een Web-Service
Moet u Hallo [importeren AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hallo JSON-bestand weer in de definitie van een Web-Service waarmee u tooupdate hello webservicedefinitie kunt is gewijzigd.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Hallo webservice bijwerken met definitie van een nieuwe Web-Service
Gebruik tot slot [Update AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello webservicedefinitie.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Samenvatting
Hallo Machine Learning PowerShell-cmdlets voor beheer kunt u Hallo getraind model van een Voorspellend webservice inschakelen van scenario's zoals bijwerken:

* Periodieke model retraining met nieuwe gegevens.
* Distributie van een model toocustomers met Hallo doel van zodat ze opnieuw trainen Hallo-model met hun eigen gegevens.

