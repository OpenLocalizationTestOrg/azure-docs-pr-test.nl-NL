U kunt virtuele machines in Azure maken met behulp van de Server Explorer in Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Maken van een virtuele machine van Azure in Server Explorer
Bij het maken van een virtuele machine in Hallo [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103), u kunt ook een virtuele machine in Azure maken met behulp van opdrachten in Server Explorer. Virtuele machines kunnen worden gebruikt, bijvoorbeeld tooprovide een front end achter een algemene taakverdeling openbaar eindpunt.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate een nieuwe virtuele machine
1. Open in Server Explorer Hallo **Azure** knooppunt en klik op **virtuele Machines**.
2. Klik in het contextmenu hello, **virtuele Machine maken**.
   
    Hallo **maken van een nieuwe virtuele Machine** wizard wordt weergegeven.
   
    ![Hallo opdracht van de virtuele Machine maken](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Op Hallo **Kies een abonnement** pagina, selecteert u een abonnement toouse bij het maken van Hallo virtuele machine en klik vervolgens op **volgende**.
   
    Als u niet bent aangemeld tooAzure, klikt u op **aanmelden** toosign in. Selecteer vervolgens uw Azure-abonnement in de vervolgkeuzelijst Hallo als deze nog niet is geselecteerd.
4. Op Hallo **selecteert u de installatiekopie van een virtuele Machine** pagina, selecteert u een afbeeldingstype in Hallo **afbeeldingstype** dropdown keuzelijst en selecteer vervolgens de installatiekopieën van een virtuele machine in Hallo **installatiekopienaam** keuzelijst met invoervak. Wanneer u bent klaar, klikt u op **volgende**.
   
    ![Selecteer een pagina van de installatiekopie van virtuele machine](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    U kunt de volgende afbeeldingstypen Hallo.
   
   * **Installatiekopieën van het openbare** geeft een lijst van virtuele machine installatiekopieën van besturingssystemen en server-software, zoals Windows Server en SQL Server.
   * **MSDN-installatiekopieën** geeft een lijst van installatiekopieën van virtuele machines van de software beschikbaar tooMSDN abonnees, zoals Visual Studio en Microsoft Dynamics.
   * **Installatiekopieën van het particuliere** lijsten gespecialiseerde en gegeneraliseerd installatiekopieën van virtuele machines die u hebt gemaakt.
     
     toolearn over gespecialiseerde en gegeneraliseerde virtuele machines, Zie [VM-installatiekopie](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Zie [hoe tooCapture een tooUse virtuele Windows-computer als een sjabloon](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) voor meer informatie over hoe een virtuele machine naar een sjabloon waarmee u tooquickly kunt maken van nieuwe tooturn vooraf virtuele machines geconfigureerde.
     
     U kunt klikken op een virtuele machine installatiekopie naam toosee informatie over de installatiekopie van het Hallo aan de rechterkant Hallo van Hallo pagina.
     
     > [!NOTE]
     > U kunt geen virtuele machine installatiekopieën toohello toevoegen **openbare afbeeldingen** of **MSDN-installatiekopieën** geeft een lijst van omdat ze alleen-lezen. Alle virtuele machines die u maakt worden toegevoegd toohello **persoonlijke afbeeldingen** lijst.
     > 
     > 
     
     Als u een MSDN-abonnee met een abonnement van de Visual Studio-niveau, kunt u een vooraf gemaakte virtuele machine van Azure met Visual Studio, evenals enkele andere afbeeldingen. Zie voor meer informatie [een virtuele Machine maken in Visual Studio door de installatiekopie met behulp van installatiekopieën van Visual Studio 2013-galerie voor MSDN-abonnees](http://visualstudio2013msdngalleryimage.azurewebsites.net) en [MSDN-abonnement](https://www.visualstudio.com/products/msdn-subscriptions-vs). |
5. Op Hallo **basisinstellingen van de virtuele Machine** pagina, voer de machinenaam van een en voegt u Hallo specificaties voor Hallo virtuele machine, met inbegrip van de grootte van hello, en een gebruikersnaam en wachtwoord. Wanneer u bent klaar, klikt u op **volgende**.
   
    Gebruikt u de nieuwe naam Hallo en toolog in Hallo-machine met behulp van extern bureaublad, dus is het een goed idee toowrite ze omlaag u in geval wachtwoord vergeet. Nadat u een virtuele machine van Azure in Visual Studio hebt gemaakt, kunt u de grootte en andere instellingen in Hallo [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Als u grotere voor Hallo virtuele machine kiest, kunnen extra kosten toepassen. Zie [prijsinformatie voor virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/) voor meer informatie.
   > 
   > 
6. Virtuele machines die zijn gemaakt in Visual Studio vereisen een cloudservice. Op Hallo **Cloud Service-instellingen** pagina, selecteert u een cloudservice voor Hallo virtuele machine of klik op **< Nieuw >** in de vervolgkeuzelijst Hallo als u een cloud service- of toouse een nieuwe wilt nog niet hebt een. Een opslagaccount is ook vereist, dus kiest u een opslagaccount (of een nieuw opslagaccount maken) in Hallo **opslagaccount** vervolgkeuzelijst. Zie [tooMicrosoft inleiding Azure Storage](../articles/storage/common/storage-introduction.md) voor meer informatie.
7. Als u wilt toospecify een virtueel netwerk (dit is optioneel), selecteert u deze in Hallo virtueel netwerk en Subnet dropdown keuzelijsten.
   
    Virtuele machines die deel uitmaken van een beschikbaarheidsset zijn geïmplementeerde toodifferent domeinen met fouten. Zie [Azure Virtual Network](https://azure.microsoft.com/services/virtual-network/) voor meer informatie.
8. Als u wilt dat uw virtuele machine toobelong tooan beschikbaarheidsset (ook optioneel), selecteert u Hallo **opgeven van een beschikbaarheidsset** selectievakje in en kies vervolgens een beschikbaarheidsset in de vervolgkeuzelijst Hallo. Wanneer u bent klaar, kiest u Hallo **volgende** knop.
   
    Toevoegen van uw virtuele machine tooan helpt beschikbaarheidsset uw toepassing beschikbaar blijven tijdens netwerkfouten, hardwarefouten lokale schijf en geplande uitvaltijd. U moet toouse hello [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103) toocreate virtuele netwerken, subnetten en beschikbaarheid ingesteld. Zie [beheren Hallo beschikbaarheid van virtuele Machines](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) voor meer informatie.
9. Op Hallo **eindpunten** pagina, Hallo openbare eindpunten die u beschikbaar toousers van uw virtuele machine wilt opgeven. Bijvoorbeeld, u kunt ervoor kiezen tooenable HTTP (poort 80) bovendien toohello extern bureaublad en PowerShell-eindpunten die zijn standaard ingeschakeld. tooadd een eindpunt, kiest u een in Hallo **poortnaam** vervolgkeuzelijst in een keuzelijst en kies vervolgens Hallo **toevoegen** knop. tooremove een eindpunt, kies Hallo rode **X** volgende toohello-naam in de lijst met eindpunten Hallo.
   
    ![Hallo eindpunten pagina in Hallo virtuele machines wizard.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    Hallo-eindpunten die beschikbaar zijn, is afhankelijk van Hallo-cloudservice die u hebt geselecteerd voor uw virtuele machine. Zie [Azure Service-eindpunten](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) voor meer informatie.
   
   > [!NOTE]
   > Inschakelen van openbare eindpunten services maakt op de virtuele machine beschikbaar toohello internet. Ervoor tooinstall zijn en goed Hallo eindpunten en services configureren op de virtuele machine, zoals instelling toegangsbeheerlijsten (ACL's) voor eindpunten Hallo. Zie [hoe tooSet Up eindpunten tooa virtuele Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) voor meer informatie.
   > 
   > 
10. Nadat u de instellingen van de virtuele machine configureren Hallo bent klaar, kiest u Hallo **maken** knop toocreate Hallo virtuele machine.
    
     Omdat Azure Hallo virtuele machine maakt, Hallo **Azure Activity Log** toont de voortgang van de bewerking voor het maken van virtuele machine Hallo Hallo.
    
     ![Virtuele machine-activiteitenlogboek - uitgevoerd.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     informatie van de virtuele machine die alleen tooview, kies Hallo **virtuele Machines** tabblad in Hallo **Azure Activity Log**.
    
     ![Activiteitenlogboek van virtuele machine - voltooid.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Als het Hallo-bewerking is voltooid, Hallo nieuwe virtuele machine moet worden weergegeven onder Hallo **virtuele Machines** knooppunt in Server Explorer. U kunt zich aanmelden bij deze door te klikken op Hallo **verbinding maken met behulp van extern bureaublad** snelkoppeling.
    
     ![Virtuele machine wordt weergegeven in Server Explorer.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Uw virtuele machines beheren
Op de virtuele machine configuratiepagina Hallo bovendien tooshutting omlaag, verbinding te maken, te vernieuwen en toe te voegen controlepunten toohello geselecteerd virtuele machine, u kunt ook weergeven of wijzigen van instellingen voor Hallo virtuele machine. U kunt:

* De grootte van de virtuele machine Hallo wijzigen.
* Selecteer Hallo beschikbaarheidsset toouse met Hallo virtuele machine.
* Toevoegen, verwijderen of wijzigen van instellingen voor openbare eindpunten.
* Toevoegen, verwijderen of extensies van virtuele machine configureren.
* Informatie weergeven over Hallo-schijven die zijn gekoppeld aan Hallo virtuele machine.

### <a name="view-or-change-virtual-machine-settings"></a>Instellingen van de virtuele machine weergeven of wijzigen
1. Kies uw virtuele machine in Hallo in Server Explorer **Azure Virtual Machines** knooppunt.
2. Kies in het snelmenu hello, **configureren** configuratiepagina voor tooview Hallo virtuele machine.
   
    ![pagina Hallo virtuele machine van Azure-configuratie](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Hallo-gegevens virtuele machine weergeven of wijzigen.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Opslaan of Hallo status van uw virtuele machine herstellen
Zoals u uw virtuele machine configureren en software op deze installeren, is het een goed idee tooregularly Sla uw voortgang door het maken van controlepunten voor virtuele machines. Een controlepunt is geen momentopname of een installatiekopie van de huidige status Hallo van uw virtuele machine. Als er iets mis met Hallo virtuele machine gaat, of u tooreconfigure Hallo virtuele machine wilt, kunt u tijd besparen door dat deze wordt hersteld tooa vorige controlepunt staat in plaats van vanaf het begin beginnen.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate controlepunt van virtuele machines
1. Kies uw virtuele machine in Hallo in Server Explorer **Azure Virtual Machines** knooppunt.
2. Kies in het snelmenu hello, **configureren** configuratiepagina voor tooview Hallo virtuele machine.
3. Kies op de configuratiepagina Hallo Hallo **installatiekopie vastleggen** knop.
   
    ![Knop voor configuratie van Azure-pagina vastleggen](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Hallo **virtuele Machine vastleggen** dialoogvenster wordt weergegeven.
   
    ![In het dialoogvenster Azure capture-virtuele machine](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Geef een label van de installatiekopie en de beschrijving. Een standaardlabel en een beschrijving zijn opgegeven, maar u kunt deze desgewenst door uw eigen overschrijven.
5. Als u al hebt Sysprep uitgevoerd op deze virtuele machine, selecteert u Hallo **ik heb Sysprep uitgevoerd op de virtuele machine van Hallo** vak.
   
    Sysprep is een hulpprogramma dat onder andere systemen-specifieke gegevens verwijdert uit Hallo virtuele machine-versie van Windows, waardoor het sjabloon dat anderen kunnen gebruiken. Zie [hoe tooCapture een tooUse virtuele Windows-computer als een sjabloon](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) voor meer informatie. Back-up Hallo VM voordat Sysprep wordt uitgevoerd.
6. Nadat u klaar bent met het configureren van Hallo vastleggingsinstellingen kiest Hallo **vastleggen** knop toocreate Hallo controlepunt.
   
    Omdat Azure Hallo controlepunt maakt, Hallo **Azure Activity Log** toont de voortgang van de bewerking Hallo Hallo.
   
    ![Vastleggen van een controlepunt van virtuele machines](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Wanneer Hallo controlepunt-bewerking is voltooid, wordt deze weergegeven in Hallo **Azure Activity Log**.
   
    ![Controlepunt is voltooid](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>controlepunten voor virtuele machines toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>een virtuele machine tooa toorestore eerder opgeslagen status
* Hallo stappen die worden beschreven in [stapsgewijze: uitvoeren Cloud herstelt van Microsoft Azure Virtual Machines met behulp van PowerShell - deel 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>een controlepunt toodelete
1. Ga toohello [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Kies op de virtuele machine configuratiepagina Hallo Hallo **installatiekopieën** tabblad bovenaan Hallo Hallo pagina.
3. Kies Hallo controlepunt u wilt toodelete en kies vervolgens Hallo **verwijderen** knop Hallo onder Hallo pagina aan.

## <a name="shut-down-your-virtual-machine"></a>De virtuele machine afsluiten
1. Kies in Server Explorer Hallo virtuele machine die u wilt dat tooshut omlaag in Hallo **Azure Virtual Machines** knooppunt.
2. In het snelmenu hello, kiest u Hallo **afsluiten** opdracht of kies **configureren** tooview Hallo configuratiepagina van de virtuele machine en kies vervolgens Hallo **afsluiten**knop.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het maken van virtuele machines, Zie [maken van een virtuele Machine waarop Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [maken van een virtuele machine waarop Windows wordt uitgevoerd in de Azure preview-portal Hallo](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

