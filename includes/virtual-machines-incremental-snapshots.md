# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen
## <a name="overview"></a>Overzicht
Azure-opslag biedt de mogelijkheid van Hallo tootake momentopnamen van blobs. Hallo blob status vastleggen momentopnamen op dat moment. In dit artikel beschrijft we een scenario waarin u back-ups van de schijven van de virtuele machine met momentopnamen kunt onderhouden. U kunt deze methode wanneer u ervoor geen toouse kiest Azure Backup en Recovery-Service en desgewenst toocreate een aangepaste back-upstrategie voor uw virtuele machine-schijven.

Virtuele machine van Azure-schijven zijn opgeslagen als pagina-blobs in Azure Storage. Aangezien we beschrijving van een back-upstrategie voor virtuele-machineschijven in dit artikel, verwijzen we toosnapshots in de context Hallo van pagina-blobs. toolearn meer informatie over de momentopnamen te verwijzen[maken van een momentopname van een Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

## <a name="what-is-a-snapshot"></a>Wat is er een momentopname?
Een blob-momentopname is een alleen-lezen-versie van een blob die is opgenomen op een punt in tijd. Wanneer een momentopname is gemaakt, kan deze worden gelezen, gekopieerd, of verwijderd, maar niet gewijzigd. Momentopnamen bieden een manier tooback van een blob, zoals deze wordt weergegeven op een moment. Pas REST versie 2015-04-05 moest u Hallo mogelijkheid toocopy volledige momentopnamen. Met de Hallo REST versie 2015-07-08 en hoger, u kunt u ook incrementele momentopnamen kopiëren.

## <a name="full-snapshot-copy"></a>Volledige momentopname kopiëren
Momentopnamen kunnen worden gekopieerd tooanother storage-account als een back-ups tookeep blob van Hallo base blob. U kunt ook een momentopname kopiëren via de base blob, is vergelijkbaar met het herstellen van Hallo blob tooan eerdere versie. Wanneer een momentopname van een storage account tooanother wordt gekopieerd, het Hallo dezelfde als Hallo basispagina blob ruimte in beslag neemt. Daarom wordt het hele momentopnamen kopiëren van een storage account tooanother traag en maakt gebruik van veel ruimte in Hallo doel storage-account.

> [!NOTE]
> Als u Hallo base blob tooanother doel kopieert, worden Hallo momentopnamen van Hallo blob niet samen met het gekopieerd. Op dezelfde manier als u een basis blob met een kopie overschrijven, momentopnamen die zijn gekoppeld met Hallo base blob worden niet beïnvloed en onder de naam van de basis blob Hallo intact blijven.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Back-up van schijven met momentopnamen
Als een back-upstrategie voor uw virtuele machine-schijven kunt u periodieke momentopnamen van Hallo schijf of pagina-blob en kopieer deze tooanother storage-account met de hulpprogramma's zoals [Blob kopiëren](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) bewerking of [AzCopy](../articles/storage/common/storage-use-azcopy.md). U kunt een momentopname tooa bestemming pagina-blob met een andere naam kopiëren. Hallo resulterende de bestemmings-pagina-blob is een beschrijfbare pagina-blob en niet een momentopname. Verderop in dit artikel worden beschreven stappen tootake back-ups van de schijven van de virtuele machine met momentopnamen.

### <a name="restore-disks-using-snapshots"></a>Schijven met momentopnamen terugzetten
Wanneer het tijd toorestore uw schijf tooa versie die eerder is vastgelegd in een van de back-upmomentopnamen Hallo stabiel is, kunt u een momentopname via Hallo basispagina blob kopiëren. Nadat de momentopname Hallo is gepromoveerde toohello basispagina blob, Hallo momentopname blijft, maar de bron wordt overschreven met een kopie die kan worden gelezen en geschreven. Verderop in dit artikel worden beschreven stappen toorestore een eerdere versie van de schijf van de momentopname is gemaakt.

### <a name="implementing-full-snapshot-copy"></a>Volledige snapshotkopieën implementeren
U kunt een kopie van de volledige momentopname implementeren door Hallo-volgende te doen

* Eerst een momentopname van Hallo base blob met Hallo [momentopname Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) bewerking.
* Vervolgens kopiëren Hallo momentopname tooa doel storage account met behulp van [Blob kopiëren](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob).
* Herhaal dit proces toomaintain back-ups van uw base blob.

## <a name="incremental-snapshot-copy"></a>Incrementele snapshotkopieën
Hallo nieuwe functie in Hallo [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API biedt een veel betere manier tooback up Hallo momentopnamen van uw pagina-blobs of de schijven. Hallo API retourneert Hallo lijst met wijzigingen tussen Hallo base blob en Hallo momentopnamen, waardoor de hoeveelheid opslagruimte die wordt gebruikt voor back-account Hallo Hallo. Hallo API biedt ondersteuning voor pagina-blobs in Premium-opslag, evenals de Standard-opslag. Deze API gebruikt, kunt u snellere en efficiëntere back-oplossingen bouwen voor Azure Virtual machines. Deze API is beschikbaar met Hallo REST-versie 2015-07-08 en hoger.

Incrementele kopie van de momentopname, kunt u toocopy uit één storage account tooanother Hallo verschil tussen,

* Base blob en de momentopname of
* De twee momentopnamen van Hallo base blob

Opgegeven Hallo volgende voorwaarden wordt voldaan,

* Hallo-blob is gemaakt op Jan-1-2016 of hoger.
* Hallo-blob is niet overschreven met [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) of [Blob kopiëren](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) tussen twee momentopnamen.

**Opmerking**: deze functie is beschikbaar voor Premium en Standard Azure-pagina-Blobs.

Wanneer u een aangepaste back-upstrategie met momentopnamen hebt, kopiëren Hallo momentopnamen van een storage account tooanother kan traag zijn en hoeveel opslagruimte kan gebruiken. In plaats van het kopiëren van Hallo volledige momentopname tooa back-storage-account, kunt u Hallo verschil tussen opeenvolgende momentopnamen tooa back-pagina-blob schrijven. Op deze manier wordt Hallo tijd toocopy Hallo ruimte toostore back-ups en aanzienlijk verminderd.

### <a name="implementing-incremental-snapshot-copy"></a>Incrementele snapshotkopieën implementeren
U kunt incrementele snapshotkopieën implementeren door Hallo-volgende te doen

* Een momentopname van het gebruik van Hallo base blob [momentopname Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob).
* Kopiëren Hallo momentopname toohello doel back-upopslag account met behulp van [Blob kopiëren](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob). Dit is Hallo back-pagina-blob. Een momentopname van de back-pagina-blob Hallo en sla deze op Hallo back-account.
* Maak nog een momentopname van Hallo base blob met momentopname Blob.
* Hallo verschil tussen Hallo eerste en tweede momentopnamen van het gebruik van Hallo base blob ophalen [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges). Gebruik de nieuwe parameter Hallo **prevsnapshot**, toospecify Hallo DateTime-waarde van Hallo momentopname die u wilt dat tooget Hallo verschil met. Als deze parameter aanwezig is, bevat Hallo REST-antwoord alleen Hallo pagina's die zijn gewijzigd tussen doel momentopname en eerdere momentopname, met inbegrip van lege pagina's.
* Gebruik [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply deze wijzigingen toohello back-pagina-blob.
* Ten slotte een momentopname van de back-pagina-blob Hallo en sla deze op Hallo back-storage-account.

In de volgende sectie hello, maar wij beschrijven in meer detail hoe u back-ups van schijven met incrementele kopie van de momentopname kunt onderhouden

## <a name="scenario"></a>Scenario
In deze sectie beschrijven we een scenario waarbij een aangepaste back-upstrategie voor schijven van de virtuele machine met momentopnamen.

U kunt een DS-serie Azure virtuele machine met een premium-opslag P30 schijf die is gekoppeld. Hallo P30 schijf met de naam *mypremiumdisk* wordt opgeslagen in een premium storage-account genoemd *mypremiumaccount*. Standard-opslagaccount aangeroepen *mybackupstdaccount* wordt gebruikt voor het opslaan van Hallo back-up van *mypremiumdisk*. Willen we graag tookeep een momentopname van *mypremiumdisk* elke 12 uur.

toolearn over het maken van de storage-account en schijven te verwijzen[over Azure storage-accounts](../articles/storage/storage-create-storage-account.md).

toolearn back-ups van virtuele machines van Azure, te verwijzen[back-ups van virtuele machine van Azure plannen](../articles/backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Stappen toomaintain back-ups van een schijf met een incrementele momentopnamen
Hallo volgende stappen wordt beschreven hoe tootake momentopnamen van *mypremiumdisk* en onderhouden van Hallo back-ups in *mybackupstdaccount*. Hallo back-up is een standaard pagina-blob aangeroepen *mybackupstdpageblob*. Hallo back-pagina-blob geeft altijd dezelfde status die als laatste momentopname van Hallo Hallo *mypremiumdisk*.

1. Hallo back-pagina-blob voor de premium-opslag-schijf maken door het maken van een momentopname van *mypremiumdisk* aangeroepen *mypremiumdisk_ss1*.
2. Deze momentopname toomybackupstdaccount kopiëren als een pagina-blob aangeroepen *mybackupstdpageblob*.
3. Een momentopname van *mybackupstdpageblob* aangeroepen *mybackupstdpageblob_ss1*met [momentopname Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) en op te slaan in *mybackupstdaccount*.
4. Tijdens de back-upvenster hello, maak nog een momentopname van *mypremiumdisk*, spreek *mypremiumdisk_ss2*, en op te slaan in *mypremiumaccount*.
5. Hallo incrementele wijzigingen tussen twee Hallo momentopnamen ophalen *mypremiumdisk_ss2* en *mypremiumdisk_ss1*met [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) op  *mypremiumdisk_ss2* Hello **prevsnapshot** parameterset toohello tijdstempel van *mypremiumdisk_ss1*. Schrijven van deze back-pagina-blob van incrementele wijzigingen toohello *mybackupstdpageblob* in *mybackupstdaccount*. Als er in Hallo incrementele wijzigingen verwijderde bereiken, moet het worden gewist van Hallo back-pagina-blob. Gebruik [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) toowrite incrementele wijzigingen toohello back-pagina-blob.
6. Een momentopname van de back-pagina-blob Hallo *mybackupstdpageblob*die *mybackupstdpageblob_ss2*. Verwijderen van de vorige momentopname Hallo *mypremiumdisk_ss1* van premium storage-account.
7. Herhaal stap 4-6 elke back-upvenster. Op deze manier kunt u back-ups van blijven *mypremiumdisk* in een standard-opslagaccount.

![Maak een back-up van schijf met behulp van incrementele momentopnamen](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Stappen toorestore een schijf van momentopnamen
Hallo volgende stappen, beschrijven hoe toorestore premium schijf Hallo *mypremiumdisk* tooan eerder een momentopname van de back-opslagaccount hello *mybackupstdaccount*.

1. Hallo punt in tijd die u wenst dat toorestore Hallo premium schijf om te identificeren. Stel de machine momentopnamen *mybackupstdpageblob_ss2*, die is opgeslagen in de back-opslagaccount hello *mybackupstdaccount*.
2. Promoveren in mybackupstdaccount, Hallo momentopname *mybackupstdpageblob_ss2* als het nieuwe back-up basispagina blob Hallo *mybackupstdpageblobrestored*.
3. Een momentopname van deze herstelde back-pagina-blob, aangeroepen *mybackupstdpageblobrestored_ss1*.
4. Hallo hersteld pagina-blob kopiëren *mybackupstdpageblobrestored* van *mybackupstdaccount* te*mypremiumaccount* als Hallo nieuwe premium schijf  *mypremiumdiskrestored*.
5. Een momentopname van *mypremiumdiskrestored*die *mypremiumdiskrestored_ss1* voor toekomstige incrementele back-ups maken.
6. Wijs Hallo DS reeks VM toohello hersteld schijf *mypremiumdiskrestored* ont Hallo oude *mypremiumdisk* van Hallo VM.
7. Beginnen met Hallo back-up wordt beschreven in de vorige sectie voor Hallo hersteld schijf *mypremiumdiskrestored*, met behulp van Hallo *mybackupstdpageblobrestored* als Hallo back-pagina-blob.

![Schijf terugzetten van momentopnamen](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Volgende stappen
Gebruik Hallo volgende toolearn meer informatie over het maken van momentopnamen van een blob en het plannen van uw back-upinfrastructuur VM gekoppeld.

* [Maken van een momentopname van een Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [Uw VM-back-infrastructuur plannen](../articles/backup/backup-azure-vms-introduction.md)

