---
title: configuratie voor Node.js in Azure-Web-App op Linux aaaUsing PM2 | Microsoft Docs
description: Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux
keywords: Azure app service, web-app, nodejs, pm2, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="ad9b6-104">PM2 configuratie gebruiken voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ad9b6-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="ad9b6-105">Als u Hallo toepassing stack tooNode.js voor Azure-Web-App op Linux instellen, krijgt u Hallo optie tooset een Node.js-bestand voor opstarten zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9b6-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Een Node.js-bestand voor opstarten][1]

<span data-ttu-id="ad9b6-107">U kunt deze optie toodo een Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9b6-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="ad9b6-108">Geef het opstartscript Hallo voor uw Node.js-app (bijvoorbeeld: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="ad9b6-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="ad9b6-109">Geef Hallo PM2 configuration file toouse voor uw Node.js-app (bijvoorbeeld: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="ad9b6-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ad9b6-110">Als u uw Node.js-processen toorestart automatisch wilt wanneer bepaalde bestanden zijn gewijzigd, moet u Hallo PM2 configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="ad9b6-111">Uw toepassing won't anders wordt opnieuw opgestart na ontvangst van meldingen (bijvoorbeeld wanneer uw toepassingscode gewijzigd).</span><span class="sxs-lookup"><span data-stu-id="ad9b6-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="ad9b6-112">U kunt controleren Hallo Node.js [verwerken bestand documentatie](http://pm2.keymetrics.io/docs/usage/application-declaration/) voor alle opties hello, maar hier een voorbeeld volgt van wat u als uw bestand process.json gebruiken kunt:</span><span class="sxs-lookup"><span data-stu-id="ad9b6-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="ad9b6-113">Belangrijke opmerkingen toonote in deze configuratie zijn:</span><span class="sxs-lookup"><span data-stu-id="ad9b6-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="ad9b6-114">de eigenschap 'script' Hello geeft startscript van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="ad9b6-115">Hallo 'exemplaren'-eigenschap geeft aan hoeveel exemplaren van Hallo knooppunt proces toolaunch.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="ad9b6-116">Als u uw toepassing op grotere virtuele machines die meerdere kernen hebben uitvoert, is het een goed idee toomaximize uw resources door een hogere waarde hier.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="ad9b6-117">Hallo 'volgen' matrix geeft alle bestanden die u toorestart Hallo knooppunt proces voor wilt zien wanneer ze wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="ad9b6-118">Voor 'watch_options' hello moet momenteel u toospecify 'usePolling' als waar vanwege Hallo manier die de inhoud van uw toepassing is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ad9b6-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad9b6-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad9b6-119">Next steps</span></span>
* [<span data-ttu-id="ad9b6-120">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="ad9b6-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="ad9b6-121">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ad9b6-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
