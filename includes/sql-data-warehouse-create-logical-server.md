### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="6dd01-101">Maak een nieuwe logische SQL-server in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6dd01-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="6dd01-102">Klik op **Nieuw**, zoek naar **logische server** en druk vervolgens op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6dd01-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![logische server zoeken](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="6dd01-104">**SQL-server (logische server)** selecteren</span><span class="sxs-lookup"><span data-stu-id="6dd01-104">Select **SQL server (logical server)**</span></span> 

    ![logische server selecteren](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="6dd01-106">Klik op **maken** tooopen Hallo nieuwe SQL-Server (logische server)-blade.</span><span class="sxs-lookup"><span data-stu-id="6dd01-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="6dd01-107"><kbd>![logische serverblade geopend](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![logische serverblade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="6dd01-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="6dd01-108">Geef een geldige naam voor de nieuwe logische server Hallo in Hallo SQL Server (logische server) blade server tekstvak naam.</span><span class="sxs-lookup"><span data-stu-id="6dd01-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="6dd01-109">Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6dd01-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nieuwe servernaam](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="6dd01-111">Hallo volledig gekwalificeerde naam voor de nieuwe server worden < Uw_servernaam >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6dd01-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="6dd01-112">Geef een gebruikersnaam voor aanmelding Hallo SQL-verificatie voor deze server in Hallo Server admin aanmelding tekstvak.</span><span class="sxs-lookup"><span data-stu-id="6dd01-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="6dd01-113">Deze aanmelding staat bekend als Hallo server principal-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6dd01-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="6dd01-114">Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6dd01-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Aanmeldgegevens SQL-beheerder](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="6dd01-116">In Hallo **wachtwoord** en **wachtwoord bevestigen** tekstvakken, een wachtwoord opgeven voor de principal-aanmelding serveraccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="6dd01-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="6dd01-117">Een groen vinkje geeft aan dat u een geldig wachtwoord hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6dd01-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Wachtwoord SQL-beheerder](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="6dd01-119">Selecteer een abonnement waarin u een machtiging toocreate objecten hebben.</span><span class="sxs-lookup"><span data-stu-id="6dd01-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![abonnement](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="6dd01-121">Selecteer in de Hallo Resource groep in het tekstvak, **nieuw** en klik vervolgens in Hallo resource groep in het tekstvak, Geef een geldige naam voor Hallo nieuwe resourcegroep (u kunt ook gebruiken een bestaande resourcegroep als u één voor uzelf al hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="6dd01-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="6dd01-122">Een groen vinkje geeft aan dat u een geldige naam hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6dd01-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nieuwe resourcegroep](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="6dd01-124">In Hallo **locatie** in het tekstvak, selecteer een gegevenstype center locatie van de juiste tooyour - zoals 'Australië-Oost'.</span><span class="sxs-lookup"><span data-stu-id="6dd01-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![serverlocatie](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="6dd01-126">selectievakje voor Hallo **toestaan azure-services tooaccess server** kan niet worden gewijzigd op deze blade.</span><span class="sxs-lookup"><span data-stu-id="6dd01-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="6dd01-127">U kunt deze instelling op Hallo firewall serverblade wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6dd01-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="6dd01-128">Zie [Aan de slag met beveiliging](../articles/sql-database/sql-database-manage-servers-portal.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6dd01-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="6dd01-129">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6dd01-129">Click **Create**.</span></span>

    ![knop Maken](./media/sql-data-warehouse-create-logical-server/create.png)

