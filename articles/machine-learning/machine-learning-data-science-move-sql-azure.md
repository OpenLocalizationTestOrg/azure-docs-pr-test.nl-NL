---
title: aaaMove gegevens tooan Azure SQL Database voor Azure Machine Learning | Microsoft Docs
description: SQL-tabel maken en te laden van gegevens tooSQL tabel
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning
In dit onderwerp bevat een overzicht van Hallo opties voor het verplaatsen van gegevens uit platte bestanden (TSV- of CSV-indeling) of van de gegevens die zijn opgeslagen in een lokale SQL Server tooan Azure SQL database. Deze taken voor zwevend gegevens toohello cloud maken deel uit van Hallo Team gegevens wetenschappelijke processen.

Zie voor in dit onderwerp bevat een overzicht van Hallo opties voor verplaatsen gegevens tooan on-premises SQL Server voor Machine Learning, [gegevens tooSQL Server op Azure een virtuele machine verplaatsen](machine-learning-data-science-move-sql-server-virtual-machine.md).

Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe tooingest gegevens in de doel-omgevingen waar Hallo gegevens kunnen worden opgeslagen en verwerkt tijdens Hallo Team gegevens wetenschap proces (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hallo volgende tabel ziet u Hallo opties voor verplaatsen gegevens tooan Azure SQL Database.

| <b>BRON</b> | <b>BESTEMMING: Azure SQL Database</b> |
| --- | --- |
| <b>Plat bestand (CSV- of geformatteerd TSV)</b> |<a href="#bulk-insert-sql-query">Bulksgewijs invoegen SQL-Query |
| <b>On-premises SQL Server</b> |1. <a href="#export-flat-file">TooFlat bestand exporteren<br> 2. <a href="#insert-tables-bcp">Wizard voor migratie van SQL-Database<br> 3. <a href="#db-migration">Back-up van database maken en terugzetten<br> 4. <a href="#adf">Azure Data Factory |

## <a name="prereqs"></a>Vereisten
Hallo-procedures die hier wordt beschreven, vereisen dat u hebt:

* Een **Azure-abonnement**. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* Een **Azure storage-account**. U kunt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel. Nadat u Hallo storage-account hebt gemaakt, moet u tooobtain Hallo account sleutel tooaccess Hallo opslagruimte hebt gebruikt. Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Toegang tooan **Azure SQL Database**. Als u een Azure SQL-Database moet ingesteld [aan de slag met Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md) bevat informatie over het tooprovision een nieuw exemplaar van een Azure SQL Database.
* Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal. Zie voor instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

**Gegevens**: Hallo migratie processen worden gedemonstreerd met behulp van Hallo [NYC Taxi gegevensset](http://chriswhong.com/open-data/foil_nyc_taxi/). Hallo NYC Taxi gegevensset bevat informatie over reis gegevens en beurzen en is beschikbaar op Azure blob-opslag: [NYC Taxi gegevens](http://www.andresmh.com/nyctaxitrips/). Een beschrijving van deze bestanden en voorbeelden vindt u in [NYC Taxi reizen gegevensset beschrijving](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Hallo procedures beschreven hier tooa set van uw eigen gegevens aanpassen of Hallo stappen zoals beschreven met behulp van Hallo NYC Taxi gegevensset. tooupload hello NYC Taxi gegevensset in uw lokale SQL Server-database, volgt u Hallo procedure beschreven in [gegevens voor bulksgewijs importeren in SQL Server-Database](machine-learning-data-science-process-sql-walkthrough.md#dbload). Deze instructies zijn voor een SQL-Server op een virtuele Machine van Azure, maar de procedure voor het uploaden van de lokale SQL Server is toohello Hallo Hallo dezelfde.

## <a name="file-to-azure-sql-database"></a>Verplaatsen van gegevens uit een plat bestand bron tooan Azure SQL database
Gegevens in platte bestanden (CSV-bestand of TSV geformatteerd) kunnen worden verplaatst tooan Azure SQL database met behulp van een Bulk Insert SQL-Query.

### <a name="bulk-insert-sql-query"></a>Bulksgewijs invoegen SQL-Query
Hallo stappen Hallo regeling Hallo Bulk Insert SQL-Query zijn vergelijkbaar toothose in Hallo secties voor het verplaatsen van gegevens uit een plat bestand bron tooSQL Server op een Azure VM besproken. Zie voor meer informatie [Bulk Insert SQL-Query](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Verplaatsen van gegevens vanuit de lokale SQL Server tooan Azure SQL database.
Als de brongegevens Hallo is opgeslagen in een lokale SQL Server, zijn er verschillende mogelijkheden voor Azure SQL-database verplaatsen Hallo-tooan voor gegevens:

1. [TooFlat bestand exporteren](#export-flat-file)
2. [Wizard voor migratie van SQL-Database](#insert-tables-bcp)
3. [Back-up van database maken en terugzetten](#db-migration)
4. [Azure Data Factory](#adf)

Hallo stappen voor het eerste drie Hallo zijn vergelijkbaar toothose secties in [gegevens tooSQL Server op Azure een virtuele machine verplaatsen](machine-learning-data-science-move-sql-server-virtual-machine.md) dat deze dezelfde procedures beslaan. Koppelingen toohello toepasselijke rubrieken in dit onderwerp vindt u in Hallo instructies te volgen.

### <a name="export-flat-file"></a>TooFlat bestand exporteren
Hallo-stappen voor deze uitvoer tooa plat bestand zijn vergelijkbaar toothose behandeld in [tooFlat bestand exporteren](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Wizard voor migratie van SQL-Database
Hallo stappen voor het gebruik van SQL Database Migration Wizard Hallo zijn vergelijkbaar toothose behandeld in [SQL Database Migration Wizard](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Back-up van database maken en terugzetten
Hallo-stappen voor het gebruik van de database back-up en herstel zijn vergelijkbaar toothose behandeld in [Database back-en herstel](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Azure Data Factory
Hallo-procedure voor het verplaatsen gegevens tooan Azure SQL database met Azure Data Factory (ADF) vindt u in Hallo onderwerp [verplaatsen van gegevens uit een lokale SQL server tooSQL Azure met Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md). Dit onderwerp wordt beschreven hoe toomove gegevens uit een lokale SQL Server-database tooan Azure SQL database via Azure Blob Storage met ADF.

Overweeg het gebruik van ADF wanneer gegevens behoeften toobe voortdurend gemigreerd in een hybride scenario die toegang heeft tot zowel on-premises en cloudresources en wanneer Hallo gegevens transactionele is of moet toobe gewijzigd of hebben zakelijke logica toegevoegd tooit wanneer wordt gemigreerd. ADF kunt Hallo planning en bewaking van taken met behulp van eenvoudige JSON-scripts die Hallo verplaatsing van gegevens op periodieke basis beheren. ADF heeft ook andere mogelijkheden, zoals ondersteuning voor complexe bewerkingen.
