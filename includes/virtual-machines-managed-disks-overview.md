# <a name="azure-managed-disks-overview"></a>Overzicht van Azure-beheerde schijven

Azure-beheerde schijven vereenvoudigt Schijfbeheer voor Azure IaaS VM's via het beheer van Hallo [opslagaccounts](../articles/storage/common/storage-introduction.md) Hallo VM schijven gekoppeld. U hoeft alleen toospecify Hallo type ([Premium](../articles/storage/common/storage-premium-storage.md) of [standaard](../articles/storage/common/storage-standard-storage.md)) en het Hallo-formaat van schijf u nodig hebt en Azure maakt en beheert Hallo schijf voor u.

## <a name="benefits-of-managed-disks"></a>Voordelen van beheerde schijven

Laten we enkele voordelen van Hallo u krijgt met behulp van beheerde schijven vanaf deze video Channel 9 [betere Azure VM tolerantie met schijven beheerd](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Eenvoudige en schaalbare implementaties van virtuele machines

Schijven ingangen opslag achter de schermen Hallo voor u beheerd. Voorheen moest u toocreate storage accounts toohold Hallo schijven (VHD-bestanden) voor uw Azure VM's. Wanneer het omhoog schalen, moest u toomake zeker dat u extra opslagaccounts hebt gemaakt, zodat u niet Hallo IOP's voor opslag met een van uw schijven overschrijden. Met beheerde schijven afhandeling van opslag, u zijn niet langer beperkt door Hallo opslagaccountlimieten (zoals 20.000 IOPS / -account). Ook niet langer hebt toocopy uw aangepaste installatiekopieën (VHD-bestanden) toomultiple storage-accounts. U kunt deze op een centrale locatie – één opslagaccount per Azure-regio – beheren en gebruiken ze toocreate honderden van virtuele machines in een abonnement.

Beheerde schijven kunt u toocreate up too10, 000 VM **schijven** in een abonnement dat kunt u toocreate duizendtallen van **VMs** in één abonnement. Deze functie ook verder verhoogt de schaalbaarheid van Hallo [virtuele Machine Scale Sets (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) doordat u toocreate up tooa duizenden virtuele machines in een VMSS met behulp van een Marketplace-installatiekopie.

### <a name="better-reliability-for-availability-sets"></a>Betere betrouwbaarheid voor Beschikbaarheidssets

Beheerde schijven biedt betere betrouwbaarheid voor Beschikbaarheidssets door ervoor te zorgen dat Hallo schijven van [virtuele machines in een Beschikbaarheidsset](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) zijn voldoende geïsoleerd van elkaar tooavoid individuele foutpunten. Dit gebeurt automatisch als Hallo schijven in verschillende opslagunits (stempels). Als een stempel is mislukt vanwege toohardware-of softwarefout, niet alleen Hallo VM-instanties met schijven op die stempels. Stel dat bijvoorbeeld een toepassing die wordt uitgevoerd op vijf virtuele machines en Hallo VM's zijn in een Beschikbaarheidsset. Hallo won't schijven voor deze VMs alle worden opgeslagen in Hallo dezelfde tijdstempel, dus als één stamp uitvalt, hello andere exemplaren van de toepassing hello toorun blijven.

### <a name="highly-durable-and-available"></a>Zeer duurzaam en hoge beschikbaarheid

Azure-schijven zijn ontworpen om 99,999% van de tijd beschikbaar te zijn. Rest-eenvoudiger weten dat u hebt drie replica's van uw gegevens waarmee hoge duurzaamheid. Als u problemen ondervindt bij één of zelfs twee replica's, zorgen Hallo resterende replica's persistentie van uw gegevens en een hoge tolerantie tegen fouten. Dankzij deze architectuur heeft Azure consistente duurzaamheid op ondernemingsniveau kunnen leveren voor IaaS-schijven, met een foutpercentage van NUL% op jaarbasis, het beste in de bedrijfstak. 

### <a name="granular-access-control"></a>Gedetailleerd toegangsbeheer

U kunt [gebaseerd toegangsbeheer (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign specifieke machtigingen voor een beheerde schijf tooone of meer gebruikers. Beheerd schijven zichtbaar gemaakt talloze voor bewerkingen, inclusief lezen, schrijven (maken/bijwerken), verwijderen en bij het ophalen van een [shared access signature (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) voor Hallo schijf. U kunt toegang tooonly Hallo bewerkingen van een persoon moet tooperform zijn taak verlenen. Bijvoorbeeld, als u niet dat een persoon toocopy beheerde schijven tooa storage-account wilt, kunt u geen toogrant access toohello export-actie voor die beheerde schijf. Op dezelfde manier als u niet dat een persoon toouse een SAS-URI-toocopy een beheerde schijf wilt, kunt u geen toogrant die machtiging toohello beheerde schijven.

### <a name="azure-backup-service-support"></a>Ondersteuning voor Azure Backup-service
Azure Backup-service met schijven beheerd toocreate een back-uptaak met back-ups op basis van tijd, eenvoudig herstel van de virtuele machine en back-up bewaarbeleidsregels gebruiken. Beheerde schijven ondersteunen alleen lokaal redundante opslag (LRS) als Hallo replicatieoptie; Dit betekent dat drie kopieën van Hallo gegevens in één regio blijven. Voor de regionale noodherstel, u moet back-up van uw VM-schijven in een andere regio met [Azure Backup-service](../articles/backup/backup-introduction-to-azure-backup.md) en een GRS-opslagaccount als back-upkluis. Azure Backup ondersteunt momenteel gegevens schijfgrootten up too1TB voor back-up. Meer informatie over deze [met behulp van Azure Backup-service voor virtuele machines met schijven beheerd](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Prijzen en facturering

Wanneer u schijven beheerd, Hallo volgende factureringsvoorwaarden van toepassing:
* Opslagtype

* Schijfgrootte

* Het aantal transacties

* Uitgaande gegevensoverdracht

* Beheerde schijf-momentopnamen (volledige schijf kopiëren)

We gaan deze nader bekijken.

**Opslagtype:** beheerde schijven biedt 2 prestatielagen: [Premium](../articles/storage/common/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../articles/storage/common/storage-standard-storage.md) (gebaseerd op harde schijf). Hallo facturering van een beheerde schijf is afhankelijk van welk type opslagruimte die u hebt geselecteerd voor Hallo schijf.


**Schijfgrootte**: facturering voor beheerde schijven, is afhankelijk van de grootte Hallo ingericht van Hallo schijf. Azure maps Hallo toohello dichtstbijzijnde schijven beheerd optie zoals opgegeven in de onderstaande tabellen voor Hallo ingerichte grootte (naar boven afronden). Elke schijf beheerde kaarten tooone Hallo ondersteund ingerichte grootten en dienovereenkomstig wordt gefactureerd. Als u een standard-beheerde schijven maken en een ingerichte grootte van 200 GB opgeeft, kunt u wordt bijvoorbeeld voor gefactureerd volgens Hallo Hallo S20 schijftype prijzen.

Hier zijn Hallo schijfgrootten beschikbaar voor premium-beheerde schijven:

| **Premium beheerd <br>schijftype** | **P4** | **P6** |**P10** | **P20** | **P30** | **P 40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Schijfgrootte        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Hier zijn Hallo schijfgrootten beschikbaar voor een standard-beheerde schijven:

| **Standaard beheerde <br>schijftype** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **AANBEVELING S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Schijfgrootte        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Het aantal transacties**: U wordt gefactureerd voor het aantal transacties die u op een standard-beheerde schijven uitvoert Hallo. Er is geen kosten voor transacties voor een premium-beheerde schijven.

**Uitgaande gegevensoverdracht**: [uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/) (gegevens uit de Azure-datacenters gaan) worden gefactureerd voor bandbreedtegebruik.

Zie voor gedetailleerde informatie over prijzen voor schijven beheerd [beheerd schijven prijzen](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Beheerde schijf momentopnamen

Een momentopname van een beheerd is een alleen-lezen kopie van een beheerde schijf die wordt opgeslagen als een standard-beheerde schijven standaard. Met momentopnamen, kunt u back-up uw beheerde schijven op elk punt in tijd. Deze momentopnamen onafhankelijk van de bronschijf Hallo bestaan en mag gebruikte toocreate nieuwe beheerde schijven. Ze worden gefactureerd op basis van de grootte Hallo gebruikt. Als u een momentopname van een beheerde schijf met ingerichte capaciteit van 64 GB en grootte van 10 GB gegevens die u gebruikt maakt, wordt bijvoorbeeld momentopname gefactureerd alleen voor Hallo gebruikt gegevensgrootte van 10 GB.  

[Incrementele momentopnamen](../articles/virtual-machines/windows/incremental-snapshots.md) worden momenteel niet ondersteund voor schijven die worden beheerd, maar worden ondersteund in toekomstige Hallo.

toolearn informatie over hoe toocreate momentopnamen met schijven beheerd check deze resources:

* [Een kopie maken van een VHD die is opgeslagen als beheerde schijf met behulp van momentopnamen in Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Een kopie maken van een VHD die is opgeslagen als beheerde schijf met behulp van momentopnamen in Linux](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Installatiekopieën

Beheerde schijven bieden ook ondersteuning voor het maken van een beheerde aangepaste installatiekopie. U kunt een installatiekopie van het maken van uw aangepaste VHD in een opslagaccount of rechtstreeks van een gegeneraliseerde (sys DomainPrep) VM. Dit wordt vastgelegd in één installatiekopie alle schijven die zijn gekoppeld aan een virtuele machine, met inbegrip van zowel hello OS- en gegevensschijven die worden beheerd. Dit kunt maken van virtuele machines met uw aangepaste installatiekopie zonder Hallo honderden moeten toocopy of beheren van alle opslagaccounts.

Check Hallo volgende artikelen voor meer informatie over het maken van installatiekopieën:
* [Hoe toocapture een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure](../articles/virtual-machines/windows/capture-image-resource.md)
* [Hoe toogeneralize en vastleggen een Linux-virtuele machine met Azure CLI 2.0 Hallo](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Installatiekopieën versus momentopnamen

Ziet u vaak Hallo woord 'installatiekopie' gebruikt met virtuele machines en u ziet nu 'momentopnamen' ook. Het is belangrijk toounderstand Hallo verschil tussen deze. U kunt een installatiekopie van een gegeneraliseerde virtuele machine die is opgeheven nemen met schijven beheerd. Deze installatiekopie bevat alle Hallo schijven die zijn gekoppeld toohello VM. Kunt u deze installatiekopie toocreate een nieuwe virtuele machine en neemt alle Hallo-schijven.

Een momentopname is een kopie van een schijf op Hallo punt in tijd die nodig is. Dit is alleen van toepassing tooone schijf. Als u een virtuele machine die slechts één schijf (hello OS heeft) hebt, kunt u een momentopname of een installatiekopie van het en maakt een virtuele machine vanuit Hallo momentopname of Hallo-installatiekopie.

Wat gebeurt er als een virtuele machine heeft vijf schijven en ze worden striped opgeslagen? U kan een momentopname van elke Hallo schijven, maar er is geen awareness binnen Hallo VM Hallo status van schijven Hallo – Hallo momentopnamen alleen weten over één schijf. In dit geval Hallo momentopnamen moet toobe coördinatie met elkaar en die momenteel niet wordt ondersteund.

## <a name="managed-disks-and-encryption"></a>Beheerde schijven en versleuteling

Er zijn twee soorten versleuteling toodiscuss verwijzing toomanaged schijven. Hallo eerst is een opslag Service versleuteling (SSE), die wordt uitgevoerd door Hallo storage-service. Hallo is tweede Azure Disk Encryption toe die u voor uw virtuele machines op Hallo besturingssysteem en gegevensschijven kunt inschakelen.

### <a name="storage-service-encryption-sse"></a>Versleuteling van opslag-Service (SSE)

[Azure Storage-Service: versleuteling](../articles/storage/common/storage-service-encryption.md) biedt versleuteling in rust en bescherming van uw gegevens toomeet uw organisatie beveiliging en naleving verplichtingen. SSE is standaard ingeschakeld voor alle beheerde schijven, momentopnamen en afbeeldingen in alle Hallo regio's waar beheerde schijven beschikbaar is. Starten van 10 juni 2017 worden alle nieuwe beheerde momentopnamen-schijven-installatiekopieën en nieuwe gegevens tooexisting beheerd schijven geschreven worden automatisch versleuteld in rust met sleutels die worden beheerd door Microsoft.  Ga naar Hallo [pagina met veelgestelde vragen voor schijven beheerd](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) voor meer informatie.


### <a name="azure-disk-encryption-ade"></a>Azure Disk Encryption (ADE)

Azure Disk Encryption kunt u tooencrypt hello OS- en gegevensschijven die wordt gebruikt door een virtuele Machine voor IaaS. Dit omvat beheerde schijven. Hallo stations zijn versleuteld met behulp van standaard-BitLocker-versleuteling technologie voor Windows. Hallo-schijven zijn versleuteld met behulp van technologie Hallo DM-Crypt voor Linux. Dit is geïntegreerd met Azure Key Vault tooallow u toocontrol en beheren van versleutelingssleutels Hallo-schijf. Zie voor meer informatie [Azure Disk Encryption for Windows en Linux IaaS VM's](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Volgende stappen

Raadpleeg toohello volgende artikelen voor meer informatie over schijven beheerd.

### <a name="get-started-with-managed-disks"></a>Aan de slag met beheerde schijven

* [Een virtuele machine maken met behulp van Resource Manager en PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Maak een Linux-VM met hello Azure CLI 2.0](../articles/virtual-machines/linux/quick-create-cli.md)

* [Koppelen van een beheerd gegevens schijf tooa virtuele machine van Windows met behulp van PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Toevoegen van een beheerde schijf tooa Linux VM](../articles/virtual-machines/linux/add-disk.md)

* [Het PowerShell-voorbeeldscripts schijven beheerd](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Beheerd schijven gebruiken in Azure Resource Manager-sjablonen](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Opties voor opslag van schijven beheerd vergelijken

* [Premium-opslag en schijven](../articles/storage/common/storage-premium-storage.md)

* [Standard-opslag en schijven](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>Gebruiksaanwijzing

* [Migreren van AWS en andere platforms tooManaged schijven in Azure](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Converteren van virtuele Azure-machines toomanaged schijven in Azure](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
