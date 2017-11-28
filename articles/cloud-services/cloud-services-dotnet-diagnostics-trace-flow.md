---
title: De stroom in een Cloud Services-toepassing met Azure Diagnostics traceren | Microsoft Docs
description: Tracering berichten toevoegen aan een Azure-toepassing om u te helpen bij foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="aaeb2-103">De stroom van een Cloud Services-toepassing met Azure Diagnostics traceren</span><span class="sxs-lookup"><span data-stu-id="aaeb2-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="aaeb2-104">Tracering is een manier om de uitvoering van uw toepassing bewaken terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="aaeb2-105">U kunt de [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), en [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) klassen voor informatie over de fouten en uitvoeren van toepassingen in Logboeken, tekstbestanden of andere apparaten voor latere analyse vastleggen.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="aaeb2-106">Zie voor meer informatie over tracering [tracering en toepassingen Instrumenteren](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="aaeb2-107">Trace-instructies en tracering switches gebruiken</span><span class="sxs-lookup"><span data-stu-id="aaeb2-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="aaeb2-108">De tracering implementeren in uw Cloud Services-toepassing door toe te voegen de [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) voor configuratie van de toepassing en het aanroepen van System.Diagnostics.Trace of System.Diagnostics.Debug aanbrengen in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="aaeb2-109">Gebruik het configuratiebestand *app.config* voor werkrollen en de *web.config* voor web-rollen.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="aaeb2-110">Wanneer u een nieuwe gehoste service met behulp van Visual Studio-sjabloon maakt, Azure Diagnostics wordt automatisch toegevoegd aan het project en de DiagnosticMonitorTraceListener wordt toegevoegd aan het juiste configuratiebestand voor de functies die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="aaeb2-111">Zie voor informatie over het plaatsen van trace-instructies, [hoe: Trace-instructies toevoegen voor toepassingscode](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="aaeb2-112">Door het plaatsen van [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in uw code kunt u bepalen of de tracering plaatsvindt en hoe uitgebreide is.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="aaeb2-113">Hiermee kunt u de status bewaken van uw toepassing in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="aaeb2-114">Dit is vooral belangrijk in een zakelijke toepassing die gebruikmaakt van meerdere onderdelen op meerdere computers.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="aaeb2-115">Zie voor meer informatie [hoe: Trace-Switches configureren](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="aaeb2-116">Configureren van de traceringslistener in een Azure-toepassing</span><span class="sxs-lookup"><span data-stu-id="aaeb2-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="aaeb2-117">Trace, foutopsporing en TraceSource, moet u instellen 'listeners' voor het verzamelen en registreren van de berichten die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="aaeb2-118">Listeners verzamelen, opslaan en routeren van berichten voor tracering.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="aaeb2-119">Ze rechtstreeks de traceringsuitvoer naar een geschikte doel, zoals een logboek, venster of tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="aaeb2-120">Maakt gebruik van Azure Diagnostics de [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="aaeb2-121">Voordat u de volgende procedure hebt voltooid, moet u de Azure diagnostische monitor initialiseren.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="aaeb2-122">Om dit te doen, Zie [diagnostische gegevens inschakelen in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="aaeb2-123">Houd er rekening mee dat als u de sjablonen die worden geleverd door Visual Studio gebruikt, de configuratie van de listener is toegevoegd automatisch voor u.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="aaeb2-124">Een traceringslistener toevoegen</span><span class="sxs-lookup"><span data-stu-id="aaeb2-124">Add a trace listener</span></span>
1. <span data-ttu-id="aaeb2-125">Open het bestand web.config of app.config voor uw rol.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="aaeb2-126">Voeg de volgende code naar het bestand.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-126">Add the following code to the file.</span></span> <span data-ttu-id="aaeb2-127">Wijzig het kenmerk versie voor het gebruik van het versienummer van de assembly waarnaar u verwijst.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="aaeb2-128">De assembly-versie wijzigen niet per se met elke versie van de Azure SDK tenzij er updates beschikbaar voor deze zijn.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="aaeb2-129">Zorg ervoor dat u hebt een projectverwijzing naar de assembly Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="aaeb2-130">Het versienummer in de bovenstaande xml zodat deze overeenkomen met de versie van de assembly waarnaar wordt verwezen Microsoft.WindowsAzure.Diagnostics bijwerken.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="aaeb2-131">Sla het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-131">Save the config file.</span></span>

<span data-ttu-id="aaeb2-132">Zie voor meer informatie over listeners [traceer-Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="aaeb2-133">Nadat u de stappen voor het toevoegen van de listener hebt voltooid, kunt u de trace-instructies toe aan uw code kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="aaeb2-134">Trace-instructie toevoegen aan uw code</span><span class="sxs-lookup"><span data-stu-id="aaeb2-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="aaeb2-135">Open een bronbestand voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-135">Open a source file for your application.</span></span> <span data-ttu-id="aaeb2-136">Bijvoorbeeld, de <RoleName>.cs-bestand voor de werkrol of Webrol.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="aaeb2-137">Voeg de volgende gebruiksinstructie als al niet is toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="aaeb2-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="aaeb2-138">Trace-instructies waarbij u wilt vastleggen van informatie over de status van uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="aaeb2-139">Een aantal methoden kunt u de uitvoer van de Trace-instructie opmaken.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="aaeb2-140">Zie voor meer informatie [hoe: Trace-instructies toevoegen voor toepassingscode](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaeb2-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="aaeb2-141">Sla het bronbestand.</span><span class="sxs-lookup"><span data-stu-id="aaeb2-141">Save the source file.</span></span>

