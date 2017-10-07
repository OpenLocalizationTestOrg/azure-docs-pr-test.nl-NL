---
title: "aaaLoad gegevens in Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: Deze zelfstudie gegevens laadt in Azure SQL Data Warehouse met behulp van Azure Data Factory en maakt gebruik van een SQL Server-database als Hallo-gegevensbron.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Gegevens laden in SQL Data Warehouse met Data Factory

U kunt Azure Data Factory tooload gegevens in Azure SQL Data Warehouse vanaf elke Hallo [ondersteunde gegevensarchieven bron](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). U kunt bijvoorbeeld gegevens uit een Azure SQL database of een Oracle-database laden in een SQL datawarehouse met behulp van de Data Factory. Zelfstudie in dit artikel leert u hoe tooload gegevens uit een lokale SQL Server-database in een SQL datawarehouse.

**Tijd schatting**: in deze zelfstudie neemt ongeveer 10-15 minuten toocomplete als Hallo vereisten is voldaan.

## <a name="prerequisites"></a>Vereisten

- U moet een **SQL Server-database** met tabellen die gegevens Hallo bevatten toobe gekopieerd toohello SQL datawarehouse.  

- U moet een online **SQL Data Warehouse**. Als u nog geen datawarehouse, meer te weten hoe te[maken van een Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).

- U moet een **Azure Storage-Account**. Als u nog geen opslagaccount, meer te weten hoe te[een opslagaccount maken](../storage/common/storage-create-storage-account.md). Zoek naar Hallo storage-account voor de beste prestaties en Hallo datawarehouse in Hallo dezelfde Azure-regio.

## <a name="configure-a-data-factory"></a>Een gegevensfactory configureren
1. Meld u bij toohello [Azure-portal][].
2. Zoek uw datawarehouse en klikt u op tooopen deze.
3. Klik op de belangrijkste blade Hallo **gegevens laden** > **Azure Data Factory**.

    ![Gegevens laden wizard starten](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Als u een gegevensfactory niet in uw Azure-abonnement hebt, ziet u een **New Data Factory** dialoogvenster in een afzonderlijke tabblad van Hallo browser. Vul Hallo aangevraagde informatie en op **maken**. Nadat Hallo gegevensfactory is gemaakt, Hallo **New Data Factory** dialoogvenster wordt gesloten en u ziet Hallo **Selecteer Data Factory** in het dialoogvenster.

    Als u een of meer gegevensfactory's al in hello Azure-abonnement hebt, ziet u Hallo **Selecteer Data Factory** in het dialoogvenster. In dit dialoogvenster, u kunt selecteren van een bestaande gegevensfactory of klik op **maken nieuwe gegevensfactory** toocreate een nieuwe.

    ![Data Factory configureren](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. In Hallo **Selecteer Data Factory** dialoogvenster, Hallo **gegevens laden** optie is standaard geselecteerd. Klik op **volgende** toostart maken van een data laden van taak.

## <a name="configure-hello-data-factory-properties"></a>Hallo data factory-eigenschappen configureren
Nu dat u een gegevensfactory gemaakt hebt, is de volgende stap Hallo tooconfigure Hallo gegevens laden van de planning.

1. Voor **taaknaam**, voer **DWLoadData fromSQLServer**.
2. Standaard-Hallo **eenmaal nu uitvoeren** optie, klikt u op **volgende**.

    ![Configureer load planning](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Hallo brongegevensarchief en gateway configureren
U kunt nu de Data Factory over Hallo lokale SQL Server-database van waaruit u gegevens tooload wilt.

1. Kies **SQL Server** uit de brongegevens Hallo ondersteund catalogus opslaan en klik op **volgende**.

    ![SQL Server-bron kiezen](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. Een **lokale SQL Server-database. Geef Hallo** dialoogvenster wordt weergegeven. Hallo eerst **verbindingsnaam** veld wordt automatisch ingevuld. Hallo tweede veld vraagt om de naam op Hallo van Hallo **Gateway**. Als u een bestaande gegevensfactory waarop al een gateway gebruikt, kunt u Hallo gateway hergebruiken door deze te selecteren in de vervolgkeuzelijst Hallo. Klik op Hallo **Gateway maken** toocreate een Data Management Gateway koppelen.  

    > [!NOTE]
    > Als de brongegevens Hallo opslaat on-premises of in een virtuele machine van Azure IaaS een Data Management Gateway is vereist. Een gateway heeft een 1-1-relatie met een data factory. Kan niet worden gebruikt uit een andere data factory, maar deze kan worden gebruikt door meerdere gegevens bij het laden van taken met in Hallo dezelfde gegevensfactory. Een gateway kan gebruikte tooconnect toomultiple gegevensarchieven worden bij het uitvoeren van taken laden van gegevens.
    >
    > Zie voor gedetailleerde informatie over gateway-Hallo [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artikel.

3. Een **Gateway maken** dialoogvenster wordt weergegeven. Voer voor de naam, **GatewayForDWLoading**, en klik op **maken**.

4. Een **Gateway configureren** dialoogvenster wordt weergegeven. Klik op **snelle installatie op deze computer starten** tooautomatically downloaden, installeren en registreren van Data Management Gateway op de huidige computer. Hallo voortgang wordt weergegeven in een pop-upvenster. Als het Hallo-computer kan geen verbinding maken toohello gegevensarchief, kunt u handmatig [download en installeer de gateway Hallo](https://www.microsoft.com/download/details.aspx?id=39717) op een computer die verbinding van toohello gegevens maken kan opslaan en gebruik vervolgens de belangrijkste tooregister Hallo.
    > [!NOTE]
    > Hallo snelle installatie werkt systeemeigen met Microsoft Edge en Internet Explorer. Als u Google Chrome gebruikt, moet u eerst Hallo ClickOnce-extensie van de Chrome web store installeren.

    ![Snelle installatie starten](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Wachten op Hallo gateway setup toocomplete. Zodra de Hallo gateway is geregistreerd en online is, Hallo pop-upvenster wordt gesloten en Hallo nieuwe gateway wordt weergegeven in het veld Hallo-gateway. Vervolgens invullen Hallo rest velden als volgt vereist, klikt u op **volgende**.
    - **Servernaam**: naam van Hallo lokale SQL Server.
    - **Databasenaam**: SQL Server-database.
    - **Versleuteling van referenties**: Hallo standaard gebruiken 'door webbrowser".
    - **Verificatietype**: Kies Hallo type verificatie dat u gebruikt.
    - **Gebruikersnaam** en **wachtwoord**: Hallo-gebruikersnaam en wachtwoord invoeren voor een gebruiker met machtigingen toocopy Hallo gegevens.

    ![Snelle installatie starten](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. de volgende stap Hallo is toochoose Hallo tabellen vanuit welke toocopy Hallo-gegevens. U kunt Hallo tabellen filteren met behulp van trefwoorden. En kunt u gegevens en tabel schema Hallo in Hallo onderpaneel bekijken. Nadat u hebt geselecteerd, klikt u op **volgende**.

    ![Selecteer tabellen](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Hallo bestemming, uw SQL Data Warehouse configureren

U kunt nu de Data Factory over informatie over het Hallo-doel.

1. De verbindingsinformatie voor SQL Data Warehouse wordt automatisch ingevuld. Hallo wachtwoord opgeven voor Hallo-gebruikersnaam. en klik op **volgende**.

    ![Doel configureren](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Een intelligente tabeltoewijzing wordt weergegeven dat is toegewezen toodestination brontabellen op basis van tabelnamen. Als Hallo tabel niet in het Hallo-doel bestaat, standaard ADF maakt een Hello dezelfde naam (dit geldt tooSQL Server of Azure SQL Database als bron). U kunt ook toomap tooan bestaande tabel. Controleer en klik op **volgende**.

    ![Tabellen toewijzen](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Bekijk Hallo schematoewijzing en zoekt u fout- of waarschuwingsberichten. Intelligent toewijzing is gebaseerd op de kolomnaam. Als er een conversie van het type niet-ondersteunde gegevens tussen de bron- en doelserver kolom hello, ziet u een foutbericht weergegeven naast de bijbehorende tabel Hallo. Als u ervoor kiest toolet Data Factory automatisch Hallo tabellen maken, typeconversie van de juiste gegevens kan gebeuren als de toofix Hallo incompatibiliteit tussen bron- en doelserver winkels nodig.

    ![Schema toewijzen](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Klik op **Volgende**.

## <a name="configure-hello-performance-settings"></a>Hallo prestatie-instellingen configureren
In Hallo prestatieconfiguraties, configureert u een Azure storage-account gebruikt voor het Faseren van Hallo gegevens voordat deze wordt geladen in SQL Data Warehouse met behulp van sommen [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Nadat de Hallo kopie is voltooid, wordt Hallo tussentijdse gegevens in de opslag automatisch opgeschoond.

Selecteer een bestaand Azure Storage-account en klikt u op **volgende**.

![Fasering blob configureren](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Samenvattingsinformatie controleren en implementeer de pijplijn Hallo

Hallo-configuratie controleren en klik op **voltooien** knop toodeploy Hallo pijplijn.

![Gegevensfactory implementeren](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Monitor gegevens voortgang van het laden

U kunt zien Hallo implementatie voortgang en resultaten in Hallo **implementatie** pagina.

1. Als Hallo-implementatie is voltooid, klikt u op Hallo koppeling waarin staat dat **Klik hier toomonitor kopieerpijplijn** toomonitor gegevens te laden uitgevoerd.

    ![De pijplijn bewaken](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Hallo nieuw gemaakte **DWLoadData fromSQLServer** gegevens laden van de pijplijn wordt automatisch geselecteerd in Hallo links **Resource Explorer**.

    ![Pijplijn voor weergeven](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Klik in de pipeline Hallo in het midden Hallo Configuratiescherm toosee Hallo gedetailleerde status voor elke tabel die is toegewezen tooan activiteit.

    ![Activiteit van de tabel weergeven](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Verder op in een activiteit en ziet u Hallo gegevens bij het laden van gegevens in het rechterpaneel Hallo inclusief gegevensgrootte, rijen, doorvoer, enzovoort.

    ![Details van activiteit tabel weergeven](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch deze controle weergave hoger, gaat u tooyour SQL Data Warehouse, klikt u op **gegevens laden > Azure Data Factory**, selecteer uw gegevensfactory en kiezen **bewaken bestaande taken laden**.

## <a name="next-steps"></a>Volgende stappen

toomigrate uw database tooSQL datawarehouse, Zie [Migratieoverzicht](sql-data-warehouse-overview-migrate.md).

toolearn meer informatie over Azure Data Factory en de mogelijkheden van de verplaatsing van gegevens Zie Hallo artikelen te volgen:

- [Inleiding tooAzure Data Factory](../data-factory/data-factory-introduction.md)
- [Verplaatsen van gegevens met behulp van kopieerbewerking](../data-factory/data-factory-data-movement-activities.md)
- [Verplaatsen van gegevens tooand van Azure SQL Data Warehouse met behulp van Azure Data Factory](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore uw gegevens in SQL Data Warehouse, Zie Hallo volgende artikelen:

- [Verbinding maken met tooSQL Data Warehouse met Visual Studio en SSDT](sql-data-warehouse-query-visual-studio.md)
- [Visuele gegevens met Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[Azure Portal]: https://portal.azure.com
