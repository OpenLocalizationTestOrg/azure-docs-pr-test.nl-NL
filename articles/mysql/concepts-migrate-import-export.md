---
title: aaaImport en exporteren in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt uitgelegd van algemene manieren tooimport en export-databases in de Azure-Database voor MySQL, met behulp van hulpprogramma's zoals MySQL-Workbench.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Uw MySQL-database migreren met behulp van importeren en exporteren
In dit artikel wordt uitgelegd van twee algemene benaderingen tooimporting en uitvoer gegevens tooan Azure Database voor de MySQL-server met behulp van MySQL-Workbench. 

## <a name="before-you-begin"></a>Voordat u begint
toostep via deze procedure-tooguide die u nodig:
- Een Azure-Database voor de MySQL-server door het volgende [maken van een Azure-Database voor de MySQL-server met Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL-Workbench [gedownload](https://dev.mysql.com/downloads/workbench/), of een ander hulpprogramma tooimport van MySQL en exporteren.

## <a name="use-common-tools"></a>Algemene hulpprogramma's gebruiken
Algemene hulpprogramma's gebruiken zoals MySQL Workbench, Toad of Navicat tooremotely verbinding maken en importeren of exporteren van gegevens in Azure-Database voor MySQL. 

Gebruik deze hulpprogramma's op de clientcomputer met een Internet verbinding tooconnect tooAzure Database voor MySQL. Een met SSL versleutelde verbinding gebruiken voor aanbevolen procedures voor beveiliging, zoals beschreven in [configureren van SSL-verbindingen in Azure-Database voor MySQL](concepts-ssl-connection-security.md).

U niet moet toomove uw importeren en exporteren tooany speciale cloud locatie bij het migreren van tooAzure Database voor MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Een database maakt op Hallo Azure Database voor de MySQL-server
Een lege database maken op Hallo Azure Database voor de MySQL-server waar u toomigrate Hallo gegevens. Gebruik een hulpprogramma zoals MySQL Workbench, Toad of Navicat toocreate Hallo-database. Hallo-database kan Hallo dezelfde naam als het Hallo-database dat Hallo gedumpt gegevens, of u bevat kunt een database maken met een andere naam hebben.

tooget verbonden, vinden de verbindingsgegevens Hallo op Hallo **eigenschappen** deelvenster in Azure voor MySQL-Database.

![Hallo-verbindingsgegevens niet vinden in hello Azure-portal](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Hallo verbinding informatie tooMySQL Workbench toevoegen.

![MySQL-Workbench verbindingsreeks](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Bepalen wanneer toouse importeren en exporteren van technieken in plaats van een dump en herstellen
Gebruik van MySQL extra tooimport en databases exporteren naar Azure MySQL-Database in de volgende scenario's Hallo. In andere scenario's, kunt u profiteren van het gebruik van Hallo [dump maken en terugzetten](concepts-migrate-dump-restore.md) in plaats daarvan benaderen. 

- Wanneer u tooselectively moet enkele tabellen tooimport kiezen uit een bestaande MySQL-database in Azure MySQL-Database, de beste toouse Hallo importeren en exporteren van techniek.  Op deze manier kunt u eventuele overbodige tabellen vanuit Hallo migratie toosave tijd en hulpbronnen weglaten. Gebruik bijvoorbeeld Hallo `--include-tables` of `--exclude-tables` overschakelen met [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) en Hallo `--tables` overschakelen met [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Wanneer u objecten in de database Hallo dan tabellen wilt verplaatsen, die expliciet te maken. Omvatten beperkingen (primaire sleutel, refererende sleutel, indexen), weergaven, functies, procedures, triggers en een andere database-objecten die u toomigrate wilt.
- Uit externe gegevensbronnen dan een MySQL-database waarnaar u gegevens migreert, platte bestanden te maken en deze importeren met behulp van [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Zorg ervoor dat alle tabellen in de database Hallo Hallo InnoDB opslag-engine gebruiken wanneer u gegevens in Azure-Database voor MySQL laadt. Azure MySQL-Database ondersteunt alleen Hallo InnoDB opslag-engine, zodat deze biedt geen ondersteuning voor alternatieve opslag-engines. Als uw tabellen engines alternatieve opslag is vereist, worden ervoor tooconvert ze toouse hello InnoDB engine indeling voordat Hallo migratie tooAzure Database voor MySQL. 

Bijvoorbeeld, hebt u een WordPress of web-app die gebruikmaakt van Hallo MyISAM engine, eerst converteren Hallo tabellen migreren Hallo van gegevens in InnoDB tabellen. Voor MySQL tooAzure Database herstellen. Gebruik Hallo component `ENGINE=INNODB` tooset Hallo-engine voor het maken van een tabel en vervolgens Hallo gegevens overdragen naar Hallo compatibel tabel vóór de migratie Hallo. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Prestaties aanbevelingen voor het importeren en exporteren
-   Geclusterde indexen en primaire sleutels maken voordat gegevens worden geladen. Laden van gegevens in de primaire sleutel volgorde. 
-   Maken van secundaire indexen pas na gegevens vertraging is geladen. Alle secundaire indexen maken na het laden. 
-   Schakel de referentiële-sleutelbeperkingen voordat deze worden geladen. Refererende sleutel controles uit te schakelen biedt aanzienlijke prestatieverbeteringen. Schakel Hallo beperkingen en Hallo gegevens na het Hallo load tooensure referentiële integriteit verifiëren.
-   Gegevens parallel worden geladen. Vermijd te veel parallelle uitvoering die zou leiden dat u een limiet resource toohit en resources bewaken met behulp van Hallo metrische gegevens beschikbaar zijn in hello Azure-portal. 
-   Gepartitioneerde tabellen, indien van toepassing gebruiken.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importeren en exporteren met behulp van MySQL Workbench
Er zijn twee manieren tooexport en importeer gegevens in de MySQL-Workbench. Elk fungeert een ander doel. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Gegevens in een tabel exporteren en importeren van wizards in het contextmenu Hallo object browser
![MySQL-Workbench wizards in het contextmenu Hallo object browser](./media/concepts-migrate-import-export/p1.png)

Hallo wizards voor tabelgegevens ondersteuning voor importeren en exporteren van bewerkingen met behulp van CSV en JSON-bestanden. Ze omvatten diverse configuratieopties, zoals scheidingstekens, kolomselectie en codering selecteren. U kunt elke wizard lokaal of extern verbonden MySQL-servers uitvoeren. Hallo importactie bevat een tabel-, kolom- en toewijzing van het type. 

U kunt deze wizards in het contextmenu Hallo object browser openen met de rechtermuisknop op een tabel. Kies een **Wizard tabel gegevens exporteren** of **Wizard tabel importeren**. 

#### <a name="table-data-export-wizard"></a>Wizard tabel gegevens exporteren
Hallo volgende voorbeeld wordt geëxporteerd Hallo tabel tooa CSV-bestand: 
1. Met de rechtermuisknop op Hallo inhoudsopgave Hallo database toobe geëxporteerd. 
2. Selecteer **Wizard gegevens exporteren tabel**. Selecteer Hallo kolommen toobe geëxporteerd, wordt een rijoffset (indien aanwezig) en count (indien aanwezig). 
3. Op Hallo **Selecteer gegevens voor het exporteren van** pagina, klikt u op **volgende**. Selecteer Hallo bestandspad, CSV of JSON bestandstype. Hallo-regelscheiding, methode van insluitende tekenreeksen en veldscheidingsteken ook selecteren. 
4. Op Hallo **Selecteer uitvoer bestandslocatie** pagina, klikt u op **volgende**. 
5. Op Hallo **gegevens exporteren** pagina, klikt u op **volgende**.

#### <a name="table-data-import-wizard"></a>Wizard tabel importeren
Hallo volgende voorbeeld worden Hallo tabel uit een CSV-bestand:
1. Met de rechtermuisknop op Hallo inhoudsopgave Hallo database toobe geïmporteerd. 
2. Bladeren tooand Selecteer Hallo CSV-bestand toobe geïmporteerd en klik vervolgens op **volgende**. 
3. Selecteer Hallo doeltabel (nieuw of bestaand) en selecteren of schakel Hallo **Truncate tabel voor de import** selectievakje. Klik op **Volgende**.
4. Schakel codering en Hallo kolommen toobe geïmporteerd en klik vervolgens op **volgende**. 
5. Op Hallo **gegevens importeren** pagina, klikt u op **volgende**. Hallo wizard importeert gegevens Hallo dienovereenkomstig.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>SQL-gegevens exporteren en importeren van wizards in Hallo Navigator deelvenster
Gebruik een wizard tooexport of SQL gegenereerd op basis van MySQL Workbench of gegenereerd op basis van Hallo mysqldump opdracht importeren. Toegang tot deze wizards van Hallo **Navigator** deelvenster of door te selecteren **Server** vanuit het hoofdmenu Hallo. Selecteer vervolgens **gegevens exporteren** of **gegevensimport**. 

#### <a name="data-export"></a>Gegevens exporteren
![MySQL-Workbench gegevens exporteren met behulp van Hallo Navigator deelvenster](./media/concepts-migrate-import-export/p2.png)

U kunt Hallo **gegevens exporteren** tabblad tooexport uw MySQL-gegevens. 
1. Selecteer elke schema dat u tooexport wilt, eventueel Kies specifieke schema objecten/tabellen uit elke schema en Hallo export genereren. Configuratieopties export tooa projectmap of zelfstandige SQL-bestand opnemen, dump opgeslagen routines en gebeurtenissen of tabelgegevens overslaan. 
 
   U kunt ook gebruiken **exporteren resultaatset** tooexport een bepaald resultaat ingesteld in Hallo SQL editor tooanother-indeling, zoals CSV, JSON, HTML en XML. 
3. Selecteer Hallo database objecten tooexport en configureer Hallo gerelateerde opties.
4. Klik op **vernieuwen** tooload Hallo huidige objecten.
5. Open desgewenst Hallo **geavanceerde opties** toorefine Hallo exportbewerking tabblad. Bijvoorbeeld toevoegen tabel vergrendelingen, vervangen voor gebruik in plaats van insert-instructies en prijsopgave-id's met backtick tekens.
6. Klik op **Start exporteren** toobegin Hallo exportproces.


#### <a name="data-import"></a>Gegevens importeren
![MySQL-Workbench gegevens importeren met behulp van de Navigator Management](./media/concepts-migrate-import-export/p3.png)

U kunt Hallo **gegevensimport** tooimport tabblad of de geëxporteerde gegevens terugzetten vanuit Hallo gegevens exportbewerking of vanuit Hallo mysqldump opdracht. 
1. Kies Hallo projectmap of zelfstandige SQL-bestand, kies Hallo schema tooimport in of kies **nieuw** toodefine een nieuw schema. 
2. Klik op **Start importeren** toobegin Hallo importproces.

## <a name="next-steps"></a>Volgende stappen
Als een andere migratie benadering lezen [migreren uw MySQL-database met dump en MySQL in Azure-Database herstellen](concepts-migrate-dump-restore.md). 
