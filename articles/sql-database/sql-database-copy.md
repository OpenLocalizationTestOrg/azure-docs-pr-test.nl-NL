---
title: een Azure SQL database aaaCopy | Microsoft Docs
description: Maak een kopie van een Azure SQL database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Een Azure SQL database kopiëren

Azure SQL Database biedt verschillende methoden voor het maken van een transactioneel consistent kopie van een bestaande Azure SQL database op beide Hallo dezelfde of een andere server. U kunt een SQL-database kopiëren via hello Azure-portal, PowerShell of T-SQL. 

## <a name="overview"></a>Overzicht

Een databasekopie is een momentopname van de brondatabase Hallo vanaf Hallo-tijd van Hallo copy-aanvraag. Kunt u dezelfde server of een andere server, de serviceniveau prijscategorie en prestatieniveau of een andere prestatieniveau binnen Hallo Hallo dezelfde servicelaag (editie). Nadat het Hallo-kopie is voltooid, wordt een volledig functionele, onafhankelijke database. U kunt op dit moment upgrade of downgrade voor tooany edition. Hallo-aanmeldingen, gebruikers en machtigingen kunnen afzonderlijk worden beheerd.  

## <a name="logins-in-hello-database-copy"></a>Aanmeldingen in Hallo databasekopie

Wanneer u een database toohello kopieert dezelfde logische server, Hallo dezelfde aanmeldingen op beide databases kunnen worden gebruikt. Hallo beveiligings-principal dat u toocopy Hallo database gebruiken eigenaar Hallo database op Hallo nieuwe database. Alle databasegebruikers en hun machtigingen hun beveiligings-id's (SID's) zijn gekopieerd toohello database-exemplaar.  

Wanneer u een database tooa andere logische server kopieert, eigenaar Hallo beveiligings-principal is op de nieuwe server Hallo Hallo database op Hallo nieuwe database. Als u [databasegebruikers opgenomen](sql-database-manage-logins.md) voor toegang tot gegevens, moet u zorgen dat beide Hallo primaire en secundaire databases altijd Hallo gebruikersreferenties hebben, zodat die nadat Hallo kopie is voltooid u onmiddellijk toegang tot deze met dezelfde Hallo de referenties. 

Als u [Azure Active Directory](../active-directory/active-directory-whatis.md), kunt u volledig Hallo nodig voor het beheren van referenties in Hallo kopie elimineren. Echter, wanneer u Hallo tooa nieuwe databaseserver kopieert, Hallo aanmelding gebaseerde toegang werkt mogelijk niet, omdat Hallo aanmeldingen niet bestaan op de nieuwe server Hallo. toolearn over het beheren van aanmeldingen bij het kopiëren van een database tooa andere logische server, Zie [hoe toomanage Azure SQL database-beveiliging na herstel na noodgevallen](sql-database-geo-replication-security-config.md). 

Nadat Hallo kopiëren is geslaagd en voordat andere gebruikers worden toegewezen, alleen hello aanmelding die geïnitieerd Hallo kopiëren, Hallo-database-eigenaar kan zich aanmelden in de nieuwe database toohello. tooresolve aanmeldingen nadat Hallo kopiëren van de bewerking is voltooid, Zie [aanmeldingen oplossen](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Kopiëren van een database met behulp van hello Azure-portal

toocopy een database met behulp van hello Azure-portal openen Hallo-pagina voor uw database en klik vervolgens op **kopie**. 

   ![Database-exemplaar](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Een database met behulp van PowerShell kopiëren

een database met behulp van PowerShell, gebruik Hallo toocopy [nieuw AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Zie voor een volledige voorbeeldscript [kopiëren van een nieuwe databaseserver voor tooa](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Kopiëren van een database met behulp van Transact-SQL

Meld u bij toohello master database met Hallo principal-aanmelding op serverniveau of Hallo-aanmelding die u wilt dat toocopy Hallo-database is gemaakt. Voor de database kopiëren toosucceed, moeten aanmeldingen die geen Hallo niveau van de server principal lid zijn van Hallo dbmanager rol. Zie voor meer informatie over aanmeldingen en aangesloten toohello server [aanmeldingen beheren](sql-database-manage-logins.md).

Beginnen met het kopiëren van de brondatabase Hallo Hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instructie. Deze instructie uitvoert initieert Hallo-database kopiëren proces. Omdat het kopiëren van een database een asynchrone is, retourneert Hallo instructie CREATE DATABASE voordat het Hallo-database kopiëren is voltooid.

### <a name="copy-a-sql-database-toohello-same-server"></a>Kopiëren van een SQL-database toohello dezelfde server
Meld u bij toohello master database met Hallo principal-aanmelding op serverniveau of Hallo-aanmelding die u wilt dat toocopy Hallo-database is gemaakt. Voor de database kopiëren toosucceed, moeten aanmeldingen die geen Hallo niveau van de server principal lid zijn van Hallo dbmanager rol.

Met deze opdracht kopieert Database1 tooa nieuwe database met de naam Database2 op Hallo dezelfde server. Afhankelijk van de grootte van de Hallo van uw database, kan Hallo kopiëren bewerking sommige toocomplete tijd duren.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Kopiëren van een andere server van SQL database tooa

Meld u bij toohello master database van Hallo-doelserver Hallo SQL database-server waar de nieuwe database Hallo toobe gemaakt is. Gebruik een aanmelding die heeft dezelfde gebruikersnaam en wachtwoord Hallo als Hallo database-eigenaar van de brondatabase Hallo op Hallo bron SQL database-server. Hallo-aanmelding op de doelserver Hallo moet ook lid zijn van Hallo dbmanager rol zijn of Hallo principal-aanmelding op serverniveau.

Met deze opdracht exemplaren Database1 op server1 tooa nieuwe database met de naam Database2 op server2. Afhankelijk van de grootte van de Hallo van uw database, kan Hallo kopiëren bewerking sommige toocomplete tijd duren.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Voortgang van Hallo Hallo bewerking kopiëren

Hallo kopiëren proces bewaken door het uitvoeren van query's Hallo sys.databases en sys.dm_database_copies weergaven. Tijdens het kopiëren van Hallo wordt uitgevoerd, Hallo **state_desc** kolom Hallo sys.databases weergave voor de nieuwe database hello te is ingesteld**kopiëren**.

* Als Hallo kopiëren is mislukt, Hallo **state_desc** kolom Hallo sys.databases weergave voor de nieuwe database hello te is ingesteld**VERMOEDT**. Hallo DROP-instructie niet uitvoeren op Hallo nieuwe database en probeer het later opnieuw.
* Als Hallo kopiëren is gelukt, hello **state_desc** kolom Hallo sys.databases weergave voor de nieuwe database hello te is ingesteld**ONLINE**. Hallo kopiëren is voltooid en de nieuwe database Hallo is gewone databases die onafhankelijk van de brondatabase Hallo kan worden gewijzigd.

> [!NOTE]
> Als u toocancel Hallo kopiëren besluit terwijl deze uitgevoerd wordt, uitvoeren Hallo [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) instructie op Hallo nieuwe database. U kunt ook de instructie DROP DATABASE Hallo worden uitgevoerd op de brondatabase Hallo ook wordt geannuleerd Hallo proces kopiëren.
> 

## <a name="resolve-logins"></a>Aanmeldingen oplossen

Nadat de nieuwe database Hallo online op de doelserver hello is, gebruik Hallo [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) instructie tooremap Hallo gebruikers van Hallo toologins op de doelserver Hallo nieuwe database. tooresolve zwevende gebruikers, Zie [zwevende gebruikers dat problemen met](https://msdn.microsoft.com/library/ms175475.aspx). Zie ook [hoe toomanage Azure SQL database-beveiliging na herstel na noodgevallen](sql-database-geo-replication-security-config.md).

Alle gebruikers in de nieuwe database Hallo behouden Hallo machtigingen die ze hebben als in de brondatabase Hallo. Hallo-gebruiker die heeft gestart databasekopie Hallo Hallo database-eigenaar van de nieuwe database Hallo en een nieuwe beveiligings-id (SID) is toegewezen. Nadat Hallo kopiëren is geslaagd en voordat andere gebruikers worden toegewezen, alleen hello aanmelding die geïnitieerd Hallo kopiëren, Hallo-database-eigenaar kan zich aanmelden in de nieuwe database toohello.

toolearn over het beheren van gebruikers en aanmeldingen bij het kopiëren van een database tooa andere logische server, Zie [hoe toomanage Azure SQL database-beveiliging na herstel na noodgevallen](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over aanmeldingen [aanmeldingen beheren](sql-database-manage-logins.md) en [hoe toomanage Azure SQL database-beveiliging na herstel na noodgevallen](sql-database-geo-replication-security-config.md).
* een database tooexport Zie [exporteren Hallo database tooa Bacpac-](sql-database-export.md).
