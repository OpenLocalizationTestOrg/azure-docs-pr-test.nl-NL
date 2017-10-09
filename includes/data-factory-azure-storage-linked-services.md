### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
Hallo **gekoppelde Azure Storage-service** kunt u een Azure storage-account tooan Azure data factory toolink met behulp van Hallo **accountsleutel**, waarmee u Hallo data factory met globale toegang toohello Azure Opslag. Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure gekoppelde Storage-service.

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureStorage** |Ja |
| connectionString |Geef informatie tooconnect tooAzure opslag voor de eigenschap connectionString Hallo nodig. |Ja |

Zie de volgende artikel voor stappen tooview/kopiëren Hallo accountsleutel voor een Azure Storage Hallo: [weergeven, kopiëren en opnieuw genereren opslag toegangssleutels](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Voorbeeld:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Sas van Azure Storage gekoppelde Service
Een shared access signature (SAS) biedt tooresources gedelegeerde toegang in uw opslagaccount. Hiermee kunt u een client toogrant beperkt tooobjects machtigingen in uw opslagaccount gedurende een bepaalde tijd en met een opgegeven set machtigingen, zonder tooshare de toegangssleutels van uw account. Hallo SAS is een URI die in de queryparameters alle Hallo gegevens die nodig zijn voor geverifieerde toegang tooa storage resource omvat. opslagbronnen tooaccess Hello SAS, Hallo-client moet alleen toopass in Hallo SAS toohello geschikte constructor of methode. Zie voor gedetailleerde informatie over SAS [Shared Access Signatures: inzicht Hallo SAS-Model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory nu ondersteunt alleen het **Service-SAS** maar geen Account-SAS. Zie [typen van handtekeningen voor gedeelde toegang](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) voor meer informatie over deze twee typen en hoe tooconstruct. Houd er rekening mee Hallo SAS-URL generable vanuit Azure-portal of Opslagverkenner is een SAS-Account, wat niet wordt ondersteund.
> 

Hallo SAS van Azure Storage gekoppelde service, kunt u een Azure Storage-Account tooan Azure data factory toolink met behulp van een Shared Access Signature (SAS). Het biedt Hallo data factory toegang beperkt/tijdsgebonden tooall/specifieke bronnen (blobcontainer) / in Hallo-opslag. Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure opslag SAS gekoppelde service. 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureStorageSas** |Ja |
| sasUri |Geef de Shared Access Signature URI toohello Azure Storage-resources zoals blob-container of tabel.  |Ja |

**Voorbeeld:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Bij het maken van een **SAS-URI**, Hallo volgende overwegen:  

* Stel de juiste lezen/schrijven **machtigingen** op objecten op basis van hoe Hallo gekoppelde service (lezen, schrijven, lezen/schrijven) wordt gebruikt in uw gegevensfactory.
* Stel **verlooptijdstip** op de juiste wijze. Zorg ervoor dat Hallo toegang tooAzure opslagobjecten verloopt niet binnen de actieve periode Hallo van Hallo-pijplijn.
* URI moet worden gemaakt op Hallo juiste container/blob of tabelniveau op basis van Hallo nodig. Een SAS-Uri tooan Azure-blob kan Hallo Data Factory-service tooaccess bepaalde blob. Een SAS-Uri tooan Azure blob-container kunt Hallo Data Factory-service tooiterate via blobs in de container. Als u toegang nodig hebt tooprovide meer/minder objecten later of update Hallo SAS URI, houd er rekening mee tooupdate Hallo gekoppelde service met de Hallo nieuwe URI.   

