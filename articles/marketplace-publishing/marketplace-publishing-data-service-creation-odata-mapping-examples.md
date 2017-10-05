---
title: Handleiding voor het maken van een Service van gegevens voor de Marketplace | Microsoft Docs
description: Gedetailleerde instructies voor het maken, certificeren en implementeren van een Service voor gegevens aanschaffen op Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="77711-103">Voorbeelden voor het toewijzen van een bestaande webservice aan OData via CSDLs</span><span class="sxs-lookup"><span data-stu-id="77711-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="77711-104">**Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.**</span><span class="sxs-lookup"><span data-stu-id="77711-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="77711-105">Als u een SaaS business-toepassing die u wilt publiceren op AppSource hebt u meer informatie vindt [hier](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="77711-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="77711-106">Als u beschikt over een IaaS-toepassingen of developer-service die u wilt publiceren op Azure Marketplace u meer informatie vindt [hier](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="77711-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="77711-107">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met "POST"</span><span class="sxs-lookup"><span data-stu-id="77711-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="77711-108">Gebruik POST onbewerkte gegevens voor het maken van een nieuwe onderliggende en retourneren van de server URL(location) of gedefinieerd URL voor het bijwerken van onderdeel van de onderliggende op de server.</span><span class="sxs-lookup"><span data-stu-id="77711-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="77711-109">Waar is de onderliggende een stream, dat wil zeggen</span><span class="sxs-lookup"><span data-stu-id="77711-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="77711-110">niet-gestructureerde, ex.</span><span class="sxs-lookup"><span data-stu-id="77711-110">unstructured, ex.</span></span> <span data-ttu-id="77711-111">een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="77711-111">a text file.</span></span>  <span data-ttu-id="77711-112">Houd er rekening mee POST in niet idempotent zonder een locatie.</span><span class="sxs-lookup"><span data-stu-id="77711-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="77711-113">Voorbeeld: FunctionImport met 'Verwijderen'</span><span class="sxs-lookup"><span data-stu-id="77711-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="77711-114">Gebruik verwijderen om te verwijderen van een opgegeven URI.</span><span class="sxs-lookup"><span data-stu-id="77711-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="77711-115">Voorbeeld: FunctionImport met 'Posten'</span><span class="sxs-lookup"><span data-stu-id="77711-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="77711-116">Gebruik POST onbewerkte gegevens voor het maken van een nieuwe onderliggende en retourneren van de server URL(location) of gedefinieerd URL voor het bijwerken van onderdeel van de onderliggende op de server.</span><span class="sxs-lookup"><span data-stu-id="77711-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="77711-117">De onderliggende is waar een structuur.</span><span class="sxs-lookup"><span data-stu-id="77711-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="77711-118">Houd er rekening mee POST is niet de idempotent zonder een locatie.</span><span class="sxs-lookup"><span data-stu-id="77711-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="77711-119">Voorbeeld: FunctionImport met behulp van 'Geplaatst'</span><span class="sxs-lookup"><span data-stu-id="77711-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="77711-120">OPSLAG gebruiken voor het maken van een nieuwe onderliggende of gedefinieerd voor het bijwerken van de hele ondergeschikte op een server URL.</span><span class="sxs-lookup"><span data-stu-id="77711-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="77711-121">Wanneer de onderliggende een structuur is, PUT idempotent is zodat meerdere exemplaren in dezelfde staat resulteert, Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="77711-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="77711-122">x = 5.</span><span class="sxs-lookup"><span data-stu-id="77711-122">x=5.</span></span>  <span data-ttu-id="77711-123">Opslag moet worden gebruikt met de volledige inhoud van de opgegeven resource.</span><span class="sxs-lookup"><span data-stu-id="77711-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="77711-124">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met 'Geplaatst'</span><span class="sxs-lookup"><span data-stu-id="77711-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="77711-125">Gebruik plaatsen onbewerkte gegevens voor het maken van een nieuwe onderliggende of bijwerken van de hele onderliggend niveau in de URL van een server is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="77711-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="77711-126">Waar is de onderliggende een stream, dat wil zeggen</span><span class="sxs-lookup"><span data-stu-id="77711-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="77711-127">niet-gestructureerde, ex.</span><span class="sxs-lookup"><span data-stu-id="77711-127">unstructured, ex.</span></span> <span data-ttu-id="77711-128">een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="77711-128">a text file.</span></span>  <span data-ttu-id="77711-129">Idempotent PUT is meerdere keren plaatsvinden resulteert in dezelfde staat, Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="77711-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="77711-130">x = 5.</span><span class="sxs-lookup"><span data-stu-id="77711-130">x=5.</span></span>  <span data-ttu-id="77711-131">Opslag moet worden gebruikt met de volledige inhoud van de opgegeven resource.</span><span class="sxs-lookup"><span data-stu-id="77711-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="77711-132">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met 'Ophalen'</span><span class="sxs-lookup"><span data-stu-id="77711-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="77711-133">OPHALEN van onbewerkte gegevens om te retourneren van een onderliggend niveau dat niet-gestructureerde, dat wil zeggen tekst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77711-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="77711-134">Voorbeeld: FunctionImport voor 'Paging"via geretourneerde gegevens</span><span class="sxs-lookup"><span data-stu-id="77711-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="77711-135">Implementeer RESTful paging via uw gegevens met GET gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77711-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="77711-136">Standaard paginering is ingesteld op 100 gegevensrij per pagina.</span><span class="sxs-lookup"><span data-stu-id="77711-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="77711-137">Zie ook</span><span class="sxs-lookup"><span data-stu-id="77711-137">See Also</span></span>
* <span data-ttu-id="77711-138">Als u geïnteresseerd bent in het algehele proces voor OData-toewijzing en het doel te begrijpen, Lees dit artikel [gegevens Service OData-toewijzing](marketplace-publishing-data-service-creation-odata-mapping.md) bekijken definities, structuren en instructies.</span><span class="sxs-lookup"><span data-stu-id="77711-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="77711-139">Als u geïnteresseerd bent in het leren van en inzicht in de specifieke knooppunten en de bijbehorende parameters, Lees dit artikel [Service OData toewijzing gegevensknooppunten](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) voor definities en uitleg, voorbeelden en gebruik case-context.</span><span class="sxs-lookup"><span data-stu-id="77711-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="77711-140">Lees dit artikel om terug te keren naar de voorgeschreven pad voor het publiceren van een Service van gegevens naar Azure Marketplace, [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="77711-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

