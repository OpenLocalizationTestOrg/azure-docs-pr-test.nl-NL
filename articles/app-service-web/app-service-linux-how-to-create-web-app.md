---
title: Een Azure-web-app uitgevoerd op Linux maken | Microsoft Docs
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="25607-104">Een Azure-web-app uitgevoerd op Linux maken</span><span class="sxs-lookup"><span data-stu-id="25607-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="25607-105">De Azure portal gebruiken om uw web-app maken</span><span class="sxs-lookup"><span data-stu-id="25607-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="25607-106">U kunt beginnen met het maken van uw web-app op Linux van de [Azure-portal](https://portal.azure.com) zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="25607-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Beginnen met het maken van een web-app in de Azure portal][1]

<span data-ttu-id="25607-108">Vervolgens moet de **blade maken** opent, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="25607-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![De blade maken][2]

1. <span data-ttu-id="25607-110">Uw web-app een naam geven.</span><span class="sxs-lookup"><span data-stu-id="25607-110">Give your web app a name.</span></span>
2. <span data-ttu-id="25607-111">Kies een bestaande resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="25607-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="25607-112">(Zie beschikbare regio's in de [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="25607-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="25607-113">Kies een bestaand Azure App Service-abonnement of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="25607-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="25607-114">(Zie de opmerkingen bij de App Service-plan in de [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="25607-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="25607-115">Kies de stack van de toepassing die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25607-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="25607-116">U kunt kiezen tussen verschillende versies van Node.js, PHP, .net Core en Ruby.</span><span class="sxs-lookup"><span data-stu-id="25607-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="25607-117">Nadat u de app hebt gemaakt, kunt u de toepassing-stack van de toepassingsinstellingen zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="25607-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Toepassingsinstellingen][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="25607-119">Uw web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="25607-119">Deploy your web app</span></span>
<span data-ttu-id="25607-120">Kiezen **implementatieopties** in de management portal biedt u de optie voor lokale Git- of GitHub-opslagplaats gebruiken voor het implementeren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25607-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="25607-121">De rest van de instructies zijn vergelijkbaar met die voor een niet-Linux-web-app.</span><span class="sxs-lookup"><span data-stu-id="25607-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="25607-122">U kunt de instructies in [lokale Git-implementatie](app-service-deploy-local-git.md) of [continue implementatie](app-service-continuous-deployment.md) om uw app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="25607-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="25607-123">U kunt ook FTP gebruiken voor het uploaden van uw toepassing naar uw site.</span><span class="sxs-lookup"><span data-stu-id="25607-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="25607-124">U kunt het FTP-eindpunt voor uw web-app krijgen van de diagnostische logboeken sectie zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="25607-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Diagnostische logboeken][4]

## <a name="next-steps"></a><span data-ttu-id="25607-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25607-126">Next steps</span></span>
* [<span data-ttu-id="25607-127">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="25607-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="25607-128">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="25607-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="25607-129">Met behulp van Ruby in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="25607-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="25607-130">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="25607-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
