
1. tooescalate bevoegdheden, type:
   
        sudo -s
   
    Voer uw wachtwoord in.
2. tooinstall MySQL Community Server edition, typt u:
   
        zypper install mysql-community-server
   
    Een ogenblik geduld terwijl MySQL downloadt en installeert.
3. tooset MySQL toostart wanneer Hallo-systeem wordt opgestart, type:
   
        insserv mysql
4. Hallo MySQL-daemon (mysqld) handmatig starten met deze opdracht:
   
        rcmysql start
   
    toocheck hello status Hallo MySQL-daemon, typt u:
   
        rcmysql status
   
    toostop hello MySQL-daemon, typt u:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Hallo MySQL hoofdwachtwoord is na de installatie standaard leeg. Het is raadzaam dat u uitvoert **mysql\_beveiligde\_installatie**, een script waarmee veilige MySQL. Hallo script toochange Hallo MySQL hoofdwachtwoord wordt u gevraagd, verwijdert anonieme gebruikersaccounts, externe hoofdmap aanmeldingen uitschakelen, test databases verwijderen en opnieuw laden Hallo bevoegdheden tabel. We raden u antwoord Ja tooall van deze opties en Hallo root-wachtwoord wijzigen.
   > 
   > 
5. Typ deze toorun Hallo script installatiescript MySQL:
   
        mysql_secure_installation
6. Meld u bij tooMySQL:
   
        mysql -u root -p
   
    Voer Hallo MySQL hoofdwachtwoord (die u in de vorige stap Hallo gewijzigd) en u moet worden gepresenteerd met een prompt waar kunt u SQL-instructies toointeract uitgeven met Hallo-database.
7. toocreate een nieuwe MySQL-gebruiker, voert u Hallo volgende op Hallo **mysql >** prompt:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Opmerking: Hallo puntkomma's (;) aan einde Hallo Hallo regels zijn essentieel voor het Hallo-opdrachten beëindigen.
8. een database en verleen Hallo toocreate `mysqluser` gebruikersmachtigingen voor het probleem Hallo volgende opdrachten:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Houd er rekening mee database gebruikersnamen en wachtwoorden alleen worden gebruikt door de scripts toohello database verbinding te maken.  Account voor database gebruikersnamen noodzakelijkerwijs niet werkelijke gebruikersaccounts op Hallo-systeem.
9. toolog in van een andere computer, type:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    waar `ip-address` Hallo IP-adres van Hallo computer van waaruit u tooMySQL verbinding.
10. tooexit hello beheerprogramma MySQL-database, typt u:
    
        quit

## <a name="add-an-endpoint"></a>Een eindpunt toevoegen
1. Nadat de MySQL is geïnstalleerd, moet u een eindpunt tooaccess MySQL tooconfigure op afstand. Meld u bij toohello [klassieke Azure-portal][AzurePortal]. Klik op **virtuele Machines**Hallo-naam van uw nieuwe virtuele machine op en klik vervolgens op **eindpunten**.
2. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
3. Toevoegen van een eindpunt met de naam 'MySQL' met protocol **TCP**, en **openbare** en **persoonlijke** poorten set te '3306'.
4. tooremotely verbinding toohello virtuele machine maken van uw computer, type:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Gebruik Hallo virtuele machine die we in deze zelfstudie hebt gemaakt, typ deze opdracht:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
