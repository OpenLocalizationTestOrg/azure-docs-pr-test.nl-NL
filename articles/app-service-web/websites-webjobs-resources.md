---
title: aaaAzure WebJobs documentatiebronnen
description: Bronnen voor informatie aanbevolen hoe toouse Azure WebJobs en hello Azure WebJobs SDK.
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Azure WebJobs documentatiebronnen
## <a name="overview"></a>Overzicht
Dit onderwerp bevat koppelingen toodocumentation resources over het toouse Azure WebJobs en hello Azure WebJobs SDK. Azure WebJobs bieden een eenvoudige manier toorun scripts of programma's als achtergrond processen in Hallo context van een [App Service-web-app, API-app of mobiele app](../app-service/app-service-value-prop-what-is.md). U kunt uploaden en uitvoeren van een uitvoerbaar bestand zoals als cmd bat, exe (.NET) ps1, servicel, php, py, js en jar. Deze programma's uitvoeren als WebJobs volgens een schema (cron) of continu.

doel van Hallo Hallo [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) is toosimplify Hallo code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden. Hallo WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's. Bovendien heeft toobe extensible ontworpen en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Azure Functions](../azure-functions/functions-overview.md) (momenteel in preview) is gebaseerd op een versie van Hallo WebJobs SDK die met C#-script, Node.js en andere talen werkt. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Maken, implementeren en beheren van WebJobs is naadloos met geïntegreerde tooling in Visual Studio. WebJobs van sjablonen maken, publiceren en beheren (uitgevoerd, stoppen, bewaken en fouten opsporen) ze. 

Hallo WebJobs-dashboard in hello Azure-portal biedt krachtige beheermogelijkheden die u u volledige controle over Hallo uitvoering van WebJobs hebt, met inbegrip van Hallo mogelijkheid tooinvoke afzonderlijke functies binnen WebJobs. Hallo dashboard worden ook de functie runtimes en logboekregistratie uitvoer weergegeven. 

## <a name="getstarted"></a>Aan de slag met webtaken en Hallo WebJobs SDK
* [Inleiding tooAzure WebJobs](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure WebJobs geweldig zijn en u moet beginnen met het gebruik ervan nu!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Blogbericht door Troy zoeken.)
* [Azure WebJobs-functies](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Wat is Hallo WebJobs SDK](websites-dotnet-webjobs-sdk.md)
* [Achtergrond taken richtlijnen door Microsoft Patterns and practice](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [1.1.0 aankondigen Hallo RTM van Microsoft Azure WebJobs SDK](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Aan de slag met hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md)
* [Hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Hoe toouse Azure table storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Hoe toouse Azure Service Bus met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs SDK Naslaggids (download PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [WebJobs instellingen documentatie in GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Video's
  * [Webtaken en Hallo WebJobs SDK](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Azure WebJobs video series op Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Inleiding tot webtaken Tooling voor Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs Tooling en foutopsporing op afstand](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Azure WebJobs-Update met Pranav Rastogi - uitbreidbaarheid in versie 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Zie ook uit te voeren op Hallo [implementeren WebJobs](#deploy) en [testen en foutopsporing WebJobs](#debug).

## <a name="deploy"></a>WebJobs implementeren
* [Hoe tooDeploy Azure WebJobs met Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Hoe toodeploy met behulp van WebJobs hello Azure Portal](web-sites-create-web-jobs.md)
* [Inschakelen van de opdrachtregel of continue levering van Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Implementatie van een .NET-console-app tooAzure WebJobs met GIT](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Een tooAzure F # WebJob implementeren](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Implementatie van aangepaste services als Azure Webjobs](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Video's
  * [Inleiding tot webtaken Tooling voor Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs Tooling en foutopsporing op afstand](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>WebJobs plannen
* [Hello Azure webtaak dialoogvenster toevoegen](websites-dotnet-deploy-webjobs.md#configure)
* [Maken van een webtaak gepland in hello Azure Portal](web-sites-create-web-jobs.md#CreateScheduled)
* [Koppelen van een scheduler-taak tooa webtaak](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Azure WebJobs met cron expressies plannen](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Afzonderlijke webtaak functies met Hallo WebJobs SDK TimerTrigger plannen](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Testen en foutopsporing WebJobs
* [Nieuwe ontwikkelaars en foutopsporing functies voor Azure WebJobs in Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hallo WebJobs-Dashboard weergeven](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Hoe toowrite registreert met behulp van Hallo WebJobs SDK en ze weergeven in Hallo Dashboard](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Externe foutopsporing WebJobs](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Wie blob geschreven?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Hosting interactieve code in Hallo Cloud](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Tracering tooAzure WebJobs toevoegen](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Controleren, vaststellen en oplossen van Microsoft Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Video's
  * [WebJobs Tooling en foutopsporing op afstand](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Schalen WebJobs
* [Schalen van uw webtoepassing met Azure Websites](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure App Service: Grootschalige gereed-voor-Business-Web-Apps worden veranderd](https://channel9.msdn.com/Events/Build/2014/3-626). Dekt schalen van web-apps met WebJobs, met inbegrip van Hallo WebJobs SDK.
* Video's
  * [WebJobs uitbreiden](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Aanvullende bronnen voor WebJobs
* [Azure WebJobs GA blogbericht door Magnus Mårtensson](http://magnusmartensson.com/azure-webjobs-ga)
* [De uitvoering van Powershell Web taken in Azure App Service](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Ophalen van een melding wanneer uw Azure WebJobs geactiveerd is voltooid](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Eenvoudige Web-App back-up bewaarbeleid met WebJobs](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Azure-Web-Apps en Cloudservices trage op de eerste aanvraag](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Toont hoe toouse WebJobs toosimulate AlwaysOn-functie is alleen beschikbaar voor de Standard-prijscategorie Hallo Hallo.
* [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Voor de WebJobs SDK correct afsluiten, Zie [correct afsluiten](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).)
* [Automatisering van back-ups met Azure WebJobs & AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Video's
  * [Azure WebJobs-video's door Magnus Mårtensson](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Azure WebJobs video series op Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Aanvullende bronnen voor WebJobs SDK
* [Opmerkingen bij de Release van de WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [De broncode WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk)
* [Broncode is WebJobs SDK extensions](https://github.com/Azure/azure-webjobs-sdk-extensions), met [uitbreidingsmodel voor gedetailleerde uitleg van toohello](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [De broncode WebJobs SDK-Script](https://github.com/Azure/azure-webjobs-sdk-script/) (gebruikt voor [Azure Functions](../azure-functions/functions-overview.md))
* [Webtaak tooupload FREB bestanden tooAzure opslag met behulp van Hallo WebJobs SDK](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Azure webjobs buiten Azure hosten, gehoste Hello logboekregistratie voordelen van een Azure webtaak](http://bypassion.dk/?p=510)
* [Het bouwen van een hulpprogramma voor het importeren van gegevens met Azure WebJobs](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Overzicht van Azure Functions](../azure-functions/functions-overview.md)
* Video's
  * [Azure WebJobs video series op Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Webtaak voorbeeldtoepassingen
* [Voorbeeldtoepassingen geleverd door Hallo WebJobs-team op GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Eenvoudige Azure-Web-App met de WebJobs Backend met Hallo WebJobs SDK](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Demonstreert gebruik van geplande en gebeurtenisafhankelijke WebJobs. Zie het blogbericht van Hallo [Rebuilding hello SiteMonitR met behulp van Azure WebJobs SDK](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogs
* [Azure Blog](/blog)
* [Blog van Amit Apple](http://blog.amitapple.com/). Richt zich op WebJobs (geen hello SDK).
* [Blog van Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Help opvragen bij WebJobs
* [StackOverflow voor WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow voor Hallo WebJobs SDK](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow voor Azure Functions](http://stackoverflow.com/questions/tagged/azure-functions)
* [Azure- en ASP.NET-forum](http://forums.asp.net/1247.aspx)
* [Azure App Service Web Apps-forum](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Azure Web Apps User Voice-site](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Hallo hashtag #AzureWebJobs gebruiken.
* [Een API-fout of probleem rapporteren](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

