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
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="44e20-103">Azure Functions externe tabel binding (Preview)</span><span class="sxs-lookup"><span data-stu-id="44e20-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="44e20-104">Dit artikel laat zien hoe de tabelgegevens toomanipulate op aanbieders van SaaS (zoals Sharepoint, Dynamics) binnen de functie met ingebouwde bindingen.</span><span class="sxs-lookup"><span data-stu-id="44e20-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="44e20-105">Azure Functions ondersteunt de invoer en uitvoer bindingen voor externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="44e20-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="44e20-106">API-verbindingen</span><span class="sxs-lookup"><span data-stu-id="44e20-106">API Connections</span></span>

<span data-ttu-id="44e20-107">Tabelverbindingen gebruikmaken van externe API verbindingen tooauthenticate met 3e SaaS leveranciers.</span><span class="sxs-lookup"><span data-stu-id="44e20-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="44e20-108">Bij het toewijzen van een binding kunt u een nieuwe API-verbinding te maken of moet u een bestaande verbinding API binnen hello gebruiken dezelfde resourcegroep</span><span class="sxs-lookup"><span data-stu-id="44e20-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="44e20-109">Ondersteunde API-verbindingen (tabel) s</span><span class="sxs-lookup"><span data-stu-id="44e20-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="44e20-110">Connector</span><span class="sxs-lookup"><span data-stu-id="44e20-110">Connector</span></span>|<span data-ttu-id="44e20-111">Trigger</span><span class="sxs-lookup"><span data-stu-id="44e20-111">Trigger</span></span>|<span data-ttu-id="44e20-112">Invoer</span><span class="sxs-lookup"><span data-stu-id="44e20-112">Input</span></span>|<span data-ttu-id="44e20-113">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="44e20-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="44e20-114">DB2</span><span class="sxs-lookup"><span data-stu-id="44e20-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="44e20-115">x</span><span class="sxs-lookup"><span data-stu-id="44e20-115">x</span></span>|<span data-ttu-id="44e20-116">x</span><span class="sxs-lookup"><span data-stu-id="44e20-116">x</span></span>
|[<span data-ttu-id="44e20-117">Dynamics 365 voor bewerkingen</span><span class="sxs-lookup"><span data-stu-id="44e20-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="44e20-118">x</span><span class="sxs-lookup"><span data-stu-id="44e20-118">x</span></span>|<span data-ttu-id="44e20-119">x</span><span class="sxs-lookup"><span data-stu-id="44e20-119">x</span></span>
|[<span data-ttu-id="44e20-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="44e20-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="44e20-121">x</span><span class="sxs-lookup"><span data-stu-id="44e20-121">x</span></span>|<span data-ttu-id="44e20-122">x</span><span class="sxs-lookup"><span data-stu-id="44e20-122">x</span></span>
|[<span data-ttu-id="44e20-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="44e20-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="44e20-124">x</span><span class="sxs-lookup"><span data-stu-id="44e20-124">x</span></span>|<span data-ttu-id="44e20-125">x</span><span class="sxs-lookup"><span data-stu-id="44e20-125">x</span></span>
|[<span data-ttu-id="44e20-126">Google Spreadsheets</span><span class="sxs-lookup"><span data-stu-id="44e20-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="44e20-127">x</span><span class="sxs-lookup"><span data-stu-id="44e20-127">x</span></span>|<span data-ttu-id="44e20-128">x</span><span class="sxs-lookup"><span data-stu-id="44e20-128">x</span></span>
|[<span data-ttu-id="44e20-129">Informix</span><span class="sxs-lookup"><span data-stu-id="44e20-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="44e20-130">x</span><span class="sxs-lookup"><span data-stu-id="44e20-130">x</span></span>|<span data-ttu-id="44e20-131">x</span><span class="sxs-lookup"><span data-stu-id="44e20-131">x</span></span>
|[<span data-ttu-id="44e20-132">Dynamics 365 voor financiële gegevens</span><span class="sxs-lookup"><span data-stu-id="44e20-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="44e20-133">x</span><span class="sxs-lookup"><span data-stu-id="44e20-133">x</span></span>|<span data-ttu-id="44e20-134">x</span><span class="sxs-lookup"><span data-stu-id="44e20-134">x</span></span>
|[<span data-ttu-id="44e20-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="44e20-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="44e20-136">x</span><span class="sxs-lookup"><span data-stu-id="44e20-136">x</span></span>|<span data-ttu-id="44e20-137">x</span><span class="sxs-lookup"><span data-stu-id="44e20-137">x</span></span>
|[<span data-ttu-id="44e20-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="44e20-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="44e20-139">x</span><span class="sxs-lookup"><span data-stu-id="44e20-139">x</span></span>|<span data-ttu-id="44e20-140">x</span><span class="sxs-lookup"><span data-stu-id="44e20-140">x</span></span>
|[<span data-ttu-id="44e20-141">Algemene gegevensservice</span><span class="sxs-lookup"><span data-stu-id="44e20-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="44e20-142">x</span><span class="sxs-lookup"><span data-stu-id="44e20-142">x</span></span>|<span data-ttu-id="44e20-143">x</span><span class="sxs-lookup"><span data-stu-id="44e20-143">x</span></span>
|[<span data-ttu-id="44e20-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="44e20-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="44e20-145">x</span><span class="sxs-lookup"><span data-stu-id="44e20-145">x</span></span>|<span data-ttu-id="44e20-146">x</span><span class="sxs-lookup"><span data-stu-id="44e20-146">x</span></span>
|[<span data-ttu-id="44e20-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="44e20-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="44e20-148">x</span><span class="sxs-lookup"><span data-stu-id="44e20-148">x</span></span>|<span data-ttu-id="44e20-149">x</span><span class="sxs-lookup"><span data-stu-id="44e20-149">x</span></span>
|[<span data-ttu-id="44e20-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="44e20-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="44e20-151">x</span><span class="sxs-lookup"><span data-stu-id="44e20-151">x</span></span>|<span data-ttu-id="44e20-152">x</span><span class="sxs-lookup"><span data-stu-id="44e20-152">x</span></span>
|[<span data-ttu-id="44e20-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="44e20-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="44e20-154">x</span><span class="sxs-lookup"><span data-stu-id="44e20-154">x</span></span>|<span data-ttu-id="44e20-155">x</span><span class="sxs-lookup"><span data-stu-id="44e20-155">x</span></span>
|<span data-ttu-id="44e20-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="44e20-156">UserVoice</span></span>||<span data-ttu-id="44e20-157">x</span><span class="sxs-lookup"><span data-stu-id="44e20-157">x</span></span>|<span data-ttu-id="44e20-158">x</span><span class="sxs-lookup"><span data-stu-id="44e20-158">x</span></span>
|<span data-ttu-id="44e20-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="44e20-159">Zendesk</span></span>||<span data-ttu-id="44e20-160">x</span><span class="sxs-lookup"><span data-stu-id="44e20-160">x</span></span>|<span data-ttu-id="44e20-161">x</span><span class="sxs-lookup"><span data-stu-id="44e20-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="44e20-162">Verbindingen met externe tabel kunnen ook worden gebruikt [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="44e20-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="44e20-163">Maken van een API-verbinding: stap voor stap</span><span class="sxs-lookup"><span data-stu-id="44e20-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="44e20-164">Maak een functie > aangepaste functie ![geen aangepaste functie maken](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="44e20-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="44e20-165">Scenario `Experimental`  >  `ExternalTable-CSharp` sjabloon > Maak een nieuwe `External Table connection` 
 ![invoer sjabloon kiezen](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="44e20-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="44e20-166">Kies uw SaaS-provider > Kies/maken van een verbinding ![configureren SaaS-verbinding](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="44e20-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="44e20-167">Selecteer uw API-verbinding > Hallo-functie maken ![tabelfunctie maken](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="44e20-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="44e20-168">Selecteer`Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="44e20-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="44e20-169">Hallo verbinding toouse uw doeltabel configureren.</span><span class="sxs-lookup"><span data-stu-id="44e20-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="44e20-170">Deze instellingen wordt zeer tussen aanbieders van SaaS.</span><span class="sxs-lookup"><span data-stu-id="44e20-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="44e20-171">Ze zijn overzicht hieronder in [gegevensbron instellingen](#datasourcesettings)
![tabel configureren](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="44e20-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="44e20-172">Gebruik</span><span class="sxs-lookup"><span data-stu-id="44e20-172">Usage</span></span>

<span data-ttu-id="44e20-173">In dit voorbeeld maakt verbinding met de naam 'Neem contact op met' met Id, LastName en FirstName kolommen tooa-tabel.</span><span class="sxs-lookup"><span data-stu-id="44e20-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="44e20-174">Hallo-code bevat Hallo Contact entiteiten in de tabel Hallo en logboeken voor- en achternamen Hallo.</span><span class="sxs-lookup"><span data-stu-id="44e20-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="44e20-175">Bindingen</span><span class="sxs-lookup"><span data-stu-id="44e20-175">Bindings</span></span>
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
<span data-ttu-id="44e20-176">`entityId`moet leeg zijn voor Tabelverbindingen.</span><span class="sxs-lookup"><span data-stu-id="44e20-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="44e20-177">`ConnectionAppSettingsKey`Hallo app-instelling die wordt Hallo API-verbindingsreeks opgeslagen identificeert.</span><span class="sxs-lookup"><span data-stu-id="44e20-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="44e20-178">Hallo app-instelling wordt automatisch gemaakt wanneer u een API toevoegen verbinding in Hallo UI integreren.</span><span class="sxs-lookup"><span data-stu-id="44e20-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="44e20-179">Een in tabelvorm connector biedt gegevenssets en elke gegevensset tabellen bevat.</span><span class="sxs-lookup"><span data-stu-id="44e20-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="44e20-180">Hallo-naam van de standaardgegevensset Hallo is 'standaard'.</span><span class="sxs-lookup"><span data-stu-id="44e20-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="44e20-181">Hallo titels voor een gegevensset en een tabel in verschillende SaaS-providers worden hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="44e20-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="44e20-182">Connector</span><span class="sxs-lookup"><span data-stu-id="44e20-182">Connector</span></span>|<span data-ttu-id="44e20-183">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="44e20-183">Dataset</span></span>|<span data-ttu-id="44e20-184">Tabel</span><span class="sxs-lookup"><span data-stu-id="44e20-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="44e20-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="44e20-185">**SharePoint**</span></span>|<span data-ttu-id="44e20-186">Site</span><span class="sxs-lookup"><span data-stu-id="44e20-186">Site</span></span>|<span data-ttu-id="44e20-187">SharePoint-lijst</span><span class="sxs-lookup"><span data-stu-id="44e20-187">SharePoint List</span></span>
|<span data-ttu-id="44e20-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="44e20-188">**SQL**</span></span>|<span data-ttu-id="44e20-189">Database</span><span class="sxs-lookup"><span data-stu-id="44e20-189">Database</span></span>|<span data-ttu-id="44e20-190">Tabel</span><span class="sxs-lookup"><span data-stu-id="44e20-190">Table</span></span> 
|<span data-ttu-id="44e20-191">**Google blad**</span><span class="sxs-lookup"><span data-stu-id="44e20-191">**Google Sheet**</span></span>|<span data-ttu-id="44e20-192">Werkblad</span><span class="sxs-lookup"><span data-stu-id="44e20-192">Spreadsheet</span></span>|<span data-ttu-id="44e20-193">Werkblad</span><span class="sxs-lookup"><span data-stu-id="44e20-193">Worksheet</span></span> 
|<span data-ttu-id="44e20-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="44e20-194">**Excel**</span></span>|<span data-ttu-id="44e20-195">Excel-bestand</span><span class="sxs-lookup"><span data-stu-id="44e20-195">Excel file</span></span>|<span data-ttu-id="44e20-196">Blad</span><span class="sxs-lookup"><span data-stu-id="44e20-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="44e20-197">Gebruik in C#</span><span class="sxs-lookup"><span data-stu-id="44e20-197">Usage in C#</span></span> #

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

<span data-ttu-id="44e20-198"><!--
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
##Instellingen voor de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="44e20-198"><!--
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
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="44e20-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="44e20-199">SQL Server</span></span>

<span data-ttu-id="44e20-200">Hallo script toocreate en vullen Hallo Neem contact op met tabel is lager dan.</span><span class="sxs-lookup"><span data-stu-id="44e20-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="44e20-201">dataSetName is 'standaard'.</span><span class="sxs-lookup"><span data-stu-id="44e20-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="44e20-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="44e20-202">Google Sheets</span></span>
<span data-ttu-id="44e20-203">In Google Docs, maakt u een werkblad met een werkblad met de naam `Contact`.</span><span class="sxs-lookup"><span data-stu-id="44e20-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="44e20-204">Hallo-connector niet Hallo werkblad weergegeven naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44e20-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="44e20-205">de interne naam Hello (in de vet weergegeven) moet toobe gebruikt als dataSetName, bijvoorbeeld: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  Hallo kolomnamen toevoegen `Id`, `LastName`, `FirstName` toohello eerst rij en vervolgens de gegevens op te vullen volgende rijen.</span><span class="sxs-lookup"><span data-stu-id="44e20-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="44e20-206">SalesForce</span><span class="sxs-lookup"><span data-stu-id="44e20-206">Salesforce</span></span>
<span data-ttu-id="44e20-207">dataSetName is 'standaard'.</span><span class="sxs-lookup"><span data-stu-id="44e20-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e20-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44e20-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
