## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Informatie over het opnieuw opstarten van VM's - onderhoud versus downtime
Er zijn drie scenario's die kunnen leiden toovirtual machine in Azure worden beïnvloed: niet-geplande hardwareonderhoud, onverwachte downtime en gepland onderhoud.

* **Niet-geplande Hardware onderhoud gebeurtenis** treedt op wanneer hello Azure-platform voorspelt die Hallo hardware of eventuele platform onderdeel gekoppeld tooa fysieke machine is over toofail. Wanneer het platform Hallo voorspelt een storing, geven deze een niet-geplande hardware onderhoud gebeurtenis tooreduce Hallo impact toohello virtuele machines die worden gehost op deze hardware. Azure maakt gebruik van livemigratie technologie toomigrate Hallo virtuele Machines van Hallo hardware tooa orde fysieke machine mislukken. Livemigratie wordt een virtuele machine bewerking dat alleen onderbroken virtuele Machine Hallo voor korte tijd te behouden. Geheugen, bestanden openen en netwerkverbindingen worden bewaard, maar mogelijk minder presteert voordat en/of na Hallo-gebeurtenis. In gevallen waarin livemigratie kan niet worden gebruikt, krijgen Hallo VM van onverwachte uitvaltijd, zoals hieronder wordt beschreven.


* **Een onverwachte Downtime** zelden treedt op wanneer het Hallo-hardware- of de fysieke infrastructuur Hallo onderliggende uw virtuele machine een fout in een bepaalde manier opgetreden is. Voorbeelden hiervan zijn lokale netwerkproblemen, lokale schijfdefecten of andere defecten op rack-niveau. Wanneer een dergelijke fout wordt gedetecteerd, hello Azure-platform worden automatisch gemigreerd (heals) uw virtuele machine tooa orde fysieke machine. Tijdens het Hallo herstel procedure, krijgen virtuele machines met uitvaltijd (opnieuw opstarten) en in sommige gevallen verlies van Hallo tijdelijke schijf. Hallo gekoppeld besturingssysteem en gegevensschijven altijd behouden. 

* **Gepland onderhoud gebeurtenissen** periodieke updates die zijn gemaakt door Microsoft toohello onderliggende Azure-platform tooimprove algehele betrouwbaarheid, prestaties en beveiliging van Hallo platforminfrastructuur die op uw virtuele machines worden uitgevoerd. Veel van deze updates worden uitgevoerd zonder dat dit van invloed is op uw virtuele machines of Cloud Services (zie [Onderhoud ter behoud van VM's](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Hello Azure-platform probeert toouse VM behouden onderhoud in alle mogelijke gevallen, zijn er zeldzame gevallen wanneer deze updates een herstart van de virtuele machine tooapply Hallo vereiste updates toohello onderliggende infrastructuur vereist. In dit geval kunt u Azure gepland onderhoud uitvoeren met onderhoud opnieuw bewerking Hallo onderhoud voor hun virtuele machines in de geschikte tijdvenster Hallo initiëren. Zie [Gepland onderhoud voor virtuele machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/) voor meer informatie.


tooreduce hello invloed de uitvaltijd vanwege tooone of meer van deze gebeurtenissen, raden we Hallo aanbevolen procedures van hoge beschikbaarheid voor uw virtuele machines te volgen:

* [Configureer meerdere virtuele machines in een beschikbaarheidsset voor redundantie]
* [Beheerde schijven voor virtuele machines in een beschikbaarheidsset gebruiken]
* [Gebruik gepland gebeurtenissen tooproactively antwoord tooVM die invloed hebben op gebeurtenissen] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configureer elke toepassingslaag in afzonderlijke beschikbaarheidssets]
* [Combineer het gebruik van een load balancer met beschikbaarheidssets]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configureer meerdere virtuele machines in een beschikbaarheidsset voor redundantie
tooprovide redundantie tooyour toepassing, wordt aangeraden dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan Hallo 99,95% Azure SLA. Zie voor meer informatie, Hallo [SLA voor virtuele Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Voorkom dat een virtuele machine met een enkele instantie als enige deel uitmaakt van een beschikbaarheidsset. Virtuele machines in deze configuratie komen niet in aanmerking voor een SLA-garantie en kunnen te maken krijgen met downtime bij geplande onderhoudswerkzaamheden aan het Azure-platform, tenzij een dergelijke enkele virtuele machine gebruikmaakt van [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md). Voor één virtuele machines met premium-opslag, hello Azure SLA van toepassing.

Elke virtuele machine in de beschikbaarheidsset is toegewezen een **updatedomein** en een **foutdomein** door Hallo onderliggende Azure-platform. Voor een opgegeven beschikbaarheidsset standaard vijf niet gebruiker configureerbare update domeinen zijn toegewezen (implementaties van Resource Manager kunnen vervolgens worden toegenomen tooprovide van too20 update domeinen) tooindicate groepen van virtuele machines en de onderliggende fysieke hardware dat kan worden opgestart op Hallo hetzelfde moment. Wanneer meer dan vijf virtuele machines worden geconfigureerd in een beschikbaarheidsset één, wordt Hallo zesde virtuele machine geplaatst in dezelfde update domein als de eerste virtuele machine Hallo Hallo zevende in dezelfde domein update Hallo tweede virtuele machine, en dus Hallo Hallo op. Hallo-volgorde van update-domeinen opnieuw wordt opgestart kan niet worden voortgezet sequentieel tijdens gepland onderhoud, maar slechts één updatedomein wordt opnieuw opgestart tegelijk. Een updatedomein opnieuw opgestart krijgt toorecover 30 minuten voordat de onderhoudsmodus wordt gestart op een andere update-domein.

Domeinen met fouten definiëren Hallo groep virtuele machines die een gemeenschappelijk power-bron- en switch delen. Standaard zijn Hallo virtuele machines zijn geconfigureerd in de beschikbaarheidsset gescheiden in up toothree foutdomeinen voor implementaties van Resource Manager (twee fault-domeinen voor klassieke). Terwijl uw virtuele machines in een beschikbaarheidsset plaatst, uw toepassing van het besturingssysteem of toepassing-specifieke fouten niet beveiligt biedt, wordt het Hallo-impact van mogelijke problemen met de fysieke hardware, netwerkstoringen of onderbrekingen van power beperkt.

<!--Image reference-->
   ![Conceptuele tekening Hallo update domein en de fout van de configuratie van](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Beheerde schijven voor VM's in een beschikbaarheidsset gebruiken
Als u momenteel virtuele machines met niet-beheerde schijven gebruikt, raden wij ten zeerste aan u [converteren van virtuele machines in de Beschikbaarheidsset toouse beheerd schijven](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Schijven die worden beheerd](../articles/virtual-machines/windows/managed-disks-overview.md) betere betrouwbaarheid voor Beschikbaarheidssets door ervoor te zorgen dat Hallo schijven van virtuele machines in een Beschikbaarheidsset voldoende zijn geïsoleerd van elkaar tooavoid individuele foutpunten opgeeft. Dit gebeurt door het plaatsen van automatisch Hallo schijven in de van verschillende opslagclusters. Als een opslagcluster vanwege toohardware-of softwarefout mislukt, niet alleen Hallo VM-instanties met schijven op die stempels.

![Foutdomeinen voor beheerde schijven](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> het aantal foutdomeinen voor beheerde beschikbaarheidssets Hallo varieert per regio - twee of drie per regio. Hallo bevat volgende tabel Hallo nummer per regio

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Als u van plan toouse virtuele machines met bent [zonder begeleiding schijven](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), volgt u onderstaande aanbevolen procedures voor het Storage-accounts waarbij virtuele harde schijven (VHD's) van virtuele machines worden opgeslagen als [pagina-blobs](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Alle schijven (OS en gegevens) die zijn gekoppeld aan een virtuele machine in Hallo houden hetzelfde opslagaccount**
2. **Bekijk Hallo [limieten](../articles/storage/common/storage-scalability-targets.md) op Hallo aantal niet-beheerde schijven in een opslagaccount** voordat u meer VHD's tooa storage-account toevoegt
3. **Gebruik een afzonderlijk opslagaccount voor elke virtuele machine in een beschikbaarheidsset.** Storage-accounts niet mag delen met meerdere virtuele machines in Hallo dezelfde Beschikbaarheidsset. Het is acceptabel voor virtuele machines in verschillende Beschikbaarheidssets tooshare storage-accounts als hierboven aanbevolen procedures zijn gevolgd

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configureer elke toepassingslaag in afzonderlijke beschikbaarheidssets
Als uw virtuele machines alle bijna identiek zijn en levert Hallo doel hetzelfde voor uw toepassing, het is raadzaam dat u een beschikbaarheidsset voor elke laag van uw toepassing configureren.  Als u twee verschillende plaatsen lagen in Hallo dezelfde beschikbaarheidsset, alle virtuele machines in Hallo dezelfde toepassingslaag kunt in één keer worden opgestart. Door voor elke laag ten minste twee virtuele machines in een beschikbaarheidsset te configureren, garandeert u dat in elke laag ten minste één virtuele machine beschikbaar is.

U kan bijvoorbeeld alle Hallo virtuele machines in Hallo-front-end van uw toepassing IIS, Apache, Nginx uitgevoerd in een enkel beschikbaarheidsset plaatst. Zorg ervoor dat alleen front-virtuele machines zijn geplaatst in Hallo dezelfde beschikbaarheidsset. Zorg er ook voor dat alleen virtuele machines uit de gegevenslaag in een eigen beschikbaarheidsset worden geplaatst, zoals gerepliceerde virtuele machines met SQL Server of virtuele machines met MySQL.

<!--Image reference-->
   ![Toepassingslagen](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combineer het gebruik van een load balancer met beschikbaarheidssets
Hallo combineren [Azure Load Balancer](../articles/load-balancer/load-balancer-overview.md) ingesteld met een beschikbaarheid tooget Hallo tolerantie voor de meeste toepassingen. Hello Azure Load Balancer wordt verkeer tussen meerdere virtuele machines. Hello Azure Load Balancer is voor virtuele machines met onze Standard-laag, opgenomen. Niet alle lagen van de virtuele machine zijn hello Azure Load Balancer. Zie voor meer informatie over het gebruik van load balancers voor uw virtuele machines [Taakverdeling voor virtuele machines](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Als Hallo load balancer niet is geconfigureerd toobalance verkeer over meerdere virtuele machines, en vervolgens een gebeurtenis gepland onderhoud is van invloed op Hallo alleen verkeer voor virtuele machine, veroorzaakt een storing tooyour toepassingslaag. Meerdere virtuele machines Hallo plaatsen laag dezelfde onder Hallo dezelfde load balancer en beschikbaarheid set kunnen verkeer toobe continu worden bediend door ten minste één exemplaar.


<!-- Link references -->
[Configureer meerdere virtuele machines in een beschikbaarheidsset voor redundantie]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configureer elke toepassingslaag in afzonderlijke beschikbaarheidssets]: #configure-each-application-tier-into-separate-availability-sets
[Combineer het gebruik van een load balancer met beschikbaarheidssets]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Beheerde schijven voor virtuele machines in een beschikbaarheidsset gebruiken]: #use-managed-disks-for-vms-in-an-availability-set
