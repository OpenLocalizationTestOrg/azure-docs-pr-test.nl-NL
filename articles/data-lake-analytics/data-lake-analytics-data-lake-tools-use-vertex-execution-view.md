---
title: aaaUse hello Vertex Execution View in Data Lake Tools voor Visual Studio | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Vertex Execution View tooexam Data Lake Analytics-taken.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="9f773-103">Hallo Vertex Execution View in Data Lake Tools voor Visual Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f773-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="9f773-104">Meer informatie over hoe toouse Hallo Vertex Execution View tooexam Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="9f773-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f773-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9f773-105">Prerequisites</span></span>

<span data-ttu-id="9f773-106">Moet u basiskennis van het gebruik van Data Lake Tools voor Visual Studio toodevelop U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="9f773-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="9f773-107">Zie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9f773-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="9f773-108">Hallo Vertex Execution View openen</span><span class="sxs-lookup"><span data-stu-id="9f773-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="9f773-109">Open een U-SQL-taak in de Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9f773-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="9f773-110">Klik op **Vertex Execution View** in Hallo linkerbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="9f773-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="9f773-111">Hebt u mogelijk na vragen aan gebruiker tooload profielen eerst en het kan even duren, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="9f773-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="9f773-113">Vertex Execution View begrijpen</span><span class="sxs-lookup"><span data-stu-id="9f773-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="9f773-114">Hallo Vertex Execution View bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="9f773-114">hello Vertex Execution View has three parts:</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="9f773-116">Hallo **hoekpunt selector** op Hallo links kunt u hoekpunten selecteren door functies (zoals top 10 gegevens lezen, of kies fase).</span><span class="sxs-lookup"><span data-stu-id="9f773-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="9f773-117">Een van de meest gebruikte Hallo-filters toosee Hallo is **hoekpunten op kritieke pad**.</span><span class="sxs-lookup"><span data-stu-id="9f773-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="9f773-118">Hallo **kritieke pad** is Hallo langste keten van hoekpunten van een U-SQL-taak.</span><span class="sxs-lookup"><span data-stu-id="9f773-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="9f773-119">Understanding Hallo kritieke pad is nuttig voor het optimaliseren van uw taken door te controleren welke hoekpunt duurt Hallo langste.</span><span class="sxs-lookup"><span data-stu-id="9f773-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="9f773-121">Hallo bovenste middelste deelvenster ziet u Hallo **verwerkingsstatus van alle Hallo hoekpunten**.</span><span class="sxs-lookup"><span data-stu-id="9f773-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="9f773-123">Hallo onder het middelste deelvenster ziet u informatie over elk hoekpunt:</span><span class="sxs-lookup"><span data-stu-id="9f773-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="9f773-124">Procesnaam: naam van Hallo van Hallo hoekpunt exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9f773-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="9f773-125">Bestaat uit verschillende onderdelen in StageName | VertexName | VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="9f773-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="9f773-126">Hallo SV7_Split [62] .v1 hoekpunt staat bijvoorbeeld voor Hallo tweede exemplaar dat wordt uitgevoerd (.v1, index die begint bij 0) van hoekpunt getal 62 in fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="9f773-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="9f773-127">Totale gegevens lezen/schriftelijke: Hallo gegevens is gelezen of weggeschreven door dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="9f773-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="9f773-128">Status/afsluitstatus: Hallo eindstatus wanneer Hallo hoekpunt wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="9f773-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="9f773-129">Exit Code/mislukte Type: Hallo fout bij het Hallo hoekpunt is mislukt.</span><span class="sxs-lookup"><span data-stu-id="9f773-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="9f773-130">Het maken van reden: Waarom Hallo hoekpunt is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f773-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="9f773-131">Resource latentie/proces latentie/PN wachtrij latentie: Hallo gebruikte tijd voor Hallo hoekpunt toowait voor resources, tooprocess gegevens en toostay in Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="9f773-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="9f773-132">GUID van proces/Maker: GUID voor de huidige actieve hoekpunt Hallo of de maker.</span><span class="sxs-lookup"><span data-stu-id="9f773-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="9f773-133">Versie: Hallo N de instantie van Hallo hoekpunt uitgevoerd (Hallo-systeem kunt plannen nieuwe exemplaren van een hoekpunt voor een groot aantal redenen, bijvoorbeeld failover compute redundantie, enz.)</span><span class="sxs-lookup"><span data-stu-id="9f773-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="9f773-134">Versie wanneer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f773-134">Version Created Time.</span></span>
* <span data-ttu-id="9f773-135">Verwerken maken Start tijd/proces in de wachtrij geplaatst tijd/proces Start tijd/proces voltooid tijd: wanneer Hallo hoekpunt proces maken start; Wanneer Hallo hoekpunt proces wordt gestart tooqueue; Hallo wanneer bepaalde hoekpunt proces gestart; Wanneer hello bepaalde hoekpunt is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9f773-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f773-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f773-136">Next steps</span></span>
* <span data-ttu-id="9f773-137">toolog diagnostische informatie, Zie [toegang tot logboeken met diagnostische gegevens voor Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="9f773-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="9f773-138">Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="9f773-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="9f773-139">taakdetails tooview, Zie [gebruik taak Browser en weergave van de taak voor Azure Data lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="9f773-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
