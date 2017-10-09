---
title: aaaAzure functies externe tabel binding (Preview) | Microsoft Docs
description: Met behulp van de externe tabel bindingen in de Azure-functies
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Azure Functions externe tabel binding (Preview)
Dit artikel laat zien hoe de tabelgegevens toomanipulate op aanbieders van SaaS (zoals Sharepoint, Dynamics) binnen de functie met ingebouwde bindingen. Azure Functions ondersteunt de invoer en uitvoer bindingen voor externe tabellen.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>API-verbindingen

Tabelverbindingen gebruikmaken van externe API verbindingen tooauthenticate met 3e SaaS leveranciers. 

Bij het toewijzen van een binding kunt u een nieuwe API-verbinding te maken of moet u een bestaande verbinding API binnen hello gebruiken dezelfde resourcegroep

### <a name="supported-api-connections-tables"></a>Ondersteunde API-verbindingen (tabel) s

|Connector|Trigger|Invoer|Uitvoer|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 voor bewerkingen](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google Spreadsheets](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 voor financiële gegevens](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle Database](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Algemene gegevensservice](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> Verbindingen met externe tabel kunnen ook worden gebruikt [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

### <a name="creating-an-api-connection-step-by-step"></a>Maken van een API-verbinding: stap voor stap

1. Maak een functie > aangepaste functie ![geen aangepaste functie maken](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Scenario `Experimental`  >  `ExternalTable-CSharp` sjabloon > Maak een nieuwe `External Table connection` 
 ![invoer sjabloon kiezen](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Kies uw SaaS-provider > Kies/maken van een verbinding ![configureren SaaS-verbinding](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Selecteer uw API-verbinding > Hallo-functie maken ![tabelfunctie maken](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Selecteer`Integrate` > `External Table`
    1. Hallo verbinding toouse uw doeltabel configureren. Deze instellingen wordt zeer tussen aanbieders van SaaS. Ze zijn overzicht hieronder in [gegevensbron instellingen](#datasourcesettings)
![tabel configureren](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Gebruik

In dit voorbeeld maakt verbinding met de naam 'Neem contact op met' met Id, LastName en FirstName kolommen tooa-tabel. Hallo-code bevat Hallo Contact entiteiten in de tabel Hallo en logboeken voor- en achternamen Hallo.

### <a name="bindings"></a>Bindingen
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId`moet leeg zijn voor Tabelverbindingen.

`ConnectionAppSettingsKey`Hallo app-instelling die wordt Hallo API-verbindingsreeks opgeslagen identificeert. Hallo app-instelling wordt automatisch gemaakt wanneer u een API toevoegen verbinding in Hallo UI integreren.

Een in tabelvorm connector biedt gegevenssets en elke gegevensset tabellen bevat. Hallo-naam van de standaardgegevensset Hallo is 'standaard'. Hallo titels voor een gegevensset en een tabel in verschillende SaaS-providers worden hieronder weergegeven:

|Connector|Gegevensset|Tabel|
|:-----|:---|:---| 
|**SharePoint**|Site|SharePoint-lijst
|**SQL**|Database|Tabel 
|**Google blad**|Werkblad|Werkblad 
|**Excel**|Excel-bestand|Blad 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Gebruik in C# #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
##Instellingen voor de gegevensbron

### <a name="sql-server"></a>SQL Server

Hallo script toocreate en vullen Hallo Neem contact op met tabel is lager dan. dataSetName is 'standaard'.

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Google Sheets
In Google Docs, maakt u een werkblad met een werkblad met de naam `Contact`. Hallo-connector niet Hallo werkblad weergegeven naam gebruiken. de interne naam Hello (in de vet weergegeven) moet toobe gebruikt als dataSetName, bijvoorbeeld: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  Hallo kolomnamen toevoegen `Id`, `LastName`, `FirstName` toohello eerst rij en vervolgens de gegevens op te vullen volgende rijen.

### <a name="salesforce"></a>SalesForce
dataSetName is 'standaard'.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
