
## <a name="about-vhds"></a>Over VHD's

Hallo VHD's die worden gebruikt in Azure zijn VHD-bestanden die zijn opgeslagen als pagina-blobs in een standard- of premium storage-account in Azure. Zie [Understanding block blobs and page blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/) (Inzicht in blok-blobs en pagina-blobs) voor meer informatie over pagina-blobs. Zie [High-performance premium storage and Azure VMs](../articles/storage/common/storage-premium-storage.md) (Hoogwaardige Premium Storage en virtuele Azure-machines) voor meer informatie over Premium Storage.

Azure ondersteunt Hallo vaste schijf VHD-indeling. Hallo vaste indeling legt Hallo logische schijf uit lineair binnen Hallo-bestand, zodat de verschuiving van die schijf X wordt opgeslagen op de X-verschuiving van de blob. Een kleine voettekst achter Hallo Hallo blob beschrijft eigenschappen Hallo Hallo VHD. Vaak verspilt Hallo vaste indeling ruimte omdat de meeste schijven grote ongebruikte bereiken bevat hebben. Echter Azure slaat VHD-bestanden in een sparse-indeling, zodat u Hallo voordelen van beide Hallo vaste ontvangt en dynamische op Hallo dezelfde schijven tijd. Zie [Getting started with virtual hard disks](https://technet.microsoft.com/library/dd979539.aspx) (Aan de slag met virtuele harde schijven) voor meer informatie.

Alle VHD-bestanden in Azure dat u wilt dat toouse als een bron toocreate schijven of afbeeldingen alleen-lezen zijn. Wanneer u een schijf of installatiekopie maakt, maakt Azure kopieën van Hallo VHD-bestanden. Deze kopieën mag alleen-lezen of lezen-en-schrijven, afhankelijk van hoe u Hallo VHD gebruiken.

Wanneer u een virtuele machine van een installatiekopie maken, maakt Azure een schijf voor Hallo virtuele machine die een kopie van Hallo bron .vhd-bestand. tooprotect tegen het onbedoeld verwijderen Azure plaatst een lease op elke bron .vhd-bestand dat toocreate een afbeelding, schijf van een besturingssysteem of een gegevensschijf gebruikt.

Voordat u een bron .vhd-bestand verwijderen kunt, moet u tooremove Hallo lease door Hallo schijf of installatiekopie te verwijderen. toodelete een .vhd-bestand dat wordt gebruikt door een virtuele machine als de schijf van een besturingssysteem, kunt u verwijderen Hallo virtuele machine en besturingssysteemschijf Hallo Hallo bron .vhd-bestand in één keer door Hallo virtuele machine wordt verwijderd en het verwijderen van alle gekoppelde schijven. Het verwijderen van een VHD-bronbestand voor een gegevensschijf vereist echter een aantal stappen in een vaste volgorde. Eerst u Hallo schijf uit de Hallo virtuele machine en vervolgens verwijderen Hallo schijf loskoppelen en verwijder vervolgens Hallo .vhd-bestand.

> [!WARNING]
> Als u een VHD-bronbestand uit de opslag verwijdert of uw opslagaccount verwijdert, kan Microsoft die gegevens niet voor u herstellen.
> 

## <a name="types-of-disks"></a>Typen schijven 

Azure-schijven zijn ontworpen om 99,999% van de tijd beschikbaar te zijn. Azure-schijven hebben dan bedrijfsniveau duurzaamheid met een toonaangevende nul % Annualized Faalpercentage consistent geleverd.

U kunt kiezen uit twee prestatielagen voor opslag wanneer u uw schijven maakt: Standard Storage en Premium Storage. Daarnaast zijn er twee soorten schijven, niet-beheerd en beheerd, die zich in elk van de twee prestatielagen kunnen bevinden.


### <a name="standard-storage"></a>Standard Storage 

Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag. Standard Storage kan lokaal worden gerepliceerd in één datacenter of kan geografisch redundant zijn met primaire en secundaire datacenters. Zie [Azure Storage-replicatie](../articles/storage/common/storage-redundancy.md) voor meer informatie over opslagreplicatie. 

Raadpleeg [Standard Storage and Disks](../articles/storage/common/storage-standard-storage.md) (Standard Storage en schijven) voor meer informatie over het gebruik van Standard Storage met VM-schijven.

### <a name="premium-storage"></a>Premium Storage 

Premium Storage maakt gebruik van SSD's en voorziet in hoogwaardige schijfondersteuning met lage latentie voor virtuele machines die I/O-intensieve workloads uitvoeren. U kunt de Premium-opslag gebruiken met Active Directory, DSv2, GS, Ls of FS reeks in het virtuele Azure-machines. Ga voor meer informatie naar [Premium Storage](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Niet-beheerde schijven

Niet-beheerde schijven zijn Hallo traditionele type schijven die zijn gebruikt door virtuele machines. Met deze, moet u uw eigen storage-account maken en die storage-account opgeven wanneer u Hallo schijf maakt. Hebt u toomake zeker dat u niet te veel schijven plaatsen hetzelfde opslagaccount Hallo omdat u Hallo kan overschrijdt [schaalbaarheidsdoelen](../articles/storage/common/storage-scalability-targets.md) van Hallo storage-account (bijvoorbeeld 20.000 IOPS), wat resulteert in Hallo virtuele machines wordt beperkt. Met niet-beheerde schijven hebt u toofigure uit hoe toomaximize hello gebruiken van een of meer accounts tooget Hallo best opslagprestaties buiten uw virtuele machines.

### <a name="managed-disks"></a>Managed Disks 

Schijven ingangen Hallo opslag maken/management op de achtergrond Hallo-account voor u en zorgt ervoor dat u hebt geen tooworry over schaalbaarheidsbeperkingen Hallo van Hallo storage-account wordt beheerd. U gewoon opgeven Hallo schijfgrootte en Hallo prestatielaag (standaard/Premium) en Azure maakt en beheert Hallo schijf voor u. Zelfs als u schijven toevoegen of Hallo VM omhoog en omlaag schalen, hebt u geen tooworry over Hallo opslag wordt gebruikt. 

U kunt ook aangepaste installatiekopieën in een opslagaccount per Azure-regio beheren en ze toocreate honderden van virtuele machines in hello gebruiken hetzelfde abonnement. Zie voor meer informatie over beheerde schijven Hallo [schijven overzicht beheerde](../articles/virtual-machines/windows/managed-disks-overview.md).

U wordt aangeraden Azure beheerd schijven te gebruiken voor de nieuwe virtuele machines en dat u uw vorige niet-beheerde schijven toomanaged schijven geconverteerd, tootake profiteren van Hallo veel functies die beschikbaar zijn in schijven beheerd.

### <a name="disk-comparison"></a>Vergelijking van schijven

Hallo volgende tabel bevat een vergelijking van Premium tegenover Standard voor zowel niet-beheerd als schijven toohelp u besluit welke toouse beheerd.

|    | Azure Premium Disk | Azure Standard Disk |
|--- | ------------------ | ------------------- |
| Schijftype | Solid-state drives (SSD) | Hardeschijfstation (HDD)  |
| Overzicht  | Hoogwaardige schijfondersteuning met lage latentie op basis van SSD's voor virtuele machines die IO-intensieve workloads uitvoeren of een bedrijfskritieke productieomgeving hosten | Voordelige schijfondersteuning op basis van HDD's voor het ontwikkelen/testen van virtuele machines |
| Scenario  | Productie- en prestatiegevoelige workloads | Ontwikkelen/testen, niet-kritiek, <br>Incidentele toegang |
| Schijfgrootte | P4: 32 GB (alleen beheerde schijven)<br>P6: 64 GB (alleen beheerde schijven)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P 40: 2048 GB<br>P50: 4095 GB | Niet-beheerde schijven: 1 GB – 4 TB (4095 GB) <br><br>Beheerde schijven:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>AANBEVELING S50: 4095 GB| 
| Max. doorvoer per schijf | 250 MB/s | 60 MB/s | 
| Max. IOP's per schijf | 7500 IOP 'S | 500 IOP's | 

