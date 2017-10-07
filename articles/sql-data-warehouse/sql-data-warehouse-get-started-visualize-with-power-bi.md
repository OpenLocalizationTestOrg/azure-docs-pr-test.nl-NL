---
title: aaaVisualize SQL Data Warehouse-gegevens met Power BI | Microsoft Azure
description: SQL Data Warehouse-gegevens visualiseren met Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Gegevens visualiseren met Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Deze zelfstudie leert u hoe toouse Power BI tooconnect tooSQL Data Warehouse en enkele eenvoudige visualisaties maakt.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Vereisten
toostep voor deze zelfstudie hebt u nodig:

* Een SQL Data Warehouse worden vooraf geladen met de database AdventureWorksDW Hallo. tooprovision deze, Zie [maken van een SQL Data Warehouse] [ Create a SQL Data Warehouse] en kies tooload Hallo voorbeeldgegevens. Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Verbinding maken met database tooyour
tooopen Power BI en verbinding maken met de database AdventureWorksDW tooyour:

1. Meld u aan bij Hallo [Azure-portal][Azure portal].
2. Klik op **SQL-databases** en kies de SQL Data Warehouse-database AdventureWorks.
   
    ![De database zoeken][1]
3. Klik op 'Openen in Power BI' Hallo-knop.
   
    ![Power BI-knop][2]
4. U ziet nu Hallo verbindingspagina voor SQL Data Warehouse om het webadres van uw database weer te geven. Klik op volgende.
   
    ![Verbinding met Power BI][3]
5. Voer uw Azure SQL server-gebruikersnaam en wachtwoord en kunt u zich volledig verbonden tooyour SQL Data Warehouse-database.
   
    ![Aanmelden bij Power BI][4]
6. Nadat u bent aangemeld bij Power BI, klikt u op Hallo AdventureWorksDW gegevensset op Hallo links blade. Hiermee opent u het Hallo-database.
   
    ![AdventureWorksDW wordt geopend in Power BI][5]

## <a name="2-create-a-report"></a>2. Een rapport maken
U bent nu klaar toouse Power BI tooanalyze uw voorbeeldgegevens van AdventureWorksDW. tooperform hello analyse, AdventureWorksDW heeft een weergave die aggregatesales wordt genoemd. Deze weergave bevat een aantal Hallo belangrijkste metrische gegevens voor het analyseren van Hallo verkoop van Hallo bedrijf.

1. toocreate een toewijzing van omzet volgens toopostal-code in deelvenster Hallo rechterdeelvenster met velden, klikt u op Hallo AggregateSales weergave tooexpand deze. Klik op Hallo PostalCode en SalesAmount kolommen tooselect ze.
   
    ![AggregateSales selecteren in Power BI][6]
   
    De gegevens, die in Power BI automatisch worden herkend als geografische gegevens, worden in een kaart geplaatst.
   
    ![Power BI-kaart][7]
2. In deze stap maakt u een staafdiagram waarin de totale verkoop per klantinkomen wordt weergegeven. toocreate deze Ga toohello uitgevouwen weergave AggregateSales. Klik op Hallo SalesAmount veld. Hallo Customer Income veld toohello links Sleep en zet het neer in as.
   
    ![As selecteren in Power BI][8]
   
    We verplaatst Hallo staafdiagram via Hallo links.
   
    ![Power BI-staafdiagram][9]
3. Met deze stap maakt u een lijndiagram waarin de omzet per datum wordt weergegeven. toocreate deze Ga toohello uitgevouwen weergave AggregateSales. Klik op SalesAmount en OrderDate. Klik in Hallo visualisaties kolom Hallo lijndiagram pictogram; Dit is het eerste pictogram Hallo in Hallo tweede regel onder visualisaties.
   
    ![Lijndiagram selecteren in Power BI][10]
   
    U hebt nu een rapport met drie verschillende visualisaties van Hallo-gegevens.
   
    ![Power BI-lijndiagram][11]

U kunt de voortgang op elk moment opslaan door op **Bestand** te klikken en **Opslaan** te selecteren.

## <a name="next-steps"></a>Volgende stappen
Nu we hebt u enige tijd toowarm maximaal verleend met voorbeeldgegevens hello, gaat u naar hoe te[ontwikkelen][develop], [laden][load], of [ migreren][migrate]. Of bekijk Hallo [website van Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
