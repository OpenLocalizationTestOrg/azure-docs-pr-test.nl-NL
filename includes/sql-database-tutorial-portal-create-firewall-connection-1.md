## <a name="log-in-to-the-azure-portal"></a>Aanmelden bij Azure Portal

Meld u aan bij [Azure Portal](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-the-azure-portal"></a>Maak een lege SQL-database met de Azure portal

Een Azure SQL-database wordt gemaakt met een gedefinieerde set [reken- en opslagresources](../articles/sql-database/sql-database-service-tiers.md). De database is gemaakt in een [Azure-resourcegroep](../articles/azure-resource-manager/resource-group-overview.md) en in een [logische Azure SQL Database-server](../articles/sql-database/sql-database-features.md). 

Volg deze stappen voor het maken van een lege SQL-database. 

1. Klik op de knop **Nieuw** in de linkerbovenhoek van Azure Portal.

2. Selecteer **Databases** op de pagina **Nieuw** en selecteer **SQL-database** op de pagina **Databases**. 

   ![lege database maken](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Vul het formulier SQL Database in met de volgende informatie, zoals in de voorgaande afbeelding wordt weergegeven:   

   | Instelling | Voorgestelde waarde | Beschrijving |
   | --------| --------------- | ----------- | 
   | **Databasenaam** | mySampleDatabase | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen. | 
   | **Abonnement** | Uw abonnement  | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | myResourceGroup | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Bron selecteren** | Lege database | Hiermee geeft u op dat een lege database moet worden gemaakt. |
   ||||

4. Klik op **Server** als u een nieuwe server voor de nieuwe database wilt maken en configureren. Vul de **nieuwe serverformulier** met de volgende informatie: 

   | Instelling | Voorgestelde waarde | Beschrijving |
   | --------| --------------- | ----------- | 
   | **Servernaam** | Een globaal unieke naam. | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Een geldige naam. | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen.|
   | **Wachtwoord** | Een geldig wachtwoord. | Uw wachtwoord moet ten minste acht tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën: hoofdletters, kleine letters, cijfers en niet-alfanumerieke tekens. |
   | **Locatie** | Geen enkele geldige locatie. | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |
   ||||

   ![database-server maken](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Klik op **Selecteren**.

6. Klik op **Prijscategorie** om de servicelaag en het prestatieniveau voor de nieuwe database op te geven. Selecteer voor deze zelfstudie **20 dtu's** en **250** GB aan opslagruimte.

   ![database-s1 maken](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Klik op **Toepassen**.  

8. Selecteer een **sortering** voor de lege database (Gebruik de standaardwaarde voor deze zelfstudie). Zie voor meer informatie over sorteringen [sorteringen](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Klik op **Maken** om de database in te richten. Inrichting vergt over een minuut en een halve te voltooien. 

10. Klik op de werkbalk op **Meldingen** om het implementatieproces te bewaken.

   ![melding](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-the-azure-portal"></a>Een firewallregel op serverniveau met de Azure portal maken

De service SQL Database maakt een firewall op niveau van de server. De firewall wordt in eerste instantie voorkomen dat externe hulpprogramma's en toepassingen op de server of op alle databases op de server geen verbinding kan maken. Verbindingen zijn toegestaan nadat een firewallregel is gemaakt om te openen, specifieke IP-adressen. Volg deze stappen voor het maken van een [SQL-Database firewallregel op serverniveau](../articles/sql-database/sql-database-firewall-configure.md) voor IP-adres van de client, en voor externe verbindingen via de firewall SQL-Database voor uw IP-adres. 


> [!NOTE]
> Azure SQL Database communiceert via poort 1433. U kunt verbinding maken met SQL Database pas nadat de firewall van uw netwerk uitgaand verkeer via poort 1433 kunt.


1. Wanneer de implementatie is voltooid, klikt u op **SQL Databases** in het menu aan de linkerkant. Klik vervolgens op de pagina **SQL Databases** op **mySampleDatabase**. De overzichtspagina voor uw database wordt geopend, met de volledig gekwalificeerde servernaam (zoals **mynewserver20170313.database.windows.net**) en opties voor verdere configuratie. Kopieer deze volledig gekwalificeerde servernaam voor later gebruik.

   > [!IMPORTANT]
   > U hebt deze volledig gekwalificeerde servernaam nodig om in de volgende Quick Starts verbinding te maken met de server en de bijbehorende databases.
   > 

   ![servernaam](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Klik op de werkbalk op **Serverfirewall instellen** zoals in de vorige afbeelding is weergegeven. De pagina **Firewallinstellingen** voor de SQL Database-server wordt geopend. 

   ![serverfirewallregel](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Klik op **IP van client toevoegen** op de werkbalk om uw huidige IP-adres aan een nieuwe firewallregel toe te voegen. Een firewallregel kan poort 1433 openen voor een afzonderlijk IP-adres of voor een aantal IP-adressen.

4. Klik op **Opslaan**. Er wordt een firewallregel op serverniveau gemaakt voor uw huidige IP-adres waarbij poort 1433 op de logische server wordt geopend.

   ![serverfirewallregel instellen](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Klik op **OK** en sluit de pagina **Firewallinstellingen**.

U kunt nu verbinding maken met de Azure SQL Database-server en de databases met een hulpprogramma zoals SQL Server Management Studio (SSMS). De verbinding van deze IP-adres en de eerder gemaakte server-beheerdersaccount wordt gebruikt.


> [!IMPORTANT]
> Voor alle Azure-services is toegang via de SQL Database-firewall standaard ingeschakeld. Klik op **UIT** op deze pagina om dit voor alle Azure-services uit te schakelen.


## <a name="get-connection-string-values-using-the-azure-portal"></a>Verbinding met de Azure portal tekenreekswaarden ophalen

Haal de volledig gekwalificeerde servernaam van uw Azure SQL Database-server op uit Azure Portal. U gebuikt de volledig gekwalificeerde servernaam om verbinding met uw server te maken via SQL Server Management Studio.

1. Meld u aan bij [Azure Portal](https://portal.azure.com/).

2. Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**. 

3. In het deelvenster **Essentials** van de Azure Portal-pagina van uw database kopieert u de **servernaam**.

   ![verbindingsgegevens](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
