---
title: Voorbeelden van aaaAzure PowerShell-scripts voor SQL-Database | Microsoft Docs
description: Azure PowerShell-script voorbeelden toohelp maken en beheren van Azure SQL Database-servers, elastische pools, databases en firewalls.
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Voorbeelden van Azure PowerShell voor Azure SQL Database

Hallo volgende tabel bevat koppelingen toosample Azure PowerShell-scripts voor Azure SQL Database.

| |  |
|---|---|
|**Een individuele database en een elastische pool maken**||
| [Maken van een individuele database en een firewallregel configureren](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script één Azure SQL database maakt en configureert u een firewallregel op serverniveau. |
| [Maken van elastische pools en gegroepeerde databases verplaatsen](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script maakt Azure SQL Database elastische pools, gegroepeerde databases worden verplaatst en prestatieniveaus wordt gewijzigd.|
|**Geo-replicatie en failover configureren**||
| [Configureren en failover een individuele database met behulp van actieve geo-replicatie](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Deze PowerShell-script configureert actieve geo-replicatie voor een enkele Azure SQL database en failover toohello secundaire replica. |
| [Configureren en failover een gegroepeerde database met behulp van actieve geo-replicatie](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Dit PowerShell-script, configureert u het actieve geo-replicatie voor een Azure SQL database in een elastische SQL-groep en failover toohello secundaire replica. |
| [Configureren en failover een failover-groep voor één database (preview)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script configureert u een failover-groep voor een exemplaar van de Azure SQL Database-server, voegt u een database toohello failover-groep en failover toohello secundaire server |
|**De schaal van een individuele databases en een elastische pool**||
| [Een individuele database schalen](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script bewaakt Hallo maatstaven voor prestaties van een Azure SQL database, op schaal tooa hoger prestatieniveau en een waarschuwingsregel maakt op een van de maatstaven voor prestaties Hallo. |
| [Een elastische pool schalen](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Dit PowerShell-script Hallo maatstaven voor prestaties van een Azure SQL Database elastische pool bewaakt, op schaal tooa hoger prestatieniveau en een waarschuwingsregel maakt op een van de maatstaven voor prestaties Hallo.  |
| **Controle en detectie van bedreigingen** |
| [Controle en detectie van dreigingen configureren](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Deze PowerShell-script configureert controle en threat beleidsregels voor een Azure SQL database. |
| **Terugzetten, kopiëren en importeren van een database**||
| [Een database herstellen](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Deze PowerShell-script voor een Azure SQL database herstelt vanuit een geografisch redundante back-up en een verwijderde Azure SQL database toohello meest recente back-up hersteld. |
| [Een databaseserver toonew kopiëren](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Deze PowerShell-script maakt een kopie van een bestaande Azure SQL database in een nieuwe Azure SQL-server. |
| [Een database uit een Bacpac-bestand importeren](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Een database tooan Azure SQL-server importeert deze PowerShell-script uit een Bacpac-bestand. |
| **Gegevens tussen databases synchroniseren**||
| [Gegevens synchroniseren tussen de SQL-databases](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script configureert toosync synchroniseren van gegevens tussen meerdere Azure SQL-databases. |
| [Gegevens synchroniseren tussen on-premises SQL-Database en SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Deze PowerShell-script configureert toosync synchroniseren van gegevens tussen een Azure SQL database en een lokale SQL Server-database. |
|||
|||
