### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Hallo DNS-naam van de virtuele machine van Hallo bepalen
tooconnect toohello SQL Server Database Engine vanaf een andere computer, moet u weten Hallo Domain Name System (DNS) naam van het Hallo virtuele machine. (Dit is Hallo naam Hallo internet gebruikt tooidentify Hallo virtuele machine. Kunt u Hallo IP-adres, maar Hallo IP-adres veranderen wanneer Azure bronnen voor redundantie en -onderhoud verplaatst. Hallo DNS-naam worden stabiele omdat deze kan worden omgeleid tooa nieuwe IP-adres.)  

1. Selecteer in hello Azure-Portal (of van de vorige stap Hallo) **virtuele machines (klassiek)**.
2. Selecteer uw SQL-VM.
3. Op Hallo **virtuele machine** blade, kopie Hallo **DNS-naam** voor Hallo virtuele machine.
   
    ![DNS-naam](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Verbinding maken met Database-Engine toohello vanaf een andere computer
1. Op een computer verbonden toohello internet, open SQL Server Management Studio.
2. In Hallo **verbinding tooServer** of **tooDatabase Engine verbinding** dialoogvenster in Hallo **servernaam** Hallo DNS- naam van Hallo virtuele machine (zoals bepaald in Hallo vorige taak) en het poortnummer van een openbaar eindpunt in de indeling van Hallo *DNSName, portnumber* zoals **mysqlvm.cloudapp.net,57500**.
   
    ![Verbinding maken met behulp van SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Als je Hallo openbaar eindpunt poortnummer dat u eerder hebt gemaakt, kunt u deze vinden in Hallo **eindpunten** gebied Hallo **virtuele machine** blade.
   
    ![Openbare poort](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. In Hallo **verificatie** de optie **SQL Server-verificatie**.
4. In Hallo **aanmelding** vak, type Hallo-naam van een aanmelding die u in een eerdere taak gemaakt.
5. In Hallo **wachtwoord** vak, het type wachtwoord op Hallo van Hallo-aanmelding die u in een eerdere taak maakt.
6. Klik op **Verbinden**.

