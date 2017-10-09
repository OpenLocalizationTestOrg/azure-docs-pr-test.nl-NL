---
title: aaaTrace hello stroom in een Cloud Services-toepassing met Azure Diagnostics | Microsoft Docs
description: Tracering berichten tooan Azure-toepassing toohelp foutopsporing, meten van de prestaties, bewaking, analyse van het netwerkverkeer en meer toevoegen.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="6d93a-103">Hallo-stroom van een Cloud Services-toepassing met Azure Diagnostics traceren</span><span class="sxs-lookup"><span data-stu-id="6d93a-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="6d93a-104">Tracering is een manier voor u toomonitor Hallo uitvoering van uw toepassing, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d93a-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="6d93a-105">U kunt Hallo [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), en [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord informatie over fouten klassen en de uitvoering van de toepassing in Logboeken, tekstbestanden of andere apparaten voor latere analyse.</span><span class="sxs-lookup"><span data-stu-id="6d93a-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="6d93a-106">Zie voor meer informatie over tracering [tracering en toepassingen Instrumenteren](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d93a-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="6d93a-107">Trace-instructies en tracering switches gebruiken</span><span class="sxs-lookup"><span data-stu-id="6d93a-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="6d93a-108">De tracering implementeren in uw Cloud Services-toepassing door toe te voegen Hallo [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello Toepassingsconfiguratie en aanbrengen aanroepen tooSystem.Diagnostics.Trace of System.Diagnostics.Debug in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="6d93a-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="6d93a-109">Gebruik Hallo-configuratiebestand *app.config* voor werkrollen en Hallo *web.config* voor web-rollen.</span><span class="sxs-lookup"><span data-stu-id="6d93a-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="6d93a-110">Wanneer u een nieuwe gehoste service met behulp van Visual Studio-sjabloon maakt, Azure Diagnostics wordt automatisch toohello project toegevoegd en Hallo DiagnosticMonitorTraceListener toegevoegd toohello juiste configuratiebestand voor Hallo-functies die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="6d93a-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="6d93a-111">Zie voor informatie over het plaatsen van trace-instructies, [hoe: Trace-instructies toevoegen tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d93a-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="6d93a-112">Door het plaatsen van [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in uw code kunt u bepalen of de tracering plaatsvindt en hoe uitgebreide is.</span><span class="sxs-lookup"><span data-stu-id="6d93a-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="6d93a-113">Hiermee kunt u Hallo status bewaken van uw toepassing in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d93a-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="6d93a-114">Dit is vooral belangrijk in een zakelijke toepassing die gebruikmaakt van meerdere onderdelen op meerdere computers.</span><span class="sxs-lookup"><span data-stu-id="6d93a-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="6d93a-115">Zie voor meer informatie [hoe: Trace-Switches configureren](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d93a-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="6d93a-116">Hallo traceringslistener configureren in een Azure-toepassing</span><span class="sxs-lookup"><span data-stu-id="6d93a-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="6d93a-117">Trace, foutopsporing en TraceSource, moet u instellen 'listeners' toocollect en record Hallo-berichten die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="6d93a-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="6d93a-118">Listeners verzamelen, opslaan en routeren van berichten voor tracering.</span><span class="sxs-lookup"><span data-stu-id="6d93a-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="6d93a-119">Ze rechtstreeks Hallo tracering uitvoer tooan juiste doel, zoals een logboek, venster of tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="6d93a-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="6d93a-120">Hallo maakt gebruik van Azure Diagnostics [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="6d93a-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="6d93a-121">Voordat u Hallo na procedure voltooien, moet u hello Azure diagnostische monitor initialiseren.</span><span class="sxs-lookup"><span data-stu-id="6d93a-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="6d93a-122">toodo deze, Zie [diagnostische gegevens inschakelen in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6d93a-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="6d93a-123">Houd er rekening mee dat als u Hallo-sjablonen die worden geleverd door Visual Studio, Hallo configuratie van Hallo-listener is toegevoegd automatisch voor u.</span><span class="sxs-lookup"><span data-stu-id="6d93a-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="6d93a-124">Een traceringslistener toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d93a-124">Add a trace listener</span></span>
1. <span data-ttu-id="6d93a-125">Open Hallo web.config of app.config-bestand voor uw rol.</span><span class="sxs-lookup"><span data-stu-id="6d93a-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="6d93a-126">Hallo na toohello codebestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d93a-126">Add hello following code toohello file.</span></span> <span data-ttu-id="6d93a-127">Hallo kenmerk toouse Hallo versienummer van Hallo assembly waarnaar u verwijst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d93a-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="6d93a-128">Hallo-assembly-versie wijzigen niet per se met elke versie van de Azure SDK tenzij er updates tooit.</span><span class="sxs-lookup"><span data-stu-id="6d93a-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="6d93a-129">Zorg ervoor dat u hebt een project verwijzing toohello Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="6d93a-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="6d93a-130">Update Hallo-versienummer in XML-Hallo hierboven toomatch Hallo versie Hallo verwezen Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="6d93a-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="6d93a-131">Hallo-configuratiebestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="6d93a-131">Save hello config file.</span></span>

<span data-ttu-id="6d93a-132">Zie voor meer informatie over listeners [traceer-Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d93a-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="6d93a-133">Nadat u Hallo stappen tooadd Hallo listener hebt voltooid, kunt u de trace-instructies tooyour code kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d93a-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="6d93a-134">tooadd trace-instructie tooyour code</span><span class="sxs-lookup"><span data-stu-id="6d93a-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="6d93a-135">Open een bronbestand voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d93a-135">Open a source file for your application.</span></span> <span data-ttu-id="6d93a-136">Bijvoorbeeld, Hallo <RoleName>.cs-bestand voor de werkrol Hallo of Webrol.</span><span class="sxs-lookup"><span data-stu-id="6d93a-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="6d93a-137">Voeg de volgende Hallo gebruiksinstructie als al niet is toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="6d93a-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="6d93a-138">Trace-instructies waar u toocapture informatie over de status van uw toepassing hello wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d93a-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="6d93a-139">U kunt verschillende methoden tooformat Hallo uitvoer Hallo Trace-instructie.</span><span class="sxs-lookup"><span data-stu-id="6d93a-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="6d93a-140">Zie voor meer informatie [hoe: Trace-instructies toevoegen tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d93a-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="6d93a-141">Hallo-bronbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="6d93a-141">Save hello source file.</span></span>

