---
title: aaaCopy gegevens tooand van Azure Data Lake Store | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens tooand van Data Lake Store met behulp van Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Kopiëren van gegevens tooand van Data Lake Store via Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens tooand van Azure Data Lake Store. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, een overzicht van de verplaatsing van gegevens met de Kopieeractiviteit.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **van Azure Data Lake Store** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Een Data Lake Store-account maken voordat u een pijplijn maakt met de Kopieeractiviteit. Zie voor meer informatie [aan de slag met Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Ondersteunde verificatietypen
Hallo Data Lake Store-connector ondersteunt de volgende verificatietypen:
* Verificatie van service-principal
* Verificatie van gebruikersreferenties (OAuth) 

Het is raadzaam dat u service-principal verificatie, met name voor een geplande gegevens opnieuw te kopiëren. Verlopen van het token kan gebeuren met verificatie van gebruikersreferenties. Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.

## <a name="get-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure Data Lake Store met verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn toocopy gegevens is toouse hello **Wizard kopiëren**. Zie voor een zelfstudie over het maken van een pijplijn met behulp van de Wizard kopiëren Hallo [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure Data Lake Store kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure Data Lake store tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure Data Lake Store, [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo. En u een andere dataset toospecify Hallo map en het bestandspad in Hallo Data Lake store Hallo gegevens gekopieerd van de blob-opslag Hallo bevat maken. Zie voor eigenschappen van gegevensset die specifieke tooAzure Data Lake Store, [eigenschappen van gegevensset](#dataset-properties) sectie.
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en AzureDataLakeStoreSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u van Azure Data Lake Store tooAzure Blob Storage kopiëren wilt, gebruikt u AzureDataLakeStoreSource en BlobSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure Data Lake Store, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.  

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure Data Lake Store zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-data-lake-store) sectie van dit artikel.

Hallo volgende secties bevatten informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory entiteiten specifieke tooData Lake Store zijn.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld. Maken van een gekoppelde service van het type **AzureDataLakeStore** toolink uw Data Lake Store gegevens tooyour data factory. Hallo volgende tabel beschrijft de JSON-elementen specifieke tooData Lake Store gekoppelde services. U kunt kiezen tussen service-principal en verificatie van gebruikersreferenties.

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **type** | de eigenschap type Hello te moet worden ingesteld**AzureDataLakeStore**. | Ja |
| **dataLakeStoreUri** | Informatie over hello Azure Data Lake Store-account. Deze informatie heeft een van de volgende indelingen Hallo: `https://[accountname].azuredatalakestore.net/webhdfs/v1` of `adl://[accountname].azuredatalakestore.net/`. | Ja |
| **abonnements-id** | Azure-abonnement-ID toowhich Hallo Data Lake Store-account hoort. | Vereist voor sink |
| **resourceGroupName** | Azure resource group name toowhich Hallo Data Lake Store-account hoort. | Vereist voor sink |

### <a name="service-principal-authentication-recommended"></a>Verificatie van de service principal (aanbevolen)
toouse service principal verificatie, de registratie een Toepassingsentiteit in Azure Active Directory (Azure AD) en verleen het Hallo toegang krijgen tot de tooData Lake Store. Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Noteer Hallo waarden, waarin u volgende toodefine Hallo gekoppelde service:
* Toepassings-id
* Sleutel van toepassing 
* Tenant-id

> [!IMPORTANT]
> Als u van Hallo Wizard kopiëren tooauthor gegevenspijplijnen gebruikmaakt, zorgt u ervoor dat u service-principal Hallo verlenen ten minste een **lezer** rol in toegangsbeheer (identiteits- en toegangsbeheer management) voor Hallo Data Lake Store-account. Ook ten minste verlenen Hallo service-principal **lezen + Execute** machtiging tooyour Data Lake Store hoofdmap ('/') en de onderliggende items. Anders ziet u mogelijk het Hallo-bericht "hello opgegeven referenties zijn ongeldig."<br/><br/>
Nadat u maken of bijwerken van een service-principal in Azure AD, kan het enkele minuten duren voordat Hallo wijzigingen tootake effect. Controleer Hallo service-principal en Data Lake Store-besturingselement toegangsbeheerlijst (ACL) configuraties. Als u nog steeds het Hallo-bericht 'hello opgegeven referenties zijn ongeldig' ziet, wacht even en probeer het opnieuw.

Verificatie van de service-principal door te geven van de volgende eigenschappen hello gebruiken:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **servicePrincipalId** | Geef Hallo van client-id op. | Ja |
| **servicePrincipalKey** | De sleutel van de toepassing hello opgeven. | Ja |
| **tenant** | Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt. U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal. | Ja |

**Voorbeeld: Service-principal-verificatie**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Verificatie van gebruikersreferenties
U kunt ook kunt u gebruiker referentie verificatie toocopy uit of tooData Lake Store door te geven Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **autorisatie** | Klik op Hallo **autoriseren** knop op Hallo Data Factory-Editor en voer uw referenties die Hallo automatisch gegenereerde autorisatie-URL toothis eigenschap toewijst. | Ja |
| **sessie-id** | OAuth-sessie-ID van Hallo OAuth-autorisatie-sessie. Elke sessie-ID is uniek en kan slechts één keer worden gebruikt. Deze instelling wordt automatisch gegenereerd wanneer u Hallo Data Factory-Editor. | Ja |

**Voorbeeld: Verificatie van gebruikersreferenties**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Verlopen van het token
Autorisatiecode die u genereren met behulp van Hallo Hallo **autoriseren** knop verloopt na een bepaalde hoeveelheid tijd. Hallo volgende bericht betekent dat verificatie Hallo token is verlopen:

Referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties. AADSTS70008: Hallo opgegeven toegangsmachtiging is verlopen of ingetrokken. Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21-09-31Z.

Hallo volgende tabel ziet u Hallo verlopen tijden van verschillende typen gebruikersaccounts:


| Gebruikerstype | Verloopt na |
|:--- |:--- |
| Gebruikersaccounts *niet* beheerd door Azure Active Directory (bijvoorbeeld @hotmail.com of @live.com) |12 uur |
| Gebruikersaccounts worden beheerd door Azure Active Directory |het is 14 dagen na de laatste segment Hallo uitvoeren <br/><br/>Als een segment op basis van een gekoppelde op basis van het OAuth-service wordt uitgevoerd in de 14 dagen ten minste eenmaal na 90 dagen |

Als u uw wachtwoord vóór Hallo token verlooptijd vallen wijzigt, wordt de Hallo-token onmiddellijk verloopt. Hier ziet u eerder in deze sectie het Hallo-bericht.

U kunt opnieuw autoriseren hello account met behulp van Hallo **autoriseren** knop wanneer Hallo-token tooredeploy Hallo verloopt gekoppelde service. U kunt ook de waarden voor Hallo genereren **sessionId** en **autorisatie** eigenschappen programmatisch met behulp van Hallo volgende code:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Zie voor meer informatie over Data Factory-klassen Hallo gebruikt in code Hallo Hallo [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [ Klasse AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen. Voeg een verwijzing tooversion `2.9.10826.1824` van `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` voor Hallo `WindowsFormsWebAuthenticationDialog` klasse die wordt gebruikt in Hallo-code.

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
toospecify een gegevensset toorepresent gegevens invoeren in een Data Lake Store, stelt u Hallo **type** eigenschap van het Hallo-gegevensset te**AzureDataLakeStore**. Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Data Lake Store gekoppelde service. Zie voor een volledige lijst van JSON-secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties van een gegevensset in JSON, zoals **structuur**, **beschikbaarheid**, en **beleid**, zijn identiek voor alle typen van de gegevensset (Azure SQL-database, blob van Azure en Azure-tabel voor voorbeeld). Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie zoals de locatie en indeling van gegevens in het gegevensarchief Hallo Hallo. 

Hallo **typeProperties** sectie voor een gegevensset van het type **AzureDataLakeStore** bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **folderPath** |Pad toohello container en map in Data Lake Store. |Ja |
| **Bestandsnaam** |Naam van het Hallo-bestand in Azure Data Lake Store. Hallo **fileName** eigenschap is optioneel en is hoofdlettergevoelig. <br/><br/>Als u opgeeft **fileName**, Hallo activiteit (inclusief kopiëren) werkt op Hallo specifiek bestand.<br/><br/>Wanneer **fileName** niet is opgegeven, kopie bevat alle bestanden in **folderPath** in Hallo invoergegevensset.<br/><br/>Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand heeft Hallo indeling gegevens. _GUID_.txt'. Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Nee |
| **partitionedBy** |Hallo **partitionedBy** eigenschap is optioneel. U kunt deze toospecify een dynamische pad en bestandsnaam voor timeseries gegevens. Bijvoorbeeld: **folderPath** kunnen als parameters worden gebruikt voor elk uur van gegevens. Zie voor meer informatie en voorbeelden [Hallo eigenschap partitionedBy](#using-partitionedby-property). |Nee |
| **indeling** | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, en  **ParquetFormat**. Set Hallo **type** eigenschap onder **indeling** tooone van deze waarden. Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties in Hallo [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel. <br><br> Als u toocopy bestanden wilt ' als-is ' tussen bestandsgebaseerde winkels (binaire kopiëren) overslaan Hallo `format` sectie in beide definities invoer en uitvoer gegevensset. |Nee |
| **compressie** | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus zijn **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

### <a name="hello-partitionedby-property"></a>Hallo partitionedBy eigenschap
Kunt u dynamische **folderPath** en **fileName** eigenschappen voor timeseries gegevens met Hallo **partitionedBy** eigenschap, Data Factory-functies en het systeem variabelen. Zie voor meer informatie, Hallo [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel.


In Hallo bijvoorbeeld na `{Slice}` is vervangen door de waarde Hallo van Hallo Data Factory systeemvariabele `SliceStart` in de opgegeven indeling Hallo (`yyyyMMddHH`). de naam van de Hallo `SliceStart` toohello begintijd van Hallo segment verwijst. Hallo `folderPath` eigenschap verschilt voor elk segment, zoals in `wikidatagateway/wikisampledataout/2014100103` of `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

In het volgende voorbeeld, Hallo jaar, maand, dag en tijd van Hallo `SliceStart` worden uitgepakt in verschillende variabelen die worden gebruikt door Hallo `folderPath` en `fileName` eigenschappen:
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Voor meer informatie over tijdreeks gegevenssets planning en segmenten, Zie Hallo [gegevenssets in Azure Data Factory](data-factory-create-datasets.md) en [Data Factory plannen en uitvoeren](data-factory-scheduling-and-execution.md) artikelen. 


## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

eigenschappen die beschikbaar zijn in Hallo Hallo **typeProperties** gedeelte van een activiteit variëren met elk activiteitstype. Voor een kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

**AzureDataLakeStoreSource** ondersteunt de volgende eigenschap in Hallo Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| **recursieve** |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True (standaardwaarde), False |Nee |


**AzureDataLakeStoreSink** ondersteunt de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| **copyBehavior** |Hiermee geeft u Hallo kopie gedrag. |<b>PreserveHierarchy</b>: Hallo bestandshiërarchie in de doelmap Hallo behouden blijft. Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.<br/><br/><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo worden gemaakt in het eerste niveau van de doelmap Hallo Hallo. Hallo doelbestanden worden gemaakt met de automatisch gegenereerde namen.<br/><br/><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als hello bestand of de blob-naam wordt opgegeven, is de samengevoegde bestandsnaam Hallo Hallo opgegeven naam. Hallo-bestandsnaam is anders wordt automatisch gegenereerd. |Nee |

### <a name="recursive-and-copybehavior-examples"></a>Voorbeelden van recursieve en copyBehavior
Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van recursieve en copyBehavior waarden.

| Recursieve | copyBehavior | Resulterende gedrag |
| --- | --- | --- |
| De waarde True |preserveHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met dezelfde structuur, als de bron Hallo Hallo<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| De waarde True |flattenHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5 |
| De waarde True |mergeFiles |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam |
| ONWAAR |preserveHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/><br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |
| ONWAAR |flattenHierarchy |Voor een bronmap Map1 Hello structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/><br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |
| ONWAAR |mergeFiles |Voor een bronmap Map1 Hello structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam. automatisch gegenereerde naam voor File1<br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |

## <a name="supported-file-and-compression-formats"></a>Ondersteunde indelingen voor bestands- en compressie
Zie voor meer informatie, Hallo [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand van Data Lake Store
Hallo volgen voorbeelden bieden voorbeeld JSON definities. U kunt deze voorbeeld definities toocreate een pijplijn met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). voorbeelden kunt u zien hoe Hallo toocopy gegevens tooand van Data Lake Store en Azure Blob storage. Echter, de gegevens kunnen worden gekopieerd _rechtstreeks_ vanaf elke Hallo bronnen tooany van Hallo ondersteund Put. Zie voor meer informatie Hallo sectie 'ondersteunde gegevensarchieven en indelingen' in hello [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md) artikel.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Voorbeeld: Gegevens kopiëren van Azure Blob Storage tooAzure Data Lake Store
Hallo voorbeeldcode in dit gedeelte ziet:

* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureDataLakeStoreSink](#copy-activity-properties).

Hallo voorbeelden laten zien hoe timeseries gegevens uit Azure Blob Storage is gekopieerd tooData Lake Store om het uur. 

**Een gekoppelde Azure Storage-service**

```JSON
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

**Gekoppelde service van Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.
>

**De Azure Blob-invoergegevensset**

In de Hallo voorbeeld te volgen, gegevens wordt opgehaald uit een nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad gebruikt Hallo jaar, maand en daggedeelte van de begintijd Hallo. Hallo-bestandsnaam Hallo uur gedeelte Hallo begintijd gebruikt. Hallo `"external": true` instelling informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Azure Data Lake Store uitvoergegevensset**

Hallo voorbeeld kopieën data tooData Lake Store te volgen. Nieuwe gegevens worden gekopieerd tooData Lake Store om het uur.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Kopieeractiviteit in een pijplijn met een blob-bron- en een Data Lake Store-sink**

Hallo voorbeeld te volgen, Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse Hallo invoer- en uitvoergegevenssets. Hallo kopieeractiviteit is geplande toorun om het uur. Hallo in Hallo pijplijn-JSON-definitie, `source` type is ingesteld, te`BlobSource`, en Hallo `sink` type is ingesteld, te`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Voorbeeld: Gegevens kopiëren van Azure Data Lake Store tooan Azure-blobopslag
Hallo voorbeeldcode in dit gedeelte ziet:

* Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [AzureDataLakeStoreSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo-code opgehaald-timeseries-gegevens uit Data Lake Store tooan Azure blob elk uur. 

**Gekoppelde service van Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.
>

**Een gekoppelde Azure Storage-service**

```JSON
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
**Azure Data Lake invoergegevensset**

In dit voorbeeld instelling `"external"` te`true` informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**De Azure Blob-uitvoergegevensset**

In de Hallo voorbeeld te volgen, gegevens worden geschreven tooa nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad gebruikt Hallo jaar, maand, dag en uur gedeelte van de begintijd Hallo.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Een kopieeractiviteit in een pijplijn met een Azure Data Lake Store-bron- en een blob-sink**

Hallo voorbeeld te volgen, Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse Hallo invoer- en uitvoergegevenssets. Hallo kopieeractiviteit is geplande toorun om het uur. Hallo in Hallo pijplijn-JSON-definitie, `source` type is ingesteld, te`AzureDataLakeStoreSource`, en Hallo `sink` type is ingesteld, te`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

U kunt ook kolommen uit Hallo bron gegevensset toocolumns in Hallo sink gegevensset toewijzen in Hallo kopie activiteitsdefinitie. Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en afstemmen
toolearn over Hallo factoren die van invloed op prestaties van de Kopieeractiviteit en hoe toooptimize, Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) artikel.
