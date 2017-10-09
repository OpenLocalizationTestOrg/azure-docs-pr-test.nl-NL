
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Meld u bij toohello [Azure-portal](https://portal.azure.com/) op http://portal.azure.com/.
2. Klik in het linkerdeelvenster vaandel hello, **door alles bladeren**. Hallo **Bladeren** blade wordt weergegeven.
3. Schuif en klik op **SQL-servers**. Hallo **SQL-servers** blade wordt weergegeven.
   
    ![Uw Azure SQL Database-server vinden in Hallo-portal][b21-FindServerInPortal]
4. Klik op Hallo voor het gemak minimaliseren besturingselement op Hallo eerder **Bladeren** blade.
5. In de filtertekstvak Hallo begint te typen Hallo-naam van uw server. De rij wordt weergegeven.
6. Klik op de rij Hallo voor uw server. Een blade voor uw server wordt weergegeven.
7. Klik op de blade van uw server **instellingen**. Hallo **instellingen** blade wordt weergegeven.
8. Klik op **Firewall**. Hallo **firewallinstellingen** blade wordt weergegeven.
   
    ![Klik op Instellingen > Firewall][b31-SettingsFirewallNavig]
9. Klik op **-Client toevoegen IP**. Typ een naam voor de nieuwe regel in de eerste tekstvak Hallo.
10. Type in Hallo hoge en lage IP-adres waarden voor de gewenste Hallo bereik tooenable.
    
    * Het kan ook handig toohave Hallo lage waarde end met **.0** en Hallo met hoge **.255**.
    
    ![Een tooallow bereik van IP-adres toevoegen][b41-AddRange]
11. Klik op **Opslaan**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
