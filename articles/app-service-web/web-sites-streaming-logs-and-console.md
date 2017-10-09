---
title: aaaStreaming logboeken en -console
description: Streaminglogboeken en overzicht van de console
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="9ef3d-103">Streaminglogboeken en Hallo Console</span><span class="sxs-lookup"><span data-stu-id="9ef3d-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="9ef3d-104">Streaminglogboeken</span><span class="sxs-lookup"><span data-stu-id="9ef3d-104">Streaming Logs</span></span>
<span data-ttu-id="9ef3d-105">Hallo **Azure-portal** biedt een geïntegreerde streaming logboekenviewer waarmee u kunt weergeven van traceringsgebeurtenissen van uw **App Service** apps in realtime.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="9ef3d-106">Deze functie in te stellen, is enkele eenvoudige stappen vereist:</span><span class="sxs-lookup"><span data-stu-id="9ef3d-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="9ef3d-107">Traceringen in uw code te schrijven</span><span class="sxs-lookup"><span data-stu-id="9ef3d-107">Write traces in your code</span></span>
* <span data-ttu-id="9ef3d-108">Toepassing inschakelen **diagnostische logboeken** voor uw app</span><span class="sxs-lookup"><span data-stu-id="9ef3d-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="9ef3d-109">Weergave Hallo stroom Hallo ingebouwde **Streaming logboeken** UI in Hallo **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="9ef3d-110">Hoe toowrite traceert in uw code</span><span class="sxs-lookup"><span data-stu-id="9ef3d-110">How toowrite traces in your code</span></span>
<span data-ttu-id="9ef3d-111">Schrijven van traceringen in uw code is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="9ef3d-112">In C# is het zo eenvoudig hello na de code te schrijven:</span><span class="sxs-lookup"><span data-stu-id="9ef3d-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="9ef3d-113">Hallo Trace klasse woont in Hallo System.Diagnostics naamruimte.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="9ef3d-114">U kunt deze code schrijven in een node.js-app tooachieve Hallo hetzelfde resultaat:</span><span class="sxs-lookup"><span data-stu-id="9ef3d-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="9ef3d-115">Hoe tooenable en bekijkt hello streaminglogboeken</span><span class="sxs-lookup"><span data-stu-id="9ef3d-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="9ef3d-116">![][BrowseSitesScreenshot]Diagnostische gegevens zijn ingeschakeld op basis van de per-app.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="9ef3d-117">Gestart door te bladeren toohello site u tooenable wilt dat deze functie op.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="9ef3d-118">![][DiagnosticsLogs]In het menu instellingen, schuif naar beneden toohello **bewaking** sectie en klik op **(1) diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="9ef3d-119">Vervolgens **(2) inschakelen** **toepassingslogboeken (bestandssysteem)** of **toepassingslogboeken (blob)** hello **niveau** optie kunt u Hallo wijzigen ernst van traceringen toocapture.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="9ef3d-120">Als u bekend bent met de functie Hallo tooget NET probeert, Hallo-niveau instellen te**uitgebreid** tooensure alle trace-instructies worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="9ef3d-121">Klik op **opslaan** Hallo boven aan het Hallo-blade en u bent klaar tooview Logboeken.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef3d-122">Hallo hoger Hallo **ernstniveau** Hallo meer bronnen worden verbruikt toolog en Hallo meer traceringen worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="9ef3d-123">Zorg ervoor dat **ernstniveau** geconfigureerde toohello juiste uitgebreidheid voor een productie- of intensief verkeer site is.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="9ef3d-124">![][StreamingLogsScreenshot]Hallo tooview **streaminglogboeken** binnen hello Azure-portal, klik op de op **(1) Logboekstream** ook in Hallo **bewaking** sectie van menu Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="9ef3d-125">Als uw app is actief trace-instructies schrijven, dan u ze in Hallo ziet moet **(2) streaming registreert UI** in bijna realtime.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="9ef3d-126">Console</span><span class="sxs-lookup"><span data-stu-id="9ef3d-126">Console</span></span>
<span data-ttu-id="9ef3d-127">Hallo **Azure-portal** tooyour-consoletoepassing toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="9ef3d-128">U kunt verkennen van uw app-bestandssysteem en powershell/cmd scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="9ef3d-129">U zijn gebonden aan Hallo dezelfde machtigingen ingesteld als uw app-code uitgevoerd bij het uitvoeren van consoleopdrachten.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="9ef3d-130">Toegang tot tooprotected mappen of actieve scripts waarvoor verhoogde machtigingen is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="9ef3d-131">![][ConsoleScreenshot]In het menu instellingen, schuif naar beneden te**ontwikkelingsprogramma's** sectie en klik op **(1) Console** en Hallo **(2) console** UI toohello rechts wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9ef3d-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="9ef3d-132">tooget bekend bent met de Hallo **console**, probeer basisopdrachten, zoals:</span><span class="sxs-lookup"><span data-stu-id="9ef3d-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
