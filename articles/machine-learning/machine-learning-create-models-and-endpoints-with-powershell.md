---
title: aaaCreate meerdere modellen van een experiment | Microsoft Docs
description: Gebruik PowerShell toocreate meerdere Machine Learning-modellen en web service-eindpunten met Hallo dezelfde algoritme maar verschillende training gegevenssets.
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Veel Machine Learning-modellen en webservice-eindpunten maken van een experiment met PowerShell
Hier volgt een veelvoorkomend probleem van machine learning: gewenste toocreate veel modellen die Hallo hebben dezelfde werkstroom training en gebruik dezelfde algoritme hello, maar hebben verschillende training gegevenssets als invoer. Dit artikel ziet u hoe toodo dit op grote schaal in Azure Machine Learning Studio met behulp van slechts een enkele experiment.

Stel dat u een globale fiets verhuur franchiseonderneming bedrijf bezit. Wilt u toobuild regressie model toopredict Hallo verhuur vraag op basis van historische gegevens. U 1000 verhuur locaties via Hallo wereld hebt en u hebt een gegevensset voor elke locatie met belangrijke functies zoals datum, tijd, weer en verkeer dat specifieke tooeach locatie worden verzameld.

U kunt het model met één keer een samengevoegde versie van alle Hallo gegevenssets op alle locaties kan trainen. Maar omdat elk van de locaties van een unieke omgeving heeft, een betere benadering zou worden tootrain uw regressiemodel met afzonderlijk Hallo gegevensset voor elke locatie. Op die manier elk getraind model kon worden in de grootte van de andere archieven Hallo account, volume, Geografie, populatie, fiets-vriendelijk verkeer-omgeving, *enzovoort*.

Die mogelijk de beste aanpak hello, maar u niet wilt dat toocreate 1.000 training experimenten in Azure Machine Learning met elkaar die een unieke locatie voorstelt. Behalve dat een enigszins overweldigend taak, het is ook heel inefficiënt lijkt omdat elk experiment alle dezelfde onderdelen, met uitzondering van Hallo training gegevensset Hallo zou hebben.

Gelukkig we dit kunt doen met behulp van Hallo [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) en automatiseren Hallo-taak met [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake ons voorbeeld sneller worden uitgevoerd, verlagen we het aantal locaties van 1000 too10 Hallo. Maar hello dezelfde beginselen en procedures toepassen too1, 000 locaties. Hallo enige verschil is dat als u wilt dat tootrain van 1000 gegevenssets u waarschijnlijk toothink wilt van het uitvoeren van de volgende PowerShell-scripts parallel Hallo. Hoe toodo die valt buiten bereik Hallo van dit artikel, maar u kunt vinden voorbeelden van PowerShell multithreading op Hallo Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Hallo trainingsexperiment instellen
We gaan een voorbeeld toouse [trainingsexperiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) die we al hebt gemaakt in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Open dit experiment in uw [Azure Machine Learning Studio](https://studio.azureml.net) werkruimte.

> [!NOTE]
> In de volgorde toofollow samen met het volgende voorbeeld kunt u toouse een standard-werkruimte in plaats van een gratis werkruimte. We één eindpunt maakt voor elke klant - voor een totaal van 10 eindpunten - en waarvoor u een standaard werkruimte omdat een gratis werkruimte beperkt too3 eindpunten is. Als u alleen een gratis werkruimte hebt, net Hallo scripts hieronder tooallow voor slechts 3 locaties te wijzigen.
> 
> 

Hallo-experiment wordt gebruikgemaakt van een **importgegevens** module tooimport Hallo training gegevensset *customer001.csv* van een Azure storage-account. Stel hebben we training gegevenssets van alle fiets verhuur locaties verzameld en opgeslagen in dezelfde locatie voor de opslag-blob met bestandsnamen, variërend van Hallo *rentalloc001.csv* te*rentalloc10.csv* .

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Houd er rekening mee dat een **Web Service uitvoer** module is toegevoegd toohello **Train Model** module.
Wanneer dit experiment wordt geïmplementeerd als een webservice, retourneren die zijn gekoppeld aan die uitvoer Hallo-eindpunt Hallo getrainde model in Hallo-indeling van een bestand .ilearner.

Let ook op dat u een web service-parameter voor Hallo-URL die Hallo stelt **importgegevens** module wordt gebruikt. Deze manier kunnen wij toouse Hallo parameter toospecify individuele training gegevenssets tootrain Hallo model voor elke locatie.
Er zijn andere manieren we kunnen dit hebt gedaan, zoals met behulp van een SQL-query met een web service parameter tooget gegevens uit een Azure SQL database of te gebruiken om een **Web Service invoer** module toopass in een gegevensset toohello-webservice.

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Nu gaan we deze trainingsexperiment met de standaardwaarde Hallo uitvoeren *rental001.csv* zoals Hallo training gegevensset. Als u hello uitvoer Hallo bekijkt **Evaluate** module (Hallo uitvoer op en selecteer **Visualize**), kunt u zien krijgen we een goede prestaties van *AUC* = 0.91. Op dit moment we klaar toodeploy een webservice buiten dit trainingsexperiment.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Hallo training en score berekenen voor webservices implementeren
Hallo toodeploy training webservice, klikt u op Hallo **webservice ingesteld** onder het experimentcanvas hello en selecteer **webservice implementeren**. Roep deze webservice '' fiets verhuur Training'.

Er moet nu toodeploy Hallo score-webservice.
toodo, we kunt klikken op **webservice ingesteld** hieronder Hallo canvas en selecteer **voorspellende webservice**. Hiermee maakt u een score experiment.
Er moet een paar kleine aanpassingen toomake deze werken als een webservice, zoals het Hallo labelkolom 'cnt' verwijderen uit de Hallo invoergegevens en beperken Hallo uitvoer tooonly Hallo exemplaar-id en de bijbehorende van Hallo voorspelde waarde toomake.

toosave zelf die werken, kunt u eenvoudig hello openen [Voorspellend experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in Hallo galerie die al is voorbereid.

Klik vervolgens op Hallo toodeploy Hallo-webservice, Hallo Voorspellend experiment uitvoeren **webservice implementeren** knop onder Hallo canvas. Naam Hallo score berekenen voor webservice 'Fiets verhuur score berekenen' '.

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>10 identiek webservice-eindpunten maken met PowerShell
Deze webservice wordt geleverd met een standaardeindpunt. Maar dit is nog niet belangstelling Hallo standaardeindpunt omdat deze niet worden bijgewerkt. Wat er moet toodo is toocreate 10 extra eindpunten, één voor elke locatie. We doen dit met PowerShell.

Eerst we onze PowerShell-omgeving hebt ingesteld:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Voer Hallo volgende PowerShell-opdracht:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Nu er 10 eindpunten is gemaakt en ze allemaal dezelfde getrainde model wordt getraind op Hallo bevatten *customer001.csv*. U kunt ze weergeven in hello Azure Management Portal.

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Hallo eindpunten toouse twee afzonderlijke trainings gegevenssets met behulp van PowerShell bijwerken
de volgende stap Hallo is tooupdate Hallo eindpunten met een unieke getraind voor elke afzonderlijke klantgegevens modellen. Maar eerst moet u tooproduce deze modellen van Hallo **fiets verhuur Training** webservice. Daarvoor gaat u terug toohello **fiets verhuur Training** webservice. Toocall moet het eindpunt BES 10 keer met 10 andere training gegevenssets in volgorde tooproduce 10 verschillende modellen. We gebruiken Hallo **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo dit.

U moet ook tooprovide referenties voor blob storage-account in `$configContent`, dat wil zeggen op Hallo velden `AccountName`, `AccountKey` en `RelativeLocation`. Hallo `AccountName` kan bestaan uit een van de accountnamen van uw, zoals in Hallo **klassieke Azure-beheerportal** (*opslag* tabblad). Nadat u op een opslagaccount op de `AccountKey` vindt u door te drukken Hallo **toegangssleutels beheren** knop op Hallo onder en kopiëren Hallo *primaire toegangssleutel*. Hallo `RelativeLocation` Hallo pad relatief tooyour opslag is waarin u een nieuw model wordt opgeslagen. Bijvoorbeeld: Hallo pad `hai/retrain/bike_rental/` in de volgende punten tooa container met de naam Hallo script `hai`, en `/retrain/bike_rental/` zijn submappen. Op dit moment kunt u geen submappen via de gebruikersinterface voor het Hallo-portal maken, maar er zijn [verschillende Azure Storage Explorers](../storage/common/storage-explorers.md) waarmee u toodo dus. Het wordt aanbevolen dat u een nieuwe container maken in uw opslag toostore Hallo nieuwe getraind modellen (.ilearner-bestanden) als volgt: van uw opslagpagina, klikt u op Hallo **toevoegen** knop Hallo onderin en noem deze `retrain`. Kortom, onderstaande Hallo noodzakelijke wijzigingen toohello-script te horen`AccountName`, `AccountKey` en `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> Hallo BES-eindpunt is modus Hallo alleen ondersteund voor deze bewerking. RRS kan niet worden gebruikt voor het produceren van getraind modellen.
> 
> 

Zoals u ziet, in plaats van 10 andere BES taak json configuratiebestanden, maken we dynamisch Hallo configuratietekenreeks in plaats daarvan maakt en voer deze toohello *jobConfigString* parameter Hallo  **InvokeAmlWebServceBESEndpoint** cmdlet, omdat er een kopie echt geen tookeep nodig op schijf is.

Als alles goed gaat, na enige tijd ziet u 10 .ilearner bestanden van *model001.ilearner* te*model010.ilearner*, in uw Azure storage-account. Nu we klaar tooupdate onze 10 score berekenen voor web service-eindpunten met deze modellen met Hallo **Patch AmlWebServiceEndpoint** PowerShell-cmdlet. Vergeet niet opnieuw kunt dat we alleen patch Hallo niet-standaard eindpunten die we programmatisch eerder hebt gemaakt.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

Dit moet vrij snel uitgevoerd. Wanneer het Hallo-uitvoering is voltooid, hebt we hebt gemaakt 10 voorspellende webservice-eindpunten, elk met een unieke op Hallo gegevensset specifieke tooa verhuur locatie, via een trainingsexperiment één getraind model is getraind. tooverify, kunt u proberen het aanroepen van deze eindpunten met Hallo **InvokeAmlWebServiceRRSEndpoint** cmdlet meeleveren Hello dezelfde gegevens en u kunt verwachten toosee verschillende voorspelling resultaten aangezien Hallo modellen zijn getraind met verschillende training sets.

## <a name="full-powershell-script"></a>Volledige PowerShell-script
Hallo-overzicht van de volledige broncode Hallo Ga als volgt:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
