---
title: Verbinding maken met Database tooAzure voor MySQL van MySQL Workbench | Microsoft Docs
description: Deze snelstartgids biedt Hallo stappen toouse MySQL Workbench tooconnect en query gegevens uit Azure-Database voor MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Azure MySQL-Database: gebruik MySQL Workbench tooconnect en query-gegevens
Deze snelstartgids demonstreert hoe tooconnect tooan Azure Database voor het gebruik van MySQL Hallo toepassing MySQL-Workbench. 

## <a name="prerequisites"></a>Vereisten
Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:
- [Een Azure-database voor een MySQL-server maken met behulp van Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Een Azure-database voor een MySQL-server maken met behulp van Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>MySQL-Workbench installeren
Download en installeer MySQL Workbench op uw computer uit [Hallo MySQL website](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen. U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).

2. Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **myserver4demo**.

3. Klik op Hallo servernaam.

4. Selecteer Hallo-server **eigenschappen** pagina. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.

 ![Azure servernaam MySQL-Database](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Verbinding maken met behulp van MySQL Workbench toohello-server 
tooAzure tooconnect MySQL-server met Hallo GUI-hulpprogramma MySQL Workbench:

1.  Hallo MySQL Workbench van toepassing op uw computer starten. 

2.  In **Setup nieuwe verbinding** dialoogvenster en voer de volgende informatie op Hallo Hallo **Parameters** tabblad:

    ![nieuwe verbinding instellen](./media/connect-workbench/2-setup-new-connection.png)

    | **Instelling** | **Voorgestelde waarde** | **Beschrijving van veld** |
    |---|---|---|
    |   Verbindingsnaam | Demo-verbinding | Geef een label op voor deze verbinding. |
    | Verbindingsmethode | Standard (TCP/IP) | Standard (TCP/IP) is voldoende. |
    | Hostnaam | *servernaam* | Hallo-server de naam van waarde dat werd gebruikt toen u eerder hebt gemaakt hello Azure Database voor MySQL opgeven. De server in ons voorbeeld is myserver4demo.mysql.database.azure.com. Gebruik Hallo volledig gekwalificeerde domeinnaam (\*. mysql.database.azure.com) zoals weergegeven in Hallo-voorbeeld. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer de servernaam van uw weet.  |
    | Poort | 3306 | Gebruik altijd poort 3306 bij het verbinden van tooAzure Database voor MySQL. |
    | Gebruikersnaam |  *aanmeldnaam van serverbeheerder* | Typ Hallo server admin aanmelding gebruikersnaam opgegeven toen u eerder hebt gemaakt hello Azure Database voor MySQL. De gebruikersnaam in ons voorbeeld is myadmin@myserver4demo. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer Hallo gebruikersnaam weet. Hallo-indeling is  *username@servername* .
    | Wachtwoord | Uw wachtwoord | Klik op **Store in kluis...**  knop toosave Hallo wachtwoord. |

3.   Klik op **testverbinding** tootest als alle parameters juist zijn geconfigureerd. 

4.   Klik op **OK** toosave Hallo verbinding. 

5.   In de aanbieding Hallo van **MySQL verbindingen**, klik op Hallo bijbehorende tooyour tegelserver en wachten op Hallo verbinding toobe tot stand gebracht.

6.   Een nieuwe SQL-tabblad is geopend met een lege editor u uw query's typt.

    > [!NOTE]
    > Standaard is de beveiliging van de SSL-verbinding vereist en afgedwongen voor uw Azure-Database voor de MySQL-server. Geen aanvullende configuratie met SSL-certificaten is doorgaans vereist voor MySQL Workbench tooconnect tooyour server. Zie voor meer informatie over SSL [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md).  Als u toodisable SSL moet, gaat u naar hello Azure-portal en klik Hallo verbinding beveiliging pagina toodisable Hallo afdwingen SSL verbinding in-of uitschakelen.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Een tabel maken, gegevens invoegen, gegevens lezen, bijwerken van gegevens en gegevens verwijderen
1. Kopieer en plak de voorbeeldcode SQL Hallo in een lege SQL tabblad tooillustrate voorbeeldgegevens.

    Deze code maakt een lege database met de naam quickstartdb en maakt vervolgens een tabel met de naam inventory. Hiermee voegt een aantal rijen en vervolgens Hallo rijen leest. Hallo-gegevens met een update-instructie wordt gewijzigd en leesbewerkingen Hallo rijen opnieuw. Ten slotte deze een rij verwijdert en opnieuw Hallo rijen leest.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    Hallo Schermafbeelding toont een voorbeeld van Hallo SQL-code in de uitvoer van SQL Workbench en Hallo nadat deze is uitgevoerd.
    
    ![MySQL-Workbench SQL tabblad toorun voorbeeldcode SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. toorun hello voorbeeld SQL-Code, klikt u op het pictogram op de werkbalk Hallo Hallo lichter Hallo **SQL-bestand** tabblad.
3. Let op drie tabbladen resulteert in een Hallo Hallo **resultaat raster** sectie in het midden Hallo van Hallo pagina. 
4. Kennisgeving Hallo **uitvoer** lijst onderaan Hallo Hallo pagina. Hallo-status van elke opdracht wordt weergegeven. 

Nu u verbinding hebt tooAzure Database gemaakt voor gebruik van MySQL Workbench MySQL en gegevens met behulp van de SQL-taal Hallo hebt opgevraagd.

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./concepts-migrate-import-export.md)
