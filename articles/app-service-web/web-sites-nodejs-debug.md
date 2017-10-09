---
title: aaaHow toodebug een Node.js-web-app in Azure App Service
description: Meer informatie over hoe toodebug een Node.js web-app in Azure App Service.
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="9a472-103">Hoe toodebug een Node.js web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9a472-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="9a472-104">Azure biedt ingebouwde diagnostics tooassist met Node.js-toepassingen die worden gehost foutopsporing [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="9a472-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="9a472-105">In dit artikel leert u hoe tooenable logboekregistratie van stdout en stderr, informatie over fout in de browser Hallo weergeven en hoe toodownload en weergave logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="9a472-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="9a472-106">Diagnostische gegevens voor Node.js-toepassingen die worden gehost op Azure wordt geleverd door [IISNode].</span><span class="sxs-lookup"><span data-stu-id="9a472-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="9a472-107">Hoewel dit artikel wordt beschreven Hallo veelgebruikte instellingen voor het verzamelen van diagnostische gegevens, biedt geen een volledig overzicht voor het werken met IISNode.</span><span class="sxs-lookup"><span data-stu-id="9a472-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="9a472-108">Zie voor meer informatie over het werken met IISNode hello [IISNode Readme] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a472-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="9a472-109">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="9a472-109">Enable logging</span></span>
<span data-ttu-id="9a472-110">Standaard bevat een App Service-web-app alleen diagnostische gegevens over implementaties, zoals wanneer u een web-app met Git implementeert.</span><span class="sxs-lookup"><span data-stu-id="9a472-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="9a472-111">Deze informatie is nuttig als u problemen tijdens de implementatie, zoals een fout ondervindt bij het installeren van een module waarnaar wordt verwezen in **package.json**, of als u een aangepaste implementatiescript gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a472-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="9a472-112">tooenable hello logboekregistratie van stdout en stderr stromen, moet u een **IISNode.yml** -bestand op basis van uw Node.js-toepassing hello en voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9a472-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="9a472-113">Hallo logboekregistratie van stderr en stdout van uw Node.js-toepassing is nu ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9a472-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="9a472-114">Hallo **IISNode.yml** bestand kan ook worden gebruikt toocontrol of beschrijvende fouten of ontwikkelaars fouten worden toohello browser geretourneerd wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="9a472-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="9a472-115">tooenable developer-fouten, toevoegen Hallo volgende regel toohello **IISNode.yml** bestand:</span><span class="sxs-lookup"><span data-stu-id="9a472-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="9a472-116">Zodra deze optie is ingeschakeld, wordt de IISNode Hallo laatste 64K van informatie die wordt verstuurd toostderr in plaats van een aangepaste fout, zoals 'Er is een interne serverfout opgetreden' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9a472-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="9a472-117">DevErrorsEnabled is handig bij het oplossen van problemen tijdens de ontwikkeling, waardoor het in een productieomgeving mogelijk fouten tot gevolg ontwikkeling tooend gebruikers worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9a472-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="9a472-118">Als hello **IISNode.yml** bestand al bestaat niet in uw toepassing, moet u uw web-app opnieuw starten na het publiceren van de toepassing hello bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9a472-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="9a472-119">Als u instellingen in een bestaand gewoon wijzigt **IISNode.yml** bestand dat eerder is gepubliceerd, niet opnieuw opstarten is vereist.</span><span class="sxs-lookup"><span data-stu-id="9a472-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="9a472-120">Als uw web-app is gemaakt met hello Azure opdrachtregelprogramma's of Azure PowerShell-Cmdlets standaard **IISNode.yml** bestand wordt automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9a472-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="9a472-121">toorestart hello web-app, selecteer Hallo web-app in Hallo [Azure Portal](https://portal.azure.com), en klik vervolgens op **opnieuw** knop:</span><span class="sxs-lookup"><span data-stu-id="9a472-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![knop opnieuw opstarten][restart-button]

<span data-ttu-id="9a472-123">Als hello Azure opdrachtregelprogramma's zijn geïnstalleerd in uw ontwikkelomgeving, kunt u Hallo opdracht toorestart Hallo web-app te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a472-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="9a472-124">Hoewel loggingEnabled en devErrorsEnabled Hallo meest gebruikte IISNode.yml configuratieopties zijn voor het vastleggen van diagnostische gegevens zijn IISNode.yml gebruikte tooconfigure tal van opties voor uw hostingomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a472-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="9a472-125">Zie voor een volledige lijst van de configuratieopties Hallo Hallo [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) bestand.</span><span class="sxs-lookup"><span data-stu-id="9a472-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="9a472-126">Toegang tot logboeken</span><span class="sxs-lookup"><span data-stu-id="9a472-126">Accessing logs</span></span>
<span data-ttu-id="9a472-127">Logboeken met diagnostische gegevens kunnen worden geopend op drie manieren; Hallo FTP File Transfer Protocol (), downloadt een Zip-archief met of bijgewerkt als een live stream van Hallo logboek (ook wel bekend als een tail).</span><span class="sxs-lookup"><span data-stu-id="9a472-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="9a472-128">Hallo Zip-archief van de logboekbestanden Hallo downloaden of de livestream Hallo weergeven vereisen hello Azure opdrachtregelprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9a472-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="9a472-129">Deze kunnen worden geïnstalleerd met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9a472-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="9a472-130">Na de installatie configureert zijn Hallo-hulpprogramma's toegankelijk via 'azure' Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="9a472-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="9a472-131">opdrachtregelprogramma's Hallo moet eerst worden geconfigureerde toouse uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9a472-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="9a472-132">Zie voor informatie over hoe de tooaccomplish bij deze taak Hallo **hoe toodownload en importeer publicatie-instellingen** sectie Hallo [hoe tooUse hello Azure opdrachtregelprogramma's](../xplat-cli-connect.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9a472-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="9a472-133">FTP</span><span class="sxs-lookup"><span data-stu-id="9a472-133">FTP</span></span>
<span data-ttu-id="9a472-134">Diagnostische gegevens over tooaccess Hallo via FTP, gaat u naar Hallo [Azure Portal](https://portal.azure.com), selecteer uw web-app en selecteer vervolgens Hallo **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="9a472-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="9a472-135">In Hallo **snelle koppelingen** sectie hello **FTP-logboeken met diagnostische gegevens** en **FTPS diagnostische LOGBOEKEN** koppelingen bieden toegang toohello logboeken met Hallo FTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="9a472-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="9a472-136">Als u niet eerder geconfigureerd gebruikersnaam en wachtwoord voor FTP- of implementatie, kunt u doen vanaf Hallo **Quick Start** pagina beheren door te selecteren **implementatiereferenties instellen**.</span><span class="sxs-lookup"><span data-stu-id="9a472-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="9a472-137">Hallo FTP-URL geretourneerd in Hallo dashboard is voor Hallo **logboekbestanden** directory waarin Hallo submappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a472-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="9a472-138">[Implementatiemethode](web-sites-deploy.md) -als u een implementatiemethode zoals Git, een directory van Hallo dezelfde naam wordt gemaakt en vindt u informatie toodeployments gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="9a472-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="9a472-139">nodejs - Stdout en stderr informatie vastgelegd van alle exemplaren van uw toepassing (wanneer loggingEnabled is ingesteld op true.)</span><span class="sxs-lookup"><span data-stu-id="9a472-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="9a472-140">Het ZIP-archief</span><span class="sxs-lookup"><span data-stu-id="9a472-140">Zip archive</span></span>
<span data-ttu-id="9a472-141">toodownload een Zip-archief van diagnostische logboeken hello, gebruik Hallo volgende opdracht uit hello Azure opdrachtregelprogramma's:</span><span class="sxs-lookup"><span data-stu-id="9a472-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="9a472-142">Dit wordt gedownload een **diagnostics.zip** in de huidige map Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a472-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="9a472-143">Dit archief bevat Hallo directory-structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a472-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="9a472-144">implementaties - een logboek van informatie over implementaties van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="9a472-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="9a472-145">Logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="9a472-145">LogFiles</span></span>
  
  * <span data-ttu-id="9a472-146">[Implementatiemethode](web-sites-deploy.md) -als u een implementatiemethode zoals Git, een directory van Hallo dezelfde naam wordt gemaakt en vindt u informatie toodeployments gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="9a472-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="9a472-147">nodejs - Stdout en stderr informatie vastgelegd van alle exemplaren van uw toepassing (wanneer loggingEnabled is ingesteld op true.)</span><span class="sxs-lookup"><span data-stu-id="9a472-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="9a472-148">Live stream (tail)</span><span class="sxs-lookup"><span data-stu-id="9a472-148">Live stream (tail)</span></span>
<span data-ttu-id="9a472-149">tooview een live stream van diagnostische logboekgegevens, gebruik Hallo volgende opdracht uit hello Azure opdrachtregelprogramma's:</span><span class="sxs-lookup"><span data-stu-id="9a472-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="9a472-150">Hiermee herstelt u een reeks gebeurtenissen die worden bijgewerkt wanneer deze zich op Hallo-server voordoen.</span><span class="sxs-lookup"><span data-stu-id="9a472-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="9a472-151">Deze stroom retourneren informatie over de implementatie, evenals stdout en stderr informatie (wanneer loggingEnabled is ingesteld op true.)</span><span class="sxs-lookup"><span data-stu-id="9a472-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="9a472-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a472-152">Next Steps</span></span>
<span data-ttu-id="9a472-153">In dit artikel u leert hoe tooenable en toegang diagnostische gegevens voor Azure.</span><span class="sxs-lookup"><span data-stu-id="9a472-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="9a472-154">Terwijl deze informatie is nuttig voor informatie over problemen die zich voordoen met uw toepassing, het tooa probleem met een module die u gebruikt of die versie Hallo van Node.js die wordt gebruikt door App Service Web Apps kan verwijzen is anders dan Hallo gebruikt in uw implementatie -omgeving.</span><span class="sxs-lookup"><span data-stu-id="9a472-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="9a472-155">Zie voor meer informatie in het werken met modules in Azure [Node.js-Modules gebruiken met Azure-toepassingen](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9a472-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="9a472-156">Zie voor meer informatie over het opgeven van een Node.js-versie voor uw toepassing [een Node.js-versie opgeven in een Azure-toepassing].</span><span class="sxs-lookup"><span data-stu-id="9a472-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="9a472-157">Zie voor meer informatie, ook Hallo [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="9a472-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="9a472-158">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="9a472-158">What's changed</span></span>
* <span data-ttu-id="9a472-159">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="9a472-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="9a472-160">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="9a472-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9a472-161">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="9a472-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[een Node.js-versie opgeven in een Azure-toepassing]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

