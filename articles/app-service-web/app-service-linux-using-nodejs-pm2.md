---
title: Met PM2 configuratie voor Node.js in Azure-Web-App op Linux | Microsoft Docs
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
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="4630d-104">PM2 configuratie gebruiken voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="4630d-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="4630d-105">Als u de toepassing-stack ingesteld op Node.js voor Azure-Web-App op Linux, krijgt u de mogelijkheid om in te stellen van een Node.js opstartbestand, zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="4630d-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Een Node.js-bestand voor opstarten][1]

<span data-ttu-id="4630d-107">U kunt deze optie gebruiken om een van de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="4630d-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="4630d-108">Geef het opstartscript voor uw Node.js-app (bijvoorbeeld: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="4630d-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="4630d-109">Geef de PM2 configuratiebestand moet worden gebruikt voor uw Node.js-app (bijvoorbeeld: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="4630d-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4630d-110">Als u wilt dat uw Node.js-processen worden automatisch opnieuw opgestart wanneer bepaalde bestanden zijn gewijzigd, gebruikt u de configuratie van de PM2.</span><span class="sxs-lookup"><span data-stu-id="4630d-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="4630d-111">Uw toepassing won't anders wordt opnieuw opgestart na ontvangst van meldingen (bijvoorbeeld wanneer uw toepassingscode gewijzigd).</span><span class="sxs-lookup"><span data-stu-id="4630d-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="4630d-112">U kunt de Node.js controleren [verwerken bestand documentatie](http://pm2.keymetrics.io/docs/usage/application-declaration/) voor alle opties maar volgende is een voorbeeld van wat u kunt gebruiken als uw bestand process.json:</span><span class="sxs-lookup"><span data-stu-id="4630d-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="4630d-113">Belangrijke opmerkingen in deze configuratie zijn:</span><span class="sxs-lookup"><span data-stu-id="4630d-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="4630d-114">De scripteigenschap '' geeft startscript van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4630d-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="4630d-115">De eigenschap 'exemplaren' bepaalt hoeveel exemplaren van het knooppunt proces te starten.</span><span class="sxs-lookup"><span data-stu-id="4630d-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="4630d-116">Als u uw toepassing op grotere virtuele machines die meerdere kernen hebben uitvoert, is het een goed idee om uw resources maximaliseren door een hogere waarde hier.</span><span class="sxs-lookup"><span data-stu-id="4630d-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="4630d-117">De matrix 'volgen' geeft alle bestanden die u het proces van het knooppunt voor het opnieuw opstarten wilt als ze wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4630d-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="4630d-118">Voor de 'watch_options' moet u momenteel 'usePolling' opgeeft als waar vanwege de manier waarop die de inhoud van uw toepassing is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4630d-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4630d-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4630d-119">Next steps</span></span>
* [<span data-ttu-id="4630d-120">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="4630d-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="4630d-121">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4630d-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
