### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Een DNS-Label configureren voor het openbare IP-adres Hallo

tooconnect toohello SQL Server Database Engine van Hallo Internet, overweeg te maken van een DNS-Label voor uw openbare IP-adres. U kunt verbinding maken met IP-adres, maar Hallo DNS-Label maakt een A-Record is eenvoudiger tooidentify en samenvattingen Hallo onderliggende openbaar IP-adres.

> [!NOTE]
> DNS-Labels zijn niet vereist als u plan tooonly verbinding toohello SQL Server-exemplaar binnen Hallo hetzelfde virtuele netwerk of alleen lokaal.

selecteert u eerst een DNS-Label toocreate **virtuele machines** in Hallo-portal. Selecteer uw SQL Server VM toobring kunt u de eigenschappen.

1. Selecteer in het overzicht van de virtuele machines hello, uw **openbaar IP-adres**.

    ![openbaar ip adres](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Vouw in de eigenschappen voor uw openbare IP-adres van Hallo **configuratie**.

1. Voer een naam voor het DNS-label in. Deze naam is een A-Record dat gebruikte tooconnect tooyour SQL Server-VM met de naam in plaats van met IP-adres kan rechtstreeks worden.

1. Klik op Hallo **opslaan** knop.

    ![dns label](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Verbinding maken met Database-Engine toohello vanaf een andere computer

1. Op een computer verbonden toohello internet, open SQL Server Management Studio (SSMS). Als u niet beschikt over SQL Server Management Studio, kunt u dit programma [hier](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) downloaden.

1. In Hallo **verbinding tooServer** of **tooDatabase Engine verbinding** dialoogvenster, bewerken Hallo **servernaam** waarde. Voer Hallo IP-adres of de volledige DNS-naam van Hallo virtuele machine (bepaald in de vorige taak Hallo). U kunt ook een komma toevoegen en de TCP-poort van SQL Server opgeven. Bijvoorbeeld `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. In Hallo **verificatie** de optie **SQL Server-verificatie**.

1. In Hallo **aanmelding** vak, type Hallo-naam van een geldige SQL-aanmelding.

1. In Hallo **wachtwoord** vak, het type wachtwoord op Hallo van Hallo aanmelding.

1. Klik op **Verbinden**.

    ![ssms verbinden](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)