---
title: Streaminglogboeken en -console
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="26c0b-103">Streaminglogboeken en de Console</span><span class="sxs-lookup"><span data-stu-id="26c0b-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="26c0b-104">Streaminglogboeken</span><span class="sxs-lookup"><span data-stu-id="26c0b-104">Streaming Logs</span></span>
<span data-ttu-id="26c0b-105">De **Azure-portal** biedt een geïntegreerde streaming logboekenviewer waarmee u kunt weergeven van traceringsgebeurtenissen van uw **App Service** apps in realtime.</span><span class="sxs-lookup"><span data-stu-id="26c0b-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="26c0b-106">Deze functie in te stellen, is enkele eenvoudige stappen vereist:</span><span class="sxs-lookup"><span data-stu-id="26c0b-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="26c0b-107">Traceringen in uw code te schrijven</span><span class="sxs-lookup"><span data-stu-id="26c0b-107">Write traces in your code</span></span>
* <span data-ttu-id="26c0b-108">Toepassing inschakelen **diagnostische logboeken** voor uw app</span><span class="sxs-lookup"><span data-stu-id="26c0b-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="26c0b-109">Weergeven van de stroom van de ingebouwde **Streaming logboeken** gebruikersinterface in de **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="26c0b-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="26c0b-110">Het schrijven van traceringen in uw code</span><span class="sxs-lookup"><span data-stu-id="26c0b-110">How to write traces in your code</span></span>
<span data-ttu-id="26c0b-111">Schrijven van traceringen in uw code is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="26c0b-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="26c0b-112">In C# is het zo eenvoudig als het schrijven van de volgende code:</span><span class="sxs-lookup"><span data-stu-id="26c0b-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="26c0b-113">De klasse Trace woont in de naamruimte System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="26c0b-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="26c0b-114">U kunt deze code om te zorgen voor hetzelfde resultaat schrijven in een node.js-app:</span><span class="sxs-lookup"><span data-stu-id="26c0b-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="26c0b-115">Het inschakelen en weergeven van de streaming-Logboeken</span><span class="sxs-lookup"><span data-stu-id="26c0b-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="26c0b-116">![][BrowseSitesScreenshot]Diagnostische gegevens zijn ingeschakeld op basis van de per-app.</span><span class="sxs-lookup"><span data-stu-id="26c0b-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="26c0b-117">Door te bladeren naar de site die u deze functie inschakelen wilt op starten.</span><span class="sxs-lookup"><span data-stu-id="26c0b-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="26c0b-118">![][DiagnosticsLogs]In het menu instellingen, schuif omlaag naar de **bewaking** sectie en klik op **(1) diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="26c0b-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="26c0b-119">Vervolgens **(2) inschakelen** **toepassingslogboeken (bestandssysteem)** of **toepassingslogboeken (blob)** de **niveau** optie schakelt u de ernst van traceringen om vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="26c0b-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="26c0b-120">Als u net probeert om vertrouwd te raken met de functie, het niveau instellen op **uitgebreid** om te controleren of alle trace-instructies worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="26c0b-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="26c0b-121">Klik op **opslaan** boven aan de blade en u bent klaar om logboeken weer te geven.</span><span class="sxs-lookup"><span data-stu-id="26c0b-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="26c0b-122">Hoe hoger de **ernstniveau** meer bronnen worden verbruikt om u te melden en de meer traceringen worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="26c0b-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="26c0b-123">Zorg ervoor dat **ernstniveau** is geconfigureerd voor de juiste uitgebreidheid voor een productie- of site intensief verkeer.</span><span class="sxs-lookup"><span data-stu-id="26c0b-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="26c0b-124">![][StreamingLogsScreenshot]Om weer te geven de **streaminglogboeken** uit binnen de Azure-portal klikt u op **(1) Logboekstream** ook in de **bewaking** sectie van het menu instellingen.</span><span class="sxs-lookup"><span data-stu-id="26c0b-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="26c0b-125">Als uw app is actief trace-instructies schrijven en vervolgens ziet u ze op in de **(2) streaming registreert UI** in bijna realtime.</span><span class="sxs-lookup"><span data-stu-id="26c0b-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="26c0b-126">Console</span><span class="sxs-lookup"><span data-stu-id="26c0b-126">Console</span></span>
<span data-ttu-id="26c0b-127">De **Azure-portal** consoletoegang tot uw app biedt.</span><span class="sxs-lookup"><span data-stu-id="26c0b-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="26c0b-128">U kunt verkennen van uw app-bestandssysteem en powershell/cmd scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="26c0b-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="26c0b-129">U zijn gebonden aan dezelfde machtigingen instellen als uw app-code uitgevoerd bij het uitvoeren van consoleopdrachten.</span><span class="sxs-lookup"><span data-stu-id="26c0b-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="26c0b-130">Toegang tot beveiligde mappen of uitvoeren van scripts waarvoor verhoogde machtigingen is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="26c0b-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="26c0b-131">![][ConsoleScreenshot]In het menu instellingen, schuif omlaag naar **ontwikkelingsprogramma's** sectie en klik op **(1) Console** en de **(2) console** UI wordt geopend aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="26c0b-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="26c0b-132">Om vertrouwd te raken met de **console**, probeer basisopdrachten, zoals:</span><span class="sxs-lookup"><span data-stu-id="26c0b-132">To get familiar with the **console**, try basic commands like:</span></span>

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
