---
title: Azure Storage toevoegen met behulp van verbonden Services in Visual Studio | Microsoft Docs
description: Azure Storage toevoegen aan uw app met behulp van de Visual Studio verbonden dialoogvenster Services toevoegen
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="80d4d-103">Azure-opslag toe te voegen met behulp van Visual Studio verbonden Services</span><span class="sxs-lookup"><span data-stu-id="80d4d-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="80d4d-104">Met Visual Studio, kunt u een van de volgende naar Azure Storage met behulp van de **verbonden Services toevoegen** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="80d4d-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="80d4d-105">C#-cloudservice</span><span class="sxs-lookup"><span data-stu-id="80d4d-105">C# cloud service</span></span>
- <span data-ttu-id="80d4d-106">.NET-back-end voor mobiele service</span><span class="sxs-lookup"><span data-stu-id="80d4d-106">.NET backend mobile service</span></span>
- <span data-ttu-id="80d4d-107">ASP.NET-website of service</span><span class="sxs-lookup"><span data-stu-id="80d4d-107">ASP.NET website or service</span></span>
- <span data-ttu-id="80d4d-108">ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="80d4d-108">ASP.NET Core service</span></span>
- <span data-ttu-id="80d4d-109">Azure webtaak-service</span><span class="sxs-lookup"><span data-stu-id="80d4d-109">Azure WebJob service</span></span> 

<span data-ttu-id="80d4d-110">De functionaliteit van de gekoppelde service worden alle benodigde verwijzingen en verbinding code toegevoegd aan uw project en de configuratiebestanden op de juiste wijze wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="80d4d-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="80d4d-111">Na voltooiing wordt de **verbonden Services toevoegen** dialoogvenster automatisch wordt weergegeven met gedetailleerde informatie over de stappen die nodig zijn om te gaan werken met blob storage, wachtrijen, documentatie en tabellen.</span><span class="sxs-lookup"><span data-stu-id="80d4d-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="80d4d-112">Verbinding maken met Azure Storage met het dialoogvenster Services verbonden</span><span class="sxs-lookup"><span data-stu-id="80d4d-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="80d4d-113">Open het project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80d4d-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="80d4d-114">In **Solution Explorer**, met de rechtermuisknop op de **verbonden Services** knooppunt en klik in het contextmenu en selecteer **verbonden Service toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="80d4d-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Toevoegen van Azure service verbonden](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="80d4d-116">In de **verbonden Services** pagina **Cloud-opslag met Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="80d4d-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure-opslag toevoegen](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="80d4d-118">In de **Azure Storage** dialoogvenster, selecteer een bestaand opslagaccount en selecteert u **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="80d4d-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="80d4d-119">Als u een opslagaccount maken wilt, gaat u naar de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="80d4d-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="80d4d-120">Ga anders verder met stap 6.</span><span class="sxs-lookup"><span data-stu-id="80d4d-120">Otherwise, skip to step 6.</span></span>
    
    ![Bestaande opslagaccount toevoegen aan project](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="80d4d-122">Een opslagaccount maken:</span><span class="sxs-lookup"><span data-stu-id="80d4d-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="80d4d-123">Selecteer **een nieuw Opslagaccount maken** aan de onderkant van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80d4d-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="80d4d-124">Vul de **Storage-Account maken** dialoogvenster en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="80d4d-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nieuwe Azure storage-account](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="80d4d-126">Wanneer de **Azure Storage** dialoogvenster wordt weergegeven, wordt het nieuwe opslagaccount wordt weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="80d4d-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="80d4d-127">Selecteer het nieuwe opslagaccount in de lijst en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="80d4d-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="80d4d-128">De opslag gekoppelde service wordt weergegeven onder de **Serviceverwijzingen** knooppunt van uw project.</span><span class="sxs-lookup"><span data-stu-id="80d4d-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="80d4d-129">Hoe uw project is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="80d4d-129">How your project is modified</span></span>
<span data-ttu-id="80d4d-130">Wanneer u klaar bent met het dialoogvenster, wordt in Visual Studio verwijzingen worden toegevoegd en bepaalde configuratiebestanden wijzigt.</span><span class="sxs-lookup"><span data-stu-id="80d4d-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="80d4d-131">De specifieke wijzigingen, is afhankelijk van het type:</span><span class="sxs-lookup"><span data-stu-id="80d4d-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="80d4d-132">ASP.NET-project - [wat is er gebeurd – ASP.NET-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="80d4d-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="80d4d-133">ASP.NET Core project - [wat is er gebeurd – ASP.NET 5-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="80d4d-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="80d4d-134">Cloudserviceproject (webrollen en werkrollen) - [wat is er gebeurd – Cloud Service-projecten](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="80d4d-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="80d4d-135">Webtaak project - [wat is er gebeurd - webtaak projecten](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="80d4d-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="80d4d-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80d4d-136">Next steps</span></span>
- [<span data-ttu-id="80d4d-137">MSDN-Forum: Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="80d4d-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="80d4d-138">Blog van Microsoft Azure Storage-Team</span><span class="sxs-lookup"><span data-stu-id="80d4d-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="80d4d-139">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="80d4d-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
