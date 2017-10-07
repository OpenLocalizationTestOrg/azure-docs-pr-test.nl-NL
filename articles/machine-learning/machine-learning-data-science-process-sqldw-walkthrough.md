---
title: 'Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse | Microsoft Docs'
description: Geavanceerde analyses proces en de technologie in actie
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse
In deze zelfstudie wordt beschreven hoe u maken en implementeren van een machine learning-model met behulp van SQL Data Warehouse (SQL DW) voor een openbaar dataset--hello [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset. Hallo binaire classificatie model samengesteld voorspelt al dan niet een tip voor een reis is betaald, en modellen voor multiklassen classificatie en regressie worden ook besproken die Hallo distributie voor betaalde Hallo tip bedragen voorspellen.

Hallo procedure volgt Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) werkstroom. Laten we zien hoe een wetenschappelijke gegevensomgeving toosetup hoe tooload gegevens in SQL DW Hallo en hoe SQL DW of Hallo een tooexplore IPython Notebook gegevens en engineer u het toomodel functies gebruiken. Vervolgens wordt gedemonstreerd hoe toobuild en implementeren van een model met Azure Machine Learning.

## <a name="dataset"></a>Hallo NYC Taxi reizen gegevensset
Hallo NYC Taxi reis gegevens bestaat uit ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), opnemen van meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald. Elke record reis omvat Hallo ophalen en inleverbibliotheek locaties en tijden, geanonimiseerde inbreken licentienummer (stuurprogramma van) en Hallo nummer straten (taxi van unieke id). Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:

1. Hallo **trip_data.csv** bestand reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis bevat. Hier volgen enkele voorbeeldrecords:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hallo **trip_fare.csv** bestand bevat de details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald. Hier volgen enkele voorbeeldrecords:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hallo **unieke sleutel** toojoin reis gebruikt\_gegevens en reis\_tarief bestaat uit de volgende drie velden Hallo:

* straten,
* inbreken\_licentie en
* ophalen\_datetime.

## <a name="mltasks"></a>Adres van de drie typen taken voorspelling
We drie voorspelling problemen op basis van Hallo formuleren *tip\_bedrag* tooillustrate drie soorten taken modelleren:

1. **Binaire classificatie**: toopredict al dan niet een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.
2. **Multiklassen classificatie**: toopredict Hallo bereik van een tip voor Hallo reis betaald. We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.  

## <a name="setup"></a>Hello Azure gegevens wetenschappelijke omgeving voor geavanceerde analyses instellen
tooset van uw omgeving Gegevenswetenschap Azure als volgt te werk.

**Uw eigen Azure blob storage-account maken**

* Wanneer u uw eigen Azure-blobopslag inricht, kiest u een geografische locatie voor uw Azure blob storage in of zo dicht mogelijk te**Zuid-centraal VS**, dit is waar Hallo NYC Taxi gegevens wordt opgeslagen. Hallo-gegevens worden gekopieerd met behulp van AzCopy van Hallo openbare blob storage-container tooa container in uw eigen opslagaccount. Hallo dichter bij de Azure blob-opslag is tooSouth VS-midden, hello sneller (stap 4) van deze taak wordt voltooid.
* toocreate account van uw eigen Azure-opslag, volg Hallo stappen die worden beschreven op [over Azure storage-accounts](../storage/common/storage-create-storage-account.md). Niet zeker toomake opmerkingen over Hallo waarden voor de volgende opslagaccountreferenties als ze later in dit scenario worden vereist.
  
  * **Naam van het opslagaccount**
  * **De sleutel van opslagaccount**
  * **Containernaam** (die u wilt dat Hallo gegevens toobe opgeslagen in hello Azure blob-opslag)

**Inrichten van uw Azure SQL DW-exemplaar.**
Ga als volgt Hallo-documentatie op [maken van een SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision een exemplaar van SQL Data Warehouse. Zorg ervoor dat u notaties op Hallo SQL Data Warehouse-referenties die worden gebruikt in latere stappen te volgen.

* **Servernaam**: <server Name>. database.windows.net
* **De naam van de SQLDW (Database)**
* **Gebruikersnaam**
* **Wachtwoord**

**Installeer Visual Studio en SQL Server Data Tools.** Zie voor instructies [Visual Studio 2015 installeren en/of SSDT (SQL Server Data Tools) voor SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Verbinding maken met Azure SQL DW tooyour met Visual Studio.** Voor instructies raadpleegt u de stappen 1 en 2 in [tooAzure SQL Data Warehouse met Visual Studio verbinding](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Voer hello volgende SQL-query op database Hallo u hebt gemaakt in uw SQL Data Warehouse (verbinding maken onderwerp, in plaats van Hallo query is opgegeven in stap 3 van Hallo) te**een hoofdsleutel**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Een Azure Machine Learning-werkruimte onder uw Azure-abonnement maken.** Zie voor instructies [maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).

## <a name="getdata"></a>Hallo gegevens laden in SQL Data Warehouse
Open een Windows PowerShell-opdracht-console. Voer de volgende Hallo PowerShell-opdrachten toodownload Hallo voorbeeld SQL scriptbestanden die we delen met u op GitHub tooa lokale map die u met de parameter Hallo opgeeft *- DestDir*. U kunt wijzigen Hallo-waarde van parameter *- DestDir* tooany lokale map. Als *- DestDir* niet bestaat, wordt deze gemaakt door Hallo PowerShell-script.

> [!NOTE]
> U moet mogelijk te**als Administrator uitvoeren** bij het uitvoeren van de volgende PowerShell-script op als Hallo uw *DestDir* directory moet Administrator-bevoegdheden toocreate of toowrite-tooit.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Na voltooiing van uitvoering, verandert de huidige werkmap te*- DestDir*. U moet kunnen toosee scherm zoals hieronder:

![][19]

In uw *- DestDir*, Hallo volgen in de beheerdersmodus een PowerShell-script uitvoeren:

    ./SQLDW_Data_Import.ps1

Wanneer Hallo PowerShell-script wordt uitgevoerd voor Hallo eerst, u gevraagd tooinput Hallo informatie van uw Azure SQL DW en uw Azure blob storage-account. Wanneer dit PowerShell-script is voltooid wordt met voor Hallo eerst Hallo referenties u invoer zijn geschreven configuratiebestand tooa SQLDW.conf in de huidige werkmap Hallo. Hallo heeft toekomstige uitvoering van dit bestand PowerShell-script Hallo optie tooread alle benodigde parameters van dit configuratiebestand. Als u nodig hebt toochange sommige parameters, kunt u kiezen tooinput Hallo parameters op het welkomstscherm bij de prompt door dit configuratiebestand verwijderen en het invoeren van parameterwaarden Hallo wanneer daarom wordt gevraagd of toochange Hallo parameterwaarden door Hallo SQLDW.conf bestand te bewerken in uw *- DestDir* directory.

> [!NOTE]
> In de volgorde tooavoid schema naam een conflict veroorzaakt met degenen die al aanwezig zijn in uw Azure SQL DW bij het lezen van parameters rechtstreeks van Hallo SQLDW.conf bestand, wordt een willekeurig getal 3-cijferige uit Hallo SQLDW.conf bestand toohello schemanaam toegevoegd als Hallo standaardnaam schema voor elke uitvoering. Hallo PowerShell-script wordt u mogelijk gevraagd voor de naam van een schema: gebruiker goeddunken Hallo naam worden opgegeven.
> 
> 

Dit **PowerShell-script** bestand is voltooid Hallo taken te volgen:

* **Downloadt en installeert AzCopy**als AzCopy nog niet is geïnstalleerd
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Kopieert de gegevens tooyour persoonlijke blob storage-account** van een openbare blob met AzCopy Hallo
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Laden van gegevens met Polybase (door het uitvoeren van LoadDataToSQLDW.sql) tooyour Azure SQL DW** van uw persoonlijke blob storage-account met de volgende opdrachten Hallo.
  
  * Een schema maken
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Een-scoped databasereferentie maken
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Maken van een externe gegevensbron voor een Azure storage-blob
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Maak een externe bestandsindeling voor een csv-bestand. Gegevens zijn niet-gecomprimeerde en velden worden gescheiden met het sluisteken Hallo.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Externe tarief en tabellen voor NYC taxi gegevensset reis maken in Azure blob-opslag.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Gegevens uit externe tabellen in Azure blob storage tooSQL Data Warehouse laden

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Maken van een gegevenstabel voorbeeld (NYCTaxi_Sample) en gegevens tooit invoegen van het SQL-query's op Hallo reis en tarief tabellen selecteren. (Een aantal stappen van dit scenario moet toouse deze voorbeeldtabel.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

laadtijden van invloed op Hallo geografische locatie van uw storage-accounts.

> [!NOTE]
> Afhankelijk van Hallo geografische locatie van uw persoonlijke blob storage-account, Hallo-proces voor het kopiëren van gegevens uit een openbare blob tooyour persoonlijke storage-account kan ongeveer 15 minuten duren, of zelfs meer en hello verwerken van het laden van gegevens uit uw storage-account Azure SQL DW tooyour kan duurt ongeveer 20 minuten of langer.  
> 
> 

Hebt u toodecide wat doen als er dubbele bron en doel-bestanden.

> [!NOTE]
> Als Hallo .csv-bestanden toobe gekopieerd van Hallo openbare blob-opslag tooyour persoonlijke blob storage-account al in uw persoonlijke blob storage-account bestaat, AzCopy u wordt gevraagd of u wilt dat toooverwrite ze. Als u niet dat toooverwrite ze, invoer wilt  **n**  wanneer u wordt gevraagd. Als u wilt dat toooverwrite **alle** , invoer **een** wanneer u wordt gevraagd. U kunt ook invoer **y** afzonderlijk toooverwrite .csv-bestanden.
> 
> 

![#21 tekenen][21]

U kunt uw eigen gegevens. Als uw gegevens in uw on-premises machine in uw toepassing praktijk is, kunt u nog steeds AzCopy tooupload lokale gegevens tooyour persoonlijke Azure-blobopslag. U hoeft alleen toochange hello **bron** locatie, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in Hallo AzCopy-opdracht van Hallo PowerShell script bestand toohello lokale map met uw gegevens.

> [!TIP]
> Als uw gegevens zich al in uw persoonlijke Azure blob-opslag in uw toepassing praktijk, kunt u Hallo AzCopy stap in Hallo PowerShell-script en Hallo gegevens tooAzure SQL DW rechtstreeks te uploaden overslaan. Hiervoor moet extra bewerkt van Hallo script tootailor toohello indeling van uw gegevens.
> 
> 

Deze Powershell-script ook aangesloten in hello Azure SQL DW-informatie naar Hallo exploratie voorbeeld gegevensbestanden SQLDW_Explorations.sql, SQLDW_Explorations.ipynb en SQLDW_Explorations_Scripts.py zodat deze drie bestanden gereed toobe geprobeerd onmiddellijk uit Nadat de Hallo PowerShell-script is voltooid.

Na een geslaagde uitvoering, ziet u scherm, zoals hieronder:

![][20]

## <a name="dbexplore"></a>Gegevensverkenning en functie-engineering in Azure SQL Data Warehouse
In deze sectie we gegevens te verkennen en functie generatie uitvoeren door met het SQL-query's uitvoeren in Azure SQL DW direct met **Visual Studio Data Tools**. Alle SQL-query's gebruikt in deze sectie vindt u in Hallo voorbeeld van een script met de naam *SQLDW_Explorations.sql*. Dit bestand is al gedownload tooyour lokale directory door Hallo PowerShell-script. U kunt ook ophalen via [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Maar Hallo-bestand in GitHub heeft geen hello Azure SQL DW-informatie is aangesloten.

Verbinding maken met Visual Studio Hallo SQL DW-aanmeldingsnaam en wachtwoord van Azure SQL DW tooyour en geopend Hallo **SQL Object Explorer** tooconfirm Hallo database en tabellen zijn geïmporteerd. Hallo ophalen *SQLDW_Explorations.sql* bestand.

> [!NOTE]
> tooopen een Parallel Data Warehouse (PDW) query-editor gebruiken Hallo **nieuwe Query** opdracht terwijl uw PDW is geselecteerd in Hallo **SQL Object Explorer**. Hallo standaard de SQL-query-editor wordt niet ondersteund door PDW.
> 
> 

Hier volgen Hallo type gegevens te verkennen en functie generatie uitgevoerd in deze sectie:

* Verken de gegevens distributies van enkele velden in verschillende tijdvensters.
* Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.
* Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.
* Genereren van functies en reis afstanden compute/vergelijken.
* Hallo twee tabellen samenvoegen en uitpakken van een steekproef die gebruikt toobuild modellen worden.

### <a name="data-import-verification"></a>Gegevens importeren verificatie
Deze query's bieden een snelle Hallo aantal rijen en kolommen in tabellen ingevuld met oudere versies van Polybase parallelle bulksgewijs importeert, Hallo-verificatie

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Uitvoer:** krijgt u 173,179,759 rijen en 14 kolommen.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploratie: Reis distributie door straten
Deze voorbeeldquery identificeert Hallo medallions (taxi getallen) die meer dan 100 reizen voltooid binnen een opgegeven periode. Hallo query wilt profiteren van Hallo gepartitioneerde tabeltoegang omdat deze wordt waarbij door Hallo partitieschema van **ophalen\_datetime**. Opvragen van de volledige gegevensset Hallo maakt ook gebruik van de gepartitioneerde tabel Hallo en/of index van de scan.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Uitvoer:** Hallo query moet een tabel met rijen geven Hallo 13,369 medallions (taxi's) worden geretourneerd en Hallo aantal reis voltooid door ze in 2013. de laatste kolom Hallo bevat Hallo aantal Hallo reizen voltooid.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploratie: Reis distributie door straten en hack_license
In dit voorbeeld identificeert Hallo medallions (taxi getallen) en hack_license getallen (stuurprogramma's) die voltooid zijn meer dan 100 reizen binnen een opgegeven periode.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Uitvoer:** Hallo query als resultaat moet een tabel met 13,369 rijen Hallo 13,369 auto stuurprogramma-id's die u meer die 100 reizen in 2013 hebt opgeven. de laatste kolom Hallo bevat Hallo aantal Hallo reizen voltooid.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Gegevens beoordeling: Controleer of records met onjuiste lengtegraad en/of breedtegraad
In dit voorbeeld onderzoekt als Hallo lengtegraad en/of breedtegraad velden een ongeldige waarde bevatten (radiaal graden moet tussen-90 en 90), of (0, 0) coördinaten.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Uitvoer:** Hallo query retourneert 837,467 reizen die ongeldige lengtegraad en/of breedtegraad velden hebben.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploratie: Punt versus niet Gekantelde reizen distributie
Dit voorbeeld wordt gezocht naar Hallo aantal reizen versus Hallo nummer zijn punt wanneer geen punt zijn in een opgegeven periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar als u deze hier is ingesteld). Deze verdeling weerspiegelt Hallo binaire label distributie toobe later gebruikt voor het modelleren van de binaire indeling.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Uitvoer:** Hallo query moet return Hallo volgende frequenties tip voor Hallo jaar 2013: 90,447,622 punt en 82,264,709 niet punt.

### <a name="exploration-tip-classrange-distribution"></a>Exploratie: Verdeling Tip klasse/bereik
In dit voorbeeld berekent Hallo distributie van tip bereiken in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar). Dit is distributiepunt Hallo Hallo label klassen die later wordt gebruikt voor multiklassen classificatie modellering.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Uitvoer:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Exploratie: Berekenen en reis afstand vergelijken
In dit voorbeeld Hallo ophalen en inleverbibliotheek lengtegraad converteert en breedtegraad tooSQL Geografie verwijst, Hallo reis afstand met behulp van SQL Geografie punten verschil wordt berekend en retourneert een willekeurig aantal Hallo resultaten voor vergelijking. Hallo voorbeeld beperkt Hallo resultaten toovalid coördineert alleen met behulp van Hallo kwaliteit assessment gegevensquery eerder besproken.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Functie-engineering met behulp van SQL-functies
SQL-functies kunnen soms een efficiënte optie voor functie-engineering zijn. In dit overzicht hebben we een SQL functie toocalculate Hallo direct afstand tussen Hallo ophalen en dropoff locaties gedefinieerd. U kunt uitvoeren Hallo volgende SQL-scripts in **Visual Studio Data Tools**.

Hier volgt Hallo SQL-script waarmee wordt gedefinieerd Hallo afstand-functie.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Hier volgt een voorbeeld toocall deze functie toogenerate functies in uw SQL-query:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Uitvoer:** deze query wordt een tabel (met 2,803,538 rijen) gegenereerd met ophalen en dropoff Latitude en lengten en de bijbehorende van Hallo directe afstanden in mijl. Hier volgen Hallo resultaten voor de eerste 3 rijen:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>Gegevens voorbereiden voor het model bouwen
Hallo volgende joins Hallo query **nyctaxi\_reis** en **nyctaxi\_tarief** tabellen, genereert een label binaire classificatie **punt**, een meerdere klasse classificatie label **tip\_klasse**, en een voorbeeld van een haalt uit Hallo volledige gekoppelde gegevensset. Hallo steekproeven wordt uitgevoerd door bij het ophalen van een subset van Hallo reizen op basis van tijd ophalen.  Deze query kan worden gekopieerd en geplakt rechtstreeks in Hallo [Azure Machine Learning Studio](https://studio.azureml.net) [importgegevens] [ import-data] -module voor directe gegevensopname vanaf Hallo SQL database-exemplaar in Azure. Hallo query worden records met onjuiste uitgesloten (0, 0) coördinaten.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Wanneer u klaar tooproceed tooAzure Machine Learning bent, mag u ofwel:  

1. Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning, of
2. Hallo door actieve en permanent engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe SQL DW tabel en de nieuwe tabel hello gebruiken in Hallo [importgegevens] [ import-data] -module in Azure Machine Learning. Hallo PowerShell-script in een eerdere stap heeft dit voor u gedaan. U kunt rechtstreeks uit deze tabel in Hallo gegevens importeren-module lezen.

## <a name="ipnb"></a>Gegevensverkenning en functie-engineering in IPython notebook
In deze sectie wordt uitgevoerd, er gegevensverkenning en functie genereren met behulp van beide Python en SQL-query's op Hallo SQL DW eerder hebt gemaakt. Een voorbeeld IPython notebook met de naam **SQLDW_Explorations.ipynb** en een scriptbestand Python **SQLDW_Explorations_Scripts.py** lokale map voor gedownloade tooyour zijn. Ze zijn ook beschikbaar is op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Deze twee bestanden zijn identiek in Python-scripts. Hallo Python scriptbestand beschikbaar tooyou als er geen een IPython laptop-server. Deze twee bestanden zijn ontworpen onder Python steekproef **Python 2.7**.

Hallo nodig Azure SQL DW-informatie in Hallo steekproef IPython Notebook en Hallo Python script bestand gedownloade tooyour lokale computer is aangesloten door Hallo PowerShell-script eerder. Ze zijn uitvoerbare zonder dat aanpassingen.

Als u al een AzureML-werkruimte hebt ingesteld, kunt u rechtstreeks uploaden Hallo voorbeeld IPython Notebook toohello AzureML IPython Notebook service en start het uitvoert. Hier volgen Hallo stappen tooupload tooAzureML IPython Notebook service:

1. Aanmelden tooyour AzureML werkruimte 'Studio' hello boven, en op 'NOTITIEBLOKKEN' aan de linkerkant Hallo van Hallo-webpagina.
   
    ![#22 tekenen][22]
2. Klik op 'Nieuw' op Hallo links benedenhoek van Hallo webpagina en selecteer ' Python 2". Vervolgens een toohello naam laptop en klik op Hallo vinkje toocreate Hallo nieuw leeg IPython Notebook.
   
    ![#23 tekenen][23]
3. Klik op Hallo 'Jupyter' symbool op Hallo links bovenhoek van Hallo nieuwe IPython laptop.
   
    ![#24 tekenen][24]
4. Slepen en neerzetten Hallo voorbeeld IPython Notebook toohello **structuur** pagina van uw service van AzureML IPython Notebook en klik op **uploaden**. Vervolgens worden Hallo voorbeeld IPython Notebook geüploade toohello AzureML IPython Notebook service.
   
    ![#25 tekenen][25]

In de volgorde toorun Hallo steekproef IPython Notebook of Python-scriptbestand Hallo, hello volgende Python pakketten zijn vereist. Als u Hallo AzureML IPython Notebook service gebruikt, zijn deze pakketten vooraf geïnstalleerd.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Hallo aanbevolen volgorde wanneer geavanceerde analytische oplossingen bouwen op AzureML met grote hoeveelheden gegevens is Hallo volgende:

* Gelezen in een klein aantal Hallo gegevens in een kader gegevens in het geheugen.
* Uitvoeren van sommige visualisaties en explorations met Hallo steekproefgegevens.
* Experiment met functie-engineering Hallo met voorbeeldgegevens.
* Voor grotere gegevensverkenning gebruiken voor gegevensmanipulatie en functie-engineering, Python tooissue SQL-query's rechtstreeks met de Hallo SQL DW.
* Bepaal Hallo voorbeeld grootte toobe geschikt is voor het bouwen van Azure Machine Learning-model.

de volgende Hallo zijn enkele gegevensverkenning, gegevensvisualisatie en engineering voorbeelden van functies. Meer gegevens explorations vindt u in het voorbeeld Hallo IPython Notebook en Python Hallo-script voorbeeldbestand.

### <a name="initialize-database-credentials"></a>Databasereferenties initialiseren
De verbindingsinstellingen voor database in de volgende variabelen Hallo initialiseren:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Databaseverbinding maken
Hier volgt Hallo verbindingsreeks die Hallo verbinding toohello database wordt gemaakt.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Rapport aantal rijen en kolommen in de tabel < nyctaxi_trip >
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Totale aantal rijen 173179759 =  
* Totale aantal kolommen = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Rapport aantal rijen en kolommen in de tabel < nyctaxi_fare >
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Totale aantal rijen 173179759 =  
* Totale aantal kolommen = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Lees in een kleine hoeveelheden gegevens voorbeeld Hallo SQL Data Warehouse-Database
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tijd tooread Hallo-voorbeeldtabel is 14.096495 seconden.  
Aantal rijen en kolommen opgehaald = (1000, 21).

### <a name="descriptive-statistics"></a>Beschrijvende statistiek
U bent nu klaar tooexplore Hallo door actieve gegevens. We beginnen met sommige beschrijvende statistieken voor Hallo kijken **reis\_afstand** (of andere velden die u kiest toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualisatie: Voorbeeld van grafiek
Vervolgens kijken we Hallo BoxPlot voor Hallo reis afstand toovisualize hello quantiles.

    df1.boxplot(column='trip_distance',return_type='dict')

![Tekenen van #1][1]

### <a name="visualization-distribution-plot-example"></a>Visualisatie: Distributie tekent voorbeeld
Waarnemingspunten die Hallo distributie en een histogram Hallo visualiseren actieve reis afstanden.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Tekenen van #2][2]

### <a name="visualization-bar-and-line-plots"></a>Visualisatie: Staaf- en tekent de regel
In dit voorbeeld we Hallo reis afstand in vijf opslaglocaties bin en visualiseren Hallo binning resultaten.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

We kunnen Hallo hierboven bin distributie in een balk wordt getekend of tekent met regel:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Tekenen van #3][3]

en

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Tekenen van #4][4]

### <a name="visualization-scatterplot-examples"></a>Visualisatie: Scatterplot voorbeelden
Laten we zien spreidingsgrafiek tekent tussen **reis\_tijd\_in\_sec** en **reis\_afstand** toosee als er correlatie

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 tekenen][6]

We kunnen op dezelfde manier controleren of Hallo relatie tussen **snelheid\_code** en **reis\_afstand**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 tekenen][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Gegevensverkenning op steekproefgegevens met SQL-query's in IPython notebook
In deze sectie besproken voor gegevens distributies met Hallo door actieve gegevens op die wordt bewaard in de nieuwe tabel Hallo die we eerder hebben gemaakt. Houd er rekening mee dat vergelijkbare explorations kunnen worden uitgevoerd met behulp van de oorspronkelijke tabellen Hallo.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Exploratie: Rapport aantal rijen en kolommen in Hallo actieve tabel
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Exploratie: Punt/niet omzeild distributie
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Exploratie: Tip klasse distributie
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Exploratie: Hallo tip distributie door klasse tekenen
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 tekenen][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Exploratie: Dagelijkse distributie van reizen
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploratie: Reis distributie per straten
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Exploratie: Reis distributie door straten en hack licentie
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Exploratie: Verdeling reis
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Exploratie: Reis afstand distributie
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Exploratie: Betaling type distributiepunt
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Controleer of de uiteindelijke vorm Hallo van Hallo featurized tabel
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Bouwen van modellen in Azure Machine Learning
Er zijn nu gereed tooproceed toomodel bouwen en implementeren van modellen in [Azure Machine Learning](https://studio.azureml.net). Hallo-gegevens is gereed toobe in Hallo voorspelling problemen geïdentificeerd eerder, namelijk gebruikt:

1. **Binaire classificatie**: toopredict al dan niet een tip voor een zakenreis is betaald.
2. **Multiklassen classificatie**: toopredict Hallo bereik van een tip betaald, toohello op basis van vooraf gedefinieerde klassen.
3. **Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.  

toobegin Hallo oefening modelleren, meld u bij tooyour **Azure Machine Learning** werkruimte. Als u nog geen een machine learning-werkruimte hebt gemaakt, raadpleegt u [maken van een Azure ML-werkruimte](machine-learning-create-workspace.md).

1. de slag met Azure Machine Learning tooget Zie [wat is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Meld u bij te[Azure Machine Learning Studio](https://studio.azureml.net).
3. Hallo-startpagina Studio biedt een schat aan informatie, video's, zelfstudies, koppelingen toohello Modules verwijzing en andere bronnen. Raadpleeg voor meer informatie over Azure Machine Learning Hallo [Azure Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).

Een typische trainingsexperiment bestaat uit Hallo stappen te volgen:

1. Maak een **+ nieuw** experimenteren.
2. Hallo-gegevens ophalen voor Azure ML.
3. Vooraf verwerken, transformeren en manipuleren van Hallo gegevens zo nodig.
4. Genereren onderdelen naar behoefte.
5. Hallo gegevens splitsen in training/testen/validatie gegevenssets (of afzonderlijke gegevenssets hebben voor elk).
6. Selecteer een of meer machine learning-algoritmen, afhankelijk van Hallo probleem toosolve leren. Bijvoorbeeld binaire classificatie, multiklassen classificatie, regressie.
7. Een of meer modellen Hallo training gegevensset met trainen.
8. Hallo validatie gegevensset met Hallo getraind modellen beoordelen.
9. Hallo modellen toocompute Hallo relevante meetgegevens voor Hallo learning probleem evalueren.
10. Afstellen Hallo modellen en selecteer Hallo best model toodeploy.

In deze oefening hebben we al verkend en engineering Hallo-gegevens in SQL Data Warehouse en besloten op Hallo voorbeeld grootte tooingest in Azure ML. Ga als volgt Hallo procedure toobuild een of meer van de Hallo voorspellende modellen:

1. Hallo-gegevens ophalen voor Azure ML Hallo met [importgegevens] [ import-data] module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie. Zie voor meer informatie, Hallo [importgegevens] [ import-data] verwijzingspagina module.
   
    ![Gegevens importeren voor Azure ML][17]
2. Selecteer **Azure SQL Database** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.
3. Voer Hallo database DNS-naam in Hallo **databaseservernaam** veld. Indeling:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Voer Hallo **databasenaam** in het bijbehorende veld Hallo.
5. Voer Hallo *SQL-gebruikersnaam* in Hallo **Server gebruikersaccountnaam**, en Hallo *wachtwoord* in Hallo **Server het wachtwoord voor gebruikersaccount**.
6. Controleer de Hallo **accepteren servercertificaat** optie.
7. In Hallo **databasequery** bewerken van tekst, Hallo query welke uitgepakt Hallo nodig databasevelden (inclusief eventuele berekende velden zoals Hallo labels) en pijl-omlaag voorbeelden Hallo gegevens toohello gewenst samplegrootte plakken.

Een voorbeeld van een binaire indeling experiment lezen van gegevens rechtstreeks van Hallo SQL Data Warehouse-database is in onderstaande afbeelding ziet hello (onthouden tooreplace Hallo tabelnamen nyctaxi_trip en nyctaxi_fare door Hallo schema naam en het Hallo tabelnamen die u gebruikt in uw overzicht). Vergelijkbare experimenten kunnen worden samengesteld voor multiklassen classificatie en regressie problemen.

![Azure ML Train][10]

> [!IMPORTANT]
> In Hallo modelleren ophalen van gegevens en wordt de query-voorbeelden die zijn opgegeven in de vorige secties **alle labels voor Hallo drie modellering oefeningen zijn opgenomen in de query Hallo**. Een belangrijke (vereist) stap in elk Hallo modelleren oefeningen is te**uitsluiten** onnodige labels voor Hallo Hallo andere twee problemen en andere **doel lekken**. Bijvoorbeeld: bij gebruik van binaire classificatie gebruiken Hallo label **punt** en Hallo velden uitsluiten **tip\_klasse**, **tip\_bedrag**, en **totale\_bedrag**. Hallo laatste doel lekken omdat ze Hallo tip impliceren worden betaald.
> 
> tooexclude alle overbodige kolommen of doel lekken, mag u Hallo [Select Columns in Dataset] [ select-columns] module of Hallo [metagegevens bewerken] [ edit-metadata]. Zie voor meer informatie [Select Columns in Dataset] [ select-columns] en [metagegevens bewerken] [ edit-metadata] verwijzen naar pagina's.
> 
> 

## <a name="mldeploy"></a>Modellen in Azure Machine Learning implementeren
Wanneer uw model klaar is, kunt u het eenvoudig implementeren als een webservice rechtstreeks vanuit het Hallo-experiment. Zie voor meer informatie over het implementeren van Azure ML webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

een nieuwe webservice toodeploy, moet u:

1. Een score experiment maken.
2. Hallo-webservice implementeren.

toocreate een score berekenen experimenteren van een **voltooid** training experiment, klikt u op **maken score berekenen EXPERIMENTEREN** in lagere actiebalk Hallo.

![Score berekenen voor Azure][18]

Azure Machine Learning probeert een score experiment op basis van onderdelen van Hallo trainingsexperiment Hallo toocreate. In het bijzonder wordt:

1. Hallo getraind model opslaan en Hallo model trainingsmodules verwijderen.
2. Een logische identificeren **poort invoer** toorepresent Hallo invoergegevens schema verwacht.
3. Een logische identificeren **uitvoerpoort** toorepresent Hallo verwachte web service-uitvoerschema.

Wanneer Hallo experiment score berekenen is gemaakt, controleren en maken indien nodig aanpassen. Een typische aanpassing is tooreplace hello invoergegevensset en/of de query met een exclusief label velden, zoals deze is alleen beschikbaar wanneer het Hallo-service wordt genoemd. Het is ook dat een goede gewoonte tooreduce Hallo grootte van Hallo invoer gegevensset en/of queryparameters tooa enkele records, net voldoende tooindicate Hallo invoer schema. Voor de uitvoerpoort hello, het algemene tooexclude alle invoervelden en bevat alleen Hallo **Scored Labels** en **berekend kansen** in uitvoer met behulp van Hallo Hallo [kolommen in gegevensset selecteren ] [ select-columns] module.

Een voorbeeld van een experiment score berekenen is opgegeven in Hallo afbeelding hieronder. Als u klaar bent toodeploy, klikt u op Hallo **WEBSERVICE PUBLICEERT** knop in lagere actiebalk Hallo.

![Azure ML publiceren][11]

## <a name="summary"></a>Samenvatting
toorecap wat we in deze zelfstudie scenario hebben gedaan, hebt u een Azure data wetenschap-omgeving hebt gewerkt met een grote openbare gegevensset hebt gemaakt die deze begeleidt Hallo Team gegevens wetenschappelijke processen, alle Hallo manier van gegevens overname toomodel training en vervolgens toohello implementatie van een Azure Machine Learning-webservice.

### <a name="license-information"></a>Licentie-informatie
In dit voorbeeld scenario en de bijbehorende scripts en IPython notebook(s) worden gedeeld door Microsoft onder Hallo MIT-licentie. Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.

## <a name="references"></a>Verwijzingen
• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
