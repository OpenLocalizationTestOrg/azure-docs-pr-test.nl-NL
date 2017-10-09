U kunt nu Hallo Data Explorer hulpprogramma gebruiken in hello Azure portal toocreate een graph-database. 

1. Klik in de Azure-portal in links navigatiemenu Hallo Hallo op **Data Explorer (Preview)**. 
2. In Hallo **Data Explorer (Preview)** blade, klikt u op **nieuwe grafiek**, vul vervolgens met behulp van de volgende informatie Hallo Hallo-pagina.

    ![Data Explorer in hello Azure-portal](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Instelling|Voorgestelde waarde|Beschrijving
    ---|---|---
    Database-id|voorbeelddatabase|Hallo-ID voor de nieuwe database. Databasenamen moeten tussen de 1 en 255 tekens zijn en mogen geen `/ \ # ?` bevatten of eindigen op een spatie.
    Graaf-id|voorbeeldgrafiek|Hallo-ID voor de nieuwe grafiek. Namen van de grafiek Hallo hebben dezelfde vereisten als de database-id's teken.
    Opslagcapaciteit| 10 GB|Laat de standaardwaarde Hallo. Dit is de opslagcapaciteit Hallo van Hallo-database.
    Doorvoer|400 RU‘s|Laat de standaardwaarde Hallo. U kunt opschalen doorvoer hello later als u wilt dat tooreduce latentie.
    Partitiesleutel|/userid|Een partitiesleutel die gegevens wordt gelijkmatig verdelen tooeach partitie. Hallo juist partitiesleutel is belangrijk bij het maken van een zodat selecteren graph Lees meer over in [ontwerpen voor het partitioneren van](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Zodra het Hallo-formulier wordt ingevuld, klikt u op **OK**.
