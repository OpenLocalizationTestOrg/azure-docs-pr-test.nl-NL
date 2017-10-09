---
title: aaaMove gegevens tooSQL Server op een virtuele machine in Azure | Microsoft Docs
description: Gegevens uit platte bestanden of van een lokale SQL Server tooSQL Server verplaatsen op de virtuele machine van Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Gegevens tooSQL Server op Azure een virtuele machine verplaatsen
In dit onderwerp bevat een overzicht van Hallo opties voor het verplaatsen van gegevens uit platte bestanden (TSV- of CSV-indeling) of van een lokale SQL Server tooSQL Server op Azure een virtuele machine. Deze taken voor zwevend gegevens toohello cloud maken deel uit van Hallo Team gegevens wetenschappelijke processen.

Zie voor in dit onderwerp bevat een overzicht van Hallo opties voor verplaatsen gegevens tooan Azure SQL Database voor Machine Learning, [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

Hallo **menu** hieronder koppelingen tootopics waarin wordt beschreven hoe gegevens in andere omgevingen doel waar Hallo gegevens kunnen worden opgeslagen en verwerkt tijdens tooingest Hallo Team gegevens wetenschap proces (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hallo volgende tabel ziet u Hallo opties voor verplaatsen gegevens tooSQL Server op Azure een virtuele machine.

| <b>BRON</b> | <b>BESTEMMING: SQL Server op Azure VM</b> |
| --- | --- |
| <b>Plat bestand</b> |1. <a href="#insert-tables-bcp">Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</a><br> 2. <a href="#insert-tables-bulkquery">Bulksgewijs invoegen SQL-Query</a><br> 3. <a href="#sql-builtin-utilities">Grafische ingebouwde hulpprogramma's in SQL Server</a> |
| <b>On-Premises SQL Server</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren</a><br> 2. <a href="#export-flat-file">Exporteren van tooa platte bestand</a><br> 3. <a href="#sql-migration">Wizard voor migratie van SQL-Database</a> <br> 4. <a href="#sql-backup">Back-up van database maken en terugzetten</a><br> |

Let op: dit document wordt ervan uitgegaan dat de SQL-opdrachten worden uitgevoerd vanuit SQL Server Management Studio of Visual Studio Database Explorer.

> [!TIP]
> Als alternatief kunt u [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate en plannen van een pijplijn die gegevens tooa SQL Server VM op Azure wordt verplaatst. Zie voor meer informatie [kopiëren van gegevens met Azure Data Factory (Kopieeractiviteit)](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Vereisten
Deze zelfstudie wordt ervan uitgegaan dat u hebt:

* Een **Azure-abonnement**. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* Een **Azure storage-account**. U wordt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel. Nadat u Hallo storage-account hebt gemaakt, moet u tooobtain Hallo account sleutel tooaccess Hallo opslagruimte hebt gebruikt. Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Ingericht **SQL Server op een virtuele machine van Azure**. Zie voor instructies [instellen van een virtuele machine van Azure SQL-Server als een server IPython Notebook voor geavanceerde analyses](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal. Zie voor instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Verplaatsen van gegevens uit een plat bestand bron tooSQL Server op een Azure VM
Als uw gegevens zich in een plat bestand (gerangschikt in een indeling rij/kolom), kan het verplaatste tooSQL Server VM op Azure via Hallo volgende methoden zijn:

1. [Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)](#insert-tables-bcp)
2. [Bulksgewijs invoegen SQL-Query](#insert-tables-bulkquery)
3. [Grafische ingebouwde hulpprogramma's in SQL Server (voor importeren/exporteren, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)
BCP is een opdrachtregelprogramma dat is geïnstalleerd met SQL Server en één Hallo snelste manieren toomove gegevens. Voor alle drie SQL Server varianten (On-premises SQL Server, SQL Azure en SQL Server VM op Azure) werkt.

> [!NOTE]
> **Waar moet mijn gegevens voor BCP**  
> Hoewel niet vereist dat bestanden die zich op dezelfde computer als Hallo doel-SQL-Server kunt u sneller overdrachten (netwerk snelheid tegenover lokale schijf i/o-snelheid) Hallo brongegevens bevat. U kunt verplaatsen Hallo platte bestanden met gegevens toohello machine waarop SQL Server is geïnstalleerd met behulp van verschillende kopiëren hulpprogramma's zoals [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Opslagverkenner](http://storageexplorer.com/) of windows kopiëren en plakken via Extern Desktop Protocol (RDP).
>
>

1. Zorg dat Hallo-database en Hallo tabellen zijn gemaakt op Hallo doel SQL Server-database. Hier volgt een voorbeeld van hoe toodo dat als u met Hallo `Create Database` en `Create Table` opdrachten:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Hallo indelingsbestand genereren die worden beschreven Hallo-schema voor Hallo tabel door uitgifte van de volgende opdracht uit vanaf de opdrachtregel van de machine Hallo HALLO hallo waarop bcp is geïnstalleerd.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Hallo gegevens invoegen in Hallo-database met behulp van de bcp-opdracht Hallo als volgt. Ervan uitgaande dat hello SQL Server is geïnstalleerd op dezelfde machine moet dit werkt van Hallo opdrachtregel:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **BCP wordt ingevoegd optimaliseren** Raadpleeg het volgende artikel Hallo ['Richtlijnen voor het optimaliseren van bulkimport'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize dergelijke wordt ingevoegd.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Voegt parallelizing voor snellere verplaatsing van gegevens
Als u overstapt Hallo-gegevens te groot is, kunt u dingen sneller maken door het gelijktijdig uitvoeren van meerdere BCP opdrachten parallel in een PowerShell-Script.

> [!NOTE]
> **BIG data opname** toooptimize gegevens laden voor grote en zeer grote gegevenssets, partitie-uw logische en fysieke databasetabellen met meerdere tabellen voor bestandsgroepen en partitie. Zie voor meer informatie over het maken en bij het laden van gegevenstabellen toopartition [parallelle Load SQL-partitietabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Hallo PowerShell-voorbeeldscript hieronder laten zien parallelle voegt met behulp van bcp:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Bulksgewijs invoegen SQL-Query
[Bulksgewijs invoegen SQL-Query](https://msdn.microsoft.com/library/ms188365) gebruikte tooimport gegevens in de database Hallo van rij/kolom op basis van bestanden kunnen worden (Hallo ondersteund typen worden behandeld in de[voorbereiden-gegevens voor bulksgewijs wilt exporteren naar of importeren (SQL Server)](https://msdn.microsoft.com/library/ms188609)) onderwerp.

Hier volgen enkele Voorbeeldopdrachten voor Bulk Insert zijn zoals hieronder:  

1. Uw gegevens analyseren en eventuele aangepaste opties instellen voordat u ervoor dat SQL Server-database hello wordt ervan uitgegaan dat dezelfde notatie voor de speciale velden zoals datums Hallo toomake importeert. Hier volgt een voorbeeld van hoe tooset Hallo datum opmaken als jaar, maand, dag (als uw gegevens bevat Hallo datum in de notatie voor jaar, maand, dag):

        SET DATEFORMAT ymd;    
2. Gegevens importeren met bulksgewijs importinstructies:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Ingebouwde hulpprogramma's in SQL Server
U kunt SQL Server integraties Services (SSIS) tooimport gegevens in SQL Server VM op Azure uit een plat bestand.
SSIS is beschikbaar in twee studio omgevingen. Zie voor meer informatie [Integration Services (SSIS) en Studio omgevingen](https://technet.microsoft.com/library/ms140028.aspx):

* Zie voor meer informatie over SQL Server Data Tools [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* Zie voor informatie over de Wizard importeren/exporteren hello, [Wizard SQL Server importeren en exporteren](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Verplaatsen van gegevens vanuit de lokale SQL Server tooSQL Server op een Azure VM
U kunt ook de volgende strategieën Hallo gebruiken:

1. [Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [TooFlat bestand exporteren](#export-flat-file)
3. [Wizard voor migratie van SQL-Database](#sql-migration)
4. [Back-up van database maken en terugzetten](#sql-backup)

We beschrijven elk van deze hieronder:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren
Hallo **implementeren van een Microsoft Azure VM-wizard van SQL Server-Database tooa** zijn de gegevens van een eenvoudige en de aanbevolen manier toomove van een lokale SQL Server-exemplaar tooSQL Server op een virtuele machine in Azure. Zie voor gedetailleerde stappen evenals een bespreking van de alternatieven, [migreren van een database tooSQL Server op een Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>TooFlat bestand exporteren
Verschillende methoden gebruikte toobulk het exporteren van gegevens uit een On-Premises SQL Server kunnen zijn, zoals beschreven in Hallo [bulksgewijs importeren en exporteren van gegevens (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) onderwerp. Dit document wordt uitgelegd hoe Hallo bulksgewijs kopiëren programma (BCP) als voorbeeld. Wanneer gegevens worden geëxporteerd naar een plat bestand, kan het geïmporteerde tooanother SQL server met behulp van bulkimport zijn.

1. Hallo gegevens exporteren uit de lokale SQL Server tooa bestand Hallo bcp hulpprogramma als volgt gebruiken

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Hallo-database en Hallo tabel maken op virtuele machine van SQL Server op Azure met behulp van Hallo `create database` en `create table` voor Hallo tabelschema in stap 1 hebt geëxporteerd.
3. Maak een indelingsbestand voor het beschrijven van het tabelschema Hallo Hallo-gegevens worden geëxporteerd/geïmporteerd. Details van het indelingsbestand Hallo worden beschreven in [maken van een indelingsbestand (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Indeling Bestandsgeneratie uitgevoerd BCP van Hallo wanneer SQL Server-computer

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Indeling van bestand genereren met het wanneer BCP op afstand uitvoeren in een SQL-Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Gebruik een van Hallo-methoden die zijn beschreven in de sectie [verplaatsen van gegevens van bestandsbron](#filesource_to_sqlonazurevm) toomove Hallo gegevens in platte bestanden tooa SQL Server.

### <a name="sql-migration"></a>Wizard voor migratie van SQL-Database
[SQL Server-Database Migration Wizard](http://sqlazuremw.codeplex.com/) biedt een gebruiksvriendelijke manier toomove gegevens tussen twee exemplaren van SQL server. Kunt u Hallo gebruiker toomap Hallo gegevensschema tussen bronnen en doeltabellen, kies kolomtypen en verschillende andere functionaliteiten. Bulksgewijs kopiëren (BCP) wordt gebruikt onder Hallo behandelt. Een schermopname van Hallo welkomstscherm voor Hallo SQL Database Migration wizard worden hieronder weergegeven.  

![Wizard SQL Server-migratie][2]

### <a name="sql-backup"></a>Back-up van database maken en terugzetten
SQL Server ondersteunt:

1. [Back-up van database en de functionaliteit herstellen](https://msdn.microsoft.com/library/ms187048.aspx) (zowel tooa lokale bestand of Bacpac-export tooblob) en [laag gegevenstoepassingen](https://msdn.microsoft.com/library/ee210546.aspx) (met behulp van bacpac).
2. Mogelijkheid toodirectly wordt SQL Server-VM's in Azure maken met een gekopieerde database of een kopie tooan bestaande Azure SQL database. Zie voor meer informatie [gebruik Hallo Database-Wizard kopiëren](https://msdn.microsoft.com/library/ms188664.aspx).

Een schermopname van Hallo Database back-up/terugzetten opties van SQL Server Management Studio wordt hieronder weergegeven.

![Hulpprogramma voor het SQL Server importeren][1]

## <a name="resources"></a>Resources
[Migreren van een Database tooSQL Server op een Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Overzicht van SQL Server op virtuele machines in Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
