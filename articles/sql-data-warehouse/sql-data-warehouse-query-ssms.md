---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: Gebruik SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Verbinding maken met SQL Server Management Studio (SSMS) met tooSQL Data Warehouse
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Gebruik SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Vereisten
toouse deze zelfstudie hebt u nodig:

* Een bestaande SQL-datawarehouse. toocreate, Zie [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) geïnstalleerd. [Installeren van SSMS] [ Install SSMS] gratis als u nog geen hebt.
* Hallo volledig gekwalificeerde naam van SQL server. toofind deze, Zie [tooSQL datawarehouse verbinding][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Verbinding maken met SQL Data Warehouse tooyour
1. Open SSMS.
2. Object Explorer geopend. toodo deze, selecteer **bestand** > **Objectverkenner verbinding**.
   
    ![SQL Server-objectverkenner][1]
3. Vul de velden Hallo Hallo Connect tooServer-venster.
   
    ![Verbinding maken met tooServer][2]
   
   * **Server name** (Servernaam). Voer Hallo **servernaam** eerder hebt geïdentificeerd.
   * **Authentication** (Verificatie). Selecteer **SQL Server Authentication** (SQL Server-verificatie) of **Active Directory Integrated Authentication** (Geïntegreerde Active Directory-verificatie).
   * **User Name** (Gebruikersnaam) en **Password** (Wachtwoord). Voer de gebruikersnaam en het wachtwoord in als u hierboven SQL Server-verificatie hebt geselecteerd.
   * Klik op **Verbinden**.
4. tooexplore, vouw uw Azure SQL-server. Hallo-databases die zijn gekoppeld aan het Hallo-server, kunt u weergeven. Vouw AdventureWorksDW toosee Hallo tabellen in de voorbeelddatabase.
   
    ![AdventureWorksDW verkennen][3]

## <a name="2-run-a-sample-query"></a>2. Een voorbeeldquery uitvoeren
Nu dat een verbinding tot stand gebrachte tooyour database is, gaan we een query schrijven.

1. Klik met de rechtermuisknop op de database in SQL Server-objectverkenner.
2. Selecteer **New Query** (Nieuwe query). Een nieuwe queryvenster wordt geopend.
   
    ![Nieuwe query][4]
3. Kopieer de volgende TSQL-query naar Hallo query-venster:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Hallo-query uitvoeren. toodo, klikt u op `Execute` of gebruik Hallo volgende snelkoppeling: `F5`.
   
    ![Query uitvoeren][5]
5. Bekijkt hello queryresultaten. In dit voorbeeld factinternetsales Hallo heeft tabel 60398 rijen.
   
    ![Queryresultaten][6]

## <a name="next-steps"></a>Volgende stappen
Nu kunt u verbinding maken en een query, proberen [Hallo-gegevens met Power BI te visualiseren][visualizing hello data with PowerBI].

tooconfigure uw omgeving voor Azure Active Directory-verificatie, Zie [tooSQL Data Warehouse verifiëren][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
