---
title: aaaChange feed voor HL7 FHIR resources - Azure Cosmos DB | Microsoft Docs
description: "Meer informatie over hoe tooset van meldingen voor HL7 FHIR gezondheidszorg patiëntrecords met Azure Logic Apps, Azure Cosmos DB en Service Bus wijzigen."
keywords: HL7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Melding patiënten van HL7 FHIR gezondheidszorg recordwijzigingen met Logic Apps en Azure Cosmos-DB

Azure MVP Howard Edidin is onlangs neemt contact met een organisatie in de gezondheidszorg die tooadd nieuwe functionaliteit tootheir patiënt portal wilden. Ze nodig toosend meldingen toopatients wanneer hun status record is bijgewerkt en deze patiënten toobe kunnen toosubscribe toothese updates nodig. 

In dit artikel wordt uitgelegd Hallo wijziging feed melding oplossing gemaakt voor deze organisatie in de gezondheidszorg met Azure Cosmos DB, Logic Apps en Service Bus. 

## <a name="project-requirements"></a>Projectvereisten
- Providers verzenden dat HL7 geconsolideerde klinische Document architectuur (C-CDA) en documenten in XML-indeling. C CDA documenten omvatten vrijwel elke soort klinische document, inclusief klinische documenten zoals familie geschiedenisgegevens en immunisatie records, alsmede als administratieve werkstroom en financiële documenten. 
- C CDA documenten te worden geconverteerd[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON-indeling.
- Gewijzigde FHIR resource documenten worden verzonden via e-mail in JSON-indeling.

## <a name="solution-workflow"></a>Werkstroom van de oplossing 

Hallo-project vereist op een hoog niveau Hallo werkstroomstappen te volgen: 
1. C CDA documenten tooFHIR resources worden geconverteerd.
2. Terugkerende trigger wordt gedelegeerd voor het gewijzigde FHIR bronnen uitvoeren. 
2. Een aangepaste app, FhirNotificationApi, tooconnect tooAzure Cosmos DB en query-aanroep voor nieuwe of gewijzigde documenten.
3. Hallo antwoord tootoohello Service Bus-wachtrij opslaan.
4. Poll op nieuwe berichten in Hallo Service Bus-wachtrij.
5. E-mailmeldingen toopatients verzenden.

## <a name="solution-architecture"></a>Oplossingsarchitectuur
Deze oplossing vereist drie Logic Apps toomeet Hallo bovenstaande vereisten en werkstroom voltooid Hallo-oplossing. Hallo drie logische apps zijn:
1. **Toewijzing van HL7 FHIR app**: Hallo HL7 C-CDA document ontvangt, toohello FHIR Resource getransformeerd en slaat deze tooAzure Cosmos-DB.
2. **EHR app**: bevraagt hello Azure Cosmos DB FHIR opslagplaats en Hallo antwoord tooa Service Bus-wachtrij wordt opgeslagen. Deze logica app gebruikmaakt van een [API-app](#api-app) tooretrieve nieuwe en gewijzigde documenten.
3. **Proces melding app**: een e-mailbericht met Hallo FHIR resource documenten in de hoofdtekst van het Hallo verzendt.

![Hallo drie Logic Apps gebruikt in deze oplossing HL7 FHIR gezondheidszorg](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Azure-services gebruikt voor Hallo-oplossing

#### <a name="azure-cosmos-db-documentdb-api"></a>Azure Cosmos DB DocumentDB API
Azure Cosmos-DB is Hallo opslagplaats voor Hallo FHIR resources, zoals wordt weergegeven in de volgende afbeelding Hallo.

![Hello Azure Cosmos DB account dat wordt gebruikt in deze gezondheidszorg HL7 FHIR-zelfstudie](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Logische Apps verwerken Hallo werkstroomproces. Hallo weergeven volgende schermafbeeldingen Hallo Logic apps die zijn gemaakt voor deze oplossing. 


1. **Toewijzing van HL7 FHIR app**: Hallo HL7 C-CDA document ontvangt en transformeren tooan FHIR resource met Enterprise Integration Pack Hallo voor Logic Apps. Hallo Enterprise Integration Pack Hallo toewijzing van Hallo C CDA tooFHIR resources verwerkt.

    ![Hallo logische App gebruikt tooreceive HL7 FHIR gezondheidszorg records](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **EHR app**: hello Azure Cosmos DB FHIR opslagplaats opvragen en sla Hallo antwoord tooa Service Bus-wachtrij. Hallo-code voor Hallo GetNewOrModifiedFHIRDocuments app is lager dan.

    ![Hallo logische App gebruikt tooquery Azure Cosmos-DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Proces melding app**: e-mailmelding met Hallo FHIR resource documenten in Hallo hoofdtekst verzenden.

    ![Hallo logische App die u patiënt e-mail met Hallo HL7 FHIR resource in de hoofdtekst van het Hallo verzendt](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Service Bus
Hallo afbeelding toont Hallo patiënten wachtrij te volgen. Hallo Tag-eigenschapswaarde wordt gebruikt voor het onderwerp e-mail Hallo.

![Hallo Service Bus-wachtrij in deze zelfstudie HL7 FHIR gebruikt](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>API-app
Een API-app verbindt tooAzure Cosmos DB en query's voor nieuwe of gewijzigde FHIR documenten per resourcetype. Deze app heeft één domeincontroller **FhirNotificationApi** met een één bewerking **GetNewOrModifiedFhirDocuments**, Zie [bron voor de API-app](#api-app-source).

We gebruiken Hallo [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasse vanuit hello Azure Cosmos DB DocumentDB .NET API. Zie voor meer informatie, Hallo [wijziging feed artikel](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>GetNewOrModifiedFhirDocuments bewerking

**Invoer**
- Database-id
- CollectionId
- De naam van de HL7 FHIR brontype
- Booleaanse waarde: Starten vanaf het begin
- Int: Het aantal geretourneerde documenten

**Uitvoer**
- Succes: Statuscode: 200, antwoord: overzicht van documenten (JSON-matrix)
- Mislukt: Statuscode: 404, antwoord: ' geen documenten gevonden voor '*resourcenaam '* brontype '

<a id="api-app-source"></a>

**Bron voor Hallo API-app**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>Hallo FhirNotificationApi testen 

Hallo volgende afbeelding laat zien hoe swagger gebruikte tootootest Hallo was [FhirNotificationApi](#api-app-source).

![Hallo Swagger-bestand gebruikt tootest Hallo API-app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Azure-portaldashboard

Hallo volgende afbeelding geeft alle hello Azure-services voor deze oplossing uitgevoerd in hello Azure-portal.

![Hello Azure-portal met alle Hallo-services die worden gebruikt in deze zelfstudie HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Samenvatting

- U hebt geleerd dat Azure Cosmos DB systeemeigen relatietype voor meldingen over nieuwe of gewijzigd documenten en hoe eenvoudig het is toouse heeft. 
- Dankzij het gebruik van Logic Apps, kunt u werkstromen maken zonder een code te schrijven.
- Het gebruik van Azure Service Bus-wachtrijen toohandle Hallo distributie voor Hallo HL7 FHIR documenten.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Cosmos DB Hallo [Azure DB die Cosmos-startpagina](https://azure.microsoft.com/services/cosmos-db/). Zie voor meer informatie over Logic Apps [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


