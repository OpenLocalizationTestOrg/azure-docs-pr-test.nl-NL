---
title: aaaUsing Import/Export-gegevens in Azure Machine Learning-webservices | Microsoft Docs
description: Ontdek hoe toouse Hallo modules toosend voor gegevens importeren en exporteren van gegevens en gegevens ontvangen van een webservice.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Azure ML-webservices implementeren die gebruikmaken van gegevensimport- en gegevensexportmodules

Wanneer u een Voorspellend experiment maakt, voegt u gewoonlijk toe een web service invoer en uitvoer. Wanneer u een experiment Hallo implementeert, kunnen consumenten verzenden en ontvangen van gegevens van de webservice Hallo via Hallo invoer en uitvoer. Voor sommige toepassingen van de consumer gegevens uit een gegevensfeed beschikbaar of al bevinden zich in een externe gegevensbron zoals Azure Blob-opslag. In dergelijke gevallen hoeven ze niet lezen en schrijven van gegevens met behulp van web service in- en uitgangen. Ze kunnen in plaats daarvan Hallo Batch uitvoering Service (BES) tooread gegevens uit het Hallo-gegevensbron met behulp van een module gegevens importeren gebruiken en schrijf Hallo score berekenen voor resultaten andere gegevenslocatie tooa met behulp van een module gegevens exporteren.

Hallo kunnen gegevens importeren en exporteren gegevens modules, lezen uit en schrijven toovarious gegevens locaties zoals een via HTTP, een Hive-Query, een Azure SQL-database, Azure Table storage, Azure Blob storage, een Gegevensfeed-URL opgeven of een lokale SQL-database.

In dit onderwerp maakt gebruik van Hallo ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' steekproef en wordt ervan uitgegaan dat Hallo dataset al is geladen in een Azure SQL-tabel met de naam censusdata.

## <a name="create-hello-training-experiment"></a>Hallo trainingsexperiment maken
Wanneer u opent Hallo ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' voorbeeld van gebruikt Hallo voorbeeldgegevensset volwassenen inventarisering Income binaire classificatie. En Hallo experiment in Hallo canvas eruit vergelijkbare toohello installatiekopie te volgen:

![De aanvankelijke configuratie van Hallo experiment.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

tooread hello gegevens uit hello Azure SQL-tabel:

1. Hallo gegevensset module verwijderen.
2. Typ in Hallo-onderdelen in het zoekvak importeren.
3. Lijst met resultaten Hallo toevoegen een *importgegevens* module toohello experimenteren canvas.
4. Verbinding maken met de uitvoer van Hallo *importgegevens* module-invoer Hallo Hallo *Clean Missing Data* module.
5. Selecteer in het eigenschappendeelvenster **Azure SQL Database** in Hallo **gegevensbron** vervolgkeuzelijst.
6. In Hallo **databaseservernaam**, **databasenaam**, **gebruikersnaam**, en **wachtwoord** velden, voer de juiste gegevens Hallo voor uw database.
7. Voer in query-databaseveld met Hallo Hallo volgende query.
   
     Selecteer [leeftijd]
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     van dbo.censusdata;
8. Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.

## <a name="create-hello-predictive-experiment"></a>Hallo Voorspellend experiment maken
De volgende instellen van Hallo Voorspellend experiment van waaruit u uw webservice implementeert.

1. Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **voorspellende Web Service (aanbevolen)**.
2. Hallo verwijderen *Web Service invoer* en *Web Service uitvoer modules* van Hallo Voorspellend experiment. 
3. Typ in Hallo-onderdelen in het zoekvak exporteren.
4. Lijst met resultaten Hallo toevoegen een *gegevens exporteren* module toohello experimenteren canvas.
5. Verbinding maken met de uitvoer van Hallo *Score Model* module-invoer Hallo Hallo *gegevens exporteren* module. 
6. Selecteer in het eigenschappendeelvenster **Azure SQL Database** Hallo gegevens bestemming vervolgkeuzelijst.
7. In Hallo **databaseservernaam**, **databasenaam**, **Server gebruikersaccountnaam**, en **Server het wachtwoord voor gebruikersaccount** velden invoeren Hallo relevante informatie voor uw database.
8. In Hallo **met door komma's gescheiden lijst met kolommen toobe opgeslagen** veld, typt u Scored Labels.
9. In Hallo **gegevensveld tabel naam**, typt u dbo. ScoredLabels. Als Hallo tabel niet bestaat, wordt deze gemaakt wanneer Hallo experiment wordt uitgevoerd of Hallo-webservice wordt aangeroepen.
10. In Hallo **door komma's gescheiden lijst met kolommen datatable** veld ScoredLabels.

Wanneer u een toepassing schrijft dat aanroepen laatste webservice hello, kunt u toospecify een andere query- of doelserver invoertabel tijdens runtime. tooconfigure deze invoer en uitvoer, gebruik Hallo Webserviceparameters functie tooset hello *importgegevens* module *gegevensbron* eigenschap en Hallo *gegevens exporteren* modus de eigenschap destination gegevens.  Zie voor meer informatie over Webserviceparameters hello [Webserviceparameters AzureML-vermelding](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) op Hallo Cortana Intelligence en Machine Learning-Blog.

tooconfigure hello Webserviceparameters voor Hallo importeren query en doeltabel Hallo:

1. In het eigenschappendeelvenster Hallo voor Hallo *gegevens importeren* -module, klik op Hallo Hallo pictogram rechts van Hallo top **databasequery** veld en selecteert u **instellen als web Serviceparameter**.
2. In het eigenschappendeelvenster Hallo voor Hallo *gegevens exporteren* -module, klik op Hallo Hallo pictogram rechts van Hallo top **gegevens tabelnaam** veld en selecteert u **instellen als web service**.
3. Hallo Hallo onderaan in *gegevens exporteren* eigenschappendeelvenster van de module in Hallo **Webserviceparameters** sectie, klikt u op databasequery en wijzig deze met een Query.
4. Klik op **gegevens tabelnaam** en wijzig de naam **tabel**.

Wanneer u klaar bent, ziet uw experiment vergelijkbare toohello installatiekopie te volgen:

![Laatste uiterlijk van experiment.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

U kunt nu Hallo experiment implementeren als een webservice.

## <a name="deploy-hello-web-service"></a>Hallo-webservice implementeren
U kunt tooeither een klassiek of nieuw webservice implementeren.

### <a name="deploy-a-classic-web-service"></a>Een klassieke webservice implementeren
toodeploy als een klassieke webservice en maken van een toepassing tooconsume het:

1. Klik op uitvoeren Hallo onderaan Hallo experimentcanvas in.
2. Wanneer Hallo uitgevoerd is voltooid, klikt u op **webservice implementeren** en selecteer **webservice implementeren [klassieke]**.
3. Zoek uw API-sleutel op Hallo web servicedashboard. Kopieer en sla toouse later.
4. In Hallo **standaard eindpunt** tabel, klikt u op Hallo **Batchuitvoering** koppeling tooopen Hallo API Help-pagina.
5. Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.
6. Hallo zoeken op Hallo API Help-pagina, **voorbeeldcode** sectie Hallo Hallo pagina onderaan in.
7. Kopiëren en plakken Hallo C#-voorbeeldcode in uw Program.cs-bestand, en verwijder alle verwijzingen toohello blob-opslag.
8. Werk de waarde Hallo Hallo *apiKey* variabele met Hallo API-sleutel eerder hebt opgeslagen.
9. Zoek Hallo aanvraag declaratie en bij te werken Hallo waarden van Web Service Parameters die zijn doorgegeven toohello *importgegevens* en *gegevens exporteren* modules. In dit geval u Hallo oorspronkelijke query gebruiken, maar de naam van een nieuwe tabel definiëren.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Hallo-toepassing uitvoeren. 

Na voltooiing van Hallo uitvoert, wordt een nieuwe tabel toohello database Hallo score berekenen resultaten met toegevoegd.

### <a name="deploy-a-new-web-service"></a>Een nieuwe webservice implementeren

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

toodeploy als een nieuwe webservice en maken van een toepassing tooconsume het:

1. Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.
2. Wanneer Hallo uitgevoerd is voltooid, klikt u op **webservice implementeren** en selecteer **Web Service implementeren [New]**.
3. Voer een naam voor uw web-service op Hallo implementeren Experiment pagina en een prijscategorie selecteren en klik vervolgens op **implementeren**.
4. Op Hallo **Quick Start** pagina, klikt u op **verbruiken**.
5. In Hallo **voorbeeldcode** sectie, klikt u op **Batch**.
6. Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Windows Klassieke bureaublad** > **Console-App (.NET Framework)**.
7. Kopieer en plak Hallo C# voorbeeldcode in uw Program.cs-bestand.
8. Werk de waarde Hallo Hallo *apiKey* variabele Hello **primaire sleutel** zich in Hallo **Basic verbruik info** sectie.
9. Zoek Hallo *scoreRequest* declaratie en update Hallo-waarden van de Webserviceparameters die zijn doorgegeven toohello *importgegevens* en *gegevens exporteren* modules. In dit geval u Hallo oorspronkelijke query gebruiken, maar de naam van een nieuwe tabel definiëren.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Hallo-toepassing uitvoeren. 

