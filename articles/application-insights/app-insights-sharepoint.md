---
title: een SharePoint-site met Application Insights aaaMonitor
description: Een nieuwe toepassing bewaken met een nieuwe instrumentatiesleutel
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="22785-103">Een SharePoint-site met Application Insights bewaken</span><span class="sxs-lookup"><span data-stu-id="22785-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="22785-104">Azure Application Insights wordt bewaakt Hallo beschikbaarheid, prestaties en het gebruik van uw apps.</span><span class="sxs-lookup"><span data-stu-id="22785-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="22785-105">U leert hier hoe tooset het voor een SharePoint-site.</span><span class="sxs-lookup"><span data-stu-id="22785-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="22785-106">Een Application Insights-resource maken</span><span class="sxs-lookup"><span data-stu-id="22785-106">Create an Application Insights resource</span></span>
<span data-ttu-id="22785-107">In Hallo [Azure-portal](https://portal.azure.com), maak een nieuwe Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="22785-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="22785-108">Kies ASP.NET als Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22785-108">Choose ASP.NET as hello application type.</span></span>

![Klik op eigenschappen en druk op ctrl + C Hallo sleutel selecteren](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="22785-110">Hallo-blade die wordt geopend is Hallo plaats hier u prestatie- en gebruiksgegevens over uw app ziet.</span><span class="sxs-lookup"><span data-stu-id="22785-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="22785-111">tooget back tooit volgende keer dat u zich tooAzure aanmeldt, moet u een tegel voor op Hallo startscherm.</span><span class="sxs-lookup"><span data-stu-id="22785-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="22785-112">U kunt ook op Bladeren toofind deze.</span><span class="sxs-lookup"><span data-stu-id="22785-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="22785-113">Onze script tooyour webpagina's toevoegen</span><span class="sxs-lookup"><span data-stu-id="22785-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="22785-114">Haal Hallo script voor webpagina's in Snel starten:</span><span class="sxs-lookup"><span data-stu-id="22785-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="22785-115">Voeg Hallo script net vóór Hallo &lt;/head&gt; tag van elke pagina die u wilt tootrack.</span><span class="sxs-lookup"><span data-stu-id="22785-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="22785-116">Als uw website een basispagina heeft, kunt u er Hallo script plaatsen.</span><span class="sxs-lookup"><span data-stu-id="22785-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="22785-117">In een ASP.NET MVC-project plaatst u deze bijvoorbeeld in View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="22785-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="22785-118">Hallo-script bevat de instrumentatiesleutel Hallo waarin wordt verwezen Hallo telemetrie tooyour Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="22785-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="22785-119">Hallo code tooyour sitepagina's toevoegen</span><span class="sxs-lookup"><span data-stu-id="22785-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="22785-120">Op de basispagina Hallo</span><span class="sxs-lookup"><span data-stu-id="22785-120">On hello master page</span></span>
<span data-ttu-id="22785-121">Als u basispagina van Hallo site bewerken kunt, wordt die voorzien in bewaking voor elke pagina van Hallo-site.</span><span class="sxs-lookup"><span data-stu-id="22785-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="22785-122">Hallo basispagina uitchecken en bewerken met behulp van SharePoint Designer of een andere editor.</span><span class="sxs-lookup"><span data-stu-id="22785-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="22785-123">Voeg code net vóór Hallo Hallo </head> label.</span><span class="sxs-lookup"><span data-stu-id="22785-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="22785-124">Of op afzonderlijke pagina’s</span><span class="sxs-lookup"><span data-stu-id="22785-124">Or on individual pages</span></span>
<span data-ttu-id="22785-125">een beperkt aantal pagina's, toomonitor Hallo script afzonderlijk toevoegen tooeach pagina.</span><span class="sxs-lookup"><span data-stu-id="22785-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="22785-126">Een webonderdeel invoegen en insluiten Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="22785-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="22785-127">Gegevens over uw app weergeven</span><span class="sxs-lookup"><span data-stu-id="22785-127">View data about your app</span></span>
<span data-ttu-id="22785-128">Implementeer uw app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="22785-128">Redeploy your app.</span></span>

<span data-ttu-id="22785-129">Retour tooyour toepassing blade in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22785-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="22785-130">Hallo eerste gebeurtenissen wordt weergegeven in de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="22785-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="22785-131">Klik na een paar seconden op Vernieuwen als u meer gegevens verwacht.</span><span class="sxs-lookup"><span data-stu-id="22785-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="22785-132">Overzichtsblade hello, klik op **gebruiksanalyse** toosee toocharts van gebruikers, sessies en paginaweergaven:</span><span class="sxs-lookup"><span data-stu-id="22785-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="22785-133">Klik op een grafiek toosee meer details - bijvoorbeeld paginaweergaven:</span><span class="sxs-lookup"><span data-stu-id="22785-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="22785-134">Of Gebruikers:</span><span class="sxs-lookup"><span data-stu-id="22785-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="22785-135">Gebruikers-id vastleggen</span><span class="sxs-lookup"><span data-stu-id="22785-135">Capturing User Id</span></span>
<span data-ttu-id="22785-136">Hallo standaardwebpagina codefragment Hallo gebruikers-id van SharePoint niet vastleggen, maar kunt u dat doen met een kleine wijziging.</span><span class="sxs-lookup"><span data-stu-id="22785-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="22785-137">Kopieer de instrumentatiesleutel van uw app van Hallo Essentials vervolgkeuzelijst in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="22785-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="22785-138">Vervangen door de instrumentatiesleutel Hallo 'XXXX' in hello codefragment hieronder.</span><span class="sxs-lookup"><span data-stu-id="22785-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="22785-139">Hallo script insluiten in uw SharePoint-app in plaats van Hallo codefragment die u via Hallo-portal krijgen.</span><span class="sxs-lookup"><span data-stu-id="22785-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="22785-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22785-140">Next Steps</span></span>
* <span data-ttu-id="22785-141">[Webtests](app-insights-monitor-web-app-availability.md) toomonitor Hallo beschikbaarheid van uw site.</span><span class="sxs-lookup"><span data-stu-id="22785-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="22785-142">[Application Insights](app-insights-overview.md) voor andere typen app.</span><span class="sxs-lookup"><span data-stu-id="22785-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


