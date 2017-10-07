---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
description: "Query’s uitvoeren bij SQL Data Warehouse met Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Verbinding maken met tooSQL Data Warehouse met Visual Studio en SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Gebruik Visual Studio tooquery Azure SQL Data Warehouse in een paar minuten. Deze methode maakt gebruik van SQL Server Data Tools (SSDT)-extensie Hallo in Visual Studio. 

## <a name="prerequisites"></a>Vereisten
toouse deze zelfstudie hebt u nodig:

* Een bestaande SQL-datawarehouse. toocreate, Zie [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].
* SSDT voor Visual Studio. Als u Visual Studio hebt, hebt u dit waarschijnlijk al. Zie [Visual Studio en SSDT installeren][Installing Visual Studio and SSDT] voor instructies en opties voor de installatie.
* Hallo volledig gekwalificeerde naam van SQL server. toofind deze, Zie [tooSQL datawarehouse verbinding][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Verbinding maken met SQL Data Warehouse tooyour
1. Open Visual Studio 2013 of 2015.
2. Open SQL Server-objectverkenner. toodo deze, selecteer **weergave** > **SQL Server Object Explorer**.
   
    ![SQL Server-objectverkenner][1]
3. Klik op Hallo **SQL-Server toevoegen** pictogram.
   
    ![SQL Server toevoegen][2]
4. Vul de velden Hallo Hallo Connect tooServer-venster.
   
    ![Verbinding maken met tooServer][3]
   
   * **Server name** (Servernaam). Voer Hallo **servernaam** eerder hebt geïdentificeerd.
   * **Authentication** (Verificatie). Selecteer **SQL Server Authentication** (SQL Server-verificatie) of **Active Directory Integrated Authentication** (Geïntegreerde Active Directory-verificatie).
   * **User Name** (Gebruikersnaam) en **Password** (Wachtwoord). Voer de gebruikersnaam en het wachtwoord in als u hierboven SQL Server-verificatie hebt geselecteerd.
   * Klik op **Verbinden**.
5. tooexplore, vouw uw Azure SQL-server. Hallo-databases die zijn gekoppeld aan het Hallo-server, kunt u weergeven. Vouw AdventureWorksDW toosee Hallo tabellen in de voorbeelddatabase.
   
    ![AdventureWorksDW verkennen][4]

## <a name="2-run-a-sample-query"></a>2. Een voorbeeldquery uitvoeren
Nu dat een verbinding tot stand gebrachte tooyour database is, gaan we een query schrijven.

1. Klik met de rechtermuisknop op de database in SQL Server-objectverkenner.
2. Selecteer **New Query** (Nieuwe query). Een nieuwe queryvenster wordt geopend.
   
    ![Nieuwe query][5]
3. Kopieer de volgende TSQL-query naar Hallo query-venster:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Hallo-query uitvoeren. toodo, klikt u op Hallo groene pijl of gebruik Hallo volgende snelkoppeling: `CTRL` + `SHIFT` + `E`.
   
    ![Query uitvoeren][6]
5. Bekijkt hello queryresultaten. In dit voorbeeld factinternetsales Hallo heeft tabel 60398 rijen.
   
    ![Queryresultaten][7]

## <a name="next-steps"></a>Volgende stappen
Nu kunt u verbinding maken en een query, proberen [Hallo-gegevens met Power BI te visualiseren][visualizing hello data with PowerBI].

tooconfigure uw omgeving voor Azure Active Directory-verificatie, Zie [tooSQL Data Warehouse verifiëren][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
