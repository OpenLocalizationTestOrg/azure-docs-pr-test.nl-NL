Er zijn twee typen opslagaccounts:

### <a name="general-purpose-storage-accounts"></a>Opslagaccounts voor algemeen gebruik
Een opslagaccounts voor algemeen gebruik biedt u toegang tot services zoals tabellen, wachtrijen, bestanden, Blobs en Azure tooAzure schijven van de virtuele machine onder één account. Dit type opslagaccount heeft twee prestatielagen:

* Een laag voor standaardopslagprestaties waarmee u toostore tabellen, wachtrijen, bestanden, Blobs en Azure kunt schijven op virtuele machine.
* Een Premium-opslagaccount, dat op dit moment alleen virtuele-machineschijven van Azure ondersteunt. Zie [Premium Storage: krachtige opslag voor Azure Virtual Machine-werkbelasting](../articles/storage/common/storage-premium-storage.md) voor een gedetailleerd overzicht van Premium-opslag.

### <a name="blob-storage-accounts"></a>Blob Storage-accounts
Een Blob Storage-account is een gespecialiseerd opslagaccount voor het opslaan van ongestructureerde gegevens als blobs (objecten) in Azure Storage. BLOB storage-accounts zijn vergelijkbaar tooyour bestaande opslagaccounts en delen alle Hallo geweldige duurzaamheid, beschikbaarheid, schaalbaarheid en prestaties van functies dat u vandaag inclusief 100 procent API-consistentie voor blok-blobs gebruikt en toevoeg-blobs. Voor toepassingen die alleen blok- of toevoeg-blob-opslag nodig hebben, wordt het gebruik van Blob-opslagaccounts aangeraden.

> [!NOTE]
> Blob Storage-accounts ondersteunen alleen blok-blobs en toevoeg-blobs. Pagina-blobs worden niet ondersteund.
> 
> 

BLOB storage-accounts beschikbaar Hallo **Toegangslaag** kenmerk die kan worden opgegeven tijdens het maken van het account en later naar behoefte worden gewijzigd. Er zijn twee soorten toegangslagen die u op basis van uw gegevenstoegangspatroon kunt opgeven:

* Een **Hot** toegangslaag waarmee wordt aangegeven dat wordt Hallo-objecten in Hallo opslagaccount vaker worden gebruikt. Hiermee kunt u toostore gegevens tegen lagere toegangskosten.
* Een **Cool** toegangslaag waarmee wordt aangegeven dat wordt Hallo-objecten in Hallo opslagaccount minder vaak worden gebruikt. Hiermee kunt u toostore gegevens op een lagere gegevensopslagkosten.

Als er een wijziging in het gebruikspatroon Hallo van uw gegevens, kunt u ook schakelen tussen deze toegangslagen op elk gewenst moment. Veranderende Hallo toegangslaag kan leiden tot extra kosten. Zie [Blob Storage-accounts: prijzen en facturering](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) voor meer informatie.

Zie [Azure Blob Storage: Cool Storage-laag en Hot Storage-laag](../articles/storage/blobs/storage-blob-storage-tiers.md) voor meer informatie.

Voordat u een opslagaccount maken kunt, hebt u een Azure-abonnement een abonnement waarmee u toegang tot tooa diverse Azure-services. Met een [gratis account](https://azure.microsoft.com/pricing/free-trial/) kunt u direct aan de slag met Azure. Als u toopurchase een plan abonnement besluit, kunt u kiezen uit diverse [aanschafopties](https://azure.microsoft.com/pricing/purchase-options/). Als u een [MSDN-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) bent, krijgt u gratis maandelijkse tegoeden die u kunt gebruiken met Azure-services, waaronder Azure Storage. Zie [Prijzen van Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor meer informatie over volumeprijzen.

hoe toocreate een opslagaccount zien toolearn [een opslagaccount maken](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) voor meer informatie. U kunt maken van een unieke naam storage-accounts aan één abonnement too200. Zie [Azure Storage Scalability and Performance Targets](../articles/storage/common/storage-scalability-targets.md) (Schaalbaarheids- en prestatiedoeleinden in Azure Storage) voor meer informatie over opslagaccountlimieten.

