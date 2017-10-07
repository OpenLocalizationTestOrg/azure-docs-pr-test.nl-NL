---
title: Versleuteling van de aaaClient aan clientzijde met Java voor Microsoft Azure Storage | Microsoft Docs
description: Hello Azure Storage-clientbibliotheek voor Java ondersteunt clientzijde versleuteling en integratie met Azure Key Vault voor een maximale beveiliging voor uw Azure Storage-toepassingen.
services: storage
documentationcenter: java
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 3df49907-554c-404a-9b0c-b3e3269ad04f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: cb40c737b9065005f0f31f654e7e43fd27b923f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a>Client-Side-versleuteling en Azure Sleutelkluis met Java voor Microsoft Azure Storage
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Overzicht
Hallo [Azure Storage-clientbibliotheek voor Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) ondersteunt de versleuteling van gegevens binnen clienttoepassingen voordat tooAzure opslag uploaden en ontsleutelen van gegevens tijdens het downloaden van toohello client. Hallo-bibliotheek ondersteunt ook integratie met [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) voor sleutelbeheer storage-account.

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Versleuteling en ontsleuteling via Hallo envelop techniek
Hallo processen van coderen en decoderen Volg Hallo envelop techniek.  

### <a name="encryption-via-hello-envelope-technique"></a>Versleuteling via Hallo envelop techniek
Versleuteling via Hallo envelop techniek werkt in de volgende manieren Hallo:  

1. Hello Azure storage-clientbibliotheek genereert een inhoud versleutelingssleutel (CEK), die een symmetrische sleutel met een eenmalig gebruik is.  
2. Gebruikersgegevens worden versleuteld met behulp van deze CEK.   
3. Hallo wordt CEK vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel). Hallo KEK wordt aangeduid met een sleutel-id en een asymmetrisch sleutelpaar of een symmetrische sleutel en kan worden lokaal beheerd of opgeslagen in Azure sleutel kluizen.  
   Hallo storage-clientbibliotheek zelf heeft nooit toegang tooKEK. Hallo-bibliotheek roept Hallo sleutel wrapping algoritme die wordt geleverd door de Sleutelkluis. Gebruikers kunnen kiezen toouse aangepaste providers voor de sleutel wrapping/uitpakken indien gewenst.  
4. Hallo versleutelde gegevens is vervolgens toohello Azure Storage-service geüpload. Hallo ingepakte sleutel samen met enkele aanvullende versleutelingsmetagegevens die is opgeslagen als metagegevens (op een blob) of geïnterpoleerd met Hallo gecodeerde gegevens (Wachtrijberichten en tabelentiteiten).

### <a name="decryption-via-hello-envelope-technique"></a>Ontsleuteling via Hallo envelop techniek
Ontsleuteling via Hallo envelop techniek werkt in de volgende manieren Hallo:  

1. Hallo-clientbibliotheek wordt ervan uitgegaan dat die gebruiker Hallo Hallo sleutelcodering sleutel (een KEK) wordt beheerd door lokaal of in kluizen van Azure-sleutel. Hallo gebruiker hoeft niet tooknow Hallo specifieke sleutel die is gebruikt voor versleuteling. In plaats daarvan worden een sleutel-omzetter die wordt omgezet tookeys verschillende sleutel-id's ingesteld en gebruikt.  
2. Hallo-clientbibliotheek downloadt Hallo versleutelde gegevens samen met versleuteling materiaal dat is opgeslagen op Hallo-service.  
3. Hallo verpakte inhoud versleutelingssleutel (CEK) is en niet-ingepakte (ontsleutelde) met behulp van Hallo sleutelcodering sleutel (KEK-sleutel). Hier opnieuw heeft Hallo-clientbibliotheek geen toegang tot tooKEK. Het aanroept aangepaste Hallo of uitpakken van de provider van de Sleutelkluis-algoritme gewoon.  
4. Hallo inhoud versleutelingssleutel (CEK) wordt vervolgens gebruikt toodecrypt Hallo versleuteld gebruikersgegevens.

## <a name="encryption-mechanism"></a>Versleuteling mechanisme
maakt gebruik van de storage-clientbibliotheek Hallo [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in volgorde tooencrypt gebruikersgegevens. In het bijzonder [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) modus met AES. Elk service enigszins anders werkt zodat elk van deze hier worden besproken.

### <a name="blobs"></a>Blobs
Hallo-clientbibliotheek biedt momenteel ondersteuning voor versleuteling van de hele BLOB's. In het bijzonder versleuteling wordt ondersteund wanneer gebruikers Hallo gebruiken **uploaden*** methoden of Hallo **openOutputStream** methode. Voor downloads, zowel volledige als bereik downloads worden ondersteund.  

Hallo-clientbibliotheek wordt tijdens het versleutelen kan genereren van een willekeurige initialisatie Vector (IV) van 16 bytes, samen met een willekeurige inhoud versleutelingssleutel (CEK) 32 bytes en uitvoeren van envelop versleuteling van blobgegevens Hallo met behulp van deze informatie. Hallo CEK ingepakt en een aantal aanvullende metagegevens worden vervolgens opgeslagen als blob-metagegevens samen met de Hallo versleutelde blob op Hallo-service.

> [!WARNING]
> Als u bewerkt of uw eigen metagegevens voor Hallo blob uploaden, moet u tooensure dat deze metagegevens behouden blijft. Als u nieuwe metagegevens zonder deze metagegevens uploadt, Hallo verpakte CEK IV en andere metagegevens niet verloren en Hallo blob-inhoud wordt nooit meer worden opgehaald.
> 
> 

Downloaden van een versleutelde blob omvat het ophalen van inhoud van de hele Hallo-blob met Hallo Hallo  **downloaden*/openInputStream** gemak methoden. Hallo verpakte CEK is al en gebruikt in combinatie met de Hallo IV (opgeslagen als blobmetagegevens in dit geval) tooreturn Hallo ontsleuteld data toohello gebruikers.

Downloaden van een willekeurig bereik (**downloadRange*** methoden) in Hallo versleutelde blob omvat het Hallo-bereik aanpassen, opgegeven door gebruikers in de volgorde tooget een kleine hoeveelheid aanvullende gegevens die gebruikt toosuccessfully worden kunnen Hallo ontsleutelen gevraagde bereik.  

Alle blob-typen (blok-blobs, pagina-blobs en toevoeg-blobs) kunnen worden versleuteld/ontsleuteld met behulp van dit schema.

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
3. Hallo CEK ingepakt en een aantal aanvullende metagegevens worden vervolgens opgeslagen als twee extra gereserveerde eigenschappen. Hallo eerste gereserveerde eigenschap (_ClientEncryptionMetadata1) is een tekenreekseigenschap dat Hallo informatie over IV, versie en verpakte sleutel bevat. Hallo tweede gereserveerde eigenschap (_ClientEncryptionMetadata2) is een binaire eigenschap van de Hallo informatie over het Hallo-eigenschappen die zijn versleuteld. Hallo-informatie in deze tweede eigenschap (_ClientEncryptionMetadata2) is versleuteld.  
4. Vervaldatum toothese extra gereserveerde vereiste eigenschappen voor versleuteling, kunnen gebruikers nu alleen 250 aangepaste eigenschappen in plaats van 252 hebben. totale grootte van entiteit Hallo Hallo moet minder dan 1MB.  
   
   Houd er rekening mee dat alleen de tekenreekseigenschappen van de kunnen worden versleuteld. Als andere typen eigenschappen toobe versleuteld zijn, moeten ze geconverteerde toostrings zijn. Hallo versleutelde tekenreeksen op Hallo-service worden opgeslagen als binaire eigenschappen en ze back toostrings na de decodering worden omgezet.
   
   Voor tabellen bovendien toohello versleutelingsbeleid, gebruikers moeten opgeven Hallo eigenschappen toobe versleuteld. Dit kan worden gedaan door een kenmerk [versleutelen] (voor POCO-entiteiten die zijn afgeleid van TableEntity) of een omzetter versleuteling in de aanvraag-opties. Een oplossing versleuteling is een gemachtigde die ervoor zorgt dat een partitiesleutel, rijsleutel en de naam van eigenschap retourneert een Booleaanse waarde die aangeeft of de eigenschap die moet worden versleuteld. Hallo-clientbibliotheek gebruiken tijdens het versleutelen kan deze informatie toodecide toe of een eigenschap tijdens het schrijven van toohello kabel moet worden versleuteld. Hallo gemachtigde biedt ook de mogelijkheid Hallo van logica over hoe eigenschappen zijn gecodeerd. (Bijvoorbeeld als X, vervolgens versleutelen eigenschap A; anders versleutelen eigenschappen A en B.) Houd er rekening mee dat deze is niet nodig tooprovide deze informatie tijdens het lezen of het uitvoeren van query's entiteiten.

### <a name="batch-operations"></a>Batchbewerkingen
In batchbewerkingen, wordt hello dezelfde KEK gebruikt in alle Hallo rijen in de desbetreffende batchbewerking omdat de clientbibliotheek Hallo slechts staat één options-object (en daarom een beleid/KEK) per batchbewerking. Echter wordt Hallo-clientbibliotheek intern Genereer een nieuwe willekeurige IV en willekeurige CEK per rij in een batch Hallo. Gebruikers kunnen ook kiezen tooencrypt verschillende eigenschappen voor elke bewerking in batch Hallo door dit gedrag definiëren in Hallo versleuteling resolver.

### <a name="queries"></a>Query's
tooperform querybewerkingen, moet u een sleutel resolver die kunnen tooresolve alle sleutels in de resultatenset Hallo Hallo. Als een entiteit die is opgenomen in het queryresultaat Hallo niet kan opgelost tooa provider worden, Hallo-clientbibliotheek genereert een fout opgetreden. Voor elke query die server side projecties uitvoert, wordt de clientbibliotheek Hallo Hallo speciale versleuteling metagegevenseigenschappen (_ClientEncryptionMetadata1 en _ClientEncryptionMetadata2) toevoegen door standaardkolommen toohello geselecteerd.

## <a name="azure-key-vault"></a>Azure Key Vault
Met Azure Key Vault kunt u de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services worden gebruikt. Met Azure Sleutelkluis gebruikers kunnen sleutels en geheimen versleutelen (zoals verificatiesleutels, opslagaccountsleutels, gegevensversleutelingssleutels. PFX-bestanden en wachtwoorden) met behulp van de sleutels die worden beveiligd door hardware security modules (HSM's). Zie voor meer informatie [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md).

Hallo storage-clientbibliotheek gebruikt Hallo Sleutelkluis-kernbibliotheek in volgorde tooprovide een gemeenschappelijk framework op Azure voor het beheren van sleutels. Gebruikers krijgen ook Hallo extra voordeel van het gebruik van Hallo Sleutelkluis extensies bibliotheek. Hallo extensies-bibliotheek biedt functionaliteit om eenvoudig en naadloze Symmetric/RSA lokale en cloud sleutel providers en met aggregatie en opslaan in cache.

### <a name="interface-and-dependencies"></a>Interface en afhankelijkheden
Er zijn drie Sleutelkluis-pakketten:  

* Azure-keyvault-core bevat Hallo IKey en IKeyResolver. Er is een klein pakket zonder afhankelijkheden. opslagclientbibliotheek voor Java Hello wordt gedefinieerd als een afhankelijkheid.
* Azure-keyvault bevat Hallo Sleutelkluis REST client.  
* Azure-keyvault-extensies bevat de extensiecode die bevat implementaties van cryptografische algoritmen en een RSAKey en een SymmetricKey. Het is afhankelijk van Hallo Core en KeyVault-naamruimten en functionaliteit toodefine biedt een cumulatieve resolver (wanneer gebruikers toouse meerdere sleutels providers willen) en een cache in belangrijke resolver. Hoewel Hallo storage-clientbibliotheek niet rechtstreeks afhankelijk van dit pakket is als gebruikers toouse Azure Key Vault toostore hun sleutels of toouse hello Sleutelkluis extensies tooconsume Hallo lokale wilt en cloud cryptografische providers, moeten ze dit pakket.  
  
  Sleutelkluis is ontworpen voor hoge waarde hoofdsleutels en bandbreedteregeling limieten per Sleutelkluis zijn ontworpen met dit in gedachten. Bij het uitvoeren van versleuteling aan clientzijde met Sleutelkluis is Hallo voorkeur model toouse symmetrische hoofdsleutels opgeslagen als geheimen in de Sleutelkluis en lokaal opgeslagen in de cache. Gebruikers moeten doen Hallo volgende:  

1. Maken van een geheim offline en upload het tooKey kluis.  
2. Gebruik van het geheim Hallo base-id als een parameter tooresolve Hallo van de huidige versie van Hallo geheim voor versleuteling en deze informatie lokaal in de cache. CachingKeyResolver gebruiken voor het opslaan in cache; gebruikers zijn niet de verwachte tooimplement hun eigen caching logica.  
3. Hallo caching resolver gebruikt als invoer tijdens het maken van Hallo versleutelingsbeleid.
   Meer informatie over het gebruik van de Sleutelkluis vindt u in de codevoorbeelden Hallo-versleuteling. <fix URL>  

## <a name="best-practices"></a>Aanbevolen procedures
Ondersteuning voor codering is alleen beschikbaar in Hallo opslagclientbibliotheek voor Java.

> [!IMPORTANT]
> Wanneer met behulp van versleuteling aan clientzijde, worden op de hoogte van deze belangrijke punten:
> 
> * Lezen van of schrijven tooan versleuteld wanneer blob, gebruik hele blob uploaden opdrachten en bereik/geheel blob downloaden opdrachten. Vermijd schrijven tooan versleutelde blob met protocolbewerkingen zoals het blok plaatsen, blokkeringslijst plaatsen, pagina's schrijven, wissen's of toevoeg-blok; anders u mogelijk Hallo versleutelde blob beschadigd en onleesbaar.
> * Een vergelijkbaar beperking bestaat voor tabellen. Worden zorgvuldige toonot update versleuteld eigenschappen zonder Hallo versleutelingsmetagegevens worden bijgewerkt.  
> * Als u de metagegevens op Hallo versleutelde blob instelt, overschrijft u mogelijk Hallo versleutelingsgerelateerde metagegevens die vereist is voor ontsleuteling, omdat de instelling van metagegevens is niet-additieve. Dit geldt ook voor momentopnamen; Vermijd metagegevens tijdens het maken van een momentopname van een versleutelde blob. Als metagegevens moet worden ingesteld, moet u ervoor toocall hello **downloadAttributes** methode eerste tooget Hallo huidige versleutelingsmetagegevens en gelijktijdige schrijfbewerkingen voorkomen tijdens het instellen van metagegevens.  
> * Hallo inschakelen **requireEncryption** vlag in Hallo standaardopties aanvraag voor gebruikers die normaal alleen met gecodeerde gegevens werken gesproken. Zie hieronder voor meer informatie.  
> 
> 

## <a name="client-api--interface"></a>Client-API / Interface
Tijdens het maken van een object EncryptionPolicy gebruikers alleen een sleutel (IKey implementeren), krijgt alleen een resolver (IKeyResolver implementeren) of beide. IKey is Hallo basic type sleutel dat wordt geïdentificeerd met een sleutel-id en biedt Hallo logica voor onmiddellijke/uitpakken. Gebruikte tooresolve een sleutel is IKeyResolver tijdens het Hallo-decoderingsproces. Hiermee definieert u een methode ResolveKey die als resultaat een IKey een sleutel-id opgegeven geeft. Dit biedt gebruikers Hallo mogelijkheid toochoose tussen meerdere sleutels die worden beheerd op meerdere locaties.

* Hallo-sleutel wordt altijd gebruikt voor versleuteling, en Hallo afwezigheid van een sleutel in een fout resulteert.  
* Voor ontsleuteling:  
  
  * Hallo sleutel resolver wordt opgeroepen als tooget Hallo sleutel opgegeven. Als het Hallo-omzetter wordt opgegeven, maar heeft geen een toewijzing voor Hallo sleutel-id, wordt er een fout gegenereerd.  
  * Als conflictoplosser niet is opgegeven, maar een sleutel is opgegeven, worden de Hallo-sleutel wordt gebruikt als de id overeenkomt met de Hallo vereist sleutel-id. Als het Hallo-id komt niet overeen met, wordt een fout gegenereerd.  
    
    Hallo [versleuteling voorbeelden](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>demonstreren van een meer gedetailleerde end-to-end-scenario voor blobs, wachtrijen en tabellen, samen met Sleutelkluis-integratie.

### <a name="requireencryption-mode"></a>RequireEncryption modus
Gebruikers kunnen eventueel inschakelen voor een werkmodus waar alle uploaden en downloaden moeten worden versleuteld. In deze modus mislukt pogingen tooupload gegevens zonder een beleid of download Versleutelingsgegevens is niet versleuteld op Hallo-service op Hallo client. Hallo **requireEncryption** van de markering van Hallo opties Aanvraagobject bepaalt dit gedrag. Als uw toepassing, worden alle objecten die zijn opgeslagen in Azure Storage gecodeerd, dan u dat Hallo instellen kunt **requireEncryption** -eigenschap op Hallo standaardopties aanvraag voor het object Hallo service-client.   

Bijvoorbeeld: **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** toorequire versleuteling voor alle bewerkingen van de blob wordt uitgevoerd via dat clientobject.

### <a name="blob-service-encryption"></a>Versleuteling van BLOB-service
Maak een **BlobEncryptionPolicy** object en stel deze in Hallo aanvraag opties (per API of op een client met behulp van **DefaultRequestOptions**). Alle andere wordt verwerkt door de clientbibliotheek Hallo intern.

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set hello encryption policy on hello request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload hello encrypted contents toohello blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt hello encrypted contents from hello blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Wachtrij-service: versleuteling
Maak een **QueueEncryptionPolicy** object en stel deze in Hallo aanvraag opties (per API of op een client met behulp van **DefaultRequestOptions**). Alle andere wordt verwerkt door de clientbibliotheek Hallo intern.

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a>Tabel-service: versleuteling
Bovendien toocreating een versleutelingsbeleid voor en instellen op verzoek-opties, u moet opgeven een **EncryptionResolver** in **TableRequestOptions**, of stel Hallo [versleutelen]-kenmerk op Hallo van entiteit getter en setter.

### <a name="using-hello-resolver"></a>Hallo conflictoplosser

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

TableRequestOptions options = new TableRequestOptions()
options.setEncryptionPolicy(policy);
options.setEncryptionResolver(new EncryptionResolver() {
    public boolean encryptionResolver(String pk, String rk, String key) {
        if (key == "foo")
        {
            return true;
        }
        return false;
    }
});

// Insert Entity
currentTable.execute(TableOperation.insert(ent), options, null);

// Retrieve Entity
// No need toospecify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a>Met behulp van kenmerken
Zoals eerder vermeld, als de entiteit Hallo TableEntity implementeert, vervolgens Hallo eigenschappen-getter en setter kunt gedecoreerd worden met kenmerk in plaats van Hallo Hallo [versleutelen] **EncryptionResolver**.

```java
private string encryptedProperty1;

@Encrypt
public String getEncryptedProperty1 () {
    return this.encryptedProperty1;
}

@Encrypt
public void setEncryptedProperty1(final String encryptedProperty1) {
    this.encryptedProperty1 = encryptedProperty1;
}
```

## <a name="encryption-and-performance"></a>Versleuteling en prestaties
Houd er rekening mee dat de opslag, resulteert in extra prestatieoverhead versleutelt. Hallo inhoud sleutel en IV moet worden gegenereerd, Hallo inhoud zelf moet worden versleuteld en aanvullende metagegevens moet zijn geformatteerd en geüpload. Deze overhead is afhankelijk van Hallo en de hoeveelheid gegevens wordt versleuteld. Het is raadzaam dat klanten hun toepassingen voor de prestaties tijdens de ontwikkeling altijd testen.

## <a name="next-steps"></a>Volgende stappen
* Hallo downloaden [Azure Storage-clientbibliotheek voor Java-Maven-pakket](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)  
* Hallo downloaden [Azure Storage-clientbibliotheek voor Java-broncode vanuit GitHub](https://github.com/Azure/azure-storage-java)   
* Download hello Azure Key Vault Maven-bibliotheek voor Java-Maven-pakketten:
  * [Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) pakket
  * [Client](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) pakket
* Ga naar Hallo [Azure Key Vault-documentatie](../../key-vault/key-vault-whatis.md)
