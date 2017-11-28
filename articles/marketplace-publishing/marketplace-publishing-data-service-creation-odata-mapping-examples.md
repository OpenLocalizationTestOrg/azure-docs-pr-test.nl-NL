---
title: aaaGuide toocreating een gegevensservice voor Hallo Marketplace | Microsoft Docs
description: Gedetailleerde instructies waarmee toocreate, certificeren en implementeren van een Service voor gegevens aanschaffen op Hallo Azure Marketplace.
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="29488-103">Voorbeelden van het toewijzen van een bestaande web service tooOData via CSDLs</span><span class="sxs-lookup"><span data-stu-id="29488-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="29488-104">**Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.**</span><span class="sxs-lookup"><span data-stu-id="29488-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="29488-105">Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="29488-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="29488-106">Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="29488-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="29488-107">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met "POST"</span><span class="sxs-lookup"><span data-stu-id="29488-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="29488-108">Gebruik POST onbewerkte gegevens toocreate een nieuwe onderliggende en retourneren van de server URL(location) of tooupdate onderdeel van de onderliggende op Hallo server Hallo URL gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="29488-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="29488-109">Waarbij Hallo ondergeschikte is een stream, dat wil zeggen ongestructureerde ex.</span><span class="sxs-lookup"><span data-stu-id="29488-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="29488-110">een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="29488-110">a text file.</span></span>  <span data-ttu-id="29488-111">Houd er rekening mee POST in niet idempotent zonder een locatie.</span><span class="sxs-lookup"><span data-stu-id="29488-111">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="29488-112">Voorbeeld: FunctionImport met 'Verwijderen'</span><span class="sxs-lookup"><span data-stu-id="29488-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="29488-113">DELETE tooremove een opgegeven URI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29488-113">Use DELETE tooremove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="29488-114">Voorbeeld: FunctionImport met 'Posten'</span><span class="sxs-lookup"><span data-stu-id="29488-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="29488-115">Gebruik POST onbewerkte gegevens toocreate een nieuwe onderliggende en retourneren van de server URL(location) of tooupdate onderdeel van de onderliggende op Hallo server Hallo URL gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="29488-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="29488-116">Hallo ondergeschikte is waar een structuur.</span><span class="sxs-lookup"><span data-stu-id="29488-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="29488-117">Houd er rekening mee POST is niet de idempotent zonder een locatie.</span><span class="sxs-lookup"><span data-stu-id="29488-117">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="29488-118">Voorbeeld: FunctionImport met behulp van 'Geplaatst'</span><span class="sxs-lookup"><span data-stu-id="29488-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="29488-119">Gebruik PUT toocreate een nieuwe onderliggende of tooupdate Hallo gehele ondergeschikte op een server URL gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="29488-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="29488-120">Wanneer een structuur is Hallo onderliggend niveau, PUT idempotent is zodat meerdere exemplaren leidt ertoe dat Hallo dezelfde status, Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="29488-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="29488-121">x = 5.</span><span class="sxs-lookup"><span data-stu-id="29488-121">x=5.</span></span>  <span data-ttu-id="29488-122">Opslag moet worden gebruikt met de volledige inhoud van de opgegeven Hallo Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="29488-122">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="29488-123">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met 'Geplaatst'</span><span class="sxs-lookup"><span data-stu-id="29488-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="29488-124">Gebruik plaatsen onbewerkte gegevens toocreate een nieuwe onderliggende of tooupdate Hallo hele onderliggende URL van een server die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="29488-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="29488-125">Waarbij Hallo ondergeschikte is een stream, dat wil zeggen ongestructureerde ex.</span><span class="sxs-lookup"><span data-stu-id="29488-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="29488-126">een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="29488-126">a text file.</span></span>  <span data-ttu-id="29488-127">Idempotent PUT is meerdere keren plaatsvinden leidt ertoe dat Hallo dezelfde status, Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="29488-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="29488-128">x = 5.</span><span class="sxs-lookup"><span data-stu-id="29488-128">x=5.</span></span>  <span data-ttu-id="29488-129">Opslag moet worden gebruikt met de volledige inhoud van de opgegeven Hallo Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="29488-129">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="29488-130">Voorbeeld: FunctionImport voor 'Raw'-gegevens geretourneerd met 'Ophalen'</span><span class="sxs-lookup"><span data-stu-id="29488-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="29488-131">OPHALEN van onbewerkte gegevens tooreturn onderliggend niveau dat niet-gestructureerde, dat wil zeggen tekst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29488-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="29488-132">Voorbeeld: FunctionImport voor 'Paging"via geretourneerde gegevens</span><span class="sxs-lookup"><span data-stu-id="29488-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="29488-133">Implementeer RESTful paging via uw gegevens met GET gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29488-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="29488-134">Standaard paginering ingesteld too100 gegevensrij per pagina.</span><span class="sxs-lookup"><span data-stu-id="29488-134">Default paging is set too100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="29488-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="29488-135">See Also</span></span>
* <span data-ttu-id="29488-136">Als u geïnteresseerd bent in kennis Hallo algehele proces voor OData-toewijzing en het doel, Lees dit artikel [gegevens Service OData-toewijzing](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definities, structuren en instructies.</span><span class="sxs-lookup"><span data-stu-id="29488-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="29488-137">Als u geïnteresseerd in learning en de specifieke kennis Hallo-knooppunten en de bijbehorende parameters bent, Lees dit artikel [Service OData toewijzing gegevensknooppunten](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) voor definities en uitleg, voorbeelden en gebruik case-context.</span><span class="sxs-lookup"><span data-stu-id="29488-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="29488-138">tooreturn toohello pad voor het publiceren van een gegevensservice toohello Azure Marketplace Lees dit artikel voorgeschreven [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="29488-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

