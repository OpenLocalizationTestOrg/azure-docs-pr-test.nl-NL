## <a name="configure-your-application-tooaccess-azure-storage"></a>Configureren van uw toepassing tooaccess Azure Storage
Er zijn twee manieren tooauthenticate van uw toepassing tooaccess Storage-services:

* Gedeelde sleutel: Gedeelde sleutel gebruiken alleen voor testdoeleinden
* Shared Access Signature (SAS): Gebruik SAS voor productietoepassingen

### <a name="shared-key"></a>Gedeelde sleutel
Verificatie met een gedeelde sleutel betekent dat uw toepassing wordt de accountnaam van uw te gebruiken en key tooaccess Storage-services account. Voor de toepassing hello snel weergeven hoe toouse deze bibliotheek we zullen gebruikmaken van verificatie met gedeelde sleutel in deze aan de slag.

> [!WARNING] 
> **Alleen voor testdoeleinden verificatie met gedeelde sleutel gebruikt.** Uw accountnaam en accountsleutel, waardoor volledige lezen/schrijven toegang toohello Storage-account dat is gekoppeld, zijn gedistribueerde tooevery persoon die uw app wordt gedownload. Dit is **niet** een goede oefenen als u het risico dat uw sleutel in gevaar komt door niet-vertrouwde clients.
> 
> 

Als u verificatie met gedeelde sleutel gebruikt, maakt u een [verbindingsreeks](../articles/storage/common/storage-configure-connection-string.md). Hallo-verbindingsreeks bestaat uit:  

* Hallo **DefaultEndpointsProtocol** -kunt u HTTP of HTTPS. Gebruik van HTTPS wordt echter ten zeerste aanbevolen.
* Hallo **accountnaam** - hello naam van uw storage-account
* Hallo **Accountsleutel** - op Hallo [Azure Portal](https://portal.azure.com), gaat u tooyour storage-account en klikt u op Hallo **sleutels** pictogram toofind deze informatie.
* (Optioneel) **EndpointSuffix** -dit wordt gebruikt voor storage-services in regio's met een ander eindpunt achtervoegsels, zoals Azure China of Azure Governance.

Hier volgt een voorbeeld van een verbindingsreeks met verificatie met gedeelde sleutel:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Shared Access Signatures (SAS)
Voor een mobiele toepassing is hello aanbevolen methode voor het verifiëren van een aanvraag door een client tegen hello Azure Storage-service door een Shared Access Signature (SAS). SAS kunt u een client access tooa resource toogrant voor een opgegeven periode, met een opgegeven set machtigingen.
Als de eigenaar van het opslagaccount hello moet u voor uw mobiele clients tooconsume toogenerate een SAS. toogenerate Hallo SAS, zult u waarschijnlijk toowrite een afzonderlijke service waarmee Hallo SAS toobe gedistribueerd tooyour clients wordt gegenereerd. Voor testdoeleinden kunt u Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) of Hallo [Azure Portal](https://portal.azure.com) toogenerate een SAS. Wanneer u Hallo SAS maakt, kunt u de tijdsinterval Hallo via welke Hallo SAS is geldig en Hallo-machtigingen die Hallo SAS verleent toohello client kunt opgeven.

Hallo volgende voorbeeld ziet u hoe toouse Hallo toogenerate van Microsoft Azure Storage Explorer een SAS.

1. Als u dat nog niet gedaan hebt, [installeren Hallo Microsoft Azure Storage Explorer](http://storageexplorer.com)
2. Verbinding maken met tooyour abonnement.
3. Klik op uw Storage-account en klik op tabblad Hallo 'acties' hello onder, links in. Klik op 'Shared Access Signature ophalen' toogenerate een verbinding-tekenreeks voor uw SAS.
4. Hier volgt een voorbeeld van een SAS-verbindingsreeks dat verleent machtigingen lezen en op Hallo-service, container en objectniveau voor Hallo blob-service van het Hallo-opslagaccount schrijven.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Zoals u ziet, wanneer u een SAS, bent u niet de sleutel van uw weergeeft in uw toepassing. U kunt meer informatie over SAS en aanbevolen procedures voor het gebruik van SAS door het uitchecken van [Shared Access Signatures: inzicht Hallo SAS-model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

