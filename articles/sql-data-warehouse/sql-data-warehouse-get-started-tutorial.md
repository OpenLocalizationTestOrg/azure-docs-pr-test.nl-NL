---
title: aan de slag aaaAzure SQL Data Warehouse - zelfstudie | Microsoft Docs
description: Deze zelfstudie leert u hoe tooprovision en gegevens laden in Azure SQL Data Warehouse. U leert ook Hallo basisbeginselen van schalen, onderbreken en afstemmen.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Aan de slag met SQL Data Warehouse

Deze zelfstudie laat zien hoe tooprovision en gegevens laden in Azure SQL Data Warehouse. U leert ook Hallo basisbeginselen van schalen, onderbreken en afstemmen. Wanneer u klaar bent u klaar tooquery en Verken uw datawarehouse.

**Geschatte tijd toocomplete:** dit is een end-to-end zelfstudie met voorbeeldcode die het duurt ongeveer 30 minuten toocomplete als u Hallo vereisten hebt voldaan. 

## <a name="prerequisites"></a>Vereisten

Hallo-zelfstudie wordt ervan uitgegaan dat u bekend bent met de basisconcepten van SQL Data Warehouse. Zie [Wat is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md) als u eerst wat meer informatie nodig hebt. 

### <a name="sign-up-for-microsoft-azure"></a>Registreren voor Microsoft Azure
Als u nog geen Microsoft Azure-account hebt, moet u toosign voor één toouse deze service. Deze stap kunt u overslaan als u al een account hebt. 

1. Navigeer toohello account pagina's [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Maak een gratis Azure-account of koop een account.
3. Volg de instructies Hallo

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Toepasselijke stuurprogramma's en hulpprogramma's installeren voor SQL-client

De meeste hulpprogramma's van SQL-client verbinding kunnen maken voor tooSQL Data Warehouse via JDBC, ODBC- of ADO.NET. Vervaldatum toohello groot aantal functies van T-SQL die ondersteuning biedt voor SQL Data Warehouse, zijn sommige clienttoepassingen niet volledig compatibel is met SQL Data Warehouse.

Als u een Windows-besturingssysteem gebruikt, raden we u aan te kiezen voor [Visual Studio] of [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Een SQL Data Warehouse maken

SQL Data Warehouse is een speciaal databasetype dat is ontworpen voor parallelle verwerking op zeer grote schaal. Hallo-database is verdeeld over meerdere knooppunten en query's parallel worden verwerkt. SQL Data Warehouse is een besturingselement-knooppunt dat activiteiten van alle knooppunten in Hallo Hallo ingedeeld. Hallo-knooppunten zelf uw gegevens toomanage SQL-Database gebruiken.  

> [!NOTE]
> Het maken van een SQL Data Warehouse kan een nieuwe factureerbare service tot gevolg hebben.  Zie [Prijzen van SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/) voor meer informatie.
>

### <a name="create-a-data-warehouse"></a>Een datawarehouse maken

1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** > **Databases** > **SQL Data Warehouse**.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Vul de implementatiegegevens in

    **Databasenaam**: kies een naam. Als u meerdere datawarehouses hebt, raden wij aan uw namen bevatten gegevens zoals Hallo regio, omgeving, bijvoorbeeld *mydw-westus-1-test*.

    **Abonnement:** uw Azure-abonnement

    **Resourcegroep**: maak een resourcegroep of gebruik een bestaande resourcegroep.
    > [!NOTE]
    > Resourcegroepen zijn handig voor het beheren van resources, waaronder het bereik van toegangsbeheer controleren en het implementeren met sjablonen. [Hier](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) vindt u meer informatie over resourcegroepen en aanbevolen procedures voor Azure

    **Bron**: lege database

    **Server**: Selecteer Hallo-server die u hebt gemaakt in [vereisten].

    **Sortering**: laat Hallo standaardsortering SQL_Latin1_General_CP1_CI_AS.

    **Selecteer prestaties**: het is raadzaam beginnen met het standaard 400DWU Hallo.

4. Kies **pincode toodashboard** ![pincode tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Terug zitten en wachten op uw datawarehouse toodeploy! Dit is normaal voor dit proces tootake enkele minuten. Hallo portal waarschuwt u als uw datawarehouse gereed toouse is. 

## <a name="connect-toosql-data-warehouse"></a>Verbinding maken met tooSQL Data Warehouse

Deze zelfstudie maakt gebruik van SQL Server Management Studio (SSMS) tooconnect toohello-datawarehouse. TooSQL Data Warehouse verbinding kunnen maken via deze ondersteunde connectors: ADO.NET, JDBC, ODBC- en PHP. Let op: de functionaliteit van hulpprogramma's die niet door Microsoft worden ondersteund, is mogelijk beperkt.


### <a name="get-connection-information"></a>Verbindingsgegevens ophalen

tooconnect tooyour datawarehouse, moet u tooconnect via Hallo logische SQL-server u hebt gemaakt in [vereisten].

1. Selecteer uw datawarehouse in Hallo dashboard of zoekt u het in uw resources.

    ![Dashboard van SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Volledige naam van de Hallo voor Hallo logische SQL-server vinden.

    ![Servernaam selecteren](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. SSMS openen en gebruiken van object explorer tooconnect toothis server met behulp van Hallo server admin-referenties die u hebt gemaakt in [vereisten]

    ![Verbinden met SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Als alles goed gaat, moet u nu verbonden tooyour logische SQL-server. Aangezien u aangemeld als serverbeheerder hello, kunt u tooany database gehost door Hallo-server, inclusief Hallo-hoofddatabase. 

Er is slechts één server-beheerdersaccount en de meeste bevoegdheden van een gebruiker Hallo heeft. Wees voorzichtig niet tooallow te veel mensen in uw organisatie tooknow Hallo admin-wachtwoord. 

U kunt ook een Azure Active Directory-beheerdersaccount hebben. Wij niet hier Hallo-gegevens. Als u toolearn meer wilt over het gebruik van Azure Active Directory-verificatie, Zie [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Hierna bespreken we het maken van extra aanmeldingen en gebruikers.


## <a name="create-a-database-user"></a>Een databasegebruiker maken

In deze stap maakt u een gebruiker account tooaccess uw datawarehouse. We ook ziet u hoe toogive die gebruiker Hallo mogelijkheid toorun query's met een grote hoeveelheid geheugen en CPU-resources.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Opmerkingen over de resource-klassen voor het toewijzen van resources tooqueries

- tookeep het gebruik van uw gegevens beschermen, niet Hallo server admin toorun-query's op uw productiedatabases. Hieraan Hallo meeste bevoegdheden van een gebruiker en gebruik van tooperform brengt bewerkingen op gegevens van gebruiker met uw gegevens in gevaar. Ook omdat Hallo serverbeheerder is tooperform beheerbewerkingen bedoeld, voert deze bewerkingen met slechts een kleine toewijzing van geheugen en CPU-resources. 

- SQL Data Warehouse maakt gebruik van vooraf gedefinieerde databaserollen resource klassen, tooallocate verschillende hoeveelheden geheugen, CPU-bronnen en gelijktijdigheid sleuven toousers aangeroepen. Elke gebruiker kan tooa klein, normaal, groot of extra groot bronklasse behoren. Hallo van gebruiker bronklasse bepaalt Hallo resources Hallo gebruiker heeft toorun query's en bewerkingen worden geladen.

- Voor optimale gegevenscompressie, Hallo gebruiker mogelijk tooload grote of extra groot toewijzingen. Meer informatie over resourceklassen vindt u [hier](./sql-data-warehouse-develop-concurrency.md#resource-classes):

### <a name="create-an-account-that-can-control-a-database"></a>Een account maken waarmee een database kan worden beheerd

Nadat u bent momenteel aangemeld in Hallo serverbeheerder hebt machtigingen toocreate aanmeldingen en gebruikers.

1. Open een nieuwe query voor **Hoofd** met behulp van SSMS of een andere queryclient.

    ![Nieuwe query in Hoofd](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nieuwe query in Hoofd1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. Voer in het queryvenster Hallo, deze toocreate T-SQL-opdracht een aanmelding met de naam MedRCLogin en een gebruiker met de naam LoadingUser. Deze aanmelding kan verbinding maken toohello logische SQL-server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Nu opvragen Hallo *SQL Data Warehouse-database*, op basis van een database-gebruikersaccount maken Hallo aanmelding u tooaccess gemaakt en worden bewerkingen uitvoeren op Hallo-database.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Hallo database gebruiker besturingselement machtigingen toohello database aangeroepen NYT geven. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Als de databasenaam van uw afbreekstreepjes in het heeft, moet u ervoor toowrap deze haakjes! 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Hallo gebruiker gemiddeld toewijzingen geven

1. Voer deze opdracht T-SQL toomake deze in een lid van Hallo gemiddeld resourceklasse, mediumrc wordt aangeroepen. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Klik op [hier](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn meer informatie over klassen gelijktijdigheid van taken en resource! 
    >

2. Toohello logische server verbinden met de nieuwe referenties Hallo

    ![Aanmelden met nieuwe aanmeldgegevens](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Gegevens laden vanuit Azure-blobopslag

U bent nu klaar tooload gegevens in uw datawarehouse. Deze stap ziet u hoe tooload New York City taxi CAB-bestand van een openbare Azure-opslag-blob. 

- Een veelgebruikte manier tooload gegevens in SQL Data Warehouse is toofirst Hallo gegevens tooAzure blob-opslag verplaatsen en vervolgens in uw datawarehouse te laden. toomake deze eenvoudiger toounderstand hoe tooload, hebben we Den Haag taxi cab-gegevens die al worden gehost in een openbare Azure-opslag-blob. 

- Voor toekomstig gebruik, toolearn hoe tooget uw gegevens tooAzure blob-opslag- of deze rechtstreeks vanuit uw bron in SQL Data Warehouse, Zie tooload hello [laden overzicht](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Externe gegevens definiëren

1. Maak een hoofdsleutel. U hoeft alleen toocreate een hoofdsleutel eenmaal per database. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Hallo-locatie van hello Azure blob met Hallo taxi CAB-bestand gegevens definiëren.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Hallo externe bestandsindelingen definiëren

    Hallo ```CREATE EXTERNAL FILE FORMAT``` opdracht is gebruikte toospecify de indeling van de bestanden die Hallo externe gegevens bevatten. Ze bevatten tekst gescheiden door een of meer tekens, genaamd scheidingstekens. Voor demonstratiedoeleinden Hallo taxi CAB-bestand gegevens opgeslagen als niet-gecomprimeerde gegevens en als gzip gecomprimeerde gegevens.

    Voer deze opdrachten T-SQL toodefine twee verschillende indelingen: niet-gecomprimeerd en gecomprimeerd.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Maak een schema voor de externe bestandsindeling. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Hallo externe tabellen maken. Deze tabellen verwijzen naar gegevens die zijn opgeslagen in Azure-blobopslag. Hallo T-SQL-opdrachten toocreate na enkele externe tabellen dat alle punt toohello Azure blob we eerder in onze externe gegevensbron gedefinieerde uitgevoerd.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Hallo-gegevens importeren uit Azure blob-opslag.

SQL Data Warehouse ondersteunt een sleutelinstructie met de naam CREATE TABLE AS SELECT (CTAS). Deze instructie maakt een nieuwe tabel op basis van Hallo resultaten van een select-instructie. Hallo nieuwe tabel heeft dezelfde kolommen en gegevenstypen Hallo Hallo resultaten van Hallo selecteert u de instructie.  Dit is een elegante manier tooimport gegevens uit Azure blob storage in SQL Data Warehouse.

1. Voer dit script tooimport uw gegevens.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Bekijk uw gegevens tijdens het laden.

   U laadt meerdere GB's aan gegevens en comprimeert die tot hoogwaardige geclusterde columnstore-indexen. Hallo volgende query worden uitgevoerd die gebruikmaakt van een dynamische Beheerweergave weergaven (DMV's) tooshow Hallo status Hallo belast. Na het starten van de query Hallo halen een koffie en een gevulde terwijl SQL Data Warehouse enkele zware werk bevat.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Bekijk alle systeemquery's.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Al uw gegevens zijn netjes geladen in uw Azure SQL Data Warehouse.

    ![Geladen gegevens bekijken](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Queryprestaties verbeteren

Er zijn verschillende manieren tooimprove prestaties van query's en tooachieve Hallo snelle prestaties van SQL Data Warehouse tooprovide ontworpen.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Zie Hallo effect van het schalen van op de prestaties van query 's 

Eenzijdige tooimprove queryprestaties is tooscale bronnen door Hallo DWU-serviceniveau voor uw datawarehouse wijzigen. Elk serviceniveau kost meer, maar u kunt op elk gewenst moment terugschalen of resources onderbreken. 

In deze stap vergelijkt u de prestaties bij twee verschillende DWU-instellingen.

Eerst schalen we Hallo sizing omlaag too100 DWU zodat we een beter beeld van hoe een rekenknooppunt krijgt op zichzelf uitvoeren kunt.

1. Ga toohello portal en selecteer uw SQL Data Warehouse.

2. Selecteer schaal in de blade SQL Data Warehouse Hallo. 

    ![DW schalen vanuit de portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Hallo-prestaties balk too100 DWU terugschroeven en klik op opslaan.

    ![Schalen en opslaan](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Wacht tot de schaal bewerking toofinish.

    > [!NOTE]
    > Query's kunnen niet worden uitgevoerd tijdens het Hallo schaal wijzigen. Het schalen **beëindigt** uw huidige actieve query's. U kunt ze opnieuw wanneer het Hallo-bewerking is voltooid.
    >
    
5. Voer een scanbewerking op Hallo reis gegevens, Hallo bovenste miljoen vermeldingen voor alle Hallo kolommen te selecteren. Als u meteen toomove snel op bent, kunt u gratis tooselect minder rijen. Let op Hallo duurt toorun deze bewerking.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Schalen van uw datawarehouse back-too400 DWU. Denk eraan dat elke 100 DWU is het toevoegen van een andere compute knooppunt tooyour Azure SQL Data Warehouse.

7. Hallo query opnieuw uitvoeren. U zou een duidelijk verschil moeten zien. 

    > [!NOTE]
    > Omdat Hallo query een grote hoeveelheid gegevens retourneert, mogelijk Hallo bandbreedte beschikbaarheid van SSMS machine Hallo een prestatieknelpunt. Dit kan tot gevolg hebben dat er helemaal geen sprake is van prestatieverbetering!

> [!NOTE]
> SQL Data Warehouse gebruikt MPP (Massively Parallel Processing). Query's die bij het scannen of analytische functies uitvoeren op miljoenen rijen ervaren Hallo true kracht van Azure SQL Data Warehouse.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Zie Hallo effect van statistieken op de prestaties van query 's

1. Voer een query dat joins datum-tabel met de Hallo reis tabel Hallo

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Deze query heeft een tijdje omdat SQL Data Warehouse tooshuffle gegevens heeft voordat het Hallo join kunt uitvoeren. Joins geen tooshuffle gegevens als ze ontworpen toojoin gegevens in Hallo zijn dezelfde manier als deze is gedistribueerd. Dat is een ingewikkelder onderwerp. 

2. Statistieken maken een groot verschil. 
3. Deze instructie toocreate statistieken worden uitgevoerd op Hallo join-kolommen.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > SQL DW beheert niet automatisch statistieken voor u. Statistieken zijn belangrijk voor de prestaties van query's en we raden u ten zeerste aan statistieken te maken en bij te werken.
    > 
    > **Krijgt u Hallo profiteren door statistieken op kolommen die betrokken zijn in joins van kolommen die worden gebruikt in Hallo waar component en kolommen gevonden in de GROUP BY.**
    >

3. Hallo query opnieuw uitvoeren van de vereisten en bekijk eventuele prestatieverschillen in. Bij Hallo verschillen in prestaties van query's wordt niet als ingrijpende als omhoog schalen, ziet u een versnellen. 

## <a name="next-steps"></a>Volgende stappen

U bent nu klaar tooquery en verkennen. Bekijk onze aanbevolen procedures en tips.

Als u klaar bent verkennen voor Hallo dag, zodat toopause ervoor dat uw exemplaar! In productie, kunt u enorm veel besparingen ervaring door te onderbreken en schalen toomeet behoeften van uw bedrijf.

![Onderbreken](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Handige documentatie

[Gelijktijdigheid en werklastbeheer][]

[Aanbevolen procedures voor Azure SQL Data Warehouse][]

[Querybewaking][]

[Top 10 aanbevolen procedures voor het bouwen van een grootschalige relationele Data Warehouse][]

[Migreren gegevens tooAzure SQL Data Warehouse][]

[Gelijktijdigheid en werklastbeheer]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Aanbevolen procedures voor Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Querybewaking]: sql-data-warehouse-manage-monitor.md
[Top 10 aanbevolen procedures voor het bouwen van een grootschalige relationele Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migreren gegevens tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[vereisten]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
