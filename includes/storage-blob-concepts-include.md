## <a name="what-is-blob-storage"></a>Wat is Blob Storage?
Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde objectgegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. U kunt Blob storage-tooexpose gegevens openbaar toohello world of toostore toepassingsgegevens privé.

Veelvoorkomende toepassingen van Blob Storage zijn onder andere:

* Voor afbeeldingen of documenten rechtstreeks tooa browser
* De opslag van bestanden voor gedistribueerde toegang
* Streaming van video en audio
* De opslag van gegevens voor back-up en herstel, herstel na noodgevallen en archivering
* De opslag van gegevens voor analyse door een on-premises in Azure gehoste service

## <a name="blob-service-concepts"></a>Concepten van Blob service
Hallo Blob-service bevat Hallo volgende onderdelen:

![Blobarchitectuur](./media/storage-blob-concepts-include/blob1.png)

* **Storage-Account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Dit opslagaccount kan een **algemeen opslagaccount** zijn of een **Blob-opslagaccount** dat speciaal is bedoeld voor de opslag van objecten/blobs. Zie [Over Azure Storage-accounts](../articles/storage/common/storage-create-storage-account.md) voor meer informatie.
* **Container:** Een container is een groepering van een reeks blobs. Alle blobs moeten zich in een container bevinden. Een account kan een onbeperkt aantal containers bevatten. Een container kan een onbeperkt aantal blobs bevatten. Houd er rekening mee dat Hallo containernaam moet een kleine letter.
* **Blob:** Een bestand van willekeurig type en willekeurige grootte. Azure Storage biedt drie typen blobs: blok-blobs, pagina-blobs en toevoeg-blobs.
  
    *Blok-blobs* zijn ideaal voor de opslag van tekst- of binaire bestanden, zoals documenten en mediabestanden. *Toevoeg-blobs* zijn vergelijkbaar tooblock blobs in dat ze bestaan uit blokken, maar ze zijn geoptimaliseerd voor toevoegbewerkingen; ze zijn daarom nuttig voor logboekscenario's. Een enkel blok-blob kan bevatten up too50, 000 blokken van too100 MB, voor een totale grootte van iets meer dan 4.75 TB (100 MB X 50.000). Een enkele toevoeg-blob kan bevatten up too50, 000 blokken van too4 MB, voor een totale grootte van iets meer dan 195 GB (4 MB X 50.000).
  
    *Pagina-blobs* kan up too1 TB groot zijn en zijn efficiënter voor regelmatige lees-en schrijfbewerkingen. In Azure Virtuele Machines worden pagina-blobs gebruikt als besturingssysteem- en gegevensschijven.
  
    Zie [Containers, blobs en metagegevens een naam geven en hiernaar verwijderen](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) voor meer informatie over de naamgeving van containers en blobs.

