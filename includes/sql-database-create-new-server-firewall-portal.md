
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Maken van een firewallregel op serverniveau in hello Azure-portal

1. Klik op Hallo SQL server-blade, onder instellingen **Firewall** tooopen Hallo Firewall blade voor Hallo SQL server.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Hallo client-IP-adres weergegeven bekijken en controleren of dit uw IP-adres op Hallo Internet via een browser naar keuze (vraag 'Wat is Mijn IP-adres). Soms komen ze niet overeen. Dit kan verschillende redenen hebben.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Ervan uitgaande dat Hallo IP-adressen overeenkomen, klikt u op **client-IP toevoegen** op Hallo-werkbalk.

    ![IP van client toevoegen](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > U kunt openen Hallo SQL Database-firewall op Hallo server tooa één IP-adres of een volledige bereik van adressen. Hallo server toowhich moeten geldige referenties openen Hallo firewall maakt het mogelijk SQL-beheerders en gebruikers toologin tooany database op.
    >

4. Klik op **opslaan** Hallo werkbalk toosave deze firewallregel op serverniveau en klik vervolgens op **OK**.

    ![IP van client toevoegen](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Zie [SQL Database-zelfstudie: een server, serverfirewallregel, voorbeelddatabase en databasefirewallregel maken en koppelen met SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
