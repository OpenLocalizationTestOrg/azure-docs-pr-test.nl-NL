---
title: aaaAzure Stream Analytics en Machine Learning-integratie | Microsoft Docs
description: Hoe toouse een gebruiker gedefinieerde functie en Machine Learning in een Stream Analytics-taak
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Gevoel analyse uitvoeren met behulp van Azure Stream Analytics en Azure Machine Learning
Dit artikel wordt beschreven hoe een eenvoudige Azure Stream Analytics-taak die Azure Machine Learning integreert tooquickly ingesteld. U gebruikt een Machine Learning gevoel analytics-model uit Hallo Cortana Intelligence Gallery tooanalyze streaming tekstgegevens en Hallo gevoel score in realtime te bepalen. Hallo Cortana Intelligence Suite kunt u deze taak uitvoeren zonder dat u Hallo gecompliceerde aspecten van het bouwen van een gevoel analytics-model.

U kunt toepassen wat u leert van dit artikel tooscenarios zoals deze:

* Analyse van realtime gevoel op Twitter gegevensstromen.
* Records van de klant analyseren chats met het ondersteunend personeel.
* Evalueren van opmerkingen over forums, blogs en video's. 
* Veel andere realtime, voorspellende scoreprofiel scenario's.

In een Praktijkscenario krijgt u rechtstreeks vanuit een gegevensstroom Twitter Hallo-gegevens. toosimplify hello zelfstudie we hebt geschreven zodat hello Streaming Analytics-taak opgehaald tweets uit een CSV-bestand in Azure Blob-opslag. U kunt uw eigen CSV-bestand maken of u kunt een CSV-voorbeeldbestand, zoals wordt weergegeven in Hallo installatiekopie te volgen:

![voorbeeld tweets in een CSV-bestand](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

Hallo Streaming Analytics-taak die u maakt is van toepassing hello gevoel analytics-model als een gebruiker gedefinieerde functie (UDF) op de voorbeeldgegevens tekst hello van Hallo bloblarchief. Hallo-uitvoer (Hallo resultaat van Hallo gevoel analyse) geschreven toohello dezelfde blob-opslag in een ander CSV-bestand. 

Hallo volgende afbeelding ziet u deze configuratie. Zoals aangegeven voor een meer realistische scenario kunt u de blob-opslag met Twitter-gegevens uit Azure Event Hubs invoer streaming vervangen. Bovendien kan u samenstellen een [Microsoft Power BI](https://powerbi.microsoft.com/) realtime visualisatie van cumulatieve gevoel Hallo.    

![Overzicht van stream Analytics Machine Learning-integratie](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Vereisten
Zorg voordat u begint, hebt u de volgende Hallo:

* Een actief Azure-abonnement.
* Een CSV-bestand met sommige gegevens in het. U kunt eerder weergegeven uit Hallo-bestand downloaden [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), of u kunt uw eigen bestand maken. Voor dit artikel nemen we aan dat u Hallo bestand vanuit GitHub.

Op een hoog niveau toocomplete Hallo taken in dit artikel wordt uitgelegd u Hallo te volgen:

1. Een Azure storage-account en een blob storage-container maken en uploaden van een CSV-indeling invoerbestand toohello-container.
3. Een gevoel analytics-model van Hallo Cortana Intelligence Gallery tooyour Azure Machine Learning-werkruimte toevoegen en dit model implementeren als een webservice in Hallo Machine Learning-werkruimte.
5. Een Stream Analytics-taak die deze webservice als een functie in volgorde toodetermine gevoel voor tekstinvoer Hallo aanroepen maken.
6. Hallo Stream Analytics-taak starten en controleer Hallo uitvoer.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Een opslagcontainer maken en uploaden Hallo CSV-bestand voor invoer
Voor deze stap kunt u een CSV-bestand, zoals Hallo een beschikbaar is via GitHub.

1. Klik in hello Azure-portal, op **nieuw** &gt; **opslag** &gt; **opslagaccount**.

   ![Nieuw opslagaccount maken](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Geef een naam (`samldemo` in Hallo voorbeeld). Hallo-naam kan gebruiken die alleen kleine letters en cijfers en deze uniek zijn binnen Azure. 

3. Geef een bestaande resourcegroep en locatie opgeven. Locatie voor het is raadzaam alle Hallo resources die zijn gemaakt in deze zelfstudie gebruik Hallo dezelfde locatie.

    ![Geef details op storage-account](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Selecteer in hello Azure-portal, Hallo storage-account. Klik in de blade opslagaccount hello **Containers** en klik vervolgens op  **+ &nbsp;Container** toocreate blob-opslag.

    ![blob-container maken](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Geef een naam voor het Hallo-container (`azuresamldemoblob` in Hallo voorbeeld) en controleer of **toegangstype** te is ingesteld**Blob**. Wanneer u klaar bent, klikt u op **OK**.

    ![Geef details van blob-container](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. In Hallo **Containers** blade, selecteer Hallo nieuwe container, Hallo blade voor die container te openen.

7. Klik op **Uploaden**.

    ![Knop voor een container uploaden](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. In Hallo **blob uploaden** blade Hallo CSV-bestand dat u voor deze zelfstudie toouse wilt opgeven. Voor **type Blob**, selecteer **blok-blob** en set Hallo blok grootte too4 MB, hetgeen voldoende is voor deze zelfstudie.

    ![blob-bestand uploaden](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Klik op Hallo **uploaden** knop Hallo Hallo blade onderaan in.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Hallo gevoel analytics-model van Hallo Cortana Intelligence Gallery toevoegen

Nu dat Hallo voorbeeldgegevens in een blob, kunt u Hallo gevoel Analytics-model in de Cortana Intelligence Gallery inschakelen.

1. Ga toohello [gevoel predictive analytics-model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) pagina in Cortana Intelligence Gallery Hallo.  

2. Klik op **openen in Studio**.  
   
   ![Stream Analytics Machine Learning, open Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Meld u aan toogo toohello werkruimte. Selecteer een locatie.

4. Klik op **uitvoeren** Hallo Hallo pagina onderaan in. Hallo-proces wordt uitgevoerd, wat duurt ongeveer een minuut.

   ![Voer experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Nadat het Hallo-proces met succes is uitgevoerd, selecteert u **webservice implementeren** Hallo Hallo pagina onderaan in.

   ![experiment in Machine Learning Studio implementeren als een webservice](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate die Hallo gevoel analytics-model is gereed toouse, klikt u op Hallo **Test** knop. Tekst invoeren, zoals 'Ik hou Microsoft' opgeven. 

   ![Test-experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Als de test Hallo werkt, ziet u een resultaat vergelijkbaar toohello voorbeeld te volgen:

   ![testresultaten in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. In Hallo **Apps** kolom, klikt u op Hallo **Excel 2010 of ouder werkmap** koppeling toodownload een Excel-werkmap. Hallo-werkmap bevat Hallo een API-sleutel en Hallo-URL moet u later tooset up Hallo Stream Analytics-taak.

    ![Stream Analytics, Machine Learning, snelle weergave](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Maken van een Stream Analytics-taak die gebruikmaakt van Hallo Machine Learning-model

U kunt nu een Stream Analytics-taak die Hallo voorbeeld tweets uit Hallo CSV-bestand in blob-opslag leest maken. 

### <a name="create-hello-job"></a>Hallo-taak maken

1. Ga toohello [Azure-portal](https://portal.azure.com).  

2. Klik op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**. 

   ![Azure portal pad voor het ophalen van tooa nieuwe Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Naam Hallo taak `azure-sa-ml-demo`, Geef een abonnement op, Geef een bestaande resourcegroep of maak een nieuwe en selecteer de locatie Hallo voor Hallo-taak.

   ![instellingen opgeven voor nieuwe Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Hallo taak invoer configureren
de invoer Hallo taak opgehaald uit Hallo CSV-bestand dat u eerder tooblob opslag geüpload.

1. Nadat het Hallo-taak is gemaakt, klikt u onder **taak topologie** Klik Hallo Hallo taakblade **invoer** vak.  
   
   ![Het selectievakje 'Invoer' in de blade voor Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. In Hallo **invoer** blade, klikt u op **+ toevoegen**.

   ![Knop voor het toevoegen van een invoer toohello Stream Analytics-taak toevoegen](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Hallo invullen **nieuwe invoer** blade met deze waarden:

    * **Invoeralias**: Gebruik de naam van Hallo `datainput`.
    * **Gegevensbrontype**: Selecteer **gegevensstroom**.
    * **Bron**: Selecteer **Blob storage**.
    * **Optie importeren**: Selecteer **gebruik blob storage uit het huidige abonnement**. 
    * **Storage-account**. Selecteer Hallo-opslagaccount die u eerder hebt gemaakt.
    * **Container**. Selecteer Hallo-container die u eerder hebt gemaakt (`azuresamldemoblob`).
    * **Gebeurtenis serialisatie-indeling**. Selecteer **CSV**.

    ![Instellingen voor nieuwe taak invoer](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Klik op **Create**.

### <a name="configure-hello-job-output"></a>Hallo taakuitvoer configureren
Hallo taak verzendt resultaten toohello dezelfde blobopslag waar deze invoer opgehaald. 

1. Onder **taak topologie** Klik Hallo Hallo taakblade **uitvoer** vak.  
  
   ![Nieuwe uitvoer voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. In Hallo **uitvoer** blade, klikt u op **+ toevoegen**, en voeg vervolgens een uitvoer met de Hallo alias `datamloutput`. 

3. Voor **Sink**, selecteer **Blob storage**. Vult Hallo rest Hallo uitvoer instellingen met behulp van dezelfde waarden die u hebt gebruikt voor blob-opslag voor invoer Hallo Hallo:

    * **Storage-account**. Selecteer Hallo-opslagaccount die u eerder hebt gemaakt.
    * **Container**. Selecteer Hallo-container die u eerder hebt gemaakt (`azuresamldemoblob`).
    * **Gebeurtenis serialisatie-indeling**. Selecteer **CSV**.

   ![Instellingen voor nieuwe taakuitvoer](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Klik op **Create**.   


### <a name="add-hello-machine-learning-function"></a>Hallo Machine Learning-functie toevoegen 
U hebt gepubliceerd eerder een Machine Learning-model tooa-webservice. In ons scenario wanneer Hallo stroom Analysis taak wordt uitgevoerd, stuurt elke tweet voorbeeld van Hallo invoer toohello webservice voor gevoel analyse. Hallo Machine Learning-webservice retourneert een gevoel (`positive`, `neutral`, of `negative`) en de kans op Hallo tweet wordt positief. 

In deze sectie van de zelfstudie hello, moet u een functie in Hallo stroom Analysis taak definiëren. Hallo-functie kan worden aangeroepen toosend een tweet toohello-webservice en terughalen antwoord Hallo. 

1. Zorg ervoor dat u hebt Hallo web service-URL en API-sleutel die u eerder in de Excel-werkmap Hallo gedownload.

2. Overzichtsblade van toohello taak retourneren.

3. Onder **instellingen**, selecteer **functies** en klik vervolgens op **+ toevoegen**.

   ![Een functie toohello Stream Analytics-taak niet toevoegen](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Voer `sentiment` functioneren alias als Hallo en geef overige Hallo Hallo-blade met deze waarden:

    * **Type functie**: Selecteer **Azure ML**.
    * **Optie importeren**: Selecteer **importeren uit een ander abonnement**. Hiermee krijgt u een kans tooenter Hallo-URL en de sleutel.
    * **URL**: plakken in Hallo webservice-URL.
    * **Sleutel**: plakken in Hallo API-sleutel.
  
    ![Instellingen voor het toevoegen van een Machine Learning functie toohello Stream Analytics-taak](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Klik op **Create**.

### <a name="create-a-query-tootransform-hello-data"></a>Maken van een query tootransform Hallo-gegevens

Stream Analytics maakt gebruik van een declaratieve, op basis van SQL-query tooexamine Hallo-invoer en verwerkt. In deze sectie maakt maken u een query waarmee elke tweet uit invoer gelezen en roept vervolgens Hallo Machine Learning functie tooperform gevoel analysis. Hallo-query verzendt vervolgens Hallo resultaat toohello uitvoer die u hebt gedefinieerd (blobopslag).

1. Overzichtsblade van toohello taak retourneren.

2.  Onder **taak topologie**, klikt u op Hallo **Query** vak.

    ![Een query voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Voer Hallo query te volgen:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    Hallo query roept Hallo-functie die u eerder hebt gemaakt (`sentiment`) in volgorde tooperform gevoel analyse op elke tweet in Hallo-invoer. 

4. Klik op **opslaan** toosave Hallo query.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Hallo Stream Analytics-taak starten en controleer Hallo-uitvoer

U kunt nu Hallo Stream Analytics-taak starten.

### <a name="start-hello-job"></a>Hallo taak starten
1. Overzichtsblade van toohello taak retourneren.

2. Klik op **Start** Hallo boven aan het Hallo-blade.

    ![Een query voor Streaming Analytics-taak maken](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. In Hallo **starttaak**, selecteer **aangepaste**, en selecteer vervolgens een dag van de voorafgaande toowhen Hallo CSV-bestand tooblob opslag die u hebt geüpload. Wanneer u bent klaar, klikt u op **Start**.  


### <a name="check-hello-output"></a>Hallo uitvoer controleren
1. Laat Hallo taak uitvoeren voor een paar minuten totdat er activiteit in Hallo **bewaking** vak. 

2. Als u een hulpprogramma hebt dat u gewoonlijk tooexamine Hallo inhoud van de blob-opslag gebruikt, gebruiken die hulpprogramma tooexamine hello `azuresamldemoblob` container. U kunt ook Hallo stappen te volgen in hello Azure-portal:

    1. In de portal Hallo Hallo zoeken `samldemo` storage account en Hallo binnen Hallo-account zoeken `azuresamldemoblob` container. Ziet u twee bestanden in de container Hallo: Hallo bestand Hallo voorbeeld tweets met en een CSV-bestand dat is gegenereerd door Hallo Stream Analytics-taak.
    2. Hallo gegenereerd bestand met de rechtermuisknop en selecteer vervolgens **downloaden**. 

   ![CSV-taakuitvoer downloaden uit Blob-opslag](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Open Hallo gegenereerd CSV-bestand. U ziet ongeveer Hallo voorbeeld te volgen:  
   
   ![Stream Analytics, Machine Learning, CSV weergeven](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Metrische gegevens weergeven
U kunt ook Azure Machine Learning functie-gerelateerde metrische gegevens weergeven. Hallo volgende functie-gerelateerde metrische gegevens worden weergegeven in Hallo **bewaking** vak in de blade taak Hallo:

* **Functie aanvragen** geeft het aantal aanvragen dat is verzonden tooa Machine Learning-webservice Hallo.  
* **Gebeurtenissen werken** geeft het aantal gebeurtenissen in de aanvraag Hallo Hallo. Standaard bevat elke aanvraag tooa Machine Learning-webservice up too1, 000 gebeurtenissen.  


## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST-API integreren en Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)



