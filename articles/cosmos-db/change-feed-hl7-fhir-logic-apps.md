---
title: Feed voor HL7 FHIR resources - Azure Cosmos DB wijzigen | Microsoft Docs
description: "Informatie over het instellen van HL7 FHIR gezondheidszorg patiëntrecords met Azure Logic Apps, Azure Cosmos DB en Service Bus-wijzigingsmeldingen."
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="d6045-104">Melding patiënten van HL7 FHIR gezondheidszorg recordwijzigingen met Logic Apps en Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="d6045-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="d6045-105">Azure MVP Howard Edidin is onlangs neemt contact met een organisatie in de gezondheidszorg die nieuwe functionaliteit toevoegen aan hun patiënt portal wilden.</span><span class="sxs-lookup"><span data-stu-id="d6045-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="d6045-106">Ze nodig zijn om meldingen te verzenden aan patiënten wanneer hun status record is bijgewerkt en deze patiënten kunnen abonneren op deze updates nodig.</span><span class="sxs-lookup"><span data-stu-id="d6045-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="d6045-107">Dit artikel helpt bij de wijziging oplossing notification gemaakt voor deze organisatie in de gezondheidszorg met Azure Cosmos DB, Logic Apps en Service Bus-feed.</span><span class="sxs-lookup"><span data-stu-id="d6045-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="d6045-108">Projectvereisten</span><span class="sxs-lookup"><span data-stu-id="d6045-108">Project requirements</span></span>
- <span data-ttu-id="d6045-109">Providers verzenden dat HL7 geconsolideerde klinische Document architectuur (C-CDA) en documenten in XML-indeling.</span><span class="sxs-lookup"><span data-stu-id="d6045-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="d6045-110">C CDA documenten omvatten vrijwel elke soort klinische document, inclusief klinische documenten zoals familie geschiedenisgegevens en immunisatie records, alsmede als administratieve werkstroom en financiële documenten.</span><span class="sxs-lookup"><span data-stu-id="d6045-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="d6045-111">C CDA documenten worden geconverteerd naar [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d6045-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="d6045-112">Gewijzigde FHIR resource documenten worden verzonden via e-mail in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d6045-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="d6045-113">Werkstroom van de oplossing</span><span class="sxs-lookup"><span data-stu-id="d6045-113">Solution workflow</span></span> 

<span data-ttu-id="d6045-114">Het project vereist op een hoog niveau de volgende werkstroomstappen:</span><span class="sxs-lookup"><span data-stu-id="d6045-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="d6045-115">C CDA documenten niet converteren naar FHIR resources.</span><span class="sxs-lookup"><span data-stu-id="d6045-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="d6045-116">Terugkerende trigger wordt gedelegeerd voor het gewijzigde FHIR bronnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d6045-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="d6045-117">Een aangepaste app FhirNotificationApi verbinding maken met Azure Cosmos DB en de query voor nieuwe of gewijzigde documenten aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d6045-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="d6045-118">Het antwoord aan de Service Bus-wachtrij opslaan.</span><span class="sxs-lookup"><span data-stu-id="d6045-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="d6045-119">Poll op nieuwe berichten in de Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6045-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="d6045-120">E-mailmeldingen verzenden naar patiënten.</span><span class="sxs-lookup"><span data-stu-id="d6045-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="d6045-121">Oplossingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="d6045-121">Solution architecture</span></span>
<span data-ttu-id="d6045-122">Deze oplossing vereist drie Logic Apps om te voldoen aan de bovenstaande vereisten en het voltooien van de werkstroom oplossing.</span><span class="sxs-lookup"><span data-stu-id="d6045-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="d6045-123">De drie logische apps zijn:</span><span class="sxs-lookup"><span data-stu-id="d6045-123">The three logic apps are:</span></span>
1. <span data-ttu-id="d6045-124">**Toewijzing van HL7 FHIR app**: het document HL7 C-CDA ontvangt, getransformeerd tot de Resource FHIR en opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6045-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="d6045-125">**EHR app**: bevraagt de opslagplaats Azure Cosmos DB FHIR en het antwoord op een Service Bus-wachtrij wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d6045-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="d6045-126">Deze logica app gebruikmaakt van een [API-app](#api-app) nieuwe en gewijzigde documenten kunnen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d6045-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="d6045-127">**Proces melding app**: verzendt een e-mailbericht met de resource FHIR documenten in de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="d6045-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![De drie logische Apps gebruikt in deze oplossing HL7 FHIR gezondheidszorg](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="d6045-129">Azure-services gebruikt voor de oplossing</span><span class="sxs-lookup"><span data-stu-id="d6045-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="d6045-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="d6045-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="d6045-131">Azure Cosmos-database is de opslagplaats voor de FHIR-bronnen zoals weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d6045-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![De Azure DB die Cosmos-account gebruikt in deze gezondheidszorg HL7 FHIR-zelfstudie](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="d6045-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d6045-133">Logic Apps</span></span>
<span data-ttu-id="d6045-134">Logische Apps verwerken het werkstroomproces.</span><span class="sxs-lookup"><span data-stu-id="d6045-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="d6045-135">De volgende schermafbeeldingen weergeven de Logic apps die zijn gemaakt voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="d6045-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="d6045-136">**Toewijzing van HL7 FHIR app**: het document HL7 C-CDA ontvangen en te transformeren en een FHIR-resource met de Enterprise-integratiepakket voor Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="d6045-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="d6045-137">De Enterprise Integration Pack verwerkt de toewijzing van de C-CDA FHIR bronnen.</span><span class="sxs-lookup"><span data-stu-id="d6045-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![De logische App gebruikt voor het ontvangen van HL7 FHIR gezondheidszorg records](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="d6045-139">**EHR app**: de opslagplaats Azure Cosmos DB FHIR vragen en in het antwoord op een Service Bus-wachtrij opslaan.</span><span class="sxs-lookup"><span data-stu-id="d6045-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="d6045-140">De code voor de app GetNewOrModifiedFHIRDocuments is lager dan.</span><span class="sxs-lookup"><span data-stu-id="d6045-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![De logische App gebruikt voor het zoeken van Azure DB die Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="d6045-142">**Proces melding app**: verzenden van een e-mailbericht met de resource FHIR documenten in de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="d6045-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![De logische App waarmee patiënt e-mailbericht met de resource HL7 FHIR worden verzonden in de hoofdtekst](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="d6045-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="d6045-144">Service Bus</span></span>
<span data-ttu-id="d6045-145">De volgende afbeelding toont de patiënt wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6045-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="d6045-146">De waarde van de Tag-eigenschap wordt gebruikt voor het onderwerp van e-mail.</span><span class="sxs-lookup"><span data-stu-id="d6045-146">The Tag property value is used for the email subject.</span></span>

![De Service Bus-wachtrij in deze zelfstudie HL7 FHIR gebruikt](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="d6045-148">API-app</span><span class="sxs-lookup"><span data-stu-id="d6045-148">API app</span></span>
<span data-ttu-id="d6045-149">Een API-app verbindt met Azure Cosmos DB en query's voor nieuwe of gewijzigde FHIR documenten per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="d6045-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="d6045-150">Deze app heeft één domeincontroller **FhirNotificationApi** met een één bewerking **GetNewOrModifiedFhirDocuments**, Zie [bron voor de API-app](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="d6045-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="d6045-151">We gebruiken de [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) klasse van de Azure Cosmos DB DocumentDB .NET API.</span><span class="sxs-lookup"><span data-stu-id="d6045-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="d6045-152">Zie voor meer informatie de [wijziging feed artikel](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="d6045-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="d6045-153">GetNewOrModifiedFhirDocuments bewerking</span><span class="sxs-lookup"><span data-stu-id="d6045-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="d6045-154">**Invoer**</span><span class="sxs-lookup"><span data-stu-id="d6045-154">**Inputs**</span></span>
- <span data-ttu-id="d6045-155">Database-id</span><span class="sxs-lookup"><span data-stu-id="d6045-155">DatabaseId</span></span>
- <span data-ttu-id="d6045-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="d6045-156">CollectionId</span></span>
- <span data-ttu-id="d6045-157">De naam van de HL7 FHIR brontype</span><span class="sxs-lookup"><span data-stu-id="d6045-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="d6045-158">Booleaanse waarde: Starten vanaf het begin</span><span class="sxs-lookup"><span data-stu-id="d6045-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="d6045-159">Int: Het aantal geretourneerde documenten</span><span class="sxs-lookup"><span data-stu-id="d6045-159">Int: Number of documents returned</span></span>

<span data-ttu-id="d6045-160">**Uitvoer**</span><span class="sxs-lookup"><span data-stu-id="d6045-160">**Outputs**</span></span>
- <span data-ttu-id="d6045-161">Succes: Statuscode: 200, antwoord: overzicht van documenten (JSON-matrix)</span><span class="sxs-lookup"><span data-stu-id="d6045-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="d6045-162">Mislukt: Statuscode: 404, antwoord: ' geen documenten gevonden voor '*resourcenaam '* brontype '</span><span class="sxs-lookup"><span data-stu-id="d6045-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="d6045-163">**Bron voor de API-app**</span><span class="sxs-lookup"><span data-stu-id="d6045-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="d6045-164">De FhirNotificationApi testen</span><span class="sxs-lookup"><span data-stu-id="d6045-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="d6045-165">De volgende afbeelding laat zien hoe swagger tot is gebruikt voor het testen van de [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="d6045-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![Het Swagger-bestand dat is gebruikt bij het testen van de API-app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="d6045-167">Azure-portaldashboard</span><span class="sxs-lookup"><span data-stu-id="d6045-167">Azure portal dashboard</span></span>

<span data-ttu-id="d6045-168">De volgende afbeelding toont alle Azure-services voor deze oplossing uitgevoerd in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d6045-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![De Azure-portal weer met alle services die worden gebruikt in deze zelfstudie HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="d6045-170">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d6045-170">Summary</span></span>

- <span data-ttu-id="d6045-171">U hebt geleerd dat Azure Cosmos DB heeft systeemeigen ondersteuning voor meldingen over nieuwe of gewijzigd documenten en hoe eenvoudig het is om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6045-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="d6045-172">Dankzij het gebruik van Logic Apps, kunt u werkstromen maken zonder een code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="d6045-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="d6045-173">Voor het verwerken van het distributiepunt voor de HL7 FHIR documenten met behulp van Azure Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="d6045-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6045-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6045-174">Next steps</span></span>
<span data-ttu-id="d6045-175">Zie voor meer informatie over Azure Cosmos DB, de [Azure DB die Cosmos-startpagina](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d6045-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="d6045-176">Zie voor meer informatie over Logic Apps [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="d6045-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


