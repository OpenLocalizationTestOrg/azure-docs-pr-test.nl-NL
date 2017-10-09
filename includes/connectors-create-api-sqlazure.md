### <a name="prerequisites"></a>Vereisten
* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [Azure SQL Database](../articles/sql-database/sql-database-get-started.md) met de verbindingsinformatie, met inbegrip van Hallo-servernaam, databasenaam en gebruikersnaam en wachtwoord. Deze informatie is opgenomen in Hallo SQL Database-verbindingsreeks:
  
    Server tcp =:*yoursqlservername*. database.windows.net,1433;Initial Catalog =*yourqldbname*; Beveiliginsinfo = False; Gebruikers-ID = {your_username}; Wachtwoord = {your_password}; Voor MultipleActiveResultSets = False; Versleutelen = True; TrustServerCertificate = False; Verbindingstime-out = 30;
  
    Lees meer over [Azure SQL-Databases](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Wanneer u een Azure SQL Database maakt, kunt u ook Hallo voorbeelddatabases die deel uitmaakt van SQL maken. 
> 
> 

Voordat u uw Azure SQL Database in een logische app, verbinding maken met tooyour SQL-Database. U kunt dit eenvoudig doen in uw logische app op Hallo Azure-portal.  

Verbinding maken met tooyour Azure SQL Database met Hallo volgende stappen:  

1. Een logische app maken. In Hallo Logic Apps designer een trigger toevoegen en voeg vervolgens een actie. Selecteer **beheerde API's van Microsoft weergeven** in Hallo vervolgkeuzelijst en voer vervolgens 'sql' in het zoekvak Hallo. Selecteer een Hallo acties:  
   
    ![Stap voor SQL Azure-verbinding maken](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Als u alle verbindingen tooSQL Database nog niet eerder hebt gemaakt, wordt u gevraagd de verbindingsdetails Hallo op te geven:  
   
    ![Stap voor SQL Azure-verbinding maken](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Geef details van Hallo SQL-Database. Eigenschappen met een sterretje zijn vereist.
   
   | Eigenschap | Details |
   | --- | --- |
   | Verbinding maken via de Gateway |Laat dit uitgeschakeld. Dit wordt gebruikt wanneer verbinding tooan lokale SQL Server. |
   | Verbindingsnaam * |Voer een naam voor de verbinding. |
   | Naam van SQL Server * |Voer Hallo servernaam; Dit is ongeveer *servername.database.windows.net*. Hallo-servernaam wordt weergegeven in Hallo SQL Database-eigenschappen in hello Azure-portal, en ook weergegeven in de verbindingsreeks Hallo. |
   | SQL-databasenaam * |Voer Hallo naam gegeven van de SQL-Database. Deze wordt vermeld in de eigenschappen van Hallo SQL-Database in de verbindingsreeks Hallo: Initial Catalog =*yoursqldbname*. |
   | Gebruikersnaam * |Geef Hallo-gebruikersnaam die u hebt gemaakt tijdens het Hallo SQL-Database is gemaakt. Deze wordt vermeld in de eigenschappen van de SQL-Database Hallo in hello Azure-portal. |
   | Wachtwoord * |Voer Hallo wachtwoord die u hebt gemaakt tijdens het Hallo SQL-Database is gemaakt. |
   
    Deze referenties gebruikte tooauthorize uw logische app tooconnect zijn en toegang tot uw SQL-gegevens. Hierna kunt zoeken uw Verbindingsdetails vergelijkbare toohello volgende:  
   
    ![Stap voor SQL Azure-verbinding maken](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Selecteer **Maken**. 
5. Kennisgeving Hallo verbinding is gemaakt. Nu gaat u verder met hello, andere stappen in uw logische app: 
   
    ![Stap voor SQL Azure-verbinding maken](./media/connectors-create-api-sqlazure/table.png)

