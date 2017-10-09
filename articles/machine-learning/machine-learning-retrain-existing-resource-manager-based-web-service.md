---
title: een bestaande voorspellende aaaRetrain webservice | Microsoft Docs
description: Meer informatie over hoe Hallo web service toouse Hallo zojuist getrainde model in Azure Machine Learning tooretrain een model en bij te werken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Een bestaande voorspellende webservice opnieuw trainen
Dit document beschrijft Hallo retraining-proces voor Hallo scenario te volgen:

* U hebt een trainingsexperiment en een Voorspellend experiment die u hebt geïmplementeerd als een geoperationaliseerd webservice.
* U hebt nieuwe gegevens die u uw predictive web service toouse tooperform de score berekenen wilt.

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

Beginnen met uw bestaande webservice en experimenten, moet u toofollow deze stappen:

1. Hallo model bijwerken.
   1. De training experiment tooallow voor web-service in- en uitgangen wijzigen.
   2. Hallo trainingsexperiment implementeren als een retraining-webservice.
   3. Hallo trainingsexperiment Batch uitvoering Service (BES) tooretrain Hallo model gebruiken.
2. Gebruik hello Azure Machine Learning PowerShell-cmdlets tooupdate Hallo Voorspellend experiment.
   1. Meld u aan tooyour Azure Resource Manager-account.
   2. Hallo webservicedefinitie ophalen.
   3. Hallo webservicedefinitie als JSON exporteren.
   4. Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.
   5. Hallo JSON importeren in de definitie van een web-service.
   6. Hallo webservice bijwerken met de definitie van een nieuwe web-service.

## <a name="deploy-hello-training-experiment"></a>Hallo trainingsexperiment implementeren
Hallo trainingsexperiment toodeploy als retraining webservice, moet u web service in- en uitgangen toohello model toevoegen. Door verbinding te maken een *Web Service uitvoer* module toohello experiment  *[Train Model] [ train-model]*  module u Hallo training experiment inschakelen een nieuw getraind model die u in uw Voorspellend experiment gebruiken kunt tooproduce. Als u hebt een *Evaluate Model* -module, kunt u ook web service uitvoer tooget Hallo evaluatieresultaten koppelen als uitvoer.

tooupdate uw trainingsexperiment:

1. Verbinding maken met een *Web Service invoer* module tooyour gegevensinvoer (bijvoorbeeld een *Clean Missing Data* module). Normaal gesproken gewenste tooensure die uw invoergegevens verwerkt in Hallo op dezelfde manier als uw oorspronkelijke trainingsgegevens.
2. Verbinding maken met een *Web Service uitvoer* module toohello uitvoer van uw *Train Model* module.
3. Als u hebt een *Evaluate Model* module en u wilt dat toooutput Hallo evaluatieresultaten, verbinding maken met een *Web Service uitvoer* module toohello uitvoer van uw *Evaluate Model* module.

Voer uw experiment.

Vervolgens moet u Hallo trainingsexperiment implementeren als een webservice die een getraind model en de resultaten van evaluatie van model produceert.  

Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld**, en selecteer vervolgens **Web Service implementeren [New]**. Hello Azure Machine Learning-webservices wordt geopend toohello **webservice implementeren** pagina. Typ een naam voor uw web-service, kies een betaald abonnement en klik vervolgens op **implementeren**. U kunt Hallo Batchuitvoering methode alleen gebruiken voor het maken van modellen getraind.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Hallo-model met nieuwe gegevens met behulp van BES Retrain
In dit voorbeeld we toocreate Hallo C# retraining toepassing gebruiken. U kunt deze taak ook Python of R voorbeeld code tooaccomplish.

toocall hello retraining API's:

1. Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.
2. Meld u aan toohello Machine Learning Web Services-portal.
3. Klik op Hallo webservice waarmee u werkt.
4. Klik op **verbruiken**.
5. Hallo Hallo onderaan in **verbruiken** pagina in Hallo **voorbeeldcode** sectie, klikt u op **Batch**.
6. Hallo C# voorbeeldcode voor Batchuitvoering Kopieer en plak deze in het bestand Program.cs Hallo. Zorg ervoor dat die naamruimte Hallo blijft intact.

Hallo NuGet-pakket Microsoft.AspNet.WebApi.Client, zoals opgegeven in Hallo opmerkingen toevoegen. tooadd hello verwijzing tooMicrosoft.WindowsAzure.Storage.dll mogelijk moet u eerst tooinstall hello [-clientbibliotheek voor Azure Storage-services](https://www.nuget.org/packages/WindowsAzure.Storage).

Hallo volgende schermafbeelding ziet u Hallo **verbruiken** pagina in hello Azure Machine Learning-webservices-portal.

![Pagina gebruiken][1]

### <a name="update-hello-apikey-declaration"></a>Hallo apikey declaratie bijwerken
Zoek Hallo **apikey** declaratie:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

In Hallo **Basic verbruik info** sectie Hallo **verbruiken** pagina, Ga naar de primaire sleutel Hallo en kopieer het toohello **apikey** declaratie.

### <a name="update-hello-azure-storage-information"></a>Hello Azure Storage-gegevens bijwerken
Hallo BES voorbeeldcode uploadt een bestand van een lokale schijf (bijvoorbeeld ' C:\temp\CensusIpnput.csv') tooAzure opslag, verwerkt en schrijft Hallo resultaten back tooAzure opslag.  

tooupdate hello Azure Storage-gegevens, moet u Hallo naam, de sleutel en de container voor uw opslagaccount van Hallo klassieke Azure-portal en vervolgens update Hallo correspondi na het uitvoeren van uw experiment Hallo resulterende storage-account ophalen de werkstroom moet vergelijkbaar toohello volgende zijn:

![Resulterende werkstroom na het uitvoeren van][4]NG waarden in Hallo-code.

1. Meld u aan toohello klassieke Azure-portal.
2. Klik in Hallo linkernavigatievenster kolom op **opslag**.
3. Selecteer één toostore hello retrained vanuit Hallo lijst met opslagaccounts, model.
4. Klik onder aan de pagina Hallo Hallo op **toegangssleutels beheren**.
5. Kopiëren en opslaan van Hallo **primaire toegangssleutel** en sluiten Hallo dialoogvenster.
6. Bovenaan Hallo Hallo pagina, klikt u op **Containers**.
7. Selecteer een bestaande container of maak een nieuwe en Hallo naam worden opgeslagen.

Zoek Hallo *StorageAccountName*, *StorageAccountKey*, en *StorageContainerName* declaraties en update Hallo waarden die u vanuit de klassieke portal Hallo opgeslagen .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Ook moet u ervoor zorgen dat Hallo-bestand voor invoer is beschikbaar op Hallo locatie die u in het Hallo-code opgeeft.

### <a name="specify-hello-output-location"></a>Hallo uitvoerlocatie opgeven
Wanneer u de uitvoerlocatie Hallo in Hallo Request-nettolading opgeeft, uitbreiding van Hallo-bestand dat is opgegeven in Hallo *RelativeLocation* moet worden opgegeven als `ilearner`. Zie Hallo voorbeeld te volgen:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Hallo Hieronder volgt een voorbeeld van uitvoer retraining: ![Retraining uitvoer][6]

## <a name="evaluate-hello-retraining-results"></a>Hallo retraining resultaten evalueren
Wanneer u de toepassing hello uitvoert, omvat Hallo uitvoer Hallo-URL en gedeelde handtekeningen toegangstoken dat nodig tooaccess Hallo evaluatieresultaten zijn.

Ziet u prestatieresultaten Hallo van Hallo retrained model door een combinatie van Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten voor *output2* (zoals weergegeven in de voorgaande afbeelding uitvoer retraining Hallo) en Hallo volledige URL in de adresbalk van de browser Hallo plakken.  

Hallo resultaten toodetermine onderzoeken of Hallo zojuist getraind model functioneert goed genoeg tooreplace Hallo een bestaande.

Kopiëren Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten.

## <a name="retrain-hello-web-service"></a>Opnieuw trainen Hallo-webservice
Wanneer u een nieuwe webservice opnieuw trainen, werkt u Hallo voorspellende web service definitie tooreference Hallo nieuwe getrainde model. Hallo webservicedefinitie is een interne representatie van het getrainde model van de webservice Hallo Hallo en kan niet rechtstreeks worden gewijzigd. Zorg ervoor dat u voor uw Voorspellend experiment en niet uw trainingsexperiment Hallo webservicedefinitie ophaalt.

## <a name="sign-in-tooazure-resource-manager"></a>Meld u aan tooAzure Resource Manager
U moet zich eerst aanmelden tooyour Azure-account uit binnen Hallo PowerShell-omgeving met behulp van Hallo [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Hallo webservicedefinitie object ophalen
Haal vervolgens Hallo webservicedefinitie object door aanroepen Hallo [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Resourcegroepnaam van een bestaande webservice Hallo Get AzureRmMlWebService cmdlet zonder parameters toodisplay Hallo webservices uitvoeren in uw abonnement. Zoek Hallo webservice en zoek vervolgens naar de web service-ID. Hallo-naam van de resourcegroep Hallo Hallo vierde element in het Hallo-ID is direct na Hallo *resourceGroups* element. Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

U kunt ook toodetermine hello Resourcegroepnaam van een bestaande webservice, toohello Azure Machine Learning-webservices portal aanmelden. Hallo-webservice selecteren. naam resourcegroep Hallo Hallo vijfde element van het Hallo-URL van webservice hello, wordt direct na Hallo *resourceGroups* element. Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Hallo webservicedefinitie object exporteren als JSON
Nieuw getraind model toomodify Hallo definitie van Hallo getrainde model toouse hello, moet u eerst hello gebruiken [Export AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport het bestand tooa JSON-indeling.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Update Hallo referentie toohello ilearner-blob
Zoek in Hallo activa, Hallo [getraind model] update Hallo *uri* waarde in Hallo *locationInfo* knooppunt met Hallo URI van Hallo ilearner-blob. Hallo URI gegenereerd door een combinatie van Hallo *BaseLocation* en Hallo *RelativeLocation* van uitvoer Hallo Hallo BES retraining-aanroep.

     "asset3": {
        "name": "Retrain Sample [trained model]",
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

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Hallo JSON importeren in een object van de webservicedefinitie
Moet u Hallo [importeren AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hallo JSON-bestand weer in een webservicedefinitie-object waarmee u tooupdate hello predicative experiment kunt is gewijzigd.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Hallo webservice bijwerken
Gebruik tot slot Hallo [Update AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hallo Voorspellend experiment.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
