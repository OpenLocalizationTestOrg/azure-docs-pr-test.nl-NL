### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>TCP-poorten openen in Hallo Windows firewall voor het standaardexemplaar Hallo Hallo Database-Engine
1. Toohello virtuele machine verbinding met extern bureaublad. Zie voor gedetailleerde instructies voor het verbinden van toohello VM [een VM SQL met extern bureaublad openen](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Zodra aangemeld, op het startscherm hello, typ **WF.msc**, en druk op ENTER.
   
    ![Hallo firewallprogramma starten](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. In Hallo **Windows Firewall met geavanceerde beveiliging**, in linkerdeelvenster hello, met de rechtermuisknop op **regels voor binnenkomende verbindingen**, en klik vervolgens op **nieuwe regel** in het actievenster Hallo.
   
    ![Nieuwe regel](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. In Hallo **nieuwe Wizard regel voor binnenkomende** dialoogvenster onder **regeltype**, selecteer **poort**, en klik vervolgens op **volgende**.
5. In Hallo **protocollen en poorten** dialoogvenster, de standaard hello gebruiken **TCP**. In Hallo **specifieke lokale poorten** vak en klik vervolgens type Hallo poortnummer van Hallo exemplaar van Database-Engine hello (**1433** voor Hallo-standaardexemplaar of uw keuze voor Hallo particuliere poort in Hallo eindpunt stap).
   
    ![TCP-poort 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Klik op **Volgende**.
7. In Hallo **actie** dialoogvenster, **Hallo verbinding toestaan**, en klik vervolgens op **volgende**.
   
    **Opmerking over beveiliging:** Selecting **Hallo verbinding toestaan als het is veilig** kan bijkomende beveiliging bieden. Selecteer deze optie als u wilt dat de extra beveiligingsopties tooconfigure in uw omgeving.
   
    ![Verbindingen toestaan](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. In Hallo **profiel** dialoogvenster, **openbare**, **persoonlijke**, en **domein**. Klik op **Volgende**.
   
    **Opmerking over beveiliging:** Selecting **openbare** kan toegang via internet Hallo. Selecteer een meer beperkend profiel indien mogelijk.
   
    ![Openbaar profiel](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. In Hallo **naam** in het dialoogvenster Typ een naam en beschrijving voor deze regel en klik vervolgens op **voltooien**.
   
    ![Regelnaam](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Open naar behoefte aanvullende poorten voor andere onderdelen. Zie voor meer informatie [Hallo Windows Firewall tooAllow toegang tot de SQL-Server configureren](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configureren van SQL Server-toolisten op Hallo TCP-protocol

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>SQL Server configureren voor verificatie in gemengde modus
Hallo SQL Server Database Engine kan geen Windows-verificatie gebruiken zonder domeinomgeving. SQL Server tooconnect toohello Database-Engine vanaf een andere computer configureren voor verificatie in gemengde modus. Verificatie in gemengde modus maakt zowel SQL Server-verificatie als Windows-verificatie mogelijk.

> [!NOTE]
> U hoeft verificatie in gemengde modus mogelijk niet te configureren als u een virtueel netwerk van Azure hebt ingesteld met een geconfigureerde domeinomgeving.
> 
> 

1. Tijdens het verbonden toohello virtuele machine op de startpagina hello, typ **SQL Server Management Studio** en klik op de geselecteerde pictogram Hallo.
   
    Hallo eerste keer openen van Management Studio het Hallo gebruikers Management Studio omgeving moet maken. Dit kan even duren.
2. Management Studio geeft Hallo **tooServer verbinding** in het dialoogvenster. In Hallo **servernaam** vak, Hallo-typenaam van Hallo virtuele machine tooconnect toohello Database-Engine Hello Object Explorer (in plaats van de naam van de virtuele machine Hallo ook u kunt **(lokaal)** of een enkele periode als Hallo **servernaam**). Selecteer **Windows-verificatie**, en laat  ***your_VM_name*\your_local_administrator** in Hallo **gebruikersnaam** vak. Klik op **Verbinden**.
   
    ![Verbinding maken met tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. In SQL Server Management Studio Object Explorer met de rechtermuisknop op het Hallo-naam van het Hallo-exemplaar van SQL Server (Hallo virtuele machine-naam) en klik vervolgens op **eigenschappen**.
   
    ![Servereigenschappen](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Op Hallo **beveiliging** pagina onder **serververificatie**, selecteer **modus van SQL Server en Windows-verificatie**, en klik vervolgens op **OK** .
   
    ![Verificatiemodus selecteren](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Hallo SQL Server Management Studio in het dialoogvenster klikt u op **OK** tooacknowledge Hallo vereiste toorestart SQL Server.
6. Klik in Objectverkenner met de rechtermuisknop op **Opnieuw starten**. (Als SQL Server Agent actief is, moet deze ook opnieuw worden gestart.)
   
    ![Opnieuw starten](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Hallo SQL Server Management Studio in het dialoogvenster klikt u op **Ja** tooagree dat u wilt dat toorestart SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Aanmelding voor SQL Server-verificatie maken
tooconnect toohello Database-Engine vanaf een andere computer, moet u ten minste één aanmelding voor SQL Server-verificatie.

1. Vouw in SQL Server Management Studio Object Explorer Hallo-map van Hallo server-exemplaar waarin wordt gezocht toocreate Hallo nieuwe aanmelding.
2. Met de rechtermuisknop op Hallo **beveiliging** map, wijs te**nieuw**, en selecteer **aanmelding...** .
   
    ![Nieuwe aanmelding](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. In Hallo **Login - nieuwe** op Hallo van het dialoogvenster **algemene** pagina, voert u Hallo-naam van de nieuwe gebruiker Hallo in Hallo **aanmeldingsnaam** vak.
4. Selecteer **SQL Server-verificatie**.
5. In Hallo **wachtwoord** Voer een wachtwoord voor de nieuwe gebruiker Hallo. Dit wachtwoord opnieuw invoeren in Hallo **wachtwoord bevestigen** vak.
6. Selecteer Hallo afdwinging wachtwoordopties vereist (**wachtwoordbeleid afdwingen**, **afdwingen Wachtwoordverlooptijd**, en **gebruiker moet wachtwoord bij volgende aanmelding wijzigen**). Als u van deze aanmelding voor uzelf gebruikmaakt, hoeft u geen toorequire een wachtwoord op Hallo volgende aanmelding wijzigen.
7. Van Hallo **standaarddatabase** , selecteert u een standaarddatabase voor Hallo aanmelding. **master** Hallo standaardwaarde voor deze optie is. Als u een gebruikersdatabase nog geen hebt gemaakt, laat u deze set te**master**.
   
    ![Aanmeldingseigenschappen](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Als dit de eerste aanmelding Hallo die u maakt is, kunt u toodesignate deze aanmelding als een SQL Server-beheerder. Zo ja, op Hallo **serverfuncties** pagina selectievakje **sysadmin**.
   
   > [!NOTE]
   > Leden van de vaste serverrol sysadmin voor Hallo hebben volledige controle over Hallo Database-Engine. Beperk deze rol daarom tot gebruikers die volledige controle nodig hebben.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Klik op OK.

Zie [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx) (Een aanmelding maken) voor meer informatie over SQL Server-aanmeldingen.

