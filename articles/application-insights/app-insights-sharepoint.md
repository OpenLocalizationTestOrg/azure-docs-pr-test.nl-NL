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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Een SharePoint-site met Application Insights bewaken
Azure Application Insights wordt bewaakt Hallo beschikbaarheid, prestaties en het gebruik van uw apps. U leert hier hoe tooset het voor een SharePoint-site.

## <a name="create-an-application-insights-resource"></a>Een Application Insights-resource maken
In Hallo [Azure-portal](https://portal.azure.com), maak een nieuwe Application Insights-resource. Kies ASP.NET als Hallo toepassingstype.

![Klik op eigenschappen en druk op ctrl + C Hallo sleutel selecteren](./media/app-insights-sharepoint/01-new.png)

Hallo-blade die wordt geopend is Hallo plaats hier u prestatie- en gebruiksgegevens over uw app ziet. tooget back tooit volgende keer dat u zich tooAzure aanmeldt, moet u een tegel voor op Hallo startscherm. U kunt ook op Bladeren toofind deze.

## <a name="add-our-script-tooyour-web-pages"></a>Onze script tooyour webpagina's toevoegen
Haal Hallo script voor webpagina's in Snel starten:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Voeg Hallo script net vóór Hallo &lt;/head&gt; tag van elke pagina die u wilt tootrack. Als uw website een basispagina heeft, kunt u er Hallo script plaatsen. In een ASP.NET MVC-project plaatst u deze bijvoorbeeld in View\Shared\_Layout.cshtml

Hallo-script bevat de instrumentatiesleutel Hallo waarin wordt verwezen Hallo telemetrie tooyour Application Insights-resource.

### <a name="add-hello-code-tooyour-site-pages"></a>Hallo code tooyour sitepagina's toevoegen
#### <a name="on-hello-master-page"></a>Op de basispagina Hallo
Als u basispagina van Hallo site bewerken kunt, wordt die voorzien in bewaking voor elke pagina van Hallo-site.

Hallo basispagina uitchecken en bewerken met behulp van SharePoint Designer of een andere editor.

![](./media/app-insights-sharepoint/03-master.png)

Voeg code net vóór Hallo Hallo </head> label. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Of op afzonderlijke pagina’s
een beperkt aantal pagina's, toomonitor Hallo script afzonderlijk toevoegen tooeach pagina. 

Een webonderdeel invoegen en insluiten Hallo codefragment.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Gegevens over uw app weergeven
Implementeer uw app opnieuw.

Retour tooyour toepassing blade in Hallo [Azure-portal](https://portal.azure.com).

Hallo eerste gebeurtenissen wordt weergegeven in de zoekopdracht. 

![](./media/app-insights-sharepoint/09-search.png)

Klik na een paar seconden op Vernieuwen als u meer gegevens verwacht.

Overzichtsblade hello, klik op **gebruiksanalyse** toosee toocharts van gebruikers, sessies en paginaweergaven:

![](./media/app-insights-sharepoint/06-usage.png)

Klik op een grafiek toosee meer details - bijvoorbeeld paginaweergaven:

![](./media/app-insights-sharepoint/07-pages.png)

Of Gebruikers:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Gebruikers-id vastleggen
Hallo standaardwebpagina codefragment Hallo gebruikers-id van SharePoint niet vastleggen, maar kunt u dat doen met een kleine wijziging.

1. Kopieer de instrumentatiesleutel van uw app van Hallo Essentials vervolgkeuzelijst in Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Vervangen door de instrumentatiesleutel Hallo 'XXXX' in hello codefragment hieronder. 
2. Hallo script insluiten in uw SharePoint-app in plaats van Hallo codefragment die u via Hallo-portal krijgen.

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



## <a name="next-steps"></a>Volgende stappen
* [Webtests](app-insights-monitor-web-app-availability.md) toomonitor Hallo beschikbaarheid van uw site.
* [Application Insights](app-insights-overview.md) voor andere typen app.

<!--Link references-->


