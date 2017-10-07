---
title: aaaConnect Excel tooSQL Database | Microsoft Docs
description: Meer informatie over hoe tooconnect Microsoft Excel tooAzure SQL-database in de cloud Hallo. Gegevens importeren in Excel voor rapportage en gegevens verkenning.
services: sql-database
keywords: verbinding maken met excel toosql, gegevens tooexcel importeren
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Verbinding maken met Excel tooan Azure SQL database en een rapport maken

Verbinding maken met Excel tooa SQL database in de cloud Hallo en gegevens importeren en tabellen en grafieken op basis van waarden in Hallo-database maken. In deze zelfstudie u Hallo verbinding tussen Excel en een databasetabel stelt Hallo-bestand met gegevens en Hallo verbindingsinformatie voor Excel opslaan, en maak vervolgens een draaigrafiek uit Hallo databasewaarden.

Voordat u begint hebt u een SQL Database in Azure nodig. Als u niet hebt, raadpleegt u [uw eerste SQL-database maken](sql-database-get-started-portal.md) tooget een database met voorbeeldgegevens binnen enkele minuten duren. In dit artikel, zult u voorbeeldgegevens importeren in Excel van dat artikel, maar u kunt dezelfde stappen volgen met uw eigen gegevens.

U hebt ook een kopie van Excel nodig. Dit artikel gebruikt [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Verbinding maken met Excel tooa SQL database en een odc-bestand maken
1. tooconnect Excel tooSQL database open Excel en maak een nieuwe werkmap of open een bestaande Excel-werkmap.
2. Klik in de menubalk Hallo bovenaan Hallo Hallo pagina **gegevens**, klikt u op **van andere bronnen**, en klik vervolgens op **van SQL Server**.
   
   ![Selecteer gegevensbron: verbinding maken met Excel tooSQL database.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Hallo Wizard Gegevensverbinding wordt geopend.
3. In Hallo **tooDatabase Server verbinding** in het dialoogvenster type Hallo SQL-Database **servernaam** tooconnect tooin Hallo formulier <*servername* > **. database.windows.net**. Bijvoorbeeld: **adworkserver.database.windows.net**.
4. Onder **aanmeldingsreferenties**, klikt u op **gebruik Hallo volgende gebruikersnaam en wachtwoord**, type Hallo **gebruikersnaam** en **wachtwoord** u is ingesteld voor Hallo SQL Database-server wanneer u het hebt gemaakt en klik vervolgens op **volgende**.
   
   ![Typ de servernaam en aanmeldingsreferenties in Hallo server](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Afhankelijk van uw netwerkomgeving u mogelijk niet kunnen tooconnect of Hallo verbinding mogelijk wordt verbroken als verkeer van de IP-adres van uw client Hallo SQL Database-server niet is toegestaan. Ga toohello [Azure-portal](https://portal.azure.com/)op SQL-servers, klikt u op uw server, klikt u op firewall onder instellingen en voeg uw client-IP-adres. Zie [hoe tooconfigure firewall-instellingen](sql-database-configure-firewall-settings.md) voor meer informatie.
   > 
   > 
5. In Hallo **Database en tabel selecteren** dialoogvenster, selecteer Hallo database u wilt toowork met uit Hallo lijst en klik vervolgens op Hallo tabellen of weergaven die u toowork met wilt (We hebben gekozen **vGetAllCategories**), en vervolgens Klik op **volgende**.
   
    ![Selecteer een database en tabel.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Hallo **bestand opslaan en voltooien** in het dialoogvenster wordt geopend, waarin u informatie over Hallo Office database connection (*.odc) bestand dat Excel gebruikt opgeven. U kunt Hallo standaardinstellingen laten staan of uw selecties aanpassen.
6. U kunt laten Hallo standaardinstellingen, maar Opmerking Hallo **bestandsnaam** in het bijzonder. Een **beschrijving**, een **beschrijvende naam**, en **zoekwoorden** helpen u en andere gebruikers te onthouden wat u verbinding maakt tooand Hallo verbinding vinden. Klik op **altijd proberen toouse deze bestandsgegevens toorefresh** als u wilt dat verbindingsgegevens worden opgeslagen in Hallo ODC-bestand, zodat deze bijgewerkt kan wanneer u verbinding maken met tooit en klik vervolgens op **voltooien**.
   
    ![Opslaan van een odc-bestand](./media/sql-database-connect-excel/save-odc-file.png)
   
    Hallo **gegevens importeren** dialoogvenster wordt weergegeven.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Hallo-gegevens importeren in Excel en maak een draaigrafiek.
Nu dat u hebt ingesteld Hallo verbinding en gemaakte Hallo-bestand met gegevens en de verbindingsinformatie, leest u tooimport Hallo gegevens.

1. In Hallo **gegevens importeren** dialoogvenster, klikt u op Hallo gewenste optie voor uw gegevens weer in Hallo werkblad en klik vervolgens op **OK**. We hebben **draaigrafiek** gekozen. U kunt ook toocreate een **nieuw werkblad** of te**toevoegen van deze gegevens tooa gegevensmodel**. Zie voor meer informatie over gegevensmodellen [Een gegevensmodel maken in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Klik op **eigenschappen** tooexplore meer informatie over Hallo ODC-bestand u hebt gemaakt in Hallo vorige stap en toochoose opties voor het vernieuwen van Hallo-gegevens.
   
    ![Hallo-indeling voor gegevens kiezen in Excel](./media/sql-database-connect-excel/import-data.png)
   
    Hallo werkblad heeft nu een lege draaitabel en grafiek.
2. Onder **PivotTable-Fields**, schakel alle selectievakjes voor Hallo Hallo velden die u wilt tooview.
   
    ![Databaserapport configureren.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Als u wilt dat tooconnect andere Excel-werkmappen en werkbladen toohello-database, klikt u op **gegevens**, klikt u op **verbindingen**, klikt u op **toevoegen**, kies Hallo-verbinding die u hebt gemaakt in de lijst Hallo en klik vervolgens op **Open**.
> ![Een verbinding openen vanuit een andere werkmap](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[tooSQL Database met SQL Server Management Studio verbinding](sql-database-connect-query-ssms.md) voor geavanceerde query's en analyse.
* Meer informatie over de voordelen van Hallo [elastische pools](sql-database-elastic-pool.md).
* Meer informatie over hoe te[maken van een webtoepassing die verbinding tooSQL Database op Hallo back-end maakt](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

