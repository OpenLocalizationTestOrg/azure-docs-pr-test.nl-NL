1. In een nieuw venster aanmelden toohello [Azure-portal](https://portal.azure.com/).
2. Klik in het linkermenu hello, **nieuw**, klikt u op **Databases**, en klik vervolgens onder **Azure Cosmos DB**, klikt u op **maken**.
   
   ![Schermopname van hello Azure-portal meer Services en Azure Cosmos DB markeren](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-1.png)

3. In Hallo **nieuwe account** blade Hallo gewenste configuratie voor hello Azure DB die Cosmos-account opgeven. 

    Met Azure Cosmos DB kunt u een van de vier programmeermodellen kiezen: Gremlin (Graph), MongoDB, SQL (DocumentDB) en Tabel (sleutelwaarde). 
    
    In deze snel starten we je worden programmeren tegen Hallo tabel API dus u kiest **tabel (sleutelwaarde)** als u Hallo formulier invullen. Maar als u grafiekgegevens voor een sociale media-app hebt, documentgegevens uit een catalogus-app, of gegevens die zijn gemigreerd uit een MongoDB-app, moet u er rekening mee houden dat Azure Cosmos DB een zeer beschikbare, globaal gedistribueerd databaseserviceplatform kan bieden voor alle bedrijfskritische toepassingen.

    Hallo nieuwe blade-account met behulp van Hallo informatie als richtlijn in Hallo schermafbeelding invullen. U kiest unieke waarden op als u uw account instellen zodat uw waarden wordt Hallo schermopname niet exact overeenkomen. 
 
    ![Schermopname van het Hallo nieuwe Azure Cosmos-DB-blade](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-2.png)

    Instelling|Voorgestelde waarde|Beschrijving
    ---|---|---
    Id|*Unieke waarde*|Een unieke naam u tooidentify hello Azure DB die Cosmos-account. *Documents.Azure.com* toegevoegde toohello id u voorzien toocreate uw URI, gebruikt u dus een uniek zijn maar persoonsgegevens-ID. Hallo-ID mag alleen kleine letters, cijfers en Hallo bevatten '-' bevatten, en moet tussen 3 en 50 tekens.
    API|Tabel (sleutelwaarde)|Er moet worden programming tegen Hallo [tabel API](../articles/cosmos-db/table-introduction.md) verderop in dit artikel.|
    Abonnement|*Uw abonnement*|Hallo Azure-abonnement dat u toouse hello Azure DB die Cosmos-account wenst. 
    Resourcegroep|*Hallo dezelfde als ID waarde*|Hallo nieuwe Resourcegroepnaam voor uw account. U kunt voor eenvoud, Hallo dezelfde naam gebruiken als uw-ID. 
    Locatie|*Hallo regio dichtstbijzijnde tooyour gebruikers*|Hallo geografische locatie in welke toohost uw Azure DB die Cosmos-account. Hallo-locatie kiezen die het dichtst tooyour gebruikers toogive ze Hallo snelste toegang tot toohello gegevens.   

4. Klik op **maken** toocreate Hallo-account.
5. Op de werkbalk Hallo **meldingen** toomonitor Hallo-implementatieproces.

    ![De melding Implementatie is gestart](./media/cosmos-db-create-dbaccount-table/notification.png)

6.  Wanneer het Hallo-implementatie is voltooid, de nieuwe account open Hallo van Hallo alle Resources tegel. 

    ![DocumentDB-account op alle Resources tegel Hallo](./media/cosmos-db-create-dbaccount-table/all-resources.png)
