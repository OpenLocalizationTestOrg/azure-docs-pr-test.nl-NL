## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Maak een lege SQL-database met behulp van hello Azure-portal

Een Azure SQL-database wordt gemaakt met een gedefinieerde set [reken- en opslagresources](../articles/sql-database/sql-database-service-tiers.md). Hallo-database wordt gemaakt binnen een [Azure-resourcegroep](../articles/azure-resource-manager/resource-group-overview.md) en in een [logische Azure SQL Database-server](../articles/sql-database/sql-database-features.md). 

Volg deze stappen toocreate een lege SQL-database. 

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Databases** van Hallo **nieuw** pagina en selecteer **SQL-Database** van Hallo **Databases** pagina. 

   ![lege database maken](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Hallo SQL-Database formulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:   

   | Instelling | Voorgestelde waarde | Beschrijving |
   | --------| --------------- | ----------- | 
   | **Databasenaam** | mySampleDatabase | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen. | 
   | **Abonnement** | Uw abonnement  | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | myResourceGroup | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Bron selecteren** | Lege database | Hiermee geeft u op dat een lege database moet worden gemaakt. |
   ||||

4. Klik op **Server** toocreate en een nieuwe server configureren voor de nieuwe database. Hallo invullen **nieuwe serverformulier** Hello volgende informatie: 

   | Instelling | Voorgestelde waarde | Beschrijving |
   | --------| --------------- | ----------- | 
   | **Servernaam** | Een globaal unieke naam. | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Een geldige naam. | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen.|
   | **Wachtwoord** | Een geldig wachtwoord. | Uw wachtwoord moet ten minste acht tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën Hallo: hoofdletters, kleine letters, cijfers en niet-alfanumerieke tekens. |
   | **Locatie** | Geen enkele geldige locatie. | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |
   ||||

   ![database-server maken](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Klik op **Selecteren**.

6. Klik op **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor de nieuwe database. Selecteer voor deze zelfstudie **20 dtu's** en **250** GB aan opslagruimte.

   ![database-s1 maken](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Klik op **Toepassen**.  

8. Selecteer een **sortering** voor Hallo lege database (voor deze zelfstudie gebruik Hallo standaardwaarde). Zie voor meer informatie over sorteringen [sorteringen](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Klik op **maken** tooprovision Hallo-database. Neemt over een minuut en een halve toocomplete inrichten. 

10. Op de werkbalk Hallo **meldingen** toomonitor Hallo-implementatieproces.

   ![melding](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Maken van een firewallregel op serverniveau met hello Azure-portal

Hallo SQL Database-service maakt een firewall op serverniveau Hallo. Hallo firewall wordt in eerste instantie voorkomen dat externe hulpprogramma's en toepassingen verbinding maken met server toohello of tooany databases op Hallo-server. Verbindingen zijn toegestaan nadat een firewallregel tooopen specifieke IP-adressen is gemaakt. Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](../articles/sql-database/sql-database-firewall-configure.md) voor de IP-adres van de client en de externe verbinding tooenable via Hallo SQL Database-firewall voor uw IP-adres. 


> [!NOTE]
> Azure SQL Database communiceert via poort 1433. U kunt tooSQL Database koppelen nadat Hallo firewall van uw netwerk uitgaand verkeer via poort 1433 staat.


1. Nadat het Hallo-implementatie is voltooid, klikt u op **SQL-databases** van Hallo links menu en klik vervolgens op **mySampleDatabase** op Hallo **SQL-databases** pagina. Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver20170313.database.windows.net**) en biedt opties voor verdere configuratie. Kopieer deze volledig gekwalificeerde servernaam voor later gebruik.

   > [!IMPORTANT]
   > U moet deze server volledig gekwalificeerde naam tooconnect tooyour server en de databases in de volgende snel aan de slag.
   > 

   ![servernaam](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo. Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend. 

   ![serverfirewallregel](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd nieuwe firewallregel tooa van uw huidige IP-adressen. Een firewallregel kan poort 1433 openen voor een afzonderlijk IP-adres of voor een aantal IP-adressen.

4. Klik op **Opslaan**. Een firewallregel op serverniveau is gemaakt voor uw huidige IP-adres poort 1433 op Hallo logische server te openen.

   ![serverfirewallregel instellen](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Klik op **OK** en sluit vervolgens Hallo **Firewall-instellingen** pagina.

U kunt nu toohello Azure SQL Database-server en de databases verbinden met een hulpprogramma zoals SQL Server Management Studio (SSMS). Hallo-verbinding van deze IP-adres is en gebruikmaakt van server-beheerdersaccount voor de Hallo eerder hebt gemaakt.


> [!IMPORTANT]
> Toegang via Hallo SQL Database-firewall is standaard ingeschakeld voor alle Azure-services. Klik op **OFF** op deze pagina toodisable voor alle Azure-services.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Ophalen van de waarden van verbindingsreeksen met hello Azure-portal

Hallo volledig gekwalificeerde servernaam voor uw Azure SQL Database-server ophalen in hello Azure-portal. U Hallo volledig gekwalificeerde naam tooconnect tooyour servers met SQL Server Management Studio gebruiken.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).

2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 

3. In Hallo **Essentials** deelvenster in Azure portal-pagina voor uw database Hallo Zoek en kopieer de Hallo **servernaam**.

   ![verbindingsgegevens](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
