Azure voert regelmatig updates tooimprove Hallo betrouwbaarheid, prestaties en beveiliging van de infrastructuur van Hallo host voor virtuele machines. Deze updates variëren van patchen softwareonderdelen in Hallo hostomgeving (zoals het besturingssysteem, hypervisor en verschillende agents die zijn geïmplementeerd op Hallo host) upgraden netwerkonderdelen, toohardware buiten gebruik stellen. Hallo meerderheid van deze updates worden uitgevoerd zonder gevolgen toohello gehoste virtuele machines. Er zijn echter gevallen bekend waarbij updates gevolgen:

- Als Hallo onderhoud niet opnieuw worden opgestart hoeft, gebruikt Azure in-place migratie toopause Hallo VM Hallo host wordt bijgewerkt.

- Als het onderhoud moet worden opgestart, krijgt u een bericht wanneer Hallo onderhoud is gepland. In dergelijke gevallen u ook krijgt een tijdvenster op waar u kunt beginnen Hallo onderhoud zelf tegelijk die geschikt is voor u.

Deze pagina wordt beschreven hoe Microsoft Azure uitvoert voor beide typen van onderhoud. Zie voor meer informatie over niet-geplande gebeurtenissen (uitval) beheren Hallo beschikbaarheid van virtuele machines voor [Windows] (... / articles/virtual-machines/windows/manage-availability.md) of [Linux](../articles/virtual-machines/linux/manage-availability.md).

Toepassingen die worden uitgevoerd in een virtuele machine kunt verzamelen informatie over toekomstige updates met behulp van hello Azure metagegevens Service voor [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) of [Linux] (... / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>In-place migratie voor VM

Als updates niet volledig opnieuw opstarten vereist, wordt een in-place live migratie wordt gebruikt. Tijdens het bijwerken van Hallo Hallo virtuele machine onderbroken ongeveer 30 seconden, Hallo geheugen in RAM, behouden terwijl Hallo hostomgeving Hallo vereiste updates en -patches toegepast. Hallo virtuele machine wordt vervolgens hervat en Hallo klok van Hallo virtuele machine automatisch wordt gesynchroniseerd.

Voor virtuele machines in beschikbaarheidssets, worden bijgewerkt een voor een update-domeinen. Alle virtuele machines in één updatedomein (UD) worden onderbroken, bijgewerkt en hervat vervolgens voordat gepland onderhoud op toohello verplaatst volgende UD.

Sommige toepassingen worden beïnvloed door deze typen updates. Toepassingen die uitvoeren van realtime-gebeurtenissen verwerken, zoals mediastreaming of transcodering of hoge doorvoersnelheid networking scenario's mogelijk niet ontworpen tootolerate een pauze van 30 seconde. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Onderhoud vereisen opnieuw opstarten

Wanneer virtuele machines opnieuw worden gestart voor gepland onderhoud toobe moeten, u een melding van tevoren. Gepland onderhoud heeft twee fasen: Hallo selfservice en een gepland onderhoud-venster.

Hallo **selfservice venster** kunt u Hallo onderhoud op uw virtuele machines starten. Gedurende deze tijd kunt u hun status van elke VM toosee opvragen en controleer of Hallo resultaat van de laatste aanvraag voor onderhoud.

Wanneer u onderhoud selfservice start, is uw virtuele machine verplaatst tooa-knooppunt dat al is bijgewerkt en wordt deze vervolgens weer ingeschakeld. Omdat Hallo VM opnieuw is opgestart, is Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.

Als u onderhoud selfservice start en er is een fout opgetreden tijdens het Hallo, Hallo-bewerking is gestopt, Hallo VM niet is bijgewerkt en deze ook verwijderd uit Hallo gepland onderhoud herhaling. U wordt verbinding gemaakt met in een later tijdstip met een nieuw schema en een nieuwe mogelijkheid toodo selfservice onderhoud aangeboden. 

Wanneer er Hallo selfservice venster is verstreken, Hallo **geplande onderhoudsvenster** begint. Tijdens dit tijdvenster kunt u nog steeds een query voor het onderhoudsvenster hello, maar niet langer kunnen toostart Hallo onderhoud zelf.

## <a name="availability-considerations-during-planned-maintenance"></a>Overwegingen voor beschikbaarheid tijdens gepland onderhoud 

Als u toowait besluit totdat Hallo onderhoudsvenster geplande, zijn er enkele dingen tooconsider voor het onderhouden van de hoogste availabilty Hallo van uw virtuele machines. 

### <a name="paired-regions"></a>Gekoppelde regio 's

Elke Azure-regio is gekoppeld aan een andere regio binnen Hallo hetzelfde Geografie samen een combinatie van regionale indienen. Azure wordt alleen Hallo virtuele machines in één regio uit een combinatie van regio bijgewerkt tijdens gepland onderhoud. Bijvoorbeeld bij het bijwerken van virtuele Machines in Noordelijk Centraal, VS hello Azure worden niet bijgewerkt in Zuid-centraal VS virtuele Machines op Hallo hetzelfde moment. Echter andere regio's, zoals Noord-Europa is in onderhoud op Hallo dezelfde tijd als VS-Oost. Uw VM's begrijpen hoe regio paren werken, kunt u beter verdelen over regio's. Zie voor meer informatie [Azure-regio paren](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Beschikbaarheidssets en schaalsets

Bij het implementeren van een werklast op Azure Virtual machines, kunt u Hallo virtuele machines binnen een beschikbaarheid set tooprovide hoge beschikbaarheid tooyour toepassing maken. Dit zorgt ervoor dat bij een stroomstoring of een onderhoud gebeurtenissen, ten minste één virtuele machine beschikbaar is.

Afzonderlijke virtuele machines worden in een beschikbaarheidsset verdeeld over van too20 update domeinen (UDs). Tijdens gepland onderhoud één updatedomein is dit van invloed op een bepaald moment. Let erop dat Hallo volgorde van update-domeinen die worden beïnvloed noodzakelijkerwijs niet opeenvolgend gebeurt. 

Virtuele-machineschaalsets zijn van een Azure compute resource waarmee u toodeploy en beheren van een set van identieke virtuele machines als één resource. Hallo scale set wordt automatisch geïmplementeerd in meerdere domeinen van de update, zoals virtuele machines in een beschikbaarheidsset. Net als met beschikbaarheidssets met schaalsets één updatedomein is dit van invloed op een bepaald moment.

Zie voor meer informatie over het configureren van uw virtuele machines voor maximale beschikbaarheid beheren Hallo beschikbaarheid van uw virtuele machines voor Windows (.. / articles/virtual-machines/windows/manage-availability.md) of [Linux](../articles/virtual-machines/linux/manage-availability.md).
