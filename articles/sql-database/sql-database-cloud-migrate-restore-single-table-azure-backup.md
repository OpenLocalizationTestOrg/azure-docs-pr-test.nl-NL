---
title: "aaaRestore één tabel vanuit back-up van Azure SQL Database | Microsoft Docs"
description: "Meer informatie over hoe toorestore één tabel vanuit Azure SQL Database back-up."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Hoe toorestore één tabel uit een back-up van Azure SQL Database
Een situatie waarin u sommige gegevens in een SQL-database per ongeluk hebt gewijzigd kunnen optreden en nu het gewenste toorecover Hallo één betrokken tabel. Dit artikel wordt beschreven hoe toorestore één tabel in een database van een SQL-Database Hallo [automatische back-ups](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Voorbereidende stappen: naam van de tabel Hallo en herstelt een kopie van het Hallo-database
1. Hallo-tabel in uw Azure SQL-database die u wilt dat tooreplace Hallo hersteld exemplaar identificeren. Microsoft SQL Management Studio toorename Hallo tabel gebruiken. Wijzig bijvoorbeeld Hallo tabel als &lt;tabelnaam&gt;_old.
   
   > [!NOTE]
   > tooavoid wordt geblokkeerd, zorg ervoor dat er geen activiteit uitgevoerd op Hallo-tabel die u de naam wijzigt. Als u problemen ondervindt, ervoor zorgen dat deze procedure uitvoeren tijdens een onderhoudsvenster.
   >

2. Herstellen van een back-up van uw database tooa punt in tijd dat u toorecover toousing hello wilt [Point-In_Time herstellen](sql-database-recovery-using-backups.md#point-in-time-restore) stappen.
   
   > [!NOTE]
   > Hallo-naam van de database hersteld Hallo is in Hallo DBName + tijdstempelnotatie; bijvoorbeeld: **Adventureworks2012_2016 01-01T22 12Z**. Deze stap overschreven niet Hallo bestaande databasenaam op Hallo server. Dit is een veiligheidsmaatregel, en het bedoeld tooallow u tooverify Hallo database teruggezet voordat ze hun huidige database verwijderen en wijzig de naam van de database hersteld Hallo voor gebruik in productieomgevingen.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Kopiëren Hallo tabel uit Hallo database teruggezet met behulp van Hallo-hulpprogramma voor migratie van de SQL-Database

1. Download en installeer Hallo [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).
2. Open Hallo SQL Database Migration Wizard op Hallo **Selecteer proces** pagina **Database onder analyseren/migreren**, en klik vervolgens op **volgende**.

   ![Migratie van de SQL-Database-wizard - proces selecteren](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. In Hallo **tooServer verbinding** dialoogvenster vak, Hallo instellingen volgende van toepassing:

   * Servernaam: **uw SQL server**
   * Verificatie: **SQL Server-verificatie**
   * Aanmelding: **uw aanmelding**
   * Wachtwoord: **uw wachtwoord**
   * Database: **Master DB (alle databases vermelden)**
   
   > [!NOTE]
   > Standaard slaat de wizard Hallo uw aanmeldingsgegevens. Als u niet wilt dat deze is, selecteert u **aanmeldingsgegevens vergeet**.
   >
   
     ![Migratie van de SQL-Database-wizard - bron selecteren - stap 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. In Hallo **bron selecteren** dialoogvenster, selecteer Hallo hersteld databasenaam van Hallo **voorbereidingsstappen** sectie als de bron en klik vervolgens op **volgende**.
   
    ![Migratie van de SQL-Database-wizard - bron selecteren - stap 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. In Hallo **objecten kiezen** dialoogvenster, selecteer Hallo **specifieke databaseobjecten selecteren** optie en selecteer vervolgens Hallo table(or tables) gewenste toomigrate toohello-doelserver.
   ![Migratie van de SQL-Database-wizard - objecten kiezen](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Op Hallo **overzicht van de Wizard Script** pagina, klikt u op **Ja** wanneer u wordt gevraagd over u klaar toogenerate een SQL-script bent. U hebt ook Hallo optie toosave Hallo TSQL-Script voor later gebruik.
   ![Migratie van de SQL-Database-wizard - samenvatting van de Wizard Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Op Hallo **samenvatting van de resultaten** pagina, klikt u op **volgende**.
   ![Migratie van de SQL-Database-wizard - overzicht](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Op Hallo **Target Server-verbinding instellen** pagina, klikt u op **tooServer verbinding**, en voer vervolgens Hallo details:
   
   * **Servernaam**: Target server-exemplaar
   * **Verificatie**: **SQL Server-verificatie**. Voer uw aanmeldingsreferenties.
   * **Database**: **Master DB (alle databases vermelden)**. Deze optie geeft een lijst van alle Hallo-databases op Hallo-doelserver.
     
     ![Migratie van de SQL-Database-wizard - doel Server-verbinding instellen](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Klik op **Connect**, selecteer Hallo doeldatabase die u wilt toomove Hallo tabel en klik vervolgens op **volgende**. Dit moet voltooien Hallo eerder gegenereerde script wordt uitgevoerd en ziet u Hallo zojuist gekopieerde toohello-doeldatabase tabel verplaatst.

## <a name="verification-step"></a>Verificatiestap

- Query's en test Hallo gekopieerd zojuist tabel toomake Hallo gegevens is beschadigd. Na bevestiging verwijderen Hallo hernoemd formulier **voorbereidende stappen** sectie. (bijvoorbeeld &lt;tabelnaam&gt;_old).

## <a name="next-steps"></a>Volgende stappen
[Automatische back-ups van SQL-Database](sql-database-automated-backups.md)

