---
title: 'Analytics platforms: Apache Storm vergelijking tooStream Analytics | Microsoft Docs'
description: Lees hoe u een cloudplatform analytics kiezen met behulp van een Apache Storm vergelijking tooStream Analytics. Verschillen in functies en begrijpen.
keywords: Analytics platform, analytics platforms, cloudplatform analytics, storm-vergelijking
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="23e50-105">Een streaming analytics platform kiezen: vergelijking van Apache Storm en Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="23e50-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="23e50-106">Azure biedt verschillende oplossingen voor het analyseren van streaminggegevens: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) en [Apache Storm op Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="23e50-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="23e50-107">Beide platforms analytics bieden Hallo voordelen van een PaaS-oplossing.</span><span class="sxs-lookup"><span data-stu-id="23e50-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="23e50-108">Maar Hallo platforms hebben enkele belangrijke verschillen in hun mogelijkheden ook als u in hoe u configureren en beheren.</span><span class="sxs-lookup"><span data-stu-id="23e50-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="23e50-109">Dit artikel bevat een side-by-side vergelijking van functies toohelp die u tussen Apache Storm en Azure Stream Analytics als een cloud analytics platform kiezen.</span><span class="sxs-lookup"><span data-stu-id="23e50-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="23e50-110">Algemene functies</span><span class="sxs-lookup"><span data-stu-id="23e50-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="23e50-113">
                    <strong>Apache Storm op HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-114">
                    <strong>Open-source?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-115">Nee.</span><span class="sxs-lookup"><span data-stu-id="23e50-115">No.</span></span> <span data-ttu-id="23e50-116">Azure Stream Analytics is een Microsoft-bedrijfseigen aanbieden.</span><span class="sxs-lookup"><span data-stu-id="23e50-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-117">Ja.</span><span class="sxs-lookup"><span data-stu-id="23e50-117">Yes.</span></span> <span data-ttu-id="23e50-118">Apache Storm is een technologie Apache in licentie gegeven.</span><span class="sxs-lookup"><span data-stu-id="23e50-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-119">
                    <strong>Ondersteuning van Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-120">Ja</span><span class="sxs-lookup"><span data-stu-id="23e50-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-121">Ja</span><span class="sxs-lookup"><span data-stu-id="23e50-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-122">
                    <strong>Hardwarevereisten</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-123">Geen.</span><span class="sxs-lookup"><span data-stu-id="23e50-123">None.</span></span> <span data-ttu-id="23e50-124">Azure Stream Analytics is een Azure-Service.</span><span class="sxs-lookup"><span data-stu-id="23e50-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-125">Geen.</span><span class="sxs-lookup"><span data-stu-id="23e50-125">None.</span></span> <span data-ttu-id="23e50-126">Apache Storm is een Azure-Service.</span><span class="sxs-lookup"><span data-stu-id="23e50-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-127">
                    <strong>Op het hoogste niveau eenheid</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-128">Gebruikers implementeren en controleren van de streaming-taken.</span><span class="sxs-lookup"><span data-stu-id="23e50-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-129">Gebruikers implementeren en controleren van een hele cluster, wat hosten kan meerdere Storm-taken, evenals andere werkbelastingen (inclusief batch).</span><span class="sxs-lookup"><span data-stu-id="23e50-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-130">
                    <strong>Prijzen</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-131">Prijs per volume van de gegevens die worden verwerkt en het aantal streaming-eenheden per uur wordt vereist die taak Hallo Hallo wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="23e50-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="23e50-132">Zie voor meer informatie <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics prijzen</a>.</span><span class="sxs-lookup"><span data-stu-id="23e50-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-133">Hallo-eenheid na aankoop op basis van het cluster is en u betaalt op Hallo tijd Hallo cluster wordt uitgevoerd, onafhankelijk van de taken die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="23e50-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="23e50-134">Zie voor meer informatie <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight prijzen</a>.</span><span class="sxs-lookup"><span data-stu-id="23e50-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="23e50-135">Ontwerpen</span><span class="sxs-lookup"><span data-stu-id="23e50-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="23e50-138">
                    <strong>Apache Storm op HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-139">
                    <strong>Mogelijkheden: SQL DSL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-140">Ja.</span><span class="sxs-lookup"><span data-stu-id="23e50-140">Yes.</span></span> <span data-ttu-id="23e50-141">Stream Analytics biedt een SQL-achtige taal voor het maken van transformaties.</span><span class="sxs-lookup"><span data-stu-id="23e50-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-142">Nee.</span><span class="sxs-lookup"><span data-stu-id="23e50-142">No.</span></span> <span data-ttu-id="23e50-143">Gebruikers schrijven van code in Java of C# of Trident-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23e50-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-144">
                    <strong>Mogelijkheden: Tijdelijke operators?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-145">Functies in vensters en tijdelijke joins, worden standaard ondersteund.</span><span class="sxs-lookup"><span data-stu-id="23e50-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-146">Tijdelijke operators moeten worden geïmplementeerd door Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="23e50-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-147">
                    <strong>Ontwikkeling biedt</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-148">Gebruikers kunnen maken, foutopsporing, taken en bewaken via hello Azure-portal met voorbeeldgegevens die zijn afgeleid van een live stream.</span><span class="sxs-lookup"><span data-stu-id="23e50-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-149">Gebruikers met .NET kunnen ontwikkelen, fouten opsporen en controleren met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23e50-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="23e50-150">Gebruikers met behulp van Java of andere talen kunnen Hallo IDE van hun keuze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23e50-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-151">
                    <strong>Ondersteuning voor foutopsporing</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-152">Algemene status en de bewerkingen taaklogboeken zijn beschikbaar toohelp foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="23e50-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="23e50-153">Stream Analytics momenteel kiest, kunnen gebruikers inhoud of hoeveel inhoud is opgenomen in het Hallo-Logboeken (dat wil zeggen, uitgebreide modus) opgeven.</span><span class="sxs-lookup"><span data-stu-id="23e50-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-154">Gedetailleerde logboeken zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="23e50-154">Detailed logs are available.</span></span> <span data-ttu-id="23e50-155">Gebruikers hebben toegang tot logboeken in Visual Studio of door logboekregistratie in toohello cluster en rechtstreekse toegang tot Hallo Logboeken.</span><span class="sxs-lookup"><span data-stu-id="23e50-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-156">
                    <strong>Uitbreidbaarheid met behulp van aangepaste code?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-157">Ondersteuning voor gedeeltelijk met JavaScript UDF's.</span><span class="sxs-lookup"><span data-stu-id="23e50-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="23e50-158">Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">integratie van JavaScript UDF</a>.</span><span class="sxs-lookup"><span data-stu-id="23e50-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-159">Ja.</span><span class="sxs-lookup"><span data-stu-id="23e50-159">Yes.</span></span> <span data-ttu-id="23e50-160">Gebruikers kunnen aangepaste code schrijven in C#, Java of een andere taal ondersteund op Storm.</span><span class="sxs-lookup"><span data-stu-id="23e50-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="23e50-161">Gegevensbronnen (invoer) en uitvoer</span><span class="sxs-lookup"><span data-stu-id="23e50-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="23e50-164">
                    <strong>Apache Storm op HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-165">
                 <strong>Invoer gegevensbronnen</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-166">Azure Event Hubs en Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="23e50-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-167">Connectors zijn beschikbaar voor Azure Event Hubs, Azure Service Bus en Kafka.</span><span class="sxs-lookup"><span data-stu-id="23e50-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="23e50-168">Gebruikers kunnen aanvullende connectors met aangepaste code maken.</span><span class="sxs-lookup"><span data-stu-id="23e50-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-169">
                    <strong>Invoergegevens indelingen</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-170">Avro JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="23e50-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-171">Gebruikers kunnen een willekeurige indeling met aangepaste code implementeren.</span><span class="sxs-lookup"><span data-stu-id="23e50-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-172">
                    <strong>Uitvoer</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-173">Een streaming-taak kan meerdere uitgangen hebben.</span><span class="sxs-lookup"><span data-stu-id="23e50-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="23e50-174">Ondersteunde uitgangen zijn Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB en Power BI.</span><span class="sxs-lookup"><span data-stu-id="23e50-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-175">Storm ondersteunt vele uitvoer in een topologie en elke uitvoer kan aangepaste regels voor de downstreamverwerking hebben.</span><span class="sxs-lookup"><span data-stu-id="23e50-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="23e50-176">Storm omvat connectors voor Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL en HBase.</span><span class="sxs-lookup"><span data-stu-id="23e50-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="23e50-177">Gebruikers kunnen aanvullende connectors met aangepaste code maken.</span><span class="sxs-lookup"><span data-stu-id="23e50-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-178">
                    <strong>Gegevenscodering indelingen</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-179">Gegevens moeten worden geformatteerd met UTF-8.</span><span class="sxs-lookup"><span data-stu-id="23e50-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-180">Gebruikers kunnen gegevens de coderingsindeling met aangepaste code implementeren.</span><span class="sxs-lookup"><span data-stu-id="23e50-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="23e50-181">Beheer van en bewerkingen</span><span class="sxs-lookup"><span data-stu-id="23e50-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="23e50-184">
                    <strong>Apache Storm op HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-185">
                    <strong>Taak implementatiemodel</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-186">Azure-portal, PowerShell en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="23e50-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-187">Azure-portal, PowerShell, Visual Studio en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="23e50-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-188">
                    <strong>Monitoring (statistieken, prestatiemeteritems, enz.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-189">Bewaking is geïmplementeerd met behulp van Azure-portal en de REST-API's.</span><span class="sxs-lookup"><span data-stu-id="23e50-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="23e50-190">Gebruikers kunnen ook configureren voor waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="23e50-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-191">Bewaking is geïmplementeerd met behulp van Hallo Storm-gebruikersinterface en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="23e50-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-192">
                    <strong>Schaalbaarheid</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-193">Schaalbaarheid wordt bepaald door Hallo aantal Streaming Units (SUs) voor elke taak.</span><span class="sxs-lookup"><span data-stu-id="23e50-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="23e50-194">Elke Streaming-eenheid van de processen van too1 MB per seconde, met een maximum 50 eenheden.</span><span class="sxs-lookup"><span data-stu-id="23e50-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="23e50-195">Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease doorvoer</a>.</span><span class="sxs-lookup"><span data-stu-id="23e50-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-196">Schaalbaarheid wordt bepaald door het aantal knooppunten in HDInsight Storm-cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="23e50-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="23e50-197">Hallo bovenste limiet voor het aantal knooppunten hello wordt gedefinieerd door Azure quotum Hallo van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="23e50-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-198">
                    <strong>Limieten voor gegevensverwerking</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-199">Gebruikers kunnen verhogen gegevensverwerking of kosten optimaliseren door het vergroten of verkleinen van Hallo aantal Streaming-eenheden met een bovengrens van 1 GB per seconde.</span><span class="sxs-lookup"><span data-stu-id="23e50-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-200">Gebruikers kunnen clustergrootte omhoog of omlaag schalen.</span><span class="sxs-lookup"><span data-stu-id="23e50-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-201">
                    <strong>Stop/hervatten</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-202">Stoppen en hervatten van de laatste plaats gestopt.</span><span class="sxs-lookup"><span data-stu-id="23e50-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-203">Stoppen en hervatten van laatste gestopt plaats op basis van een watermerk.</span><span class="sxs-lookup"><span data-stu-id="23e50-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-204">
                    <strong>Update-service en framework</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-205">Automatisch patchen zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="23e50-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-206">Automatisch patchen zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="23e50-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-207">
                    <strong>Zakelijke continuïteit via een maximaal beschikbare Service met de gegarandeerde Sla 's</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="23e50-208">SLA van 99,9% beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="23e50-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="23e50-209">Automatisch herstel van fouten</span><span class="sxs-lookup"><span data-stu-id="23e50-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="23e50-210">Ingebouwde herstel van stateful tijdelijke operators</span><span class="sxs-lookup"><span data-stu-id="23e50-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-211">SLA van 99,9% beschikbaarheid van Hallo Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="23e50-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="23e50-212">Apache Storm is een fouttolerante streaming platform.</span><span class="sxs-lookup"><span data-stu-id="23e50-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="23e50-213">Het is echter van Hallo gebruiker verantwoordelijkheid tooensure dat streaming uitvoeren ononderbroken taken.</span><span class="sxs-lookup"><span data-stu-id="23e50-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="23e50-214">Geavanceerde functies</span><span class="sxs-lookup"><span data-stu-id="23e50-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="23e50-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="23e50-217">
                    <strong>Apache Storm op HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-218">
                    <strong>Laat aankomst en out-van-order gebeurtenisverwerking</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-219">Ingebouwde configureerbaar beleid kunnen opnieuw rangschikken van gebeurtenissen, verwijdert u gebeurtenissen of gebeurtenistijd aanpassen.</span><span class="sxs-lookup"><span data-stu-id="23e50-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-220">Gebruikers moeten logica toohandle dit scenario implementeren.</span><span class="sxs-lookup"><span data-stu-id="23e50-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-221">
                    <strong>Referentiegegevens</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-222">Referentiegegevens is beschikbaar via Azure Blob-opslag met een maximum van 100 MB van de cache in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="23e50-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="23e50-223">Referentiegegevens wordt door Hallo-service vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="23e50-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-224">Er zijn geen limieten op de omvang van gegevens.</span><span class="sxs-lookup"><span data-stu-id="23e50-224">No limits on data size.</span></span> <span data-ttu-id="23e50-225">Connectors zijn beschikbaar voor HBase, Azure Cosmos DB, SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="23e50-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="23e50-226">Gebruikers kunnen aanvullende connectors met aangepaste code maken.</span><span class="sxs-lookup"><span data-stu-id="23e50-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="23e50-227">Referentiegegevens moeten worden vernieuwd met aangepaste code.</span><span class="sxs-lookup"><span data-stu-id="23e50-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="23e50-228">
                    <strong>Integratie met Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="23e50-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="23e50-229">Azure Machine Learning-modellen als functies kunnen worden geconfigureerd tijdens het maken van de taak wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="23e50-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="23e50-230">Zie voor meer informatie <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">schaal voor Machine Learning-functies</a>.</span><span class="sxs-lookup"><span data-stu-id="23e50-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="23e50-231">Beschikbaar via Storm Bolts.</span><span class="sxs-lookup"><span data-stu-id="23e50-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
