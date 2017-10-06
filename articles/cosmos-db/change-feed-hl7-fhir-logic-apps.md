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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="df3fd-104">Melding patiënten van HL7 FHIR gezondheidszorg recordwijzigingen met Logic Apps en Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="df3fd-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="df3fd-105">Azure MVP Howard Edidin is onlangs neemt contact met een organisatie in de gezondheidszorg die tooadd nieuwe functionaliteit tootheir patiënt portal wilden.</span><span class="sxs-lookup"><span data-stu-id="df3fd-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="df3fd-106">Ze nodig toosend meldingen toopatients wanneer hun status record is bijgewerkt en deze patiënten toobe kunnen toosubscribe toothese updates nodig.</span><span class="sxs-lookup"><span data-stu-id="df3fd-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="df3fd-107">In dit artikel wordt uitgelegd Hallo wijziging feed melding oplossing gemaakt voor deze organisatie in de gezondheidszorg met Azure Cosmos DB, Logic Apps en Service Bus.</span><span class="sxs-lookup"><span data-stu-id="df3fd-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="df3fd-108">Projectvereisten</span><span class="sxs-lookup"><span data-stu-id="df3fd-108">Project requirements</span></span>
- <span data-ttu-id="df3fd-109">Providers verzenden dat HL7 geconsolideerde klinische Document architectuur (C-CDA) en documenten in XML-indeling.</span><span class="sxs-lookup"><span data-stu-id="df3fd-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="df3fd-110">C CDA documenten omvatten vrijwel elke soort klinische document, inclusief klinische documenten zoals familie geschiedenisgegevens en immunisatie records, alsmede als administratieve werkstroom en financiële documenten.</span><span class="sxs-lookup"><span data-stu-id="df3fd-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="df3fd-111">C CDA documenten te worden geconverteerd[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="df3fd-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="df3fd-112">Gewijzigde FHIR resource documenten worden verzonden via e-mail in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="df3fd-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="df3fd-113">Werkstroom van de oplossing</span><span class="sxs-lookup"><span data-stu-id="df3fd-113">Solution workflow</span></span> 

<span data-ttu-id="df3fd-114">Hallo-project vereist op een hoog niveau Hallo werkstroomstappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="df3fd-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="df3fd-115">C CDA documenten tooFHIR resources worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="df3fd-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="df3fd-116">Terugkerende trigger wordt gedelegeerd voor het gewijzigde FHIR bronnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="df3fd-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="df3fd-117">Een aangepaste app, FhirNotificationApi, tooconnect tooAzure Cosmos DB en query-aanroep voor nieuwe of gewijzigde documenten.</span><span class="sxs-lookup"><span data-stu-id="df3fd-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="df3fd-118">Hallo antwoord tootoohello Service Bus-wachtrij opslaan.</span><span class="sxs-lookup"><span data-stu-id="df3fd-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="df3fd-119">Poll op nieuwe berichten in Hallo Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="df3fd-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="df3fd-120">E-mailmeldingen toopatients verzenden.</span><span class="sxs-lookup"><span data-stu-id="df3fd-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="df3fd-121">Oplossingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="df3fd-121">Solution architecture</span></span>
<span data-ttu-id="df3fd-122">Deze oplossing vereist drie Logic Apps toomeet Hallo bovenstaande vereisten en werkstroom voltooid Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="df3fd-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="df3fd-123">Hallo drie logische apps zijn:</span><span class="sxs-lookup"><span data-stu-id="df3fd-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="df3fd-124">**Toewijzing van HL7 FHIR app**: Hallo HL7 C-CDA document ontvangt, toohello FHIR Resource getransformeerd en slaat deze tooAzure Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="df3fd-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="df3fd-125">**EHR app**: bevraagt hello Azure Cosmos DB FHIR opslagplaats en Hallo antwoord tooa Service Bus-wachtrij wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="df3fd-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="df3fd-126">Deze logica app gebruikmaakt van een [API-app](#api-app) tooretrieve nieuwe en gewijzigde documenten.</span><span class="sxs-lookup"><span data-stu-id="df3fd-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="df3fd-127">**Proces melding app**: een e-mailbericht met Hallo FHIR resource documenten in de hoofdtekst van het Hallo verzendt.</span><span class="sxs-lookup"><span data-stu-id="df3fd-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Hallo drie Logic Apps gebruikt in deze oplossing HL7 FHIR gezondheidszorg](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="df3fd-129">Azure-services gebruikt voor Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="df3fd-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="df3fd-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="df3fd-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="df3fd-131">Azure Cosmos-DB is Hallo opslagplaats voor Hallo FHIR resources, zoals wordt weergegeven in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="df3fd-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![Hello Azure Cosmos DB account dat wordt gebruikt in deze gezondheidszorg HL7 FHIR-zelfstudie](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="df3fd-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="df3fd-133">Logic Apps</span></span>
<span data-ttu-id="df3fd-134">Logische Apps verwerken Hallo werkstroomproces.</span><span class="sxs-lookup"><span data-stu-id="df3fd-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="df3fd-135">Hallo weergeven volgende schermafbeeldingen Hallo Logic apps die zijn gemaakt voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="df3fd-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="df3fd-136">**Toewijzing van HL7 FHIR app**: Hallo HL7 C-CDA document ontvangt en transformeren tooan FHIR resource met Enterprise Integration Pack Hallo voor Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="df3fd-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="df3fd-137">Hallo Enterprise Integration Pack Hallo toewijzing van Hallo C CDA tooFHIR resources verwerkt.</span><span class="sxs-lookup"><span data-stu-id="df3fd-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Hallo logische App gebruikt tooreceive HL7 FHIR gezondheidszorg records](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="df3fd-139">**EHR app**: hello Azure Cosmos DB FHIR opslagplaats opvragen en sla Hallo antwoord tooa Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="df3fd-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="df3fd-140">Hallo-code voor Hallo GetNewOrModifiedFHIRDocuments app is lager dan.</span><span class="sxs-lookup"><span data-stu-id="df3fd-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Hallo logische App gebruikt tooquery Azure Cosmos-DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="df3fd-142">**Proces melding app**: e-mailmelding met Hallo FHIR resource documenten in Hallo hoofdtekst verzenden.</span><span class="sxs-lookup"><span data-stu-id="df3fd-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Hallo logische App die u patiënt e-mail met Hallo HL7 FHIR resource in de hoofdtekst van het Hallo verzendt](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="df3fd-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="df3fd-144">Service Bus</span></span>
<span data-ttu-id="df3fd-145">Hallo afbeelding toont Hallo patiënten wachtrij te volgen.</span><span class="sxs-lookup"><span data-stu-id="df3fd-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="df3fd-146">Hallo Tag-eigenschapswaarde wordt gebruikt voor het onderwerp e-mail Hallo.</span><span class="sxs-lookup"><span data-stu-id="df3fd-146">hello Tag property value is used for hello email subject.</span></span>

![Hallo Service Bus-wachtrij in deze zelfstudie HL7 FHIR gebruikt](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="df3fd-148">API-app</span><span class="sxs-lookup"><span data-stu-id="df3fd-148">API app</span></span>
<span data-ttu-id="df3fd-149">Een API-app verbindt tooAzure Cosmos DB en query's voor nieuwe of gewijzigde FHIR documenten per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="df3fd-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="df3fd-150">Deze app heeft één domeincontroller **FhirNotificationApi** met een één bewerking **GetNewOrModifiedFhirDocuments**, Zie [bron voor de API-app](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="df3fd-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="df3fd-151">We gebruiken Hallo [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasse vanuit hello Azure Cosmos DB DocumentDB .NET API.</span><span class="sxs-lookup"><span data-stu-id="df3fd-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="df3fd-152">Zie voor meer informatie, Hallo [wijziging feed artikel](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="df3fd-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="df3fd-153">GetNewOrModifiedFhirDocuments bewerking</span><span class="sxs-lookup"><span data-stu-id="df3fd-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="df3fd-154">**Invoer**</span><span class="sxs-lookup"><span data-stu-id="df3fd-154">**Inputs**</span></span>
- <span data-ttu-id="df3fd-155">Database-id</span><span class="sxs-lookup"><span data-stu-id="df3fd-155">DatabaseId</span></span>
- <span data-ttu-id="df3fd-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="df3fd-156">CollectionId</span></span>
- <span data-ttu-id="df3fd-157">De naam van de HL7 FHIR brontype</span><span class="sxs-lookup"><span data-stu-id="df3fd-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="df3fd-158">Booleaanse waarde: Starten vanaf het begin</span><span class="sxs-lookup"><span data-stu-id="df3fd-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="df3fd-159">Int: Het aantal geretourneerde documenten</span><span class="sxs-lookup"><span data-stu-id="df3fd-159">Int: Number of documents returned</span></span>

<span data-ttu-id="df3fd-160">**Uitvoer**</span><span class="sxs-lookup"><span data-stu-id="df3fd-160">**Outputs**</span></span>
- <span data-ttu-id="df3fd-161">Succes: Statuscode: 200, antwoord: overzicht van documenten (JSON-matrix)</span><span class="sxs-lookup"><span data-stu-id="df3fd-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="df3fd-162">Mislukt: Statuscode: 404, antwoord: ' geen documenten gevonden voor '*resourcenaam '* brontype '</span><span class="sxs-lookup"><span data-stu-id="df3fd-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="df3fd-163">**Bron voor Hallo API-app**</span><span class="sxs-lookup"><span data-stu-id="df3fd-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="df3fd-164">Hallo FhirNotificationApi testen</span><span class="sxs-lookup"><span data-stu-id="df3fd-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="df3fd-165">Hallo volgende afbeelding laat zien hoe swagger gebruikte tootootest Hallo was [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="df3fd-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![Hallo Swagger-bestand gebruikt tootest Hallo API-app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="df3fd-167">Azure-portaldashboard</span><span class="sxs-lookup"><span data-stu-id="df3fd-167">Azure portal dashboard</span></span>

<span data-ttu-id="df3fd-168">Hallo volgende afbeelding geeft alle hello Azure-services voor deze oplossing uitgevoerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="df3fd-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Hello Azure-portal met alle Hallo-services die worden gebruikt in deze zelfstudie HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="df3fd-170">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="df3fd-170">Summary</span></span>

- <span data-ttu-id="df3fd-171">U hebt geleerd dat Azure Cosmos DB systeemeigen relatietype voor meldingen over nieuwe of gewijzigd documenten en hoe eenvoudig het is toouse heeft.</span><span class="sxs-lookup"><span data-stu-id="df3fd-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="df3fd-172">Dankzij het gebruik van Logic Apps, kunt u werkstromen maken zonder een code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="df3fd-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="df3fd-173">Het gebruik van Azure Service Bus-wachtrijen toohandle Hallo distributie voor Hallo HL7 FHIR documenten.</span><span class="sxs-lookup"><span data-stu-id="df3fd-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df3fd-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df3fd-174">Next steps</span></span>
<span data-ttu-id="df3fd-175">Zie voor meer informatie over Azure Cosmos DB Hallo [Azure DB die Cosmos-startpagina](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="df3fd-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="df3fd-176">Zie voor meer informatie over Logic Apps [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="df3fd-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


