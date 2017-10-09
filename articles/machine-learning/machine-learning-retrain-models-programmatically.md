---
title: aaaRetrain Machine Learning-modellen programmatisch | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically opnieuw trainen model en update Hallo web service toouse Hallo nieuw model is getraind in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Machine Learning modellen programmatisch opnieuw trainen
In dit scenario leert u hoe een Azure Machine Learning-webservice met C# en Hallo Machine Learning-batchuitvoeringsservice in tooprogrammatically opnieuw trainen.

Zodra u hebt Hallo model retrained, tonen Hallo volgen scenario's hoe tooupdate Hallo-model in uw predictive webservice:

* Als u een webservice klassieke in Hallo Machine Learning-webservices-portal hebt geïmplementeerd, Zie [opnieuw trainen van een webservice klassieke](machine-learning-retrain-a-classic-web-service.md). 
* Als u een nieuwe webservice hebt geïmplementeerd, Zie [opnieuw trainen Hallo Machine Learning Management cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).

Zie voor een overzicht van Hallo proces retraining [opnieuw een Machine Learning-Model te trainen](machine-learning-retrain-machine-learning-model.md).

Als u wilt dat toostart met uw bestaande web-service op basis van nieuwe Azure Resource Manager, Zie [opnieuw trainen van een bestaande voorspellende webservice](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Een trainingsexperiment maken
In dit voorbeeld gebruikt u ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' van Hallo Microsoft Azure Machine Learning-voorbeelden. 

Hallo-experiment toocreate:

1. Aanmelden bij tooMicrosoft Azure Machine Learning Studio. 
2. Klik op Hallo rechterbenedenhoek van Hallo dashboard **nieuw**.
3. Selecteer in de Microsoft Samples hello, voorbeeld 5.
4. toorename hello experiment Hallo boven aan het experimentcanvas hello, selecteert u de naam van de Hallo-experiment "voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset '.
5. Type telling Model.
6. Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.
7. Klik op **instellen webservice** en selecteer **Retraining webservice**. 

Hallo hieronder vindt u de eerste experiment Hallo.
   
   ![Eerste experiment.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Een Voorspellend experiment maken en publiceren als een webservice
Vervolgens maakt u een Experiment Predicative.

1. Hallo onder aan het experimentcanvas hello, klikt u op **webservice ingesteld** en selecteer **voorspellende webservice**. Hallo model opgeslagen als een getraind Model en web service invoer en uitvoer modules worden toegevoegd. 
2. Klik op **Run**. 
3. Nadat het Hallo-experiment is voltooid, klikt u op **webservice implementeren [klassieke]** of **Web Service implementeren [New]**.

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Hallo trainingsexperiment implementeren als een webservice Training
tooretrain hello getrainde model, moet u Hallo trainingsexperiment die u hebt gemaakt als een webservice Retraining implementeren. Deze webservice moet een *Web Service uitvoer* module verbonden toohello  *[Train Model] [ train-model]*  module, toobe kunnen tooproduce nieuwe modellen zijn opgeleid.

1. tooreturn toohello trainingsexperiment Hallo experimenten pictogram in het linkerdeelvenster hello, klik op Hallo experiment telling Model met de naam.  
2. Typ in Experiment zoekitems zoekvak Hallo-webservice. 
3. Sleep een *Web Service invoer* module op Hallo canvas experimenteren en verbinding maken met de uitvoer toohello *Clean Missing Data* module.  Dit zorgt ervoor dat uw retraining gegevens worden verwerkt Hallo op dezelfde manier als uw oorspronkelijke trainingsgegevens.
4. Sleep twee *webservice uitvoer* modules op Hallo experimenteren canvas. Verbinding maken met uitvoer Hallo Hallo *Train Model* module tooone Hallo uitvoer en Hallo *Evaluate Model* module toohello andere. Hallo web service uitvoer voor **Train Model** biedt ons Hallo nieuwe getrainde model. Hallo uitvoer te gekoppeld**Evaluate Model** retourneert die module-uitvoer, namelijk Hallo prestatieresultaten.
5. Klik op **Run**. 

Vervolgens moet u Hallo trainingsexperiment implementeren als een webservice die een getraind model en de resultaten van evaluatie van model produceert. tooaccomplish dit de volgende reeks acties zijn afhankelijk van of u werkt met een webservice klassieke of een nieuwe webservice.  

**Klassieke webservice**

Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **webservice implementeren [klassieke]**. Hallo-webservice **Dashboard** voor Batchuitvoering met Hallo API-sleutel en Hallo API help-pagina wordt weergegeven. Alleen Hallo Batchuitvoering methode kan worden gebruikt voor het maken van de Trained Models.

**Nieuwe webservice**

Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **Web Service implementeren [New]**. Web Service Azure Machine Learning-webservices Hello wordt toohello implementeren service webpagina geopend. Typ een naam voor uw web-service en kies een betaald abonnement en klik vervolgens op **implementeren**. Alleen Hallo Batchuitvoering methode kan worden gebruikt voor het maken van de Trained Models

In beide gevallen nadat experiment voltooide uitgevoerd heeft ziet Hallo resulterende werkstroom er als volgt:

![Resulterende workflow nadat uitgevoerd.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Hallo-model met nieuwe gegevens met behulp van BES Retrain
Bijvoorbeeld, u toocreate Hallo C# retraining toepassing gebruikt. U kunt ook gebruiken Hallo Python of R voorbeeld code tooaccomplish deze taak.

toocall hello Retraining API's:

1. Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.
2. Meld u aan toohello Machine Learning-webservice-portal.
3. Als u met een klassiek-webservice werkt, klikt u op **klassieke webservices**.
   1. Klik op Hallo met werken web-service.
   2. Klik op het standaardeindpunt Hallo.
   3. Klik op **verbruiken**.
   4. Hallo Hallo onderaan in **verbruiken** pagina in Hallo **voorbeeldcode** sectie, klikt u op **Batch**.
   5. Toostep 5 van deze procedure blijven.
4. Als u met een nieuwe webservice werkt, klikt u op **webservices**.
   1. Klik op Hallo met werken web-service.
   2. Klik op **verbruiken**.
   3. Hallo Hallo verbruiken pagina in Hallo onderaan in **voorbeeldcode** sectie, klikt u op **Batch**.
5. Hallo C# voorbeeldcode voor Batchuitvoering Kopieer en plak deze in het bestand Program.cs hello om ervoor te zorgen Hallo naamruimte blijft intact.

Hallo Nuget-pakket Microsoft.AspNet.WebApi.Client zoals opgegeven in Hallo opmerkingen toevoegen. tooadd hello verwijzing tooMicrosoft.WindowsAzure.Storage.dll mogelijk moet u eerst tooinstall Hallo-clientbibliotheek voor Microsoft Azure storage-services. Zie voor meer informatie [Windows Storage-Services](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Hallo apikey declaratie bijwerken
Zoek Hallo **apikey** declaratie.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

In Hallo **Basic verbruik info** sectie Hallo **verbruiken** pagina, Ga naar de primaire sleutel Hallo en kopieer het toohello **apikey** declaratie.

### <a name="update-hello-azure-storage-information"></a>Hello Azure Storage-gegevens bijwerken
Hallo BES voorbeeldcode uploadt een bestand van een lokale schijf (bijvoorbeeld 'C:\temp\CensusIpnput.csv') tooAzure opslag, verwerkt en schrijft Hallo resultaten back tooAzure opslag.  

tooaccomplish deze taak moet u Hallo Storage account name, -sleutel en container-gegevens ophalen voor uw opslagaccount van Hallo klassieke Azure-portal en bijbehorende waarden in de code Hallo Hallo-update. 

1. Meld u aan toohello klassieke Azure-portal.
2. Klik in Hallo linkernavigatievenster kolom op **opslag**.
3. Selecteer één toostore hello retrained vanuit Hallo lijst met opslagaccounts, model.
4. Klik onder aan de pagina Hallo Hallo op **toegangssleutels beheren**.
5. Kopiëren en opslaan van Hallo **primaire toegangssleutel** en sluiten Hallo dialoogvenster. 
6. Bovenaan Hallo Hallo pagina, klikt u op **Containers**.
7. Selecteer een bestaande container of maak een nieuwe en Hallo naam worden opgeslagen.

Zoek Hallo *StorageAccountName*, *StorageAccountKey*, en *StorageContainerName* declaraties en update Hallo waarden die u hebt genoteerd in hello Azure-portal.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Ook moet u ervoor zorgen Hallo-bestand voor invoer is beschikbaar op Hallo-locatie die u in het Hallo-code opgeeft. 

### <a name="specify-hello-output-location"></a>Hallo uitvoerlocatie opgeven
Bij het Hallo-uitvoerlocatie opgeven in Hallo Request-nettolading, uitbreiding van Hallo dat is opgegeven in Hallo *RelativeLocation* moet worden opgegeven als ilearner. 

Zie Hallo voorbeeld te volgen:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> Hallo-namen van de uitvoerlocaties afwijken van Hallo uitzonderingen in deze stapsgewijze kennismaking op basis van Hallo volgorde waarin u Hallo web service uitvoer modules hebt toegevoegd. Omdat u dit trainingsexperiment met twee uitvoer hebt ingesteld, opnemen Hallo resultaten locatiegegevens van opslag voor beide parameters.  
> 
> 

![Uitvoer retraining][6]

Diagram 4: Retraining uitvoer.

## <a name="evaluate-hello-retraining-results"></a>Hallo Retraining resultaten evalueren
Wanneer u de toepassing hello uitvoert, Hallo uitvoer bevat de URL van de Hallo en SAS-token nodig tooaccess Hallo resultaten van evaluatie.

Ziet u prestatieresultaten Hallo van Hallo retrained model door een combinatie van Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten voor *output2* (zoals weergegeven in de voorgaande afbeelding uitvoer retraining Hallo) en Hallo volledige URL in de adresbalk van Hallo browser te plakken.  

Hallo resultaten toodetermine onderzoeken of Hallo zojuist getraind model functioneert goed genoeg tooreplace Hallo een bestaande.

Kopiëren Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* van resultaten van de uitvoer hello, wordt u ze gebruiken tijdens Hallo retraining proces.

## <a name="next-steps"></a>Volgende stappen
Als u voorspellende Hallo-webservice geïmplementeerd door te klikken op **webservice implementeren [klassieke]**, Zie [opnieuw trainen van een webservice klassieke](machine-learning-retrain-a-classic-web-service.md).

Als u voorspellende Hallo-webservice geïmplementeerd door te klikken op **Web Service implementeren [New]**, Zie [opnieuw trainen Hallo Machine Learning Management cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
