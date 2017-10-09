### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Maak een nieuwe logische SQL-server in hello Azure-portal

1. Klik op **Nieuw**, zoek naar **logische server** en druk vervolgens op **ENTER**.

    ![logische server zoeken](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. **SQL-server (logische server)** selecteren 

    ![logische server selecteren](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Klik op **maken** tooopen Hallo nieuwe SQL-Server (logische server)-blade.

   <kbd>![logische serverblade geopend](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![logische serverblade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Geef een geldige naam voor de nieuwe logische server Hallo in Hallo SQL Server (logische server) blade server tekstvak naam. Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.
    
    ![nieuwe servernaam](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Hallo volledig gekwalificeerde naam voor de nieuwe server worden < Uw_servernaam >. database.windows.net.
    >
    
4. Geef een gebruikersnaam voor aanmelding Hallo SQL-verificatie voor deze server in Hallo Server admin aanmelding tekstvak. Deze aanmelding staat bekend als Hallo server principal-aanmelding. Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.
    
    ![Aanmeldgegevens SQL-beheerder](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. In Hallo **wachtwoord** en **wachtwoord bevestigen** tekstvakken, een wachtwoord opgeven voor de principal-aanmelding serveraccount Hallo. Een groen vinkje geeft aan dat u een geldig wachtwoord hebt opgegeven.
    
    ![Wachtwoord SQL-beheerder](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Selecteer een abonnement waarin u een machtiging toocreate objecten hebben.

    ![abonnement](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Selecteer in de Hallo Resource groep in het tekstvak, **nieuw** en klik vervolgens in Hallo resource groep in het tekstvak, Geef een geldige naam voor Hallo nieuwe resourcegroep (u kunt ook gebruiken een bestaande resourcegroep als u één voor uzelf al hebt gemaakt). Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.

    ![nieuwe resourcegroep](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. In Hallo **locatie** in het tekstvak, selecteer een gegevenstype center locatie van de juiste tooyour - zoals 'Australië-Oost'.
    
    ![serverlocatie](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > selectievakje voor Hallo **toestaan azure-services tooaccess server** kan niet worden gewijzigd op deze blade. U kunt deze instelling op Hallo firewall serverblade wijzigen. Zie [Aan de slag met beveiliging](../articles/sql-database/sql-database-manage-servers-portal.md) voor meer informatie.
    >
    
9. Klik op **Create**.

    ![knop Maken](./media/sql-data-warehouse-create-logical-server/create.png)

