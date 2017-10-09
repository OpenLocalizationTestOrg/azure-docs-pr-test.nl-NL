---
title: Versleuteling van de aaaClient aan clientzijde met behulp van Python voor Microsoft Azure Storage | Microsoft Docs
description: Hello Azure Storage-clientbibliotheek voor Python biedt ondersteuning voor versleuteling aan clientzijde voor een maximale beveiliging voor uw Azure Storage-toepassingen.
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: d2e943977322b97b777369508b957a1b2cbaa4e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Versleuteling van de Client-Side met behulp van Python voor opslag op Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Overzicht
Hallo [Azure Storage-clientbibliotheek voor Python](https://pypi.python.org/pypi/azure-storage) ondersteunt de versleuteling van gegevens binnen clienttoepassingen voordat tooAzure opslag uploaden en ontsleutelen van gegevens tijdens het downloaden van toohello client.

> [!NOTE]
> Hello Azure Storage Python-bibliotheek is een Preview-versie.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Versleuteling en ontsleuteling via Hallo envelop techniek
Hallo processen van coderen en decoderen Volg Hallo envelop techniek.

### <a name="encryption-via-hello-envelope-technique"></a>Versleuteling via Hallo envelop techniek
Versleuteling via Hallo envelop techniek werkt in de volgende manieren Hallo:

1. Hello Azure storage-clientbibliotheek genereert een inhoud versleutelingssleutel (CEK), die een symmetrische sleutel met een eenmalig gebruik is.
2. Gebruikersgegevens worden versleuteld met behulp van deze CEK.
3. Hallo wordt CEK vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel). Hallo KEK wordt aangeduid met een sleutel-id en kan een asymmetrisch sleutelpaar of een symmetrische sleutel, die lokaal wordt beheerd.
   Hallo storage-clientbibliotheek zelf heeft nooit toegang tooKEK. Hallo-bibliotheek roept de algoritme die wordt geleverd door Hallo KEK wrapping Hallo-sleutel. Gebruikers kunnen kiezen toouse aangepaste providers voor de sleutel wrapping/uitpakken indien gewenst.
4. Hallo versleutelde gegevens is vervolgens toohello Azure Storage-service geüpload. Hallo ingepakte sleutel samen met enkele aanvullende versleutelingsmetagegevens die is opgeslagen als metagegevens (op een blob) of geïnterpoleerd met Hallo gecodeerde gegevens (Wachtrijberichten en tabelentiteiten).

### <a name="decryption-via-hello-envelope-technique"></a>Ontsleuteling via Hallo envelop techniek
Ontsleuteling via Hallo envelop techniek werkt in de volgende manieren Hallo:

1. Hallo-clientbibliotheek wordt ervan uitgegaan dat die gebruiker Hallo Hallo sleutelcodering sleutel (een KEK) lokaal wordt beheerd. Hallo gebruiker hoeft niet tooknow Hallo specifieke sleutel die is gebruikt voor versleuteling. In plaats daarvan worden een sleutel resolver, die wordt omgezet tookeys verschillende sleutel-id's, ingesteld en gebruikt.
2. Hallo-clientbibliotheek downloadt Hallo versleutelde gegevens samen met versleuteling materiaal dat is opgeslagen op Hallo-service.
3. Hallo verpakte inhoud versleutelingssleutel (CEK) is en niet-ingepakte (ontsleutelde) met behulp van Hallo sleutelcodering sleutel (KEK-sleutel). Hier opnieuw heeft Hallo-clientbibliotheek geen toegang tot tooKEK. Het aanroept algoritme voor het uitpakken van Hallo aangepaste provider gewoon.
4. Hallo inhoud versleutelingssleutel (CEK) wordt vervolgens gebruikt toodecrypt Hallo versleuteld gebruikersgegevens.

## <a name="encryption-mechanism"></a>Versleuteling mechanisme
maakt gebruik van de storage-clientbibliotheek Hallo [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in volgorde tooencrypt gebruikersgegevens. In het bijzonder [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) modus met AES. Elk service enigszins anders werkt zodat elk van deze hier worden besproken.

### <a name="blobs"></a>Blobs
Hallo-clientbibliotheek biedt momenteel ondersteuning voor versleuteling van de hele BLOB's. In het bijzonder versleuteling wordt ondersteund wanneer gebruikers Hallo gebruiken **maken*** methoden. Voor downloads, zowel volledige als bereik downloads worden ondersteund en garandeert van beide uploaden en downloaden is beschikbaar.

Hallo-clientbibliotheek wordt tijdens het versleutelen kan genereren van een willekeurige initialisatie Vector (IV) van 16 bytes, samen met een willekeurige inhoud versleutelingssleutel (CEK) 32 bytes en uitvoeren van envelop versleuteling van blobgegevens Hallo met behulp van deze informatie. Hallo CEK ingepakt en een aantal aanvullende metagegevens worden vervolgens opgeslagen als blob-metagegevens samen met de Hallo versleutelde blob op Hallo-service.

> [!WARNING]
> Als u bewerkt of uw eigen metagegevens voor Hallo blob uploaden, moet u tooensure dat deze metagegevens behouden blijft. Als u nieuwe metagegevens zonder deze metagegevens uploadt, Hallo verpakte CEK IV en andere metagegevens niet verloren en Hallo blob-inhoud wordt nooit meer worden opgehaald.
> 
> 

Downloaden van een versleutelde blob omvat het ophalen van inhoud van de hele Hallo-blob met Hallo Hallo **ophalen*** gemak methoden. Hallo verpakte CEK is al en gebruikt in combinatie met de Hallo IV (opgeslagen als blobmetagegevens in dit geval) tooreturn Hallo ontsleuteld data toohello gebruikers.

Downloaden van een willekeurig bereik (**ophalen*** methoden met bereik parameters doorgegeven) in Hallo versleutelde blob omvat het aanpassen van Hallo bereik dat wordt geleverd door gebruikers in de volgorde tooget een kleine hoeveelheid aanvullende gegevens die kunnen worden gebruikt toosuccessfully ontsleutelen Hallo aangevraagd bereik.

Blok-blobs en pagina-blobs kunnen alleen worden versleuteld/ontsleuteld met behulp van dit schema. Er is momenteel geen ondersteuning voor het versleutelen van toevoeg-blobs.

### <a name="queues"></a>Wachtrijen
Omdat berichten in wachtrij plaatsen van een willekeurige indeling zijn kunnen, definieert de clientbibliotheek Hallo een aangepaste indeling met Hallo initialisatie Vector (IV) en Hallo versleutelde inhoud versleutelingssleutel (CEK) in de berichttekst Hallo.

Tijdens het versleutelen kan Hallo-clientbibliotheek genereert een willekeurige IV van 16 bytes samen met een willekeurige CEK 32 bytes en versleuteling van Hallo wachtrij bericht met deze informatie envelop uitgevoerd. Hallo CEK ingepakt en bepaalde metagegevens extra codering toohello versleutelde wachtrijbericht vervolgens worden toegevoegd. Dit gewijzigde bericht (Zie hieronder) wordt opgeslagen op Hallo-service.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Tijdens het ontsleutelen, Hallo ingepakte sleutel opgehaald uit de wachtrij het Hallo-bericht en al. Hallo IV is ook opgehaald uit de wachtrij het Hallo-bericht en gebruikt samen met de Hallo al sleutel toodecrypt Hallo wachtrij berichtgegevens. Houd er rekening mee dat Hallo versleutelingsmetagegevens zijn kleine (onder 500 bytes), zodat terwijl deze telt mee voor de limiet van 64KB Hallo voor een wachtrijbericht, Hallo impact beheerd worden moet.

### <a name="tables"></a>Tabellen
Hallo van client-bibliotheek ondersteunt de versleuteling van entiteitseigenschappen voor invoegen en vervang bewerkingen.

> [!NOTE]
> Samenvoegen wordt momenteel niet ondersteund. Omdat een subset van eigenschappen mogelijk zijn versleuteld eerder met een andere sleutel, leidt gewoon samenvoegen Hallo nieuwe eigenschappen en bijwerken van Hallo metagegevens tot verlies van gegevens. Samenvoegen van een vereist extra service waardoor tooread Hallo vooraf bestaande entiteit aanroepen vanaf Hallo service of met een nieuwe sleutel per eigenschap, die beide zijn niet geschikt voor betere prestaties.
> 
> 

Tabel gegevensversleuteling werkt als volgt:

1. Gebruikers opgeven Hallo eigenschappen toobe versleuteld.
2. Hallo-clientbibliotheek genereert een willekeurige initialisatie Vector (IV) van 16 bytes samen met een willekeurige inhoud versleutelingssleutel (CEK) 32 bytes voor elke entiteit en envelop versleuteling op Hallo afzonderlijke eigenschappen toobe versleuteld met een nieuwe IV per afgeleid uitgevoerd de eigenschap. Hallo versleuteld eigenschap wordt als binaire gegevens opgeslagen.
3. Hallo CEK ingepakt en een aantal aanvullende metagegevens worden vervolgens opgeslagen als twee extra gereserveerde eigenschappen. Hallo eerst eigenschap gereserveerd (\_ClientEncryptionMetadata1) is een tekenreekseigenschap dat Hallo informatie over IV, versie en verpakte sleutel bevat. tweede gereserveerde eigenschap Hallo (\_ClientEncryptionMetadata2) is een binaire eigenschap van de Hallo informatie over het Hallo-eigenschappen die zijn versleuteld. informatie in deze tweede eigenschap Hallo (\_ClientEncryptionMetadata2) zelf versleuteld.
4. Vervaldatum toothese extra gereserveerde vereiste eigenschappen voor versleuteling, kunnen gebruikers nu alleen 250 aangepaste eigenschappen in plaats van 252 hebben. totale grootte van entiteit Hallo Hallo moet minder dan 1MB.
   
   Houd er rekening mee dat alleen de tekenreekseigenschappen van de kunnen worden versleuteld. Als andere typen eigenschappen toobe versleuteld zijn, moeten ze geconverteerde toostrings zijn. Hallo versleutelde tekenreeksen op Hallo-service worden opgeslagen als binaire eigenschappen en ze back toostrings (onbewerkte tekenreeksen, niet EntityProperties met type EdmType.STRING) na de decodering worden omgezet.
   
   Voor tabellen bovendien toohello versleutelingsbeleid, gebruikers moeten opgeven Hallo eigenschappen toobe versleuteld. Dit kunt doen door op te slaan deze eigenschappen in TableEntity-objecten met Hallo type set tooEdmType.STRING en set tootrue of instelling Hallo encryption_resolver_function op Hallo tableservice object versleutelen. Een oplossing versleuteling is een functie die ervoor zorgt dat een partitiesleutel, rijsleutel en de naam van eigenschap retourneert een Booleaanse waarde die aangeeft of de eigenschap die moet worden versleuteld. Hallo-clientbibliotheek gebruiken tijdens het versleutelen kan deze informatie toodecide toe of een eigenschap tijdens het schrijven van toohello kabel moet worden versleuteld. Hallo gemachtigde biedt ook de mogelijkheid Hallo van logica over hoe eigenschappen zijn gecodeerd. (Bijvoorbeeld als X, vervolgens versleutelen eigenschap A; anders versleutelen eigenschappen A en B.) Houd er rekening mee dat deze is niet nodig tooprovide deze informatie tijdens het lezen of het uitvoeren van query's entiteiten.

### <a name="batch-operations"></a>Batchbewerkingen
Een versleutelingsbeleid geldt tooall rijen in de Hallo batch. Hallo-clientbibliotheek wordt een nieuwe willekeurige IV en willekeurige CEK per rij in een batch Hallo intern gegenereerd. Gebruikers kunnen ook kiezen tooencrypt verschillende eigenschappen voor elke bewerking in batch Hallo door dit gedrag definiëren in Hallo versleuteling resolver.
Als een batch is gemaakt als een manager context met Hallo tableservice batch() methode, versleutelingsbeleid van Hallo tableservice toegepaste toohello batch automatisch worden. Als een batch expliciet gemaakt wordt door het Hallo-constructor aanroepen, moet Hallo versleutelingsbeleid worden doorgegeven als een parameter en links ongewijzigd voor Hallo levensduur van Hallo batch.
Houd er rekening mee dat entiteiten worden gecodeerd als ze worden ingevoegd in Hallo batch met behulp van de batch Hallo versleutelingsbeleid (entiteiten worden niet versleuteld gelijktijdig Hallo met het doorvoeren van Hallo batch met behulp van Hallo tableservice versleutelingsbeleid).

### <a name="queries"></a>Query's
tooperform querybewerkingen, moet u een sleutel resolver die kunnen tooresolve alle sleutels in de resultatenset Hallo Hallo. Als een entiteit die is opgenomen in het queryresultaat Hallo niet kan opgelost tooa provider worden, Hallo-clientbibliotheek genereert een fout opgetreden. Voor elke query die server side projecties uitvoert, Hallo-clientbibliotheek Hallo speciale versleuteling metagegevenseigenschappen worden toegevoegd (\_ClientEncryptionMetadata1 en \_ClientEncryptionMetadata2) door standaard toohello kolommen geselecteerd .

> [!IMPORTANT]
> Wanneer met behulp van versleuteling aan clientzijde, worden op de hoogte van deze belangrijke punten:
> 
> * Lezen van of schrijven tooan versleuteld wanneer blob, gebruik hele blob uploaden opdrachten en bereik/geheel blob downloaden opdrachten. Vermijd schrijven tooan versleutelde blob met protocolbewerkingen zoals het blok plaatsen, blokkeringslijst plaatsen, pagina's schrijven of wissen pagina's. anders u mogelijk Hallo versleutelde blob beschadigd en onleesbaar.
> * Een vergelijkbaar beperking bestaat voor tabellen. Worden zorgvuldige toonot update versleuteld eigenschappen zonder Hallo versleutelingsmetagegevens worden bijgewerkt.
> * Als u de metagegevens op Hallo versleutelde blob instelt, overschrijft u mogelijk Hallo versleutelingsgerelateerde metagegevens die vereist is voor ontsleuteling, omdat de instelling van metagegevens is niet-additieve. Dit geldt ook voor momentopnamen; Vermijd metagegevens tijdens het maken van een momentopname van een versleutelde blob. Als metagegevens moet worden ingesteld, moet u ervoor toocall hello **get_blob_metadata** methode eerste tooget Hallo huidige versleutelingsmetagegevens en gelijktijdige schrijfbewerkingen voorkomen tijdens het instellen van metagegevens.
> * Hallo inschakelen **require_encryption** vlag op Hallo serviceobject voor gebruikers die normaal alleen met gecodeerde gegevens werken gesproken. Zie hieronder voor meer informatie.
> 
> 

Hallo storage-clientbibliotheek verwacht Hallo opgegeven KEK en sleutel resolver tooimplement Hallo interface te volgen. [Azure Sleutelkluis](https://azure.microsoft.com/services/key-vault/) ondersteuning voor Python-KEK-management in behandeling is en zal worden geïntegreerd in deze bibliotheek als voltooid.

## <a name="client-api--interface"></a>Client-API / Interface
Nadat een opslagobject van service (dat wil zeggen blockblobservice) is gemaakt, Hallo-gebruiker kan waarden toewijzen toohello velden die deel uitmaken van een versleutelingsbeleid: key_encryption_key, key_resolver_function, en require_encryption. Gebruikers kunnen alleen een KEK bieden alleen een resolver of beide. key_encryption_key is Hallo basic type sleutel dat wordt geïdentificeerd met een sleutel-id en biedt Hallo logica voor onmiddellijke/uitpakken. gebruikte tooresolve een sleutel is key_resolver_function tijdens het Hallo-decoderingsproces. Retourneert een geldige KEK een sleutel-id opgegeven. Dit biedt gebruikers Hallo mogelijkheid toochoose tussen meerdere sleutels die worden beheerd op meerdere locaties.

Hallo KEK Hallo volgende moet implementeren methoden toosuccessfully gegevens versleutelen:

* wrap_key(cek): terugloopt Hallo CEK (bytes) met behulp van een algoritme van de keuze van de gebruiker Hallo opgegeven. Retourneert Hallo ingepakte sleutel.
* get_key_wrap_algorithm(): retourneert Hallo algoritme toowrap sleutels gebruikt.
* get_kid(): retourneert Hallo tekenreeks sleutel-id voor deze KEK-sleutel.
  Hallo KEK moet implementeren Hallo methoden toosuccessfully decoderen van gegevens te volgen:
* unwrap_key (cek, algoritme): retourneert Hallo al formulier Hallo CEK met Hallo tekenreeks opgegeven algoritme opgegeven.
* get_kid(): retourneert een tekenreeks met sleutel-id voor deze KEK-sleutel.

Hallo sleutel resolver moet ten minste een methode die een sleutel-id opgegeven Hallo bijbehorende KEK geïmplementeerd Hallo interface bovenstaande retourneert implementeren. Alleen deze methode is toobe toohello key_resolver_function-eigenschap op Hallo serviceobject toegewezen.

* Hallo-sleutel wordt altijd gebruikt voor versleuteling, en Hallo afwezigheid van een sleutel in een fout resulteert.
* Voor ontsleuteling:
  
  * Hallo sleutel resolver wordt opgeroepen als tooget Hallo sleutel opgegeven. Als het Hallo-omzetter wordt opgegeven, maar heeft geen een toewijzing voor Hallo sleutel-id, wordt er een fout gegenereerd.
  * Als conflictoplosser niet is opgegeven, maar een sleutel is opgegeven, worden de Hallo-sleutel wordt gebruikt als de id overeenkomt met de Hallo vereist sleutel-id. Als het Hallo-id komt niet overeen met, wordt een fout gegenereerd.
    
    Voorbeelden van versleuteling in azure.storage.samples Hallo <fix URL>een meer gedetailleerde end-to-end-scenario voor blobs, wachtrijen en tabellen te demonstreren.
      Voorbeeldimplementaties van Hallo KEK en sleutel resolver vindt u in de voorbeeldbestanden Hallo als KeyWrapper en KeyResolver respectievelijk.

### <a name="requireencryption-mode"></a>RequireEncryption modus
Gebruikers kunnen eventueel inschakelen voor een werkmodus waar alle uploaden en downloaden moeten worden versleuteld. In deze modus mislukt pogingen tooupload gegevens zonder een beleid of download Versleutelingsgegevens is niet versleuteld op Hallo-service op Hallo client. Hallo **require_encryption** vlag op Hallo service object besturingselementen dit gedrag.

### <a name="blob-service-encryption"></a>Versleuteling van BLOB-service
Hallo versleuteling Beleidsvelden instellen op Hallo blockblobservice-object. Alle andere wordt verwerkt door de clientbibliotheek Hallo intern.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Wachtrij-service: versleuteling
Hallo versleuteling Beleidsvelden op Hallo queueservice object instellen. Alle andere wordt verwerkt door de clientbibliotheek Hallo intern.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Tabel-service: versleuteling
Bovendien toocreating een versleutelingsbeleid voor en instellen op verzoek-opties, u moet opgeven een **encryption_resolver_function** op Hallo **tableservice**, of set Hallo versleutelen van kenmerk op Hello EntityProperty.

### <a name="using-hello-resolver"></a>Hallo conflictoplosser

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Met behulp van kenmerken
Zoals eerder vermeld, een eigenschap kan worden gemarkeerd voor codering opslaan in een object EntityProperty en instellen Hallo veld versleutelen.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Versleuteling en prestaties
Houd er rekening mee dat de opslag, resulteert in extra prestatieoverhead versleutelt. Hallo inhoud sleutel en IV moet worden gegenereerd, Hallo inhoud zelf moet worden versleuteld en aanvullende metagegevens moet zijn geformatteerd en geüpload. Deze overhead is afhankelijk van Hallo en de hoeveelheid gegevens wordt versleuteld. Het is raadzaam dat klanten hun toepassingen voor de prestaties tijdens de ontwikkeling altijd testen.

## <a name="next-steps"></a>Volgende stappen
* Hallo downloaden [Azure Storage-clientbibliotheek voor Java PyPi-pakket](https://pypi.python.org/pypi/azure-storage)
* Hallo downloaden [Azure Storage-clientbibliotheek voor Python broncode vanuit GitHub](https://github.com/Azure/azure-storage-python)
