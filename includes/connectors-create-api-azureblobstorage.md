### <a name="prerequisites"></a>Vereisten
* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [Azure Blob Storage-account](../articles/storage/common/storage-create-storage-account.md) inclusief Hallo opslagaccountnaam en de toegangssleutel. Deze informatie wordt vermeld in de eigenschappen van Hallo van Hallo-opslagaccount in hello Azure-portal. Lees meer over [Azure Storage](../articles/storage/common/storage-introduction.md).

Voordat u uw Azure Blob Storage-account in een logische app, tooyour Azure Blob Storage-account te koppelen. U kunt dit eenvoudig doen in uw logische app op Hallo Azure-portal.  

Verbinding maken met tooyour Azure Blob Storage-account met behulp van Hallo stappen te volgen:  

1. Een logische app maken. In Hallo Logic Apps designer een trigger toevoegen en voeg vervolgens een actie. Selecteer **beheerde API's van Microsoft weergeven** in Hallo vervolgkeuzelijst en voer vervolgens 'blob' in het zoekvak Hallo. Selecteer een Hallo acties:  
   
    ![Stap met Azure Blob Storage verbinding maken](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Als u nog niet eerder hebt gemaakt verbindingen tooAzure opslag, wordt u gevraagd de verbindingsdetails Hallo op te geven:   
   
    ![Stap met Azure Blob Storage verbinding maken](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Voer accountdetails Hallo-opslag. Eigenschappen met een sterretje zijn vereist.
   
   | Eigenschap | Details |
   | --- | --- |
   | Verbindingsnaam * |Voer een naam voor de verbinding. |
   | Naam van het Azure-Opslagaccount * |Voer opslagaccountnaam Hallo. Hallo opslagaccountnaam wordt weergegeven in de eigenschappen van het Hallo-opslag in hello Azure-portal. |
   | Azure Storage-Accounttoegangssleutel * |Hallo opslagaccountsleutel invoeren. Hallo toegangstoetsen worden weergegeven in eigenschappen van het Hallo-opslag in hello Azure-portal. |
   
    Deze referenties gebruikte tooauthorize uw logische app tooconnect zijn en toegang tot uw gegevens. 
4. Selecteer **Maken**.
5. Kennisgeving Hallo verbinding is gemaakt. Nu gaat u verder met hello, andere stappen in uw logische app: 
   
    ![Stap met Azure Blob Storage verbinding maken](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

