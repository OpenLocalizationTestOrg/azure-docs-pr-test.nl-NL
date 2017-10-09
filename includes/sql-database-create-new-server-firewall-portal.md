
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="89bd7-101">Maken van een firewallregel op serverniveau in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="89bd7-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="89bd7-102">Klik op Hallo SQL server-blade, onder instellingen **Firewall** tooopen Hallo Firewall blade voor Hallo SQL server.</span><span class="sxs-lookup"><span data-stu-id="89bd7-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="89bd7-103">Hallo client-IP-adres weergegeven bekijken en controleren of dit uw IP-adres op Hallo Internet via een browser naar keuze (vraag 'Wat is Mijn IP-adres).</span><span class="sxs-lookup"><span data-stu-id="89bd7-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="89bd7-104">Soms komen ze niet overeen. Dit kan verschillende redenen hebben.</span><span class="sxs-lookup"><span data-stu-id="89bd7-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="89bd7-105">Ervan uitgaande dat Hallo IP-adressen overeenkomen, klikt u op **client-IP toevoegen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="89bd7-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![IP van client toevoegen](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="89bd7-107">U kunt openen Hallo SQL Database-firewall op Hallo server tooa één IP-adres of een volledige bereik van adressen.</span><span class="sxs-lookup"><span data-stu-id="89bd7-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="89bd7-108">Hallo server toowhich moeten geldige referenties openen Hallo firewall maakt het mogelijk SQL-beheerders en gebruikers toologin tooany database op.</span><span class="sxs-lookup"><span data-stu-id="89bd7-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="89bd7-109">Klik op **opslaan** Hallo werkbalk toosave deze firewallregel op serverniveau en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="89bd7-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![IP van client toevoegen](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="89bd7-111">Zie [SQL Database-zelfstudie: een server, serverfirewallregel, voorbeelddatabase en databasefirewallregel maken en koppelen met SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="89bd7-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
