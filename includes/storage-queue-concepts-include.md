## <a name="what-is-queue-storage"></a>Wat is Queue Storage?
Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.

Veelvoorkomende toepassingen van Queue Storage zijn onder andere:

* Een achterstand van werk tooprocess maken asynchroon
* Doorgeven van berichten van een Azure-web-rol tooan Azure-werkrol

## <a name="queue-service-concepts"></a>Concepten van Queue-service
Hallo Queue-service bevat Hallo volgende onderdelen:

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* **URL-indeling:** wachtrijen worden opgevraagd met Hallo URL-indeling te volgen:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    URL na Hello wordt een wachtrij in Hallo diagram:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Storage-Account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Zie [Azure Storage Scalability and Performance Targets](../articles/storage/common/storage-scalability-targets.md) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.
* **Wachtrij:** Een wachtrij bevat een set berichten. Alle berichten moeten zich in een wachtrij bevinden. Houd er rekening mee dat Hallo wachtrijnaam moet alleen kleine letters bevatten. Zie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Wachtrijen en metagegevens een naam geven) voor informatie over de naamgeving van wachtrijen.
* **Bericht:** A-bericht, in een willekeurige indeling van up too64 KB. Hallo maximale tijd aan dat een bericht in de wachtrij Hallo blijven kan is 7 dagen.

