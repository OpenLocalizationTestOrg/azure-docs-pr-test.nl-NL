---
title: aaaUse Azure Machine Learning met SQL Data Warehouse | Microsoft Docs
description: Zelfstudie voor het gebruik van Azure Machine Learning met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Gebruik Azure Machine Learning met SQL datawarehouse
Azure Machine Learning is een volledig beheerde predictive analytics-service dat u kunt het gebruiken van voorspellende modellen toocreate op basis van uw gegevens in SQL Data Warehouse en vervolgens als webservices gereed om te gebruiken publiceren. U kunt de basisbegrippen Hallo van predictive analytics en machine learning door te lezen [inleiding tooMachine Learning in Azure][Introduction tooMachine Learning on Azure].  Vervolgens leert u hoe toocreate, trainen, beoordelen en testen van een machine learning-model met Hallo [maken experiment zelfstudie][Create experiment tutorial].

In dit artikel leert u hoe toodo Hallo volgen met behulp van Hallo [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Gegevens lezen uit de database-toocreate, te trainen en een Voorspellend model beoordelen
* Gegevens tooyour database schrijven

## <a name="read-data-from-sql-data-warehouse"></a>Lezen van gegevens uit SQL Data Warehouse
Leest gegevens uit de tabel Product in de database AdventureWorksDW Hallo.

### <a name="step-1"></a>Stap 1
Start een nieuw experiment door te klikken op + Nieuw onderin Hallo Hallo Machine Learning Studio-venster EXPERIMENT selecteren en selecteer vervolgens leeg Experiment. Selecteer Hallo standaard naam Hallo boven aan het papier Hallo experiment en wijzig deze toosomething zinvolle, bijvoorbeeld fiets prijs voorspelling.

### <a name="step-2"></a>Stap 2
Leesmodule hello in Hallo palet met gegevenssets en modules op Hallo links van het experimentcanvas Hallo zoekt. Sleep Hallo module toohello experimentcanvas.
![][drag_reader]

### <a name="step-3"></a>Stap 3
Leesmodule hello Selecteer en invullen Hallo eigenschappendeelvenster.

1. Selecteer de Azure SQL Database als Hallo gegevensbron.
2. Database-servernaam: typenaam van het Hallo-server. U kunt Hallo [Azure-portal] [ Azure portal] toofind dit.

![][server_name]

1. Databasenaam: Type Hallo-naam van een database op Hallo-server die u zojuist hebt opgegeven.
2. Server gebruikersaccountnaam: Typ de gebruikersnaam van een account met toegangsmachtigingen voor de database Hallo Hallo.
3. Het wachtwoord voor gebruikersaccount server: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.
4. Een servercertificaat accepteren: Gebruik deze optie (minder veilig) als u wilt dat tooskip Hallo sitecertificaat controleren voordat u uw gegevens leest.
5. Databasequery: Voer een SQL-instructie waarmee Hallo gegevens u wilt dat tooread worden beschreven. In dit geval wordt we gegevens uit de tabel Product met behulp van de volgende query Hallo lezen.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Stap 4
1. Hallo-experiment door te klikken op uitvoeren onder het experimentcanvas Hallo uitgevoerd.
2. Wanneer het Hallo-experiment is voltooid, hebt Hallo leesmodule een groen vinkje tooindicate die het met succes is voltooid. U ziet ook Hallo status uitgevoerd in de rechterbovenhoek Hallo voltooid.

![][run]

1. toosee Hallo geïmporteerde gegevens, klikt u op de uitvoerpoort Hallo HALLO hallo auto gegevensset onderaan in en selecteer visualiseren.

## <a name="create-train-and-score-a-model"></a>Maken, te trainen en een model beoordelen
Nu kunt u deze gegevensset te gebruiken:

* Een Model maken: gegevens verwerken en functies definiëren
* Train Hallo model: kiezen en toepassen van een leeralgoritme
* Score en test Hallo model: nieuwe fiets prijs voorspellen

![][model]

meer informatie over hoe toocreate, trainen, beoordelen en testen van een machine learning-model gebruik Hallo toolearn [maken experiment zelfstudie][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Schrijven van gegevens tooAzure SQL Data Warehouse
We schrijft set Hallo-tooProductPriceForecast resultaattabel in de database AdventureWorksDW Hallo.

### <a name="step-1"></a>Stap 1
Hallo-schrijfmodule in Hallo palet met gegevenssets en modules op Hallo links van het experimentcanvas Hallo zoekt. Sleep Hallo module toohello experimentcanvas.

![][drag_writer]

### <a name="step-2"></a>Stap 2
Hallo-schrijfmodule Selecteer en invullen Hallo eigenschappendeelvenster.

1. Selecteer Azure SQL Database als Hallo gegevensbestemming.
2. Database-servernaam: typenaam van het Hallo-server. U kunt Hallo [Azure-portal] [ Azure portal] toofind dit.
3. Databasenaam: Type Hallo-naam van een database op Hallo-server die u zojuist hebt opgegeven.
4. Server gebruikersaccountnaam: Typ de gebruikersnaam van een account met schrijfmachtigingen voor de database Hallo Hallo.
5. Het wachtwoord voor gebruikersaccount server: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.
6. Een servercertificaat (onbeveiligde) accepteren: Selecteer deze optie als u niet dat tooview Hallo certificaat wilt.
7. Door komma's gescheiden lijst met kolommen toobe opgeslagen: een lijst verstrekken van Hallo gegevensset of het resultaat van de kolommen die u toooutput wilt.
8. Data-tabelnaam: Hallo naam opgeven van Hallo gegevenstabel.
9. Door komma's gescheiden lijst met datatable kolommen: Hallo kolom namen toouse in de nieuwe tabel Hallo opgeven. Hello kolomnamen kunnen afwijken van Hallo die in Hallo bron gegevensset, maar u moet de lijst met hetzelfde aantal kolommen hierheen die u voor de uitvoertabel Hallo definieert Hallo.
10. Aantal rijen per SQL Azure-bewerking geschreven: U kunt configureren Hallo aantal rijen dat tooa SQL-database zijn geschreven in één bewerking.

![][writer_properties]

### <a name="step-3"></a>Stap 3
1. Hallo-experiment door te klikken op uitvoeren onder het experimentcanvas Hallo uitgevoerd.
2. Wanneer het Hallo-experiment is voltooid, hebben alle modules een groen vinkje tooindicate dat ze is voltooid.

## <a name="next-steps"></a>Volgende stappen
Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
