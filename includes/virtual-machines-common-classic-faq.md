


In dit artikel komen enkele veelgestelde vragen gebruikers over Azure virtuele machines die zijn gemaakt met het klassieke implementatiemodel Hallo vragen.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Kan ik mijn VM gemaakt in Hallo klassieke model toohello nieuwe Resource Manager-implementatiemodel migreren?
Ja. Voor instructies over het toomigrate, Zie:

* [Migreren van klassieke tooAzure Resource Manager met Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migreren van klassieke tooAzure Resource Manager met Azure CLI](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>Wat kan ik uitvoeren op een VM van Azure?
Alle abonnees kunnen serversoftware uitvoeren op een virtuele machine van Azure. U kunt recente versies van Windows Server uitvoeren, evenals een aantal Linux-distributies. Zie deze artikelen voor meer informatie over ondersteuning:

• Voor VM's van Windows -- [Ondersteuning van Microsoft-serversoftware voor Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Voor VM's van Linux -- [Linux op door Azure goedgekeurde distributies](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Voor Windows client-installatiekopieën zijn bepaalde versies van Windows 7 en Windows 8.1 beschikbaar tooMSDN Azure voordeel abonnees en abonnees van een MSDN ontwikkelen en testen betalen naar gebruik voor ontwikkel- en taken. Zie het Engelstalige blogbericht [Windows Client images for MSDN subscribers](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/) voor meer informatie, zoals instructies en beperkingen.

## <a name="why-are-affinity-groups-being-deprecated"></a>Waarom worden affiniteitsgroepen afgeschaft?
Affiniteitsgroepen zijn een verouderd concept voor een geografische groepering van cloudservice-implementaties en opslagaccounts van een klant in Azure. Ze zijn oorspronkelijk tooimprove VM-VM netwerkprestaties in Hallo vroege Azure-netwerkontwerpen opgegeven. Ze ook ondersteund de eerste release Hallo van virtuele netwerken (vnet's) die beperkt tooa kleine set hardware in een regio zijn.

Hallo huidige Azure-netwerk in een regio is zodanig ontworpen dat affiniteitsgroepen niet langer vereist zijn. Virtuele netwerken ondersteunen nu ook een regionaal bereik en dus is een affiniteitsgroep niet meer vereist wanneer u een virtueel netwerk gebruikt. Vervaldatum toothese verbeteringen, niet langer wordt aangeraden dat klanten affiniteitsgroepen gebruiken omdat ze in sommige scenario's kunnen worden beperkt. Met behulp van affiniteitsgroepen koppelt uw virtuele machines toospecific hardware die de keuze van VM-grootten beschikbaar tooyou zijn Hallo beperkt onnodig. Het kan ook toocapacity gerelateerde fouten leiden wanneer u tooadd nieuwe virtuele machines probeert als Hallo specifieke hardware die is gekoppeld aan een affiniteitsgroep Hallo is bijna bereikt.

Affiniteitsgroep onderdelen zijn al afgeschaft in Azure Resource Manager-implementatiemodel hello en in hello Azure-portal. We zijn ondersteuning voor het maken van affiniteitsgroepen en storage-resources die vastgemaakt tooan affiniteitsgroep zijn maken bestandstypen voor Hallo klassieke Azure-portal. U hoeft niet toomodify bestaande cloud-services die van een affiniteitsgroep gebruikmaken. Het wordt echter afgeraden om affiniteitsgroepen te gebruiken voor nieuwe cloudservices, tenzij dit wordt geadviseerd door een ondersteuningsmedewerker van Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Hoeveel opslagruimte kan ik gebruiken met een virtuele machine?
Elke gegevensschijf kan zijn van too1 TB. Hallo aantal gegevensschijven die u kunt gebruiken, is afhankelijk van Hallo grootte van Hallo virtuele machine. Zie [Grootten voor virtuele machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

Een Azure storage-account biedt opslag voor de besturingssysteemschijf hello en eventuele gegevensschijven. Elke schijf is een VHD-bestand dat wordt opgeslagen als een pagina-blob. Zie [deze pagina](http://go.microsoft.com/fwlink/p/?LinkId=396819) voor prijsinformatie.

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Welke typen virtuele harde schijf kan ik gebruiken?
Azure ondersteunt alleen vaste, virtuele harde schijven met de indeling VHD. Als u een VHDX die u wilt dat toouse in Azure hebt, moet u toofirst converteert u deze met behulp van Hyper-V-beheer of Hallo [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. Nadat u dat doet, gebruikt u [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet (in de modus van de Service Management) tooupload Hallo VHD tooa storage-account in Azure, zodat u deze met virtuele machines gebruiken kunt.

* Zie voor instructies voor Linux [maakt en uploadt u een virtuele harde schijf met Linux-besturingssysteem Hallo](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Zie voor instructies voor Windows [maken en uploaden van een Windows Server-VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Zijn dat deze virtuele machines Hallo hetzelfde als Hyper-V virtuele machines?
Op vele manieren ze zijn vergelijkbaar te 'Generatie 1' Hyper-V-machines, maar ze zijn niet precies Hallo dezelfde. Beide typen bieden gevirtualiseerde hardware, en virtuele harde schijven in VHD-indeling met Hallo compatibel zijn. Dit betekent dat u ze kunt verplaatsen tussen Hyper-V en Azure. Er zijn echter drie belangrijke verschillen die gebruikers van Hyper-V soms verrassen:

* Azure biedt niet console toegang tooa virtuele machine. Er is geen tooaccess manier een virtuele machine totdat dit is gedaan opstarten.
* VM's van Azure hebben in de meeste [grootten](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) maar één virtuele netwerkadapter, wat betekent dat ze ook maar één extern IP-adres kunnen hebben. (Hallo A8 en A9-groottes gebruiken een tweede netwerkadapter voor de toepassing communicatie tussen exemplaren in beperkte scenario's.)
* VM's van Azure bieden geen ondersteuning voor functies van Hyper-V-VM's van de tweede generatie. Zie voor meer informatie over deze functies [Specificaties van virtuele machines voor Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) en [Overzicht van virtuele machines van generatie 2](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Kunnen deze virtuele machines mijn bestaande, on-premises netwerkinfrastructuur gebruiken?
Voor virtuele machines in het klassieke implementatiemodel Hallo hebt gemaakt, kunt u Azure Virtual Network tooextend uw bestaande infrastructuur. Hallo-methode is vergelijkbaar met een filiaal instellen. U kunt inrichten en beheren van virtuele particuliere netwerken (VPN's) in Azure, alsmede veilig verbinding kunnen maken ze tooon-premises IT-infrastructuur. Zie [Overzicht van Azure Virtual Network](../articles/virtual-network/virtual-networks-overview.md) voor meer informatie.

U moet toospecify Hallo netwerk op dat u wilt Hallo van virtuele machine toobelong toowhen u Hallo virtuele machine maken. U kunt een bestaand virtueel netwerk voor virtuele machine tooa kan niet deelnemen aan. U kunt echter dit probleem omzeilen door Hallo virtuele harde-schijf (VHD) van de bestaande virtuele machine Hallo loskoppelen en vervolgens worden gebruikt toocreate een nieuwe virtuele machine met de gewenste Hallo-netwerkconfiguratie.

## <a name="how-can-i-access--my-virtual-machine"></a>Hoe krijg ik toegang tot mijn virtuele machine?
U moet tooestablish een verbinding met extern toolog op toohello virtuele machine via Extern bureaublad-verbinding voor een virtuele machine van Windows of een "Secure Shell" (SSH) voor een Linux-VM. Instructies vindt u hier:

* [Hoe tooLog op virtuele Machine Running Windows Server tooa](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Maximaal 2 gelijktijdige verbindingen worden ondersteund, tenzij het Hallo-server is geconfigureerd als een extern bureaublad-Services sessiehost.  
* [Hoe tooLog op virtuele Machine waarop Linux tooa](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). SSH biedt standaard ondersteuning voor maximaal tien gelijktijdige verbindingen. U kunt dit getal verhogen door Hallo-configuratiebestand bewerken.

Als u problemen met extern bureaublad of SSH ondervindt, installeren en gebruiken van Hallo [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extensie toohelp fix Hallo probleem.

Voor Windows-VM's gelden nog deze extra opties:

* In klassieke Azure-portal hello, Hallo VM zoeken en klik vervolgens op **externe toegang opnieuw instellen** uit Hallo opdrachtbalk.
* Bekijk [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Gebruik Windows PowerShell voor externe toegang tooconnect toohello VM of extra eindpunten voor andere resources tooconnect toohello VM maken. Zie voor meer informatie [hoe tooSet Up eindpunten tooa virtuele Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Als u bekend met Hyper-V bent, kijkt u misschien voor een vergelijkbaar tooVMConnect hulpprogramma. Azure biedt geen een vergelijkbaar hulpprogramma bieden omdat console toegang tooa virtuele machine wordt niet ondersteund.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Kan ik Hallo tijdelijke schijf (hello D: station voor Windows of /dev/sdb1 voor Linux) toostore gegevens gebruiken?
U kunt Hallo tijdelijke schijf (hello D: station voor Windows of /dev/sdb1 voor Linux) toostore gegevens niet gebruikt. Deze schijven zijn alleen als tijdelijke opslag bedoeld, wat betekent dat u het risico loopt gegevens kwijt te raken die dan niet kunnen worden hersteld. Dit kan gebeuren wanneer Hallo virtuele machine wordt verplaatst tooa andere host. Grootte wijzigen van een virtuele machine, zijn Hallo host of een hardwarefout op Hallo host bijwerken Hallo redenen die een virtuele machine mogelijk verplaatsen.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Hoe kan ik de stationsletter op Hallo van de tijdelijke schijf Hallo wijzigen?
Op een virtuele machine van Windows, kunt u de stationsletter Hallo door bewegende Hallo wisselbestand en stationsletters opnieuw toewijzen, maar moet u zeker dat u de stappen in een bepaalde volgorde Hallo toomake. Zie voor instructies [wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Hoe kan ik Hallo gastbesturingssysteem bijwerken?
Hallo term upgrade betekent meestal bewegende tooa meer recente versie van het besturingssysteem bijwerkt op Hallo dezelfde hardware. Hallo proces voor het verplaatsen van tooa voor Azure VM's meer recente versie verschilt voor Linux en Windows:

* Gebruik Hallo pakket beheerhulpprogramma's en procedures die geschikt is voor de distributie van Hallo voor Linux VM's.
* Voor een virtuele machine van Windows moet u toomigrate Hallo server met behulp van ongeveer Hallo Windows Server Migration Tools. Niet tooupgrade Hallo gastbesturingssysteem proberen, terwijl deze deel van Azure uitmaakt. Dit wordt niet ondersteund vanwege Hallo risico van het verlies van toegang toohello virtuele machine. Als er problemen optreden tijdens de upgrade hello, kunt u verliezen Hallo mogelijkheid toostart een extern bureaublad sessie en kunnen tootroubleshoot Hallo problemen zou niet.

Raadpleeg voor algemene informatie over het Hallo-hulpprogramma's en processen voor het migreren van een Windows-Server [rollen en functies migreren tooWindows Server](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Wat is Hallo standaardgebruikersnaam en wachtwoord op Hallo virtuele machine?
Hallo-installatiekopieën die zijn verstrekt door Azure hebben niet vooraf geconfigureerde gebruikersnaam en een wachtwoord. Wanneer u een virtuele machine met een van deze installatiekopieën maakt, moet u tooprovide een gebruikersnaam en wachtwoord, gebruikt u toolog op toohello virtuele machine.

Als u Hallo-gebruikersnaam of wachtwoord bent vergeten, en u Hallo VM-Agent hebt geïnstalleerd, kunt u installeren en gebruiken van Hallo [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extensie toofix Hallo probleem.

Aanvullende details:

* Hallo Linux-installatiekopieën, als u Hallo klassieke Azure-portal gebruikt, 'azureuser' wordt weergegeven als een standaardnaam van de gebruiker maar u kunt dit wijzigen met behulp van 'Van galerie' in plaats van snelle invoer als Hallo manier toocreate Hallo virtuele machine. Met behulp van Galerij kunt u ook bepalen of toouse een wachtwoord, een SSH-sleutel, of beide toolog u in. Hallo gebruikersaccount is een niet-gemachtigde gebruiker met 'sudo ' uitgebreid toegang toorun bevoegde opdrachten. Hallo 'root'-account is uitgeschakeld.
* Voor Windows-installatiekopieën moet u tooprovide een gebruikersnaam en wachtwoord bij het maken van Hallo VM. Hallo-account wordt de groep Administrators toohello toegevoegd.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Kan Azure een antivirusprogramma uitvoeren op mijn virtuele machines?
Azure biedt verschillende opties voor antivirus-oplossingen, maar is tooyou toomanage deze. Bijvoorbeeld, moet u mogelijk een afzonderlijk abonnement voor antimalware-software en moet u toodecide wanneer toorun gescand en updates installeren. U kunt ondersteuning voor een antivirusprogramma toevoegen met behulp van een VM-extensie voor Microsoft Antimalware, Symantec Endpoint Protection of TrendMicro Deep Security Agent wanneer u een virtuele Windows-computer maakt. Dit kan trouwens ook op een later tijdstip. Hallo Symantec en TrendMicro uitbreidingen kunnen u een gratis proefabonnement voor tijdelijke of een bestaand enterprise-abonnement gebruiken. Microsoft Antimalware is gratis. Zie deze artikelen voor meer informatie:

* [Hoe tooinstall en Symantec Endpoint Protection configureren op een virtuele machine in Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Hoe tooinstall en Trend Micro grondige Security configureren als een Service op een Azure VM](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Deploying Antimalware Solutions on Azure Virtual Machines](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/) (Antimalware-oplossingen implementeren op virtuele machines van Azure)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Wat zijn de opties voor back-up en herstel?
Azure Backup is beschikbaar als preview in bepaalde regio's. Zie [Back-ups maken van virtuele machines van Azure](../articles/backup/backup-azure-vms.md) voor meer informatie. Andere oplossingen zijn beschikbaar van gecertificeerde partners. toofind informatie over wat er momenteel beschikbaar is, zoek hello Azure Marketplace.

Een extra optie is toouse hello momentopnamefunctionaliteit van blob-opslag. toodo, moet u tooshut omlaag Hallo VM voordat de bewerking die afhankelijk van een momentopname van een blob is. Schrijfbewerkingen die nog moeten worden opgeslagen en plaatst het Hallo-bestandssysteem een consistente status.

## <a name="how-does-azure-charge-for-my-vm"></a>Hoe worden er in Azure kosten in rekening gebracht voor mijn VM?
Azure rekent een uurprijs op basis van de grootte en het besturingssysteem Hallo van de virtuele machine. Voor de hele uren Azure rekent alleen voor Hallo minuten van gebruik. Als u Hallo VM met een VM-installatiekopie met bepaalde vooraf geïnstalleerde software maakt, kunnen extra kosten voor elk uur software toepassen. Azure kosten voor opslag voor het besturingssysteem en de gegevensschijven Hallo van de virtuele machine afzonderlijk. Tijdelijke opslagruimte is gratis.

U in rekening gebracht wanneer Hallo VM-status uitgevoerd of gestopt wordt, maar er niet in rekening gebracht zijn wanneer Hallo VM-status is gestopt (ongedaan toegewezen). een virtuele machine in Hallo tooput gestopt (ongedaan toegewezen) staat, doe een van de volgende Hallo:

* Afgesloten of Hallo VM verwijderen uit Hallo klassieke Azure-portal.
* Gebruik Hallo Stop-AzureVM cmdlet, die beschikbaar zijn in hello Azure PowerShell-module.
* Hallo afsluiten rol bewerking gebruiken in Hallo REST API van Opslagservicebeheer en StoppedDeallocated voor Hallo PostShutdownAction element opgeven.

Zie [Prijzen van virtuele machines](https://azure.microsoft.com/pricing/details/virtual-machines/) voor meer informatie.

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Wordt mijn VM opnieuw opgestart door Azure voor onderhoud?
Azure uw virtuele machine wordt soms ook opnieuw opgestart als onderdeel van de reguliere en geplande onderhoud updates in hello Azure-datacenters.

Niet-gepland onderhoudsgebeurtenissen kunnen optreden wanneer Azure een ernstige hardwareprobleem vaststelt dat betrekking heeft op uw VM. Voor niet-geplande gebeurtenissen Azure automatisch Hallo VM tooa orde host wordt gemigreerd en Hallo VM opnieuw wordt opgestart.

Voor een zelfstandige virtuele machine (wat betekent Hallo VM maakt geen deel uit van een beschikbaarheidsset), Azure waarschuwt servicebeheerder Hallo-abonnement via e-mail ten minste één week voor gepland onderhoud omdat Hallo VMs kan opnieuw worden gestart tijdens het Hallo bijwerken. Toepassingen die worden uitgevoerd op virtuele machines Hallo kunnen krijgen met uitvaltijd.

Ook kunt u Azure PowerShell tooview Hallo opnieuw opstarten Logboeken of de klassieke Azure-portal Hallo wanneer opnieuw opstarten Hallo vanwege tooplanned onderhoud opgetreden. Zie voor meer informatie [VM-opstartlogboeken bekijken](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

tooprovide redundantie, plaats twee of meer op dezelfde manier geconfigureerd virtuele machines in Hallo dezelfde beschikbaarheidsset. Op deze manier zorgt u ervoor dat er ten minste één VM beschikbaar is tijdens gepland of ongepland onderhoud. Azure garandeert bepaalde niveaus van VM-beschikbaarheid voor deze configuratie. Zie voor meer informatie [Hallo beschikbaarheid van virtuele machines beheren](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Aanvullende bronnen
[Informatie over Azure Virtual Machines](../articles/virtual-machines/virtual-machines-linux-about.md)

[Maken en beheren van virtuele Linux-machines met hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Windows-VM's maken en beheren met Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

