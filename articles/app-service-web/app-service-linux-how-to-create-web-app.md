---
title: een Azure aaaCreate web-app uitgevoerd op Linux | Microsoft Docs
description: Web-app maken van workflow voor Azure-Web-App op Linux.
keywords: Azure app service, web-app, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="24d34-104">Een Azure-web-app uitgevoerd op Linux maken</span><span class="sxs-lookup"><span data-stu-id="24d34-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="24d34-105">Hello Azure portal toocreate uw web-app gebruiken</span><span class="sxs-lookup"><span data-stu-id="24d34-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="24d34-106">U kunt beginnen met het maken van uw web-app op Linux van Hallo [Azure-portal](https://portal.azure.com) zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="24d34-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Beginnen met het maken van een web-app op Hallo Azure-portal][1]

<span data-ttu-id="24d34-108">Vervolgens Hallo **blade maken** wordt geopend zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="24d34-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![blade Hallo-maken][2]

1. <span data-ttu-id="24d34-110">Uw web-app een naam geven.</span><span class="sxs-lookup"><span data-stu-id="24d34-110">Give your web app a name.</span></span>
2. <span data-ttu-id="24d34-111">Kies een bestaande resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="24d34-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="24d34-112">(Zie beschikbare regio's in Hallo [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="24d34-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="24d34-113">Kies een bestaand Azure App Service-abonnement of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="24d34-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="24d34-114">(Zie de opmerkingen bij de App Service-plan in Hallo [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="24d34-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="24d34-115">Kies de toepassing hello stack die u van plan toouse bent.</span><span class="sxs-lookup"><span data-stu-id="24d34-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="24d34-116">U kunt kiezen tussen verschillende versies van Node.js, PHP, .net Core en Ruby.</span><span class="sxs-lookup"><span data-stu-id="24d34-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="24d34-117">Nadat u Hallo app hebt gemaakt, kunt u Hallo toepassing stack van Hallo toepassingsinstellingen zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="24d34-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Toepassingsinstellingen][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="24d34-119">Uw web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="24d34-119">Deploy your web app</span></span>
<span data-ttu-id="24d34-120">Kiezen **implementatieopties** van Hallo management portal biedt u Hallo optie toouse lokale Git- of GitHub-opslagplaats toodeploy uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="24d34-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="24d34-121">Hallo overige Hallo-instructies zijn vergelijkbaar toothose voor een niet-Linux-web-app.</span><span class="sxs-lookup"><span data-stu-id="24d34-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="24d34-122">U kunt Hallo instructies in [lokale Git-implementatie](app-service-deploy-local-git.md) of [continue implementatie](app-service-continuous-deployment.md) toodeploy uw app.</span><span class="sxs-lookup"><span data-stu-id="24d34-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="24d34-123">U kunt uw toepassing tooyour site ook FTP-tooupload.</span><span class="sxs-lookup"><span data-stu-id="24d34-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="24d34-124">U kunt krijgen Hallo FTP-eindpunt voor uw web-app van Hallo diagnostics sectie logs zoals weergegeven in Hallo volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="24d34-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Diagnostische logboeken][4]

## <a name="next-steps"></a><span data-ttu-id="24d34-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24d34-126">Next steps</span></span>
* [<span data-ttu-id="24d34-127">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="24d34-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="24d34-128">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="24d34-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="24d34-129">Met behulp van Ruby in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="24d34-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="24d34-130">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="24d34-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
