---
title: Gebruik de Vertex Execution View in Data Lake Tools voor Visual Studio | Microsoft Docs
description: Informatie over het gebruik van de Vertex Execution View naar examen Data Lake Analytics-taken.
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
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="aa9d2-103">Gebruik de Vertex Execution View in Data Lake Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa9d2-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="aa9d2-104">Informatie over het gebruik van de Vertex Execution View naar examen Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa9d2-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa9d2-105">Prerequisites</span></span>

<span data-ttu-id="aa9d2-106">Moet u basiskennis van het gebruik van Data Lake Tools voor Visual Studio voor het ontwikkelen van U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="aa9d2-107">Zie [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aa9d2-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="aa9d2-108">Open de Vertex Execution View</span><span class="sxs-lookup"><span data-stu-id="aa9d2-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="aa9d2-109">Open een U-SQL-taak in de Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="aa9d2-110">Klik op **Vertex Execution View** in de linkerbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="aa9d2-111">U wordt mogelijk gevraagd eerst profielen laden en het kan even duren, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="aa9d2-113">Vertex Execution View begrijpen</span><span class="sxs-lookup"><span data-stu-id="aa9d2-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="aa9d2-114">De Vertex Execution View bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="aa9d2-114">The Vertex Execution View has three parts:</span></span>

![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="aa9d2-116">De **hoekpunt selector** op de links kunt u hoekpunten selecteren door functies (zoals top 10 gegevens lezen, of kies fase).</span><span class="sxs-lookup"><span data-stu-id="aa9d2-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="aa9d2-117">Een van de filters voor het meest gebruikt om te zien is de **hoekpunten op kritieke pad**.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="aa9d2-118">De **kritieke pad** is de langste keten van hoekpunten van een U-SQL-taak.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="aa9d2-119">Inzicht in het kritieke pad is nuttig voor het optimaliseren van uw taken door te controleren welke hoekpunt het langste tijd in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="aa9d2-121">In het deelvenster ziet u boven de **verwerkingsstatus van de hoekpunten**.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Data Lake Analytics Tools Vertex Execution View](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="aa9d2-123">Het deelvenster onderaan center bevat informatie over elk hoekpunt:</span><span class="sxs-lookup"><span data-stu-id="aa9d2-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="aa9d2-124">Procesnaam: De naam van het hoekpunt-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="aa9d2-125">Bestaat uit verschillende onderdelen in StageName | VertexName | VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="aa9d2-126">Het SV7_Split [62] .v1 hoekpunt staat bijvoorbeeld voor de tweede actieve instantie (.v1, index die begint bij 0) van hoekpunt getal 62 in fase SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="aa9d2-127">Totale gegevens lezen/schriftelijke: De gegevens zijn gelezen of weggeschreven door dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="aa9d2-128">Status/afsluitstatus: De laatste status wanneer het hoekpunt wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="aa9d2-129">Exit Code/mislukte Type: De fout bij het hoekpunt is mislukt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="aa9d2-130">Het maken van reden: Waarom het hoekpunt is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="aa9d2-131">Resource latentie/proces latentie/PN wachtrij latentie: de gebruikte tijd voor het hoekpunt moet worden gewacht voor bronnen om gegevens te verwerken en om te blijven in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="aa9d2-132">GUID van proces/Maker: GUID voor de persoon die of het huidige actieve hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="aa9d2-133">Versie: de N de instantie van het actieve hoekpunt (het systeem kunt plannen nieuwe exemplaren van een hoekpunt voor een groot aantal redenen, bijvoorbeeld failover compute redundantie, enz.)</span><span class="sxs-lookup"><span data-stu-id="aa9d2-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="aa9d2-134">Versie wanneer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-134">Version Created Time.</span></span>
* <span data-ttu-id="aa9d2-135">Verwerken maken Start tijd/proces in de wachtrij geplaatst tijd/proces Start tijd/proces voltooid tijd: wanneer het proces hoekpunt maken start; Wanneer het hoekpunt-proces wordt gestart in de wachtrij; Wanneer het bepaalde hoekpunt-proces wordt gestart; Wanneer het bepaalde hoekpunt is voltooid.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa9d2-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa9d2-136">Next steps</span></span>
* <span data-ttu-id="aa9d2-137">Zie [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md) (Diagnostische logboeken openen voor Azure Data Lake Analytics) voor logboekregistratie van diagnostische informatie.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="aa9d2-138">Zie [Websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md) voor een complexere query.</span><span class="sxs-lookup"><span data-stu-id="aa9d2-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="aa9d2-139">Taakdetails Zie [gebruik taak Browser en weergave van de taak voor Azure Data lake Analytics-taken](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="aa9d2-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
