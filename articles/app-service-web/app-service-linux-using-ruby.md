---
title: Met behulp van Ruby in Azure App Service-Web-App op Linux | Microsoft Docs
description: Met behulp van Ruby in Azure App Service-Web-App op Linux.
keywords: Azure app service, web-app, veelgestelde vragen over, linux, besturingssystemen, ruby
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="5aaff-104">Met behulp van Ruby in Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5aaff-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="5aaff-105">Er is ondersteuning voor Ruby v.2.3 geïntroduceerd met de meest recente update naar de back-end.</span><span class="sxs-lookup"><span data-stu-id="5aaff-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="5aaff-106">De configuratie van uw Linux-web-app instelt, kunt u de toepassing-stack.</span><span class="sxs-lookup"><span data-stu-id="5aaff-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="5aaff-107">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="5aaff-107">Using the Azure portal</span></span> ##

<span data-ttu-id="5aaff-108">In het nieuwe menu in de [Azure-portal](https://portal.azure.com), kunt u een Web-App maken in Linux van Web + mobiel optie, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="5aaff-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Beginnen met het maken van een web-app in de Azure portal][1]

<span data-ttu-id="5aaff-110">Vervolgens moet de **blade maken** opent, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="5aaff-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![De blade maken][2]

1. <span data-ttu-id="5aaff-112">Uw web-app een naam geven.</span><span class="sxs-lookup"><span data-stu-id="5aaff-112">Give your web app a name.</span></span>
2. <span data-ttu-id="5aaff-113">Kies een bestaande resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="5aaff-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="5aaff-114">(Zie beschikbare regio's in de [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5aaff-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="5aaff-115">Kies een bestaand Azure App Service-abonnement of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="5aaff-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="5aaff-116">(Zie de opmerkingen bij de App Service-plan in de [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5aaff-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="5aaff-117">Kies de Ruby in de stacks ingebouwde Runtime.</span><span class="sxs-lookup"><span data-stu-id="5aaff-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="5aaff-118">Nadat uw Ruby web-app wordt gemaakt, kunt u met de Git- of FTP-implementeren.</span><span class="sxs-lookup"><span data-stu-id="5aaff-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="5aaff-119">Voor meer informatie over het maken van een app Ruby, Controleer de [get-handleiding](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5aaff-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5aaff-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5aaff-120">Next steps</span></span>
* [<span data-ttu-id="5aaff-121">Wat is een op Linux-Web-App?</span><span class="sxs-lookup"><span data-stu-id="5aaff-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5aaff-122">Lokale Git-implementatie op de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5aaff-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="5aaff-123">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5aaff-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="5aaff-124">Een Ruby App maken met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5aaff-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png