---
title: aaaUse Azure Stream Analytics met SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Azure Stream Analytics met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Azure Stream Analytics gebruiken met SQL datawarehouse
Azure Stream Analytics is een volledig beheerde service lage latentie, maximaal beschikbare, schaalbare complexe verwerking van gebeurtenissen boven het streamen van gegevens in de cloud Hallo bieden. U kunt basisbegrippen Hallo door te lezen [inleiding tooAzure Stream Analytics][Introduction tooAzure Stream Analytics]. Vervolgens leert u hoe een end-to-end-oplossing met Stream Analytics door toocreate Hallo [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.

In dit artikel leert u hoe toouse uw Azure SQL Data Warehouse-database als uitvoerlocatie voor uw stoom Analytics-taken.

## <a name="prerequisites"></a>Vereisten
Voer eerst via de volgende stappen uit in Hallo Hallo [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.  

1. De invoer van een Event Hub maken
2. Configureren en starten van de gebeurtenis generator-toepassing
3. Inrichten van een Stream Analytics-taak
4. Taak invoer- en query opgeven

Vervolgens maakt u een Azure SQL Data Warehouse-database

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Geef de taakuitvoer: Azure SQL Data Warehouse-database
### <a name="step-1"></a>Stap 1
Klik in de Stream Analytics-taak op **uitvoer** vanaf de bovenkant Hallo Hallo pagina en klik vervolgens op **uitvoer toevoegen**.

### <a name="step-2"></a>Stap 2
Selecteer de SQL-Database en klik op volgende.

![][add-output]

### <a name="step-3"></a>Stap 3
Voer de volgende waarden op de volgende pagina Hallo Hallo:

* *Uitvoer Alias*: een beschrijvende naam voor de taakuitvoer van deze.
* *Abonnement*:
  * Als uw SQL Data Warehouse-database in Hallo is hetzelfde abonnement als Hallo Stream Analytics-taak, selecteert u gebruik SQL Database uit het huidige abonnement.
  * Als uw database zich in een ander abonnement, selecteert u gebruik SQL Database in een ander abonnement.
* *Database*: Hallo-naam van een doeldatabase opgeven.
* *Servernaam*: Geef de servernaam Hallo voor Hallo-database die u zojuist hebt opgegeven. U kunt Hallo klassieke Azure-Portal toofind deze gebruiken.

![][server-name]

* *Gebruikersnaam*: Geef de gebruikersnaam op Hallo van een account met schrijfmachtigingen voor Hallo-database.
* *Wachtwoord*: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.
* *Tabel*: Hallo naam opgeven van de doeltabel Hallo in Hallo-database.

![][add-database]

### <a name="step-4"></a>Stap 4
Klik op Hallo selectievakje knop tooadd deze taakuitvoer en tooverify dat Stream Analytics verbinding toohello database maken kan.

![][test-connection]

Als de databaseverbinding toohello Hallo is geslaagd, ziet u een melding onderaan Hallo Hallo-portal. U kunt klikken op verbinding testen op Hallo onder tootest Hallo verbinding toohello database.

## <a name="next-steps"></a>Volgende stappen
Zie voor een overzicht van de integratie van [overzicht van de integratie van SQL Data Warehouse][SQL Data Warehouse integration overview].

Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
