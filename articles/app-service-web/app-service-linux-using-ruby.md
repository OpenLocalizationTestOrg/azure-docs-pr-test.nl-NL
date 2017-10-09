---
title: aaaUsing Ruby in Azure App Service Web-App op Linux | Microsoft Docs
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
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="543cb-104">Met behulp van Ruby in Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="543cb-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="543cb-105">Met Hallo meest recente update tooour back-end, is er ondersteuning voor Ruby v.2.3 geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="543cb-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="543cb-106">Instelling Hallo configuratie van uw Linux-web-app, kunt u Hallo toepassing stack wijzigen.</span><span class="sxs-lookup"><span data-stu-id="543cb-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="543cb-107">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="543cb-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="543cb-108">In de nieuwe menu Hallo in Hallo [Azure-portal](https://portal.azure.com), kunt u toocreate een Web-App op Linux Hallo Web + mobiel option zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="543cb-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Beginnen met het maken van een web-app op Hallo Azure-portal][1]

<span data-ttu-id="543cb-110">Vervolgens Hallo **blade maken** wordt geopend zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="543cb-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![blade Hallo-maken][2]

1. <span data-ttu-id="543cb-112">Uw web-app een naam geven.</span><span class="sxs-lookup"><span data-stu-id="543cb-112">Give your web app a name.</span></span>
2. <span data-ttu-id="543cb-113">Kies een bestaande resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="543cb-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="543cb-114">(Zie beschikbare regio's in Hallo [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="543cb-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="543cb-115">Kies een bestaand Azure App Service-abonnement of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="543cb-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="543cb-116">(Zie de opmerkingen bij de App Service-plan in Hallo [sectie beperkingen](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="543cb-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="543cb-117">Hallo Ruby kiezen uit Hallo ingebouwde Runtime stacks.</span><span class="sxs-lookup"><span data-stu-id="543cb-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="543cb-118">Nadat uw Ruby web-app wordt gemaakt, kunt u met Git- of FTP-tooit kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="543cb-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="543cb-119">toolearn informatie over het maken van een Ruby app Hallo controleren [get-handleiding](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="543cb-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="543cb-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="543cb-120">Next steps</span></span>
* [<span data-ttu-id="543cb-121">Wat is een op Linux-Web-App?</span><span class="sxs-lookup"><span data-stu-id="543cb-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="543cb-122">Lokale Git-implementatie tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="543cb-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="543cb-123">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="543cb-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="543cb-124">Een Ruby App maken met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="543cb-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png