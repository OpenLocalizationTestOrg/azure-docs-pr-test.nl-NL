Azure virtuele machines (VM's) kunnen soms opnieuw worden opgestart voor geen zichtbare reden, zonder bewijs van uw hebben gestart bewerking Hallo-opnieuw opstarten. Dit artikel worden Hallo acties en gebeurtenissen die kunnen leiden tot virtuele machines tooreboot en biedt inzicht in hoe tooavoid onverwachte problemen opnieuw opstarten of de Hallo gevolgen van dergelijke problemen.

## <a name="configure-hello-vms-for-high-availability"></a>Hallo VM's voor hoge beschikbaarheid configureren
Hallo aanbevolen manier tooprotect een toepassing die wordt uitgevoerd op Azure tegen VM opnieuw wordt opgestart en de uitvaltijd tooconfigure Hallo VM's voor hoge beschikbaarheid.

Dit niveau van redundantie tooyour toepassing tooprovide, wordt aangeraden dat u twee of meer virtuele machines in een beschikbaarheidsset groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de 99,95% Hallo [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Zie voor meer informatie over beschikbaarheidssets Hallo artikelen te volgen:

- [Hallo-beschikbaarheid van virtuele machines beheren](../articles/virtual-machines/windows/manage-availability.md)
- [Beschikbaarheid van virtuele machines configureren](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Statusgegevens van de resource 
Azure resourcestatus is een service die beschrijft Hallo status van afzonderlijke Azure-resources en biedt bruikbare richtlijnen voor het oplossen van problemen. In een omgeving waar het is niet mogelijk toodirectly-servers voor clienttoegang of Infrastructuurelementen, is Hallo doel van de resourcestatus tooreduce Hallo die u aan het oplossen van problemen besteden. Hallo-doel is met name tooreduce Hallo tijd nodig voor het bepalen of Hallo hoofdmap van Hallo probleem wordt veroorzaakt in Hallo toepassing of in een gebeurtenis binnen hello Azure-platform. Zie voor meer informatie [Understand and gebruik resourcestatus](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Acties en gebeurtenissen die leiden Hallo VM tooreboot tot kunnen

### <a name="planned-maintenance"></a>Gepland onderhoud
Microsoft Azure voert regelmatig updates via Hallo wereld tooimprove Hallo betrouwbaarheid, prestaties en beveiliging van Hallo host infrastructuur waarop virtuele machines. Veel van deze updates, waaronder geheugen behouden updates worden uitgevoerd zonder invloed op uw virtuele machines of cloudservices.

Sommige updates vereisen echter opnieuw worden opgestart. In dergelijke gevallen zijn Hallo VM's afgesloten terwijl we Hallo infrastructuur patch en vervolgens Hallo virtuele machines opnieuw worden gestart.

toounderstand welke Azure gepland onderhoud is en hoe dit invloed heeft op Hallo beschikbaarheid van uw virtuele Linux-machines, Zie Hallo artikelen die hier worden vermeld. Hallo artikelen vindt u achtergrondinformatie over hello Azure gepland onderhoudsproces en hoe tooschedule gepland onderhoud toofurther de Hallo gevolgen.

- [Gepland onderhoud voor virtuele machines in Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Hoe tooschedule gepland onderhoud op Azure Virtual machines](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Updates met geheugenbehoud   
Gebruikers krijgen voor deze klasse van updates in Microsoft Azure, niet van invloed op de actieve virtuele machines. Veel van deze updates zijn toocomponents of services die kunnen worden bijgewerkt zonder interactie aangaan met Hallo met een exemplaar. Sommige zijn platform infrastructuurupdates op Hallo hostbesturingssysteem die kunnen worden toegepast zonder Hallo virtuele machines opnieuw worden opgestart.

Deze updates met behoud van geheugen worden bewerkstelligd met-technologie waarmee in-place live migratie. Wanneer deze wordt bijgewerkt, Hallo VM wordt geplaatst in een *onderbroken* status. Deze status blijft Hallo RAM-geheugen behouden terwijl de onderliggende host-besturingssysteem Hallo Hallo vereiste updates en patches ontvangt. Hallo VM hervat binnen 30 seconden wordt onderbroken. De klok wordt na Hallo die VM wordt hervat, automatisch gesynchroniseerd.

Vanwege Hallo korte pauze periode vermindert aanzienlijk implementeren van updates via dit mechanisme Hallo impact op Hallo van virtuele machines. Niet alle updates kunnen echter op deze manier worden geïmplementeerd. 

Meerdere exemplaren updates (voor VM's in een beschikbaarheidsset) zijn toegepaste één updatedomein tegelijk.

> [!NOTE]
> Linux-machines met oude versie van de kernel een zijn beïnvloed door een paniek kernel tijdens deze updatemethode. tooavoid dit probleem, update tookernel versie 3.10.0-327.10.1 of hoger. Zie voor meer informatie [An Azure virtuele Linux-machine op een kernel 3.10 gebaseerde panics na de upgrade van een host knooppunt](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Gebruiker gestart opnieuw opstarten of afsluiten acties
 
Als u opnieuw opstarten vanuit hello Azure-portal, Azure PowerShell, opdrachtregelinterface of API opnieuw uitvoert, kunt u Hallo gebeurtenis vinden in Hallo [Azure Activity Log](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Als u Hallo actie van het besturingssysteem Hallo van de virtuele machine uitvoert, kunt u Hallo-gebeurtenis in het systeemlogboek in Logboeken Hallo vinden.

Andere scenario's die doorgaans Hallo VM tooreboot veroorzaken bevatten meerdere configuratiewijziging acties. Normaal gesproken ziet u een waarschuwing die aangeeft dat de uitvoering van een bepaalde actie leidt ertoe dat Hallo VM opnieuw worden opgestart. Voorbeelden zijn VM formaat bewerkingen, wachtwoord op Hallo van Hallo Administrator-account wijzigen en het instellen van een statisch IP-adres.

### <a name="azure-security-center-and-windows-update"></a>Azure Security Center en Windows Update
Azure Security Center bewaakt dagelijkse Windows en Linux VM's voor het besturingssysteem updates ontbreken. Security Center haalt een lijst met beschikbare beveiligingsupdates en essentiële updates via Windows Update of Windows Server Update Services (WSUS), afhankelijk van welke service is geconfigureerd op een virtuele machine van Windows. Security Center controleert ook of de meest recente updates Hallo voor Linux-systemen. Als uw VM een systeemupdate ontbreekt is, wordt door Security Center adviseert systeemupdates toe te passen. Hallo-toepassing van deze systeemupdates wordt geregeld via Hallo Security Center in hello Azure-portal. Nadat u de updates hebt toegepast, is het mogelijk dat virtuele machine opnieuw opstarten vereist. Zie voor meer informatie [toepassen systeemupdates in Azure Security Center](../articles/security-center/security-center-apply-system-updates.md).

Zoals lokale servers biedt Azure geen push-updates van Windows Update tooWindows Azure virtuele machines, omdat deze machines beoogde toobe beheerd door hun gebruikers. U bent, echter aangemoedigd tooleave Hallo automatisch Windows Update-instelling is ingeschakeld. Automatische installatie van updates van Windows Update kan ook leiden tot toooccur opnieuw wordt opgestart nadat het Hallo-updates worden toegepast. Zie voor meer informatie [Veelgestelde vragen over de Windows Update](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>In andere gevallen die invloed hebben op Hallo beschikbaarheid van uw virtuele machine
Er zijn andere gevallen waarin Azure actief Hallo gebruik van een virtuele machine mogelijk onderbreken. U ontvangt e-mailmeldingen voordat deze actie wordt ondernomen, dus u hebt een kans tooresolve Hallo onderliggende problemen. Voorbeelden van problemen die invloed hebben op de beschikbaarheid van de VM zijn beveiligingsschendingen en Hallo verlopen van betalingswijzen.

### <a name="host-server-faults"></a>Host-server-fouten 
Hallo VM wordt gehost op een fysieke server die wordt uitgevoerd binnen een Azure-datacenter. Hallo fysieke server wordt uitgevoerd een agent genoemd Hallo Hostagent in toevoeging tooa enkele andere Azure-onderdelen. Wanneer deze Azure softwareonderdelen op Hallo fysieke server reageert, activeert Hallo bewakingssysteem Hallo host serverherstelproces tooattempt opnieuw worden opgestart. Hallo VM vindt meestal binnen vijf minuten opnieuw en op dezelfde als eerder host Hallo toolive blijft.

Server-fouten worden gewoonlijk veroorzaakt door hardwarefouten, zoals Hallo uitval van een harde schijf of een SSD-schijf. Azure continu bewaakt deze instanties, identificeert Hallo onderliggende fouten, en de updates nadat Hallo risicobeperking is geïmplementeerd en getest.

Omdat sommige host-server-fouten specifieke toothat server zijn kunnen, mogelijk een situatie met een herhaalde VM opnieuw opstarten worden verbeterd door Hallo VM tooanother host-server handmatig opnieuw te distribueren. Deze bewerking kan worden geactiveerd met behulp van Hallo **implementeren** optie op de detailpagina Hallo Hallo VM of Hallo te stoppen en opnieuw starten van de VM in hello Azure-portal.

### <a name="auto-recovery"></a>Automatisch herstel
Als Hallo host-server kan niet opnieuw voor een of andere reden opgestart, initieert hello Azure-platform een automatisch herstel actie tootake Hallo defecte host-server buiten rotatie voor verder onderzoek. 

Alle virtuele machines op die host zijn automatisch verplaatste tooa afwijken, in orde host-server. Dit proces is meestal voltooid binnen 15 minuten. toolearn meer informatie over Hallo auto-herstelproces, Zie [automatisch herstel van virtuele machines](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Niet-gepland onderhoud
In zeldzame gevallen Hallo team van Azure-bewerkingen mogelijk moeten tooperform onderhoud activiteiten tooensure Hallo algemene status van hello Azure-platform. Dit probleem kan invloed hebben op de beschikbaarheid van de virtuele machine en meestal leidt dit tot Hallo dezelfde automatisch herstel actie zoals eerder beschreven.  

Niet-geplande maintenances zijn Hallo volgende:

- Urgente knooppunt defragmentatie
- Switch-updates voor urgente netwerk

### <a name="vm-crashes"></a>VM-crashes
Virtuele machines opnieuw opstarten vanwege problemen met binnen Hallo VM zelf. Hallo werkbelasting of rol die wordt uitgevoerd op Hallo VM mogelijk een controle bug in het gastbesturingssysteem Hallo geactiveerd. Voor hulp bij het bepalen Hallo reden voor de crash hello, Hallo systeem- en toepassingslogboeken voor Windows-VM's weergeven en hello seriële logboeken voor virtuele Linux-machines.

### <a name="storage-related-forced-shutdowns"></a>Opslag-gerelateerde geforceerd afsluiten
Virtuele machines in Azure, is afhankelijk van virtuele schijven voor het besturingssysteem en de opslag van gegevens die wordt gehost op Hallo Azure Storage-infrastructuur. Wanneer Hallo beschikbaarheid connectiviteit tussen Hallo VM en virtuele schijven die zijn gekoppeld Hallo is invloed op een of meer dan 120 seconden, voert hello Azure-platform geforceerd afsluiten Hallo VMs tooavoid gegevensbeschadiging. Hallo VM's worden automatisch ingeschakeld terug nadat de opslagverbinding is hersteld. 

Hallo duur Hallo afgesloten kan zo kort vijf minuten wel aanzienlijk langer. Hallo volgende is een van de specifieke gevallen Hallo die is gekoppeld aan de opslag-gerelateerde geforceerd afsluiten: 

**I/o van meer dan beperkt**

Virtuele machines is mogelijk tijdelijk afgesloten wanneer de i/o-aanvragen zijn consistent beperkt omdat Hallo volume van i/o-bewerkingen per seconde (IOPS) groter is dan Hallo i/o-limieten voor het Hallo-schijf. (Standaard schijfopslag is beperkt too500 IOPS.) toomitigate dit probleem Gebruik striping van de schijf of opslagruimte Hallo binnen Hallo Gast-VM, afhankelijk van de werkbelasting Hallo configureren. Zie voor meer informatie [Azure VM's configureren voor optimale opslagprestaties](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Hogere IOPS-limieten zijn beschikbaar via Azure Premium-opslag met up too80, 000 IOPS. Zie voor meer informatie [High-Performance Premium-opslag](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Andere incidenten
In zeldzame gevallen kan een probleem met de wijdverbreid kan invloed hebben op meerdere servers in een Azure-datacenter. Als dit probleem optreedt, verzendt Hallo team van Azure e-mail meldingen toohello van invloed op een abonnementen. U kunt controleren Hallo [Azure Service Health dashboard](https://azure.microsoft.com/status/) en hello Azure-portal voor Hallo status van actieve storingen en voorbij incidenten.
