U kunt nu Hallo Data Explorer hulpprogramma in hello Azure portal toocreate een database en verzameling. 

1. Klik in de Azure-portal in links navigatiemenu Hallo Hallo op **Data Explorer (Preview)**. 

2. Op Hallo **Data Explorer (Preview)** blade, klikt u op **nieuwe verzameling**, en geef vervolgens Hallo volgende informatie:

    ![Hello Azure Data Explorer-portalblade](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Instelling|Voorgestelde waarde|Beschrijving
    ---|---|---
    Database-id|Taken|Hallo-naam voor de nieuwe database. Databasenamen moeten tussen de 1 en 255 tekens zijn en mogen geen /, \\, # of ? bevatten en mogen niet eindigen met een spatie.
    Verzamelings-id|Items|Hallo-naam voor de nieuwe verzameling. Verzamelingsnamen van de Hallo hebben dezelfde vereisten als de database-id's teken.
    Opslagcapaciteit| Vast (10 GB)|Gebruik de standaardwaarde Hallo. Deze waarde is Hallo opslagcapaciteit van Hallo-database.
    Doorvoer|400 RU|Gebruik de standaardwaarde Hallo. Als u tooreduce latentie wilt, kunt u opschalen doorvoer hello later.
    Partitiesleutel|/category|Een partitiesleutel die gegevens gelijkmatig gedistribueerd tooeach partitie. Selecteren Hallo juist partitiesleutel is belangrijk bij het maken van een verzameling zodat. toolearn meer, Zie [ontwerpen voor het partitioneren van](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Nadat u Hallo formulier hebt voltooid, klikt u op **OK**.

Data Explorer toont Hallo nieuwe Database en verzameling. 
